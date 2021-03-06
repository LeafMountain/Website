---
layout: game
title: 'Rest A-shored'
meta: 'A group of teenagers are stranded on an island and have no idea how to survive. Its your job to try and guide these defiant people and help them survive until they find a way to get home again.'
coverImg: img/RestAshored/cover.png
logo: img/RestAshored/logo.png
category: game
tags:
    - C++
    - Speech-to-Text
duration: '4 weeks' #4 weeks
engine: 'Unreal Engine 4'
languages: C++
roles: 'Programmer'
teamSize: '12 (3 programmers)'
genre: 'Management Survival'
year: '2018'
github: 'https://github.com/LeafMountain/RestAshored'
trailer: 'https://www.youtube.com/embed/4HDeKBsptXE?autoplay=1&mute=1'
---
<br/>
<center>
A group of teenagers are stranded on an island and have no idea how to survive. Its your job to try and guide these defiant people and help them survive until they find a way to get home again.
</center>

<div id="horizontalGrid2">
    <div>
        <table style="text-align:center; width: 80%;">
            <tr>
                <td style="background: #8c8c8c; border-radius: 3px; font-size:150%;" colspan="3">
                        Astrid, go to tent.
                </td>
            </tr>
            <tr>
                <td style="background: #E68364; border-radius: 3px;">
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
                <td style="background: #E68364; border-radius: 3px;">
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
                <td style="background: #E68364; border-radius: 3px;">
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
        <i>Units are registered as objects as well to let other units interact with them.</i>
    </div>
        <div>
    <h1>
      Parsing Commands
    </h1>
    <ul>
    <li>Speech to Text</li>
    <li>Splits the commnd into smaller parts</li>
    <li>Tries to find a Name, the interactable Object and what to use the Object on.</li>
    </ul>
    <p>
        We used an external "speech to text"-plugin called Sphinx. The output from Sphinx were the input used in the parsing system. The system tries to find out if the words are a "Name", "Action" or "Object".

        <ul>
            <li>If the name is in the beginning of the sentence the unit corresponding to that name is selected (registered as a listener to the command system).</li>
            <li>The next thing it looks for is an action like "pick up", "eat" or "hug".</li>
            <li>The last part of the command is what to do the Action to so it tries to identify an Object.</li>
        </ul>
    </p>
  </div>
    <div class="wrap-collabsible">
    <input id="collapsible" class="toggle" type="checkbox">
    <label for="collapsible" class="lbl-toggle">Parsing System</label>
    <div class="collapsible-content">
        <div class="content-inner">
        <pre><code class='language-c_cpp'>
    void ATTCommandSystem::StringToCommand(FString text)
    {
        // Exit function since there's no command listeners
        if (listeners.Num() < 1 || !listeners[0])
            return;

        // Remove the spaces in the beginning of the string
        text.TrimStartInline();

        // Check if the first word is a name (Special check on the first word)
        TArray<UTTCommandListenerComponent*> commandListeners;

        // Check if the word is everyone
        FString listenerName = "everyone";
        if (text.StartsWith(listenerName))
        {
            // Add all the listeners
            for (UTTCommandListenerComponent* listener : listeners)
            {
                commandListeners.Add(listener);
            }
        }
        // Or check which listeners the player tried to select
        else
        {
            int listenersNum = listeners.Num();
            for (int i = 0; i < listenersNum; i++)
            {
                text.TrimStartInline();

                FString listenerName = listeners[i]->ListenerTag.ToString();
                bool wordsMatched = text.RemoveFromStart(listenerName);
                if (wordsMatched)
                {
                    if(!commandListeners.Contains(listeners[i]))
                        commandListeners.Add(listeners[i]);
        
                    i = -1;
                }
            }
        }

        // Select the listeners if any has been found
        if(commandListeners.Num() > 0)
            SelectListeners(commandListeners);

        int verbsNum = verbs.Num();
        int interactablesNum = interactableNames.Num();

        while(text.Len() > 2)
        {
            bool wordsMatched = false;

            // loop through all the words
            for (int i = 0; i < verbsNum + interactablesNum; i++)
            {
                // Clean up the text
                text.TrimStartInline();

                // Flag to check if within verbs arrays range
                bool withinVerbsRange = i < verbsNum;
                // Calculate the correct index to use depending on array
                int correctIndex = withinVerbsRange ? i : i - verbsNum;
                // Get the word we want to compare
                FString wordToCompare = withinVerbsRange ? verbs[correctIndex] : interactableNames[correctIndex];

                wordsMatched = text.RemoveFromStart(wordToCompare) ;
                if (wordsMatched)
                {
                    // add the command as well
                    FCommandQueueStruct newCommand;
                    newCommand.type = withinVerbsRange ? CT_Verb : CT_Object;
                    newCommand.text = wordToCompare;

                    commandQueue.Add(newCommand);

                    break;
                }
            }

            // Remove the first word since it's not recognized
            if (!wordsMatched)
            {
                // Remove first word
                int spaceIndex;
                text.FindChar(' ', spaceIndex);

                if (spaceIndex < 0)
                    text.Empty();
                else
                    text.RemoveAt(0, spaceIndex + 1);
            }
        }

        PrintQueue(&commandQueue);
        SendCommandToUnit();
    }
        </code></pre>

        <!-- <a class="button" href="https://github.com/LeafMountain/RestAshored/tree/master/Source/GP2_Team3/CommandSystem" target="_blank">View on GitHub</a>
        <br><br> -->
        </div>
    </div>
    </div>
</div>

