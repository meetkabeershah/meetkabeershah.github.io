---
layout: post
title: How to configure Heroku on Ubuntu 16.04.3 x64
---

[![You need to enable JavaScript to run this app.][1]][1]

Today, I purchased `Ubuntu 16.04.3 x64` server running on [DigitalOcean](https://www.digitalocean.com/) infrastructure. It’s not too different than the ones on [premise](https://www.softwareadvice.com/resources/cloud-erp-vs-on-premise/):
Configuring [Heroku](https://www.heroku.com/) is quite straight-forward. After ssh-ing, run the following commands with [sudo](https://linuxacademy.com/blog/linux/linux-commands-for-beginners-sudo/):

<pre>
<code>
wget https://cli-assets.heroku.com/heroku-cli/channels/stable/heroku-cli-linux-x64.tar.gz -O heroku.tar.gz
tar -xvzf heroku.tar.gz
mkdir -p /usr/local/lib /usr/local/bin
</code>
</pre>

List the content of the current directory with `ls`. I found this output:

<pre>
<code>
heroku-cli-v6.15.22–3f1c4bd-linux-x64
heroku.tar.gz
</code>
</pre>

This output determines the value in the next step, use the first file name in the next command:

<pre>
<code>
mv heroku-cli-v6.15.22-3f1c4bd-linux-x64 /usr/local/lib/heroku
ln -s /usr/local/lib/heroku/bin/heroku /usr/local/bin/heroku
</code>
</pre>

And that’s it.

[1]: https://miro.medium.com/max/1120/1*CCK9eHjkC9vU22Qolppilw.png
