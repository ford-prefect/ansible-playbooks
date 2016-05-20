# Deploying

This assumes that your inventory consists of hosts named `boxes` to which all these playbooks apply. Modify to taste.

## `group_vars`

The `group_vars.sample` directory contains an example of the group variables that need to be set up. You can edit these to fit your needs. The password for the vault files is `password`. You'll probably want to replace them using `ansible-vault create`.

## init.yml

* Set up `group_vars/common` with a `user_name`, crypted `user_password` and `user_ssh_pubkey`
* `ansible-playbook -i ansible_source_dir/contrib/inventory/linode.py --ask-pass --ask-vault-pass init.yml`
  * You will likely need to do a manual SSH first so `--ask-pass` doesn't complain about the host not being in `known_hosts`
* Will be run as root
* Sets up a new user
* Sets up sshd config to not allow root access

## setup.yml

* Add a `mariadb_password` variable to `group_vars/db` (suggested that you use a vault)
* `ansible-playbook -i ansible_source_dir/contrib/inventory/linode.py --ask-become-pass --ask-vault-pass setup.yml`
* Sets up the box to host the services that are needed
