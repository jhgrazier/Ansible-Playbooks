
# Juniper Playbooks with SSH-Key Authentication
Playbooks for Managing Juniper Devices with SSH-Key Authentication

## Requirements

Generate an SSH-Key on your host
Install SSH-Key on your Juniper device

### How to generate your SSH-Key

#### Choosing an Algorithm and Key Size

SSH supports several public key algorithms for authentication keys. These include:

    rsa - an old algorithm based on the difficulty of factoring large numbers. A key size of at least 2048 bits is recommended for RSA; 4096 bits is better. RSA is getting old and significant advances are being made in factoring. Choosing a different algorithm may be advisable. It is quite possible the RSA algorithm will become practically breakable in the foreseeable future. All SSH clients support this algorithm.

    dsa - an old US government Digital Signature Algorithm. It is based on the difficulty of computing discrete logarithms. A key size of 1024 would normally be used with it. DSA in its original form is no longer recommended.

    ecdsa - a new Digital Signature Algorithm standarized by the US government, using elliptic curves. This is probably a good algorithm for current applications. Only three key sizes are supported: 256, 384, and 521 (sic!) bits. We would recommend always using it with 521 bits, since the keys are still small and probably more secure than the smaller keys (even though they should be safe as well). Most SSH clients now support this algorithm.

    ed25519 - this is a new algorithm added in OpenSSH. Support for it in clients is not yet universal. Thus its use in general purpose applications may not yet be advisable.

```bash
The algorithm is selected using the -t option and key size using the -b option. The following commands illustrate:

ssh-keygen -t rsa -b 4096
ssh-keygen -t dsa 
ssh-keygen -t ecdsa -b 521
ssh-keygen -t ed25519
```

#### Specifying the File Name
Normally, the tool prompts for the file in which to store the key. However, it can also be specified on the command line using the -f <filename> option.

```bash
ssh-keygen -f ~/tatu-key-ecdsa -t ecdsa -b 521
```

### Install the SSH-Key on the Juniper Device

1. SSH to your Juniper.
2. Create a file named id_rsa.pub using the "vi" editor.
3. Copy and paste the contents of your id_rsa.pub file from where you generated the key and write and save the file with the ":wq" command.
4. Verify the file exists with the "ls" command.
5. Switch to CLI Mode.
6. Switch to configure mode.
7. Run the following command to add the SSH-Key to the authentication list to allow the ansible server to authenticate against the Juniper device.
- Note - Replace "user5" with your target username.

```bash
set system login user user5 authentication load-key-file id_rsa.pub 
show system login user user5
```

#### Validation

8. Run the following command to validate.

```bash
[edit]
lab@vMX-1# show system login user user5                                           
uid 2002;
class super-user;
authentication {
    encrypted-password "REMOVED"; ## SECRET-DATA
    ssh-rsa "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQCI+Ezq8iFwpGnkWO2h7Qot0FeKfXHe63QLdhVDaueKW2gCrTypw8AC6JafOaOobOrYjHcCTzEmnxpJvNGvMx5jYEV/rpP9VYPyCvJIRGfIMAfZ4OwaV+/n7jkuKa2QKSGm8k3RdWXP48ioKg2e94b4A/VdBaWQ5UZBdAzY2Iwf8N3pQWNV4G865EGW8ELuZjSeqv0y4JdrOs38J8fMyMRq/rtgVUDOe5AwjZjFea5z0x7nkNbGQJlhkk/tKlZKnGMI4atezjF5JmZ8MrW9pQY4aBcD79S5HXpvr1MIUPFeC7Gg5NiHU9GYaUXR1l5fxY9wlpCkSLQ6o8e3sIMrhkQ0VoQ+UjlZvdQ1mYy92cwYDZmyPRq3DHLgmPktmKvPbODbcCqHUxbpobQUAIyo1PYIqWL2a7OFnn3OBsW+SJSvnMbO5cV9Mco9FP8A1QLsIjcDybPyMh2DU1BvKIqEkX030mFhBWRmK537uHQNxcm93lvdLqeHriwgUyXXTxSNtBs= eve@linux-1"; ## SECRET-DATA
}

[edit]
lab@vMX-1#
```

9. Commit the changes

```bash
commit
```

