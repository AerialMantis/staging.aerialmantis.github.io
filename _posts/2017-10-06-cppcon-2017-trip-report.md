---
layout: post
title:  "CppCon2017 Trip Report"
date:   2017-10-06 12:00:00 +0000
categories: events
---

Last month I flew out to Seattle for CppCon 2017 with fellow Codeplayer's Michael Wong and Christopher Di Bella. This was my second time at CppCon and as with the previous year it was a real pleasure to be there, I saw a lot of familiar faces and digested a lot of great content.

My trip report is a little later than I had hoped because I wanted to wait until the talks were available online before posting.

## Highlights

CppCon this year was bigger than ever with 7 tracks, making it even harder to pick which talks to go to, and approaching 1200 attendees. Thankfully all the talks are made available online you if you couldn't make it or even if you did but couldn't get to see all the talks you wanted to, you can go back and watch them back. I only got to a handful of the talks as I often had conflicting appointments, but I've highlighted a few from what I saw that I would recommend checking out and some which I didn't make it to but heard good things about.

* The opening keynote from Bjarne Stroustrup [Learning and Teaching Modern C++][learning-and-teaching-modern-cpp] was set around the theme of "we are all students, and we are all teachers", and this set the tone for much of the rest of the conference. This was continued in the Trainers Panel, with a surprise appearance of Scott Meyers.
* Ben Deane & Jason Turner presented [Constexpr ALL the Things!][constexpr-all-the-things]. A look at the current, and potentially future capabilities of constexpr, and how they can be used to create a compile-time JSON parser. A great practical demonstration of the power of constexpr and a very enjoyable presentation.
* Anthony Williams presented [Concurrency, Parallelism and Coroutines][concurreny-parallelism-coroutines]. An overview of the current parallelism and concurrency landscape. Good for either those unfamiliar with parallelism and concurrency in C\+\+ and interested in what it's all about or for those already familiar and looking to see what's new.
* Herb Sutter presented a keynote [Meta: Thoughts on generative C++][thoughts-on-generative-cpp]. An early look at proposed new feature for C\+\+ that would allow developers to redefine the behavior of a class using compiler-time code injection. This was a great and thought-provoking presentation which I could not do justice here so it really needs to be seen to be appreciated.
* Jan Babst presented [Driving Into the Future With Modern C++: A Look at Adaptive Autosar][adaptive-autosar]. A look at new standardization of guidelines for safety-critical C\+\+ in automotive with practical examples and guidance. A really interesting insight into a rapidly developing industry and how they are adapting to C\+\+.
* David Watson presented [C++ Exceptions and Stack Unwinding][cpp-exceptions-and-stack-unwinding]. An in-depth look at how exception handling is implemented. A great talk for anyone who's ever wondered how the magic of exception handling works.
* Chandler Caruth presented [Going Nowhere Faster][going-nowhere-fast]. Another great talk from Chandler on optimisation, this time looking at loop optimisation as well as how you can profile memory access to understand where performance is lost. Another must see for those interested in getting the most performance out of their code.
* Matt Godbolt presented the closing keynote [Unbolting the Compiler's Lid: What Has My Compiler Done for Me Lately?][what-has-my-compiler-done-for-me]. A look back at the creation of the popular compiler explorer tool and the very clever things compilers regularly do for us. A very interesting and entertaining talk, well worth checking out.
* Sara Chipps presented [Building for the Best of Us: Design and Development with Kids in Mind][building-for-the-best-of-us] presented programmable friendship braceltes for pre-teen girls called [Jewel Bots][jewel-bots], and how to design a more accessible C\+\+ API for a younger demographic. It was a very intertaining presentation with some users of the Jewel Bots as guest speakers, presenting what they had done on the devices.

## Our Presentations

As well as enjoying the conference I was also there to present myself along with my two colleagues. My work is in parallelism and heterogeneity in C\+\+, which I was happy to see is a growing area of interest at CppCon.

* I presented [Designing a Unified Interface for Execution][unified-interface-for-execution], a look at the current proposal for executors.
* Michael presented [The landscape of parallel programming models: is it still hard or just OK?][parallel-programming-models] with Paul McKenney and Maged Michael, an analysis of existing programming models for parallel programming models and what the future of parallel programming in C+ looks like.
* Michael and I presented [C++17 ParallelSTL: A Standardization Experience Report for CPU and GPU on SYCL][parallelstl-standardization-report], a look back at the standardization process of ParallelSTL and how Codeplay implemented ParallelSTL to accelerate the parallel algorithms on GPUs with a live demo.
* Christopher presented Learning C\+\+ Isn't Difficult - Teaching C\+\+ Is The Trick, an open discussion session on best practices for teaching C\+\+ and ran a class on Exploring the C\+\+ Standard Library.

## Getting the Most out of CppCon

For anyone considering attending a later CppCon, I thought I'd give some pointers why you should go and how to get the best out of it.

You might think that since the talks are made available online there's not much point in going to the conference itself. But the talks are just the tip of the iceberg at CppCon. There is a great deal of content that is not made available online such as classes, open content and the poster session, and this is not to mention the benefit of simply being at the conference amongst a welcoming community of C\+\+ developers.

The classes are of a very high quality; last year I went to Anthony Williams' class on concurrency in C\+\+ and this year I went to Stephen Dewhurst's class on template programming, and each time I learnt a great deal which I was able to take back not just for myself but also for my company.

Simply being at the conference itself provides so many opportunities to meet people and develop yourself, your company or contribute to the community. At the conference, you have direct access to fellow developers, potential customers or partners, library developers and committee members.  This year I spent every lunch and evening after the conference meeting people and I still never found time to see everyone I'd have liked to.

One aspect of CppCon I would highlight, and this is true for many conferences but I feel more so of CppCon is that there is an overwhelming amount of content. I found myself on many occasions struggling to decide what to go to because every option was interesting. So it helps greatly to have an idea of what you want to see in advance.

For any content which is not recorded such as open sessions, classes or posters, make sure to take notes and/or request slides or learning resources to take back with you as you may forget things soon after the conference, there's only so much information your brain can hold.

## Conclusion

To wrap up, CppCon is a great conference that is well worth attending, not just for the talks and classes, though they are great, but also to be part of the C\+\+ community there. I hope to be there again next year.

[cpp-con-youtube]: https://www.youtube.com/channel/UCMlGfpWw-RUdWX_JbLCukXg
[learning-and-teaching-modern-cpp]: https://www.youtube.com/watch?v=fX2W3nNjJIo
[constexpr-all-the-things]: https://www.youtube.com/watch?v=PJwd4JLYJJY
[concurreny-parallelism-coroutines]: https://www.youtube.com/watch?v=JvHZ_OECOFU
[thoughts-on-generative-cpp]: https://www.youtube.com/watch?v=4AfRAVcThyA
[adaptive-autosar]: https://www.youtube.com/watch?v=YzyGgZ_RClw
[cpp-exceptions-and-stack-unwinding]: https://www.youtube.com/watch?v=_Ivd3qzgT7U
[going-nowhere-fast]: https://www.youtube.com/watch?v=2EWejmkKlxs
[what-has-my-compiler-done-for-me]: https://www.youtube.com/watch?v=bSkpMdDe4g4
[unified-interface-for-execution]: https://www.youtube.com/watch?v=wr4YBDS-0Tc
[parallel-programming-models-p1]: https://www.youtube.com/watch?v=YM8Xy6oKVQg
[parallel-programming-models-p2]: https://www.youtube.com/watch?v=74QjNwYAJ7M
[parallelstl-standardization-report]: https://www.youtube.com/watch?v=RoUYiHTsEFE
[building-for-the-best-of-us]: https://www.youtube.com/watch?v=zX0YoCDWGxc
[jewel-bots]: https://jewelbots.com/