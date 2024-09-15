
# Juniper Playbooks
Playbooks for Managing Juniper Devices

## Installation Requirements

Ansible 2.5
Python 3.8+
jxmlease
xmltodict
jsnapy

### Juniper Required Modules

```bash
ansible-galaxy collection install juniper.device
ansible-galaxy install juniper.junos
pip install junos-eznc
pip install -U junos-eznc
pip install jxmlease
pip install xmltodict
pip install jsnapy
```

## Playbook Usage

### Playbooks with SSH-Key Authentication
[SSH-Key Authentication Playbooks](https://github.com/jhgrazier/ansible-playbooks/tree/main/juniper/playbooks-with-ssh-key-auth/README.md)

### Playbooks with Username and Password Authentication
[Username and Password Authentication Playbooks](https://github.com/jhgrazier/ansible-playbooks/tree/main/juniper/playbooks-with-username-auth/README.md)

