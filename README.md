Role InsonusK.AmneziaWG
=========

Install [AmneziaWG](https://amnezia.org/) to Ubuntu

[Ansible galaxy](https://galaxy.ansible.com/ui/standalone/roles/InsonusK/AmneziaWG/install/)

Requirements
------------

Ubuntu 24.10+

Role Variables
--------------

- awg_client_path - path to awg client config file
- go_package - package of GO.

Dependencies
------------

None

Example Playbook
----------------

```yaml
- hosts: server
  roles:
  - role: InsonusK.AmneziaWG
    vars:
      awg_client_path: "{{ awg_client_config_path }}"
```

License
-------

Apache 2.0

Author Information
------------------

[InsonusK](https://github.com/InsonusK)

FAQ
------------------

Common errors on step:
- [Install amneziawg-go](./docs/errors/Install%20amneziawg-go.md)
