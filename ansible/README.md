# Playbooks
These playbooks are the main functionality of `env-setup`. 

These playbooks are much more simplified than a standard Ansible playbook to make adjustment/management easy for non-DevOps engineers who don't care that much about tweaking Ansible ops.

- The directory schema follows a `${OS}/${ORDER_NUMBER}-${PLAYBOOK_NAME}` pattern
- `${OS}/.00-init`: is meant to be a one-time run playbook to verify env-setup is ready to be used.
- `${OS}/.00-init` contains some common symlinked config files that will used across all playbooks:
    - `${OS}/.00-init/ansible.cfg`: Anisble run-time config.
    - `${OS}/.00-init/inventory`: Host to target (i.e., `localhost`)
    - `${OS}/.00-init/requirements.yml`: [Ansible-Galaxy packages](https://galaxy.ansible.com/) requirements for modules/roles/collections.
- `.main.yml`: starter "hello world" playbook template.
