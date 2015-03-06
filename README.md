Memcache Role
=============

Ansible Role to install Memcache on a Foorge cluster.

RESTRICTIONS: This role only allows to create exactly one node in each memcache "cluster",
because of restrictions in envconsul that I am trying to overcome at some point.

Resource
--------

This role provides Memcache servers for your infrastructure.

It is specificially tailored at the Ubuntu memcache init scripts - that allow
multiple instances of Memcache to run - to aovid potential key clashes between
different applications of the same project.

For an application the following environment variable will be provided:

    MEMCACHE_URL_FOO='foo1.memcache.service.consul:11211,foo2.memcache.service.consul:11212'

It contains a list seperated by comma containing the host and port of all
memcache servers in a given pool. Please note: Multiple nodes are technically
not supported at the moment!

Minimal Example
---------------

    ---
    - hosts: memcache
      roles:
        - role: memcache
          memcache_pools:
            - { app: 'foo', name: 'query', port: 11211 }
            - { app: 'foo', name: 'session', port: 11212 }

It is required that the memcache hosts group only matches exactly one host.

License
-------

MIT
