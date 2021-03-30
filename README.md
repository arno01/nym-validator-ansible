# Ansible Role: nym validator

## Description

Deploy nym validator using ansible. With an option to install the right version of Go on your local machine to compile binaries locally.
This role also takes care of TLS certs with a little help of certbot and installs nginx on your domain. 


## Requirements

- Ansible >= 2.9 (It might work on previous versions, but we cannot guarantee it)
- Go version >=1.15 (possible to use included go-install task if you need to automate this. Stock version on my Ubuntu 20.04 was 1.14 and it did not work.)
- Debian-based distro (other distros will be added soon.)
- domain name with set up DNS records for your host ip. 

## Role Variables

All variables which can be overridden are stored in [defaults/main.yml](defaults/main.yml) 
Check that file first and edit as needed. 

## Usage


- `git clone git@gitlab.nymte.ch:hans/ansible-validator.git`

Execute the playbook from a directory you just cloned where you have your **inventory**(hosts) file(edit the example from this repo) and **playbook.yaml**. 

Ansible will look for the supplied role in nym-validator/roles/nym-validator/ directory and for tasks within that directory. 

The example playbook looks like this:
```yaml
- hosts: all
  roles: 
    - nym-validator
  environment: 
    LD_LIBRARY_PATH: /home/nym/nymd/
```

Make sure to check list of tasks in [tasks/main.yml](tasks/main.yml) ! 

**WARNING:** If you do not want to install latest version of **Go** on your local machine, then uncomment the first *import_tasks:* or use option to exclude tags. Tags are listed in `/roles/tasks/go_install.yml` - this is still a rough draft so they are not listed in this README.  

To execute the sample playbook after you tweak variables in [defaults/main.yml](defaults/main.yml) and hosts.yaml, simply run this from ~/.ansible/ directory:
```
ansible-playbook -i hosts.yaml playbook1.yaml -v 
```
add `--step` if you want to confirm each task. 