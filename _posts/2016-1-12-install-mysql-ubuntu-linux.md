---
layout: post
title: Installing Mysql on Ubuntu linux
---

![Mono](https://kaylesblog.com/wp-content/uploads/2015/08/mysql-logo.png)

[courtesy](https://kaylesblog.com/tag/mysql/)

[SQL server](http://www.microsoft.com/sqlserver/) is considered the best database for [.NET](https://www.microsoft.com/net) on [Windows](https://www.microsoft.com/en-in/windows). In my *personal* opinion, the analogy with [Mono](http://www.mono-project.com/) is [MySql](https://www.mysql.com/).

In this post, we'll see how to setup it and it's [connector](https://www.mysql.com/products/connector/) on Ubuntu.

I was trying to do some [Mysql](https://www.mysql.com/), to support a project which need it and can run on [.NET on Ubuntu linux](http://xameeramir.github.io/install-mysql-mono-connector-ubuntu-linux/). In an effort to get everything out of [Windows](https://www.microsoft.com/en-in/windows).

During the process, the [software center](https://apps.ubuntu.com/cat/applications/software-center/) had some fever:

![Ubuntu software center greyed out](https://lh3.googleusercontent.com/BvpG8vJouknr4XJKWvu-PGsYkJalHlFzz4bK-msxjmjvPmsmXrUnF6n2Cj9cSj1v4cGMM-MeQZVlFjPbpifHkBFMuyzGmyd095mwWbJxa50m-sPbwqERYu1JBAtjp6IWywnpz-2hziNC6mhPC9w9GgNAqFA7Yw5ZPhvev0tkEHbSHKPh61dKQTNMUlnTF_pWZWVwEVGgXw-N5gWt1ChUVCK8nR5XFfM4WUgkwLnJRxOoIb8-o1RT-TLj0138utco2EbPyW_uZ5IQV9Z23U0LXnk7Ws1jPHTNxpybqFuPa-8rG9S2UotWoU0FTkAEq-DmY7jBBUg3pidc52feU294M12b0KdwFVvHBKtSZd0zGCVkPVJsQ-tAFDVAG_UcV6D6FJ5ltfeY0Sli_e1twoOePDbnSNXg-MqbRJvgwnlWBav9mawXLdjMTvjMRhV9MylHm6WuSzSu1aaX1lrsr8pBHdvE5vFdQN4r9ObIBKI3TGz5dVmjh1sTgDv19ZC1fWUJthHCBNBq4km83y8svw4L5Yw9WA417J2SKdy9bpI1sS5J3LImXe8CmlsXrikSxRvZ953h=w1166-h682-no)

Initially, I tried individual installations of [Workbench](https://www.mysql.com/products/workbench/) and [Mysql from APT](https://dev.mysql.com/downloads/repo/apt/). However, since I was not 100% sure (and the above eclipse), I just [purged](http://askubuntu.com/q/151941/219603) everything and followed the [sure](http://askubuntu.com/a/323715/219603) way.

# Setup Mysql on Ubuntu

Installed mysql server using command `sudo apt-get install mysql-server`

Gave password (*and [forgot](http://stackoverflow.com/a/5683179/2404470)*):

![Enter mysql root password](https://lh3.googleusercontent.com/5psh3R9Fji2_bSKk4nPiA7u2kqN37rMV5l4Be-Ra_WamRh01SNvu-CapGsN9UZgfyNbw1-DpkNHAZreDL-1e_3Z_bSxfjGmiMoc5VihcbrwS7_rB-MVKGUEZUkg5qlYJBbOrvWh1GYwBDaGRylvcxeg-txyTlPx8n4oO3nE_-lrLR0GmNyxkK5vLdmIBaJemWlvXS_7tdcA8G0Dx2xAx1qyWdi3-S7MI-GEZU1DDQe2Pry1vt-3FjqDIJgtUeeX3LpwETk9v9Fx0tqvAbRqwjbvb13FAMKPHqLcrFlgu_VgJ_iBVAGfzubczs9bibmZw2VC4dX2msRLYSxZfbpvbrpW7TTs6vh--21SAjmREDHT90vu_FKdVj0N69yMiQQpXLQStUaOFmliMAVBCTNxhmS34lJ3wJLS9K5PGoISiPB-JweQxGgqgFgIR-wMBusS9f0P7T-I4zktk_5FyT3hyA2Q7-HA6VwXrOXrtxwyeMPZOCAwWhkyiFDW5GWqxtFRHTu8BeFdrOBGvfzxEa13hiOEKH4THU_yoBXqa-0UfeUxYp6ByFwd3ylHXTEtshgshXuXq=w722-h462-no)

![Re-enter mysql root password](https://lh3.googleusercontent.com/5psh3R9Fji2_bSKk4nPiA7u2kqN37rMV5l4Be-Ra_WamRh01SNvu-CapGsN9UZgfyNbw1-DpkNHAZreDL-1e_3Z_bSxfjGmiMoc5VihcbrwS7_rB-MVKGUEZUkg5qlYJBbOrvWh1GYwBDaGRylvcxeg-txyTlPx8n4oO3nE_-lrLR0GmNyxkK5vLdmIBaJemWlvXS_7tdcA8G0Dx2xAx1qyWdi3-S7MI-GEZU1DDQe2Pry1vt-3FjqDIJgtUeeX3LpwETk9v9Fx0tqvAbRqwjbvb13FAMKPHqLcrFlgu_VgJ_iBVAGfzubczs9bibmZw2VC4dX2msRLYSxZfbpvbrpW7TTs6vh--21SAjmREDHT90vu_FKdVj0N69yMiQQpXLQStUaOFmliMAVBCTNxhmS34lJ3wJLS9K5PGoISiPB-JweQxGgqgFgIR-wMBusS9f0P7T-I4zktk_5FyT3hyA2Q7-HA6VwXrOXrtxwyeMPZOCAwWhkyiFDW5GWqxtFRHTu8BeFdrOBGvfzxEa13hiOEKH4THU_yoBXqa-0UfeUxYp6ByFwd3ylHXTEtshgshXuXq=w722-h462-no)

Set up [terminal](http://askubuntu.com/a/183777/219603) client using `sudo apt-get install mysql-client`, which can be accesed as [root](http://askubuntu.com/a/548703/219603) by using command `mysql -u root -p`

![run Mysql from terminal](https://lh3.googleusercontent.com/Hp9pT23KFMfpiAHHL2Lrlr-1IomrG5PPro1IcLrTd8lBgt_WVAxGYFRMicUP8cbTmk14J2y5gxRIZkdXqCEaJ5w0INd2QlCrF0tcknlbbQ4n1_9t51M8-H5KW5jiKuUuSbz-1rR5HWPW7BQImUO5LQSheLSt09gjMoR7q6xm1RL0jGqB_gIDoHriuhOiVv1MJO2Sa1WAOjQKuMpbCzaU6KdRcm-tddlh9Y9Xw1FCjcGq3CW13SQ5Sd_Pccu6J1u6Td2pcPIyK8IX9jzI7oL30--EZ6thAS3Wf65bHFw9Hlfy1Lt8xsBwAS2U5CE5nR9CWJEZPushJwyE7DlCksCWkrgC08yZkxGDCyegv6Uop2EtBNi32i15ayj25HtmVko8LVxqE3RELXAbCg1bwHOCTZZSFKJejRT7LydijQjLXlUcRMHxRlv_nXOQDhvfXd3zAC2whtilXfivvwkJyF2ec2kyFsaTUwCyPxkK3tjurnsMubALXk48-_2_lMvJwX8vAvTf03V_rNTBUo-3iAPc6-mkEiAbdbBiJiwxMQ_qnazjXfpmNVWWcMHTnGWoo-w9HbAI=w852-h339-no)

And/Or from [UI](https://www.mysql.com/products/workbench/) using `sudo apt-get install mysql-workbench`

![Accessing Mysql from workbench](https://lh3.googleusercontent.com/2Tb-zqVp5nBgt04cTTjT1hUNnAqG8qxyf2wo8PSUYUdsTR4HC6GzIKW6S-Ld8wDWTJIG74es8XR5NcXAs8qTVEgV5gFFW5Dz_oB33A6gSnJXSxcL3u6olxqe0t_z9XzgcdHCg1Zl9w0UY9IVj-MVbGpSnPjwamoYtyOU6zQzKHym_3rwXeu4iUr1alY3D_mk9DvaxKc7TGPEhYf44EXR-Porb0QsmQ6Z0qWr7aCtw8y995VsAq9QbH4XCCqLfORmLfBpR8lqC0N_eqzgFwIwl7pdkC-vAZvaKhGOzt2OtYu2x8tAOE3PpuizYMy0LNTx1qcvizthrQMFsczM7ObibZJfUrAgl2R9duZo7XXG1y0Xq8VvvuipvuXnlWIzLG_xjpRGrs7Um9E4guBKeveZi4hH_v0LVSOEnKEUc-CJi1iU-6_Y6bzpmhU3WNokvDE1dx1DixIBVBN5dpjh-D2fqnWzYqSCEuzQz7RVYlBybDU1alWo1zqUii0S6GZFIlTTXLPbxYUG0lr-vP-P952O7lvRVx7z6Vookb30L56mH6IC6oja57x6ewRAif9UOxncUDbB=w512-h293-no)

# Setting up Mysql connector

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
