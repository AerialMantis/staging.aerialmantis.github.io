---
layout: post
title:  "Introduction to Template Meta Programming"
date:   2017-05-01 12:00:00 +0000
categories: c++
---

One of the most powerful techniques that C++ templates provide is the ability to perform compile-time computations in order to create more generic and optimised code; this is known as template meta programming (TMP).

In this post I describe the basic principles behind template meta programming and provide some examples of how it can be used.

## What is Template Meta Programming?

TMP can be seen as an embedded language sitting a layer above standard C++, that is interpreted by a C++ compiler's type system, in particular the template system and outputting standard C++ code which is then compiled as normal. It allows you to perform general purpose computations with types, templates, functions, constant variables and literals as the objects, it is entirely functional and therefore immutable and stateless (with some exceptions).

## How Does it Work?

So now that you have a definition; you’re probably wondering how it actually works? As described in a previous post; a C\+\+ template does not define a function, class or variable in itself, it must be instantiated with suitable template arguments first, and it is this process of instantiation that can be used to provide compile-time equivalents of many general purpose computational concepts.

Before diving into compile-time computations, it's important to first look at variables; the fundamental components of any computation. While runtime computations are performed on dynamic variables such as integrals, pointers and references, compile-time computations are performed on types, templates, functions, constant variables, literals and (including those produced by constexpr functions); essentially anything that can be used as a template argument. So the compile-time equivalent of a variable is any value or type that is known at compile-time, for example:

{% highlight cpp %}
/* runtime variables. */
char c = 'a';
int *p = new int(5);

/* compile-time variables. */
const int n = 3;
typedef float t;
{% endhighlight cpp %}

Here the variables 'i' and 'p' are dynamic runtime variables that can be assigned any value during the execution of the program and the variables 'n' and 't' are compile-time variables that can only be assigned once during compilation and are immutable during the execution of the program.

Now as an example of how TMP can be used i'll walk through how the runtime concept of a function can be mapped to a compile-time computation using TMP. Consider the following function:

{% highlight cpp %}
/* runtime function taking two integer parameters. */
int add(int a, int b) {
    /* returns the sum of the two parameters. */
    return a + b;
}
{% endhighlight cpp %}

The function `add` is compiled once and generates code that can be called multiple times with different values, resulting in different return values during the execution of the program, for example:

{% highlight cpp %}
int main() {
    int a = 3, b = 5, c = 7;

    int r1 = add(a, b);
    int r2 = add(a, c);
}
{% endhighlight cpp %}

You can map the concept of a function to a compile-time computation using class template instantiation, where: the class template body is the function body, the template parameters are the function parameters, an anonymous enum is the return value and the act of instantiating the template is the execution of the function:

{% highlight cpp %}
/* compile-time function taking integer parameters. */
template <int a, int b>
struct add {
    /* instantiate the sum of the two template parameters at compile-time. */
    enum { value = (a + b) };
};
{% endhighlight cpp %}

The struct template `add` is compiled for each unique instantiation of the template generating a unique type each time. The evaluation of the enumerator 'value' during instantiation of the struct performs the exact same computation as the runtime function shown above, only this computation is performed during instantiation and therefore entirely at compile-time.

The anonymous enum could be replaced with a static const int, however by using an anonymous enum the computation happens entirely in the type system of the compiler so there is not storage required for the value.

The arguments can be any valid template arguments provided at compile-time and the arguments and return value of each instantiation are immutable once compiled, for example:

{% highlight cpp %}
const int a = 3, b = 5, c = 7;

const int r1 = add<a, b>::value;
const int r2 = add<a, c>::value;
{% endhighlight cpp %}

As mentioned earlier TMP allows you to construct compile-time computations that act on types as well as constant variables and literals, for example:

{% highlight cpp %}
/* compile-time function taking a type. */
template <typename t>
struct as_ptr {
    /* returns a pointer type. */
    typedef t *type;
};
{% endhighlight cpp %}

{% highlight cpp %}
typedef int a;
typedef float b;

typedef as_ptr<a>::type r1;
typedef as_ptr<b>::type r2;
{% endhighlight cpp %}

This can also be taken further by creating compile-time functions that can define mappings between constant variables, types and functions.

## Modern C\+\+ TMP Constructs

C\+\+11 and C\+\+14 introduced new features that help to make these TMP techniques first class features of the C\+\= language.

