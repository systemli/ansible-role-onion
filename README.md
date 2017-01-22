ansible-role-hidden-service
===========================

[![Build Status](https://travis-ci.org/systemli/ansible-role-hidden-service.svg)](https://travis-ci.org/systemli/ansible-role-hidden-service) [![Ansible Galaxy](http://img.shields.io/badge/ansible--galaxy-hiddenservice-blue.svg)](https://galaxy.ansible.com/systemli/hidden-service/)


Install and configure one or multiple Tor Hidden Services.

Hostname and private key will be generated if not supplied as variable.

Hint: It may take up to one minute, until the service is announced in the tor network and reachable.

Be careful: Using the default 127.0.0.1 as Hidden Service IP-address could possibly leak meta data: https://help.riseup.net/en/security/network-security/tor/onionservices-best-practices#be-careful-of-localhost-bypasses

Role Variables
--------------

```
# defaults file for hidden-service
hidden_service_active: True
hidden_service_ipaddr: 127.0.0.1
hidden_service_tor_apt_state: present
hidden_service_services:
  ssh:
    hidden_service_hostname:
    hidden_service_ports:
      - [22, 22]
    hidden_service_authorized_clients: []
    hidden_service_private_key:

hidden_services_configuration:
  SocksPort: 9050
  SocksPolicy: "reject *"

# List of auth cookies for connecting to Authenticated Tor Hidden Services.
#
hidden_service_hid_serv_auth: []

hidden_service_monit_enabled: False
```

Download
--------

Download latest release with `ansible-galaxy`

	ansible-galaxy install systemli.hidden-service

Example Playbook
----------------

```
    - hosts: servers
      roles:
         - { role: systemli.hidden-service }
```

Extended Variables Example
--------------------------

```
hidden_service_active: True
hidden_service_ipaddr: 192.168.3.12

hidden_service_services:
  ssh:
     hidden_service_hostname:
     hidden_service_ports:
        - [22, 22]
     hidden_service_private_key:
  mail:
     hidden_service_hostname:
     hidden_service_ports:
        - [25, 25] #[redirected_from, redirected_to]
        - [587,587]
     hidden_service_private_key:
  examplewithhostname:
     hidden_service_hostname: onionurl.onion
     hidden_service_ports:
        - [25, 25]
        - [587,587]
     hidden_service_private_key: |
      -----BEGIN RSA PRIVATE KEY-----
      the
      private
      key
      -----END RSA PRIVATE KEY-----
  absenthiddenservice:
     hidden_service_state: absent
     hidden_service_hostname: onionurl.onion
     hidden_service_ports:
        - [25, 25]
        - [587,587]
     hidden_service_private_key: |
      -----BEGIN RSA PRIVATE KEY-----
      the
      private
      key
      -----END RSA PRIVATE KEY-----

hidden_service_services:
  ssh:
    hidden_service_ports:
      - [22, 22]
    hidden_service_authorized_clients:
      - admin

hidden_services_configuration:
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

# Hosts that specified `hidden_service_authorized_clients` will generate
# auth cookies for restricted access. Collect those values from the
# hostname file and add them to the torrc for intended clients, e.g.
# the Ansible controller, via the list var below.
hidden_service_hid_serv_auth:
  - "r7w3xdf3r5smxokv.onion p0xMVci7ffeQFA4IWkcBxR # client: admin"
```

Testing & Development
---------------------

For developing and testing the role we use Travis CI and Vagrant. On the local environment you can easily test the role with

```
vagrant up trusty
# other available releases are precise, wheezy and jessie
```

License
-------

GPLv3

Author Information
------------------

https://www.systemli.org
