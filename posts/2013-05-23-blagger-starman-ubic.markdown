Topic: Deploy blagger with starman, rex and ubic
Date: 2013-05-23T15:24:15Z
Category: perl, deploy, cloud

If you come from a python or ruby background and are used to services
such as virtualenv, rbenv then this document should be easy to
follow. If not, no problem it is still easy :)

## Pre-reqs

Youll want to install perlbrew which is perl's equivalent to virtualenv and rbenv.

<pre class="prettyprint">
$ curl -kL http://install.perlbrew.pl | bash
</pre>

Follow the on screen instructions and install your desired perl version (this doc uses 5.16.3)

<pre class="prettyprint">
$ perlbrew install perl-5.16.3
$ perlbrew switch perl-5.16.3
</pre>

Install cpanm

<pre class="prettyprint">
$ perlbrew install-cpanm
</pre>

## Setup

### Checkout source locally and on remote server

It is best to fork the code into your github account since you'll be
storing your own posts. This is for demonstration only.

<pre class="prettyprint">
$ git clone git://github.com/battlemidget/blagger.git
</pre>

### Install dependencies locally and on remote server

This is equivalent to python's pip or ruby's gem.

<pre class="prettyprint">
$ cpanm --installdeps .
</pre>

### Setup nginx on remote server

<pre class="prettyprint">
$ cp blog.nginx.conf /etc/nginx/sites-enabled/blog.conf
</pre>

Edit the configuration to match your hostname and root directory for this application.

### Setup [Ubic][] on the remote server where you host your blog

You can install this right in your home directory to keep your application self-contained.

<pre class="prettyprint">
$ ubic-admin setup
</pre>

Place the following in your $HOME/ubic/service/blog

<pre class="prettyprint">
use Ubic::Service::Plack;
return Ubic::Service::Plack->new({
   server => "Starman",
   server_args => {
   env => 'production',
   host => '127.0.0.1',
   workers => 5,
   port => 9001,
 },
 app => '/home/blagger/blagger',
 app_name => 'blagger',
});
</pre>

Start the service monitor

<pre class="prettyprint">
$ ubic start blog
</pre>

## Write a blog post

<pre class="prettyprint">
$ ./blagger blag a-new-blog-post
</pre>

## Commit and deploy

<pre class="prettyprint">
$ git commit -asm 'new blog post' && git push -q
$ rex deploy
</pre>

This will deploy and checkout your source remotely via [Rex][] and restart the gaurdian service for the blog.

Once you've done the first deployment any future posts only require you to commit to git and deploy.

[Ubic]: https://metacpan.org/release/Ubic
[Rex]: http://rexify.org
