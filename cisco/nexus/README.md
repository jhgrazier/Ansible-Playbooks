
# Cisco Nexus Playbooks
Playbooks for Managing Cisco Nexus Devices

## Installation Requirements

Ansible 2.5
Python 3.8+
cisco.nxos

### Cisco Required Module Installation

```bash
ansible-galaxy install cisco.nxos
```

### Ansible Inventory Example

```bash
nexus_cisco:
  vars:
    ansible_connection: network_cli
    ansible_network_cli_ssh_type: paramiko
    ansible_user: ansible
    ansible_network_os: nxos
    ansible_ssh_common_args: '-o KexAlgorithms=+diffie-hellman-group1-sha1 -o HostKeyAlgorithms=+ssh-rsa -o Ciphers=+aes256-cbc'
    ansible_python_interpreter: /usr/bin/python3
  children:
    nexus_cisco:
      children:
        nexus9k:
              hosts:
                  cisco-nexus1:
```

### Ansible Authentication
You can use either username / password authentication or SSH-Key authentication.

#### SSH-Key Authentication
You will want to copy your id_rsa.pub file to the bootflash of the Nexus switch prior to executing this procedure.

```bash
vswitch1(config)# username ansible role network-admin
warning: password for user:ansible not set. S/he may not be able to login
vswitch1(config)# !CMD: PASSWORD statement not print^C
vswitch1(config)# username ansible sshkey file bootflash:id_rsa.pub
vswitch1(config)# end
cisco-nexus1# copy running-config startup-config
[########################################] 100%
Copy complete, now saving to disk (please wait)...
Copy complete.
cisco-nexus1#
```

#### User / Password Authentication
You will want to build a username / password for local authentication or a service account user on a TACACS/ISE server.

## Playbook Usage / Examples

### Install Playbook to your Ansible Host
Depending on what you need, you can pull system configuration, interface configuration, services configuration, etc.

Run the Playbooks

#### Playbook Example 1
This specific playbook will pull interface configuration and display it on the terminal in an XML format.

