# AnsibleAviAclVs

## Goals
Configure an ACL and apply it to all the VS except those listed in the exception list

## Prerequisites:
- The following python packages are installed:
```
sudo apt install -y python3-pip
sudo apt install -y python3-jmespath
pip3 install --upgrade pip
pip3 install ansible-core==2.12.5
pip3 install ansible==5.7.1
pip3 install avisdk
sudo -u ubuntu ansible-galaxy collection install vmware.alb
pip3 install dnspython
pip3 install netaddr
```
- Avi Controller API is reachable (HTTP 443) from your ansible host

## Environment:

### OS version:

```
NAME="Ubuntu"
VERSION="20.04.3 LTS (Focal Fossa)"
ID=ubuntu
ID_LIKE=debian
PRETTY_NAME="Ubuntu 20.04.3 LTS"
VERSION_ID="20.04"
HOME_URL="https://www.ubuntu.com/"
SUPPORT_URL="https://help.ubuntu.com/"
BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
VERSION_CODENAME=focal
UBUNTU_CODENAME=focal
```

### Ansible version

```
ansible [core 2.12.5]
  config file = /etc/ansible/ansible.cfg
  configured module search path = ['/home/ubuntu/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
  ansible python module location = /usr/local/lib/python3.8/dist-packages/ansible
  ansible collection location = /home/ubuntu/.ansible/collections:/usr/share/ansible/collections
  executable location = /usr/local/bin/ansible
  python version = 3.8.10 (default, Mar 15 2022, 12:22:08) [GCC 9.4.0]
  jinja version = 2.10.1
  libyaml = True
```


### Avi version

```
Avi 22.1.5
```

## Input/Parameters:

- Make sure you have a json file with the Avi credentials like the following:
```
{"avi_credentials": {"username": "ansible", "controller": "*****", "password": "*****", "api_version": "*****"}}
```

- All the other variables are stored in vars/datas.yml



## Use the ansible playbook to:
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
ansible-playbook local.yml --extra-vars @pathto/creds.json --extra-var state=delete
```