10. Try to ssh from the Linux device to the JunOS device.

```bash
Last login: Fri Dec 29 05:55:33 2023 from 192.168.20.5
--- JUNOS 20.4R3-S2.6 Kernel 64-bit  JNPR-11.0-20211117.c779bdc_buil
user5@vMX-1>
```

## Playbook Usage / Examples

### Install Playbook to your Ansible Host
Depending on what you need, you can pull system configuration, interface configuration, services configuration, etc.

Run the Playbooks

#### Playbook Example 1
This specific playbook will pull system/services configuration and display it on the terminal in an XML format.

```bash
  [ansible@ansible]$ ansible-playbook juniper/juniper-get-all-interface-configuration-hierarchies.yaml

PLAY [Get Junos OS configuration via SSH] ****************************************************************************************************************************************

TASK [Get selected configuration hierarchies] ************************************************************************************************************************************
ok: [juniper1.ignyte.lab]

TASK [Print result] **************************************************************************************************************************************************************
ok: [juniper1.ignyte.lab] => {
    "response": {
        "changed": false,

PLAY RECAP ***********************************************************************************************************************************************************************
juniper1.ignyte.lab        : ok=2    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

#### Playbook Example 2
This specific playbook will pull system/services configuration and display it on the terminal.

```bash
  [ansible@ansible]$ ansible-playbook juniper/juniper-get-interface-configuration-hierarchies.yaml

PLAY [Get Junos OS configuration via SSH] ****************************************************************************************************************************************

TASK [Get selected configuration hierarchies] ************************************************************************************************************************************
ok: [juniper1.ignyte.lab]

TASK [Print result] **************************************************************************************************************************************************************
ok: [juniper1.ignyte.lab] => {
    "response": {
        "changed": false,
        "config": "\n## Last commit: 2024-09-08 16:28:33 MDT by root\ninterfaces {\n    ge-0/0/1 {\n        description SRX-LAN;\n        unit 0 {\n            family ethernet-switching {\n                interface-mode trunk;\n                vlan {\n                    members [ vlan-150 vlan-400 vlan-401 vlan-402 vlan-403 vlan-404 vlan-405 vlan-406 vlan-407 vlan-408 vlan-409 vlan-410 vlan-175 vlan-411 vlan-200 ];\n                }\n            }\n        }\n    }\n}\n",
        "config_lines": [
            "",
            "## Last commit: 2024-09-08 16:28:33 MDT by root",
            "interfaces {",
            "    ge-0/0/1 {",
            "        description SRX-LAN;",
            "        unit 0 {",
            "            family ethernet-switching {",
            "                interface-mode trunk;",
            "                vlan {",
            "                    members [ vlan-150 vlan-400 vlan-401 vlan-402 vlan-403 vlan-404 vlan-405 vlan-406 vlan-407 vlan-408 vlan-409 vlan-410 vlan-175 vlan-411 vlan-200 ];",
            "                }",
            "            }",
            "        }",
            "    }",
            "}"
        ],
        "failed": false,
        "msg": "Configuration has been: opened, retrieved, closed."
    }
}

PLAY RECAP ***********************************************************************************************************************************************************************
juniper1.ignyte.lab        : ok=2    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

#### Playbook Example 3
This specific playbook will pull system/services configuration and display it on the terminal.

