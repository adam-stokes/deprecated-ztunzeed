Topic: "SOSreport now supports Debian/Ubuntu"
Date: 2013-01-08T15:00:00Z
Category: debian, sosreport, ubuntu

Sosreport is a set of tools is designed to provide information to support organizations
in an extensible manner, allowing third parties, package maintainers, and
anyone else to provide plugins that will collect and report information that
is useful for supporting software packages.

This project is hosted at [Github](http://github.com/sosreport/sosreport) For the latest
version, to contribute, and for more information, please visit there.

Installing it through Launchpad PPA:

    sudo add-apt-repository ppa:debugmonkeys/sosreport
    sudo apt-get update
    sudo apt-get install sosreport

If you are coming from a Red Hat Enterprise Linux or Fedora background and are familiar with sosreport we'd like to invite you to participate in porting over plugins to work across these distributions as well. Several plugins have been ported over that you can use as a guide for making other plugins distribution aware.
