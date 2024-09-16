
# Juniper Playbooks with Username and Password Authentication
Playbooks for Managing Juniper Devices with Username and Password Authentication

## Playbook Usage / Examples

### Install Playbook to your Ansible Host
Depending on what you need, you can pull system configuration, interface configuration, services configuration, etc.

Run the Playbooks

#### Playbook Example 1
This specific playbook will pull system/services configuration and display it on the terminal in an XML format.

```bash
[ansible@ansible]$ ansible-playbook juniper-get-all-interface-configuration-hierarchies.yaml
Junos Username: root
Junos Password:

PLAY [Get Junos OS configuration via SSH] ****************************************************************************************************************************************

TASK [Get selected configuration hierarchies] ************************************************************************************************************************************
ok: [juniper1.ignyte.lab]

TASK [Print result] **************************************************************************************************************************************************************
ok: [juniper1.ignyte.lab] => {
    "response": {
        "changed": false,
```

#### Playbook Example 2
This specific playbook will pull system/services configuration and display it on the terminal.

```bash
[ansible@ansible]$ ansible-playbook juniper-get-interface-configuration-hierarchies.yaml
Junos Username: root
Junos Password:

PLAY [Get Junos OS configuration via SSH] ****************************************************************************************************************************************

TASK [Get selected configuration hierarchies] ************************************************************************************************************************************
ok: [juniper1.ignyte.lab]

TASK [Print result] **************************************************************************************************************************************************************
ok: [juniper1.ignyte.lab] => {
    "response": {
        "changed": false,
        "config": "\n## Last commit: 2024-09-15 01:27:44 MDT by root\ninterfaces {\n    ge-0/0/1 {\n        description SRX-LAN;\n        unit 0 {\n            family ethernet-switching {\n                interface-mode trunk;\n                vlan {\n                    members [ vlan-150 vlan-400 vlan-401 vlan-402 vlan-403 vlan-404 vlan-405 vlan-406 vlan-407 vlan-408 vlan-409 vlan-410 vlan-175 vlan-411 vlan-200 vlan-412 ];\n                }\n            }\n        }\n    }\n}\n",
        "config_lines": [
            "",
            "## Last commit: 2024-09-15 01:27:44 MDT by root",
            "interfaces {",
            "    ge-0/0/1 {",
            "        description SRX-LAN;",
            "        unit 0 {",
            "            family ethernet-switching {",
            "                interface-mode trunk;",
            "                vlan {",
            "                    members [ vlan-150 vlan-400 vlan-401 vlan-402 vlan-403 vlan-404 vlan-405 vlan-406 vlan-407 vlan-408 vlan-409 vlan-410 vlan-175 vlan-411 vlan-200 vlan-412 ];",
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
[ansible@ansible]$ ansible-playbook juniper-get-system_services-configuration-hierarchies.yaml
Junos Username: root
Junos Password:

PLAY [Get Junos OS configuration via SSH] ****************************************************************************************************************************************

TASK [Get selected configuration hierarchies] ************************************************************************************************************************************
ok: [juniper1.ignyte.lab]

TASK [Print result] **************************************************************************************************************************************************************
ok: [juniper1.ignyte.lab] => {
    "response": {
        "changed": false,
        "config": "\n## Last commit: 2024-09-15 01:27:44 MDT by root\nsystem {\n    services {\n        ssh {\n            root-login allow;\n            sftp-server;\n            client-alive-count-max 30;\n            client-alive-interval 30;\n        }\n        netconf {\n            ssh {\n                port 830;\n            }\n        }\n        dhcp-local-server {\n            group jdhcp-group {\n                interface irb.0;\n            }\n        }\n    }\n}\n",
        "config_lines": [
            "",
            "## Last commit: 2024-09-15 01:27:44 MDT by root",
            "system {",
            "    services {",
            "        ssh {",
            "            root-login allow;",
            "            sftp-server;",
            "            client-alive-count-max 30;",
            "            client-alive-interval 30;",
            "        }",
            "        netconf {",
            "            ssh {",
            "                port 830;",
            "            }",
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
[ansible@ansible]$ ansible-playbook juniper-set-interface-configuration-hierarchies.yaml
Junos Username: root
Junos Password:

PLAY [Set Junos OS configuration via SSH] ****************************************************************************************************************************************

TASK [Apply set configuration] ***************************************************************************************************************************************************
ok: [juniper1.ignyte.lab]

TASK [Print result] **************************************************************************************************************************************************************
ok: [juniper1.ignyte.lab] => {
    "config_results": {
        "changed": false,
        "failed": false,
        "file": "junos_apply_set_commands.set",
        "msg": "Configuration has been: opened, loaded, checked, diffed, closed."
    }
}

PLAY RECAP ***********************************************************************************************************************************************************************
juniper1.ignyte.lab        : ok=2    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

#### Playbook Example 5
This specific playbook will pull all configuration and dump into a file on your ansible server.

```bash
[ansible@ansible]$ ansible-playbook juniper-get-configuration-hierarchies.yaml
Junos Username: root
Junos Password:

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
#### Playbook Example 6
This specific playbook will upgrade the Juniper code to the release specified and reboot the device to that code. 

