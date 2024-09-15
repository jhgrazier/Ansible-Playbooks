
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

## Playbook Usage / Examples

###Install Playbook to your Ansible Host
Depending on what you need, you can pull system configuration, interface configuration, services configuration, etc.

Run the Playbooks

#### Playbook Example 1
This specific playbook will pull system/services configuration and display it on the terminal in an XML format.

```bash

```

#### Playbook Example 2
This specific playbook will pull system/services configuration and display it on the terminal.

```bash

```

#### Playbook Example 3
This specific playbook will pull system/services configuration and display it on the terminal.

```bash

```

#### Playbook Example 4
This specific playbook will push configuraton to an interface, or really any configuration you want.

```bash

```

#### Playbook Example 5
This specific playbook will pull all configuration and dump into a file on your ansible server.

```bash

```

