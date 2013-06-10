Topic: SOSreport reaches 3.0
Date: 2013-06-10T14:09:55Z
Category: ubuntu, sosreport

## New release!

After what seems like the longest development cycle ever we've finally released
sosreport 3.0.

Because of the lengthy development cycle I am just going to point you to the
[commits](https://github.com/sosreport/sosreport/commits/master) to see what
changes were made. The most notable changes are:

+ Mult-distribution (Debian, Ubuntu, Fedora, RHEL)
+ Increase speed, roughly 2-3s for an average of 61 plugins tested against.
+ Cloud technologies included (but not limited too):
  - openstack
  - juju
  - maas
  - openshift
  - azure
  - cloudforms
+ Cleaner codebase.

I've also uploaded sosreport to Debian archive and now just waiting on
ftpmaster approval. Until then keep an eye out on my
[ppa](https://launchpad.net/~debugmonkeys/+archive/sosreport) for updates.

Thanks to everyone involved!
