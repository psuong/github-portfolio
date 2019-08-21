---
title: Projects
description: General info about projects I've worked on.
menu:
  main:
  sidebar:
    identifier: projects
weight: -210
---

So, I've worked on a number of projects over the years and I definitely need to spruce out this page or split it up 
in the future, but here are a few projects which meant the most to me:

## Reactive Disposal ##
Reactive Disposal is a small micro framework to help manage unmanaged memory. Even though I work in C#, I often use a 
lot of unmanaged/unsafe memory, meaning I have to release every single one of them. To help me manage that, I made a 
small reactive framework which releases unmanaged memory when an entity is considered "destroyed".

***This is still very much a WIP so expect updates over the coming months!***

* [Github](https://github.com/InitialPrefabs/ReactiveDisposal)

## Dani AI ##
Dani AI is a node based editor to help design and prototype AI in Unity. Each AI designed and built using Dani AI
follows a neural network like schema and attempts to treat each agent as an organism with senses that update in
realtime.

Senses provide natural information about the simulated world and hook into decisions, where the agent executes a series
of authored actions from the user. Dani AI is currently used in Ian Cheng's Emissary in the Squat of Gods art exhibit!

You can grab it here on the [Asset Store](https://assetstore.unity.com/packages/tools/ai/dani-ai-108309).

***I am deprecating DANI AI as I think Machine Learning can certainly do better than my tool.***

## Unity Editor Tool Bag ##
The Unity Editor Tool Bag provides common decorates for Unity's Inspector to visually enhance the visual capabilities.
These visual capabilities currently provide:

* Progress Bars
* Static Message Infos, Warnings and Errors
* Dynamic/Togge-able Message Infos, Warnings and Errors

The project is open sourced and is actively worked on when I have free time. You can grab it on
[Github](https://github.com/InitialPrefabs/UnityEditorToolBag)!

## Arcade Vehicle Controller ##
The project is currently dated but provides an example of how to create an arcade vehicle controller in a **Data Oriented Tech Stack**.
There are design plans I currently have in place to upgrade and support Unity's new Data Oriented Physics Integration and to
rebuilt the module from the ground up.

* [Example](https://twitter.com/PorrithSuong/status/1045689589736730625)
* [Github](https://github.com/psuong/arcade-vehicle-controller)
