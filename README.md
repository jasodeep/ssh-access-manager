# Ansible Grant/Revoke SSH Access
This is a Ansible Playbook to automate the process of granting / revoking SSH access to a group of servers instances to a new user

## Pre-requisites
You must have Ansible 2.3 installed.

## Run Playbook
* Add hosts in `inventory/{development,staging,production}/hosts` file. See the given hosts file to add hosts.  

* Add public key in `roles/public-keys/`. __e.g__ if we grant access for john doe user, copy and rename public key into that path like `roles/public-keys/john_doe/john_doe.id_rsa.pub`  

* Run command `ansible-playbook -i inventory -e "access={grant|revoke} ssh_user={SSH_USER} user={USER} servers={webservers|appservers}" {main.yml|development.yml|staging.yml|production.yml} --tag={del_user|add_user}`


## Example
Grant/Revoke SSH access to a group of instances to a user
### Add New User & Grant SSH Access
`ansible-playbook -i inventory -e "access=grant ssh_user=foobar user=foobar servers=webservers" main.yml --tag=add_user`
### Grant SSH Access to an existing user
`ansible-playbook -i inventory -e "access=grant ssh_user=foobar user=john_doe servers=webservers" main.yml`
### Revoke SSH Access
`ansible-playbook -i inventory -e "access=revoke ssh_user=foobar user=foobar servers=webservers" main.yml`
### Revoke SSH Access & Delete the User
`ansible-playbook -i inventory -e "access=revoke ssh_user=foobar user=foobar servers=webservers" main.yml --tag=del_user`

