Zeroconf
================================================================================

A simple Python 2.7 interface to Zeroconf service discovery and registration.

Installation
--------------------------------------------------------------------------------

The `zeroconf` module assumes that the [avahi](http://avahi.org/) command-line 
tools `avahi-browse` and `avahi-publish` are available.
On Ubuntu for example, they may me installed with:

    $ sudo apt-get install avahi-tools

The module also depend on [Andrew Moffat's subprocess wrapper][pbs]. Install
it with

    $ sudo pip install pbs

[pbs]: https://github.com/amoffat

Usage
--------------------------------------------------------------------------------

### Zeroconf Services Discovery

Searching for all available Zeroconf services is done by

    >>> import zeroconf
    >>> services = zeroconf.search()

The search can be made more specific, for example:

    >>> services = zeroconf.search(name=None, type="_workstation._tcp", domain="local")

The arguments, all optional, to the `search` functions are:

  - `name`: service name, defaults to `None` (interpreted as all),
  - `type`: service type, defaults to `None` (interpreted as all),
  - `domain`: domain name, defaults to `"local"`.

Search results are dictionaries:

    >>> print services
    {('tide [f0:7b:cb:42:ff:e0]', '_workstation._tcp', 'local'): 
       {'txt': '', 'hostname': 'tide.local', 'port': '9', 'address': '192.168.0.13'}, 
     ('wreck [00:26:18:4c:3f:ee]', '_workstation._tcp', 'local'): 
       {'txt': '', 'hostname': 'wreck.local', 'port': '9', 'address': '192.168.0.10'}, 
     ('biohazard [00:18:8b:ac:c8:45]', '_workstation._tcp', 'local'): 
       {'txt': '', 'hostname': 'biohazard.local', 'port': '9', 'address': '192.168.0.12'}}

The keys are `(name, type, domain)` tuples and the values are dictionaries with `txt`, 
`hostname`, `port` and `address` keys.


