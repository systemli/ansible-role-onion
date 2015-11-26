Role Name
=========

Install and configures a Tor Hidden Service

Requirements
------------

You already need a Hidden Service hostname and private key.

Role Variables
--------------

* `hidden_service_active: True`
* `hidden_service_hostname:`
* `hidden_service_ports: [22, ]`
* `hidden_service_private_key:`


Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: username.hiddenservice }

License
-------

GPLv3

Author Information
------------------

https://www.systemli.org
