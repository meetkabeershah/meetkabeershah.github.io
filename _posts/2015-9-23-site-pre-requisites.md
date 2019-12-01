---
layout: post
title: site launch pre-requisites
---

![To do](http://blogs.sch.gr/news/files/2015/07/collaboration.png)

[courtesy](http://blogs.sch.gr/news/archives/390)

I'm writing this post to jot down all the things I need to do during [cloudy](http://cloud.google.com/) ASP.NET website deployments.

 - Get the [database connector](http://dev.mysql.com/downloads/connector/net)
 - **Re-*Publish*** project
 - Grab that awesome [URL rewrite module](http://stackoverflow.com/a/25317499/2404470)
 - Set [IIS_IUSRS](http://stackoverflow.com/a/18621550/2404470) and [app pool](http://stackoverflow.com/a/7334485/2404470) free
 - Check that your application pool refers to correct version of .NET
 - Get [re-certified](https://in.godaddy.com/help/request-an-ssl-certificate-562) - obviously it's a new server, right?
 - [Import](http://windows.microsoft.com/en-us/windows/import-export-certificates-private-keys#1TC=windows-7) and [install](https://in.godaddy.com/help/installing-an-ssl-certificate-in-microsoft-iis-5-and-6-4875) certificate
 - Import the same in [IIS](https://www.godaddy.com/help/installing-an-ssl-certificate-in-microsoft-iis-8-4951)
 