```bash
[ansible@ansible nexus]$ ansible-playbook nexus9k/nexus9k-get-configuration-interface-hierarchies.yaml

PLAY [Get Nexus 9K Interface configuration via SSH] ******************************************************************************************************************************

TASK [Gathering Facts] ***********************************************************************************************************************************************************
ok: [cisco-nexus1]

TASK [Get selected configuration hierarchies and save to file] *******************************************************************************************************************
ok: [cisco-nexus1]

TASK [Print result] **************************************************************************************************************************************************************
ok: [cisco-nexus1] => {
    "response": {
        "changed": false,
        "failed": false,
        "stdout": [
            "!Command: show running-config interface\n!Running configuration last done at: Sat Sep 14 17:44:46 2024\n!Time: Sat Sep 14 18:03:03 2024\n\nversion 9.2(1) Bios:version  \n\ninterface Vlan1\n\ninterface Vlan100\n  no shutdown\n  ip address 192.168.128.1/24\n\ninterface Vlan200\n  no shutdown\n  ip address 192.168.129.1/24\n\ninterface Vlan300\n  no shutdown\n  ip address 192.168.130.1/24\n\ninterface Ethernet1/1\n  description P2P Link for MGMT\n  no switchport\n  ip address 192.168.120.4/24\n  ip router ospf 400 area 0.0.164.85\n  no shutdown\n\ninterface Ethernet1/2\n  switchport mode trunk\n  switchport trunk allowed vlan 100\n\ninterface Ethernet1/3\n  switchport mode trunk\n  switchport trunk allowed vlan 200\n\ninterface Ethernet1/4\n  switchport mode trunk\n  switchport trunk allowed vlan 300\n\ninterface Ethernet1/5\n  no cdp enable\n  no switchport\n  ip address 172.16.25.2/24\n  ip verify unicast source reachable-via any allow-default\n  isis network point-to-point\n  ip router isis 300\n  no shutdown\n\ninterface Ethernet1/6\n  shutdown\n\ninterface Ethernet1/7\n  shutdown\n\ninterface Ethernet1/8\n  shutdown\n\ninterface Ethernet1/9\n  shutdown\n\ninterface Ethernet1/10\n  shutdown\n\ninterface Ethernet1/11\n  shutdown\n\ninterface Ethernet1/12\n  shutdown\n\ninterface Ethernet1/13\n  shutdown\n\ninterface Ethernet1/14\n  shutdown\n\ninterface Ethernet1/15\n  shutdown\n\ninterface Ethernet1/16\n  shutdown\n\ninterface Ethernet1/17\n  shutdown\n\ninterface Ethernet1/18\n  shutdown\n\ninterface Ethernet1/19\n  shutdown\n\ninterface Ethernet1/20\n  shutdown\n  switchport trunk allowed vlan 100\n\ninterface Ethernet1/21\n  shutdown\n\ninterface Ethernet1/22\n  shutdown\n\ninterface Ethernet1/23\n  shutdown\n\ninterface Ethernet1/24\n  shutdown\n\ninterface Ethernet1/25\n  shutdown\n\ninterface Ethernet1/26\n  shutdown\n\ninterface Ethernet1/27\n  shutdown\n\ninterface Ethernet1/28\n  shutdown\n\ninterface Ethernet1/29\n  shutdown\n\ninterface Ethernet1/30\n  shutdown\n  switchport trunk allowed vlan 200\n\ninterface Ethernet1/31\n  shutdown\n\ninterface Ethernet1/32\n  shutdown\n\ninterface Ethernet1/33\n  shutdown\n\ninterface Ethernet1/34\n  shutdown\n\ninterface Ethernet1/35\n  shutdown\n\ninterface Ethernet1/36\n  shutdown\n\ninterface Ethernet1/37\n  shutdown\n\ninterface Ethernet1/38\n  shutdown\n\ninterface Ethernet1/39\n  shutdown\n\ninterface Ethernet1/40\n  shutdown\n  switchport trunk allowed vlan 300\n\ninterface Ethernet1/41\n  shutdown\n\ninterface Ethernet1/42\n  shutdown\n\ninterface Ethernet1/43\n  shutdown\n\ninterface Ethernet1/44\n  shutdown\n\ninterface Ethernet1/45\n  shutdown\n\ninterface Ethernet1/46\n  shutdown\n\ninterface Ethernet1/47\n  shutdown\n\ninterface Ethernet1/48\n  shutdown\n\ninterface Ethernet1/49\n  shutdown\n\ninterface Ethernet1/50\n  shutdown\n\ninterface Ethernet1/51\n  shutdown\n\ninterface Ethernet1/52\n  shutdown\n\ninterface Ethernet1/53\n  shutdown\n\ninterface Ethernet1/54\n  shutdown\n\ninterface Ethernet1/55\n  shutdown\n\ninterface Ethernet1/56\n  shutdown\n\ninterface Ethernet1/57\n  shutdown\n\ninterface Ethernet1/58\n  shutdown\n\ninterface Ethernet1/59\n  shutdown\n\ninterface Ethernet1/60\n  shutdown\n\ninterface Ethernet1/61\n  shutdown\n\ninterface Ethernet1/62\n  shutdown\n\ninterface Ethernet1/63\n  shutdown\n\ninterface Ethernet1/64\n  shutdown\n\ninterface Ethernet1/65\n  shutdown\n\ninterface Ethernet1/66\n  shutdown\n\ninterface Ethernet1/67\n  shutdown\n\ninterface Ethernet1/68\n  shutdown\n\ninterface Ethernet1/69\n  shutdown\n\ninterface Ethernet1/70\n  shutdown\n\ninterface Ethernet1/71\n  shutdown\n\ninterface Ethernet1/72\n  shutdown\n\ninterface Ethernet1/73\n  shutdown\n\ninterface Ethernet1/74\n  shutdown\n\ninterface Ethernet1/75\n  shutdown\n\ninterface Ethernet1/76\n  shutdown\n\ninterface Ethernet1/77\n  shutdown\n\ninterface Ethernet1/78\n  shutdown\n\ninterface Ethernet1/79\n  shutdown\n\ninterface Ethernet1/80\n  shutdown\n\ninterface Ethernet1/81\n  shutdown\n\ninterface Ethernet1/82\n  shutdown\n\ninterface Ethernet1/83\n  shutdown\n\ninterface Ethernet1/84\n  shutdown\n\ninterface Ethernet1/85\n  shutdown\n\ninterface Ethernet1/86\n  shutdown\n\ninterface Ethernet1/87\n  shutdown\n\ninterface Ethernet1/88\n  shutdown\n\ninterface Ethernet1/89\n  shutdown\n\ninterface Ethernet1/90\n  shutdown\n\ninterface Ethernet1/91\n  shutdown\n\ninterface Ethernet1/92\n  shutdown\n\ninterface Ethernet1/93\n  shutdown\n\ninterface Ethernet1/94\n  shutdown\n\ninterface Ethernet1/95\n  shutdown\n\ninterface Ethernet1/96\n  shutdown\n\ninterface Ethernet1/97\n  shutdown\n\ninterface Ethernet1/98\n  shutdown\n\ninterface Ethernet1/99\n  shutdown\n\ninterface Ethernet1/100\n  shutdown\n\ninterface Ethernet1/101\n  shutdown\n\ninterface Ethernet1/102\n  shutdown\n\ninterface Ethernet1/103\n  shutdown\n\ninterface Ethernet1/104\n  shutdown\n\ninterface Ethernet1/105\n  shutdown\n\ninterface Ethernet1/106\n  shutdown\n\ninterface Ethernet1/107\n  shutdown\n\ninterface Ethernet1/108\n  shutdown\n\ninterface Ethernet1/109\n  shutdown\n\ninterface Ethernet1/110\n  shutdown\n\ninterface Ethernet1/111\n  shutdown\n\ninterface Ethernet1/112\n  shutdown\n\ninterface Ethernet1/113\n  shutdown\n\ninterface Ethernet1/114\n  shutdown\n\ninterface Ethernet1/115\n  shutdown\n\ninterface Ethernet1/116\n  shutdown\n\ninterface Ethernet1/117\n  shutdown\n\ninterface Ethernet1/118\n  shutdown\n\ninterface Ethernet1/119\n  shutdown\n\ninterface Ethernet1/120\n  shutdown\n\ninterface Ethernet1/121\n  shutdown\n\ninterface Ethernet1/122\n  shutdown\n\ninterface Ethernet1/123\n  shutdown\n\ninterface Ethernet1/124\n  shutdown\n\ninterface Ethernet1/125\n  shutdown\n\ninterface Ethernet1/126\n  shutdown\n\ninterface Ethernet1/127\n  shutdown\n\ninterface Ethernet1/128\n  shutdown\n\ninterface mgmt0\n  vrf member management\n  ip address 10.10.1.7/24\n\ninterface loopback0\n  ip address 192.168.160.3/32\n  ip ospf network point-to-point\n  ip router ospf 400 area 0.0.164.85"
        ],
        "stdout_lines": [
            [
                "!Command: show running-config interface",
                "!Running configuration last done at: Sat Sep 14 17:44:46 2024",
                "!Time: Sat Sep 14 18:03:03 2024",
                "",
                "version 9.2(1) Bios:version  ",
                "",
                "interface Vlan1",
                "",
                "interface Vlan100",
                "  no shutdown",
                "  ip address 192.168.128.1/24",
                "",
                "interface Vlan200",
                "  no shutdown",
                "  ip address 192.168.129.1/24",
                "",
                "interface Vlan300",
                "  no shutdown",
                "  ip address 192.168.130.1/24",
                "",
                "interface Ethernet1/1",
                "  description P2P Link for MGMT",
                "  no switchport",
                "  ip address 192.168.120.4/24",
                "  ip router ospf 400 area 0.0.164.85",
                "  no shutdown",
                "",
                "interface Ethernet1/2",
                "  switchport mode trunk",
                "  switchport trunk allowed vlan 100",
                "",
                "interface Ethernet1/3",
                "  switchport mode trunk",
                "  switchport trunk allowed vlan 200",
                "",
                "interface Ethernet1/4",
                "  switchport mode trunk",
                "  switchport trunk allowed vlan 300",
                "",
                "interface Ethernet1/5",
                "  no cdp enable",
                "  no switchport",
                "  ip address 172.16.25.2/24",
                "  ip verify unicast source reachable-via any allow-default",
                "  isis network point-to-point",
                "  ip router isis 300",
                "  no shutdown",
                "",
                "interface Ethernet1/6",
                "  shutdown",
                "",
                "interface Ethernet1/7",
                "  shutdown",
                "",
                "interface Ethernet1/8",
                "  shutdown",
                "",
                "interface Ethernet1/9",
                "  shutdown",
                "",
                "interface Ethernet1/10",
                "  shutdown",
                "",
                "interface Ethernet1/11",
                "  shutdown",
                "",
                "interface Ethernet1/12",
                "  shutdown",
                "",
                "interface Ethernet1/13",
                "  shutdown",
                "",
                "interface Ethernet1/14",
                "  shutdown",
                "",
                "interface Ethernet1/15",
                "  shutdown",
                "",
                "interface Ethernet1/16",
                "  shutdown",
                "",
                "interface Ethernet1/17",
                "  shutdown",
                "",
                "interface Ethernet1/18",
                "  shutdown",
                "",
                "interface Ethernet1/19",
                "  shutdown",
                "",
                "interface Ethernet1/20",
                "  shutdown",
                "  switchport trunk allowed vlan 100",
                "",
                "interface Ethernet1/21",
                "  shutdown",
                "",
                "interface Ethernet1/22",
                "  shutdown",
                "",
                "interface Ethernet1/23",
                "  shutdown",
                "",
                "interface Ethernet1/24",
                "  shutdown",
                "",
                "interface Ethernet1/25",
                "  shutdown",
                "",
                "interface Ethernet1/26",
                "  shutdown",
                "",
                "interface Ethernet1/27",
                "  shutdown",
                "",
                "interface Ethernet1/28",
                "  shutdown",
                "",
                "interface Ethernet1/29",
                "  shutdown",
                "",
                "interface Ethernet1/30",
                "  shutdown",
                "  switchport trunk allowed vlan 200",
                "",
                "interface Ethernet1/31",
                "  shutdown",
                "",
                "interface Ethernet1/32",
                "  shutdown",
                "",
                "interface Ethernet1/33",
                "  shutdown",
                "",
                "interface Ethernet1/34",
                "  shutdown",
                "",
                "interface Ethernet1/35",
                "  shutdown",
                "",
                "interface Ethernet1/36",
                "  shutdown",
                "",
                "interface Ethernet1/37",
                "  shutdown",
                "",
                "interface Ethernet1/38",
                "  shutdown",
                "",
                "interface Ethernet1/39",
                "  shutdown",
                "",
                "interface Ethernet1/40",
                "  shutdown",
                "  switchport trunk allowed vlan 300",
                "",
                "interface Ethernet1/41",
                "  shutdown",
                "",
                "interface Ethernet1/42",
                "  shutdown",
                "",
                "interface Ethernet1/43",
                "  shutdown",
                "",
                "interface Ethernet1/44",
                "  shutdown",
                "",
                "interface Ethernet1/45",
                "  shutdown",
                "",
                "interface Ethernet1/46",
                "  shutdown",
                "",
                "interface Ethernet1/47",
                "  shutdown",
                "",
                "interface Ethernet1/48",
                "  shutdown",
                "",
                "interface Ethernet1/49",
                "  shutdown",
                "",
                "interface Ethernet1/50",
                "  shutdown",
                "",
                "interface Ethernet1/51",
                "  shutdown",
                "",
                "interface Ethernet1/52",
                "  shutdown",
                "",
                "interface Ethernet1/53",
                "  shutdown",
                "",
                "interface Ethernet1/54",
                "  shutdown",
                "",
                "interface Ethernet1/55",
                "  shutdown",
                "",
                "interface Ethernet1/56",
                "  shutdown",
                "",
                "interface Ethernet1/57",
                "  shutdown",
                "",
                "interface Ethernet1/58",
                "  shutdown",
                "",
                "interface Ethernet1/59",
                "  shutdown",
                "",
                "interface Ethernet1/60",
                "  shutdown",
                "",
                "interface Ethernet1/61",
                "  shutdown",
                "",
                "interface Ethernet1/62",
                "  shutdown",
                "",
                "interface Ethernet1/63",
                "  shutdown",
                "",
                "interface Ethernet1/64",
                "  shutdown",
                "",
                "interface Ethernet1/65",
                "  shutdown",
                "",
                "interface Ethernet1/66",
                "  shutdown",
                "",
                "interface Ethernet1/67",
                "  shutdown",
                "",
                "interface Ethernet1/68",
                "  shutdown",
                "",
                "interface Ethernet1/69",
                "  shutdown",
                "",
                "interface Ethernet1/70",
                "  shutdown",
                "",
                "interface Ethernet1/71",
                "  shutdown",
                "",
                "interface Ethernet1/72",
                "  shutdown",
                "",
                "interface Ethernet1/73",
                "  shutdown",
                "",
                "interface Ethernet1/74",
                "  shutdown",
                "",
                "interface Ethernet1/75",
                "  shutdown",
                "",
                "interface Ethernet1/76",
                "  shutdown",
                "",
                "interface Ethernet1/77",
                "  shutdown",
                "",
                "interface Ethernet1/78",
                "  shutdown",
                "",
                "interface Ethernet1/79",
                "  shutdown",
                "",
                "interface Ethernet1/80",
                "  shutdown",
                "",
                "interface Ethernet1/81",
                "  shutdown",
                "",
                "interface Ethernet1/82",
                "  shutdown",
                "",
                "interface Ethernet1/83",
                "  shutdown",
                "",
                "interface Ethernet1/84",
                "  shutdown",
                "",
                "interface Ethernet1/85",
                "  shutdown",
                "",
                "interface Ethernet1/86",
                "  shutdown",
                "",
                "interface Ethernet1/87",
                "  shutdown",
                "",
                "interface Ethernet1/88",
                "  shutdown",
                "",
                "interface Ethernet1/89",
                "  shutdown",
                "",
                "interface Ethernet1/90",
                "  shutdown",
                "",
                "interface Ethernet1/91",
                "  shutdown",
                "",
                "interface Ethernet1/92",
                "  shutdown",
                "",
                "interface Ethernet1/93",
                "  shutdown",
                "",
                "interface Ethernet1/94",
                "  shutdown",
                "",
                "interface Ethernet1/95",
                "  shutdown",
                "",
                "interface Ethernet1/96",
                "  shutdown",
                "",
                "interface Ethernet1/97",
                "  shutdown",
                "",
                "interface Ethernet1/98",
                "  shutdown",
                "",
                "interface Ethernet1/99",
                "  shutdown",
                "",
                "interface Ethernet1/100",
                "  shutdown",
                "",
                "interface Ethernet1/101",
                "  shutdown",
                "",
                "interface Ethernet1/102",
                "  shutdown",
                "",
                "interface Ethernet1/103",
                "  shutdown",
                "",
                "interface Ethernet1/104",
                "  shutdown",
                "",
                "interface Ethernet1/105",
                "  shutdown",
                "",
                "interface Ethernet1/106",
                "  shutdown",
                "",
                "interface Ethernet1/107",
                "  shutdown",
                "",
                "interface Ethernet1/108",
                "  shutdown",
                "",
                "interface Ethernet1/109",
                "  shutdown",
                "",
                "interface Ethernet1/110",
                "  shutdown",
                "",
                "interface Ethernet1/111",
                "  shutdown",
                "",
                "interface Ethernet1/112",
                "  shutdown",
                "",
                "interface Ethernet1/113",
                "  shutdown",
                "",
                "interface Ethernet1/114",
                "  shutdown",
                "",
                "interface Ethernet1/115",
                "  shutdown",
                "",
                "interface Ethernet1/116",
                "  shutdown",
                "",
                "interface Ethernet1/117",
                "  shutdown",
                "",
                "interface Ethernet1/118",
                "  shutdown",
                "",
                "interface Ethernet1/119",
                "  shutdown",
                "",
                "interface Ethernet1/120",
                "  shutdown",
                "",
                "interface Ethernet1/121",
                "  shutdown",
                "",
                "interface Ethernet1/122",
                "  shutdown",
                "",
                "interface Ethernet1/123",
                "  shutdown",
                "",
                "interface Ethernet1/124",
                "  shutdown",
                "",
                "interface Ethernet1/125",
                "  shutdown",
                "",
                "interface Ethernet1/126",
                "  shutdown",
                "",
                "interface Ethernet1/127",
                "  shutdown",
                "",
                "interface Ethernet1/128",
                "  shutdown",
                "",
                "interface mgmt0",
                "  vrf member management",
                "  ip address 10.10.1.7/24",
                "",
                "interface loopback0",
                "  ip address 192.168.160.3/32",
                "  ip ospf network point-to-point",
                "  ip router ospf 400 area 0.0.164.85"
            ]
        ]
    }
}

PLAY RECAP ***********************************************************************************************************************************************************************
cisco-nexus1               : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

#### Playbook Example 2
This specific playbook will show BGP summary and advertised/received routes and display it on the terminal.

##### Requirements
Install the playbook nxos_show_ip_bgp_parser.yaml to parse the data.

```bash
vars:
  route:
    network: "{{ item.network }}"
    next_hop: "{{ item.next_hop }}"
    metric: "{{ item.metric }}"
    local_preference: "{{ item.local_pref }}"
    weight: "{{ item.weight }}"
    path: " {{ item.path }}"
    installed: "{{ item.status_var == '>' }}"
