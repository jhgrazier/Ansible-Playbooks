
# Palo Alto Playbooks with Username and Password Authentication
Playbooks for Managing Palo Alto Devices with Username and Password Authentication

## Requirements

```bash
pan-os-python
pan-python
```

## Installation

```bash
pip3 install pan-os-python
pip3 install pan-python
```

## Playbook Usage / Examples
When you are authenticating against the target device, the playbooks prompt for a username, password and API key.

To pull the API key, use curl command against the Palo Alto instance

Example:

```bash
curl -k -X POST 'https://192.168.99.15/api/?type=keygen&user=admin&password=admin'

<response status = 'success'><result><key>--EXAMPLE33lkjljDLFJLFDLJSDFLKJKEYlkjLKALKFJDSFLKJ1-==DLKJLKJFDLJ!!!!</key></result></response>

```

### Install Playbook to your Ansible Host
Depending on what you need, you can pull system configuration, interface configuration, services configuration, etc.

### Run the Playbooks

#### Playbook Example 1
This specific playbook will check the Palo Alto device to validate if the device is ready and display the status on the terminal in an XML format.

```bash
[ansible@ansible]$ ansible-playbook palo-check-device-ready.yaml
Palo Username: admin
Palo Password:
Palo API Key:

PLAY [Gather system info] ********************************************************************************************************************************************************

TASK [Gathering Facts] ***********************************************************************************************************************************************************
ok: [palo-alto1]

TASK [Check to see if device is ready] *******************************************************************************************************************************************
ok: [palo-alto1]

TASK [Print result] **************************************************************************************************************************************************************
ok: [palo-alto1] => {
    "response": {
        "changed": false,
        "disconnected": false,
        "failed": false,
        "msg": "Done",
        "stdout": "{\"response\": {\"@status\": \"success\", \"result\": \"yes\"}}",
        "stdout_lines": [
            "{\"response\": {\"@status\": \"success\", \"result\": \"yes\"}}"
        ],
        "stdout_xml": "<response status=\"success\"><result>yes\n</result></response>"
    }
}

PLAY RECAP ***********************************************************************************************************************************************************************
palo-alto1      

[ansible@ansible]$

```

#### Playbook Example 2
This specific playbook will pull system/services configuration and display it on the terminal.

```bash
[ansible@ansible]$ ansible-playbook palo-get-system-info.yaml
Palo Username: admin
Palo Password:
Palo API Key:

PLAY [Gather system info] ********************************************************************************************************************************************************

TASK [Gathering Facts] ***********************************************************************************************************************************************************
ok: [palo-alto1]

TASK [Gather facts for Palo device] **********************************************************************************************************************************************
ok: [palo-alto1]

TASK [Display information] *******************************************************************************************************************************************************
ok: [palo-alto1] => {
    "msg": [
        "Hostname: PA-VM",
        "Serial: unknown",
        "Model: PA-VM",
        "Version: 9.0.4",
        "Uptime: 0 days, 15:49:03",
        "HA Enabled: False",
        "HA Type: standalone",
        "HA Status: active",
        "Multi-VSYS: off",
        "0 out of 1248 sessions in use"
    ]
}

PLAY RECAP ***********************************************************************************************************************************************************************
palo-alto1                 : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

[ansible@ansible]$

```

#### Playbook Example 3
This specific playbook will pull create various objects on a Palo Alto device.

