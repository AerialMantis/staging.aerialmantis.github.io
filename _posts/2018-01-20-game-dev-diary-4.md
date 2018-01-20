---
layout: post
title:  "Game Dev Diary 4: Humans and zombies (kind of)"
date:   2018-01-20 12:00:00 +0000
categories: gamedev
---

In my [last post][previous-post] I learnt the steps involved in creating a 3D scene in Blender. Now that I felt I had a reasonable grasp on 3d modelling (at least enough to create something I could work with) I was eager to start working on the game itself. Since my last post I have created a new character model, this time with a number of different animations and tested them out in Unity.

![alt text](https://github.com/AerialMantis/aerialmantis.github.io/raw/master/images/game-dev-diary-4/animations-in-unity.png "Human walk animation in Unity"){:width="100%"}

## Game Design

For the final game I want the survival aspec to take many forms; survival from zombies of some kind, survival with and potentially from other humans, and survival in general. But to begin with I thought I'd start with the zombies, as they will likely be the main focus of the combat and navigation mechanics.

## Annimating Humans and Zombies

The first thing I needed for the game was a character model. As I showed in a previous post I created a character model already, though that one was a copy of the model the tutorial was demonstrating and I wanted something a little different. As a first character model for my game I wanted something very simple, without any details or texturing, and something which could be used for both the human characters and the zombie characters, a placeholder for future more detailed models.

In order to experiement with different mechanics I needed this model to have a range of different animations. Though the animations too didn't have to be particularly detailed, they also just had to be enough that you could identify what the characters in the game were doing.

For this character model I followed the same tutorials which I used in [my post on 3D modelling in Blender][post-on-3d-modelling]. Though this time I used them for as a reference rather than a step by step guide. I still followed the general steps of the modelling process, though I made this character simpler and more toonish. Doing my own animations was tough, but I felt by the end I was starting to get the hang of it, even if all my animations we extremely basic.

The first animation I did was a walk animation cycle for the human character; this was pretty straight forward as I pretty closely followed the walk animation from the [tutorial][animation-tutorial].

![alt text](https://github.com/AerialMantis/aerialmantis.github.io/raw/master/images/game-dev-diary-4/human-walk.png "Human walk animation cycle"){:width="100%"}

Next I did a run animation cycle for the human character. This was a bit trickier; I was able to use the poses from the walk animation as a guide but I had to figure out what those poses should be for a fun cycle. It was also a lot of fun, slow motion running around my house enacing the poses in order to figure out the key frames.

![alt text](https://github.com/AerialMantis/aerialmantis.github.io/raw/master/images/game-dev-diary-4/human-run.png "Human run animation cycle"){:width="100%"}

After that I did a walk animation cycle for the zombie character. For this one I cheated a little, I based the poses off of the human walk cycle, but made the feet drag rather than lift, and raised the arms forward. I also staggered the certain poses so that the movement seemed staggered rather than smooth.

![alt text](https://github.com/AerialMantis/aerialmantis.github.io/raw/master/images/game-dev-diary-4/zombie-walk.png "Zombie walk animation cycle"){:width="100%"}

I also created idle and attack animations for the human character and idle, attack and death animations for the zombie. Though I made a bit of a mistake with the death animations, as I didn't disable the inverse kinematics on the feet of the model, so the feet ended up in some strange positions.

![alt text](https://github.com/AerialMantis/aerialmantis.github.io/raw/master/images/game-dev-diary-4/human-die.png "Human death animation"){:width="100%"}

## What's Next

For my next task I'm going to start writing some code, I'm going to create an RTS camera controller for Unity so I can naviagate the same world better.

[previous-post]: http://www.aerialmantis.co.uk/blog/2017/11/17/game-dev-diary-3/
[post-on-3d-modelling]: http://www.aerialmantis.co.uk/blog/2017/04/16/game-dev-diary-2/
[animation-tutorial]: https://www.youtube.com/watch?v=DuUWxUitJos