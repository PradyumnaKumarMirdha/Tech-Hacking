# Enumeration

Increasing attack vectors. Decreasing the path gives the right direction.

- The attacker creates an active connection to the system and performs directed queries to gain more info about the target.
- Attackers establish an active connection with the victim and discover as many attack vectors as possible.
- Enumeration techniques are conducted in an intranet environment.
- Scanning is finding an attack surface, enumeration is expanding it.
- Enumeration is the key to a successful penetration test.

**Information enumerated by Intruders:**
- Network resources
- Network shares
- Routing tables
- Audit and service settings
- SNMP and DNS details
- Machine names
- Users and Groups
- Application and banners

**Enumeration Techniques:**

- Extract user names using email IDs
- Extract information using the default passwords
- Extract user names using SNMP
- Brute force Active Directory
- Extract user groups from Windows
- Extract information using DNS Zone Transfer

### Services and Ports to Enumerate

- TCP/UDP 53: DNS Zone Transfer
- TCP/UDP 135: Microsoft RPC Endpoint Mapper
- UDP 137: NetBIOS Name Service (NBNS)
- TCP 139: NetBIOS Session Service (SMB over NetBIOS)
- TCP/UDP 445: SMB over TCP (Direct Host)
- UDP 161: Simple Network Management Protocol (SNMP)
- TCP/UDP 389: Lightweight Directory Access Protocol (LDAP)
- TCP/UDP 3268: Global Catalog Service
- TCP 25: Simple Mail Transfer Protocol (SMTP)
- TCP/UDP 162: SNMP Trap

---

## Network Resources