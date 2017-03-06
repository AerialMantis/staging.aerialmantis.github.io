---
layout: post
title:  "Get the Frack out of the Way!"
date:   2017-02-27 12:00:00 +0000
categories: events
---

It was January again which meant it was time for our yearly trip to Glasgow Caledonia University for the Global Game Jam.  This year we left after the 48-hour game dev crunch with a game called ['Frack the Planet'][frack-the-planet].

![alt text](https://github.com/AerialMantis/aerialmantis.github.io/raw/master/images/gg17-compilation-1.jpg "Game Jam 2017"){:width="100%"}

The [Global Game Jam][global-game-jam] is a yearly event held in many different locations all over the world where game dev enthusiasts come together in teams in order to make a game in 48 hours under a common theme. The games that are created during the jam are generally video games but it does also see other kinds of games like board games, card games and social media games as well. The experience of a game jam is probably best described as the full game development process; including game design, content creation and crunch time, condensed into 48 hours.

## What the Frack?

This year I learnt my lesson and I took the Friday and Monday surrounding the game jam off work, this meant I could get a long rest before hand. Despite this we didn't arrive as early as we have in the past, though we were still able to find a good spot, setting up camp in a booth with white boards.

Unfortunately one of our regular teammates Aaron was unable to make it this year, Aaron was very ill leading up to the jam and had to stay at home. However he was still with us in spirit, kindly preparing all of the infrastructures we took with us and all helping us brainstorm ideas over chat as well as helping make improvements to the game after the jam was over.

We got everything set up just in time to attend the keynote and find out the theme for this year's jam, which turned out to be 'waves'. With that, we got to work brainstorming ideas, and this year we had the opposite problem from last year in that we had too many ideas. Some of the ideas we thought of included waving a someone in a crown, matching patterns on an oscillograph, trying to build sand castles on the beach without them being destroyed by waves, throwing balls into a pool of water to create waves and a puzzle game based on the particle wave duality. However, in the end, we settled on a game about fracking, where players would use seismic waves to detect gas pockets for drilling. Admittedly the biggest contributing factor to this choice may have been that we were able to call our game 'Frack the Planet'.

Technology wise we quickly decided to use [Love2D][love-2d] again, we had a good experience working with it last year and we had a good experience with it again this year. Love2D is a 2d game engine with a Lua scripting language, it's very simple and easy to pick up with good documentation.

My task this year was to write the shaders for rendering the seismic waves and transforming the world into polar coordinates allowing the player to move around a circular planet. I really enjoyed this as it had been a while since I last wrote graphics shaders. The polar coordinates transformation, in the end, was a joint effort, I made a silly mistake which lead to me frustratingly staring at the code for about an hour, but was saved by my teammates in the end.

Unfortunately, we lost another member of our team during the jam, Luke took ill on the evening of the first day and despite trying to continue on had to go home.

We managed to pull everything together just in time and the finished game looked pretty great I think and was fun to play too, so I call that a win. We were missing a few things such as general balancing and feedback improvements, controller input, scoreboards etc, though Andy has been hard at work since the jam ading these extra features and polishing everything off. If you'd like to play our game you can check it out [here][source].

![alt text](https://github.com/AerialMantis/aerialmantis.github.io/raw/master/images/gg17-compilation-2.jpg "Game Jam 2017"){:width="100%"}

## Tips for those Considering a Jam

The [keynote][extra-credits] this year gave tips for new jammers, and this gave me the idea to share some tips for those who may be considering taking part in a game jam but may be put off by certain aspects of it.

There are some who take game jams very seriously and push themselves very hard, attempting to stay awake and work as much of the jam as possible. But for most, it's simply about getting together with a group of friends or even srtangers to create something, maybe learn something new in the process, but mostly just to have fun.

I've put together some tips for people who are still on te fence about taking part in a jam:

* You might be put off by the idea of working for 48 hours and barely sleeping, but it's not like this at all, almost everyone sleeps, often for as long as they would if they were at home. You don't even have to be there for the whole weekend, you can come along for a day or an afternoon if you don't have the time to commit an entire weekend.

* You might be put off by the idea of sleeping in a university or whichever venue your local jam is held in, but that's not necessary either, many jammers go home at night or go stay at a nearby hotel. There's nothing wrong with wanting to get a good nights rest, in fact, it's good for you.

* You might be put off because you feel you don't have the right skills and won't be able to contribute, but everyone has something they can contribute and your team will adapt to your strengths. A game jam is as much about learning from and helping each other as it is about making a game.

* You might be put off by the idea of being under pressure to deliver something in 48 hours, but it's important to remember that it's not a competition. As long as you don't go into a jam with unrealistic expectations you'll always come out with something to be proud of, even if that just experience you can put towards your next game jam or hobby project.

* You might be put off because you don't know anyone to form a team with, but there are many people that go along by themselves, and there are always teams that are looking for additional members to join them.

*All photos in this post are courtesy of our team photographer [Aidan Dodds][aidan-twitter]*

[global-game-jam]: http://globalgamejam.org/

[frack-the-planet]: http://globalgamejam.org/2017/games/frack-planet

[love-2d]: https://love2d.org/

[source]: https://github.com/adurdin/ggj2017

[extra-credits]: https://www.youtube.com/watch?v=2xfxx27HbM4

[aidan-twitter]: https://twitter.com/Aidan_Dodds







