Topic: python-salesforce on pypi
Date: 2013-05-20 23:04:34
Category: ubuntu, python, salesforce

I've got a project going to utilize Salesforce.com api over json and oauth
rather than soap. Today I uploaded the package to the cheeseshop in hopes to
pull in some interest from the community.

Right now the library contains authorization over OAuth 1.0a and client methods
for retrieving basic Account, Case, and Asset information. My goal is to be api
complete by the end of the year.

I would love to have contributors join the project in order to shape this young
project into a well documented, tested, and easy to use library. As far as
I can tell there isn't another python library like this that doesn't utilize
SOAP for its endpoints.

Using the library is pretty straight forward, currently, I have 2 scripts that
provide a simple way to authorize yourself and communicate with the endpoints.

**sf-exchange-auth** provides a local ssl enabled web server for going through
the OAuth process and storing your token/secret.

**sf-cli** provides some arguments for pulling in rudimentary account and case
information. Usage documentation is provided for this script.

The current focus is to stick to the
[YAGNI](http://en.wikipedia.org/wiki/You_Ain%27t_Gonna_Need_It) principles and
utilize OO when it makes sense. This may or may not be the way to go so I am
open to ideas and patches :D.

You can currently install python-salesforce through pip

    $ pip install python-salesforce

The project page is located at

http://python.salesforce.astokes.org

Looking forward to hearing from you.
