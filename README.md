ansible-role-onion
===========================

[![Build Status](https://github.com/systemli/ansible-role-onion/workflows/Integration/badge.svg?branch=main)](https://github.com/systemli/ansible-role-onion/actions?query=workflow%3AIntegration)
[![Ansible Galaxy](http://img.shields.io/badge/ansible--galaxy-onion-blue.svg)](https://galaxy.ansible.com/systemli/onion/)

Install and configure one or multiple Tor Onion Services (formerly known as Hidden Services).

Hostname and private key will be generated if not supplied as variable.

Hint: It may take up to one minute, until the service is announced in the tor network and reachable.

Be careful: Using the default 127.0.0.1 as Onion Service IP-address could possibly leak meta data: https://help.riseup.net/en/security/network-security/tor/onionservices-best-practices#be-careful-of-localhost-bypasses

Only supports Onion Services in version 3 previously known as [Next Gen Onion Services](https://trac.torproject.org/projects/tor/wiki/doc/NextGenOnions#Howtosetupyourownprop224service) only if tor version >= [0.3.2.1](https://blog.torproject.org/tor-0321-alpha-released-support-next-gen-onion-services-and-kist-scheduler)!

Version 2 Onion Services are currently in a [deprecation phase](https://blog.torproject.org/v2-deprecation-timeline).
If you need an v2 onion service, please use a previous release of this role!

Role Variables
--------------

```
# defaults file for onion
onion_active: True
onion_ipaddr: 127.0.0.1
onion_tor_apt_state: present
onion_services:
  ssh:
    onion_hostname:
    onion_ports:
      - [22, 22]
    onion_authorized_clients: []
    onion_private_key:

onions_configuration:
  SocksPort: 9050
  SocksPolicy: "reject *"

# List of auth cookies for connecting to Authenticated Tor Onion Services.
#
onion_hid_serv_auth: []

onion_monit_enabled: False
```

Download
--------

Download latest release with `ansible-galaxy`

	ansible-galaxy install systemli.onion

Example Playbook
----------------

```
    - hosts: servers
      roles:
         - { role: systemli.onion }
```

Extended Variables Example
--------------------------

```
onion_active: True
onion_ipaddr: 192.168.3.12

onion_services:
  #
  # nextgeneration onion (v3) only available in tor >= 0.3.2.1
  # https://trac.torproject.org/projects/tor/wiki/doc/NextGenOnions#Howtosetupyourownprop224service
  #
  nextgenonion:
     onion_hostname: onionv3url.onion
     onion_ports:
        - [25, 25]
        - [587,587]
     onion_public_key_b64encoded: "\nPT0gZWQyNTUxOaYxLXB1YmxpYzogdHlwZTAgPT0AAABADSX6gVbfuClP6aBXz8V00oMw5Sovn0ZU\nftKei9UWmw==\n"
     onion_secret_key_b64encoded: "\nPT0gZWQyNTUxOaYxLXNlY3JldDogdHlwZTAgPT0AAAAYzbVMulElZeorlRoSKWG4VVVwWQN0lHac\nhpR5jLcqb2iuHQu7K9yrdRUrSUWW42gFUvl7lCDQPV7aGWQcf9TI\n"

  absentonion:
     onion_state: absent
     onion_hostname: onionv3url.onion
     onion_ports:
        - [25, 25]
        - [587,587]
     onion_public_key_b64encoded: "\nPT0gZWQyNTUxOaYxLXB1YmxpYzogdHlwZTAgPT0AAABADSX6gVbfuClP6aBXz8V00oMw5Sovn0ZU\nftKei9UWmw==\n"
     onion_secret_key_b64encoded: "\nPT0gZWQyNTUxOaYxLXNlY3JldDogdHlwZTAgPT0AAAAYzbVMulElZeorlRoSKWG4VVVwWQN0lHac\nhpR5jLcqb2iuHQu7K9yrdRUrSUWW42gFUvl7lCDQPV7aGWQcf9TI\n"

#
# Example for torrc with special onion configurations
# such as Sandboxing, custom data directory, auth cookies ...

onion_services:
  ssh:
    onion_ports:
      - [22, 22]
    onion_authorized_clients:
      - admin

onions_configuration:
  SocksPort: 9050
  SocksPolicy: "reject *"
  RunAsDaemon: 1
  # Enabling Sandbox for the first time may prevent
  # the tor service from restarting. Make sure your
  # SSH connection is not over Tor when enabling it.
  Sandbox: 1
  FetchDirInfoEarly: 1
  FetchDirInfoExtraEarly: 1
  DataDirectory: /var/lib/tor

# Hosts that specified `onion_authorized_clients` will generate
# auth cookies for restricted access. Collect those values from the
# hostname file and add them to the torrc for intended clients, e.g.
# the Ansible controller, via the list var below.
onion_hid_serv_auth:
  - "r7w3xdf3r5smxokv.onion p0xMVci7ffeQFA4IWkcBxR # client: admin"
```


Testing & Development
---------------------

Tests
-----

For developing and testing the role we use Github Actions, ansible-lint, Molecule, and Vagrant.

Run local tests with:

```
molecule test
```

License
-------

GPLv3

Author Information
------------------

https://www.systemli.org