keys:
  bgp_routes:
    value: "{{ route }}"
    items: "\\*(?P<status_var>\\S)(?P<bgp_session>\\w)(?P<network>[0-9./]+)\\s+(?P<next_hop>[0-9./]+)\\s{10,20}(?P<metric>\\d+|[ ])\\s{5,20}(?P<local_pref>\\d+|[ ])\\s{5,20}(?P<weight>\\d+)\\s{1}(?P<path>.+)"
```

```bash
[ansible@ansible nexus]$ ansible-playbook nexus9k/nexus9k-get-bgp-status.yaml

PLAY [Get Nexus 9K BGP Summary and Advertised/Received Routes via SSH] ***********************************************************************************************************

TASK [Gathering Facts] ***********************************************************************************************************************************************************
ok: [cisco-nexus1]

TASK [Get BGP Summary and Display on Terminal] ***********************************************************************************************************************************
ok: [cisco-nexus1]

TASK [Get BGP Info and Display on Terminal] **************************************************************************************************************************************
ok: [cisco-nexus1]

TASK [Print result] **************************************************************************************************************************************************************
ok: [cisco-nexus1] => {
    "response": {
        "changed": false,
        "failed": false,
        "stdout": [
            "BGP routing table information for VRF default, address family IPv4 Unicast\nBGP table version is 1331, Local Router ID is 192.168.160.3\nStatus: s-suppressed, x-deleted, S-stale, d-dampened, h-history, *-valid, >-best\nPath type: i-internal, e-external, c-confed, l-local, a-aggregate, r-redist, I-injected\nOrigin codes: i - IGP, e - EGP, ? - incomplete, | - multipath, & - backup\n\n   Network            Next Hop            Metric     LocPrf     Weight Path\n*>i10.8.0.0/24        10.50.5.2                         100          0 42069 80085 42069 80085 42069 80085 52420 102 2808 998 i\n*>l192.168.128.0/24   0.0.0.0                           100      32768 i\n*>l192.168.129.0/24   0.0.0.0                           100      32768 i\n*>l192.168.130.0/24   0.0.0.0                           100      32768 i"
        ],
        "stdout_lines": [
            [
                "BGP routing table information for VRF default, address family IPv4 Unicast",
                "BGP table version is 1331, Local Router ID is 192.168.160.3",
                "Status: s-suppressed, x-deleted, S-stale, d-dampened, h-history, *-valid, >-best",
                "Path type: i-internal, e-external, c-confed, l-local, a-aggregate, r-redist, I-injected",
                "Origin codes: i - IGP, e - EGP, ? - incomplete, | - multipath, & - backup",
                "",
                "   Network            Next Hop            Metric     LocPrf     Weight Path",
                "*>i10.8.0.0/24        10.50.5.2                         100          0 42069 80085 42069 80085 42069 80085 52420 102 2808 998 i",
                "*>l192.168.128.0/24   0.0.0.0                           100      32768 i",
                "*>l192.168.129.0/24   0.0.0.0                           100      32768 i",
                "*>l192.168.130.0/24   0.0.0.0                           100      32768 i"
            ]
        ]
    }
}

