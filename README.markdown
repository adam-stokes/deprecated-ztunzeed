# ztunzeed

### recommended perl setup

I like [perlbrew](http://perlbrew.pl) and so should you :)

### installation

    $ git clone git://github.com/battlemidget/blagger.git
    $ cpanm --installdeps .

### deploy

    $ export BLAGGER_USER=username
    $ export BLAGGER_SERVER=example.com
    $ rex deploy

### running webserver (development)

    $ plackup -R

### running webserver (production)

    $ plackup -l /tmp/webserver.sock -R -D -s Starman

## author

[Adam Stokes](mailto:adamjs@cpan.org)

## disclaimer

Jon Portnoy [avenj at cobaltirc.org](http://www.cobaltirc.org) is original author of blagger
in which this code is based heavily off of.

## license

Licensed under the same terms as Perl.
