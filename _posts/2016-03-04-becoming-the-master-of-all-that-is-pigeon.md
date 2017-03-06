---
layout: post
title:  "Becoming the Master of all that is Pigeon"
date:   2015-05-16 12:00:00 +0000
categories: events
---

The Global Game Jam had come around again and as with last year, some friends and I attended the Glasgow Global Game Jam at Glasgow Caledonia University, where we created our game 'B.F. Skinner: Pigeon Herder'.

The [Global Game Jam][global-game-jam] is a yearly event held in many different locations all over the world where game dev enthusiasts come together in teams in order to make a game in 48 hours under a common theme. The games that are created during the jam are generally video games but it does also see other kinds of games like board games, card games and social media games as well. The experience of a game jam is probably best described as the full game development process; including game design, content creation and crunch time, condensed into 48 hours.

![alt text](https://github.com/AerialMantis/aerialmantis.github.io/raw/master/images/game-jam-2016.jpg "Game Jam 2016"){:width="100%"}

A couple of my friends arrived early in the afternoon to pick out a good spot and get set up, and despite some trouble with electricity supply we managed to get a really good set-up. The rest of us arrived just as the theme was announced, which this year was 'ritual'.

You might wonder how we got to a game about herding pigeons from the theme 'ritual', and that's a very good question. So after the theme was announced we spent some time brainstorming ideas that involved ritualistic designs or mechanics for a game until we finally decided on a combination of two concepts.

The first was an idea based on the [research of B.F. Skinner][b-f-skinner], who performed experiments in which he would randomly feed pigeons, leading to the pigeons developing superstitious rituals attempting to reproduce what they were doing when they were fed. The problem with this was that since the reinforcement was random it was difficult to come up with game mechanics that would give genuine feedback to the player.

The second was an idea in which you played an overlord controlling a group of minions and by issuing commands the player would have the minions perform rituals.

![alt text](https://github.com/AerialMantis/aerialmantis.github.io/raw/master/images/pigeon-herder.jpg "B.F Skinner: Pigeon Herder"){:width="100%"}

The combination of these two ideas would result in the concept for our final game; [B.F Skinner: Pigeon Herder][pigeon-herder], in which a kit of pigeons perform random movements and actions and the player must strategically feed the pigeons in order to reinforce the behaviour they want when they see it in order to move the pigeons to a particular location or have them perform a particular pattern of behaviours. The difficulty for the player comes in influencing the behaviour they want to see in the pigeons while not influencing other behaviours or other pigeons.

Now that we had our idea we just had to decide on which tech we wanted to use to make the game. We decided to make a 2d game since no one on our team was particularly experienced with 3d art. For coding we went for a Lua based game framework called [Love2D][love-2d], which was great, using new tech did add some additional challenge, but i'm glad we did because it was fun learning something new.

We spent a lot of time working on the pigeon AI in order to come up with behaviour that gave pigeons the right balance of randomness and feedback for the player. We were concerned at some points within the development that the game would be too difficult to play, but in the end it worked very well.

The final game had just a few levels with the objective of getting a certain number of the pigeons to a certain location, however if we had the time we wanted to add further objectives involving herding the pigeons into performing a particular pattern of behaviours.

If you're interested, you can check out our game [here][pigeon-herder], and see if you can become the ultimate pigeon herder. Note that the version there has a few minor bugs that have since been fixed and you can checkout the source for the latest version [here][source], which you can run with [Love2D][love-2d].

[global-game-jam]: http://globalgamejam.org/
[b-f-skinner]: http://psychclassics.yorku.ca/Skinner/Pigeon/
[pigeon-herder]: http://globalgamejam.org/2016/games/bf-skinner-pigeon-herder
[love-2d]: https://love2d.org/
[source]: https://github.com/mulingkittens