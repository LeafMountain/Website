---
layout: game
title: 'Momentum'
meta: 'Momentum is set in a place where the technology is run on the forces of time. In order to sustain it, time has been harvested from several timelines. Due to this harvest, the time continuum has started to fall apart. It is up to you to find the locks which are keeping the time vault closed and release time back into the world before it is too late.'
coverImg: img/Momentum/cover.jpg
logo: img/Momentum/logo.png
category: game
tags:
    - C#
    - Player Movement
    - Tools
duration: 'Under Development'
engine: Unity3D
languages: C++
roles: 'Gameplay Programmer'
github: 'https://github.com/LeafMountain/Momentum'
---

Momentum is set in a place where the technology is run on the forces of time. In order to sustain it, time has been harvested from several timelines. Due to this harvest, the time continuum has started to fall apart. It is up to you to find the locks which are keeping the time vault closed and release time back into the world before it is too late.

The objective was to create a rhythm based game play which challenges the player’s abilities on timing and planning. The player is equipped with a time manipulation device which can alter the states of certain platforms, structures and mechanisms. The player need to progress the level while overcoming the device's limitation of control.

During this project I worked on:
* Player Input / Movement
* Level Design Tools to ease the level creation for designers

<video class="video" controls>
  <source src="https://carbon-media.accelerator.net/0000000l2gC/isQ469qytVfcekq8Zgljvc;video.mp4" type="video/mp4">
  <!-- <source src="movie.ogg" type="video/ogg"> -->
    Your browser does not support the video tag.
</video>
<center><i>Trailer</i></center>

## Player Movement

To make it feel responsive I approached the creating by first creating a very harsh and "responsive" movement (move at full speed when pressing forward). This didn't feel too good but it was a good first step. After this I used the feedback to adjust the movement with custom velocity, acceleration and a bunch of other variables to let the movement behave different during the grounded and ariborne state.

Since the player were supposed to move with the mobile platform I created a simple solution to let the player follow the ground he or she was standing on when grounded. This was to make it easy to keep moving even when landing on an already moving platform. A problem that came with this solution was that the jump didn't feel good when leaving the platform. We solved this by using the players velocity with the jump to launch he or she even further.

In the end a bunch of modifications to the movement created a bug that let the player accelerate when turning. Even tho this was not the intended design this was met with excitement so we kept it.

## Time Manipulation tool

* Iteration.
* Showing rather than guessing.
* Work closely with design.

## Level Design Tools

* Path and follower.

Hej|![alt text](http://oliviafollin.com/____impro/1/onewebmedia/Custom_tool_to_see_path_in_editor_mode.gif?etag=%2283e18-5da090cf%22&sourceContentType=image%2Fgif&ignoreAspectRatio&resize=576%2B441 "Harvesting Rocks")

## Final Thoughts
Define gameplay to test, create, iterate.