PLAY RECAP ***********************************************************************************************************************************************************************
cisco-nexus1               : ok=4    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

#### Playbook Example 3
This specific playbook will show OSPF neighbors and database and display it on the terminal.

```bash
[ansible@ansible nexus]$ ansible-playbook nexus9k/nexus9k-get-ospf-status.yaml

PLAY [Get Nexus 9K OSPF Neighbors/Database via SSH] ******************************************************************************************************************************

TASK [Gathering Facts] ***********************************************************************************************************************************************************
ok: [cisco-nexus1]

TASK [Get OSPF Neighbors/Database and Display on Terminal] ***********************************************************************************************************************
ok: [cisco-nexus1]

TASK [Print result] **************************************************************************************************************************************************************
ok: [cisco-nexus1] => {
    "response": {
        "changed": false,
        "failed": false,
        "stdout": [
            "OSPF Router with ID (192.168.120.4) (Process ID 400 VRF default)\n\n                Router Link States (Area 0.0.164.85)\n\nLink ID         ADV Router      Age        Seq#       Checksum Link Count\n192.168.120.2   192.168.120.2   1465       0x800003bf 0x8244   2   \n192.168.120.3   192.168.120.3   525        0x80000884 0xee07   2   \n192.168.120.4   192.168.120.4   1440       0x8000060b 0xd194   2   \n\n                Network Link States (Area 0.0.164.85)\n\nLink ID         ADV Router      Age        Seq#       Checksum \n192.168.120.2   192.168.120.2   1465       0x80000006 0xb802\n\n                Type-5 AS External Link States \n\nLink ID         ADV Router      Age        Seq#       Checksum Tag\n0.0.0.0         192.168.120.3   525        0x80000850 0xa062    400\n0.0.0.0         192.168.120.4   310        0x80000008 0x6f75    0"
        ],
        "stdout_lines": [
            [
                "OSPF Router with ID (192.168.120.4) (Process ID 400 VRF default)",
                "",
                "                Router Link States (Area 0.0.164.85)",
                "",
                "Link ID         ADV Router      Age        Seq#       Checksum Link Count",
                "192.168.120.2   192.168.120.2   1465       0x800003bf 0x8244   2   ",
                "192.168.120.3   192.168.120.3   525        0x80000884 0xee07   2   ",
                "192.168.120.4   192.168.120.4   1440       0x8000060b 0xd194   2   ",
                "",
                "                Network Link States (Area 0.0.164.85)",
                "",
                "Link ID         ADV Router      Age        Seq#       Checksum ",
                "192.168.120.2   192.168.120.2   1465       0x80000006 0xb802",
                "",
                "                Type-5 AS External Link States ",
                "",
                "Link ID         ADV Router      Age        Seq#       Checksum Tag",
                "0.0.0.0         192.168.120.3   525        0x80000850 0xa062    400",
                "0.0.0.0         192.168.120.4   310        0x80000008 0x6f75    0"
            ]
        ]
    }
}

PLAY RECAP ***********************************************************************************************************************************************************************
cisco-nexus1               : ok=3    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

#### Playbook Example 4
This specific playbook will push configuraton for hostname, MOTD, nameservers and login banner.

```bash
[ansible@ansible nexus]$ ansible-playbook nexus9k/nexus9k-configure-top-level-config.yaml

