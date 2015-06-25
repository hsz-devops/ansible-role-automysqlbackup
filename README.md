Role: Automysqlbackup set up
============================

Install Automysqlbackup Role and configure.

This role enables you to install and configure Automysqlbackup.
It gives you the option of installing from package manager or
from a repo.
The latest version of Automysqlbackup is not in the repos typically and therefore
to use the latest version you need toinstall from a repo.
I have placed a fork of automysqlbackup on github in case other sources disappear.
The main reason for using the latest version is that it avoids errors in trying to back up events tables etc.

The role also enables you to provide scripts for pre and post backup tasks.
Typically these are used (e.g. post) for pushing the backups off server.

Requirements
------------
Requires MySQL

Role Variables
--------------
For full role vars details see defaults/main.yml

Typically you only need to supply the following:

    automysqlbackup_src: 'manual'

    automysqlbackup_user: # user for the backup folder ownership
    automysqlbackup_group: # group for the backup folder ownership

    automysqlbackup_dump_user: #user to perform the backup
    automysqlbackup_dump_user_pword: # password for the dump user


    automysqlbackup_mail_address: # an email address
    automysqlbackup_mailcontent:  'log'
    # get from package (old version) or from repo (latest)


    automysqlbackup_dump_port: "{{ mysql_port }}"

    # You can supply a folder containing the pre and post tasks
    automysqlbackup_task_folder: "/var/ansible/project/common/files/automysqlbackup"

    automysqlbackup_dir: '/var/backups/db'


Example Playbook
-----------------

    - hosts: dbservers
      roles:
        - { role: ansible-role-automysqlbackup }

License
-------

BSD

Author Information
------------------
George Boobyer (Blue-Bag Ltd)
Part of the BBServer provision
