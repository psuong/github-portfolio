---
date: 2020-02-05
title: Reactive Disposal
authors: ["porrithsuong"]
categories:
  - ecs
tags:
  - ecs
---

Reactive Disposal is really just a small layer on top of Unity's Entity Component System to dispose unmanaged memory. 
This is not the same as a garbage collector as it does not do it automatically - the dispose function must still be 
called but this reduces the amount of code needed to write the same functionality over and over again.

[Github Link](https://github.com/InitialPrefabs/ReactiveDisposal)
