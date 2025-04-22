# Fortigate Firewall VM Setup & Configuration Lab

1. Under System Tab:
    - create custom admin profile(group)
    - Allow all access permissions except Admin users & CLI

2. Under Interfaces Tab:
    - Physical Interface:
        - [PORT1]
            - set [port1] as WAN
            - Address:
                - Addressing mode [DHCP]
        - [PORT2]
            - set [port2] as LAN
            - Address: 
                - Manual [IP/Netmask] - [10.40.254.1/24]
                - Create address object matching subnet [disabled]
            - Administrative Access
                - IPV4 [ALlowed]
                    - [PING] [HTTPS] [SSH]
                -Receive LLDP
                    - User VDOM Setting
                -Transmit LLDP
                    - Enable
            - DHCP Server [enabled]
                - DHCP Status [Enabled]
                    - Address range - [10.40.254.2-10.40.254.254]
                    - Netmask 255.255.255.0
                    - Default gateway [Specify] - [10.40.254.1]
                    - DNS server
                        - Same as System DNS

3. Under Policy & Objects Tab:
    - Addresses
        + Create new
            - Name:
                - LAN_port2
            - Interface:
                - LAN(port2)
            - Type:
                - Subnet
            - IP/Netmask:
                - [10.40.254.0/24]
    - Firewall Policy
        + Create new
            - Name: 
                - LAN_to_WAN
                - Incoming interface [LAN(port2)]
                - Outgoing interface [WAN(port1)]
            - Source & Destination
                - Source [LAN_port2]
                - Destination [all] -- set as all for now since I don't have any list of IP or DNS to route to
                - Service [ALL] -- set service to all as I don't have speficic type of service to config yet