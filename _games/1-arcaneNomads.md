---
layout: game
title: 'Arcane Nomads'
meta: 'A survival rpg co-op top-down shooter with a focus on the feeling of ownership. One of the main features of the game is the ability to upgrade pretty much everything to make it feel like the player has created the game and tactics.'
coverImg: img/arcaneNomads.png
logo: img/arcaneNomadsLogo.png
category: game
roles:
    - Gameplay
    - AI
---

Arcane Nomads is a co-op multiplayer top-down survival shooter set in a dark post-apocalyptic zombie ridden world. Your goal as survivors is simply surviving, you cannot stay in place or you will be swarmed by the unliving hordes roaming the city. You have to find somewhere safe to hold up and regroup, to plan your way out of the city and consider places that could still hold useful items or weapons vital to the perseverance of your group.

My contributions to this project is
* Initial design, setting and feeling of the game
* Main programmer
* Main AI programmer

Tools used:
* Unity
* C#

<br>

<center>
<iframe width="80%" src="https://www.youtube.com/embed/MRJTUXejQXI?rel=0" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>
</center>


<br>

## Camera

In the beginning of the project an experimental camera was created to see what fit the game. This camera has the ability to change to a third-person perspective from a first-person perspective with a few setting easily accessible to the design team.

<br>

<iframe src="https://pastebin.com/embed_iframe/8rNXrye6" style="border:none;width:100%; height:500px"></iframe>


<br>

## Equipment and Items

The whole game is about customization and to be able to equip a character with different equipment is a part of that. The process of creating equipment is a simple data type in Unity that's easy for the design team to use.

To make it easier to manage the equipment code I sorted the items in to categories using inheritance.

<br>

This crates a skinned mesh and assigns the correct bones.

<iframe src="https://pastebin.com/embed_iframe/8hBdEvac" style="border:none;width:100%; height:500px;"></iframe>

## AI

While developing the project we wanted a simple AI with the core functionality of hearing, sight and decisions based on health. A state machine was created to be able to control the behavior of the AI with a clean layout.

* State machine
* Show sight
* Show hearing
* Show fleeing when low health