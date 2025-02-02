---
date: 2021-08-31
title: Games
authors: ["porrithsuong"]
categories:
  - work
  - games
tags:
  - games
---

Here are some of the games I've worked on over the past few years!

# Table of Contents
  * Released
    * [Kitty in the Box 2](#kitty-in-the-box)
    * [Emissary the Sunsets the Self](#emissary)
    * [Bag of Beliefs](#bob)
    * [Kart Microgame](#kart)
    * [Kung Fu Kickball](#kfk)
    * [Cell To Singularity](#cells)
  * Not Released
    * [Inwards](#inwards)
    * [Gestalt: Steam & Cinder](#gestalt)
    * [Kitty in the Box VR](#kittyvr)
---

# Released
## Kitty in the Box 2 (Released, Mobile){#kitty-in-the-box}

![banner](http://mokuni.com/press/Kitty%20in%20the%20Box%202/images/header.png)

Kitty in the Box 2 is a mobile game where you aid, Sushi our lovable cat, jump into boxes. The game 
is released for Android and iOS in 2017.

* [Android](https://play.google.com/store/apps/details?id=com.mokuni.kib2&hl=en_US)
* [iOS](https://apps.apple.com/us/app/kitty-in-the-box-2/id1106313526)
* [Presskit](http://mokuni.com/press/sheet.php?p=Kitty%20in%20the%20Box%202)

## Emissary the Sunsets the Self (Released){#emissary}

![banner](https://d2w9rnfcy7mm78.cloudfront.net/2455622/display_c572f2f995faf7d9d8ceb3b7e6749739.png)

Emissary the Sunsets the Self is the final episode in Ian Cheng's Emissary's trilogy, which follows 
a civilization's relationship with a sentient slime like creature. The episode was built in Unity 
where I primarily worked on developing a utility theory based AI.

The project was first released and shown at Museum of Modern Art in 2017.
* [Link](http://iancheng.com/emissaries)

## Bag of Beliefs (Released){#bob}

![banner](https://d2w9rnfcy7mm78.cloudfront.net/2663713/original_5961e121e6b2cc91b90ce77bda1563f8.jpg)

Bag of Beliefs is another art exhibit and game, where attendees can interact with a sentient create 
called BOB. BOB uses exhibit provided phones to allow attendees to interact with it in order to receive 
acceleromter and motion data and determine how the attendede is interactign with it. I worked on 
optimizing the runtime and building the infrastructure to enable teammates to focus on building 
BOB's AI.

The project was first released and shown at the Gladstone Gallery in 2018.
* [Link](http://iancheng.com/BOB)

## Kart Microgame (Released){#kart}

![banner](https://assetstorev1-prd-cdn.unity3d.com/key-image/1c64e0ff-1b57-48ad-8b3d-ab7bf63e6d0c.webp)

Kart Microgame is Unity's beginner template for an arcade racing game. I helped developed this for 
Unity via Thousand Ant in order to bring gameplay updates to the kart vehicle physics, provide the 
initial ML Agents template for new users, and to optimize the game for mobile WebGL.

The project was officially upgraded at the end of 2019.

Please view the associated video [here](../thousandant).

## Kung Fu Kickball (Released){#kfk}

![banner](https://www.kungfukickball.com/images/Screenshot1.png)

Kung Fu Kickball is a multiplayer fighting sports game where the goal is to score the most points 
by kicking the ball into your goal. In order to help Whalefood Games potentially compensate for a 
lack of players online, I helped them train an agent to introduce competitive bots instead of 
building a classical experts based AI system (State Machine/Decision Trees). 

The research to train the AI was primarily based on the following [paper](https://arxiv.org/pdf/1702.06230.pdf).

Kung Fu Kickball is recently [released as of 2021](https://store.steampowered.com/app/1004620/KungFu_Kickball/).

## Cell to Singularity{#cells}

![banner](https://www.celltosingularity.com/img/cell_to_singularity_app_icon.png)

Cell to Singularity is an educational clicker idle game, where I was contracted to help Computer 
Lunch develop a feasible save system in their existing architecture. This was to help delay and 
potentially prevent users from editing their save file which may allow them to cheat and gain 
tons of resources. Simultaneously, this was used as the backbone for the team's cloud saving 
architecture, as save data was stamped and signed allowing for easy version control.

For more information on where you can grab Cell To Singularity, please see [here](https://www.celltosingularity.com/).

---

# Not Released

## Inwards VR{#inwards}

![banner](https://static.wixstatic.com/media/7e1185_7e2d1afe25994e019c616392d5f72a41~mv2.jpg/v1/fill/w_1956,h_1108,al_c,q_90,usm_0.66_1.00_0.01/Screen%2520Shot%25202021-03-12%2520at%252015_42_.webp)

Inwards is a VR game about exploring your choices. Most of my work with Inwards involve creating custom 
workflow tools for teammates and optimizing the current rendering stack in order to improve performance.

[Link](https://www.vrwiz.co/projects)

## Gestalt Steam & Cinder{#gestalt}

![banner](https://cdn.akamai.steamstatic.com/steam/apps/1231990/header.jpg?t=1629970667)

In 2018, I was contracted to help Metamorphosis Games build Gestalt: Steam & Cinder. Here I was responsible 
for creating editor tools to help the team visualize AI actions in a behavior tree.

[Link](https://store.steampowered.com/app/1231990/Gestalt_Steam__Cinder/)

## Kitty in the Box VR{#kittyvr}

![banner](http://mokuni.com/press/Kitty%20in%20the%20Box%20VR/images/header.png)

Kitty in the Box VR originally started as marketing material for Kitty in the Box 2. Eventually, the folks 
at Mokuni Games found inspiration to turn it into a game and so I started transitioning from prototyping 
work in VR into creating the backbone infrastructure to allow users to interact with Sushi. I developed 
the navigational sampling system such that Sushi would always jump on valid surfaces.

[Link](http://mokuni.com/press/sheet.php?p=Kitty%20in%20the%20Box%20VR)