# AnsibleAviAclVs

## Goals
Configure an ACL and apply it to all the VS except those listed in the exception list

## Prerequisites:
1. Make sure pip install avisdk is installed:
```
pip install avisdk==21.1.1
sudo -u ubuntu ansible-galaxy install -f avinetworks.avisdk
```
3. Make sure your Avi Controller is reachable from your ansible host
4. Make sure you have an IPAM/DNS profile configured

## Environment:

### Ansible version

```
ansible 2.10.13
  config file = None
  configured module search path = ['/home/ubuntu/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
  ansible python module location = /home/ubuntu/.local/lib/python3.8/site-packages/ansible
  executable location = /home/ubuntu/.local/bin/ansible
  python version = 3.8.10 (default, Jun  2 2021, 10:49:15) [GCC 9.4.0]
```

### Avi version

```
Avi 21.1.1
```

## Input/Parameters:

- Make sure you have a json file with the Avi credentials like the following:
```
{"avi_credentials": {"username": "ansible", "controller": "*****", "password": "*****", "api_version": "*****"}}
```

- All the other paramaters/variables are stored in vars/datas.yml



## Use the the ansible playbook to:
- Create an ACL
- Apply this ACL to all the VS (through Network Security Group)
- add --extra-var state=absent to disable the ACL (through Network Security Group)

## Run the playbook:
- download the playbook:
```
git clone https://github.com/tacobayle/ansibleAviAclVs
```
- initialize the variables (vars/datas.yml)
- to create the ACL and apply it:
```
ansible-playbook local.yml --extra-vars @pathto/creds.json
```
- to disable the ACL:
```
ansible-playbook local.yml --extra-vars @pathto/creds.json --extra-var state=disable
```
