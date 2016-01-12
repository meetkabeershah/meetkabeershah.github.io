---
layout: post
title: Install Visual studio code on Ubuntu linux
---

![Visual studio code](http://www.omnisharp.net/images/vscode.png)

[courtesy](http://www.omnisharp.net/)

If you're [trying to work on .NET outside of Windows](http://xameeramir.github.io/install-asp-net-vnext-ubuntu-linux/), you probably might be missing [Visual studio](https://www.visualstudio.com/). An sub-alternative is [VS code](https://code.visualstudio.com/).

Now, we're going to [setup](https://code.visualstudio.com/docs/editor/setup) it on [Ubuntu linux](http://www.ubuntu.com/)

 - Download the [executable from here](https://code.visualstudio.com/)
 - Move the download and extract it in a folder as per your preference

The contents of the extracted folder will look something like:

![visual studio code extracted folder](https://lh3.googleusercontent.com/hj7w01EKuNwe56sDu-h8tIWNo_uUhfOF9cl0kL1VHTx1p1zl31R_elTqwzhjRfdn7dh0EjKVC2tVk-OMGW77bCNILG6hPo88OBu7fWCSDdCOuYdidZiQfRjTSF_AE0s0vfdIhkYThC5vrfuznbT9HJC-BusHkH4ioqujUBsnO1ABtqy9ODHeWJ8gim8f6TZc5Ena16uab4plfGt0wVANRIwAvpwFYAKduBZnXbxFbfm0C3jPvMsRe8JQQFRL9V0jLiTkVERQux_NBebbokW4rC8E0S49T46e3efMW854L8oiLDi0yZ3sqULf20ylWha9166q5iv6j_EreVZDPdRVUeayVGaV8A-kC__nfQNiRrHgl_8c5kVq-eYa6nxQjmGbhob7vzv_fifP7E6JiIsvpoW-SxCJOLGmaZpWtt2M1Y_d9jwgHDWCjKvGW-H4HOhuL3yh6MLijkOjuM2tqDV4Mn7iTaaHinPWHM1SmoX-WEI4J1N6IaazY0SijkaaUJAWnoLix_N040xC4LtND-jqtf0BfqGwbHv6hQTejGPunxs0F3BfExny3lqiuuwoiggI7goY=w1234-h353-no) 

 - Double click executable file which is named `code`

![visual studio code is an executable file](https://lh3.googleusercontent.com/lno1v_aedIcyTdhEa1Yk62SxcjdN_P6cWaS8dG1O--fViQ-bL-maxxtetiIvnqpJo66RR6CU1kucTQImuIRWqX0r_h8v8WmMnxYeJJHrlG224exL7CBX2ZGwGcrSUyBN766YKjsjDOmU0wFKPHBqB07jiuHd_yCj8cuQbkXYKqGts3IXszf0l0iNGtzwmdkGf_zuD67Dwm6YzcdjlUPa5HTNuhyi4LNXa5E_bvtYgxpowYCuzoFvM_Zd4jFOjEgK3IYSRgKlcc3QyPc-0HruFMDROBH4Mh_YjpaIgUNNrIKWSI0wMRMFgTBwCasvzmD02xhpecWl_T5cAyMQRDDfhD8GSDd-knYYMHyH1LrXBeUAJcQLuJDil36R6LrtrwYsStST8a9i8XX6aPXEQFTP99oQE0ISrM-uysh-whN88H7PINu_ByTUqq2ZZHIA66bEL6KsgiXAR8FiIe4u2r2hUWmj8VK7KUnchWmDBxMGRD1iaI3xCwsYD3GIDaaovzKeuDA2Rz_Zs0OdcFPi0Nx0G22rlBo-Knl4JljQOrKfMGgUEg9X2oVQWrcesNNHmNGQwSoc=w545-h526-no)

For the sake of organisation, I have all the downloaded setups in a separate directory called `Programs`. Yes, inspired by [Windows](https://www.microsoft.com/en-in/windows)

Running `code` everytime from it's folder is too much work. To stay away from it, we can [create a symbolic link](http://askubuntu.com/a/616082/219603) using the command `sudo ln -s /path/to/vscode/Code /usr/local/bin/code`

In my case, I replaced `/path/to/vscode/Code` with `~/Programs/VSCode-linux-x64/Code` so the complete syntax is

`sudo ln -s ~/Programs/VSCode-linux-x64/Code /usr/local/bin/code`

In case, you've already created the symbolic link, an error will be shown:

![linux error when symbolic link is already created](https://lh3.googleusercontent.com/scbRBa5nLd_IoQnXnnbFZicvMfrDEsu-h282A_zpjAzLDLdOdrLuZkhgYExxOczP0c96tlYbW2nPksmELy0rnxhRzRZtzsff-zucSg4qYa7R7EeLGpjS97OU0wfpY3s0ZLol5lWydGdPqbndUaeGS72w6NzKvxrJRQn2VWx2Cf0x62_XJPzlMSROXzNHasqMGPC19tJfw5r4ztrHDDU9kIH1_LzA8Y_gEo-9UXCr8EsdtojTO0tJxrTUSdYy0Zek00ewVwtSOIQCB1_1WzNI2JgUuWR3iqbT3_UmyIzuCveE9QE89c5hFDvyNu2YhIBxlR-_zFJ6LNfM-NOLbsnvD1TQc89VoEGRmo1agL-f1iXecqQgr3cAM_alDd4XHrwQ0tfOQfS_tX8nRTeov1Y4e7uRshkljGxiV9fME5WABdFQ7yHRmKdA4txx9rN4Xh6uiFiC0YQfWdMTH3jZJPvHt9_BZVUAPh91-DnYprDuiN7k1jl6rotbUHnRbTUfM2hyvahOvglBatKaAfk4X0GPKT07xKt_-wSiCy98lhh5lhutF-x44Kr6kP9yOY6zkdpJwmFf=w722-h197-no)

From next time, we can just open a terminal with <kbd> Ctrl </kbd> <kbd> Alt </kbd> <kbd> T </kbd> and type code

![open visual studio code on terminal](https://lh3.googleusercontent.com/-gGXfrVgvd2QWSGg6ZK2VqsDkJnoSI2Sx5reaCgGBrWSuXM79e63Mj9PKRuVksDKZpuPuP7V2o0QQi_xc0a-CtIJk4q3UObOVxPNISLD2MnPagwwtng8Ew7ZKgiu7UDHg_v5opKgqPerdHnFUtgjydPm_eo0CyluiwW6uP3h4jaaXbLtP5mynOMwly9VPt3iEzeQqeYJnU1XGY9ivAEOuj5Q2-h7lM4bNPZRmANgtnDfZMRO6sMh3nlZz1Wuu_Pdnp2qldHJlksk1hWrOkt_sU3uBseMq0TrCAFX5LP2TbQYfifjEJpfAi3lHvDn6M8SX20_9GmHwjmuA1w__GQASr4KWqvF4vahquBwuDPeMORF_cRpDyhVZ_pyX1Qk4lVwlXXrXALnI4fEYpvZtekRLzKf0cyYqbS69UKJpLWodUtk8a9SSMFTbwcg_Q3bIwBkkKNd7NkDcqqDH9ODA0YztSE5364oHnlIV0XHEqm7tH1otALMZ84FmcZLbAIbbz8JaLw7L0ZoGzjU3Nti86ry65YtK2_5ba9l2KsldC7H_3uGfqJxLIYLSAskYAg5GM1OTfUz=w722-h199-no)

And VS code is ready to use:

![visual studio code welcome page](https://lh3.googleusercontent.com/RTMTkA9XdbBo-mzjSGfYSaX0vox9NwlgVgrb7nFV7mGN3jl-tH1kAeXTJ2_CCvonp2xi4xUrE3FC7N1JPozx3NYYXakLno4BPrr0oRfVoHSze7bGyHkeSqd8Pfr_jomLLoLB-GNPHf2cWBrdwoghBoM63YUQtIcpA8ssO98wNY9aEiz7HxIUB0nsrrDXaJ0jUYk3Rtu4fS_FQ7_ETuAv0lRQ72twH6FDBVeTPOSvZlb1xdQpdkyd-Ise3EuszMy7hzQgPI4_cU_Ah8NCeD4sLb3Qq9d6M7TSe8FgGMo8EOW3s3j-a-noagUysJhF6i6-UgUUfIz1L_f2fKA28eN2oO_-QeBuKJ-Qfh9tGZzEx4cFMiTDhWJALPcJKHP8g6USLQ3gzBAUC2Pw_zBL68RMMoeeuQDv5VaJWMWPzNQmsLLgQipaiL-a1Q35yiJtNLMZDQPOHup4aFxWm3bvyhkFQi9V9xvdtZLeUingqKCgSvqgKZkDqhpgqTuDzQYz1rs-7dg9vYieBkZh1ru2QHq8Jj0oJYW_2B7Q3HI7S9moGESX8CzF6ymfXpuKcmhqouxMajQL=w1114-h637-no)

[Photos](https://goo.gl/photos/Mg4vCPgbdUGFsCrm6)
