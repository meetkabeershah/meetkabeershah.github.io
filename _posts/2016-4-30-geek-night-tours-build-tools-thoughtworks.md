---
layout: post
title: Geek Night Tours - build tools
---

![Geek night tours Build Tools Thoughtworks](https://cdn-az.allevents.in/banners/805e0c0c4a07a5562b2b9b9d3e19d4e8)

[courtesy](https://allevents.in/mumbai/geeknight-tours-mumbai/1539396199689544)

Today, I attended [Geek Night Tours](http://engage.thoughtworks.com/E0P0Q0MoDvj0Q0mE0t0qn0q). It was sponsored by [ThoughtWorks](http://www.thoughtworks.com/). 

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
