Topic: Simple way to get wordpress going in vagrant
Date: 2013-06-18T22:06:41Z
Category: linux, vagrant, wordpress, php

Im working on some wordpress stuff recently and realized how much I hate
setting up php development environments. Specifically anything prior to php 5.4
because of the lack of a built in web server.

I decided at this point it is a good time to invest some time into [vagrant][] and
attempt to get a more tolerable way of hacking on anything php. I managed to
come across a [github project][] that allows me to setup a vagrant session and have
wordpress installed and configured with no fuss.

Fortunately, the developer is receptive to pull requests and merged a few of my
additions to make this project a great way to get started with wordpress
easily.

Here are the simple steps to getting a wordpress development environment setup
in Ubuntu Precise (12.04) and on your way to hacking a new exciting plugin :)

First install VirtualBox

<pre class="prettyprint">
$ sudo apt-get install virtualbox
</pre>

Install [vagrant][] from their site. Once that is done follow the next steps to
get up and running.

<pre class="prettyprint">
$ git clone https://github.com/chad-thompson/vagrantpress.git
$ cd vagrantpress
$ vagrant up
</pre>

You can view your wordpress installation at 

<pre class="prettyprint">
http://localhost:8080/wordpress
# or for a more fqdn approach
http://lvh.me:8080/wordpress
</pre>

[github project]: https://github.com/chad-thompson/vagrantpress
[vagrant]: http://vagrantup.com
