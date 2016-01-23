---
layout: post
title: Solving Mysql Mono port issues
---

![solving MySql problems when porting to Mono](https://ccmit.mit.edu/wp-content/uploads/2014/09/problem-questions1.png)

[courtesy](https://ccmit.mit.edu/problem-solving/)

[Checklist items to tick](http://atulgawande.com/book/the-checklist-manifesto/) when porting [ASP.NET](http://www.asp.net/) [MySql](https://www.mysql.com/) projects from [.NET](http://www.microsoft.com/net) on [Windows](http://www.microsoft.com/en-in/windows) to [Mono.NET](http://www.mono-project.com/) on [Ubuntu linux](http://www.ubuntu.com/):

 - Since Mysql is *more* [case-sensitive on Linux](http://dev.mysql.com/doc/refman/5.6/en/identifier-case-sensitivity.html), make sure that [`Database=` names matches with actual database names](http://stackoverflow.com/a/26457971/2404470) in [connection strings](https://www.connectionstrings.com/mysql/). Better, keep them in lowercase.
 - Make sure that [MySql 5.6+ is installed](http://www.tocker.ca/2014/04/21/installing-mysql-5-6-on-ubuntu-14-04-trusty-tahr.html) since [the default command `sudo apt-get install mysql-server` installs version 5.5](http://xameeramir.github.io/install-mysql-ubuntu-linux/)
 - The version of MySql on [Ubuntu Linux](https://www.google.com/search?q=check+mysql+version+ubuntu+linux) and [Windows](https://www.google.com/search?q=check+mysql+version+windows) shall match
 - MySql v5.5 tables doesn't support [FULLTEXT indices](http://stackoverflow.com/q/963534/2404470) and [CURRENT_TIMESTAMP](http://stackoverflow.com/a/23153922/2404470) features, upgrade from it