PLAY [Configure top level config] ************************************************************************************************************************************************

TASK [Configure hostname] ********************************************************************************************************************************************************
ok: [cisco-nexus1]

TASK [configure name servers] ****************************************************************************************************************************************************
ok: [cisco-nexus1]

TASK [Update login banner] *******************************************************************************************************************************************************
changed: [cisco-nexus1]

PLAY RECAP ***********************************************************************************************************************************************************************
cisco-nexus1               : ok=3    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

##### Validation

```bash
[ansible@ansible nexus]$ cat nexus9k/configs/show_run_cisco-nexus1.txt
“!Command: show running-config
!Running configuration last done at: Sat Sep 14 17:44:46 2024
!Time: Sat Sep 14 17:45:33 2024

version 9.2(1) Bios:version
hostname cisco-nexus1
vdc cisco-nexus1 id 1
  limit-resource vlan minimum 16 maximum 4094
  limit-resource vrf minimum 2 maximum 4096
  limit-resource port-channel minimum 0 maximum 511
  limit-resource u4route-mem minimum 248 maximum 248
  limit-resource u6route-mem minimum 96 maximum 96
  limit-resource m4route-mem minimum 58 maximum 58
  limit-resource m6route-mem minimum 8 maximum 8

feature scp-server
feature sftp-server
feature ospf
feature bgp
feature isis
feature interface-vlan

banner motd @
                     **** WARNING NOTICE ****
This system is restricted solely to authorized users for legitimate
  purposes only. The actual or attempted unauthorized access, use
      or modification of this system is strictly prohibited.
   Unauthorized users are subject to disciplinary proceedings
and/or criminal and civil penalties under state, federal or other
applicable domestic and foreign laws. The use of this system may be
monitored and recorded for administrative and security reasons. Anyone
accessing this system expressly consents to such monitoring and is
advised that if such monitoring reveals possible evidence of criminal
activity, the owner may provide the evidence of such activity to law
                      enforcement officials.
@

ip domain-lookup
ip name-server 192.168.120.1
crypto key param rsa label vswitch1 modulus 2048
copp profile strict
ip ssh source-interface mgmt0
rmon event 1 description FATAL(1) owner PMON@FATAL
rmon event 2 description CRITICAL(2) owner PMON@CRITICAL
rmon event 3 description ERROR(3) owner PMON@ERROR
rmon event 4 description WARNING(4) owner PMON@WARNING
rmon event 5 description INFORMATION(5) owner PMON@INFO
snmp-server community DveviM5YpB!! group network-operator

ip route 0.0.0.0/0 Ethernet1/1 192.168.120.1
vlan 1,100,200,300,400

ip prefix-list BGP_ROUTES seq 5 permit 192.168.128.0/24 le 32
ip prefix-list BGP_ROUTES seq 10 permit 192.168.129.0/24 le 32
ip prefix-list BGP_ROUTES seq 15 permit 192.168.130.0/24 le 32
ip prefix-list OSPF-LOOPBACKS seq 10 permit 192.168.160.0/29 ge 30
route-map BGP-ROUTES permit 10
  match ip address prefix-list BGP_ROUTES
route-map LOCAL-PREF permit 10
  match ospf-area 400
  set local-preference 200
route-map OSPF-LOOPBACKS permit 10
  match ip address prefix-list OSPF-LOOPBACKS
vrf context management
  ip route 0.0.0.0/0 mgmt0 10.10.1.1


interface Vlan1

interface Vlan100
  no shutdown
  ip address 192.168.128.1/24

interface Vlan200
  no shutdown
  ip address 192.168.129.1/24

interface Vlan300
  no shutdown
  ip address 192.168.130.1/24

interface Ethernet1/1
  description P2P Link for MGMT
  no switchport
  ip address 192.168.120.4/24
  ip router ospf 400 area 0.0.164.85
  no shutdown

interface Ethernet1/2
  switchport mode trunk
  switchport trunk allowed vlan 100

interface Ethernet1/3
  switchport mode trunk
  switchport trunk allowed vlan 200

interface Ethernet1/4
  switchport mode trunk
  switchport trunk allowed vlan 300

interface Ethernet1/5
  no cdp enable
  no switchport
  ip address 172.16.25.2/24
  ip verify unicast source reachable-via any allow-default
  isis network point-to-point
  ip router isis 300
  no shutdown

interface Ethernet1/6
  shutdown

interface Ethernet1/7
  shutdown

interface Ethernet1/8
  shutdown

interface Ethernet1/9
  shutdown

interface Ethernet1/10
  shutdown

interface Ethernet1/11
  shutdown

interface Ethernet1/12
  shutdown

interface Ethernet1/13
  shutdown

interface Ethernet1/14
  shutdown

interface Ethernet1/15
  shutdown

interface Ethernet1/16
  shutdown

interface Ethernet1/17
  shutdown

interface Ethernet1/18
  shutdown

interface Ethernet1/19
  shutdown

interface Ethernet1/20
  shutdown
  switchport trunk allowed vlan 100

interface Ethernet1/21
  shutdown

interface Ethernet1/22
  shutdown

interface Ethernet1/23
  shutdown

interface Ethernet1/24
  shutdown

interface Ethernet1/25
  shutdown

interface Ethernet1/26
  shutdown

interface Ethernet1/27
  shutdown

interface Ethernet1/28
  shutdown

interface Ethernet1/29
  shutdown

interface Ethernet1/30
  shutdown
  switchport trunk allowed vlan 200

interface Ethernet1/31
  shutdown

interface Ethernet1/32
  shutdown

interface Ethernet1/33
  shutdown

interface Ethernet1/34
  shutdown

interface Ethernet1/35
  shutdown

interface Ethernet1/36
  shutdown

interface Ethernet1/37
  shutdown

interface Ethernet1/38
  shutdown

interface Ethernet1/39
  shutdown

interface Ethernet1/40
  shutdown
  switchport trunk allowed vlan 300

interface Ethernet1/41
  shutdown

interface Ethernet1/42
  shutdown

interface Ethernet1/43
  shutdown

interface Ethernet1/44
  shutdown

interface Ethernet1/45
  shutdown

interface Ethernet1/46
  shutdown

interface Ethernet1/47
  shutdown

interface Ethernet1/48
  shutdown

interface Ethernet1/49
  shutdown

interface Ethernet1/50
  shutdown

interface Ethernet1/51
  shutdown

interface Ethernet1/52
  shutdown

interface Ethernet1/53
  shutdown

interface Ethernet1/54
  shutdown

interface Ethernet1/55
  shutdown

interface Ethernet1/56
  shutdown

interface Ethernet1/57
  shutdown

interface Ethernet1/58
  shutdown

interface Ethernet1/59
  shutdown

interface Ethernet1/60
  shutdown

interface Ethernet1/61
  shutdown

interface Ethernet1/62
  shutdown

interface Ethernet1/63
  shutdown

interface Ethernet1/64
  shutdown

interface Ethernet1/65
  shutdown

interface Ethernet1/66
  shutdown

interface Ethernet1/67
  shutdown

interface Ethernet1/68
  shutdown

interface Ethernet1/69
  shutdown

interface Ethernet1/70
  shutdown

interface Ethernet1/71
  shutdown

interface Ethernet1/72
  shutdown

interface Ethernet1/73
  shutdown

interface Ethernet1/74
  shutdown

interface Ethernet1/75
  shutdown

interface Ethernet1/76
  shutdown

interface Ethernet1/77
  shutdown

interface Ethernet1/78
  shutdown

interface Ethernet1/79
  shutdown

interface Ethernet1/80
  shutdown

interface Ethernet1/81
  shutdown

interface Ethernet1/82
  shutdown

interface Ethernet1/83
  shutdown

interface Ethernet1/84
  shutdown

interface Ethernet1/85
  shutdown

interface Ethernet1/86
  shutdown

interface Ethernet1/87
  shutdown

interface Ethernet1/88
  shutdown

interface Ethernet1/89
  shutdown

interface Ethernet1/90
  shutdown

interface Ethernet1/91
  shutdown

interface Ethernet1/92
  shutdown

interface Ethernet1/93
  shutdown

interface Ethernet1/94
  shutdown

interface Ethernet1/95
  shutdown

interface Ethernet1/96
  shutdown

interface Ethernet1/97
  shutdown

interface Ethernet1/98
  shutdown

interface Ethernet1/99
  shutdown

interface Ethernet1/100
  shutdown

interface Ethernet1/101
  shutdown

interface Ethernet1/102
  shutdown

interface Ethernet1/103
  shutdown

interface Ethernet1/104
  shutdown

interface Ethernet1/105
  shutdown

interface Ethernet1/106
  shutdown

interface Ethernet1/107
  shutdown

interface Ethernet1/108
  shutdown

interface Ethernet1/109
  shutdown

interface Ethernet1/110
  shutdown

interface Ethernet1/111
  shutdown

interface Ethernet1/112
  shutdown

interface Ethernet1/113
  shutdown

interface Ethernet1/114
  shutdown

interface Ethernet1/115
  shutdown

interface Ethernet1/116
  shutdown

interface Ethernet1/117
  shutdown

interface Ethernet1/118
  shutdown

interface Ethernet1/119
  shutdown

interface Ethernet1/120
  shutdown

interface Ethernet1/121
  shutdown

interface Ethernet1/122
  shutdown

interface Ethernet1/123
  shutdown

interface Ethernet1/124
  shutdown

interface Ethernet1/125
  shutdown

interface Ethernet1/126
  shutdown

interface Ethernet1/127
  shutdown

interface Ethernet1/128
  shutdown

interface mgmt0
  vrf member management
  ip address 10.10.1.7/24

interface loopback0
  ip address 192.168.160.3/32
  ip ospf network point-to-point
  ip router ospf 400 area 0.0.164.85
line console
line vty
boot nxos bootflash:/nxos.9.2.1.bin
router ospf 400
  router-id 192.168.120.4
  default-information originate
  area 0.0.164.85 filter-list route-map OSPF-LOOPBACKS out
  area 0.0.164.85 filter-list route-map OSPF-LOOPBACKS in
router bgp 200
  router-id 192.168.160.3
  log-neighbor-changes
  address-family ipv4 unicast
    network 192.168.128.0/24
    network 192.168.129.0/24
    network 192.168.130.0/24
  neighbor 192.168.160.2
    remote-as 200
    dont-capability-negotiate
    update-source loopback0
    address-family ipv4 unicast
      prefix-list BGP-ROUTES out
      soft-reconfiguration inbound”
```

