---
layout: game
title: 'Rest A-shored'
meta: 'A group of teenagears are stranded on an island and have no idea how to survive. Its your job to try and guide these defiant people and help them survive until they find a way to get home again.'
coverImg: img/RestAshored/cover.png
logo: img/RestAshored/logo.png
category: game
tags:
    - C++
    - Unreal Engine 4
    - 4 weeks
duration: '1'
engine: 'Unreal Engine 4'
languages: C++
roles: 'Programmer'
github: 'https://github.com/LeafMountain/RestAshored'
---
## The Idea
A group of teenagears are stranded on an island and have no idea how to survive. Its your job to try and guide these defiant people and help them survive until they find a way to get home again.

<br/>
<center>
<iframe width="80%" height="500" src="https://www.youtube.com/embed/qiopL5JH13k" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>
<br/>
<i> The intro cinematic to the game. </i>
</center>

<center>
<iframe width="80%" height="500" src="https://www.youtube.com/embed/4HDeKBsptXE" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>
<br/>
<i> One of the developers playing the game. </i>
</center>

## The Parsing System
My main task for this project was to create the system that translates text into commands the designers can use.

We used an external voice to text plugin. To be able to use the input we needed a parsing system. I tried to emulate the action a user would do if he was using a mouse. The player first selects a unit by saying its name. This connects the unit's listener to the voice input system. Then the player is expected to issue a command with the use of a verb. After the verb has been said the parser looks for an object. This will trigger certain events later down the line that the designer can use to create the desired behavior.

<table style="text-align:center; width: 80%;">
    <tr>
        <td style="background: #8c8c8c; border-radius: 3px; font-size:150%;" colspan="3">
                Astrid, go to tent.
        </td>
    </tr>
    <tr>
        <td style="background: #f6d443; border-radius: 3px;">
            <b>Name:</b><br> Astrid
        </td>
        <td style="background: #00724e; border-radius: 3px;">
            <b>Action:</b><br> Go To
        </td>
        <td style="background: #6495ed; border-radius: 3px;">
            <b>Object:</b><br> Tent
        </td>
    </tr>
</table>

<br>

<table style="text-align:center; width: 80%;">
    <tr>
        <td style="background: #8c8c8c; border-radius: 3px; font-size:150%;" colspan="3">
                Beatrice, pick up fishing rod.
        </td>
    </tr>
    <tr>
        <td style="background: #f6d443; border-radius: 3px;">
            <b>Name:</b><br> Beatrice
        </td>
        <td style="background: #00724e; border-radius: 3px;">
            <b>Action:</b><br> Pick Up
        </td>
        <td style="background: #6495ed; border-radius: 3px;">
            <b>Object:</b><br> Fishing Rod
        </td>
    </tr>
</table>

<br>

<table style="text-align:center; width: 80%;">
    <tr>
        <td style="background: #8c8c8c; border-radius: 3px; font-size:150%;" colspan="4">
                Beatrice, give fishing rod to Astrid.
        </td>
    </tr>
    <tr>
        <td style="background: #f6d443; border-radius: 3px;">
            <b>Name:</b><br> Beatrice
        </td>
        <td style="background: #00724e; border-radius: 3px;">
            <b>Action:</b><br> Give
        </td>
        <td style="background: #6495ed; border-radius: 3px;">
            <b>Object:</b><br> Fishing Rod
        </td>
        <td style="background: #6495ed; border-radius: 3px;">
            <b>2nd Object:</b><br> Astrid
        </td>
    </tr>
</table>

<center>
<i>Units are registered at objects as well to let other units interact with them.</i>
</center>

<br><br>
<a class="button" href="https://github.com/LeafMountain/RestAshored/tree/master/Source/GP2_Team3/CommandSystem">Command System</a>
<br><br>


## Components
I'm also a big supporter of a component based system and were a big part of planning the architechture of the game. The reason we picked this architechture is to give the designers the freedom to create the game they wanted.

Me and my programmer teammates worked close with the designers to provide the functionality the designers needed to create the player experience they had envisioned. This worked very well and made it possible to iterate on the game in an effective manner.

Other than that I have been a part of many different systems, either by planning, helping or writing code toghether with other members of the team.

<!-- ## Gameplay -->

<!-- <table>
<tr>
<td>
<h3> Voice Input: </h3>
The game uses voice input to control the game. By saying the characters name the player are able to select that character. After that the character listens for certain command such as "Go to camp" or "Pick up axe".
</td>
</tr>

</table>
<table>

<tr>
<td>
<h3> Survival: </h3>
<p>
The players goal is to help the characters survive on the island by guideing them. By telling them what to do the characters can collect, feed and move to locations that will help them survive. Part of the challenge is getting them to listen, they are teenagears after all.
</p>
</td>
<td>
<img src="{{site.baseurl}}/img/RestAshored/RobinUseStone.gif" height="250px" width="400px">
</td>
</tr>

</table>
<table>

<tr>
<td>
<h3> Ownership: </h3>
<p>
We want to give the player the ability to make the game their own adventure. By letting the player build up their own camp the player will be able to create their own story.
</p>
</td>
</tr>

</table>
<table>

<tr>
<td>
<h3> Management: </h3>
<p>
The game features three values that each character need to keep at a desired level. Each character has Hunger, Temperature and Comfort. Hunger slowly decreses and the character needs to eat to refill this value. Temperature is the temperature of the character which is affected by the weather, water and nearby heatsources. The final value is Comfort which controls the feelings of the character.
</p>
</td>
<td>
<img src="{{site.baseurl}}/img/RestAshored/punchastrid.gif" height="250px" width="400px">
</td>
</tr>

</table>
<table>

<tr>
<td>
<h3> A Living Game: </h3>
<p>
We want the people to feel more alive. By adding the ability for them to have feelings towords different beings on the island. This makes them interact with each other in different ways.
</p>
</td>
</tr>

</table>
<table>

<tr>
<td>
<h3> A Living Game: </h3>
<p>
We want the people to feel more alive. By adding the ability for them to have feelings towords different beings on the island. This makes them interact with each other in different ways.
</p>
</td>
<td>
<img src="{{site.baseurl}}/img/RestAshored/astridgetwarm.gif" height="250px" width="400px">
</td>
</tr>
</table> -->


## Final Thoughts

One of the most difficult challenges of this project was the relatively unique way of controlling the game. We picked voice input because of the player engagement. We wanted the player to feel kind of like a nagging parent and get to know the people they were controlling. Ofcourse speech recognition is at its best not fully accurate, especially with different accents, which made this a somewhat difficult way of controlling the game. The game were planned and build around this feature which made it hard in the end to switch to another input, which in turn could have enhanced the game play.

Another challenge was the way we wanted the game to be experienced vs the way people interacted with the game. We wanted the player to try and communicate with the people by using different phrases which the player would find on its own. But with the feedback we got it was obvious that this was not a very fun way to experience this game. By adding a more extensive tutorial we believe we got a good balance between knowing the basic command while still throwing in some other "secret" phrases and keywords.




## Acknowledgement

* Folke Ströving Nielsen - Programmer
* Johan Andersson - Programmer
* Bruno Brito - Game Designer
* Daniel Nyberg - Game Designer
* Andreas Tobiasson - Game Designer
* Vilhelm Lindroos - 3D Artist
* Tony Högye - 3D Artist
* Nomi Bontegard - 3D Artist
* Johannes Ekholm - 2D Artist
* Beatrice Karlsson - 2D Artist
* Oneal Priyanto - 2D Artist