##### Notes
When you execute the software or juniper_junos_software module, it performs the following operations:

Compares the Junos OS version specified in the version argument, or in the software package filename if the version argument is omitted, to the installed version on the managed device. If the installed and desired versions are identical, the module skips the remaining installation steps and sets changed and failed to false.

If the software package is located on the Ansible control node, and the no_copy parameter is omitted or set to False, the module performs the following operations:

Computes the checksum of the local software package or packages using the algorithm specified in the checksum_algorithm argument, if the checksum is not already provided in the checksum argument. Acceptable checksum_algorithm values are md5, sha1, and sha256. The default is md5.

Performs a storage cleanup on the target device to create space for the software package, unless the cleanfs argument is set to false.

SCP or FTP copies any packages to the target device.

When the module includes local_package, the package is copied to the remote_package directory, or if remote_package is not specified, to the /var/tmp directory, if a file with the same name and checksum does not already reside in the target location on the device. When the module includes pkg_set, the packages are always copied to the /var/tmp directory on the Virtual Chassis primary device.

Note:

If the cleanfs argument is omitted or set to true, the module copies the software package to the device even if it already exists in the target location, because the storage cleanup operation removes the existing file. If cleanfs: false is present and the file already resides at the target location, the module skips the file copy operation.

Computes the checksum of each remote file and compares it to the value of the local file.

```bash
[ansible@ansible]$ ansible-playbook juniper-upgrade-device.yaml
Junos Username: root
Junos Password:

PLAY [Perform a Junos OS software upgrade] ***************************************************************************************************************************************

TASK [Upgrade Junos OS] **********************************************************************************************************************************************************
changed: [juniper1.ignyte.lab]

TASK [Print the response] ********************************************************************************************************************************************************
ok: [juniper1.ignyte.lab] => {
    "response": {
        "changed": true,
        "check_mode": false,
        "failed": false,
        "msg": "Package /srv/ansible/ansible-playbooks/juniper/playbooks-with-username-auth/junos-srxsme-24.2R1.17.tgz successfully installed. Response from device is: \nFormatting alternate root (/dev/da0s1a)...\n/dev/da0s1a: 588.2MB (1204616 sectors) block size 16384, fragment size 2048\n\tusing 4 cylinder groups of 147.06MB, 9412 blks, 18944 inodes.\nsuper-block backups (for fsck -b #) at:\n 32, 301216, 602400, 903584\nsaving package file in /var/sw/pkg ...\nInstalling package '/altroot/cf/packages/install-tmp/junos-24.2R1.17' ...\nVerified junos-boot-srxsme-24.2R1.17.tgz signed by PackageProductionECP256_2024 method ECDSA256+SHA256\nVerified junos-srxsme-24.2R1.17-domestic signed by PackageProductionECP256_2024 method ECDSA256+SHA256\nVerified manifest signed by PackageProductionECP256_2024 method ECDSA256+SHA256\nJUNOS 24.2R1.17 will become active at next reboot\nWARNING: A reboot is required to load this software correctly\nWARNING:     Use the 'request system reboot' command\nWARNING:         when software installation is complete\nSaving state for rollback ...\n Reboot successfully initiated. Reboot message: Shutdown NOW! [pid 72995]"
    }
}

PLAY RECAP ***********************************************************************************************************************************************************************
juniper1.ignyte.lab        : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

[ansible@ansible]$
```

