---
layout: post
title:  "When and why the template & typename keywords are needed"
date:   2017-03-17 12:00:00 +0000
categories: c++
---

When working with C\+\+ templates you'll likely be familiar with the `template` and `typename` keywords in the context of template declarations, for example:

```cpp
template <typename T>
void foo(T t);
```

However, there are two other contexts where it is necessary to use the `template` and `typename` keywords, which often cause confusion at first sight. This post aims to demystify these cases, explaining when and why they are needed.

## Template Keyword
Consider the following code example:

```cpp
template <typename T>
struct foo {
  template <typename U>
  void bar() { }
};

template <typename T>
void func(foo<T> f) {
  f.bar<float>();
}
```

At first glance this code looks correct, however, when you compile this you will get an error that looks something like:

> error: expected primary-expression before 'float'

Being faced with this error message it may not be clear what the problem is. The reason for the error can actually be found in two-phase name lookup; the rule that every template is compiled in two phases, firstly for general syntax and again once any dependent names (names that depend on a template parameter) are known. More specifically, due to a grammar ambiguity in C\+\+; being that the `<` token in an expresion such as `f.bar<float>()` can be parsed either as the start of a template argument list of a call to a member function template specialisation or as a less than operator, the compiler is not able to differentiate until the type of `f` is known.

This means that in a case such as this when `f` is a dependent type; `foo<T>`, the compiler does not yet know what type `f` is, so the `.` operator is unable to lookup `bar` and the compiler treats it purely syntactically as a field of `foo<T>` so the following `<` is therefore interpreted as a less than operator. In order to instruct the compiler that this is, in fact, a call to a member function template specialisation it is necessary to add the `template` keyword immediately after the `.` operator:

```cpp
template <typename T>
struct foo {
  template <typename U>
  void bar() { }
};

template <typename T>
void func(foo<T> f) {
  f.template bar<float>();
}
```

This same rule is also applied to the pointer operator and to nested name qualifiers:

```cpp
template <typename T>
struct foo {
  template <typename U>
  void bar() { }
};

template <typename T>
void func(foo<T> *fp) {
  fp->template bar<float>();
}
```

```cpp
template <typename T>
struct foo {
  template <typename U>
  static void bar() { }
};

template <typename T>
void func() {
  foo<T>::template bar<float>();
}
```

An interesting case for this is where you have to use the `template` keyword even when it involves the this pointer:

```cpp
template <typename T>
struct foo_base {
  template <typename U>
  void base_bar() {
  }
};

template <typename T>
struct foo : public foo_base<T> {
  template <typename U>
  void bar() {
    this->template base_bar<U>();
  }
};
```

This might seem odd, but there are cases due to inheritance where the full type of the this pointer cannot be known until the class template is specialised, such as when the type inherits from another class template.

For those interested in the C\+\+ standardese, the section which describes this rule is as follows:

> *$14.2/4:*
**When the name of a member template specialization appears after . or -> in a postfix-expression, or after nested-name-specifier in a qualified-id, and the postfix-expression or qualified-id explicitly depends on a template-parameter (14.6.2), the member template name must be prefixed by the keyword template. Otherwise the name is assumed to name a non-template.**

## Typename Keyword

Take another code example:

```cpp
template <typename T>
struct type_or_value;

template <>
struct type_or_value<int> {
  static const bool tv = true;
};

template <>
struct type_or_value<float> {
  using tv = float;
};

template <typename T>
void func() {
  using t = type_or_value<T>::tv;
  bool v = type_or_value<T>::tv;
}
```

If you were to compile this code as it is, you would get an error for the line `using t = type_or_value<T>::tv;` something like:

> error: need 'typename' before 'type_or_value<T>::tv' because 'type_or_value<T>' is a dependent scope

This error is better than the previous one as it tells you what to do, essentially add the `typename` keyword immediately before the expression. But why is this necessary? Again the reason for this can be found in the two-phase name lookup.

When the compiler parses code like this involving a dependant type, in this case, `type_or_value<T>` it cannot know whether the member `tv` resolves to a type or a non-type. Therefore the compiler will assume non-type and it assumes the latter. In order to instruct the compiler that `tv` is, in fact, resolves to a type it is necessary to add the `typename` keyword immediately before the expression:


```cpp
template <typename T>
struct type_or_value;

template <>
struct type_or_value<int> {
  static const bool tv = true;
};

template <>
struct type_or_value<float> {
  using tv = float;
};

template <typename T>
void func() {
  using t = typename type_or_value<T>::tv;
  bool v = type_or_value<T>::tv;
}
```

However now that this keyword is there the compiler assumes that the expression will always resolve to a type, so if a later instantiation were to not conform to this, the compiler would through an error. For example:

```cpp
int main () {
  func<int>(f);
}
```

This would result in an error like:

> error: no type named 'tv' in 'struct type_or_value<int>'

The `typename` keyword is not only needed in this case but every where an unknown member exists in a context where either a type or a non-type is valid. For example:

```cpp
template <typename T>
struct type_or_value;

template <>
struct type_or_value<int> {
  static const bool tv = true;
};

template <>
struct type_or_value<float> {
  using tv = float;
};

template <typename T>
struct foo {
};

template <typename T>
void func() {
  foo<typename type_or_value<T>::tv> f;
}
```