#### Playbook Example 5
This specific playbook will pull all configuration and dump into a file on your ansible server.

```bash
  [ansible@ansible nexus]$ ansible-playbook nexus9k/nexus9k-get-configuration-hierarchies.yaml

PLAY [Get Nexus 9K OS configuration via SSH] *************************************************************************************************************************************

TASK [Gathering Facts] ***********************************************************************************************************************************************************
ok: [cisco-nexus1]

TASK [confirm or create configs directory] ***************************************************************************************************************************************
ok: [cisco-nexus1]

TASK [Get selected configuration hierarchies and save to file] *******************************************************************************************************************
ok: [cisco-nexus1]

TASK [Save config output] ********************************************************************************************************************************************************
changed: [cisco-nexus1]

PLAY RECAP ***********************************************************************************************************************************************************************
cisco-nexus1               : ok=4    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

#####  Validation

```bash
[ansible@ansible nexus]$ cat nexus9k/configs/show_run_cisco-nexus1.txt
“!Command: show running-config
!Running configuration last done at: Sat Sep 14 17:44:46 2024
!Time: Sat Sep 14 17:45:33 2024

version 9.2(1) Bios:version
hostname cisco-nexus1
vdc cisco-nexus1 id 1
  limit-resource vlan minimum 16 maximum 4094
  limit-resource vrf minimum 2 maximum 4096
  limit-resource port-channel minimum 0 maximum 511
  limit-resource u4route-mem minimum 248 maximum 248
  limit-resource u6route-mem minimum 96 maximum 96
  limit-resource m4route-mem minimum 58 maximum 58
  limit-resource m6route-mem minimum 8 maximum 8

