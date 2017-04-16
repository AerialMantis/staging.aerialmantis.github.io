---
layout: post
title:  "Game Dev Diary 2"
date:   2017-04-16 12:00:00 +0000
categories: gamedev
---

In my first post I didn't do much beyond telling you that i'd like to make a game and and a little about how I'd like to go about it. To be honest that post was largely for me, I wanted to put myself out there and make a promise to myself that I will continue the project and not get distracted. Unfortunately it has taken me longer to get this second post out than I had hoped, but at least I'm back with something to show.

I've spent the time since my last post trying to learn 3d modelling using Blender so that I could create my own assets for my game.

To be honest I was scpetical as to whether I was going to be able to achieve much at all, my last and only experience of 3d modelling was in University about 8 years ago and I don't recall being very good at it. However I was pleasantly surprised by what I was able to create.

## Learning Blender

The first task I set myself was to create a character model, and I know what you're thinking - why would you pick that first? Well my reasoning was that the fundemental component my game would need in order to create interactions is a character, there really isn't much I can do without one. Additionally a character moddel covered all of the stages of 3d modelling that I wanted to learn; modelling, texturing, rigging and animmating.

Fortunately I found a great tutorial series on youtube that walks you through this entire process, at a very reasonable pace, whilst providing useful advice along the way. Sebastian also showed his key presses throughout the videos, which was very important as there were times where I would rewind and watch back his keypresses to reproduce the same effects.

![alt text](https://github.com/AerialMantis/aerialmantis.github.io/raw/master/images/blender-character.png "Character model in Blender"){:width="100%"}

My second task was to create a house model, something that my character model could interact within. I definitely found this less challenging than creating a character model, as it mostly involved constructing a model from a blueprint.

![alt text](https://github.com/AerialMantis/aerialmantis.github.io/raw/master/images/blender-house.png "House model in Blender"){:width="100%"}

If anyone is interested in following these tutorial series' you can find them here: character model ([modelling][blender-character-tutorial-modelling], [texturing][blender-character-tutorial-texturing], [rigging part 1][blender-character-tutorial-rigging-1], [rigging part 2][blender-character-tutorial-rigging-2], [ranimating][blender-character-tutorial-animating]), house ([part 1][blender-house-tutorial-1], [part 2][blender-house-tutorial-2], [part 3][blender-house-tutorial-3], [part 4][blender-house-tutorial-4]).

## Integrating into Unity

Once I had my models the next stage was to integrate them into Unity, which with all of the many tools that Unity provides for animation control and navigation, was very straight forward. The challenge I came across here was in creating game mechanics around these models.

Firstly I wanted to have the top of the house model disapear, when the character is close to it, ideally this kind of effect would be best done with a graphics shader, however for now I opted to do this through game logic to get something up and running quickly.

Next I wanted to have the doors of the house open when a character goes to walk through them. This was challenging because as far as I know, Unity doesn;t seem to have the functionality to detect obstacles in the path of a nav agent. My current solution is simplly to check if the characteris moving and the forward vector collides with a door, and if so it opens the door.

![alt text](https://github.com/AerialMantis/aerialmantis.github.io/raw/master/images/unity-house-character.png "Character and housse models in Unity"){:width="100%"}

## Takeaways

My take away from 3d modelling was that it is challenging, but not the ways that I expected it to be.

My prior expectations were that modelling would require artistic ability and a good eye for proportions above all, skills I regretably don't possese. I believe these skills are definitely nessesary for more advanced modelling, hwoever for the simple primitive models that I was looking to create, this wasn't a challenge. The reason for this was that; as I learnt during this process, it's common practice in 3d modelling to use orhographic views of the objects your modeling as a guide to contructing the initial shapes of your models. This meant getting the details and proportions right were simply a matter of tracing a background, which I can do.

What I did find challenging was maintianing patience, careful detail and a vision for the model as a whole, throughout the process. Every mistake I made was due to forgetting someting improtant, doing sommething too quickly or not thinking about the later stages or how the finished model will look, and every time the problem would escalate because it would be later that I would notice my mistake.

This experience was very reqarding and has given me a great deal of admiration of 3d modellers, even with the simplest models, I struggled to maintain my patience, as I slowly saw my models take shape.

Another aspect I found cahllenging was simply remembering the shortcuts of all the different commands you can do and remembering in wich contexts those commands are valid.

# Tips for Following these Tutorials

Some tips for using Blender from my experiences:

* When selecting vertices of a model in edit mode, if you are in wireframe you will also select the vertices directly behind those, but if you are not you won't.
* When creating seems on a model for texturing, look out for pixels very close together as if you don't spot them it can cause strange unwrapping.
* When painting weights onto a model for rigging a model to a skeleton, you have to select the skeleton and switch to pose mode before selecting the model.
* If you are exporting multiple models that will interact with each other you have to be careful of where the origin of each model is as this will affect where the object rotates from when loaded into a game engine such as Unity.

## What's Next

What I have learnt from my expereicne over the past months is that creating my own 3d assets for my game is not unrealistic, providing I don't require them to be too detailed, but I have also learnt that the time required to do this means I have to be more realistic with my goals for this game.

I've dediced to make my first goal to create a working prototype of my game. This prototype doesn't need to have any detailed models and textures, it doesn't have to have any advanced gameplay mechanics and it doesn't have to have any UI. It's purpose is simply to serve as a proof of concept. I believe this milestone is challenging but not unrealistic.

Having this prototype will allow me to experiment with different gameplay mechanics that I've been considering to find out what works.

In my next post I aim to present a design for this prototype and some of the game mechanics I hope to have in it.

[unity-website]: https://unity3d.com/
[blender-website]: https://www.blender.org
[blender-character-tutorial-modelling]: https://www.youtube.com/watch?v=DiIoWrOlIRw
[blender-character-tutorial-texturing]: https://www.youtube.com/watch?v=JYBPXTful2g
[blender-character-tutorial-rigging-1]: https://www.youtube.com/watch?v=Q9f-WVs3ghI
[blender-character-tutorial-rigging-2]: https://www.youtube.com/watch?v=TPEmonfLo94
[blender-character-tutorial-animating]: https://www.youtube.com/watch?v=DuUWxUitJos
[blender-house-tutorial-1]: https://www.youtube.com/watch?v=1fYPUf_ozHg
[blender-house-tutorial-2]: https://www.youtube.com/watch?v=Rpg4yDcqoSk
[blender-house-tutorial-3]: https://www.youtube.com/watch?v=4c8TRSYK3Vo
[blender-house-tutorial-4]: https://www.youtube.com/watch?v=DJkoHLzYozU

## Texturing

* When creating seems for texturing watch out for vertices in the same location hiding a face as this will cause issues

## Exporting

* Issue exporting different layers as different obejcts.

## House

* How to export the house and the doors separately
* Problem setting origin of object - door
* Had to split house in half - streight forward if you have a split through all of the geometry
* Problem adding porch and steps - have all walls from the beginining before you extrude

* How to mae the top part of te house disapear
* How to make the door open though navigation
