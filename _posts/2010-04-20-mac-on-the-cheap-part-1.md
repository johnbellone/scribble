---
layout: post
title: Mac On The Cheap, Part 1
tags: Apple,Apple,Hackintosh,Hackintosh,Mac,Os X,Osx86
---
For as long as I can remember I have been a fan of free operating
systems. _Free_ as in price is always great, but I was referring to
the freedom to tinker with the guts of my operating system without
having to worry. Until I purchased my first MacBook I did not realize
how much I would enjoy the experience of not _needing_ to tinker with
the operating system. When I ran a Windows box there was always driver
updates, service packs and software enhancements that would be
required in order to get optimum performance out of my machine. At
least with a Mac I knew that it was going to work damn well out of the
box. That's what happens when you control every single piece that goes
into your machines.

So as the title might illude this series of blog posts is about how to
build a computer that can run OS X on the cheap - e.g. without having
to purchase expensive hardware from Apple to get the user
experience. Ever since OS X 10.4 Tiger was preloaded on my MacBook I
have purchased a full retail, _legal_, copy of every Apple operating
system. Yeah, I bitched and moaned, but I am an adult now (working in
the software industry) so I can afford to drop the funds necessary to
get what I want. When I purchased Snow Leopard I was never asked if I
was going to install this on an Apple branded Macintosh computer, I
was not required to present a receipt to prove the machine that I had
purchased was capable of running Snow Leopard, thus as far as I am
concerned I am free and in the clear to install this bad boy on any
hardware I have accessible to me.

I am not a lawyer. Is what I have done completely legal? Maybe
not. Apple does all it can to _stop_ us from installing our purchased
operating system on custom hardware. Be aware that Apple absolutely
does not support this at all - you cannot call them up and ask them
why your desktop motherboard's onboard audio doesn't work. But luckily
there is an [awesome community][1] who live and breathe this
stuff. You're not on your own.

So now I present you with the first installment of my _Mac On The
Cheap_ series. The purpose of this blog is to provide an easy-peasy
way to build your own Macintosh for a fraction of the cost while
continuing to perform up to snuff with the vanilla Apple hardware. You
have nothing to worry about. As long as the major component inside of
your build is compatible the rest should simply fall into place.

Buying hardware is key to building a custom Macintosh computer. Since
Apple only supports a small subset of the available computer hardware
you want to match the vanilla components as best as possible. For this
reason I went with purchasing a genuine Intel processor. There are
many tutorials on how to get an AMD processor running OS X, but why
jump through even _more_ hoops when Apple has already made it such a
pain in the ass? Intel processors tend to also perform _much, much,_
*better* than their AMD counterparts. My processor of choice for this
build is the [Intel Core i7-920][2], the consumer model of the Intel's
new architecture

As I mentioned earlier the key component for this whole build is the
motherboard. Most Intel motherboards will work to some degree with OS
X, but for this particular build we want to go with an <em
style="font-style: italic;">unmodified</em> version of the Darwin
kernel (the brain to the OS X operating system). What is the reason
for this? When you run an vanilla kernel <em style="font-style:
italic;">most</em> of Apple's standard updates will work without a
hitch. Occasionally you may run into a snag that nukes your audio, but
for the most part you do not have to worry about allowing Software
Update to run its due course. I did a fair amount of research before
purchasing my motherboard and I found that Gigabyte tends to a great
manufacturer that is well supported in the
[InsanelyMac.com community][1]. My motherboard of choice was the
[Gigabyte GA-X58A-UD3R][3], primarily due to the support of SATA3 and
USB3, as well as future support for Intel's newer processors with
six-cores (twelve threads of execution).

From what it seems memory is aribitrary, but I was luckily able to
reuse some DDR3 from my previous setup. With this motherboard the DDR3
memory can run in triple channel mode which vastly boosts your
performance. My memory is over a year old but it is still running
perfectly fine - I have four 2GB sticks of
[PC3-12800 Patriot Viper memory][4]. This motherboard is able to run
my memory at its full speed - 1600MHZ - without showing any problems.

The last piece of the puzzle was the video card. My previous system
was designed to double as a gaming rig, so I purchased (at the time) a
rather expensive set of video cards so that I could achieve SLI
performance. With the addition of another hard-drive to run OS X on I
had to remove one of the video cards to conserve power (and it was bit
of a tight fit with the motherboard layout). The single card runs
perfectly fine and is seemingly supported right out of the
box. Because Apple has both nVIDIA and ATI (AMD) video cards I do not
think it would be a problem to buy either, but I have been an nVIDIA
man for the past couple of years. The video card in my rig is the EVGA
branded [nVIDIA GTX 260][5].

I do not believe that hard-drives (as long as you have enough space to
install OS X) matter, but from what I hear over the grapevine a good
number of optical drives may have problems inside of OS X. I have yet
to have a need to install my optical drive (it is currently unplugged
on the floor) but I doubt there would be an issue. Lite-on makes a
great optical drive, and I have been a fan of theirs for awhile
now. Choose your flavor, but make sure to steer clear of the Blu-ray
selection for now.

That is it for the first part of this article. The next part will, of
course, be assembly and installation of OS X. For that part of the
process I would suggest that you pick up a decent
[16GB USB flash drive][6] for the installation and boot
process. Remember a couple of things when purchasing hardware - if a
feature is not available yet on a vanilla Macintosh it may be hard to
have it running smoothly. So the SATA3 and USB3 on this board are not
_yet_ supported. I purchased it with the future in mind. As a
forewarning, the only problem that I encountered during the
installation process was getting the audio to work correctly. So be
prepared for to spend some time on that portion!

As always, if you have any questions feel free to leave a comment and
I will respond as soon as possible. For anything more technical
related to the [Hackintosh/OSx86 project][7], be sure to head on over
and sign up for an account at [InsanelyMac.com][1] and start reading
up on some articles!

[1]: http://www.insanelymac.com/
[2]: http://www.newegg.com/Product/Product.aspx?Item=N82E16819115202
[3]: http://www.gigabyte.us/Products/Motherboard/Products_Overview.aspx?ProductID=3317
[4]: http://www.patriotmem.com/products/detailp.jsp?prodline=5&amp;catid=23&amp;prodgroupid=72&amp;id=763&amp;type=1
[5]: http://www.nvidia.com/object/product_geforce_gtx_260_us.html
[6]: http://www.amazon.com/Corsair-Flash-Voyager-Drive-CMFUSB2-0-16GB/dp/B000LXTUT8/ref=sr_1_1?ie=UTF8&amp;s=electronics&amp;qid=1269311610&amp;sr=8-1
[7]: http://www.osx86project.org/
