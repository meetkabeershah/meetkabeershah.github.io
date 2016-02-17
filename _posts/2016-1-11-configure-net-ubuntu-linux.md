---
layout: post
title: Getting started with .NET on Ubuntu Linux
---

![MS with linux](https://pbs.twimg.com/media/CPdDZ2XVEAAgIA6.png)

[courtesy](https://twitter.com/sjvn/status/646381868133273600)

Since, [ASP.NET vNext's](http://www.asp.net/vnext) [open source](https://dotnet.github.io/) [.NET core](https://dotnet.github.io/)'s [`1.0.0` release is nearby](https://github.com/aspnet/Home/wiki/Roadmap), I was trying to get my hands dirty with [.NET](https://www.microsoft.com/net) *outside [Windows](https://www.microsoft.com/en-in/windows)*.

# [Install](https://docs.asp.net/en/latest/getting-started/installing-on-linux.html#install-the-net-version-manager-dnvm) the .NET Version Manager (DNVM)

First install `unzip` and `curl` if you don’t already have them

`sudo apt-get install unzip curl`

Download and install [DNVM](https://github.com/aspnet/dnvm)

`curl -sSL https://raw.githubusercontent.com/aspnet/Home/dev/dnvminstall.sh | DNX_BRANCH=dev sh && source ~/.dnx/dnvm/dnvm.sh`

Use `dnvm` to verify installation

![verify dnvm installation](https://lh3.googleusercontent.com/qQFjNyFUZHwM4wj-5hr4XLrUEzK97CijVOC47dYXqBizF1xk2tUEoI8p6SfG3EAoCfwjJWYpsiRN4PWCTtiy8hI2Sf5M40zGVraTt-RAQ7oUrAVwse0rX5ZupCRnQSuDWhQCKKoxMQhCqFOJKZfJsez1jSyNgJU_jyZYOQvWsOWya8D-YelZ0cSfsa2ieYYc1rGWaarfuSpRfN_zRZfcUrf0YEivfXU-qM8XZMGjrYIrUWO4AiopnD6ZrEVtqO7-r1jj4iJvN7sBUEUyQSOorevyEPXDXOe3lqOlgmsxGY5FFPmYc51NZnc0Uw96YCGT1VmHgdsnWf1Opo5GUSBpjme1tKXU3wrAY1KSSwFE7QBjs4JKGRpUx5SmuVPKZaSynti1jM8rxyA_1TBOfrowIh5zdm5tqSyz_p6bfP5613XQLTCKFftw2a2R5Zh6SQkCXjhV8NjAuMb_8ukQw7qRWsv1APSJs_5ap8rKarND7Jr7L8geX9bCk34EWQzKsGdP9kBvX166cwpP9cZmnxbddxsEOfrq5YQ1uabmktDGPySJbG_cDMgab5-xk4BoSimN3Mt_=w1086-h395-no)

# Installing the Mono.NET Execution Environment (DNX)

[.NET core is still immature](https://docs.asp.net/en/latest/getting-started/choosing-the-right-dotnet.html), so for the time being it's better to at least get started with [Mono](http://www.mono-project.com/). 

The below [commands were tested on a 64bit laptop to install Mono](http://askubuntu.com/a/607055/219603) on [Ubuntu](http://www.ubuntu.com/):

 - Add Signing Key using `wget "http://keyserver.ubuntu.com/pks/lookup?op=get&search=0x3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF" -O out && sudo apt-key add out && rm out`
 - Add Repository using `echo "deb http://download.mono-project.com/repo/debian wheezy main" | sudo tee /etc/apt/sources.list.d/mono-xamarin.list`
 - Update repolist using `sudo apt-get update`
 - Install mono-devel using `sudo apt-get install mono-devel`
 - Install mono-complete using `sudo apt-get install mono-complete`
 - Install referenceassemblies-pcl using `sudo apt-get install referenceassemblies-pcl`

[Verify installation](http://askubuntu.com/a/423556/219603) using `dpkg`

![Verify mono-devel, mono-complete and referenceassemblies-pcl installation](https://lh3.googleusercontent.com/rdfvoQiVOeNtzC1cCaYe3SpkGZgzaSKZXNpyidq_kEwRWUPJ467gjZrDnekSn3_MxWY_zaRHoNOg4-rI5olRSICZWlb8RfleqAVEHnW1UO8Dof9X6r3aCSQl0XHCgv_ov0rVigTfU_uJprLcRFk1-d3AGCx3TXuMAPCGWB8_d6leH_WxGaCbYRm-JF8h_q0kTMnL9LTcelxgIADYtOXJ_7Q4uQ_t96JU2zH7K15N5NPXjtbDo5NzOgMD0DY22DRICWxIk7Tr1OYrdQgJL_hzBWnzoH60fVacEidqTKHZ73xy5vkdBgRyXhC9mnLBL9oA91An1FKi1AqTt7B04anVVYSfTa5WhHKJZOwYdlly8teswo9JNFrRUB70ZdbJd-3TcFh6J-1aOmMHsAJ7pJbE8DOD26BsyQnDmhgAdYt-nHd3ciOyEjCCbWjTa8vRv1VfXeyV3e9Pic2gBPXWfqxPCWl864mpQHSrFXV4Tsf8xfKGXC0FV7SmuzbWCSy63U_7z9jjQPDhCxbiTMkmJ4TL9djCp0XWbU99GYh0BenRAFA1_EJ2vOeeMpk0UgQRvIaqCvMQ=w1301-h480-no)

`apt-cache policy <package-name>` can also be used to verify installation

![verifying mono-complete install using apt-cache policy](https://lh3.googleusercontent.com/AmMeUpHLkGAgDVSWKN_dNiNZR8_leieM4OfDwqyXVtjWZ_W-HO9xu6KQ6h3z98jgCEsBWjSf-rffV8FMoUoaKi43RmPniYBtig8xeAr-NSNP9m2GYsnAgmUDz_zVDiqv-pzOsw6PJgXxR44YSoxMD9Eb3rYQ12fspmeDbLV3gTeW4Jxssp2wv8JWDyF3ArzjOGTHWhaOvee6MtfmnPnFbz27nlqjZ87vio6eClPpYw29FKmNm7Brla2Y2b8vtqpyahRpSP_r3LLegqepR_GYzmHoY5OH0IrBEO4kdhHc5z21y-wExtWVsWlBOtwuTr16_062t4fslB57VX-zXifb7Dxt90VnAcIGMUMwDhzhUe8Xb9WXEhAv5yKtMetySq4j2w1Ng9rr05HEHGpBZhkE4XHE7Wn3jpitS8Z4WcHpWX63nJYaHpY9ALumz-podZODkdnlVZuJx3PMUxve28WZ5_lrHksmL0Bk6BbTd4REbv_SnxRE-B7XmI0aW8WdSp3ptyKxwZHDiDFRUtZpIPbZu2gFe3UaNWzJXREb3JGvmdnrEk74q94RUo-BHj7WkwmQEfns=w722-h325-no)

I was having troubles setting up Mono on my [Ubuntu 14.4](http://releases.ubuntu.com/14.04/) machine, I was not able to get [required `ca-certificates-mono` package](http://www.mono-project.com/docs/getting-started/install/linux/#notes).

So, I had uninstalled Mono with `sudo apt-get purge mono-complete` and followed the above commands.

# Installing libuv

To [host ASP.NET MVC 5 apps outside IIS](http://stackoverflow.com/q/34649424/2404470), it's necessary to [install](https://docs.asp.net/en/latest/getting-started/installing-on-linux.html#install-libuv) [libuv](https://github.com/libuv/libuv), follow the below commands:

<pre>
<code>
    sudo apt-get install make automake libtool curl
    curl -sSL https://github.com/libuv/libuv/archive/v1.4.2.tar.gz | sudo tar zxfv - -C /usr/local/src
    cd /usr/local/src/libuv-1.4.2
    sudo sh autogen.sh
    sudo ./configure
    sudo make
    sudo make install
    sudo rm -rf /usr/local/src/libuv-1.4.2 && cd ~/
    sudo ldconfig
</code>
</pre>

# Install Monodevelop IDE

From [VS code docs](https://code.visualstudio.com/Docs/languages/csharp)
> An example of a non-supported project type is an ASP.NET MVC Application.

In this case, [MonoDevelop](http://www.monodevelop.com/download/linux/) can be used

`sudo apt-get install monodevelop`

which supports ASP.NET MVC projects.

![Monodevelop works with ASP.NET MVC projects](https://lh3.googleusercontent.com/lvkPVzBw0KNyohIJK2aWPjGurWsspstj-7v9ofUq-qt9JY-pszXOpccLsMj7_S69HTxjsM6rd-tt3eWbSKaRif0DAzwQUDKOg5o6iWEZCKkjbVQDITGao-J_clWkcXn8uj2oysrQI1Ixh17jr8mvlmsRjHpIgx9897U-wEqT3rfkI1Cfb9pfNjjK905kv2JWgmr9aZni5YhET87kkbNAjvkw7hBISGw330RViDydD-ev_Z_CBc5IeibYHefs2MBBev6cdAYwC2JPp25KgaxOLXiPyLGbQG90Cf8d3VgYtvDp1gA9itFnry_mvaPHakYQuy39mkuB5mZUuOi_0aovJwY6pUigFxxe66B4OQeJgO93_87YS-XGrd7d2evWzy7KY28OOsefafzaFN6IPQP31451p6KaQDmwwlC2H4sWNFL3aULsEYmmjqS2X6AyJGjvgmubAz8C9_94med7gFwLgzyIBiK2ORQ6o5cPEHzo9mODIqdmu-rCT1afazvsFSbrjMUOMot0nr77ABoLdwrVsnLhEAUiPZ3eC-_k3A9wgkW2mPg0AaZ7oGmoGn3HrkT7b3l_=w901-h660-no)

Phew, it looks like everything is ready to see .NET in action outside Windows.

[Photos](https://goo.gl/photos/q8uMU5v4DuyS2WVx8)
