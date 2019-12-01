---
layout: post
title: Setting up node app with SSL on a DigitalOcean droplet
---

![Digital Ocean](https://media.licdn.com/mpr/mpr/AAEAAQAAAAAAAAJOAAAAJGMzZjVlNjM4LWI0ZTctNGY2YS1hOWFlLWI2YTRmMzNhN2U3Ng.png)

[courtesy](https://www.linkedin.com/pulse/five-reasons-why-developers-love-digitalocean-janakiram-msv/)

You probably [Googled it](https://www.google.com/search?q=Setting+up+node+app+with+SSL+on+a+DigitalOcean+droplet) it and are here!
Okey, no more time waste (for MYSELF in future)...

Let's see how to setup node app with SSL on a DigitalOcean VPS

1. [Install Heroku for it's versioning feature](https://devcenter.heroku.com/articles/heroku-cli#debian-ubuntu)
2. [Git push the app to Heroku](https://devcenter.heroku.com/articles/git#deploying-code)
3. [Setup a drop let](https://www.digitalocean.com/community/tutorials/how-to-create-your-first-digitalocean-droplet)
4. [Generate SSH keys](https://confluence.atlassian.com/bitbucketserver/creating-ssh-keys-776639788.html)
5. [Setup git bash for SSH-ing to droplet](http://guides.beanstalkapp.com/version-control/git-on-windows.html)	
6. [Connect to Droplet using SSH keys](https://www.digitalocean.com/community/tutorials/how-to-connect-to-your-droplet-with-ssh)
7. [Install node](https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-ubuntu-16-04)
8. Confirm node installation using `node -v`
9. [Install MongoDB if the app needs to persist data](https://www.digitalocean.com/community/tutorials/how-to-install-mongodb-on-ubuntu-16-04)
10. Confirm if mongodb is running using the command `sudo systemctl status mongodb`
11. [Setup and configure pm2 to orchestrate the node app](https://www.digitalocean.com/community/tutorials/how-to-use-pm2-to-setup-a-node-js-production-environment-on-an-ubuntu-vps)
12. Confirm pm2 installation using `pm2 -v`
13. [Clone to a location in the server](https://devcenter.heroku.com/articles/git-clone-heroku-app)
14. [Start the node app for first cut testing](https://docs.npmjs.com/cli/start)
15. [Start node app as a process](http://pm2.keymetrics.io/docs/usage/quick-start/#usage)
16. [Install nginx](https://www.digitalocean.com/community/tutorials/how-to-install-nginx-on-ubuntu-16-04)
17. Make sure that the nginx service is running using command `sudo systemctl status nginx`
18. [Make sure that UFW is enabled](https://ubuntuforums.org/showthread.php?t=1514714)
19. [Setup nginx reverse proxy to the port on which the app is running](https://www.digitalocean.com/community/tutorials/how-to-set-up-a-node-js-application-for-production-on-ubuntu-16-04#set-up-nginx-as-a-reverse-proxy-server)
20. When reverse-proxying nginx server, keep `try_files $uri $uri/ =404;` inside `location` if absolutely necessary inside `/etc/nginx/sites-available/default`
21. [Purchase a domain](https://in.godaddy.com/domains)
22. [Set up SSL with Let's Encrypt for the purchased domain](https://www.digitalocean.com/community/tutorials/how-to-secure-nginx-with-let-s-encrypt-on-ubuntu-16-04)
23. Keep a [backup of default nginx configuration](https://gist.github.com/xameeramir/a5cb675fb6a6a64098365e89a239541d) (and all other important stuff) to revert back in case of an [earthquack](http://www.n1ads.com/data-recovery/pics/raid-server-data-recovery-services.jpg)

Notice that we shall use services like [heroku's git feature](https://devcenter.heroku.com/articles/git) instead of the globally famous [github](https://github.com/) for version control to keep code closed source.