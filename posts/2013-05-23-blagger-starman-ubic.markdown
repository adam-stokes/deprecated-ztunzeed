Topic: Deploy blagger with starman, rex and ubic
Date: 2013-05-23T15:24:15Z
Category: perl, deploy, cloud

If you come from a python or ruby background and are used to services
such as virtualenv, rbenv then this document should be easy to
follow. If not, no problem it is still easy :)

## Pre-reqs

Youll want to install perlbrew which is perl's equivalent to virtualenv and rbenv.

    curl -kL http://install.perlbrew.pl | bash

Follow the on screen instructions and install your desired perl version (this doc uses 5.16.3)

    perlbrew install perl-5.16.3
    perlbrew switch perl-5.16.3

Install cpanm

    perlbrew install-cpanm


## Setup

### Checkout source locally and on remote server

It is best to fork the code into your github account since you'll be
storing your own posts. This is for demonstration only.

    git clone git://github.com/battlemidget/blagger.git

### Install dependencies locally and on remote server

This is equivalent to python's pip or ruby's gem.

    cpanm --installdeps .

### Setup nginx on remote server

    cp blog.nginx.conf /etc/nginx/sites-enabled/blog.conf

Edit the configuration to match your hostname and root directory for this application.

### Setup [Ubic][] on the remote server where you host your blog

You can install this right in your home directory to keep your application self-contained.

    ubic-admin setup

Place the following in your $HOME/ubic/service/blog

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

Start the service monitor

    ubic start blog

## Write a blog post

    ./blagger blag a-new-blog-post
    ...
    ...

## Commit and deploy

    git commit -asm 'new blog post' && git push -q
    rex deploy

This will deploy and checkout your source remotely via [Rex][] and restart the gaurdian service for the blog.

Once you've done the first deployment any future posts only require you to commit to git and deploy.

[Ubic]: https://metacpan.org/release/Ubic
[Rex]: http://rexify.org
