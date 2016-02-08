---
layout: post
title: Installing ionic on Ubuntu linux
---

![Ionic framework](https://www.codetutorial.io/wordpress/wp-content/uploads/2015/03/headerIonic1.jpg)

[courtesy](https://www.codetutorial.io/use-html-canvas-on-ionic-app-for-image-overlay/)

For [installing Ionic](http://ionicframework.com/docs/guide/installation.html) specifically on [Ubunu](http://www.ubuntu.com/)

 - Install [Git](http://xameeramir.github.io/install-git-windows-ubuntu-linux/)
 - Install [node](http://xameeramir.github.io/install-node/)
 - Install [Cordova](http://xameeramir.github.io/installing-cordova/)
 - Install [Java](http://xameeramir.github.io/install-java-windows-ubuntu-linux/)
 - Install [Android](http://xameeramir.github.io/install-android-studio-ubuntu-linux/)

# Installing ionic 

If you are running a 64-bit version of Ubuntu, you'll need to install the 32-bit libraries since Android is only 32-bit at the moment. Use the below command:

`sudo apt-get install ia32-libs`

If you are on Ubuntu 13.04 or greater, `ia32-libs` has been removed. You can use the following packages instead: 

`sudo apt-get install lib32z1 lib32ncurses5 lib32bz2-1.0`

Use command `sudo npm install -g ionic`

![sudo npm install -g ionic](https://lh3.googleusercontent.com/28bTTaWn1JuJf7nxsq3TSEW4pSSmF2hNcNEOUejrhG4ywKJC2YecWqDsiEXU27-L22FPQmYKi-u6_gx5Ua_j5G_Hcvr6mY61UCOAxwbsYtTMbA1KkOq2rfL9eytSfGfSmpvs8TqIKfp0B5V6Ma9Wk3XAh1sAiRiurqDVNO4Ancav05XJmh05BNqLyEpkDv4MglVIoaLRBacRPfpLAsC23QkJJQy8fB5WbV3VFTpSS06P2AocTHpprCi4s4KLdrant7s92n_mKSIYtqiAkO4VQbFZ-xPfXjCZ9am6xXnWleSBnj_tX1cEBaqh5PXRggIBXMriOWsBT05ef6qK_LQJoMhwy6OVDTYgskqVa4KHtFaQiFnvHoy9wA8GuzabRTyiGkwzC_VM6d2NszP9Urti__TR6GOyKqqq7hFoJMZCKUxBU8VQPXRykPt1Quyj4X_6AH-4VDOC3wY_r-paGKz0ooJW_13LeKhJcBBmRR-UCyxK3t0P0z84Ghr-GgB0U6W4Op81y2TV0HXWrCxWkct3moy-nI2limUk3lmkKrQleEoAUwEVfM5XdGnSBefwZYznKxXg=w722-h417-no)
 
Verify the installation of Ionic using command [`ionic info`](http://stackoverflow.com/a/31540411/2404470)
 
![Verify the Ionic installation](https://lh3.googleusercontent.com/AU5-ZE9fnPTzDlhhUwhA3hR0VDb8qrkP2jriNML4cR3qvq5brysM8i5rpG2k-F84W0b6D0UmFefEf39wT0Mab0xZPKRubITCL0YBAe4kJgJI_0F-gy3cAVARnp-dyRnoBym65c4awMHgkiOh2IrvDgmGuVI2-6ZYHGb8v8fVfE99cxuHlcPYuIPtXj6KCNpZt7AtgGAXkqJEee6fF7YToaVGqA3GCXPeoZS_XrU7UJ4NK5Yys0AdSIhNZIq4iZeFt4rpicbtQp5eHDtclTXo13JCoQgbLBmEfXLMkcMzn4yhY6mQRNpFy1gdt1JD03ZPeZuNM_0v57m04vh37vMUhMC7iR6Qr7qp_W0azPpjk3ax_vmTB6zFeM-gpv4MUugfKCNPqMYMky4ApAzANfI2HIIarodtzx_FSy7YXE_02mh7NjCeH-94YJjnYGEOUv55ccMB6nHtwXkF-gCFakYincfUF_YXn0n6riuUOWdfVH8WAJfksnOWSnH0VAVRP1Kw4Q1c3ERHMIGn23q4EL7BUCWJ5L2DHrwZSLqiAoeNmBcpwVaNBQfnZXp57Swy4zWoXCqd=w664-h165-no)
 
In case, the Cordova CLI is undetectable, use `sudo npm install -g cordova` command
 
And verify if it's ready by using `npm -v cordova`
 
![Checking Cordova version](https://lh3.googleusercontent.com/LQbtTVGZ-MQXyIK7-hZwg0Qax5xPZ-amYzyM9e_hVWUlMHhdbnNAaPCsFBCV4nEyoWNQn7B4cSMt1fJudbOyEf78idD9AR4KhzUteUc7U2H-qeczaMH_UQWd0efQu0T3tQUXtaTErnmh0AxESFKWSBx-Ai6sjo-7sMP2i8f7_Shk36hWvhiVoabBICh_TVId7wWlC_ddABbyCiOic6G1FUiuaBs366kxDwyG4T5pmWNk1G-iJoeXuW5hmqEGaXZNZ_-wIfk_bUv8anDXtZBQFadFU8Kyl0i_StQnzw_8PLZkaKuxml21PdC7I_ik7jft8fTPg-ukkodbuj6Tu5imf8AnpDj2om_kpVUmylPLkYH1PBCgH1FIUVaM2MsBWrxm2_5rz6vlFuOHSRGvwjrXANsvcbj-AcYATxHLO8HQE3C9Yxq5ixoQgm62OtQNMsf9hZM01JBKqV2y76UP5tB1LRYD9Efb6IXfvA6USCGxsS-R_Jfmbb-3RhKq667djuafWGanfuTw7dD1CMRFmCSsrJGLW-6724UJtmJPeDkOAsqtJSAAvtPsYmsc3FqhAkQdUNdv=w507-h140-no)
 
[Photos](https://goo.gl/photos/2MFkc2ZFshm3ZEPYA)
 
