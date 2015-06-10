# quassel-core-static
A PKGBUILD for Archlinux users to pull the statically compiled Quassel core from [Quassel-IRC.org](http://quassel-irc.org/) and configure it accordingly to run a Quassel Core instance.

Some questions you might ask have been answered below.

## How to use?
Type the following in sequence in a terminal to install:
```
git clone https://github.com/sunitknandi/quassel-core-static.git
cd quassel-core-static
makepkg -si
```

Expecting more steps? Sorry to disappoint, mate. xD

Start/stop/restart/check the core with:
`sudo systemctl (start|stop|restart|status) quassel`

Enable/disable the core to start at boot with:
`sudo systemctl (enable|disable) quassel`

Read logs with:
`sudo journalctl -u quassel.service --since today -f`

## Does it really work?
I currently use it as a Quassel core on an Archlinux server for me and my friends. The Quassel core has 10 active users as of now and hasn't given us any trouble.
You may either try it yourself or you can take my word for it. Either way, you are gonna try it out while installing. xD

## Why do I need it?
The officially maintained `quassel-core` package on Archlinux repositories [reqire a lot of dependencies](https://www.archlinux.org/packages/community/x86_64/quassel-core/) i.e. 
+ icu
+ qca-qt5
+ qt5-script
+ cmake (make)
+ extra-cmake-modules (make)
+ knotifyconfig (make)
+ qca-qt5 (make)
+ qt5-base (make)
+ qt5-script (make)
+ qt5-tools (make)
More than half of them are _make dependencies_ which means after the packages are compiled they are no longer needed, which means nothing but bloat.

But that's not the motivation for this git repo. The real motivation is actually this:
```
[sunit@quasselcore ~]$ sudo pacman -S quassel-core
[sudo] password for sunit: 
resolving dependencies...
:: There are 5 providers available for libgl:
:: Repository ec2
   1) nvidia-libgl
:: Repository extra
   2) mesa-libgl  3) nvidia-304xx-libgl  4) nvidia-340xx-libgl  5) nvidia-libgl
```
When one tries to install `quassel-core` from the official repos, the dependencies pull another set of dependencies and then another... until it tries to _pull parts of the X.org video stack and libGL_ (I mean like seriously, mate?). Why the heck are those things needed on a headless Quassel core server for god's sake? The Debian package of `quassel-core`, on the other hand is very lightweight and doesn't need the whole stack of video deps (because why on earth?).

The easiest solution to avoid is to use the statically compiled version of Quassel core from the official website itself and save yourself the trouble.

## Where did you get the idea for this repo?
I thought of this idea while installing Quassel Core for the first time on an Archlinux server I run and seeing the hell load of deps. Initially I ran the static core without packaging it. Later when I wanted to write a PKGBUILD, I noticed that Nowaker had already written it [here](https://aur.archlinux.org/packages/quassel-core-static/) but its not being actively maintained.

With time, I started maintaining my private PKGBUILD after forking from Nowaker's to keep the Quassel core on the server updated. It started to get tedious, so I decided to make a git so that I can maintain it and clone and deploy anywhere.

## Why this repo when you could post on the AUR itself?
1. I hate creating a duplicate package when Nowaker already has one.
2. I have sent a pull request to Nowaker to get my commits merged and I'm waiting.
3. The `quassel.conf` and `quassel.service` in Nowaker's original PKGBUILD setup isn't exactly like the way I want it to be. The `quassel.conf` file was useless and modifying the values in it had no effect on the operation of the Quassel core service. I have corrected that behaviour and now editing the file lets you change the host IP and the port Quassel listens to.
4. I want to maintain my Quassel Core server with ease and not be worried about getting broken by future updates posted without properly proofreading the code on the AUR.
5. Since I use this PKGBUILD myself, you can expect me to keep it up-to-date with official Quassel releases.

## What's the license?
My PKGBUILD is licensed under the GPLv2.

## Can I contribute?
Yes, feel free to fork it, edit it and send me a pull request. It can greatly help in timely updates.

## I have something else to ask.
Feel free to shoot me a mail at sunitnandi834 (at) gmail (dot) com and I'll get back to you. :)