<div id="horizontalGrid2">
  <img src="{{site.baseurl}}/img/RestAshored/SurvivalIslandui.png">
  <div>
    <h1>
      Command System
    </h1>
    <ul>
    <li>Component base</li>
    </ul>
    <p>
      When the system have recognized the whole command it is sent out to the listener. The listener have different events that the desginers of the game could use to create the desired action in game.
    </p>
  </div>
    <div class="wrap-collabsible">
    <input id="collapsible" class="toggle" type="checkbox">
    <label for="collapsible" class="lbl-toggle">Command System</label>
    <div class="collapsible-content">
        <div class="content-inner">
        <pre><code class='language-c_cpp'>
    void ATTCommandSystem::StringToCommand(FString text)
    {
        // Exit function since there's no command listeners
        if (listeners.Num() < 1 || !listeners[0])
            return;

        // Remove the spaces in the beginning of the string
        text.TrimStartInline();

        // Check if the first word is a name (Special check on the first word)
        TArray<UTTCommandListenerComponent*> commandListeners;

        // Check if the word is everyone
        FString listenerName = "everyone";
        if (text.StartsWith(listenerName))
        {
            // Add all the listeners
            for (UTTCommandListenerComponent* listener : listeners)
            {
                commandListeners.Add(listener);
            }
        }
        // Or check which listeners the player tried to select
        else
        {
            int listenersNum = listeners.Num();
            for (int i = 0; i < listenersNum; i++)
            {
                text.TrimStartInline();

                FString listenerName = listeners[i]->ListenerTag.ToString();
                bool wordsMatched = text.RemoveFromStart(listenerName);
                if (wordsMatched)
                {
                    if(!commandListeners.Contains(listeners[i]))
                        commandListeners.Add(listeners[i]);
        
                    i = -1;
                }
            }
        }

        // Select the listeners if any has been found
        if(commandListeners.Num() > 0)
            SelectListeners(commandListeners);

        int verbsNum = verbs.Num();
        int interactablesNum = interactableNames.Num();

        while(text.Len() > 2)
        {
            bool wordsMatched = false;

            // loop through all the words
            for (int i = 0; i < verbsNum + interactablesNum; i++)
            {
                // Clean up the text
                text.TrimStartInline();

                // Flag to check if within verbs arrays range
                bool withinVerbsRange = i < verbsNum;
                // Calculate the correct index to use depending on array
                int correctIndex = withinVerbsRange ? i : i - verbsNum;
                // Get the word we want to compare
                FString wordToCompare = withinVerbsRange ? verbs[correctIndex] : interactableNames[correctIndex];

                wordsMatched = text.RemoveFromStart(wordToCompare) ;
                if (wordsMatched)
                {
                    // add the command as well
                    FCommandQueueStruct newCommand;
                    newCommand.type = withinVerbsRange ? CT_Verb : CT_Object;
                    newCommand.text = wordToCompare;

                    commandQueue.Add(newCommand);

                    break;
                }
            }

            // Remove the first word since it's not recognized
            if (!wordsMatched)
            {
                // Remove first word
                int spaceIndex;
                text.FindChar(' ', spaceIndex);

                if (spaceIndex < 0)
                    text.Empty();
                else
                    text.RemoveAt(0, spaceIndex + 1);
            }
        }

        PrintQueue(&commandQueue);
        SendCommandToUnit();
    }
        </code></pre>

        <!-- <a class="button" href="https://github.com/LeafMountain/RestAshored/tree/master/Source/GP2_Team3/CommandSystem" target="_blank">View on GitHub</a>
        <br><br> -->
        </div>
    </div>
    </div>
</div>


<br><br>

<div id="horizontalGrid3">
    <img src="{{site.baseurl}}/img/RestAshored/RobinUseStone.gif">
    <img src="{{site.baseurl}}/img/RestAshored/punchastrid.gif">
    <img src="{{site.baseurl}}/img/RestAshored/astridgetwarm.gif">
</div>
<!-- ## Components


I'm a big supporter of a component based system and were a big part of planning the architecture of the game. The reason we picked this architecture is to give the designers the freedom to create the game they imagined.

Me and my programmer teammates worked close with the designers to provide the functionality the designers needed to create the player experience they had envisioned. This worked very well and made it possible to iterate on the game in an effective manner.

Other than that I have been a part of many different systems, either by planning, helping or writing code together with other members of the team. -->

## Final Thoughts
The greatest hurdle during this project was to find the fun. The lesser used input method did in the end damage the game play by making it harder to control and less responsive. In the end we accepted this as a failed game, but we also recognized that this was still a fun experiment. Even though the game weren’t as fun as we hoped, some players found the game enjoyable in other ways. By just trying commands and see what happens did sometimes have a comical effect.

If I was to create another similar game I would focus more on developing the idea and figuring out beforehand how the input enhances the game play, and not just include it and see it become a gimmick.

## Intro Cinematic

<center>
<iframe class="video" src="https://www.youtube.com/embed/qiopL5JH13k" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>
</center>

<!-- One of the most difficult challenges of this project was the relatively unique way of controlling the game. We picked voice input because of the player engagement. We wanted the player to feel kind of like a nagging parent and get to know the people they were controlling. Of course speech recognition is at its best not fully accurate, especially with different accents, which made this a somewhat difficult way of controlling the game. The game were planned and build around this feature which made it hard in the end to switch to another input, which in turn could have enhanced the game play.

Another challenge was the way we wanted the game to be experienced vs the way people interacted with the game. We wanted the player to try and communicate with the people by using different phrases which the player would find on its own. But with the feedback we got it was obvious that this was not a very fun way to experience this game. By adding a more extensive tutorial we believe we got a good balance between knowing the basic command while still throwing in some other "secret" phrases and keywords. -->

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


<!-- ## Acknowledgement

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
* Oneal Priyanto - 2D Artist -->
