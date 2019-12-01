---
layout: post
title: Installing Android studio on Ubuntu linux
---

![Android studio](https://www.punchkick.com/wp-content/uploads/2014/12/android_studio_setup_wizard.jpg)

[courtesy](https://www.punchkick.com/blog/2014/12/08/what-android-studio-means-for-your-brands-android-app)

 - Download the [Android Studio](http://developer.android.com/sdk/index.html#Other).

 - Extract downloaded [`.zip`](https://dl.google.com/dl/android/studio/ide-zips/1.5.1.0/android-studio-ide-141.2456560-linux.zip) file. 

 The extracted folder name will read somewhat like **android-studio**

To keep navigation easy, move this folder to **Home** directory.

 - *After moving*, copy the moved folder by right clicking it. This action will place folder's location to clipboard.

 - Use <kbd> Ctrl </kbd>  <kbd> Alt </kbd> <kbd> T </kbd> to open a terminal
 
 - Go to this folder's directory using `cd /home/(USER NAME)/android-studio/bin/` 

 - Type command `sudo chmod 777 -R studio.sh`

 - Type `./studio.sh`

A pop up will be shown asking for installation settings. In my particular case, it is a fresh install so I'll go with selecting *I do not have a previous version of Stuio or I do not want to import my settings*

![./studio.sh popup](https://lh3.googleusercontent.com/YcoXtYpxfhuFyz7smqIdvz38b_ae3RYZDt34opvUJp-0rRnagL31Or6RB_ci2BJuTkrmclaNzW6LnxyilZYGXPBsB27o9RZRlsDPufcaq3-fNXzPXM7gvGD1O6L12hOSv5YeChAImazypVym_JDBFiDrdw5IcmNfaHyTl1Ca9uK_nTF2ZlJT-cAx5XNK-i_bAjRIrffvyzYhmD0VVAyMjl-dbXBM2dZ9jousuyFmp8dHMZ9l8Z6X6Y3J5IsNOlA3wWHZnR820Uv9TvtmJiq0Ov6xEDajqP6obW5oFw0zYMe7llskfGqLZXHRXycjj5Npplt7jSBZWVhjoErAa5OrKXMyDmQMIQ5o3GfsJY-rIzcgHXCqnqwpDRnBNaoBYuan7hyny48tExdJnA0hhaUgQJIyRKU6MHIIrh35vaKGFrG8j_oN1P5OrVTYJh5qpEMQgXLCWWzP-Q5uc1HISrX6bn4lZxmJSgBqOYhqK6H3XoJJ1XVT0xjyFoPIMTLUSk56fHdgiwbGB326onY450UoIRf0z3WlhyapIBxdaqTtm4oApVxurcmxtSS_8Td7QSM7acS1=w584-h215-no)

From now onwards, setup wizard will guide you.

![Android studio setup wizard](https://lh3.googleusercontent.com/RiAYd96BlVPbWRwvFmyecMM_iiCR26T7H5V2TCBypWQU2CBriSx3ZHx4hAWjuiRRPbQ4c0Fta2lG4uxtR5lteSRkyXItCTuVuxMUpnRRsqTQ1cjhou1zfWJFhJCE_f9PDx5WGz6B-ZiLCaMxvK96j1LTwYsJXV6jL9MOMUlGW3cgfEJkGgYcSJ0J9KVrfqOe9uGlgzPnnr-26a-l027FjOjDMSdTDqe1nCohx5SoXr_DQjTcp16_X4bXqjbgVgAgHJUrboBjf_YyO9tKooMU7Y8kU4fpsNBtt9zL-ifgLUFYVMkqVuCklJECRN7V7HMYHjpSyXSBedcDsf6OdcBdVESNVAOCb8ROWXjbNr1Og2I9OWWlJy7okyJrdMr1-t-svCAsp_j-Hzk2B-y0dYWt-ozmtgNFGGWhW4vQTuiiigP5PitqcRjWuzyv2GB1-031IJKk0jFrgHmIwA8-4z5u6ShmJKQNneH5JgkUoAjnAxlob9mo2E88xrtE827WmZ_rSp7pSzmXwDVN5GdHJxxyzBWpzeL20U6BoMtuS-8CFZ86mkQtqOD_eObXBxmt5ofzxwKb=w1120-h640-no)

Android Studio can work with both [Open JDK](http://openjdk.java.net/) and [Oracle's JDK](https://www.oracle.com/java/index.html) (recommended). Incase, Open JDK is installed the wizard will recommend installing Oracle Java JDK because some UI and performance issues are reported while using OpenJDK.

The downside with Oracle's JDK is that it [won't update](http://stackoverflow.com/a/14788889/2404470) with the rest of your system like OpenJDK will.

The wizard may also prompt about the [input problems with IDEA ](https://youtrack.jetbrains.com/issue/IDEA-78860).

Select install type

![Select Android studio install type](https://lh3.googleusercontent.com/ponDe1VfYzuq-1B5fMIRoI-hbIabKjqpNFBXzEguF2lP9gYbMyxQ_ZIoR67gMP-KMG9TcK0YWqwitXaTg-olXxSXSoayed5F3sMQnPFQdBPKvxv9MGACp_4U41T2nDURLPybVQ1Ur0n6hlvXpTFA_jdREft1tNgUL_HsVBlk2OvqhTfJhaYHwm4Mfd1kI2otaVe3riypBJQ3sUmeDGjv3Nnu25VROw5-_XFGdrjMuua_6MjBD7wPUA9g7ZO2dwI26nB8EFKJASxA4HIR42rqcrngNa0aE6gvOR8kHMvVooejAosIwcnQHPpA7g1Mu4IQL7EgCrY9cFFZMRTRE5F0kDWWENzgMjoIIlkA6Z3VUD5bd3P8rnNou57b8VDqqWO0-zuXScJXBDHqSHVjLOXRdTnrA6XZKrMnlnu28x86Wjt4MKuPEPspMEaiC_UapKokOIWOQ1m3e6Yqxv2FRI3Qdq9blPIxcOdfPTheIKY1ood5d1CuRu-pdfWcAO6BwDggu-ByAFKtH1VNC2oOVMfzNMhq-yrV7zATFkTW2qCHYMTabuQI7w57bgQy9LsCApK_N3rm=w1120-h640-no)

Verify installation settings

![Verify Android studio installation settings](https://lh3.googleusercontent.com/WhowThzbS3cUe2uHKuxAsda9-cLZSUWTGxQWPRb5XvBBsNVSb9lA3qGyfO1EjlSns_4Rv-2kV2CdDBG6LXaFwCMmJd5bOyvg0YydSQI8k6IWi8tjPx3Tqpr2QtKAo0y6h2prUGPgee3VdZBABwuSYfKJGPJJsHVqKSK9Yfm7lr0GzD8ils19FuLeBm8xJSrEB3giehtn61rgO-epRnJbJ-T7X3WK7Zaga-svLfiqkDVuI8s1ftGIL9XhCWZegiFL4qxn90WDV7kAVYxBtR8ynCvWgCZITX4HI8w-A5y2oCzv7dd0eteKeAhIZXM7hJdfn0MLic2QZUjBQ2KkVgmPnfIMO6Tl1QEgCV36fMJx5DQtekUJW_n5-EUAsyJqP5OTW-6Gns5RFWZ4WxVlv7kC7bBneYOXkDRvVuvMf2PIgbbpyzgkL-7s7hoPMIFrJbxzaEAx9bZbOE97yMDKbGpMRxgxRxZKZvHcutx-_-P2DFzBp0IblZKfi-fiXbODPo0Q_X5wYVlyjwj8iNjTNmzah-p--cepJ61_SsR7dm3Q-IqAh8rddDBsi3s8TXkG6RcS8lZn=w1120-h640-no)

An emulator can [also be configured](http://developer.android.com/tools/devices/emulator.html#vm-linux) as needed. 

![Android studio emulator configuration prompt](https://lh3.googleusercontent.com/69Or3dy7xpQWKfz34_Rn81nZ7muqqs7AMPyMvtk0kkgPPlRHD5snQ0VtO5q0DbRPY_N2Ulscb3ppkET8T_KLvXYXt0u6-90pud2_oxqIUtoj3GZcBNCjIMJdhVurSIVpX5aIzH9wEidHA0JoCrC_-4ObyooA8LYdgDUcZZ2sr32XmNfSOc2iXxlcxW6wuCvMtcVm2NskXdT-jnnvobi-hjiG6YVQ8ia7v5-CULTJ9521rA8Dmf3tT-oV1OF-uN1h8R9tJ1vy3_5xEle9n-7elHg14ToPigR9_RJSBRenrITAxsIW8f58BBnt5vfh7HlJJztLODDNGgJsp4djeVd79B1cMzUTbXqLgunqK5OdF6K-UMbvf0lhBu0lqhpElDY0hXQL4ZWxRN-XM3o9TDJDNBRESDKxG5sx78hCqBWiu5VcjOsUQX_JEXz9BbjFIiplFs-M1TMNpxllZ6Qs64T8-fIkbS9-tcjT12Bk-JiMlEhlNjvRTfgKG_ftR-kbzjkUcmBn2-VCdZ-FOeEvJyvHef96_CHxUbR0T8lvc6DBNZP2cOkhNTlCcNNqoF_9qyw1Fc11=w1120-h640-no)

The wizard will start downloading the necessary SDK tools 

The wizard may also show an error about [Linux 32 Bit Libraries](http://tools.android.com/tech-docs/linux-32-bit-libraries), which can be solved by using the below command:

`sudo apt-get install libc6:i386 libncurses5:i386 libstdc++6:i386 lib32z1`

After this, all the required components will be downloaded and installed automatically.

After everything is upto the mark, just click finish

![Completed installation of Android studio](https://lh3.googleusercontent.com/rGeADkMAFrGJBHKjTLqxhwO_nH5QiRa3Z9vKOKmBPAcqkT_xveXcm5nTmlFgMY9-4pfKGODm2e_gkCcWgFnqS42kEC52pTbB_EVC2l8QhoZcUeQQ_xhJuqd7O_tB6NT4XFm-ERSOmAhCuiPBr7GHhQmh4JZF3OCyRIUDivF3CTNzyIH0GjM7NFs6Kr5c7Ahpra9S4Yc__BQCsUkyyZhSselUaTwNyFwwzvRrk2ZbLEg2wFHnSM6e_VG4SAWlf4b6gIkQCmK9g1gLqVIZM5vGAy34GO-kYaANdYBssezBOVHTQPdPxYSxLDZTjbfPcJJZMuy7EbE2RgRFBDoHwZy3fTtC3pu_77g2btpzdFLFGSqqp7dAKnML1rw_zUOEnbQn7DrwH67jGbW_uCHstPT6HzDnVjBk_LPxxOxZmIcgqceAcZYB7EWGdBfBu0ELFMyQZ_Sr35gQEf5qd1QnEAy64ZVucnox6gYQAW0qFF-ylfy_IpYeAuksyOGrHAQcT_iZBJ_OIu8KLO4Wa_c-HUV9f4TLY_6YL9l3S29dD2orzuT-xrkNyJ1XulYXgG484M3fWSO0=w1120-h640-no)

To make a Desktop icon, go to 'Configure' and then click 'Create Desktop Entry'

![Creating Android studio desktop icon](https://lh3.googleusercontent.com/vrcyI9RY4RB6eGoyFp6W5TRYmB76wNBOXLuz11SzpSPe8NCggMBePTtRmeSd9NpoOA54CAgT4nnXjgaZ7W2ct-bHS0iziUi69ON09bi2T5gl21Eb86epp-7Sdwb9LSVMDqeIUswVfvQi32hjglVEcQ4DZqoHKvXvq7FMSud7AaK2nHEOnzUIIcYCopKGgRiU8KnNtJVovpOCpNwRH21Rg17zMF4-gDFUvkyv_2g0LSrBS9ObL6VEeNXf3Mf47i51W2vXehVXAZzSEUbt3xiMgLZNrNshSwBE6FRYhxgcNWcCGABw_ldO-faAovINFI9iiw6zld5tfLzV7ScEsnjLHmbaKcqTFI2zpbM8UZH5edXkKfyK1nPQ_TEO9Nybr95r7saiypWoIWP2dCKVK5DYd33e3ZcmtXvG4xTniZwOVJBBQ4h8IzRtWn-s4EgJUlHX_nTP8OBxPqk7pNuGxXURTDPFKRJO6ROH5zLl6FpHwDs39xDeoWZ6TWI55e9YPlr5UfGwLK03UJm8VKA8klc19wJ7Lzr_LJ8WVTBNmjDouaOhsexFWiovN_kqpAxr4odtoY39=w707-h639-no)

![Creating Android studio desktop icon for one or multiple users](https://lh3.googleusercontent.com/I7Wc9WFHt2P2qFvoTgGW3HVwChwKrFy3soi-AL2ls6mTzWKkSz9jiqRieg0BVUlsMGZVEUZPqTpOAzdg3j1JPdDXnOuvCmuASe0VCCXkmboBZQ6WKl_M-KN-imMsU96jj1AZjFGhIW8wXlnJr0NBg4cX5MFyeMKjQxd7zPPrI3h2llcv0b8WBClFoIhzAUvGWhk7Cpj_N3gG2Woyn6CFg6l-Pqt4WB3fSPDaY7Opifh10TFYQuPxAM71KEBpFbOeKiuNyfh0ebU2sd75qs17Cf3yBNxeUNpakFJqUeRe4JiANkFsEQZdFg-969TbOfme8tvStapykTg2Faq6zXkVkS-X6eLh0LZqZ59wVFEsitjj9zO5RrHJEppew2yx0jCQKUB_0SUpuFLxzoRruYip2Exj_lOTjztm230dnsH7jEGo1US4ixqPsTj_zX8tOD_z0Wvfk638c5_ZZY5CbIK1eE9VXHCp1FLgW4707FAFMTFEMZ_41bcCRLg7RHHQwOeJKqO5d42mARtzmROlMRkOHOAUa5Ft7wnh4FEfrbzob1CiB0UYSN3nAusKN9kaBIcHtm14=w585-h209-no)

[Photos](https://goo.gl/photos/4dsusmShYjwgQYws8)