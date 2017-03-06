If you are have become familiar with writing and using C\+\+ templates you will likely be familiar with the `template` and `typename` keywords in the context of a template declaration, for example:

```cpp
template <typename T>
void foo(T t);
```

However there are two additional contexts in which it is nessesary to use the `template` and `typename` keywords, which often cause confusion at first sight. This post aims to demistify these cases, explaining when and why tey are nessesary.

### Template Keyword
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

At first glance this code looks correct, however when you compile this you will get an error that looks something like:

```
error: expected primary-expression before 'float'
```

Being faced with this error message it may not be clear what the problem is. The reason for this can be found in the two-phase name lookup; the rule that every template is compiled in two phases, firstly for general syntax and again once any depedant names are know.

In this example the function template `func` is compiled first for syntactical correctness without requiring the typename `T` and then again once the typename `T` is known. However due to a grammer ambiguity in C\+\+; being that the `<` keyword can be parsed in one of two ways, depending on the context. Either as the opening template brace of a call to a member function template specialisation or as a less than operator on the right hand side of a non-template.

Since `foo<T>` is dependant on the type `T` the compiler is unable to infer which context this is and asumed the latter. Therefore in order to instruct the compiler that this is in fact a call to a member function template specialisation it is nessesary to add an additional `template` keyword directly after the `.`:

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

This same rule also applied to the pointer operator and to nested name qualifiers:

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

For those interested in the C++ standardese, the section which describes this rule is as follows:

> *$14.2/4:*
*When the name of a member template specialization appears after . or -> in a postfix-expression, or after nested-name-specifier in a qualified-id, and the postfix-expression or qualified-id explicitly depends on a template-parameter (14.6.2), the member template name must be prefixed by the keyword template. Otherwise the name is assumed to name a non-template.*

### Typename Keyword

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
void func(foo<T> f) {
  using t = type_or_value<T>::tv;
  bool v = type_or_value<T>::tv;
}
```

If you were to compile this code as it is, you would get an error for ` using t = type_or_value<T>::tv;` something like:

```
error: need 'typename' before 'type_or_value<T>::tv' because 'type_or_value<T>' is a dependent scope
```

This error is better than the previous one as it tells you what to do, essentialy add a typename on the right hand side of the assignment. But why is this nessesary? Again the reason for this can be found in the two-phase name lookup.

During the first phase `type_or_value<T>::tv` is dependant on the type `T`, which means that the compiler cannot know whether that expression resolved to a type or a type or a non-type. Therefore the compiler will asume non-type, requring the additional `typename` keyword to instruct the compiler that this should resolve to a type:

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
void func(foo<T> f) {
  using t = typename type_or_value<T>::tv;
  bool v = type_or_value<T>::tv;
}
```

However now that this keyword is there the compiler asumes that expression to always resolve to a type, so if a later instantiation were to not conform to this, the compiler would through an error. For example:

```cpp
int main () {

  foo<int> f;s
  func(f);

}
```

This would result in an error like:

```
error: no type named 'tv' in 'struct type_or_value<int>'
```

+ Add standardese

+ Next blog post class template vs template class

+ It can be tempting to just nsert these keyword everywhere, but thi is not recommended.

+ research: http://stackoverflow.com/questions/610245/where-and-why-do-i-have-to-put-the-template-and-typename-keywords