```bash
[ansible@ansible]$ ansible-playbook palo-change-fw-objects.yaml
Palo Username: admin
Palo Password:
Palo API Key:

PLAY [Create various objects on a PAN-OS device.] ********************************************************************************************************************************

TASK [Gathering Facts] ***********************************************************************************************************************************************************
ok: [palo-alto1]

TASK [Create tag objects] ********************************************************************************************************************************************************
changed: [palo-alto1] => (item={'name': 'Prod', 'color': 'red'})
changed: [palo-alto1] => (item={'name': 'SI', 'color': 'blue gray'})
changed: [palo-alto1] => (item={'name': 'Dev', 'color': 'green'})

TASK [Create address objects] ****************************************************************************************************************************************************
changed: [palo-alto1] => (item={'name': 'Test-1.1.1.1', 'value': '1.1.1.1', 'description': 'Description One', 'tag': ['Prod']})
changed: [palo-alto1] => (item={'name': 'Test-2.2.2.2', 'value': '2.2.2.2', 'description': 'Description Two', 'tag': ['Prod']})
changed: [palo-alto1] => (item={'name': 'Test-3.3.3.3', 'value': '3.3.3.3', 'description': 'Description Three', 'tag': ['Prod']})
changed: [palo-alto1] => (item={'name': 'Test-4.4.4.4', 'value': '4.4.4.4', 'description': 'Description Four', 'tag': ['SI']})
changed: [palo-alto1] => (item={'name': 'Test-5.5.5.5', 'value': '5.5.5.5', 'description': 'Description Five', 'tag': ['SI']})

TASK [Create address ranges] *****************************************************************************************************************************************************
changed: [palo-alto1] => (item={'name': 'Test-Range-1', 'value': '1.1.1.1-2.2.2.2', 'description': 'Test Range 1'})
changed: [palo-alto1] => (item={'name': 'Test-Range-2', 'value': '2.2.2.2-3.3.3.3', 'description': 'Test Range 2'})
changed: [palo-alto1] => (item={'name': 'Test-Range-3', 'value': '3.3.3.3-4.4.4.4', 'description': 'Test Range 3'})

TASK [Create address groups] *****************************************************************************************************************************************************
changed: [palo-alto1] => (item={'name': 'Prod-Instances', 'static_value': ['Test-1.1.1.1', 'Test-2.2.2.2', 'Test-3.3.3.3'], 'tag': ['Prod']})
changed: [palo-alto1] => (item={'name': 'SI-Instances', 'static_value': ['Test-4.4.4.4', 'Test-5.5.5.5'], 'tag': ['SI']})

TASK [Create service objects] ****************************************************************************************************************************************************
changed: [palo-alto1] => (item={'name': 'ssh-tcp-22', 'destination_port': '22', 'description': 'SSH on tcp/22', 'tag': ['Prod']})
changed: [palo-alto1] => (item={'name': 'mysql-tcp-3306', 'destination_port': '3306', 'description': 'MySQL on tcp/3306', 'tag': ['Prod']})

TASK [Create service group objects] **********************************************************************************************************************************************
changed: [palo-alto1] => (item={'name': 'Prod-Services', 'value': ['ssh-tcp-22', 'mysql-tcp-3306'], 'tag': ['Prod']})

PLAY RECAP ***********************************************************************************************************************************************************************
palo-alto1                 : ok=7    changed=6    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

[ansible@ansible

```

#### Playbook Example 4
This specific playbook checks for uncommitted changes and commits if necessary on the Palo Alto device..

```bash
[ansible@ansible]$ ansible-playbook palo-show-changes.yaml
Palo Username: admin
Palo Password:
Palo API Key:

PLAY [Checks for uncommitted changes and commits if necessary.] ******************************************************************************************************************

TASK [Gathering Facts] ***********************************************************************************************************************************************************
ok: [palo-alto1]

TASK [Check for pending changes] *************************************************************************************************************************************************
ok: [palo-alto1]

TASK [Display changes] ***********************************************************************************************************************************************************
ok: [palo-alto1] => {
    "msg": {
        "response": {
            "@status": "success",
            "result": {
                "journal": {
                    "entry": [
                        {
                            "action": "EDIT",
                            "admin-history": "admin",
                            "component-type": "device-network",
                            "owner": "admin",
                            "xpath": "/config/mgt-config/users/entry[@name='admin']"
                        },
                        {
                            "action": "EDIT CREATE",
                            "admin-history": "admin",
                            "component-type": "vsys",
                            "owner": "admin",
                            "xpath": "/config/devices/entry[@name='localhost.localdomain']/vsys/entry[@name='vsys1']/address-group"
                        },
                        {
                            "action": "EDIT",
                            "admin-history": "admin",
                            "component-type": "vsys",
                            "owner": "admin",
                            "xpath": "/config/devices/entry[@name='localhost.localdomain']/vsys/entry[@name='vsys1']/service"
                        },
                        {
                            "action": "EDIT CREATE",
                            "admin-history": "admin",
                            "component-type": "vsys",
                            "owner": "admin",
                            "xpath": "/config/devices/entry[@name='localhost.localdomain']/vsys/entry[@name='vsys1']/address"
                        },
                        {
                            "action": "EDIT CREATE",
                            "admin-history": "admin",
                            "component-type": "vsys",
                            "owner": "admin",
                            "xpath": "/config/devices/entry[@name='localhost.localdomain']/vsys/entry[@name='vsys1']/tag"
                        },
                        {
                            "action": "EDIT",
                            "admin-history": "admin",
                            "component-type": "vsys",
                            "owner": "admin",
                            "xpath": "/config/devices/entry[@name='localhost.localdomain']/vsys/entry[@name='vsys1']/service-group"
                        }
                    ]
                }
            }
        }
    }
}

TASK [Commit changes if needed] **************************************************************************************************************************************************
changed: [palo-alto1]

PLAY RECAP ***********************************************************************************************************************************************************************
palo-alto1                 : ok=4    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

ansible@ansible

```