```bash
  [ansible@ansible]$ ansible-playbook juniper/juniper-get-system_services-configuration-hierarchies.yaml

PLAY [Get Junos OS configuration via SSH] ****************************************************************************************************************************************

TASK [Get selected configuration hierarchies] ************************************************************************************************************************************
ok: [juniper1.ignyte.lab]

TASK [Print result] **************************************************************************************************************************************************************
ok: [juniper1.ignyte.lab] => {
    "response": {
        "changed": false,
        "config": "\n## Last commit: 2024-09-08 16:28:33 MDT by root\nsystem {\n    services {\n        ssh {\n            root-login allow;\n            sftp-server;\n            client-alive-count-max 30;\n            client-alive-interval 30;\n        }\n        netconf {\n            ssh;\n        }\n        dhcp-local-server {\n            group jdhcp-group {\n                interface irb.0;\n            }\n        }\n    }\n}\n",
        "config_lines": [
            "",
            "## Last commit: 2024-09-08 16:28:33 MDT by root",
            "system {",
            "    services {",
            "        ssh {",
            "            root-login allow;",
            "            sftp-server;",
            "            client-alive-count-max 30;",
            "            client-alive-interval 30;",
            "        }",
            "        netconf {",
            "            ssh;",
            "        }",
            "        dhcp-local-server {",
            "            group jdhcp-group {",
            "                interface irb.0;",
            "            }",
            "        }",
            "    }",
            "}"
        ],
        "failed": false,
        "msg": "Configuration has been: opened, retrieved, closed."
    }
}

PLAY RECAP ***********************************************************************************************************************************************************************
juniper1.ignyte.lab        : ok=2    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

#### Playbook Example 4
This specific playbook will push configuraton to an interface, or really any configuration you want as long as you edit the file "junos_apply_set_commands.set" with the commands that you want to set.

##### Example contents of junos_apply_set_commands.set File

```bash
set interfaces ge-0/0/6 unit 0 family ethernet-switching vlan members vlan-200
delete interfaces ge-0/0/6 unit 0 family ethernet-switching vlan members vlan-150
```

Run the Playbook

```bash
  [ansible@ansible ansible-playbooks]$ ansible-playbook juniper/juniper-set-interface-configuration-hierarchies.yaml

PLAY [Set Junos OS configuration via SSH] ****************************************************************************************************************************************

TASK [Apply set configuration] ***************************************************************************************************************************************************
changed: [juniper1.ignyte.lab]

TASK [Print result] **************************************************************************************************************************************************************
ok: [juniper1.ignyte.lab] => {
    "config_results": {
        "changed": true,
        "diff": {
            "prepared": "\n[edit interfaces ge-0/0/6 unit 0 family ethernet-switching vlan]\n-       members vlan-150;\n+       members vlan-200;\n"
        },
        "diff_lines": [
            "",
            "[edit interfaces ge-0/0/6 unit 0 family ethernet-switching vlan]",
            "-       members vlan-150;",
            "+       members vlan-200;"
        ],
        "failed": false,
        "file": "junos_apply_set_commands.set",
        "msg": "Configuration has been: opened, loaded, checked, diffed, committed, closed."
    }
}

PLAY RECAP ***********************************************************************************************************************************************************************
juniper1.ignyte.lab        : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

#### Playbook Example 5
This specific playbook will pull all configuration and dump into a file on your ansible server.

```bash
  [ansible@ansible ansible-playbooks]$ ansible-playbook juniper/juniper-get-configuration-hierarchies.yaml

PLAY [Get Junos OS configuration via SSH] ****************************************************************************************************************************************

TASK [confirm or create configs directory] ***************************************************************************************************************************************
ok: [juniper1.ignyte.lab]

TASK [Get selected configuration hierarchies and save to file] *******************************************************************************************************************
ok: [juniper1.ignyte.lab]

PLAY RECAP ***********************************************************************************************************************************************************************
juniper1.ignyte.lab        : ok=2    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

##### Validation

```bash
[ansible@ansible]$ ls -ltr juniper/configs/
total 28
-rw-r--r--. 1 ansible ansible 25804 Sep  8 23:23 juniper1.ignyte.lab.config

[ansible@ansible ansible-playbooks]$ head -n 50 juniper/configs/juniper1.ignyte.lab.config

## Last commit: 2024-09-08 16:28:33 MDT by root
version 23.1R1.8;
system {
    host-name juniper-srx;
    root-authentication {
    }
    services {
        ssh {
            root-login allow;
            sftp-server;
            client-alive-count-max 30;
            client-alive-interval 30;
        }
        netconf {
            ssh;
        }
        dhcp-local-server {
            group jdhcp-group {
                interface irb.0;
            }
        }
    }
    time-zone America/Denver;
    name-server {
        8.8.8.8;
        8.8.4.4;
    }
    syslog {
        archive size 100k files 3;
        user * {
            any emergency;
        }
        file interactive-commands {
            interactive-commands any;
        }
        file messages {
            any notice;
            authorization info;
        }
    }
    max-configurations-on-flash 5;
    max-configuration-rollbacks 25;
    license {
        autoupdate {
            url https://ae1.juniper.net/junos/key_retrieval;
        }
    }
```

