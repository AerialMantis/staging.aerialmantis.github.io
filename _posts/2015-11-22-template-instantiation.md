---
layout: post
title:  "Template Instantiation"
date:   2015-11-22 12:00:00 +0000
categories: c++
---

Have you ever encountered strange cryptic errors messages involving deduction or substitution failures in your C\+\+ templates and had a really tough time debugging them? This is a very common problem and probably the biggest that templates suffer from, the template instantiation process is very complex and contains various stages at which errors can occur. In my previous post I gave a brief example of template instantiation, in this post I break down the stages of the template instantiation process and explain what is happening under the hood.

If you're still new to C\+\+ templates you may want to check out my [previous post][introduction-to-templates] on an introduction to templates.

## Template Instantiation

A template declaration and it’s associated definition do not generate any code on their own, they defines a generic parameterized group of functions, member functions, classes, aliases or variables, from which an instance can be constructed.

When a template declaration is referenced in a context which requires an instance of that group, a non-generic declaration is constructed with a particular set of arguments. This process is often broadly referred to as ‘template instantiation’, however there are multiple stages involved and understanding these stages can be invaluable when writing and particularly debugging template code:

![alt text](https://github.com/AerialMantis/aerialmantis.github.io/raw/master/images/template-instantiation.png "Game Jam 2015"){:width="100%"}

During this process the template declaration being instantiated can either be a regular template declaration, referred to as the primary template, or an explicit template specialization. During this process the resulting non-generic instance is represented by it’s template id, that in broadest terms is treated by the compiler as a regular non-template declaration.

{% highlight cpp %}
/* Function template declaration. */   
template <typename T>                 ->  /* Instantiated template id. */
T add(T a, T b) { return a + b; }         int add<int>(int a, int b) { return a + b; }
{% endhighlight cpp %}

## Name Lookup

When the compiler parses a name the first thing it must do is associate it with the declaration that introduced it; this process is known as name lookup.

This is where one of the first differences between types of template occurs. Name lookup for non-function templates such as a class, alias or variable template, must produce a single declaration, where as name lookup for function and member function templates can produce multiple declarations which are all instantiated and later passed to overload or specialization resolution where a single template id must be chosen.

There are two kinds of name lookup; qualified and unqualified. A qualified name lookup is performed when the name has an explicit namespace or class qualifier preceding it and will be limited to that specified scope and an unqualified name lookup is performed when the name does not and will look in multiple contexts. For example:


{% highlight cpp %}
/* Qualified name lookup. */
bar::function<int>();
 
/* Unqualified name lookup. */
function<int>();
{% endhighlight cpp %}

Name lookup is not explicitly part of the instantiation process, however there are some aspects of it that can directly effect the way in which instantiation is triggered, therefore it is important to mention.

One of these is two-phase lookup; the principle that a C\+\+ compiler will compile your source code in two phases. In the first phase, all code is parsed and checked for general syntax, however only non-dependent names are compiled fully. In the second phase, dependent names are re-compiled once the template parameters those names depend on have been substituted.

A dependent name is one one that contains a non-substituted template parameter from a surrounding scope, such as a function or class template parameter.

As a simple example, consider the following function template:

{% highlight cpp %}
template <typename T>
void bar(T var) {
  /* The lookup for the first call is done in phase
  one as it does not contain any dependent
  types. */
  foo(10);
 
  /* The lookup for the second call is deferred to
  phase two as it contains the dependent
  type 'T' in its argument 'var'. */
  foo(var);
}
{% endhighlight cpp %}

The first function call takes as its argument, the integer literal `10`, as this argument is non-dependent, the lookup can be performed immediately in the first phase. The second function call takes as it’s argument the function parameter `var`, as this argument is dependent on the template parameter `T`, the lookup must be deferred to the second phase, once the function template function ‘bar’ has been instantiated and `T` has been substituted.

It is worth noting however, that not all C\+\+ compilers implement two-phase lookup fully, some still adopt an early implementation method in which entire template definitions are deferred to the second phase, which can sometimes lead to invalid C\+\+ code being accepted by the compiler, and therefore causing trouble for cross platform applications.

## Argument Deduction and Substitution

For each template declaration returned by the name lookup, the compiler will construct a template id, with a specific set of template arguments. To do this, a template argument is determined and substituted into the template id for each template parameter of the template declaration.

There are three different ways in which template arguments can be determined, which influence how the arguments are substituted into the template id; they can be specified explicitly, they can be deduced from default template arguments and in the case of function and member function templates they can be deduced from the types of the function call arguments. The argument deduction and substitution is done in this order:

* Substitution of explicit template arguments
* Deduction of non-explicit template arguments
* Substitution of non-explicit template arguments

## Substitution of Explicit Template Arguments

Template arguments that are specified explicitly are substituted into the template id first before non-explicit template arguments are deduced. Additionally explicitly specified template arguments are always substituted from left to right. For example:

{% highlight cpp %}
template <typename T>
void function() {
  /* do something. */
}
 
int main () {
  /* Typename 'T' is explicitly specified as
  'float'. */
  function<float>();
}
{% endhighlight cpp %}

Here the template parameter `T` is determined from the explicit template explicit argument `float`.

## Deduction of Non-Explicit Template Arguments

After explicit template arguments are substituted, the compiler will attempt to determine template arguments for the rest of the templates parameters. First, if the template is a function or member function template, it will then attempt to deduce each template argument from the types of the function parameters. For example:

{% highlight cpp %}
template <typename T>
void function(T var) {
  /* do something. */
}
 
int main () {
  /* Typename 'T' is deduced by the function
  parameter 'false' as 'bool'. */
  function(false);
}
{% endhighlight cpp %}

Here the template argument `T` is determined from the function parameter `false`.

Next the compiler will attempt to deduce each template argument from from a default argument if one is available. For example:

{% highlight cpp %}
template <typename T = int>
void function() {
  /* do something. */
}
 
int main () {
  /* Typename 'T' is deduced by the default argument
  as 'int'. */
  function();
}
{% endhighlight cpp %}

Here the template argument `T` is determined from a default argument as `int`.

Note that unlike default function arguments, default template arguments do not have to be at the end of the parameter list.

## Substitution of Non-Explicit Template Arguments

Once the compiler has successfully determined the non-explicit template arguments, it attempts to substitute those arguments into each corresponding template parameter of the template id.

This is where the [substitution failure is not an error][sfinae] (SFINAE) principle is applied. SFINAE states that if a template id is ill formed as a result of a template argument substitution, then rather than triggering a error, the template id candidate is simply dropped and not considered for overload or specialisation resolution.

## Specialization

Once a valid template id declaration has been constructed with substituted template arguments, it is then added to the list of specializations for that template declaration, provided that template id declaration has not been added already.

The specialization process is generally triggered in this way, as an implicit pre-requisite to instantiation, however it can be triggered explicitly when an explicit template specialization directive is encountered.

## Instantiation

Finally if the template declaration was referenced in a context which requires a definition and the template id has not previously been instantiation then the compiler will instantiate it, constructing a definition for the template id.

If the definition of the template being instantiated is not available at this point, for function or member function templates the instantiating of the definition is then deferred until the template definition appears in the translation unit, for class, alias or variable templates the compiler will trigger a error.

To do this he compiler will substitute all uses of the template declaration’s parameters within the associated definition, with the arguments of the template id, to construct a definition for the template id.

For example, consider a function template with three template parameters typename `S`, typename `T` and int `D` that defines a group of functions that take a parameter of type `T`, construct a pointer of type `S`, passing the parameter and the value of `D` to the constructor and then returning the pointer:

{% highlight cpp %}
template <typename S, typename T, int D = 5>
S *create(T param) {
  S *s = new S(param, D);
  return s;
}
 
struct foo { foo(float, int) { /* do something. */ } };
 
int main() {
  /* The create function body is instantiated to
  create an instance of foo with a float parameter
  and return that instance by value. */
  auto f = create<foo>(10.0f);
}
{% endhighlight cpp %}

When the function template is specialized a template id is constructed where, typename `S` is specified explicitly as the type `foo`, typename `T` is deduced as the type 'float' form the argument `10.0f` and int `D` is deduced from the default argument as `5`.

Now when the function template definition is instantiated all uses of the templates parameters within the definition are substituted with the associated arguments from the template id.

{% highlight cpp %}
foo *create(float param) {
  /* S is substituted with 'foo' and D is
  substituted with '5'. */
  foo *s = new foo(param, 5);
  return s;
}
{% endhighlight cpp %}

Once the instantiation process is done the template id has a valid declaration and definition and is then inserted into the generated code. It is important to note here that at this point the template id must conform to the [one definition rule][odr] (ODR).

## Overload or Specialization Resolution

After argument deduction and substitution, specialization and instantiation has been performed for each template declaration returned by name lookup the compiler then performs overload or specialization resolution. This is the process by which the compiler chooses the best candidate from the function or member function overloads or from the class, alias or variable specializations and if no candidate can be chosen the compiler triggers an ambiguity error.

[introduction-to-templates]: http://www.aerialmantis.co.uk/blog/2015/09/19/introduction-to-templates/
[cpp-samples]: https://github.com/AerialMantis/cpp_samples/tree/master/blog
[sfinae]: http://en.cppreference.com/w/cpp/language/sfinae
[odr]: http://en.cppreference.com/w/cpp/language/definition