feature scp-server
feature sftp-server
feature ospf
feature bgp
feature isis
feature interface-vlan

banner motd @
                     **** WARNING NOTICE ****
This system is restricted solely to authorized users for legitimate
  purposes only. The actual or attempted unauthorized access, use
      or modification of this system is strictly prohibited.
   Unauthorized users are subject to disciplinary proceedings
and/or criminal and civil penalties under state, federal or other
applicable domestic and foreign laws. The use of this system may be
monitored and recorded for administrative and security reasons. Anyone
accessing this system expressly consents to such monitoring and is
advised that if such monitoring reveals possible evidence of criminal
activity, the owner may provide the evidence of such activity to law
                      enforcement officials.
@

ip domain-lookup
ip name-server 192.168.120.1
crypto key param rsa label vswitch1 modulus 2048
copp profile strict
ip ssh source-interface mgmt0
rmon event 1 description FATAL(1) owner PMON@FATAL
rmon event 2 description CRITICAL(2) owner PMON@CRITICAL
rmon event 3 description ERROR(3) owner PMON@ERROR
rmon event 4 description WARNING(4) owner PMON@WARNING
rmon event 5 description INFORMATION(5) owner PMON@INFO
snmp-server community DveviM5YpB!! group network-operator

ip route 0.0.0.0/0 Ethernet1/1 192.168.120.1
vlan 1,100,200,300,400

ip prefix-list BGP_ROUTES seq 5 permit 192.168.128.0/24 le 32
ip prefix-list BGP_ROUTES seq 10 permit 192.168.129.0/24 le 32
ip prefix-list BGP_ROUTES seq 15 permit 192.168.130.0/24 le 32
ip prefix-list OSPF-LOOPBACKS seq 10 permit 192.168.160.0/29 ge 30
route-map BGP-ROUTES permit 10
  match ip address prefix-list BGP_ROUTES
route-map LOCAL-PREF permit 10
  match ospf-area 400
  set local-preference 200
route-map OSPF-LOOPBACKS permit 10
  match ip address prefix-list OSPF-LOOPBACKS
vrf context management
  ip route 0.0.0.0/0 mgmt0 10.10.1.1


interface Vlan1

interface Vlan100
  no shutdown
  ip address 192.168.128.1/24

interface Vlan200
  no shutdown
  ip address 192.168.129.1/24

interface Vlan300
  no shutdown
  ip address 192.168.130.1/24

interface Ethernet1/1
  description P2P Link for MGMT
  no switchport
  ip address 192.168.120.4/24
  ip router ospf 400 area 0.0.164.85
  no shutdown

interface Ethernet1/2
  switchport mode trunk
  switchport trunk allowed vlan 100

interface Ethernet1/3
  switchport mode trunk
  switchport trunk allowed vlan 200

interface Ethernet1/4
  switchport mode trunk
  switchport trunk allowed vlan 300

interface Ethernet1/5
  no cdp enable
  no switchport
  ip address 172.16.25.2/24
  ip verify unicast source reachable-via any allow-default
  isis network point-to-point
  ip router isis 300
  no shutdown

interface Ethernet1/6
  shutdown

