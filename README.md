# Postfix Puppet Module

[![Puppet Forge Version](http://img.shields.io/puppetforge/v/camptocamp/postfix.svg)](https://forge.puppetlabs.com/camptocamp/postfix)
[![Puppet Forge Downloads](http://img.shields.io/puppetforge/dt/camptocamp/postfix.svg)](https://forge.puppetlabs.com/camptocamp/postfix)
[![Build Status](https://img.shields.io/travis/camptocamp/puppet-postfix/master.svg)](https://travis-ci.org/camptocamp/puppet-postfix)
[![Gemnasium](https://img.shields.io/gemnasium/camptocamp/puppet-postfix.svg)](https://gemnasium.com/camptocamp/puppet-postfix)
[![By Camptocamp](https://img.shields.io/badge/by-camptocamp-fb7047.svg)](http://www.camptocamp.com)

This module requires Augeas.

## Simple usage

    include postfix

    postfix::config { "relay_domains": value  => "localhost host.foo.com" }

## Exec paths

In order to not have any path problem, you should add the following line in
some globally included .pp file:

    Exec {
      path => '/some/relevant/path:/some/other:...',
    }

For example:

    Exec {
      path => '/bin:/sbin:/usr/sbin:/usr/bin',
    }

## Classes

### postfix

The top-level class, to install and configure Postfix.

#### Parameters

##### `alias_maps`

A string defining the location of that alias map file.
Default: 'hash:/etc/aliases'

##### `inet_interfaces`

A string defining the network interfaces that Postfix will listen on.
Default: 'all'
Example: '127.0.0.1, [::1]'

##### `ldap`

A boolean defining whether to configure Postfix for LDAP use.
Default: false

##### `ldap_base`

A string defining the LDAP search base to use. This maps to the search_base parameter (ldap_table(5)). 
Default: Undefined. 
Example 'cn=Users,dc=example,dc=com'

##### `ldap_host`

A string defining the LDAP host. This maps to the server_host parameter (ldap_table(5)).
Default: Undefined.
Example: 'ldaps://ldap.example.com:636 ldap://ldap2.example.com'

##### `ldap_options`

A 
Default: Undefined.
Example: 

##### `mail_user`

A string defining the mail user, and optionally group, to execute external commands as. This maps to the user parameter (pipe(8)).
Default: 'vmail'.
Example: 'vmail:vmail'

##### `mailman`

A boolean defining whether to configure a basic smtp server that is able to work for the mailman mailing list manager.
Default: false.

##### `maincf_source`

A string defining the location of a skeleton main.cf file to be used. The default file supplied is blank. However, if the main.cf file already exists on the system the contents will NOT be replaced by the contents from maincf_source.
Default: "puppet:///modules/${module_name}/main.cf"
Example: "puppet:///modules/some/other/location/main.cf"

##### `manage_conffiles`

A boolean defining whether the puppet module should replace the configuration files for postfix. 
This setting currently effects the following files:
* /etc/mailname
* /etc/postfix/master.cf
This setting does NOT effect the following files:
* /etc/aliases
* /etc/postfix/main.cf

Default: true.


## Definitions

### postfix::config

Add/alter/remove options in Postfix main configuration file (main.cf)

### postfix::hash

Creates Postfix hashed "map" files, and build the corresponding db file.

### postfix::transport

Manages content in the transport map.

### postfix::virtual

Manages content in the virtual map.


