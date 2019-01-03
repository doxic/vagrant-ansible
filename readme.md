# vagrant-ansible

Example project showing how to test Ansible playbooks (whole infrastructures) with Molecule.

## Molecule Installation

### CentOS 7
```
$ sudo yum install -y epel-release
$ sudo yum install -y gcc python-pip python-devel openssl-devel libselinux-python
```
### Ubuntu 16.x
```
$ sudo apt-get update
$ sudo apt-get install -y python-pip libssl-dev
```

### Ubuntu 18.x
https://www.digitalocean.com/community/tutorials/how-to-test-ansible-roles-with-molecule-on-ubuntu-18-04
```
$ sudo apt-get update
$ sudo apt install -y python3-pip libssl-dev
$ sudo apt install -y build-essential libssl-dev libffi-dev python3-dev
$ sudo apt install -y python3-venv
```

### Install
Create a new virtual environment
```
$ python3 -m venv .venv
```
Activate it to ensure that your actions are restricted to that environment. Leave with `deactivate`
```
$ source .venv/bin/activate
```
Install requirements for Ansible
```
$ pip install --upgrade pip
$ python3 -m pip install wheel
```
Install Molecule:
```
$ python3 -m pip install molecule ansible python-vagrant ansible-lint
```

Init Molecule with Vagrant driver (just for copy-paste)
```
$ molecule init role -r test-role-vagrant -d vagrant
```

molecule folder and `.yamllint` copied to project directory.

## References
[How To Test Ansible Roles with Molecule on Ubuntu 18.04](https://www.digitalocean.com/community/tutorials/how-to-test-ansible-roles-with-molecule-on-ubuntu-18-04)
[Testing Ansible Roles using Molecule and Vagrant](https://medium.com/@sebinjohn/testing-ansible-roles-using-molecule-and-vagrant-a15c22af23ab)
[Test-driven infrastructure development with Ansible & Molecule](https://blog.codecentric.de/en/2018/12/test-driven-infrastructure-ansible-molecule/)
