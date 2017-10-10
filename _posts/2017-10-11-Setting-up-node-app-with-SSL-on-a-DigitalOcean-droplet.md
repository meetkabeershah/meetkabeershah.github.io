---
layout: post
title: Setting up node app with SSL on a DigitalOcean droplet
---

![Digital Ocean](https://media.licdn.com/mpr/mpr/AAEAAQAAAAAAAAJOAAAAJGMzZjVlNjM4LWI0ZTctNGY2YS1hOWFlLWI2YTRmMzNhN2U3Ng.png)

[courtesy](https://www.linkedin.com/pulse/five-reasons-why-developers-love-digitalocean-janakiram-msv/)

You probably [Googled it](https://www.google.com/search?q=Setting+up+node+app+with+SSL+on+a+DigitalOcean+droplet) it and are here!
Okey, no more time waste (for MYSELF in future)...

Let's see how to setup node app with SSL on a DigitalOcean VPS

1. [Setup a drop let](https://www.digitalocean.com/community/tutorials/how-to-create-your-first-digitalocean-droplet)
2. [Generate SSH keys](https://confluence.atlassian.com/bitbucketserver/creating-ssh-keys-776639788.html)
3. [Setup git bash for SSH-ing to droplet](http://guides.beanstalkapp.com/version-control/git-on-windows.html)	
4. [Connect to Droplet using SSH keys](https://www.digitalocean.com/community/tutorials/how-to-connect-to-your-droplet-with-ssh)
5. [Install node](https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-ubuntu-16-04)
6. Confirm node installation using `node -v`
7. [Install MongoDB if the app needs to persist data](https://www.digitalocean.com/community/tutorials/how-to-install-mongodb-on-ubuntu-16-04)
8. Confirm if mongodb is running using the command `sudo systemctl status mongodb`
9. [Setup and configure pm2 to orchestrate the node app](https://www.digitalocean.com/community/tutorials/how-to-use-pm2-to-setup-a-node-js-production-environment-on-an-ubuntu-vps)
10. Confirm pm2 installation using `pm2 -v`
11. [Install nginx](https://www.digitalocean.com/community/tutorials/how-to-install-nginx-on-ubuntu-16-04)
12. Make sure that the nginx service is running using command `sudo systemctl status nginx`
13. [Make sure that UFW is enabled](https://ubuntuforums.org/showthread.php?t=1514714)
14. [Setup nginx reverse proxy to the port on which the app is running](https://www.digitalocean.com/community/tutorials/how-to-set-up-a-node-js-application-for-production-on-ubuntu-16-04#set-up-nginx-as-a-reverse-proxy-server)
15. [Purchase a domain](https://in.godaddy.com/domains)
16. [Set up SSL with Let's Encrypt for the purchased domain](https://www.digitalocean.com/community/tutorials/how-to-secure-nginx-with-let-s-encrypt-on-ubuntu-16-04)
17. Keep a [backup of default nginx configuration](https://gist.github.com/xameeramir/a5cb675fb6a6a64098365e89a239541d) (and all other important stuff) to revert back in case of an earthquack
