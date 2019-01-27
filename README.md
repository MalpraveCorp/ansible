# Ansible playbooks for Malprave Corp   [![Build Status][buildstatus]][travisci]

Malprave Corp uses Ansible to manage all its configuration management needs.

## Get Started
Pull repo
```
git clone https://github.com/MalpraveCorp/ansible.git; cd ansible;
```
Install Ansible
```
pip install ansible
```
Install Kitchen CI
```
gem install test-kitchen
```
Test a playbook

(Kitchen CI will bootstrap a container and run the playbook against it)
```
kitchen converge mal-node-p
```
Clean up
```
kitchen destroy all
```
## Servers

 - node: "API Gateway" that is used to authenticate requests using OpenResty/Redis on the "edge".
 - be: Backend application in PHP with some container micro services.

## Operations Playbooks
In `ops/` you can find a multitude of playbooks for various operational tasks.

 - Rolling ES: Perform a rolling restart of a ES cluster
 - Sync Mongo: Sync your mongo cluster across environments.

## Author

Pedro Gomes

## License

MIT

[buildstatus]: https://travis-ci.org/MalpraveCorp/ansible.svg?branch=master
[circleci]: https://travis-ci.org/MalpraveCorp/ansible
