---
layout: post
title: Running ASP.NET 5 with on Ubuntu linux
---

![Running ASP.NET 5 with on Ubuntu linux](https://lh3.googleusercontent.com/0sxgq8spWKYyayyuUBBTAZB90UaS8N2wnLPrvVQ3D7B-3YMcdoK5SQ-IAOk-D7m5Ifskm62lVf_ZhGq-2JuxKSoS-nJxLHxANDJpwV9rGjP5cgQ7kEvzadAh0-QcRjxYPN-PBuwd_esMRbD11wzEByVsUqLZVhSLa2GuTakMl3OgvchtnA2dEz-dfCRU_Z-bqDeCRJRMxAypQhnKkG0cklaq1SAXprqkMqiJB66KzI7OtmxUsstHqcQpKYWuaV8nOvblt4pLV0caltkfFqUhXUJkV9gyGB4cTrksTZBOix8A5hv63Wexl_JHKNUUvgHrSfgL8TUHwLS2Oqy_CCvl4m2rdT79QWHIn2Qj0FjgQJIF7zKbWCfVsYPUvN34VVLy9HPxIllMEasWeiOc9mIi7HlrdpfamRqdbFPRsWl6B3sQ0ScsXMRDoJ6wPxDV_HCXsuxPn67N64FeTCXG6BHk7zkW-DDBwIclbhsNjpsiVsCTnJ-KqKBI5ZKACXDP12efoqbW_v291B6kbiPCkQztDs5QTuYtXN9g-JZeeIYiSCQamdBrTOA4a2qriq9V0_gz_Z9u=w492-h199-no)

After [configuring .NET on Ubuntu Linux](http://xameeramir.github.io/configure-net-ubuntu-linux/), I was looking at ways to start developing [ASP.NET vNext](http://www.asp.net/vnext) projects on [Ubuntu 14.04 Linux](http://releases.ubuntu.com/14.04/) using [Visual Studio Code](https://code.visualstudio.com/docs/runtimes/ASPnet5).

#First, install ASP.NET for Ubuntu Linux

Although [official instuctions are given](https://docs.asp.net/en/latest/getting-started/installing-on-linux.html), I [re-wrote them again](http://xameeramir.github.io/configure-net-ubuntu-linux/) since details related to [Mono](http://www.mono-project.com/) are <s>less</s> invisible.

After installation, [make sure to always run the `dnvm` and `dnu` commands by adding to `.bash_profile`](http://stackoverflow.com/a/35031584/2404470) using the below commands:

    echo 'source dnvm.sh' >> ~/.bash_profile
    echo 'export MONO_MANAGED_WATCHER=disabled' >> ~/.bash_profile

Verify that commands are actually added:
 
 - Go to **Home** in Files explorer

![Home in file explorer](https://lh3.googleusercontent.com/qNKdbe5SLANvFBO35_1kqJA4R424zia1zgSYAsMYZsig9fWVVuP39ih18XAkWrnsUeRNndMH-nHlWEFrRF15kc1zBEHSdPjX6xCN8hy1zbUzlgIpjZPVXfk6X1ymCE53CBrVfoZD5agsXdl5Nmf8a21lfl1CwZWgW1l7QA2RNBFipI3yf24WPvzipXM-p0i2YnBm1MvbTQK71jxsSJB9oYow8iFujo-rF6lX0Gnefn7vfamJwFjm3MOyXcOn4RMK7IK4SNZ-jhUE_VwNWKhBTCqE7l9Xw-ulG_zcJyWzlAYVRFq-P0luL6mvSo9nhfN9HWlUUWSw0k8pxl0bg1bZO-I7tZJt5klVr6yfp8RNp_F5GoEOWkxCdL35-wXu7Wcs8rtzRSPkMylccEvrjLFl8fdMtV9dO2LTk_32cr8IEmCLk64sP-97sqrTEP_OI17zgTAxp2xBPa1st2ldAc2eHXHymzpO1bHInpx1yppzovI9Cv4V1AwaGOAS2OZ81wwlVcXDyfw8_LI02va4AaEZH8bSfSL_fs4fAQzbYeLEVshInrQc8_4xl06QbgtZP8a-x2sT=w88-h241-no)

 - Unhide hidden files using <kbd>Ctrl</kbd>+<kbd>H</kbd>
 - Locate the `.bash_profile` file
 - Open it with `gedit` or your favourite editor

![.bash_profile in gedit](https://lh3.googleusercontent.com/up-4rd2-wzt7vC9ossJ0RZADJFhQ0NwOqMkQOrtRdaMky6HIOyPnKGhhUbmm80bEVoJPK45yHn0tyCRDJyvwbls8ASHsUXNJKgs3CQYeVE17StRPtTNjd_UbE8W0zZ3eKn9KxIzzgiu0rlXtjEUvwlItlcs1Zi_PvQHUyBkQbRUdGS62GZHdoDGr9AAUff55wsi9eaoAuHGJYlyuKStqH0loYS2Xv8MjroDqkZTJuAVem0e3VXJYYngH_7vVHPJqutoYKA3_7ClEoo454MiCjvbuBAXJdyf1Ou09fZ9tJAXmDQIgxcUrSk4HfqZs62GeTNaPIv2LBlcN2f9E6ZOQaTVG61ubBIdTt2TTc-SuwP6XEIv5eD3T9-ADKOBK5q2iQDpDcpLzYhT-ve0KC2Gg2MOpHSootqN_gpjEVtWMqWcg_YfBQlfX8hSpbQ2k8iF8ZsTg3-VwEnZAbwRtZ_BgKP92crNKT3qtfIKw-ongOgErlVODHnulaqw4ZysAk1QmqFNtJuTnEOh_WMRKQhzNM-erZiJgZIR6CAPDPOE2ankj37d-owAxnbz-XPmB0dgmjUUU=w665-h277-no)

 - Locate the below lines:

<pre>
<code>
    source dnvm.sh
    export MONO_MANAGED_WATCHER=disabled
</code>
</pre>
 
Alternatively, [use `cat` or `less` commands](http://askubuntu.com/a/261902/219603):

![using cat command for .bash_profile file](https://lh3.googleusercontent.com/uTHD-VFvkelKxKwrETcCHGlW5CzqhtWlLXmuiotBAplc_xKOrqsPKb9l2yKat5uILtQJMCd2twI9CXQ_fltWzZv-9xnObT_QpTvjD1WFzdoirsrh-IYu1NHhV0jnXvxMAdZ03li97GFmnyRPWnvK1WAiXt4Zi3FPaQDrkUv6c-ld2sprOivOz--wViw9jxYxL89X-J3PDyNzfHAdUrcxiDces01vG4k7VvWyjymQUcUVxMhJXQZRH7EW55Kgv3f-8HzCeqW7TZdcSActhBal8KPv-IFOA5qTBU32qxLkatf0sAmELW5PLZTPr603oeHkwCnPDZQqtWlf2kk1ScPlON8UkPq1KfcyuYu88Hs5lEXd2My2ZdS_SE-aj3xLCJc--NYxOhsIYOu-zPi_O8vjcMHRNU2MG-mZx_9AbKtTjG1o_dgPtt_VzXX6foILuYsqpwTKTi_SvPWWdM59jP3EMMudpfLFFb-TX10eQM2DK48hrScwfMB7p87HdR6Mm81RIqwnNHLjMpWoE6guT4PwBgVz-q7wAP1PSzImmYMOiRJ_ix49XyKKLQEcjuEvRBY494c8=w507-h203-no)

#Scaffolding the ASP.NET project

Since, there is no **File** -> **New Project** facility in [Code](https://code.visualstudio.com) till now, we can either use [MonoDevelop](http://www.monodevelop.com/) or alternatives such as [Yeoman](http://yeoman.io/), asp.net generator, bower and gulp.

Yeoman is a scaffolding tool for modern webapps. Install it, asp.net generator, bower and gulp using [node](http://xameeramir.github.io/install-node/), using the following command: 

`sudo npm install -g yo generator-aspnet gulp bower`

**Scaffolding the ASP.NET 5 project:**

 - run `yo aspnet`
 - select **Web Application**
 
![generating ASP.NET project with yeoman](https://lh3.googleusercontent.com/3vi6In7tDIe2i4rSvWy4DE6mYIHyTiJVHOTn3Y9fKh5rlly5CYQ47ZU0K5pArTkOwm_JONI8UXFwN2Z_YPRmthz8jxYcrnRFQtSavn17_3hNoOT_PIg4qu8F3SUlt5vXUQl5iwT14sem3I49zINREjHZGx8Zy7c-QSpEljeRE1FTodgG0JXvGFs37RZtA3nwLynutdxzLO_tlTam3kII34x86-tls7gO1H7lVLbhyQgIAgYXsXTa5l1ESmQHABXs7nfpba8OdCTUB4ks0DmYpgvccHuXdyRGrLRURlLJ6ZoiVMn__L8cgKpHVIWi-b63Non6XhJVvPmFZpRx32fQCu2qMrPNgynTjtCX82D30E9ebeIOmZEVhDrBNsnuXqOfBNgisgCo9uR5Vbt2bflQ__VrYBGHeSxCQrw8oP8tGYOUdk3Ku8wkdYxaz2YxJhvN74jeK0QwD7IeyAfDYySZCnXtL-3qXbdIgmvy-Zv1N9sW0bB4xMk3Lt5W3-VeK-5pnOgKBVn2sHTgd_Ytes5GYRPWRKhyM652TVGhO8dGOOCk0_CuyHN2p62IAhBbgutoRB9j=w1091-h516-no)

 - give name to your project on **What's the name of your ASP.NET application?** prompt, I named it `FirstASPNET5`
 - go to the project folder, in this case using `cd FirstASPNET5`
 - install the necessary [NuGet](https://www.nuget.org/) packages using `dnu restore`
 - run the project using `dnx web`
 
The project will [start running](https://lh3.googleusercontent.com/IIl36_X3S5-bs3qkLqTH_DN8vuUkKLf3QuTuVnlhdTgFwQv9xHYl70lveYXoYN6tBgch5kjYJrQgQk7uUMbb6lrmT5xoSZuXyLJdvmnd_Ly-RkYs0TgMYwrMMKsUALUFr5OoxPKmozc_vvcyJGuODf6cA52H-CbJ1eGbi0_wMvKCDv0EVmLqX342Q2t8qXQYTNZ9Q5DZojlrk9iYQGeM-rh-pwkh83hF9JVOZlCxOmiPoZfeEf7xIc6yTWiGOEHyd4j4FRQDsZbd7fIaWm5VeJIrZmXqBlEmpKqgQMdHDHHGw-Yxj3OG7oH7vsyUDkk88c2rly56eQhQLaaE0UsbDEPAVpzS6vKDQ3QbbrkNwJyBb5lKJH2GdhvUBqJkShMSpeS3yPZF310f_kv6rJIr6fE_bKl2XcQGUYp_ANzuxPYS9Ueptq9oubNAHD5j6GJyC7mSW8cw4OAGAMXeh21XnlddqZAm5S35XlKtkp0bXqOd9e6i3vA3iRPmDwnysRrYCyeCigw9tnZt35DUjXBlY-5SlsCU_wosAGl5W7knmt8TcyA6V0WOfUeeReu6ryttseE4=w722-h462-no) at [http://localhost:5000](http://localhost:5000).

#Troubleshooting

In case of errors, [upgrade npm](http://askubuntu.com/a/480642/219603). In my specific case, the `<VERSION>` is `5.4.1`:

![Upgrading npm on Ubuntu Linux](https://lh3.googleusercontent.com/nFUbK778yH9ONxdn-q2Yuomrz2LCn1qbHXW5S7HyHpFUdfr7F32LJxoYxLMhB_NSmyuCDizyYE__ElNkgzsfBOlV6gxEj9tpBzVDhKxc6URr9ingiaEV-Y3RyApJaI1hFElgfDjBIfVTfz1OjWVqz2F55EFGv7pcqSJYNe6VPYAyp5qNaSESMJFsGWDLaI8cql0NBjCkA1l0YOR5al0rY_V31C8QtwGdXvdQUCM3OV5pdzOR13jT51xMIJNqgeWv7rt-RJUtZzwZXPqLjf4sxEITigl411qw5RXV6EWQQ0S8xHLVDsMIkoldpjYF8Kdl8G7aj4qPLlzZM_SUWKXGKE5QfIrjCG584Cpu6k2j1N2AJyXL6d3qnGGxaSCnuhZGWlEMJMeJG4pIhwQ-x8ESl5trJyNshkMpsWO1c3BQxRVXCxdyYkDUwoRJ-tbGDC0BRoBOf1umtFo-_wWIKHMOyGQQlKZmJ_GAmhBcKis8qxZDr62yHHimsDx-gC9GC0X9BZa-AVMrsvgJg2QRWrNgLA67iQa50XZNsxX-AzVXiJ20tFODF8gTTmb8lL5-Gue3s3bn=w722-h462-no)

Make sure that Mono is latest using `mono --version`:

![Check Mono version](https://lh3.googleusercontent.com/g8eJfx3yyNx9ApVmP5jmpo_rMVHeScwpoXZ10sHZlyOl9VW-18J58oDiwXMqwo6InTmM82t5v0y_efg5awzQ21DXs19BQkZFeJ7XIflWI4Pg-HIF-i6uG6NL-luJm3gjCrVIkqsy9WwUcI9hy7YysqC4OYAm1dp7RWNwjOiI3h8TZibXP4qyr7KJp2SMxVXs2OAOq6Cqb-gQfpDcrIrzJkTrXohmLZKY03lkwn_OyFWQuwRjj3mgyW9v8enCWEb4XYp4MaSvqDMWOiBxvR0MIYacpdxwPoLe1c2moXbvJ3Nl5AZIFVVdevVh99bKXY6KSTM16Leij9guW1nqDdZtA_78CN8Mo0sc89mP1CWu5DiopeqgeEc6sncGC96EoyiNiqPYAl1N-ytTtK-I3PehGEp-bJhvVZvMOcCEnqL_kEDErAhbK7Of81WrhGP4BXyr_8RaSUyXOfF7mR2YSoOfZPGQyUFBr7qExy6cfIyOi_QlKrVt40nCheaLD9Gi8A9rPFPRxFgzVC_5mmDf9SmAOfm5ZepXl2a2S3z2azONRtlNtdrtfdpuvwpQIjcoGqiLeGNI=w722-h303-no)

Also check if `dnvm` (.NET version manager) is latest or not using `dnvm upgrade`, upgrade if not:

![upgrading dnvm](https://lh3.googleusercontent.com/4zlg7JmHDBscn4X0CmbQcFqSUljf6XDArRHBliSA6bPCV1QVFRYNqqg5vIL5Wdta0QeHPf56QuzQS-fxWz4UccMYdyTtotPHlACIVnkWa_lcv855ZkfDl6sXgZKZ5a4yb5DgubHBZ0hkr4yfXgJaM_4JF4a9FTYKNamF9AlHGmFLANWekqGkmbocmmx8xc_8i-N0QEfKMcgt1Aup3-wNgCwV7s7q0uESEeSgozT-W44uSzCmWFxRziPw6ebjaM69UGlsPNewxpWoVzBy8PiWkEZw4pOFcN1mb5gtiYH7eDyAVFgGpXVGFd4XS9Q0Q-C0s4a7D86-AllXO5t9Bh2Xi4qX0gi0eXJpBYucV2ATJi7bNYAY-QUA8LalD5W9HZGujjV3fYmRkKh4KYY4329mGHBi6KOyJlK6aXfRAPOWL7PG3fy7mtaqnKdp94_MxUld14JcRyccvQANVZo_byBRyK11njiBa0tuR5pB97HNlSIWRRGgJrC_GGe8Q_1tUayEH9b9GQfLoEOHpxgx40Swiq8JiygwKXHk-GnIMmL6xDCb1JASO4fufeIXjwyPdVQfJJbL=w722-h236-no)

After every piece fits into the place, something like this will show up:

![Running ASP.NET 5 with on Ubuntu linux](https://lh3.googleusercontent.com/8XYNP8wNLEPU-4Xs06l4T01jrgRRbKjdSmCw0k5-lDd5n60quUqxJm0SiiJKuPPYlMO3nbZAgYkmDeBKNcgVMut5gwCrZ5PzUuabJ8pRLl_vniRKmaULdXfvqR7prnx823UQP4aEapriD9ykjT48oG-9qqEPDGTZL5lLTFZk38zVz65iou25hkkSIly6NfJiSKMynav7EgxZOE_RIIjC5ex3XTPlS6kWTUTN1TD9VFg6VCgE5rTs6PhmGOYi1I4CjuNWBOnpnz3Ck8CsIGjoITD7QKdhaiOR7zW19CCUsYhjewLgOjtPYn55RcJdl9MePHvmcIRRWpTUe3xjc6it98GLquqIzTti1jf2Mv8ahpmKBOefOi4j3Ntv7fhpSKIWW8LEp0s2tx66vR0A5p9-cQq99jr8-EP8WycV7Zud3oVQNEgW3nJ5NYdsYWeqEZERk7F1uqrx3vsgu89x1p38s3J3X1lwqp1ZwK9_WEeQGP0kEP66ZazfIl-O3exdZuoxoJLEYRpeIpuX-zoeJ7T8LkS3HixEzGomRKgSil8qr_lS0Ok3gdGJlVh5id3IonXkKSLs=w1215-h683-no)

[Photos](https://goo.gl/photos/GVXrTLg9ugg1h5t97)
