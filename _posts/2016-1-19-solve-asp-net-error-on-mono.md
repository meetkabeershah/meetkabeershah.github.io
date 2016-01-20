---
layout: post
title: Solving ASP.NET MVC project runtime errors on Mono
---

![Monodevelop logo](https://chornsokun.files.wordpress.com/2011/11/monodevelop-2-8-2-git.png)

[courtesy](https://chornsokun.wordpress.com/2011/11/11/build-monodevelop-on-ubuntu-11-10/)

In case we're running an [ASP.NET application on Mono](http://www.mono-project.com/docs/web/aspnet/) using [Monodevelop](http://www.monodevelop.com/) for the first time, [we may receive the below error](http://stackoverflow.com/a/34872143/2404470):

![Could not launch ASP.NET web server](https://lh3.googleusercontent.com/2vI7SdMsVHBFLR7cOuqb7eoTF561t5BRLLmEfliOvKXH-9zZZ0t8dRM_2_t6jFF75C9kIz8fN3mgXRgg9ZiLzw80bbBMmvEVgevbBFgnuJpQXJ8E9kKQSKXbORy9rhFyIznWRgm7RaEJn_JjRGtAqIbgiCGW69GcoEwDjGloJW3pO0ayMt1J8N0V-4VhRllq-I9HWzEOJcC9SoDelR3d-zdYBxqQQ_M58USmJuYN5YtpulFfrh4UeeOPcJFrBGXMdwdXWvxLOt4mvf-QHHbYXV004KME6iZOZSN9g3O6MT2Iy3KtN13YlvRip_bERgyqRRs2BxJmfQoWnuEGVC7eymjcE5Qjf2pLuCg9RB_mZuOsleCyh2vlxzWKSpaU63Hp6U2aPrMko2-qmobCjSJNMCMi2Qfg9EzJ3ObWQ88W0alel_Lzfd_rWPoQLpJEnEKhP7ZkC8HQYezKj4jEPzSP4zF_S8TBGqAd-LGSb44m2OniZYHoev6Z9fjVjyX3fSWDKu2D48i9VIk6a8UyrVhveJerlZQk3aYOexOoaToYEmnaSE-1ZULem0dH-hG2N4eBI6Zh=w478-h179-no)

In some cases, the problem is incorrect installation of [`xsp4`](http://packages.ubuntu.com/precise/web/mono-xsp4) server.

Install it using:

`sudo apt-get install mono-xsp4`

This solved the above error.

**Optional:** get it from **Ubuntu software center** by searching for `xsp4`

![mono-xsp4 in Ubuntu software center](https://lh3.googleusercontent.com/C5-5C3FHK2RE7--bmz6VSqU6keQXyvUAxhtoGOPt2xXrp1oZVOhMdgF0-J91A7ptJWyyu33OY1I6s6oToOeV8B3IvC2XT6pU1FNb-WqIOA4xs3Xp6Eo0lK8CRsNrza4j6HXGZQUg536VoCbAaCvOykTkll0Rxo7aJp8etcKT6v7UvQvqUv5si9agQoVeF5n6fenW9evfZ55VoHldYUnYM2qcKe8BKIg5GXEya4sv0ESPktYXfZfi3VPVvhuzk-NqvNJrriTGiWnUgPm9Vci1efPzeriHgVx6L91WoBwrs0d5M8eNZxm1dg9G_22i5f3WuZe65QOkuT9AO_3ysC9o9ZLpIM6JQNNS6expj9sXAqMVUhTBm7yzV5EoeHOWE9XIA6R1C9eo-00JvWxDDhABP6U8aMbYeT_10yy0v_jfP2Y-qk3m1st-lnSBnQyCNBuj_qNMcxK7sR0zh4lDIbNEha_wKMy1rsfUEUexYFspMDBXLkZz1kJt9qnPgyVMp5rYIGLt5i_Kn32IfLDmqwA2aePfyTE3i_6LIq7S5eU3cuP6VqiSMxI11hcB8lYAFjI0ofbo=w1088-h637-no)

After the `xsp4` server is installed and ready. The project will start running at [http://127.0.0.1:8080/](http://127.0.0.1:8080/)

A directory access error saying [`Access to the path “/etc/mono/registry” is denied`](http://stackoverflow.com/q/24872394/2404470) may also show up which can be solved by *simply* creating the folder using [`mkdir`](http://alvinalexander.com/unix/edu/examples/mkdir.shtml)

`sudo mkdir /etc/mono/registry`

and setting the right permissions using [`chmod`](https://en.wikipedia.org/wiki/Chmod) 

`sudo chmod uog+rw /etc/mono/registry`

[Photos](https://goo.gl/photos/1GKy1Q5cQErmafNWA)
