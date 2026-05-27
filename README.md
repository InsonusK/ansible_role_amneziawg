Role InsonusK.AmneziaWG
=========

Install [AmneziaWG](https://amnezia.org/) to Ubuntu

[Ansible galaxy](https://galaxy.ansible.com/ui/standalone/roles/InsonusK/AmneziaWG/install/)

Requirements
------------

Ubuntu avaliable in https://ppa.launchpadcontent.net/amnezia/ppa/ubuntu/dists/

Role Variables
--------------

- awg_client_config_path - path to awg client config file
- go_package - package of GO.
- use_alt_flow - use alternative flow for instalation

Dependencies
------------

None

Error
-----

May return error that repository has different pgp key. Fixed by
```shell
grep -R amnezia /etc/apt/
sudo rm /etc/apt/sources.list.d/ppa_amnezia_ppa_noble.list
sudo rm /etc/apt/sources.list.d/amnezia-ubuntu-ppa-noble.sources
```

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