#### Playbook Example 5
This specific playbook will pull all security rules from the Palo Alto device and display on your terminal.

```bash
[ansible@ansible paloalto]$ ansible-playbook palo-get-security-rules.yaml
Palo Username: admin
Palo Password:
Palo API Key:

PLAY [Gather Palo Security Rules] ************************************************************************************************************************************************

TASK [Gathering Facts] ***********************************************************************************************************************************************************
ok: [palo-alto1]

TASK [Get all security rules] ****************************************************************************************************************************************************
ok: [palo-alto1]

TASK [Output] ********************************************************************************************************************************************************************
ok: [palo-alto1] => {
    "msg": {
        "changed": false,
        "failed": false,
        "gathered": [
            {
                "action": "allow",
                "antivirus": null,
                "application": [
                    "acme-protocol"
                ],
                "category": [
                    "any"
                ],
                "data_filtering": null,
                "description": null,
                "destination_devices": null,
                "destination_ip": [
                    "any"
                ],
                "destination_zone": [
                    "any"
                ],
                "disable_server_response_inspection": null,
                "disabled": null,
                "file_blocking": null,
                "group_profile": null,
                "group_tag": null,
                "hip_profiles": [
                    "any"
                ],
                "icmp_unreachable": null,
                "log_end": null,
                "log_setting": null,
                "log_start": null,
                "negate_destination": null,
                "negate_source": null,
                "negate_target": null,
                "rule_name": "Block ACME",
                "rule_type": null,
                "schedule": null,
                "service": [
                    "application-default"
                ],
                "source_devices": null,
                "source_ip": [
                    "any"
                ],
                "source_user": [
                    "any"
                ],
                "source_zone": [
                    "any"
                ],
                "spyware": null,
                "tag_name": null,
                "target": null,
                "url_filtering": null,
                "uuid": "2d51ce19-5e8f-495e-86d1-e0ac629b7c6a",
                "vulnerability": null,
                "wildfire_analysis": null
            }
        ],
        "gathered_xml": [
            "<?xml version=\"1.0\" encoding=\"utf-8\"?>\n<entry name=\"Block ACME\" uuid=\"2d51ce19-5e8f-495e-86d1-e0ac629b7c6a\">\n\t<from>\n\t\t<member>any</member>\n\t</from>\n\t<to>\n\t\t<member>any</member>\n\t</to>\n\t<source>\n\t\t<member>any</member>\n\t</source>\n\t<source-user>\n\t\t<member>any</member>\n\t</source-user>\n\t<hip-profiles>\n\t\t<member>any</member>\n\t</hip-profiles>\n\t<destination>\n\t\t<member>any</member>\n\t</destination>\n\t<application>\n\t\t<member>acme-protocol</member>\n\t</application>\n\t<service>\n\t\t<member>application-default</member>\n\t</service>\n\t<category>\n\t\t<member>any</member>\n\t</category>\n\t<action>allow</action>\n</entry>\n"
        ]
    }
}

PLAY RECAP ***********************************************************************************************************************************************************************
palo-alto1                 : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

[ansible@ansible]$

```

Playbook Example 6

This specific playbook will pull all configuration and dump into a file on your ansible server.

```bash
[ansible@ansible]$ ansible-playbook palo-get-config.yaml
Palo Username: admin
Palo Password:
Palo API Key:

PLAY [Gather Palo Configuration] *************************************************************************************************************************************************

TASK [Gathering Facts] ***********************************************************************************************************************************************************
ok: [palo-alto1]

TASK [Export Palo Alto device configuratoin] *************************************************************************************************************************************
ok: [palo-alto1]

PLAY RECAP ***********************************************************************************************************************************************************************
palo-alto1                 : ok=2    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

[ansible@ansible]$

```

#### Playbook Example 6
This specific playbook will upgrade the Palo Alto code to the release specified and reboot the device to that code. 

```bash
[ansible@ansible]$ ansible-playbook palo-download-panos-version.yaml
```

