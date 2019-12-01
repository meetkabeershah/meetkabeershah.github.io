---
layout: post
title: Geek Night Tours
---

![Geek night tours Build Tools Thoughtworks](https://cdn-az.allevents.in/banners/805e0c0c4a07a5562b2b9b9d3e19d4e8)

[courtesy](https://allevents.in/mumbai/geeknight-tours-mumbai/1539396199689544)

I attended [Geek Night Tours](http://engage.thoughtworks.com/E0P0Q0MoDvj0Q0mE0t0qn0q). It was sponsored by [ThoughtWorks](http://www.thoughtworks.com/). 

Experts [Suvish](https://www.linkedin.com/in/suvish-thoovamalayil-01aa2133) and [Mushtaq](https://www.linkedin.com/in/mushtaq-ahmed-a0b76b) covered a lot of things about `Gradle` and `SBT` as build tools.

It gave a brief introduction to continuous integration and build automations. Since, I work and prefer `.NET` - my intentions of attending was:

 - Why shall I set-up a separate build server when I can do a **simple** <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>B</kbd> in [`Visual studio`](https://www.visualstudio.com/)?
 - I personally have built a large `.NET` solution with multiple projects with ~50k+ SLOC which doesn't take more than 2-3 minutes, it's quite **fast**. So what is the reason of using a separate build infrastructure?
 - I can **already** build and verify the dependencies inside `VS`. What is build server trying to build already build and verified solution?

Although `.NET` was not specifically focused. However, I understood that [`Gradle` can be used for `.NET` as well](http://google.com/search?q=Gradle+.NET) however it might need some plugins. A few more take aways:

# Continous integration

Continuous Integration (CI) is a development practice that requires developers to integrate code into a shared repository several times a day. Each check-in is then verified by an automated build, allowing teams to detect problems early. [source](https://www.thoughtworks.com/continuous-integration)

Here is a simple use case, in my own words:

 - Make a commit to `git` source control
 - Source control pushes notification (or CI server polls from source control) to build server
 - Build system builds the project along with dependencies (e.g. `.dlls` for a `.NET` solution)
 - Build system publishes the repository to production (e.g. to `IIS` server)

One can read and read a lot about it, however the best way to learn something is to see it in action.

The summary of May'28 edition is:

# Part 1: Agile game

Moral of the story:

-	We need to be in continuous contact with the client
-	Product owner / client are more of like becoming the part of the dev team
-	The tasks need to be divided evenly based on the skill sets
-	Planning is most important
-	Agile methodology reduces wastage

# Part 2: Android apps ready for N

Important points:

-	There are Android apps for reducing battery usage (**app level**)
-	To reduce battery usage, Android will provide ways at the **platform level**
-	The biggest culprit for battery waste is connectivity changes (wifi to broadband and vice versa), N will use job schedulers for solving this problem
-	They’ve removed system level broadcast, the speaker suggested content resolvers
-	Google forcing devs to start optimizing their apps because Android will not support implicit broadcasts
-	There’re 3 types of services in Android
 1. Bound
 2.	Foreground
 3.	Unbound
-	Android will stop supporting unbound services
-	Multi window support is provided at the platform level
-	Uses `Android:resizableActivity:true` in app manifest for multi window support, all apps no matter what version of Android will have this property set to `true`
-	To make sure that the apps run in correct window (single or multiple) devs need to make sure that this property is set
-	To show new windows open in the adjacent window use property `FLAG_ACTIVITY_LAUNCH_ADJACENT`
-	**Question**: How to decide a screen is in landscape or portrait mode?
-	**Ans**: Landscape : width size is large and same concept for portrait
-	For *Android N*, devs are forced to code different layouts for different screen orientations (landscape and portrait), **this was not needed till now**

# Part 3: View debugging in iOS and other magic

The speaker shown some hacking the UI of a jail break iPhone using [AppReveal](http://revealapp.com/).