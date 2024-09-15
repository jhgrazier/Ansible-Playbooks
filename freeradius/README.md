
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
[ansible@ansible freeradius]$ ansible-playbook renew-feed-the-chicken-certificate.yaml -K
BECOME password:

PLAY [Update FreeRadius certificate] *********************************************************************************************************************************************

TASK [Create certificate signing request (CSR) for self-signed certificate] ******************************************************************************************************
changed: [localhost]

TASK [Renew self-signed certificate from CSR] ************************************************************************************************************************************
ok: [localhost]

PLAY [Backup existing keys, certificates, copy new keys, certificates and restart Free Radius] ***********************************************************************************

TASK [Gathering Facts] ***********************************************************************************************************************************************************
ok: [freeradius3]
ok: [freeradius1]
ok: [freeradius4]
ok: [freeradius2]

TASK [Backup radius.domain.org.key] **********************************************************************************************************************************************
ok: [freeradius3]
ok: [freeradius1]
ok: [freeradius4]
ok: [freeradius2]

TASK [Backup radius.domain.org.crt Certificate] **********************************************************************************************************************************
changed: [freeradius1]
changed: [freeradius3]
changed: [freeradius2]
changed: [freeradius4]

TASK [Copy new radius.domain.org.key to remote servers] **************************************************************************************************************************
ok: [freeradius3]
ok: [freeradius4]
ok: [freeradius1]
ok: [freeradius2]

TASK [Copy new radius.domain.org.crt certificate to remote servers] **************************************************************************************************************
ok: [freeradius1]
ok: [freeradius2]
ok: [freeradius3]
ok: [freeradius4]

TASK [restart freeradius] ********************************************************************************************************************************************************
changed: [freeradius3]
changed: [freeradius1]
changed: [freeradius4]
changed: [freeradius2]

PLAY RECAP ***********************************************************************************************************************************************************************
freeradius1                : ok=6    changed=2    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
freeradius2                : ok=6    changed=2    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
freeradius3                : ok=6    changed=2    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
freeradius4                : ok=6    changed=2    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
localhost                  : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

[ansible@ansible]
```

## Validation 
This playbook validates the SSL certificate expiration dates for the renewed certificate and validates the file on each server with the md5sum command and displays the output on the terminal..

```bash
[ansible@ansible]$ ansible-playbook validate-freeradius-certificate.yaml -K
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
        "notAfter=Sep 15 22:44:57 2025 GMT"
    ]
}
ok: [freeradius2] => {
    "out.stdout_lines": [
        "notAfter=Sep 15 22:44:57 2025 GMT"
    ]
}
ok: [freeradius3] => {
    "out.stdout_lines": [
        "notAfter=Sep 15 22:44:57 2025 GMT"
    ]
}
ok: [freeradius4] => {
    "out.stdout_lines": [
        "notAfter=Sep 15 22:44:57 2025 GMT"
    ]
}

TASK [Validate the certificate has been updated with md5sum command] *************************************************************************************************************
changed: [freeradius1]
changed: [freeradius2]
changed: [freeradius4]
changed: [freeradius3]

TASK [debug] *********************************************************************************************************************************************************************
ok: [freeradius1] => {
    "out.stdout_lines": [
        "c0cabfaafc40e667bcc0de4823e9ef4d  /etc/raddb/certs/radius.domain.org.crt"
    ]
}
ok: [freeradius2] => {
    "out.stdout_lines": [
        "c0cabfaafc40e667bcc0de4823e9ef4d  /etc/raddb/certs/radius.domain.org.crt"
    ]
}
ok: [freeradius3] => {
    "out.stdout_lines": [
        "c0cabfaafc40e667bcc0de4823e9ef4d  /etc/raddb/certs/radius.domain.org.crt"
    ]
}
ok: [freeradius4] => {
    "out.stdout_lines": [
        "c0cabfaafc40e667bcc0de4823e9ef4d  /etc/raddb/certs/radius.domain.org.crt"
    ]
}

PLAY RECAP ***********************************************************************************************************************************************************************
freeradius1                : ok=4    changed=2    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
freeradius2                : ok=4    changed=2    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
freeradius3                : ok=4    changed=2    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
freeradius4                : ok=4    changed=2    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0

[ansible@ansible]$
```
