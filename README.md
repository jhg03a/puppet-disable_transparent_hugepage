# disable_transparent_hugepage

##Overview

This module disables Transparent Hugepages (THP) on Linux platforms as required by applications such as MongoDB and Redis.  The procedure is based on recommendations published at [mongodb.org](https://docs.mongodb.org/manual/tutorial/transparent-huge-pages/).

The module changes the `/sys/kernel/mm/transparent_hugepage/enabled` and `/sys/kernel/mm/transparent_hugepage/defrag` settings, adds an init service to ensure the changes persist across reboots, and if applicable, configures tuned.

##Usage

Basic use:

```puppet
include disable_transparent_hugepage
```

##Known issues

As a result of Puppet bug [PUP-5296](https://tickets.puppetlabs.com/browse/PUP-5296) it will be necessary for affected users to set the service provider to 'redhat'.  To do that pass the `service_provider` parameter:

```puppet
class { 'disable_transparent_hugepage':
  service_provider => 'redhat',
}
```

##Development

Please read CONTRIBUTING.md before contributing.

###Testing

Make sure you have:

* rake
* bundler

Install the necessary gems:

    bundle install

Note that gems are installed in `.gems` and binaries in `.bin`.  See `.bundle/config`.

To run the tests from the root of the source code:

    bundle exec rake spec