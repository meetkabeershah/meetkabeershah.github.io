---
layout: post
title: Installing Mysql Mono.NET connector on Ubuntu linux
---

![Mono](https://www.bluewhaleseo.com/wp-content/uploads/2013/11/labimg_940_350_4_mono-project.png)

[courtesy](https://www.bluewhaleseo.com/blog/asp-netc-linux-centos6-apache2-ispconfig3-mono3/)

[SQL server](http://www.microsoft.com/sqlserver/) is considered the best database for [.NET](https://www.microsoft.com/net) on [Windows](https://www.microsoft.com/en-in/windows). In my *personal* opinion, the analogy with [Mono](http://www.mono-project.com/) is [MySql](https://www.mysql.com/).

In this post, we'll see how to setup it's [connector](https://www.mysql.com/products/connector/) on Ubuntu.

Go [here](http://dev.mysql.com/downloads/connector/net/) to download the connector. Select `.NET & Mono` platform and initiate download process.

Extract the downloaded file and move it to your directory of preference.

An inside view of the directory will look like this:

![0](https://lh3.googleusercontent.com/nN4pQvDTU2ywT4RKpV6XVdYgZ7Pw_8CS8v2LoRkDZ0vW8LpLUU_FKUkdLWbzeMO5iUZQ8_BDedjAn8aBF1gQUdnV9sp48p-LpaNJ6QwMv2LOtpn_ydwMK9EUPJwkrFo407xvGgOPGwxADctXYpvCsbcos7sl2PkO_lAdtYus-v3YwBr_C6jG1clLS_y2hJ_ZrYDdxihiCyK4WrVGhSww8tQnGKIBEmC_7EgCc6zZS8dH_PjNXIPZOMHJcOgKsUFqAr-ZXjJoBFtCY_acAVfnUelIL5lZxSbaBSFnexLwGn6CMqPmHef6W1qnlLqm0w_NE03jgftWLm5Zb-f4sRNUbTQFjEkCRFjrCEdC5xnm7J27eXuB0fKwER4OuZO6hXjpJoEEZSkHcRumubCTsmeWi7DAqUf_4WtvSvqDr_gPgdz4YpmyoaoptX3BeONJUrJIWZOoSqJq3DnUH_gJM2gHvyN8T8z97p5-vkJOXkeD-4zi2j2tMHqeTiuzSX-f4rAwNynX6oI8buzFwqK6m6tQgnIAcO0863MnGZB6oqr798le1AnxN_D6a-Stjs7uPkbJbncQ=w1104-h262-no)

`cd` to the directory and ensure that `MySql.Data.dll` indeed exists by using `ls` command. I went to `v4.5` to make sure that I have all the new patches.

Use command `sudo gacutil /i MySql.Data.dll` to register it to Global Assembly Cache (GAC)

![1](https://lh3.googleusercontent.com/vjIRGDgAHD9RzRpZObBQhE9er3XsbNFNlTfFENzNakWBS-DQB3zU6yWiDpQenX8rxZbF7Z3jlSUrwHsFBpc5ZtKATbQcA2WLNpD7WMg6Aw8XXPLxOyBYbVzLvEtee6-ocrgzrsjyzXR-zAuqvMRVDWuYC0KsxKouP0uWBpwoZL51P0kR-mkzlu09sIQ_AvEC2vOrT1ZNFwa9EMewbWChOrZdkSFtuDRA6-vTl3yY8L9vYAHQDwGtmmDmAr3t-rGK5-UO0GT7COUcjQyWP4uvNUEpkZ2EASZnxZONQSCb8J04wkDk2y9TlGPfOAomEmiQVzynE4CeFzkIxjKhz-L9PZTceOUtvGqQmXasauhhV9WUV6WcLwTwi__eSJDWrcq5953-sb3RnpWvumaQRIQQx79o4-UnX7rzCraET1eRZYMlIw6kFGlBpWVjBd-niCSQXc03yBMfDOFr4b10Rmc5580JCnDMj17llBgcPbY5jDbKMfc3u3RSrLXZ4izTG0-98A7qeMwPv3Rl0ZC_E93MjGdGiMRpuTxt84YBIqpOB0KPaVCSgfx7t5l2_k4DsE-Z2Yg3=w722-h180-no)

To confirm registration:
 - Go to directory `/usr/lib/mono/gac` by using command `cd /usr/lib/mono/gac`
 - List it's contents by using command `ls`

You will find `MySql.Data` if the registration has been successful.

![MySql Mono connector registered in GAC](https://lh3.googleusercontent.com/ImIP4NdoCwBJPVb7SxIfjS0jJr2CcW34JayIXGDzYY9rmhkEOM8iF-h3JBfy1cTmJ7YLIZbw0CE_3oZnov7m0Vhh6l5Gk8BzH4eASb-yXBeHNBolMVBDPpxK9MFN3ILzIsPkSrSJShrKsRLZKoxw7FMiXW7l_4l9bbDz2phmJC7u-rsJ3_9TWUo22cgx2tog2kcKEkrKM5bUA-GJsfW9kFmlmZ_SBtvUbeMyuc9TT3Pr5eKanW3EvIPXylIaIdKYF4b51qlExbVcQmI6OOAzVLwUs20zmqaBI9WQOwPaHwtHerbqh068p7fzfH2dz1hCj2vs7kVMpYcQst2YD2999vouJXqzV1DN0IkU1qRMoVSKtHtD69a5c75KCBWALctOSaMUo-XDnNHmm4qX2TfZewD_4PpE9FGdv8XhAFcBcLrirK49th35UCEYUgs-LUIHY_PN0SRqx4SM_31E1pvuYcyBtHYdzsyvvLMnms3eLmCtU_kxp2pKLkIJLF81WLtQ3ZegzoX7zC5U2kQOIGPoQb6p-HPyEUlGCMt1ruKCRGfI1DAzVcrb4jp-Wb_hAJf23RvO=w722-h138-no)

I tried following [official installation instruction](https://dev.mysql.com/doc/connector-net/en/connector-net-installation-unix.html) but [didn't found it perfect](http://stackoverflow.com/questions/34357752/how-to-identify-javascript-undeletable-properties#comment56457971_34357842), the above steps were tried on 64bit Ubuntu 14.6.

[Photos](https://goo.gl/photos/A3gzYoWUq2LDBq2Q9)
