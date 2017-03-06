---
layout: post
title:  "Introduction to Templates"
date:   2015-09-19 12:00:00 +0000
categories: c++
---

C\+\+ template programming is difficult, the instantiation process is complex and template code can often be difficult to debug and sometimes even read. However it can also be extremely powerful for creating generic code that can dramatically reduce duplication and improve the runtime performance of your application.

When I was learning templates I found many concepts difficult to grasp, however I understood them better after spending some time looking at templates from the perspective of the compiler. This lead me to write a series of blog posts; providing a bottom up approach to template programming, starting with an introduction to instantiation. In this post I aim to introduce C\+\+ templates and describe a simple example of template instantiation in order to provide a foundation for later posts covering more advanced features.

## What are Templates

This may seam very trivial, however one of the biggest problems that many; myself included, encounter when starting out with C\+\+ templates stems from understanding what a template is and therefore understanding how to approach them. A template is not a class or a function in itself, it’s a generic blueprint with a list of parameters that defines a group of types or a group of functions. This means that no code is generated from a template alone, it must first be instantiated with suitable template arguments to create an actual class or function.

This instantiation is performed at compile time, allowing you to make use of several useful techniques involving compile time evaluation of template expressions, this is what’s known as template meta programming.

There are five different kinds of template that can be defined in C\+\+: class templates, function and member function templates, alias templates (from C\+\+11 onwards) and variable templates (from C\+\+14 onwards).

{% highlight cpp %}
/* Class template. */
template <typename T> class my_class;

/* Function template. */
template <typename T> void foo(T param);

/* Member function template. */
class my_class { template <typename T> void foo(T param); }

/* Template alias (C\+\+11). */
template <typename T> using alias = typename T::type;

/* Variable template (C\+\+14). */
template <typename T> T var = T(5);
{% endhighlight cpp %}

Additionally there are three different kinds of template parameters that a template can be parameterized with: type parameters (this is specified by the typename or class keyword), non-type parameters (this can be specified by any integral types including bool and c-strings and also references and pointers, and template parameters (this is specified by the template keyword).

{% highlight cpp %}
/* Type template parameter. */
template <typename T> void typename_param();

/* Integral non-type template parameter. */
template <int T> void integral_param();

/* Enum class non-type template parameter. */
template <enum_class T> void enum_class_param();

/* Const char array non-type parameter. */
template <const char* T> void string_param();

/* Template template parameter. */
template <template <typename T> typename T> void template_param();
{% endhighlight cpp %}

It is also possible to define variadic template parameters, which are an unspecified sized pack of parameters of a specific kind, this is specified in the same way as before but with the ellipses syntax.

{% highlight cpp %}
/* Variadic typename parameter pack. */
template <typename TN...> void variadic_param();
{% endhighlight cpp %}

It’s important to note here the terminology for template parameters and arguments: parameters are the generic types and integrals that are associated with a template declaration as seen above and arguments are the non-generic types and integrals that are provided in order to instantiate the template.

## Template Instantiation

Instantiation is the core concept of C\+\+ templates; it is the mechanism by which a class or function is created from it’s respective template.

The general template instantiation model is the same for any template, however there are different forms of instantiation and there are some special rules and exceptions surrounding specific kinds of templates.

As a simple example consider this function template that defines a generic group of functions that take two reference parameters of the template argument type 'T' and swaps their values:

{% highlight cpp %}
template <typename T>
void swap(T &a, T &b) {
  T tmp = a;
  a = b;
  b = tmp;
}
{% endhighlight cpp %}

As the function template swap itself is simply a parametrized blueprint, it does not generate any code on it’s own. In order to generate a function from the template, it must be instantiated. The template instantiation process can be triggered in two ways: it can be triggered implicitly; whenever a template declaration is referenced in a context where a definition is required, or explicitly; when an explicit template instantiation directive is used.

A call to the function template `swap` is made with two function parameters of type `int`, triggering implicit instantiation of the template:

{% highlight cpp %}
int main() {
  int a = 2, b = 5;
  swap(a, b);
}
{% endhighlight cpp %}

Before the template can be instantiated, it must first be specialized; this is the process by which each parameter of a template declaration is substituted with a template argument to construct a non-generic template specialization. For both implicit and explicit instantiation, this process is performed as an implicit pre-requisite, however the specialization process can also be triggered explicitly; when an explicit template specialization directive is used.

As the function template swap is called with two `int` parameters, the typename argument `T` is deduced as type `int` and therefore the function parameters `T&` are substituted with `int&`:

{% highlight cpp %}
/* Function template. */
template <typename T>         ->      /* Function template specialization. */
void swap(T &a, T &b);                int swap(int &a, int &b);
{% endhighlight cpp %}

Once the template specialization has been constructed the function definition can be instantiated; this is the process by which a template specialization is used to compile it’s associated template definition, substituting in the template arguments from the template specialization creating an instantiated function definition.

Once the template specialization for the function template swap has been constructed, the function definition is then compiled, substituting any use of the typename `T` with `int`:

{% highlight cpp %}
/* Function template. */
template <typename T>         ->    /* Function template instantiation. */
void swap(T &a, T &b) {             void swap(int &a, int &b) {
  T tmp = a;                          int tmp = a;
  a = b;                              a = b;
  b = tmp;                            b = tmp;
} 
{% endhighlight cpp %}

My [next post][template-instantiation] will look at the implicit instantiation process seen here in further detail.

[cpp-samples]: https://github.com/AerialMantis/cpp_samples/tree/master/blog
[template-instantiation]: http://www.aerialmantis.co.uk/blog/2015/11/22/template-instantiation/