Firstly C\+\+11 introduced alias templates. An alias is a replacement for the typedef, and an alias template is new type of template which instantiates aliases. The example involving the struct `as_ptr` from earlier re-written using alias templates would look something like:

{% highlight cpp %}
/* compile-time function taking a type. */
template <typename t>
struct as_ptr {
    /* returns a pointer type. */
    using type = t *;
};
{% endhighlight cpp %}

{% highlight cpp %}
using a = int;
using b = float;

using r1 = as_ptr<a>::type;
using r2 = as_ptr<b>::type;
{% endhighlight cpp %}

Secondly C\+\+14 introduced variable templates. A variable template is a template which instantiates variables. The example involving the struct `add` from earlier re-written using a variable template would look something like:

{% highlight cpp %}
/* compile-time function taking integer parameters. */
template <int a, int b>
int add = (a + b);
{% endhighlight cpp %}

{% highlight cpp %}
const int a = 3, b = 5, c = 7;

const int r1 = add<a, b>;
const int r2 = add<a, c>;
{% endhighlight cpp %}

## Constexpr

C\+\+11 also introduced constexpr; which provides another way to describe compile time computations. The constexpr keyword can be used to annotate variables and functions as constant expressions. This allows compile-time computations be describe with standard C\+\+ function syntax, the example involving the struct `add` from earlier re-written using constexpr would look something like:

{% highlight cpp %}
/* compile-time function taking integer parameters. */
constexpr int add(const int a, const int b) {
  return a + b;
}
{% endhighlight cpp %}

{% highlight cpp %}
const int a = 3, b = 5, c = 7;

const int r1 = add(a, b);
const int r2 = add(a, c);
{% endhighlight cpp %}

Type based TMP however cannot be performed using constexpr, only value based TMP.

## Pros and Cons

There are many great benefits of TMP, however it can be a double ended sword in that there are also many problems that can arise from its misuse.

The major benefits of TMP are that it allows you to create generic code that can massively reduce the size of your source and in some cases solve problems that would be almost unsolvable otherwise. TMP also allows the compiler to generate highly optimised code, for example in the compile-time function described earlier, the value is defined as an (anonymous) enum class which means it's expressed entirely in the type system of the compiler and therefore doesn't require any storage within the compiled program enabling the compiler to directly use compile-time values which can lead to further optimizations and more efficient code generation.

There can also be major disadvantages of TMP, the obvious caveat being it's limitation that everything must be known at compile-time. As TMP is based upon template instantiation and every compile-time computation triggers template instantiation, over-use can dramatically increase compile times and potentially the size of you application's binary. Additionally TMP can very easily become overly complex and therefore making it difficult for others (including yourself at a later date) to understand how it works. TMP can also be notoriously difficult to debug, as I'm sure anyone who has encountered errors deep within the STL will be familiar with.

It's all about finding the right balance between generality and complexity, sometimes TMP is the perfect tool for a job, and a powerful one at that, but it is by no means a one-size-fits-all solution and over complicating code with needless templates is a very easy trap to fall into.

## Applications

There are many useful applications of TMP such as type traits, SFINAE, generic programming, embedded DSLs and complex compile-time computations.

One of the most common uses of TMP is to construct what's known as type traits. Type traits are small snippets of TMP that are used to provide information on a type or value, such as determining if a type is an integral or standard layout. The C++ STL now provides a wide range of type traits in the standard for just this purpose.

Another is SFINAE (substitution failure is not an error), which is a feature of C++ that is used to determine the availability of a function overload or class specialisation at compile-time based on TMP.

TMP is also often used for generic programming, in which you define functions or classes which have multiple small segments of specialised template code that is chosen via TMP.

Embedded DSLs (domain specific languages) also heavily make use of TMP. C++ embedded DSLs use TMP to construct entire expressions of compile-time computations as compile-time types in order to execute them in a certain context or perform transformations on them.

Finally sometimes, particularly on low latency platforms, it's important to perform multiple complex computations at compile-time, in order to save on runtime performance, so by using TMP you can determine those results at compile-time.

It is also possible to use TMP to construct containers capable of mutable state, however this involves a complex trick that is generally considered a misuse of C++ template instantiation, therefore although this can be an interesting exercise it is not advise-able for production code.

## Conclusion

Here I demonstrated an example of how TMP can be used to construct compile-time computations by creating the compile-time equivalent of a function. Though this is just the tip of the iceberg, TMP can be used to create much larger and more complex compile-time computations involving compile-time if statements, for loops, while loops, containers and even algorithms.