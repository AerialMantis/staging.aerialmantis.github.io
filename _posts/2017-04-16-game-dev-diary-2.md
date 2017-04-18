---
layout: post
title:  "Game Dev Diary 2: Modelling in Blender"
date:   2017-04-16 12:00:00 +0000
categories: gamedev
---

In my first post I didn't do much beyond telling you that I'd like to make a game and and a little about how I'd like to go about it. To be honest that post was largely for me, I wanted to put myself out there and make a promise to myself that I will continue the project and not get distracted. Unfortunately it has taken me longer to get this second post out than I had hoped, but I do have something to show.

I've spent the time since my last post trying to learn 3d modelling using Blender so that I could create my own assets for my game. To be honest I was scpetical as to whether I was going to be able to achieve much at all, my last and only experience of 3d modelling was in University about 8 years ago and I don't remember being very good at it. I was though, pleasantly surprised by what I was able to create.

## Learning Blender

The first task I set myself was to create a character model, and I know what you're thinking - why would you pick that first? Well, a caracter model is very important to the game I want to create so I can't do much wthout one, and I needed to know if creating my own character models was feasible or not. Another reason is that a character moddel requires all of the steps of 3d modelling that I wanted to learn; modelling, texturing, rigging and animmating.

I found a great tutorial series on youtube that walks you through the steps of creating a simple character model, and also does a good job of explaining how everything works for beginners like me. The tutorials also showed the key presses throughout the videos, which was very useful as there were times where I would have to rewind and watch the videos back to see what shortcuts were being used to acheive the effects I was seeing.

This task was challenging, and I hit a few issues along the way, but with the help of the tutorial I managed to create something that looked reasonably like a character, even if it did walk a little funny.

![alt text](https://github.com/AerialMantis/aerialmantis.github.io/raw/master/images/blender-character.png "Character model in Blender"){:width="100%"}

My second task was to create a house model, something that my character model could interact within. I definitely found this less challenging than creating a character model as it mostly involved constructing a model from a blueprint. Altough this had it's own challenges, when creating a model of a building it was much more improtant that everything consistent and to scale. I often made mistakes where I would forget to split up a piece of geometry or I would get the dimensions of a piece of geometry wrong early own and it would come back to bite me later.

![alt text](https://github.com/AerialMantis/aerialmantis.github.io/raw/master/images/blender-house.png "House model in Blender"){:width="100%"}

If anyone is interested in following these tutorial series' you can find them here: character model ([modelling][blender-character-tutorial-modelling], [texturing][blender-character-tutorial-texturing], [rigging part 1][blender-character-tutorial-rigging-1], [rigging part 2][blender-character-tutorial-rigging-2], [ranimating][blender-character-tutorial-animating]), house ([part 1][blender-house-tutorial-1], [part 2][blender-house-tutorial-2], [part 3][blender-house-tutorial-3], [part 4][blender-house-tutorial-4]).

## Integrating into Unity

Once I had my models next I had to integrate them into Unity, which, with the tools that Unity provides for animation control and navigation, was pretty straight forward. The challenge came in creating the interaction between the models.

Firstly I wanted to have the top half of the house model disapear when the character got close to it. Ideally this kind of effect would be best done with a graphics shader, but for now I opted to do this through game logic to get something up and running quickly. I split the model into two and simply disabled rendering of the top part when the caracter got within a bounding box around the house.

Next I wanted to have the doors of the house open when a character goes to walk through them. This was challenging because as far as I know, Unity doesn't seem to have the functionality to detect obstacles in the path of a navigation agent. My solution was to not include the doors in the nav mesh and to check if the character is moving and the forward vector collides with a door, and if so open the door by roatating it.

![alt text](https://github.com/AerialMantis/aerialmantis.github.io/raw/master/images/unity-house-character.png "Character and housse models in Unity"){:width="100%"}

## Takeaways

My take away from 3d modelling was that it is challenging, but not the ways that I expected it to be.

My expectation were that modelling would require artistic ability and a good eye for proportions which are skills I don't possese. I believe these skills are definitely nessesary for more advanced modelling, however for the simple models that I was looking to create, this didn't feel as important. The reason for this was that; as I learnt during this process, it's common practice in 3d modelling to use orhographic views of the objects your modeling as a guide to contructing the initial shapes. This meant getting the details and proportions right were simply a matter of tracing a background, which I coud definitely do.

What I did find challenging was having patience, careful detail and a vision for the model as a whole. Every mistake I made was due to forgetting someting improtant, doing sommething too quickly and missing an important step or not thinking about how the finished model will look and setting myself up for failure later.

Another aspect I found cahllenging was simply remembering the shortcuts of all the different commands you can do and remembering in wich contexts those commands are valid. This may just be a trait of the Blender editor, as I've not much experience with any other, but it's a lot to remember.

This experience was very rewarding and has given me a great deal of admiration for 3d modellers, even with the simplest models, I struggled to keep my cool, as I slowly saw my models take shape. But it was also very enjoyable and it's also given me a lot of motivation for creating my own assets for my game.

## Tips for Following these Tutorials

My biggests tip for anyone thinking about trying out 3d modelling would be to just give it a try, it's not as tough as it looks and there's plenty of resources out there to help you.

I've put also together a few tips for trying out 3d modelling with Blender based on my experience:

* When selecting vertices of a model in edit mode, if you are in wireframe you will also select the vertices directly behind those, but if you are not you won't.
* When creating seems on a model for texturing, look out for pixels very close together as if you don't spot them it can cause strange unwrapping.
* When painting weights onto a model for rigging a model to a skeleton, you have to select the skeleton and switch to pose mode before selecting the model.
* If you are exporting multiple models that will interact with each other you have to be careful of where the origin of each model is as this will affect where the object rotates from when loaded into a game engine such as Unity.

## What's Next

What I have learnt from the past months is that creating my own assets for my game is not unrealistic, providing I don't require them to be too detailed. But I have also learnt that the time required to do this means I have to be more realistic with my goals for this game.

I've dediced to make my first goal to create a working prototype of my game. This prototype doesn't need to have any detailed models and textures, it doesn't have to have any advanced gameplay mechanics and it doesn't have to have any creative UI. It's purpose is simply to serve as a proof of concept from which I can experiement with different gameplay mechanics to find out what works. I believe this milestone is challenging but not unrealistic.

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