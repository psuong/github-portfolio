---
date: 2020-04-28
title: The Making of UGUIDOTS
authors: ["porrithsuong"]
categories:
  - ecs
  - dod
tags:
  - ecs
  - dod
---

[UGUIDOTS](https://github.com/InitialPrefabs/UGUIDots) is a data oriented workflow of Unity default runtime UI, UGUI. 
This provides a conversion workflow to convert the authored GameObject UI to a more DOTS friendly UI system, that works 
with their Universal Render Pipeline (formerly known as Lightweight Render Pipeline).

> While UIElements certainly scales better and a DOTS version is in the works, I wanted to solve my current issues and 
have a good understanding of the UI Pipeline.

## How it came to be?
UGUIDOTS was born from my need to have a much more efficient UI system for mobile and lower end hardware. When demoing 
[Project Arena](https://initialprefabs.com/games/repurpose/) (now called Carte Diem) at PlayNYC, I noticed that my 
demo devices were heating up too quickly after short play sessions. This was primarily due to Unity's auto batching and 
mesh rebuilding for their UI taking a large slice of the CPU. 

So, more work done over extended periods of time means more heat generated. On mobile devices, this can mean a very 
uncomfortable play session.

## Why does this happen?
Well Unity's UI has a tendency to auto batch common UI elements. The goal behind this is to limit the number of draw 
calls issued to the GPU. By combining elements together into a single mesh, Unity can send less instructions and upload 
everything it needs in one as little calls as possible.

This is interesting by design, due to doing the heavy lifting for you but can be flawed. For example, let's take a 
simple nested UI with the same material and texture. By design, Unity will batch the hierarchy into 1 draw call. 
You can see this in the Frame Debugger at Editor or runtime.

![hierarchy](/images/uguidots/hierarchy.jpg)
![frame-debugger](/images/uguidots/frame-debugger.jpg)

This made me wonder how images moved if there was a single draw call to render all the images. If an image 
moves, then the whole canvas is marked dirty and rebuilt. Now splitting your UI into smaller canvases is a [Unity 
recommended optimization tip](https://unity3d.com/how-to/unity-ui-optimization-tips), 
but it _does not solve the underlining issue_.

## The First Attempt
The first step to building UGUIDOTS was to build a basic image. Images are just represented as quad with a texture 
slapped onto it. Typically images will just have 4 vertices and 6 indices as its basic building blog. (I'm selectively 
ignoring 9 slicing images because I have not yet supported that feature yet). 

Instead of batching all the elements together, I left each image to have it's own drawcall. At that time, I figure...

> Instead of just rebatching the UI altogether and recomputing where the new vertices will be, why not just have them 
drawn individually and update the transformation matrix?

The idea was very naive, but it worked. Now my issue was that I was issuing more draw calls than necessary to draw a 
simple screen. After some basic tests and battery usage comparisons, I saw that the idea, while it solved the issue of 
batching, it used way more battery life than I expected (8% app battery usage compared to UGUI's 5% app usage in 30 
minutes).

Ultimately, I had to batch and issue roughly, the same number of draw calls as Unity's Default UI System.

## The Second Attempt
There were a couple of questions that came to my mind when revisiting the batching issue:

* Should UGUIDOTS automatically handle batching for me?
* If I didn't have auto batching, can my needs still be solved?

At the time, all I wanted was to have a joystick UI that was dynamic and followed the finger's position. Ultimately, 
I foregoed the idea of runtime batcher because I would effectively be recreating Unity's UI in DOTS. Instead, it made 
much more sense to perform static analysis on the hierarchy and embed this information for runtime. Rather than recreate 
it whenever there is a change in the UI, the information is readily available to rebuild the batch.

### Batches
Batches are stored into two parts.

1. An array of rendered elements
2. An array of spans, which define which entities belong to which batch

This means that batch information is readily available, as you simply had to check if the rendered element's index
is within some range `(a, b)`, where `a` is the start index of the span, and `b` is the total number of elements within 
the span.

However, there are certainly some limitations in regards to static analysis. Dynamic UI is not as easy as you have to 
predefine the number of elements early on or manually manipulate the runtime representation of the batch, which can 
become very messy.

## Text, text, text
My biggest gripe with text in C# or even C++, is the `string` type.
