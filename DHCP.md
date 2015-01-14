# Dynamic Host Configuration Protocol
## By Tang Bei

---

# DHCP Basic Concept
- A standardized network protocol used on Internet Protocol networks for dynamically distributing network configuration parameters, such as IP addresses for interfaces and services.
- Client-Server model
- Client sends a broadcast query requesting necessary information
- Server responds a request with specific information
- Using UDP, port number 67 is used by server, port number 68 is used by client
- Dynamic allocation, automatic allocation, static allocation

---

# Four Phases of DHCP operations
- Server discovery
- IP lease offer
- IP request
- IP lease acknowledgement
- Abbreviated as DORA: discovery, offer, request, and acknowledgement

---

# DHCP Relay
- Allow DHCP clients on subnets not directly served by DHCP servers
- DHCP client broadcasts on the local link, the relay agent receives the broadcast and transmits it to one or more DHCP servers using unicast
- The relay agent stores its own IP address in the GIADDR field of the DHCP packet
- The DHCP server uses the GIADDR to determine the subnet on which the relay agent received the broadcast, and allocates an IP address on that subnet.

---

# dhcpd
- DHCP server daemon
- Configuration file: /etc/dhcpd.conf, sample file in /usr/share/doc/dhcp-<version>/dhcpd.conf.sample
- Client lease database: /var/lib/dhcpd/dhcp.leases
- Other options: /etc/sysconfig/dhcpd
- /sbin/service dhcpd start

---

# dhcrelay
- DHCP Relay Agent
- /etc/sysconfig/dhcrelay
- service dhcrelay start

---

# References
- http://en.wikipedia.org/wiki/Dynamic_Host_Configuration_Protocol
- http://www.centos.org/docs/5/html/Deployment_Guide-en-US/s1-dhcp-configuring-server.html
