---
date: 2019-08-12
title: Ten Months into the Making of Repurposed
authors: ["porrithsuong"]
categories:
  - management
tags:
  - planning
---

So just a bit of background information, Repurposed is a 2D action arena game with heavy card game elements. I think 
videos do more justice at the moment instead of me pitching, so here's the actual gameplay video link:

<iframe src="https://player.vimeo.com/video/347782662" width="640" height="360" frameborder="0" allow="autoplay; fullscreen" allowfullscreen></iframe>
<p><a href="https://vimeo.com/347782662">Repurposed Server/Client Gameplay</a> from <a href="https://vimeo.com/user97280022">initialPrefabs</a> on <a href="https://vimeo.com">Vimeo</a>.</p>

Around ten months ago, October of 2018, I prototyped a game idea on Google Slides on how I wanted people to play the 
game, and entered it into Unity's 2D challenge. But, considering we only had 3 months and the game was very quite large 
for the scope of the challenge, I turned the game into a much larger vision. 

And well...right now I am at a very content point of working on the game into a playable MVP and I'd love to describe 
the process on what worked in managing a team, a project, and to avoid burnout. Now this is in the context of me 
building the game on my free time while primarily doing consulting/freelance work as my primary day job.

# Sprints Don't Work

So I'm just going to go right off the bat, but for my team sprints did not work. A sprint in a development cycle is 
getting tasks with common goals done within a specified amount of time (most commonly around 2 weeks of development). 

So here are a few things that I have noticed about sprints. Sprinting implies we have to move fast, so the naming 
convention can be off putting as it implies that people have to work fast to get tasks done. Of course, we held daily 
"scrum" to ensure we know where the progress is with said tasks, but even then there was that sort of pressure.

# What worked instead of sprints?

Instead, I encouraged the person who did the work to estimate how long it takes for _them_ to do said work. Here's the 
approach that ended up feeling the most comfortable:

We started off with a basic user story:

```
As <whatever role>, I want <some feature> for <x, y, z reasons>.
```

So for example:

```
As a game designer, I want minute camera shakes, so that each time I flinch from an attack, the attack feels powerful.
```

Alright so we can list some unknowns/dependencies:

* Unknowns
  * How much should the camera shake?
  * What is the threshold of the damage a player can take before the camera shakes?
* Dependencies
  * Camera

Now this is a basic user story and pretty much you can get the jist of the idea on what we're supposed to implement and why. 
Now, on a game design approach, this makes sense! And we can likely map this to our code. Now, it's worth mentioning that I 
personally prefer doing a "data oriented" workflow, where data comes first and is mostly separated from 

But let's think about this technically and architecturally. This user story is pretty basic and leaves a lot to the 
imagination. Before anyone starts working on a user story like this, I usually delve into the technical details for a 
few minutes and ask the following questions:

1. What is the minimum amount of data I need to do x thing?
2. Where do I get this data?
3. What do I do with this data?
4. Where do I put this data?

Decomposing that user story, I can answer like so:

1. I need the:
  - a. delta of the health
  - b. the minimum threshold for the camera shake
  - c. some noise
  - d. the position of the camera
2. I can find the
  - a. delta of the health on the player entity
  - b. the shake threshold component attached to the player
  - c. noise by generating the random values on in a `Random.Next(...)` function
  - d. the cardinal position of the camera associated specifically with the camera
3. I need to check the delta of the health and compare it to the shake threshold on the camera, generate some random 
   offset and apply it to the camera's position
4. The only data I need to put back is the positional offset on the camera

By doing this, we go over specifically the data we need to touch and we can catch what we're missing while we're 
planning, like 

* How long does the camera shake?

It allows us as a team to reason about our infrastructure and feature on a technical side and limit the amount of 
surprises we can expect throughout the development process.

Now I'm all for iterative and collaborative development, but quite a few people have told me that the way I structure 
this emphasizes a lot on planning early on, which is "anti agile." While I can definitely see that 

# Avoiding Burnout

Respect the invidiual who is working on some task! However long it takes is however long it takes. Now in an ideal 
scenario that would be gold, but we live in a world of deadlines and making sure we live and get paid.

If a task honestly takes too long, provide your teammate some help. Rubber duckying and whiteboarding it helps out a 
lot. But this is where I personally think it gets interesting.

Imagine this scenario, you've got a looming deadline in about a month (which is not a lot of time when working part 
time on a project!). Now most indie game developers would go in a period called "crunch," which is a mad dash to the 
finish line to get whatever remaining tasks done.  

Now this is certainly worth repeating:

> Crunch is bad!!! By putting your team under crunch, we encourage a culture where crunch is okay and that the short 
term decisions typically end up being the long term ones.

What I found that worked with the team was:

If we're definitely running behind, we revisit our backlog and we make _hard_ decisions early. For example, let's say 
we had to overhaul a major piece of infratstructure because it is just too cumbersome to work with, and we expect it 
will take a few weeks to do. We defer a lot of intended features to some future date.

To meet our PlayNYC (August 10th) deadline, we made our feature lockout date, July 23rd and we deferred tasks to as 
late as 2020.

# Daily Goals

So, personally, I always think that exploring and expanding your skills is typically a good idea. I don't think anyone 
should be grounded in just 1 thing, because experiencing other things helps us emphasize with each other!

While it is important to go into your day thinking

> "What can I do which brings the most value for today?"

It is equally important to consider,

> "Can I explore anything new so I can experiment and add to my toolbag of utilities?"

We all have to learn something new and no one is a master at everything, that's a given. By ensuring that we let 
ourselves explore, we again can empathize with our team members who is working on a similar topic/issue and help solve 
the problem.

# Some Last Thoughts

So I think that's really it regarding team management on a more humane perspective. I'm nowhere near done finishing my 
game and I've certainly have things to learn about managing a project, but hope this helps and happy game deving!
