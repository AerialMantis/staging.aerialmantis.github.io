---
layout: post
title:  "CppCon2017 Trip Report"
date:   2017-10-06 12:00:00 +0000
categories: events
---

Last month I flew out to Seattle with fellow Codeplayer's Michael Wong and Christopher Di Bella, and now that i've recovered from my jet lag I thought I'd give you my thoughts. This was my second time at CppCon and it was great to be back again and see a lot of familiar faces as well as a few new ones (actually quite a few new ones, there were nearly 1200 attendees this year).

Just as with last year the conference was full to the brim with great presentations, classes and evening sessions. Though this was just half of the experience, the rest came from random conversations in the hallways and out at lunch or dinner.

## Highlights

The opening keynote from Bjarne Stroustrup was set around the theme of "we are all students, and we are all teachers", and this set the tone for the rest of the conference. This was continued in the Trainers Panel, with surprise appearance of Scott Meyers.

There were so many interesting talks at the conference that I often struggled to choose what to go see (thankfully all the talks are recorded and putup on youtube). Below are few of my favourites that I woudl recommend checking out:

* Ben Deane & Jason Turner presented [Constexpr ALL the Things!][constexpr-all-the-things]. A look at the current and potentially future capabilities of constexpr, and they can be used to create a compile-time JSON parser. A great practical demonstration of the power of constexpr.
* Anthony Williams presented [Concurrency, Parallelism and Coroutines][concurreny-parallelism-coroutines]. An overview of the current parallelism and concurrency landscape. Good for either those unfamiliar with paralellism and concurrency in C++ or those looking to see what's new.
* Herb Sutter presented a keynote [Meta: Thoughts on generative C++][thoughts-on-generative-cpp]. An early look at proposed new feature for C++ that would allow developers to redefine the behaviour of a class using compiler-time code injection. This is one which really needs to be seen to be appreciated.
* Jan Babst presented [Driving Into the Future With Modern C++: A Look at Adaptive Autosar][adaptive-autosar]. A look at new standard set of guidelines for safety critical C++ in automotive with practical examples and guidance. A realling interesting insite into a rapidly developing industry and how they are adapting to C++.
* David Watson presented [C++ Exceptions and Stack Unwinding][cpp-exceptions-and-stack-unwinding]. An in-depth look at how exception handling is implemented. A great talk for anyone who's ever wondered how the magic of exception handling works.
* Chandler Caruth presented [Going Nowhere Faster][going-nowhere-fast]. Another great talk from Chandler on optimisation, this time looking at loop optimisation as well as how you can profile memory access to understand where performance is lost. Another must see for those interested in getting the most performance out of their code.
* Matt Godbolt presented the closing keynote [Unbolting thee Compiler's Lid: What Has My Compiler Done for Me Lately?][what-has-my-compiler-done-for-me]. A look back at the creation to popular compiler explorer tool and the very clever things compilers regularly do for us. A very interesting and entertaining talk, well worth checking out.

## ?

As well as enjoying the conference I was also there to present, as were my two collegues. We presented X, X, X, X and class Y. These will also be available on youtube, though I can never bring myself to watch my own presentations.

## Conclusion

To wrap up, CppCon is a great conference that is well worth attending, not just for the presentations and classes, though they are great, but also to be part of the C++ community there. I hope to be there again next year.

[cpp-samples]: https://github.com/AerialMantis/cpp_samples/tree/master/blog