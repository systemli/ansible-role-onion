ansible-role-hidden-service
===========================

[![Build Status](https://travis-ci.org/systemli/ansible-role-hidden-service.svg)](https://travis-ci.org/systemli/ansible-role-hidden-service) [![Ansible Galaxy](http://img.shields.io/badge/ansible--galaxy-hiddenservice-blue.svg)](https://galaxy.ansible.com/detail#/role/6317)


Install and configure one or multiple Tor Hidden Services.
Hostname and private key will be generated via tor restart, if not supplied as variable.


Role Variables
--------------

```
hidden_service_active: True

hidden_services:
  ssh:
     hidden_service_hostname:
     hidden_service_ports:
        - [22, 22]
     hidden_service_private_key:
```

Example Playbook
----------------

```
    - hosts: servers
      roles:
         - { role: shadow.hiddenservice }
```

Extended Variables Example
--------------------------

```
hidden_service_active: True

hidden_services:
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
```

License
-------

GPLv3

Author Information
------------------

https://www.systemli.org


