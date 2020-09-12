# AnsibleAviAclVs

## Goals
Configure an ACL and apply it to all the VS except those listed in the exception list

## Prerequisites:
1. Make sure pip install avisdk is installed:
```
pip install avisdk==18.2.9
sudo -u ubuntu ansible-galaxy install -f avinetworks.avisdk
```
3. Make sure your Avi Controller is reachable from your ansible host
4. Make sure you have an IPAM/DNS profile configured

## Environment:

### Ansible version

```
nic@jumphp:~/ansible/aviAclVs$ ansible --version
ansible 2.9.12
  config file = None
  configured module search path = ['/home/nic/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
  ansible python module location = /home/nic/.local/lib/python3.8/site-packages/ansible
  executable location = /home/nic/.local/bin/ansible
  python version = 3.8.2 (default, Jul 16 2020, 14:00:26) [GCC 9.3.0]
nic@jumphp:~/ansible/aviAclVs$
```

### Avi version

```
Avi 20.1.1
avisdk 18.2.9
```

### Avi Environment
- LSC Cloud

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
ansible-playbook pbAviAclVs.yml --extra-vars @pathto/creds.json
```
- to disable the ACL:
```
ansible-playbook pbAviVs.yml --extra-vars @pathto/creds.json --extra-var state=disable
```
