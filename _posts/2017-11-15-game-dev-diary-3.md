---
layout: post
title:  "Game Dev Diary 3: Creting a Scene in Blender"
date:   2017-11-15 12:00:00 +0000
categories: gamedev
---

In my [last post][last-post] I talked about learning to use [Blender][blender-website] so I could creating models for my game and my experiences with it. Since then I've been having a go at on creating a 3d scene. It's been a while since I last posted, I've not had as much time to work on this project lately as I'd have liked and I wanted to finish the scene before posting again.

## Game Design

I have been thinking a lot about the design of the game I want to make and what kind of mechanics I want to have in it. To give a little more information about the idea; I want it to be a top down perspective, real-time strategy game where you control a group of survivors. I want it to have the usual survival genre mechanics like gathering resources, construction, crafting but I also want it to have role playing mechanisms where members of a party can level up their skills. Beyond this though I've not yet decided on the specific mechanics of the game, like navigation and combat, I've got some ideas but I think I'm going to have to play around with them to figure out what will be fun.

I also want narrative to play a big part in the game. When I play survival games I feel many have a lack of direction or objective, other than simply surviving, so I quickly loose my motivation to keep on going. So I want my game to be a sandbox where the player has a lot of freedom, but I also want it to have a strong narative which keeps the game moving forward.

## Creating a 3D Scene

For my next task I wanted to learn everything needed to create a 3D scene which my character could move around in. This sounded simple at first, but as you can tell from the time since my last post it took me longer than I expected. This was very rewarding, just with learning character modelling, I learnt a great deal about modelling a 3D scene including constructing a terrain, modelling trees, creating textures and how to use the different Blender renderers.

The scene I wanted to create was a woodland area with a small lake and a log cabin. The picture below is one of the concept images I used for inspiration.

![alt text](https://github.com/AerialMantis/aerialmantis.github.io/raw/master/images/game-dev-diary-3/log-cabin.png "Log cabin reference image"){:width="100%"}

## Terrain

Creating the terrain itself was pretty simply, I created a plane and then tesselated it into a grid so I could manipulate the pixels to form the shape.

> A tip form my experience working with large terrain meshes in Blender, it's best to unwrap the uv coordinates before you start modifying the terrain as when done the other way around the uv unwrapping can sometimes have strange effects.

![alt text](https://github.com/AerialMantis/aerialmantis.github.io/raw/master/images/game-dev-diary-3/terrain-solid.png "Terrain in wireframe"){:width="100%"}

The tough part was texturing it. I could have just downloaded free stock textures from the internet (there's a lot of websites out there) but I wanted to have a go at creating the textures myself. I was worried about this part as I'm not very good at computer art, though after looking around I found some tutorials at [abmera.wordpress.com][abmera-tutorials] on very simple techniques that would create nice looking textures in very little time at all.

![alt text](https://github.com/AerialMantis/aerialmantis.github.io/raw/master/images/game-dev-diary-3/terrain-textures.png "Terrain textures"){:width="100%"}

Admittedly I created several textures, experimenting with different techniques and these were my better attempts.

Once I had the textures I had to paint them onto the terrain. In Blender this can be a little complicated but it's not so bad once you get used to it. I followed a [tutorial][painting-textures] which goes through the steps of importing textures and then painting them onto a new texture file that's mapped to your model using the uv coordinates (in this case my terrain model). You have to play around with the resolution of the brushes and the sample textures until you get it looking how you want.

> A tip from my experience with painting textures in Blender, be aware that Blender doesn't save textures files along with the model, you have to manually save them. I got burnt by this a couple of times, losing a lot of work, before I realised what I was doing wrong.

![alt text](https://github.com/AerialMantis/aerialmantis.github.io/raw/master/images/game-dev-diary-3/terrain-textured.png "Terrain textured"){:width="100%"}

## Cabin

For the log cabin I followed the same technique as I did for the house in my previous post, by using a blueprint as a guide.

![alt text](https://github.com/AerialMantis/aerialmantis.github.io/raw/master/images/game-dev-diary-3/log-cabin-blueprint.png "Terrain textured"){:width="100%"}

Once finished I added this to the scene.

![alt text](https://github.com/AerialMantis/aerialmantis.github.io/raw/master/images/game-dev-diary-3/log-cabin-model.png "Terrain textured"){:width="100%"}

## Trees

For creating the trees I tried a couple of different approaches. I first tried modelling the trees manually, I found this approach fun but difficult to get natural looking trees. Next I tried using a Blender add-on called sapling which generates the curves of a tree procedurally, following a [tutorial][creating-trees]. I felt like I was cheating a bit, but this approach gave me very natural looking trees so I went it.

> A tip from my experience with using the sapling add-on, before you can texture a tree you need to convert it to a mesh. To do this you have to press `Alt + C`, and then select `Mesh from Curve`.

In order to add the leaves to the tree I had to add a transparency shader to the renderer in order to render the leaves realistically.

> This tutorial shows how to do this using the Cycles renderer which provides fine grained control over the render pipeline. Beware when following other tutorials, Blender has other renderers which work differently, so it takes some time to get used to this.

![alt text](https://github.com/AerialMantis/aerialmantis.github.io/raw/master/images/game-dev-diary-3/finished-scene.png "Finished scene"){:width="100%"}

## Integrating with Unity

Once the scene was complete I tried it out in [Unity][unity-website]. I loaded the model in and created a navigation mesh to allow my character to move around on the terain. I also created a blue plane for the water of the lake.

![alt text](https://github.com/AerialMantis/aerialmantis.github.io/raw/master/images/game-dev-diary-3/finished-scene-in-game.png "Finished scene"){:width="100%"}

## What's Next

From now on I'd like to put out smaller posts much more frequently. For my next task I'm going to try to learn how to create different character animations. I touched on this for creating my character model in my last post, but this was only for a single walk animation cycle. I feel like for my game I will need to know how to create other kinds of animations.

[last-post]: http://www.aerialmantis.co.uk/blog/2017/04/16/game-dev-diary-2/
[unity-website]: https://unity3d.com/
[blender-website]: https://www.blender.org
[abmera-tutorials]: https://abmera.wordpress.com/2012/05/21/creating-nice-looking-game-textures-using-gimp/
[gimp]: https://www.gimp.org/
[painting-textures]: https://www.youtube.com/watch?v=xYVVhC60mz0
[creating-trees]: https://www.youtube.com/watch?v=rN2CYXVKH0s