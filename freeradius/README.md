
# Free Radius Playbooks

Playbooks for Managing Free Radius Servers


## Requirements

On each of the Free Radius nodes, you will need:

python3
pip
cryptography

```bash
  dnf install -y python3
  dnf install -y pip
  pip install cryptography
```
    
## Playbook Usage / Examples

Install Playbook to your Ansible Host

### Run the Playbooks

#### Playbook Example 1
This playbook creates a self-signed SSL certificate required for Free Radius

```bash
[ansible@ansible]$ ansible-playbook freeradius/create-freeradius-certificate.yaml -K
BECOME password:

PLAY [Create FreeRadius certificate] *********************************************************************************************************************************************

TASK [Create certificate signing request (CSR) for self-signed certificate] ******************************************************************************************************
changed: [freeradius2]
changed: [freeradius4]
changed: [freeradius3]
changed: [freeradius1]

TASK [Renew self-signed certificate from CSR] ************************************************************************************************************************************
changed: [freeradius4]
changed: [freeradius3]
changed: [freeradius1]
changed: [freeradius2]

PLAY RECAP ***********************************************************************************************************************************************************************
freeradius1                : ok=4    changed=2    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
freeradius2                : ok=4    changed=2    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
freeradius3                : ok=4    changed=2    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
freeradius4                : ok=4    changed=2    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

#### Playbook Example 2
This playbook renews the SSL certificate required for Free Radius

```bash
ansible@ansible]$ ansible-playbook freeradius/renew-freeradius-certificate.yaml -K
BECOME password:

PLAY [Update FreeRadius certificate] *********************************************************************************************************************************************

TASK [Backup original radius*.key file] ******************************************************************************************************************************************
ok: [freeradius1]
ok: [freeradius3]
ok: [freeradius2]
ok: [freeradius4]

TASK [Backup original radius*.crt file] ******************************************************************************************************************************************
ok: [freeradius1]
ok: [freeradius3]
ok: [freeradius4]
ok: [freeradius2]

TASK [Create certificate signing request (CSR) for self-signed certificate] ******************************************************************************************************
changed: [freeradius2]
changed: [freeradius4]
changed: [freeradius3]
changed: [freeradius1]

TASK [Renew self-signed certificate from CSR] ************************************************************************************************************************************
changed: [freeradius4]
changed: [freeradius3]
changed: [freeradius1]
changed: [freeradius2]

PLAY RECAP ***********************************************************************************************************************************************************************
freeradius1                : ok=4    changed=2    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
freeradius2                : ok=4    changed=2    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
freeradius3                : ok=4    changed=2    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
freeradius4                : ok=4    changed=2    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

## Validation 
This playbook validates the SSL certificate expiration dates for the renewed certificate.

```bash
[ansible@ansible ansible-playbooks]$ ansible-playbook freeradius/validate-freeradius-certificate.yaml -K
BECOME password:

PLAY [Validate FreeRadius certificate Expiration] ********************************************************************************************************************************

TASK [Validate the certificate has been updated with openssl command] ************************************************************************************************************
changed: [freeradius1]
changed: [freeradius3]
changed: [freeradius4]
changed: [freeradius2]

TASK [debug] *********************************************************************************************************************************************************************
ok: [freeradius1] => {
    "out.stdout_lines": [
        "notAfter=Sep 10 00:05:11 2025 GMT"
    ]
}
ok: [freeradius2] => {
    "out.stdout_lines": [
        "notAfter=Sep 10 00:05:11 2025 GMT"
    ]
}
ok: [freeradius3] => {
    "out.stdout_lines": [
        "notAfter=Sep 10 00:05:11 2025 GMT"
    ]
}
ok: [freeradius4] => {
    "out.stdout_lines": [
        "notAfter=Sep 10 00:05:11 2025 GMT"
    ]
}

PLAY RECAP ***********************************************************************************************************************************************************************
freeradius1                : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
freeradius2                : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
freeradius3                : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
freeradius4                : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```
