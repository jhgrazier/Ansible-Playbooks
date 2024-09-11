
# Juniper Playbooks
Playbooks for Managing Juniper Devices

## Installation Requirements

Ansible 2.5
Python 3.8+
jxmlease
xmltodict
jsnapy

###Juniper Required Modules

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

####Playbook Example 1
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
        "config": "<configuration commit-seconds=\"1725834513\" commit-localtime=\"2024-09-08 16:28:33 MDT\" commit-user=\"root\">\n  <interfaces>\n    <interface>\n      <name>ge-0/0/0</name>\n      <unit>\n        <name>0</name>\n        <description>SRX-WAN</description>\n        <family>\n          <inet>\n            <dhcp>\n                        </dhcp>\n          </inet>\n          <inet6>\n            <address>\n              <name>26XX:XXX:XXX:4158::2/64</name>\n            </address>\n          </inet6>\n        </family>\n      </unit>\n    </interface>\n    <interface>\n      <name>gr-0/0/0</name>\n      <unit>\n        <name>0</name>\n        <tunnel>\n          <source>172.19.1.2</source>\n          <destination>172.19.1.1</destination>\n        </tunnel>\n        <family>\n          <inet>\n            <mtu>1476</mtu>\n            <address>\n              <name>172.19.2.9/30</name>\n            </address>\n          </inet>\n        </family>\n      </unit>\n    </interface>\n    <interface>\n      <name>ge-0/0/1</name>\n      <description>SRX-LAN</description>\n      <unit>\n        <name>0</name>\n        <family>\n          <ethernet-switching>\n            <interface-mode>trunk</interface-mode>\n            <vlan>\n              <members>vlan-150</members>\n              <members>vlan-400</members>\n              <members>vlan-401</members>\n              <members>vlan-402</members>\n              <members>vlan-403</members>\n              <members>vlan-404</members>\n              <members>vlan-405</members>\n              <members>vlan-406</members>\n              <members>vlan-407</members>\n              <members>vlan-408</members>\n              <members>vlan-409</members>\n              <members>vlan-410</members>\n              <members>vlan-175</members>\n              <members>vlan-411</members>\n              <members>vlan-200</members>\n            </vlan>\n          </ethernet-switching>\n        </family>\n      </unit>\n    </interface>\n    <interface>\n      <name>ge-0/0/2</name>\n      <description>R620 VMWARE-ESXI-MGMT-PORT</description>\n      <unit>\n        <name>0</name>\n        <family>\n          <ethernet-switching>\n            <vlan>\n              <members>vlan-150</members>\n            </vlan>\n          </ethernet-switching>\n        </family>\n      </unit>\n    </interface>\n    <interface>\n      <name>ge-0/0/3</name>\n      <description>R620-VMWARE-ESXI-VM-PORT</description>\n      <unit>\n        <name>0</name>\n        <family>\n          <ethernet-switching>\n            <interface-mode>trunk</interface-mode>\n            <vlan>\n              <members>vlan-150</members>\n              <members>vlan-400</members>\n              <members>vlan-401</members>\n              <members>vlan-402</members>\n              <members>vlan-403</members>\n              <members>vlan-404</members>\n              <members>vlan-405</members>\n              <members>vlan-406</members>\n              <members>vlan-407</members>\n              <members>vlan-408</members>\n              <members>vlan-409</members>\n              <members>vlan-410</members>\n              <members>vlan-175</members>\n              <members>vlan-411</members>\n              <members>vlan-200</members>\n            </vlan>\n          </ethernet-switching>\n        </family>\n      </unit>\n    </interface>\n    <interface>\n      <name>ge-0/0/4</name>\n      <description>R620-VMWARE-ESXI-VM-PORT</description>\n      <unit>\n        <name>0</name>\n        <description>VMWARE-ESXI-VM-PORT</description>\n        <family>\n          <ethernet-switching>\n            <interface-mode>trunk</interface-mode>\n            <vlan>\n              <members>vlan-150</members>\n              <members>vlan-400</members>\n              <members>vlan-401</members>\n              <members>vlan-402</members>\n              <members>vlan-403</members>\n              <members>vlan-404</members>\n              <members>vlan-405</members>\n              <members>vlan-406</members>\n              <members>vlan-407</members>\n              <members>vlan-408</members>\n              <members>vlan-409</members>\n              <members>vlan-410</members>\n              <members>vlan-175</members>\n              <members>vlan-411</members>\n              <members>vlan-200</members>\n            </vlan>\n          </ethernet-switching>\n        </family>\n      </unit>\n    </interface>\n    <interface>\n      <name>ge-0/0/5</name>\n      <description>VMWARE-ESXI-MGMT-PORT</description>\n      <unit>\n        <name>0</name>\n        <family>\n          <ethernet-switching>\n            <vlan>\n              <members>vlan-150</members>\n            </vlan>\n          </ethernet-switching>\n        </family>\n      </unit>\n    </interface>\n    <interface>\n      <name>ge-0/0/6</name>\n      <unit>\n        <name>0</name>\n        <family>\n          <ethernet-switching>\n            <vlan>\n              <members>vlan-150</members>\n            </vlan>\n          </ethernet-switching>\n        </family>\n      </unit>\n    </interface>\n    <interface>\n      <name>ge-0/0/7</name>\n      <unit>\n        <name>0</name>\n        <family>\n          <inet>\n            <dhcp>\n              <vendor-id>Juniper-srx320</vendor-id>\n            </dhcp>\n          </inet>\n        </family>\n      </unit>\n    </interface>\n    <interface>\n      <name>cl-1/0/0</name>\n      <dialer-options>\n        <pool>\n          <name>1</name>\n          <priority>100</priority>\n        </pool>\n      </dialer-options>\n    </interface>\n    <interface>\n      <name>dl0</name>\n      <unit>\n        <name>0</name>\n        <family>\n          <inet>\n            <negotiate-address/>\n          </inet>\n          <inet6>\n            <negotiate-address/>\n          </inet6>\n        </family>\n        <dialer-options>\n          <pool>1</pool>\n          <dial-string>1234</dial-string>\n          <always-on/>\n        </dialer-options>\n      </unit>\n    </interface>\n    <interface>\n      <name>irb</name>\n      <unit>\n        <name>0</name>\n        <family>\n          <inet>\n                    </inet>\n        </family>\n      </unit>\n      <unit>\n        <name>150</name>\n        <family>\n          <inet>\n            <address>\n              <name>10.10.1.2/24</name>\n            </address>\n          </inet>\n          <inet6>\n            <address>\n              <name>2XXX:XXX:XXXX:4157::2/64</name>\n            </address>\n          </inet6>\n        </family>\n      </unit>\n      <unit>\n        <name>175</name>\n        <family>\n          <inet>\n            <address>\n              <name>10.10.2.2/24</name>\n            </address>\n          </inet>\n          <inet6>\n            <address>\n              <name>2XXX:XXX:XXXX:415c::2/64</name>\n            </address>\n          </inet6>\n        </family>\n      </unit>\n      <unit>\n        <name>200</name>\n        <family>\n          <inet>\n            <address>\n              <name>192.168.99.2/24</name>\n            </address>\n          </inet>\n        </family>\n      </unit>\n      <unit>\n        <name>400</name>\n        <family>\n          <inet>\n            <address>\n              <name>192.168.120.2/24</name>\n            </address>\n          </inet>\n        </family>\n      </unit>\n      <unit>\n        <name>401</name>\n        <family>\n          <inet>\n            <address>\n              <name>192.168.121.2/24</name>\n            </address>\n          </inet>\n        </family>\n      </unit>\n      <unit>\n        <name>402</name>\n        <family>\n          <inet>\n            <address>\n              <name>192.168.122.2/24</name>\n            </address>\n          </inet>\n        </family>\n      </unit>\n      <unit>\n        <name>403</name>\n        <family>\n          <inet>\n            <address>\n              <name>192.168.123.2/24</name>\n            </address>\n          </inet>\n        </family>\n      </unit>\n      <unit>\n        <name>404</name>\n        <family>\n          <inet>\n            <address>\n              <name>192.168.124.2/24</name>\n            </address>\n          </inet>\n        </family>\n      </unit>\n      <unit>\n        <name>405</name>\n        <family>\n          <inet>\n            <address>\n              <name>192.168.125.2/24</name>\n            </address>\n          </inet>\n        </family>\n      </unit>\n      <unit>\n        <name>406</name>\n        <family>\n          <inet>\n            <address>\n              <name>192.168.126.2/24</name>\n            </address>\n          </inet>\n          <inet6>\n                    </inet6>\n        </family>\n      </unit>\n      <unit>\n        <name>407</name>\n        <family>\n          <inet>\n            <address>\n              <name>192.168.168.2/24</name>\n            </address>\n          </inet>\n          <inet6>\n            <address>\n              <name>2XXX:XXX:XXXX:415a::2/64</name>\n            </address>\n          </inet6>\n        </family>\n      </unit>\n      <unit>\n        <name>408</name>\n        <family>\n          <inet>\n            <address>\n              <name>192.168.169.2/24</name>\n            </address>\n          </inet>\n          <inet6>\n            <address>\n              <name>2XXX:XXX:XXXX:415b::2/64</name>\n            </address>\n          </inet6>\n        </family>\n      </unit>\n      <unit>\n        <name>409</name>\n        <family>\n          <inet>\n            <address>\n              <name>192.168.170.2/24</name>\n            </address>\n          </inet>\n          <inet6>\n            <address>\n              <name>2XXX:XXX:XXXX:4159::2/64</name>\n            </address>\n          </inet6>\n        </family>\n      </unit>\n      <unit>\n        <name>410</name>\n        <family>\n          <inet>\n            <address>\n              <name>192.168.171.2/24</name>\n            </address>\n          </inet>\n        </family>\n      </unit>\n      <unit>\n        <name>411</name>\n        <family>\n          <inet>\n            <address>\n              <name>172.18.1.2/28</name>\n            </address>\n          </inet>\n        </family>\n      </unit>\n    </interface>\n    <interface>\n      <name>lo0</name>\n      <unit>\n        <name>0</name>\n        <family>\n          <inet>\n            <address>\n              <name>127.0.0.1/32</name>\n            </address>\n            <address>\n              <name>192.168.160.1/32</name>\n            </address>\n          </inet>\n        </family>\n      </unit>\n    </interface>\n    <interface>\n      <name>st0</name>\n      <unit>\n        <name>0</name>\n        <family>\n          <inet>\n            <address>\n              <name>10.50.5.1/30</name>\n            </address>\n          </inet>\n          <inet6>\n                    </inet6>\n        </family>\n      </unit>\n    </interface>\n  </interfaces>\n</configuration>\n",
        "config_lines": [
            "<configuration commit-seconds=\"1725834513\" commit-localtime=\"2024-09-08 16:28:33 MDT\" commit-user=\"root\">",
            "  <interfaces>",
            "    <interface>",
            "      <name>ge-0/0/0</name>",
            "      <unit>",
            "        <name>0</name>",
            "        <description>SRX-WAN</description>",
            "        <family>",
            "          <inet>",
            "            <dhcp>",
            "                        </dhcp>",
            "          </inet>",
            "          <inet6>",
            "            <address>",
            "              <name>2XXX:XXX:XXXX:XXXX::2/64</name>",
            "            </address>",
            "          </inet6>",
            "        </family>",
            "      </unit>",
            "    </interface>",
            "    <interface>",
            "      <name>gr-0/0/0</name>",
            "      <unit>",
            "        <name>0</name>",
            "        <tunnel>",
            "          <source>172.19.1.2</source>",
            "          <destination>172.19.1.1</destination>",
            "        </tunnel>",
            "        <family>",
            "          <inet>",
            "            <mtu>1476</mtu>",
            "            <address>",
            "              <name>172.19.2.9/30</name>",
            "            </address>",
            "          </inet>",
            "        </family>",
            "      </unit>",
            "    </interface>",
            "    <interface>",
            "      <name>ge-0/0/1</name>",
            "      <description>SRX-LAN</description>",
            "      <unit>",
            "        <name>0</name>",
            "        <family>",
            "          <ethernet-switching>",
            "            <interface-mode>trunk</interface-mode>",
            "            <vlan>",
            "              <members>vlan-150</members>",
            "              <members>vlan-400</members>",
            "              <members>vlan-401</members>",
            "              <members>vlan-402</members>",
            "              <members>vlan-403</members>",
            "              <members>vlan-404</members>",
            "              <members>vlan-405</members>",
            "              <members>vlan-406</members>",
            "              <members>vlan-407</members>",
            "              <members>vlan-408</members>",
            "              <members>vlan-409</members>",
            "              <members>vlan-410</members>",
            "              <members>vlan-175</members>",
            "              <members>vlan-411</members>",
            "              <members>vlan-200</members>",
            "            </vlan>",
            "          </ethernet-switching>",
            "        </family>",
            "      </unit>",
            "    </interface>",
            "    <interface>",
            "      <name>ge-0/0/2</name>",
            "      <description>R620 VMWARE-ESXI-MGMT-PORT</description>",
            "      <unit>",
            "        <name>0</name>",
            "        <family>",
            "          <ethernet-switching>",
            "            <vlan>",
            "              <members>vlan-150</members>",
            "            </vlan>",
            "          </ethernet-switching>",
            "        </family>",
            "      </unit>",
            "    </interface>",
            "    <interface>",
            "      <name>ge-0/0/3</name>",
            "      <description>R620-VMWARE-ESXI-VM-PORT</description>",
            "      <unit>",
            "        <name>0</name>",
            "        <family>",
            "          <ethernet-switching>",
            "            <interface-mode>trunk</interface-mode>",
            "            <vlan>",
            "              <members>vlan-150</members>",
            "              <members>vlan-400</members>",
            "              <members>vlan-401</members>",
            "              <members>vlan-402</members>",
            "              <members>vlan-403</members>",
            "              <members>vlan-404</members>",
            "              <members>vlan-405</members>",
            "              <members>vlan-406</members>",
            "              <members>vlan-407</members>",
            "              <members>vlan-408</members>",
            "              <members>vlan-409</members>",
            "              <members>vlan-410</members>",
            "              <members>vlan-175</members>",
            "              <members>vlan-411</members>",
            "              <members>vlan-200</members>",
            "            </vlan>",
            "          </ethernet-switching>",
            "        </family>",
            "      </unit>",
            "    </interface>",
            "    <interface>",
            "      <name>ge-0/0/4</name>",
            "      <description>R620-VMWARE-ESXI-VM-PORT</description>",
            "      <unit>",
            "        <name>0</name>",
            "        <description>VMWARE-ESXI-VM-PORT</description>",
            "        <family>",
            "          <ethernet-switching>",
            "            <interface-mode>trunk</interface-mode>",
            "            <vlan>",
            "              <members>vlan-150</members>",
            "              <members>vlan-400</members>",
            "              <members>vlan-401</members>",
            "              <members>vlan-402</members>",
            "              <members>vlan-403</members>",
            "              <members>vlan-404</members>",
            "              <members>vlan-405</members>",
            "              <members>vlan-406</members>",
            "              <members>vlan-407</members>",
            "              <members>vlan-408</members>",
            "              <members>vlan-409</members>",
            "              <members>vlan-410</members>",
            "              <members>vlan-175</members>",
            "              <members>vlan-411</members>",
            "              <members>vlan-200</members>",
            "            </vlan>",
            "          </ethernet-switching>",
            "        </family>",
            "      </unit>",
            "    </interface>",
            "    <interface>",
            "      <name>ge-0/0/5</name>",
            "      <description>VMWARE-ESXI-MGMT-PORT</description>",
            "      <unit>",
            "        <name>0</name>",
            "        <family>",
            "          <ethernet-switching>",
            "            <vlan>",
            "              <members>vlan-150</members>",
            "            </vlan>",
            "          </ethernet-switching>",
            "        </family>",
            "      </unit>",
            "    </interface>",
            "    <interface>",
            "      <name>ge-0/0/6</name>",
            "      <unit>",
            "        <name>0</name>",
            "        <family>",
            "          <ethernet-switching>",
            "            <vlan>",
            "              <members>vlan-150</members>",
            "            </vlan>",
            "          </ethernet-switching>",
            "        </family>",
            "      </unit>",
            "    </interface>",
            "    <interface>",
            "      <name>ge-0/0/7</name>",
            "      <unit>",
            "        <name>0</name>",
            "        <family>",
            "          <inet>",
            "            <dhcp>",
            "              <vendor-id>Juniper-srx320</vendor-id>",
            "            </dhcp>",
            "          </inet>",
            "        </family>",
            "      </unit>",
            "    </interface>",
            "    <interface>",
            "      <name>cl-1/0/0</name>",
            "      <dialer-options>",
            "        <pool>",
            "          <name>1</name>",
            "          <priority>100</priority>",
            "        </pool>",
            "      </dialer-options>",
            "    </interface>",
            "    <interface>",
            "      <name>dl0</name>",
            "      <unit>",
            "        <name>0</name>",
            "        <family>",
            "          <inet>",
            "            <negotiate-address/>",
            "          </inet>",
            "          <inet6>",
            "            <negotiate-address/>",
            "          </inet6>",
            "        </family>",
            "        <dialer-options>",
            "          <pool>1</pool>",
            "          <dial-string>1234</dial-string>",
            "          <always-on/>",
            "        </dialer-options>",
            "      </unit>",
            "    </interface>",
            "    <interface>",
            "      <name>irb</name>",
            "      <unit>",
            "        <name>0</name>",
            "        <family>",
            "          <inet>",
            "                    </inet>",
            "        </family>",
            "      </unit>",
            "      <unit>",
            "        <name>150</name>",
            "        <family>",
            "          <inet>",
            "            <address>",
            "              <name>10.10.1.2/24</name>",
            "            </address>",
            "          </inet>",
            "          <inet6>",
            "            <address>",
            "              <name>2XXX:XXX:XXXX:4157::2/64</name>",
            "            </address>",
            "          </inet6>",
            "        </family>",
            "      </unit>",
            "      <unit>",
            "        <name>175</name>",
            "        <family>",
            "          <inet>",
            "            <address>",
            "              <name>10.10.2.2/24</name>",
            "            </address>",
            "          </inet>",
            "          <inet6>",
            "            <address>",
            "              <name>2XXX:XXX:XXXX:415c::2/64</name>",
            "            </address>",
            "          </inet6>",
            "        </family>",
            "      </unit>",
            "      <unit>",
            "        <name>200</name>",
            "        <family>",
            "          <inet>",
            "            <address>",
            "              <name>192.168.99.2/24</name>",
            "            </address>",
            "          </inet>",
            "        </family>",
            "      </unit>",
            "      <unit>",
            "        <name>400</name>",
            "        <family>",
            "          <inet>",
            "            <address>",
            "              <name>192.168.120.2/24</name>",
            "            </address>",
            "          </inet>",
            "        </family>",
            "      </unit>",
            "      <unit>",
            "        <name>401</name>",
            "        <family>",
            "          <inet>",
            "            <address>",
            "              <name>192.168.121.2/24</name>",
            "            </address>",
            "          </inet>",
            "        </family>",
            "      </unit>",
            "      <unit>",
            "        <name>402</name>",
            "        <family>",
            "          <inet>",
            "            <address>",
            "              <name>192.168.122.2/24</name>",
            "            </address>",
            "          </inet>",
            "        </family>",
            "      </unit>",
            "      <unit>",
            "        <name>403</name>",
            "        <family>",
            "          <inet>",
            "            <address>",
            "              <name>192.168.123.2/24</name>",
            "            </address>",
            "          </inet>",
            "        </family>",
            "      </unit>",
            "      <unit>",
            "        <name>404</name>",
            "        <family>",
            "          <inet>",
            "            <address>",
            "              <name>192.168.124.2/24</name>",
            "            </address>",
            "          </inet>",
            "        </family>",
            "      </unit>",
            "      <unit>",
            "        <name>405</name>",
            "        <family>",
            "          <inet>",
            "            <address>",
            "              <name>192.168.125.2/24</name>",
            "            </address>",
            "          </inet>",
            "        </family>",
            "      </unit>",
            "      <unit>",
            "        <name>406</name>",
            "        <family>",
            "          <inet>",
            "            <address>",
            "              <name>192.168.126.2/24</name>",
            "            </address>",
            "          </inet>",
            "          <inet6>",
            "                    </inet6>",
            "        </family>",
            "      </unit>",
            "      <unit>",
            "        <name>407</name>",
            "        <family>",
            "          <inet>",
            "            <address>",
            "              <name>192.168.168.2/24</name>",
            "            </address>",
            "          </inet>",
            "          <inet6>",
            "            <address>",
            "              <name>2XXX:XXX:XXXX:415a::2/64</name>",
            "            </address>",
            "          </inet6>",
            "        </family>",
            "      </unit>",
            "      <unit>",
            "        <name>408</name>",
            "        <family>",
            "          <inet>",
            "            <address>",
            "              <name>192.168.169.2/24</name>",
            "            </address>",
            "          </inet>",
            "          <inet6>",
            "            <address>",
            "              <name>2XXX:XXX:XXXX:415b::2/64</name>",
            "            </address>",
            "          </inet6>",
            "        </family>",
            "      </unit>",
            "      <unit>",
            "        <name>409</name>",
            "        <family>",
            "          <inet>",
            "            <address>",
            "              <name>192.168.170.2/24</name>",
            "            </address>",
            "          </inet>",
            "          <inet6>",
            "            <address>",
            "              <name>2XXX:XXX:XXXX:4159::2/64</name>",
            "            </address>",
            "          </inet6>",
            "        </family>",
            "      </unit>",
            "      <unit>",
            "        <name>410</name>",
            "        <family>",
            "          <inet>",
            "            <address>",
            "              <name>192.168.171.2/24</name>",
            "            </address>",
            "          </inet>",
            "        </family>",
            "      </unit>",
            "      <unit>",
            "        <name>411</name>",
            "        <family>",
            "          <inet>",
            "            <address>",
            "              <name>172.18.1.2/28</name>",
            "            </address>",
            "          </inet>",
            "        </family>",
            "      </unit>",
            "    </interface>",
            "    <interface>",
            "      <name>lo0</name>",
            "      <unit>",
            "        <name>0</name>",
            "        <family>",
            "          <inet>",
            "            <address>",
            "              <name>127.0.0.1/32</name>",
            "            </address>",
            "            <address>",
            "              <name>192.168.160.1/32</name>",
            "            </address>",
            "          </inet>",
            "        </family>",
            "      </unit>",
            "    </interface>",
            "    <interface>",
            "      <name>st0</name>",
            "      <unit>",
            "        <name>0</name>",
            "        <family>",
            "          <inet>",
            "            <address>",
            "              <name>10.50.5.1/30</name>",
            "            </address>",
            "          </inet>",
            "          <inet6>",
            "                    </inet6>",
            "        </family>",
            "      </unit>",
            "    </interface>",
            "  </interfaces>",
            "</configuration>"
        ],
        "config_parsed": {
            "configuration": {
                "interfaces": {
                    "interface": [
                        {
                            "name": "ge-0/0/0",
                            "unit": {
                                "description": "SRX-WAN",
                                "family": {
                                    "inet": {
                                        "dhcp": ""
                                    },
                                    "inet6": {
                                        "address": {
                                            "name": "2XXX:XXX:XXXX:4158::2/64"
                                        }
                                    }
                                },
                                "name": "0"
                            }
                        },
                        {
                            "name": "gr-0/0/0",
                            "unit": {
                                "family": {
                                    "inet": {
                                        "address": {
                                            "name": "172.19.2.9/30"
                                        },
                                        "mtu": "1476"
                                    }
                                },
                                "name": "0",
                                "tunnel": {
                                    "destination": "172.19.1.1",
                                    "source": "172.19.1.2"
                                }
                            }
                        },
                        {
                            "description": "SRX-LAN",
                            "name": "ge-0/0/1",
                            "unit": {
                                "family": {
                                    "ethernet-switching": {
                                        "interface-mode": "trunk",
                                        "vlan": {
                                            "members": [
                                                "vlan-150",
                                                "vlan-400",
                                                "vlan-401",
                                                "vlan-402",
                                                "vlan-403",
                                                "vlan-404",
                                                "vlan-405",
                                                "vlan-406",
                                                "vlan-407",
                                                "vlan-408",
                                                "vlan-409",
                                                "vlan-410",
                                                "vlan-175",
                                                "vlan-411",
                                                "vlan-200"
                                            ]
                                        }
                                    }
                                },
                                "name": "0"
                            }
                        },
                        {
                            "description": "R620 VMWARE-ESXI-MGMT-PORT",
                            "name": "ge-0/0/2",
                            "unit": {
                                "family": {
                                    "ethernet-switching": {
                                        "vlan": {
                                            "members": "vlan-150"
                                        }
                                    }
                                },
                                "name": "0"
                            }
                        },
                        {
                            "description": "R620-VMWARE-ESXI-VM-PORT",
                            "name": "ge-0/0/3",
                            "unit": {
                                "family": {
                                    "ethernet-switching": {
                                        "interface-mode": "trunk",
                                        "vlan": {
                                            "members": [
                                                "vlan-150",
                                                "vlan-400",
                                                "vlan-401",
                                                "vlan-402",
                                                "vlan-403",
                                                "vlan-404",
                                                "vlan-405",
                                                "vlan-406",
                                                "vlan-407",
                                                "vlan-408",
                                                "vlan-409",
                                                "vlan-410",
                                                "vlan-175",
                                                "vlan-411",
                                                "vlan-200"
                                            ]
                                        }
                                    }
                                },
                                "name": "0"
                            }
                        },
                        {
                            "description": "R620-VMWARE-ESXI-VM-PORT",
                            "name": "ge-0/0/4",
                            "unit": {
                                "description": "VMWARE-ESXI-VM-PORT",
                                "family": {
                                    "ethernet-switching": {
                                        "interface-mode": "trunk",
                                        "vlan": {
                                            "members": [
                                                "vlan-150",
                                                "vlan-400",
                                                "vlan-401",
                                                "vlan-402",
                                                "vlan-403",
                                                "vlan-404",
                                                "vlan-405",
                                                "vlan-406",
                                                "vlan-407",
                                                "vlan-408",
                                                "vlan-409",
                                                "vlan-410",
                                                "vlan-175",
                                                "vlan-411",
                                                "vlan-200"
                                            ]
                                        }
                                    }
                                },
                                "name": "0"
                            }
                        },
                        {
                            "description": "VMWARE-ESXI-MGMT-PORT",
                            "name": "ge-0/0/5",
                            "unit": {
                                "family": {
                                    "ethernet-switching": {
                                        "vlan": {
                                            "members": "vlan-150"
                                        }
                                    }
                                },
                                "name": "0"
                            }
                        },
                        {
                            "name": "ge-0/0/6",
                            "unit": {
                                "family": {
                                    "ethernet-switching": {
                                        "vlan": {
                                            "members": "vlan-150"
                                        }
                                    }
                                },
                                "name": "0"
                            }
                        },
                        {
                            "name": "ge-0/0/7",
                            "unit": {
                                "family": {
                                    "inet": {
                                        "dhcp": {
                                            "vendor-id": "Juniper-srx320"
                                        }
                                    }
                                },
                                "name": "0"
                            }
                        },
                        {
                            "dialer-options": {
                                "pool": {
                                    "name": "1",
                                    "priority": "100"
                                }
                            },
                            "name": "cl-1/0/0"
                        },
                        {
                            "name": "dl0",
                            "unit": {
                                "dialer-options": {
                                    "always-on": "",
                                    "dial-string": "1234",
                                    "pool": "1"
                                },
                                "family": {
                                    "inet": {
                                        "negotiate-address": ""
                                    },
                                    "inet6": {
                                        "negotiate-address": ""
                                    }
                                },
                                "name": "0"
                            }
                        },
                        {
                            "name": "irb",
                            "unit": [
                                {
                                    "family": {
                                        "inet": ""
                                    },
                                    "name": "0"
                                },
                                {
                                    "family": {
                                        "inet": {
                                            "address": {
                                                "name": "10.10.1.2/24"
                                            }
                                        },
                                        "inet6": {
                                            "address": {
                                                "name": "2XXX:XXX:XXXX:4157::2/64"
                                            }
                                        }
                                    },
                                    "name": "150"
                                },
                                {
                                    "family": {
                                        "inet": {
                                            "address": {
                                                "name": "10.10.2.2/24"
                                            }
                                        },
                                        "inet6": {
                                            "address": {
                                                "name": "2XXX:XXX:XXXX:415c::2/64"
                                            }
                                        }
                                    },
                                    "name": "175"
                                },
                                {
                                    "family": {
                                        "inet": {
                                            "address": {
                                                "name": "192.168.99.2/24"
                                            }
                                        }
                                    },
                                    "name": "200"
                                },
                                {
                                    "family": {
                                        "inet": {
                                            "address": {
                                                "name": "192.168.120.2/24"
                                            }
                                        }
                                    },
                                    "name": "400"
                                },
                                {
                                    "family": {
                                        "inet": {
                                            "address": {
                                                "name": "192.168.121.2/24"
                                            }
                                        }
                                    },
                                    "name": "401"
                                },
                                {
                                    "family": {
                                        "inet": {
                                            "address": {
                                                "name": "192.168.122.2/24"
                                            }
                                        }
                                    },
                                    "name": "402"
                                },
                                {
                                    "family": {
                                        "inet": {
                                            "address": {
                                                "name": "192.168.123.2/24"
                                            }
                                        }
                                    },
                                    "name": "403"
                                },
                                {
                                    "family": {
                                        "inet": {
                                            "address": {
                                                "name": "192.168.124.2/24"
                                            }
                                        }
                                    },
                                    "name": "404"
                                },
                                {
                                    "family": {
                                        "inet": {
                                            "address": {
                                                "name": "192.168.125.2/24"
                                            }
                                        }
                                    },
                                    "name": "405"
                                },
                                {
                                    "family": {
                                        "inet": {
                                            "address": {
                                                "name": "192.168.126.2/24"
                                            }
                                        },
                                        "inet6": ""
                                    },
                                    "name": "406"
                                },
                                {
                                    "family": {
                                        "inet": {
                                            "address": {
                                                "name": "192.168.168.2/24"
                                            }
                                        },
                                        "inet6": {
                                            "address": {
                                                "name": "2XXX:XXX:XXXX:415a::2/64"
                                            }
                                        }
                                    },
                                    "name": "407"
                                },
                                {
                                    "family": {
                                        "inet": {
                                            "address": {
                                                "name": "192.168.169.2/24"
                                            }
                                        },
                                        "inet6": {
                                            "address": {
                                                "name": "2XXX:XXX:XXXX:415b::2/64"
                                            }
                                        }
                                    },
                                    "name": "408"
                                },
                                {
                                    "family": {
                                        "inet": {
                                            "address": {
                                                "name": "192.168.170.2/24"
                                            }
                                        },
                                        "inet6": {
                                            "address": {
                                                "name": "2XXX:XXX:XXXX:4159::2/64"
                                            }
                                        }
                                    },
                                    "name": "409"
                                },
                                {
                                    "family": {
                                        "inet": {
                                            "address": {
                                                "name": "192.168.171.2/24"
                                            }
                                        }
                                    },
                                    "name": "410"
                                },
                                {
                                    "family": {
                                        "inet": {
                                            "address": {
                                                "name": "172.18.1.2/28"
                                            }
                                        }
                                    },
                                    "name": "411"
                                }
                            ]
                        },
                        {
                            "name": "lo0",
                            "unit": {
                                "family": {
                                    "inet": {
                                        "address": [
                                            {
                                                "name": "127.0.0.1/32"
                                            },
                                            {
                                                "name": "192.168.160.1/32"
                                            }
                                        ]
                                    }
                                },
                                "name": "0"
                            }
                        },
                        {
                            "name": "st0",
                            "unit": {
                                "family": {
                                    "inet": {
                                        "address": {
                                            "name": "10.50.5.1/30"
                                        }
                                    },
                                    "inet6": ""
                                },
                                "name": "0"
                            }
                        }
                    ]
                }
            }
        },
        "failed": false,
        "msg": "Configuration has been: opened, retrieved, closed."
    }
}

PLAY RECAP ***********************************************************************************************************************************************************************
juniper1.ignyte.lab        : ok=2    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

####Playbook Example 2
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

####Playbook Example 3
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

####Playbook Example 4
This specific playbook will push configuraton to an interface, or really any configuration you want as long as you edit the file "junos_apply_set_commands.set" with the commands that you want to set.

#####Example contents of junos_apply_set_commands.set File

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

####Playbook Example 5
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

