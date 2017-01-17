Borgbackup
==========

Ansible [Borgbackup](https://borgbackup.readthedocs.io/en/stable/) role.

Features:
 * Repository or binary installation
 * Schedules regular backup jobs
 * Schedules regular prune jobs to keep backup windows clean
 * Flexible configuration to list backup targets

Role Variables
--------------

see `defaults/main.yml`

Example Playbook
----------------

    - hosts: all
      roles:
        - role: SphericalElephant.borgbackup
          borgbackup_client: True
          borgbackup_client_backup_server: backup01.example.com
          borgbackup_client_jobs:
            - name: system
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
          borgbackup_prune_jobs:
            - name: system
              prune_options: "--keep-daily=7 --keep-weekly=4"
              day: "*"
              hour: "8"
              minute: "0"

You can easily assign client and server attributes from your inventory with something similar to the following:

    borgbackup_client: "{{ (inventory_hostname in groups.borgbackup_server)|ternary(False, True) }}"
    borgbackup_client_backup_server: "{{ groups.borgbackup_server[0] }}"

License
-------

Apache 2.0
