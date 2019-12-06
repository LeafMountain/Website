---
layout: game
title: 'The Good Few'
meta: 'The Good Few is a colorful turn-based role-playing game sprinkled with city-building elements and resource management. The game revolves around the story of a band of mercenaries who get drawn into an unending conflict between a trinity of nations, each with its own reasons for bloodshed and conquest.'
coverImg: img/TheGoodFew/cover.png
logo: img/TheGoodFew/logo.png
category: game
tags:
    - C#
    - Gameplay
duration: '2' #2 months
engine: Unity3D
languages: C#
roles: 'Tech Lead / Lead Programmer'
github: 'https://github.com/LeafMountain/TheGoodFew'
---

The Good Few is a colorful turn-based role-playing game sprinkled with city-building elements and resource management.

The game revolves around the story of a band of mercenaries who get drawn into an unending conflict between a trinity of nations, each with its own reasons for bloodshed and conquest.

The idea featured a class and sub-class-based leveling system, an upgradeable player hub, customizable equipment, exciting character development, a variety of different environments to explore, and obviously lots of enemies and bosses to defeat.

<br>
<center>
<iframe class="video" src="https://www.youtube.com/embed/674sdlZJsLI?autoplay=1&mute=1" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>
<br>
<i> This game was sent to Swedish Game Awards. It did not get nominated but we are proud see our game next to other great contributions. </i>
</center>

## Turn System

## Skills System

![Skillbar]({{site.baseurl}}/img/TheGoodFew/skillbar.png)

<div id="horizontalGrid2">
  <img src="{{site.baseurl}}/img/TheGoodFew/skillAsset.png">
  <p>
    Using scriptable assets
  </p>
</div>

<div id="horizontalGrid2">
  <img src="{{site.baseurl}}/img/TheGoodFew/skillInGame.png">
  <p>
    Straight forward to set the values that's used in the UI and when using the skill
  </p>
</div>

## Level Tools and Grid

<div id="horizontalGrid2">
  <video autoplay muted loop="loop" src="{{site.baseurl}}/img/TheGoodFew/placementGrid.mp4" type="video/mp4" width="100%" height="auto">
    Picture of walkable grid in game changing shape.

    Your browser does not support the video tag.
  </video>
  <p>
    To design levels I added a grid that showed the walkable tiles. If an area were supposed to be blocked we used a components that made those cells unwalkable.
  </p>
</div>

<div id="horizontalGrid2">
  <video autoplay muted loop="loop" src="{{site.baseurl}}/img/TheGoodFew/movementGrid.mp4" type="video/mp4" width="100%" height="auto">
  Picture of walkable grid in game changing shape.

  Your browser does not support the video tag.
  </video>
  <p>
    To show the interactable cells I created a simple texture and generated a mesh. The mesh changes size depending on the distance the character can reach with different abilities or walk distance. I adjust the vertices in the y-axis to not clip the ground. To differentiate between friendly units, enemy units and empty tiles I generate submeshes and apply a different color to the material.
  </p>
</div>

## UI
* Separated the "UI component" and the system that updated it to make it easy to set values.

<div id="horizontalGrid2">
  <p>Image of something</p>
  <p>Hello</p>
</div>


<!-- <div class="wrap-collabsible">
  <input id="collapsible" class="toggle" type="checkbox">
  <label for="collapsible" class="lbl-toggle">UI Component</label>
  <div class="collapsible-content">
    <div class="content-inner">
    <pre><code class='language-c_sharp'>

    </code></pre>

    <a class="button" href="https://github.com/LeafMountain/RestAshored/tree/master/Source/GP2_Team3/CommandSystem" target="_blank">View on GitHub</a>
    <br><br>
    </div>
  </div>
</div>

<div class="wrap-collabsible">
<input id="collapsible" class="toggle" type="checkbox">
<label for="collapsible" class="lbl-toggle">System Updating UI</label>
<div>
  <div class="content-inner">
  <pre><code class='language-c_sharp'>

  </code></pre>

  <a class="button" href="https://github.com/LeafMountain/RestAshored/tree/master/Source/GP2_Team3/CommandSystem" target="_blank">View on GitHub</a>
  <br><br>
  </div>
</div>
</div> -->

<!-- ```

class TestClass
{
  void Test()
  {
    float hej;
    return;
  }
}

``` -->

<!-- 
## Components
Since I was the sole programmer on this project, I had to create simple components that other team members could use to build gameplay.

## Movement

* Using NavMesh
* Snapping the Unit to the destination in case of error
* Grid made of a mesh to mark the positions that the unit can move to. (Generating mesh and just adjusting verts)

## Turn System

* Player
* Enemy

## Final Thoughts
We had a huge scope with several different games integrated into one. In the end we created the core game play, the combat. -->