interface Ethernet1/7
  shutdown

interface Ethernet1/8
  shutdown

interface Ethernet1/9
  shutdown

interface Ethernet1/10
  shutdown

interface Ethernet1/11
  shutdown

interface Ethernet1/12
  shutdown

interface Ethernet1/13
  shutdown

interface Ethernet1/14
  shutdown

interface Ethernet1/15
  shutdown

interface Ethernet1/16
  shutdown

interface Ethernet1/17
  shutdown

interface Ethernet1/18
  shutdown

interface Ethernet1/19
  shutdown

interface Ethernet1/20
  shutdown
  switchport trunk allowed vlan 100

interface Ethernet1/21
  shutdown

interface Ethernet1/22
  shutdown

interface Ethernet1/23
  shutdown

interface Ethernet1/24
  shutdown

interface Ethernet1/25
  shutdown

interface Ethernet1/26
  shutdown

interface Ethernet1/27
  shutdown

interface Ethernet1/28
  shutdown

interface Ethernet1/29
  shutdown

interface Ethernet1/30
  shutdown
  switchport trunk allowed vlan 200

interface Ethernet1/31
  shutdown

interface Ethernet1/32
  shutdown

interface Ethernet1/33
  shutdown

interface Ethernet1/34
  shutdown

interface Ethernet1/35
  shutdown

interface Ethernet1/36
  shutdown

interface Ethernet1/37
  shutdown

interface Ethernet1/38
  shutdown

interface Ethernet1/39
  shutdown

interface Ethernet1/40
  shutdown
  switchport trunk allowed vlan 300

interface Ethernet1/41
  shutdown

interface Ethernet1/42
  shutdown

interface Ethernet1/43
  shutdown

interface Ethernet1/44
  shutdown

interface Ethernet1/45
  shutdown

interface Ethernet1/46
  shutdown

interface Ethernet1/47
  shutdown

interface Ethernet1/48
  shutdown

interface Ethernet1/49
  shutdown

interface Ethernet1/50
  shutdown

interface Ethernet1/51
  shutdown

interface Ethernet1/52
  shutdown

interface Ethernet1/53
  shutdown

interface Ethernet1/54
  shutdown

interface Ethernet1/55
  shutdown

interface Ethernet1/56
  shutdown

interface Ethernet1/57
  shutdown

interface Ethernet1/58
  shutdown

interface Ethernet1/59
  shutdown

interface Ethernet1/60
  shutdown

interface Ethernet1/61
  shutdown

interface Ethernet1/62
  shutdown

interface Ethernet1/63
  shutdown

interface Ethernet1/64
  shutdown

interface Ethernet1/65
  shutdown

interface Ethernet1/66
  shutdown

interface Ethernet1/67
  shutdown

interface Ethernet1/68
  shutdown

interface Ethernet1/69
  shutdown

interface Ethernet1/70
  shutdown

interface Ethernet1/71
  shutdown

interface Ethernet1/72
  shutdown

interface Ethernet1/73
  shutdown

interface Ethernet1/74
  shutdown

interface Ethernet1/75
  shutdown

interface Ethernet1/76
  shutdown

interface Ethernet1/77
  shutdown

interface Ethernet1/78
  shutdown

interface Ethernet1/79
  shutdown

interface Ethernet1/80
  shutdown

interface Ethernet1/81
  shutdown

interface Ethernet1/82
  shutdown

interface Ethernet1/83
  shutdown

interface Ethernet1/84
  shutdown

interface Ethernet1/85
  shutdown

interface Ethernet1/86
  shutdown

interface Ethernet1/87
  shutdown

interface Ethernet1/88
  shutdown

interface Ethernet1/89
  shutdown

interface Ethernet1/90
  shutdown

interface Ethernet1/91
  shutdown

interface Ethernet1/92
  shutdown

interface Ethernet1/93
  shutdown

interface Ethernet1/94
  shutdown

interface Ethernet1/95
  shutdown

interface Ethernet1/96
  shutdown

interface Ethernet1/97
  shutdown

interface Ethernet1/98
  shutdown

interface Ethernet1/99
  shutdown

interface Ethernet1/100
  shutdown

interface Ethernet1/101
  shutdown

interface Ethernet1/102
  shutdown

interface Ethernet1/103
  shutdown

interface Ethernet1/104
  shutdown

interface Ethernet1/105
  shutdown

interface Ethernet1/106
  shutdown

interface Ethernet1/107
  shutdown

interface Ethernet1/108
  shutdown

interface Ethernet1/109
  shutdown

interface Ethernet1/110
  shutdown

interface Ethernet1/111
  shutdown

interface Ethernet1/112
  shutdown

interface Ethernet1/113
  shutdown

interface Ethernet1/114
  shutdown

interface Ethernet1/115
  shutdown

interface Ethernet1/116
  shutdown

interface Ethernet1/117
  shutdown

interface Ethernet1/118
  shutdown

interface Ethernet1/119
  shutdown

interface Ethernet1/120
  shutdown

interface Ethernet1/121
  shutdown

interface Ethernet1/122
  shutdown

interface Ethernet1/123
  shutdown

interface Ethernet1/124
  shutdown

interface Ethernet1/125
  shutdown

interface Ethernet1/126
  shutdown

interface Ethernet1/127
  shutdown

interface Ethernet1/128
  shutdown

interface mgmt0
  vrf member management
  ip address 10.10.1.7/24

interface loopback0
  ip address 192.168.160.3/32
  ip ospf network point-to-point
  ip router ospf 400 area 0.0.164.85
line console
line vty
boot nxos bootflash:/nxos.9.2.1.bin
router ospf 400
  router-id 192.168.120.4
  default-information originate
  area 0.0.164.85 filter-list route-map OSPF-LOOPBACKS out
  area 0.0.164.85 filter-list route-map OSPF-LOOPBACKS in
router bgp 200
  router-id 192.168.160.3
  log-neighbor-changes
  address-family ipv4 unicast
    network 192.168.128.0/24
    network 192.168.129.0/24
    network 192.168.130.0/24
  neighbor 192.168.160.2
    remote-as 200
    dont-capability-negotiate
    update-source loopback0
    address-family ipv4 unicast
      prefix-list BGP-ROUTES out
      soft-reconfiguration inbound”
```

