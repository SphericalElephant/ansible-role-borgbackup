Borgbackup
==========

Ansible [Borgbackup](https://borgbackup.readthedocs.io/en/stable/) role

Requirements
------------

* Debian Jessie or newer

Role Variables
--------------

see `defaults/main.yml`

Example Playbook
----------------

    - hosts: all
      roles:
        - role: SphericalElephant.ansible
          borgbackup_client: True
          borgbackup_client_backup_server: backup01.example.com
          borgbackup_client_jobs:
            - name: system
              backup_repository: "system"
              day: "*"
              hour: "0"
              minute: "{{ 59 | random }}"
              directories:
                - /etc
                - /home
                - /var
              excludes:
                - 're:^/var/lib/apt'
                - 're:^/var/[^/]+\/cache/'

License
-------

Apache 2.0
