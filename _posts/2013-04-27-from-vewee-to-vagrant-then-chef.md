---
layout: post
title: From Veewee, to Vagrant, then Chef
tags: Veewee, Vagrant, Chef, Provisioning, DevOps, Testing
---
My good British friend [Phil Sturgeon][14] posted an awesome writeup
regarding [Vagrant][0] and [Chef][4]. I've been meaning to do a post
of my own. Over the last few months a side project of mine has got me
involved a lot with [Vagrant][0], [Chef][4] and [Veewee][3]. But to
find resources on the Internet, especially tutorials, which combine
all that knowledge is definitely a task I would not wish on anyone
else.

So I figured I'd put together a simple little blog post that gets you
started building out your own testing environment. Just a heads up: I
am going to assume you have the [Vagrant][0] dependencies installed. I
prefer installing these from the website and not through RubyGems, but
to each his own. The version I am using is 1.1.3. Everything else
should be picked up automatically from the appropriate files.

I am going to walk you through the steps that I used to build the
[example application][15] which is available as a Gist.  Remember that
you can just run this using the `vagrant up` command and it will be
available (in a few minutes) by accessing the _8080 port_ on your host
machine. You're still going to have to go through the whole
[Veewee][3] build of the base boxes. But after you add the base box
that you've built you can just start the application with
[Vagrant][0].

The first order of business is to checkout some base box
definitions. I tend to use [Opscode][1] [bento repository][2] which
contains [Veewee][3] definitions that pre-builds your machines with
[Chef 11][4] already ready to rock. This obviously alleviates the need
to spend time on the nitty-gritty and just get down to the business.

        $ git clone git://github.com/opscode/bento.git bento
        $ cd bento
        $ bundle install

Now that you have the [bento repository][2] checked out and all of the
dependencies installed using [Bundler][5] you can begin by building
your initial base box. I'm a fan of [CentOS][6] but most of the
[open source cookbooks][7] out there will work flawlessly with
[Ubuntu][13]. So let's start with using that.

        $ bundle exec veewee vbox build 'ubuntu-12.04-i386' --nogui --force
        $ bundle exec veewee vbox export 'ubuntu-12.04-i386'
        $ vagrant box add 'ubuntu-12.04-i386' 'ubuntu-12.04-i386.box'

The first command that we executed there will take a little while to
finish. But it performs a headless installation of [Ubuntu][13] 12.04
32-bit and will *overwrite any existing* [Vagrant][0] [VirtualBox][8]
machine that previously built in this directory. They key off of the
_ubuntu-12.04-i386_ definition name. After that we export to the
[Vagrant][0] recognized format.

Because [Veewee][3] is using [Vagrant][0] to interact with
[VirtualBox][8] we actually have all of the flexibility with our
[base box definitions][2]. What does that mean exactly? [Vagrant][0]
has several [plugins][9] which allow us to use many different
providers for provisioning. For local testing it makes sense to use
[VirtualBox][8] but perhaps our integration machines are vanilla Linux
and we want to use [KVM][10]. Its very simple with [Vagrant][0] to
configure our project to have multiple providers for provisioning.

        $ vagrant init

But once again for flexibility (and making this tutorial easy) let's
stick with the basics. Our project is very simple and we just want to
get a virtual machine ready for testing. This means we just want a
simple [Ruby][11] and [Rack][12] application since I'm more familiar
with those.

We need to modify our _Vagrantfile_ that was created using the
`vagrant init` command. This is the file where we define the
directives necessary for provisioning your virtual machine. Once
again, we're going to use [Ruby][11] and [Rack][12] so your mileage
may vary with any other languages or frameworks.

You can clear out all of the default logic, or place this at the top
so that you have that for reference. Here's the basic changes we're
going to do:

1. Set our base box name to the one that we exported using
   [Veewee][3].
2. Forward HTTP traffic from the [Rack][12] application so it is
   accessible to our host machine.
3. Only use the amount of memory that we think we'll need.
4. Provision using [Chef 11][4] a [Ruby][11] and [Rack][12]
   application.

<script src="https://gist.github.com/johnbellone/5474236.js">
</script>

Now that we have our Vagrantfile setup we just need to get all of our
cookbook dependencies. I've kept this a little light so that you can
easily work through everything. Using the _librarian-chef_ gem we can
define cookbook dependencies similar to using [Bundler][5] for gems.

        $ bundle exec librarian-chef install

I have defined the path the Unicorn webserver to point to the current
working directory which has been mounted in the guest virtual machine
as _/vagrant_. This is defined in the rack_application Chef role. I am
not going to go into the Rack application itself, you can take a look
at the [whole project's repository][15] and check it out.

At this point assuming you've added the base box to Vagrant you can
just do `vagrant up` and see the application from your localhost
running on port 8080. Once the virtual machine is running you can use
`vagrant reload` if you are aking modifications to any recipes or
roles. I'm going to post some more in depth articles about writing
custom cookbooks in the near future, but I hope that this was
useful. If you have any additional questions feel free to hit me up on
[Twitter][16].

[0]: http://vagrantup.com "Vagrant"
[1]: http://opscode.com "Opscode"
[2]: https://github.com/opscode/bento "Bento repository"
[3]: https://github.com/jedi4ever/veewee "Veewee repository"
[4]: http://www.opscode.com/chef/ "Opscode Chef"
[5]: http://gembundler.com/ "Gem Bundler"
[6]: http://centos.org/ "CentOS"
[7]: https://github.com/opscode-cookbooks "Cookbooks"
[8]: http://virtualbox.org "VirtualBox"
[9]: https://github.com "Vagrant plugins"
[10]: http://www.linux-kvm.org "Linux KVM"
[11]: http://ruby-lang.org "Ruby language"
[12]: http://rack.github.io "Rack framework"
[13]: http://ubuntu.com "Ubuntu"
[14]: http://philsturgeon.co.uk/blog/2013/04/vagrant-and-chef-upgrade-party "Vagrant and Chef: Upgrade Party"
[15]: https://github.com/johnbellone/chef-vagrant-rack-app
[16]: http://twitter.com/johnbellone "Twitter"
