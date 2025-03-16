![ci](https://github.com/rafael-c-alexandre/ansible-role-provision/actions/workflows/ci.yml/badge.svg)
![release](https://github.com/rafael-c-alexandre/ansible-role-provision/actions/workflows/release.yml/badge.svg)

rafael-c-alexandre.provision
=========

An Ansible role to provision an automated user for executing Ansible playbooks on Debian servers. It creates a user and configures SSH access. Optionally, it can also create new users and user groups.

Requirements
------------

- **Ansible Version**: Ensure you are running Ansible version 2.18 or higher.
- **Supported Systems**: This role is designed for Debian-based systems.

Role Variables
--------------

The following variables can be customized to tailor the role to your needs. Default values are defined in `defaults/main.yml`.

- `automated_user`: *(Default: `"ansible"`)* The username of the automated user to be created.
- `ssh_pub_key_location`: *(Default: `"~/.ssh/ansible.pub"`)* The path to the SSH public key that will be added to the user's `authorized_keys`.
- `custom_new_groups`: *(Default: `"[]"`)* New user groups to be created in the target machine.
- `custom_new_users`: *(Default: `"[]"`)* New users to be created in the target machine and optional groups to assign those users to.

Dependencies
------------

This role has no external dependencies.

Example Playbook
----------------

```yaml
- hosts: all
  become: true
  roles:
    - role: rafael-c-alexandre-provision
      vars:
        automated_user: deploy
        ssh_pub_key_location: "/home/user/.ssh/deploy.pub"
        custom_new_groups:
          - provision-group
        custom_new_users:
          - user: provision-user
            groups: provision-group
            system: true
            shell: /usr/sbin/nologin
```

License
-------

MIT
