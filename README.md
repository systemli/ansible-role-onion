ansible-role-hidden-service
===========================

[![Build Status](https://travis-ci.org/systemli/ansible-role-hidden-service.svg)](https://travis-ci.org/systemli/ansible-role-hidden-service)

Install and configure a Tor Hidden Service.
Hostname and private key will be generated, if not supplied as variable.


Role Variables
--------------

* `hidden_service_active: True`
* `hidden_service_hostname:`
* `hidden_service_ports: [22, ]`
* `hidden_service_private_key:`


Example Playbook
----------------

    - hosts: servers
      roles:
         - { role: shadow.hiddenservice }

License
-------

GPLv3

Author Information
------------------

https://www.systemli.org
