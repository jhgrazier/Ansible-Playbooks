
# Cisco CSR1000V
Playbooks for Managing Cisco CSR1000V

## Installation Requirements

Ansible 2.5
Python 3.8+
ansible-pylibssh

### Cisco Required Modules

```bash
ansible-galaxy collection install cisco.ios
pip install ansible-pylibssh
```

## Playbook Usage / Examples

### Install Playbook to your Ansible Host
Depending on what you need, you can pull system configuration, interface configuration, services configuration, etc.

Run the Playbooks

#### Playbook Example 1
This specific playbook will configure hostname, dns lookup sources, nameservers, remove the old login banner and update the login banner..

```bash
[ansible@ansible]$ ansible-playbook csr1000v/csr1000v-configure-top-level-config.yaml

PLAY [Configure top level config] ************************************************************************************************************************************************

TASK [Configure hostname] ********************************************************************************************************************************************************
changed: [cisco-router1]

TASK [configure DNS lookup sources] **********************************************************************************************************************************************
changed: [cisco-router1]

TASK [configure name servers] ****************************************************************************************************************************************************
changed: [cisco-router1]

TASK [Remove uneeded banners] ****************************************************************************************************************************************************
ok: [cisco-router1] => (item=motd)
ok: [cisco-router1] => (item=exec)
ok: [cisco-router1] => (item=incoming)

TASK [Update login banner] *******************************************************************************************************************************************************
changed: [cisco-router1]

PLAY RECAP ***********************************************************************************************************************************************************************
cisco-router1              : ok=5    changed=4    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

#### Playbook Example 2
This specific playbook will replace OSPF level configuration.

```bash
[ansible@ansible]$ ansible-playbook csr1000v/csr1000v-configure-ospf-level-config.yaml
```

#### Playbook Example 3 
This specific playbook will pull all configuration and dump into a file on your ansible server.

```bash
[ansible@ansible routers]$ ansible-playbook csr1000v/csr1000v-get-configuration-hierarchies.yaml

PLAY [Get CSR1000V OS configuration via SSH] *************************************************************************************************************************************

TASK [Gathering Facts] ***********************************************************************************************************************************************************
ok: [cisco-router1]

TASK [confirm or create configs directory] ***************************************************************************************************************************************
changed: [cisco-router1]

TASK [Get selected configuration hierarchies and save to file] *******************************************************************************************************************
ok: [cisco-router1]

TASK [Save config output] ********************************************************************************************************************************************************
changed: [cisco-router1]

PLAY RECAP ***********************************************************************************************************************************************************************
cisco-router1              : ok=4    changed=2    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```
##### Validation

```bash
[ansible@ansible csr1000v]$ cat configs/show_run_cisco-router1.txt
“Building configuration...

Current configuration : 4666 bytes
!
! Last configuration change at 15:32:31 UTC Sat Sep 14 2024 by ansible
!
version 16.3
service timestamps debug datetime msec
service timestamps log datetime msec
no platform punt-keepalive disable-kernel-core
platform console auto
!
hostname cisco-router1
!
boot-start-marker
boot-end-marker
!
!
no logging console
!
aaa new-model
!
!
aaa authentication login default local
aaa authentication enable default none
aaa authorization exec default local if-authenticated
!
!
!
!
!
aaa session-id common
no process cpu autoprofile hog
!
ip multicast-routing distributed
!
!
!
!
!
!
!
!
ip name-server 192.168.120.1
no ip domain lookup
ip domain name ignyte.lab
!
!
!
!
!
!
!
!
!
!
subscriber templating
!
!
!
multilink bundle-name authenticated
!
domain ignyte.lab
!
!
!
!
!
!
!
!
!
!
!
!
!
license udi pid CSR1000V sn 99E74LGZD6J
diagnostic bootup level minimal
!
spanning-tree extend system-id
!
!
!
redundancy
!
!
!
!
!
cdp run
!
!
!
!
!
!
!
!
!
!
!
!
!
!
!
!
!
!
!
!
!
!
interface Loopback0
 ip address 192.168.160.2 255.255.255.255
 ip ospf 400 area 0.0.164.85
!
interface GigabitEthernet1
 description P2P Link for MGMT
 ip address 192.168.120.3 255.255.255.0
 no ip redirects
 ip ospf 400 area 0.0.164.85
 negotiation auto
 no mop enabled
 no mop sysid
!
interface GigabitEthernet2
 dampening
 ip address 172.16.25.1 255.255.255.0
 no ip redirects
 no ip unreachables
 no ip proxy-arp
 ip router isis 300
 load-interval 30
 negotiation auto
 no mop enabled
 no mop sysid
!
interface GigabitEthernet3
 ip address 172.16.29.1 255.255.255.0
 negotiation auto
 no mop enabled
 no mop sysid
!
router ospf 400
 router-id 192.168.120.3
 network 192.168.160.0 0.0.0.255 area 0.0.164.85
 default-information originate
!
router isis 300
 net 49.0000.0000.0000.0000.0003.00
 is-type level-2-only
 router-id Loopback0
 metric-style wide
 log-adjacency-changes
 nsf ietf
 passive-interface default
 no passive-interface GigabitEthernet2
!
router bgp 200
 bgp router-id 192.168.160.2
 bgp log-neighbor-changes
 bgp graceful-restart restart-time 1
 bgp graceful-restart
 neighbor 192.168.160.1 remote-as 200
 neighbor 192.168.160.1 description juniper-srx
 neighbor 192.168.160.1 update-source Loopback0
 neighbor 192.168.160.3 remote-as 200
 neighbor 192.168.160.3 description nexus-switch
 neighbor 192.168.160.3 dont-capability-negotiate enhanced-refresh
 neighbor 192.168.160.3 update-source Loopback0
 !
 address-family ipv4
  network 192.168.128.0
  network 192.168.129.0
  network 192.168.130.0
  neighbor 192.168.160.1 activate
  neighbor 192.168.160.1 route-reflector-client
  neighbor 192.168.160.1 soft-reconfiguration inbound
  neighbor 192.168.160.1 prefix-list BGP-ROUTES out
  neighbor 192.168.160.3 activate
  neighbor 192.168.160.3 next-hop-self
  neighbor 192.168.160.3 soft-reconfiguration inbound
  neighbor 192.168.160.3 prefix-list BGP-ROUTES in
 exit-address-family
!
!
virtual-service csr_mgmt
!
ip forward-protocol nd
no ip http server
no ip http secure-server
!
ip route 0.0.0.0 0.0.0.0 GigabitEthernet1 192.168.120.1
ip ssh source-interface GigabitEthernet1
ip ssh version 2
!
!
!
ip prefix-list BGP_ROUTES seq 5 permit 192.168.128.0/24 le 32
ip prefix-list BGP_ROUTES seq 10 permit 192.168.129.0/24 le 32
ip prefix-list BGP_ROUTES seq 15 permit 192.168.130.0/24 le 32
!
!
route-map OSPF-LOOPBACKS permit 10
 match ip address prefix-list OSPF-LOOPBACKS
!
route-map BGP-ROUTES permit 10
 match ip address prefix-list BGP_ROUTES
!
snmp-server community public RO
!
!
!
!
control-plane
!
 !
 !
 !
 !
!
!
!
!
banner login ^C
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
^C
!
line con 0
 stopbits 1
line vty 1
 length 0
line vty 2 4
!
wsma agent exec
!
wsma agent config
!
wsma agent filesys
!
wsma agent notify
!
!
```
