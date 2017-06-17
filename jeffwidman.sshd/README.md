sshd Ansible role
=========

Configures sshd and adds authorized keys for users who need SSH access

Role Variables
--------------

The main variable you need to adjust is `ssh_users`. This is the list of users
who need their keys added to the box. If you have another role that manages users,
then just set `ssh_users` to inherit from `users`.

For safety, this role only alters `sshd_config` if the authorized keys were
successfully added to the box.

This role also defaults the `wheel` group to having passwordless sudo so that if
you accidentally disable root login via ssh you won't be locked out of root.

Other Notes
------------

One gotcha: Ansible will convert unquoted `yes`/`no` values to `True`/`False`,
but `sshd_config` only accepts `yes`/`no` values. So just quote the Ansible
variables like this: `permit_root_login: "yes"`

Requirements
------------

Tested on CentOS 7.
Untested but will likely work on CentOS 6 and equivalent RHEL versions.

Example Playbook
----------------

    - hosts: servers
      roles:
        - { role: sshd,
              permit_root_login: "no",
              password_authentication: "no",
              challenge_response_authentication: "no",
              tags: ['sshd'] }

License
-------

MIT

Author Information
------------------

Jeff Widman jeff@jeffwidman.com
