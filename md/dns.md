---
runme:
  id: 01HN7WDXEE4XHQ50Y5MPH6CY0J
  version: v2.2
---

# DNS

## Origin

- 1970s - the ARPAnet was a small, friendly community of a few hundred hosts. A
   single file, HOSTS.TXT, contained a name-to-address mapping for every host
   connected to the ARPAnet. The familiar Unix host table, /etc/hosts, was
   compiled from HOSTS.TXT.

   HOSTS.TXT was maintained by SRI’s Network Information Center (dubbed “the
   NIC”) and distributed from a single host, SRI-NIC.* ARPAnet administrators
   typically emailed their changes to the NIC, and periodically FTP’ed to SRI-NIC
   and grabbed the current HOSTS.TXT file. Their changes were compiled into a new
   HOSTS.TXT file once or twice a week.

- Population Explosion

   - Traffic and load
   - Name collisions: No two hosts in HOSTS.TXT could have the same name.
      However, while the NIC could assign addresses in a way that guaranteed
      uniqueness, it had no authority over hostnames. There was nothing to prevent
      someone from adding a host with a conflicting name and breaking the whole
      scheme. Adding a host with the same name as a major mail hub, for example,
      could disrupt mail service to much of the ARPAnet.
   - Consistency

- The ARPAnet’s governing bodies chartered an investigation to develop a
   successor for HOSTS.TXT. Their goal was to create a system that solved the
   problems inherent in a unified host-table system. The new system should allow
   local administration of data yet make that data globally available. The
   decentralization of administration would eliminate the single-host bottleneck
   and relieve the traffic problem. And local manage- ment would make the task of
   keeping data up-to-date much easier. The new system should use a hierarchical
   namespace to name hosts. This would ensure the unique- ness of names.

   Paul Mockapetris, then of USC’s Information Sciences Institute, was
   responsible for designing the architecture of the new system. In 1984, he
   released RFCs 882 and 883, which described the Domain Name System. These RFCs
   were superseded by RFCs 1034 and 1035, the current specifications of the
   Domain Name System.* RFCs 1034 and 1035 have since been augmented by many
   other RFCs, which describe potential DNS security problems, implementation
   problems, administrative gotchas, mechanisms for dynamically updating
   nameservers and for securing zone data, and more.

## DNS in a Nutshell

The Domain Name System is a distributed database. This structure allows local con-
trol of the segments of the overall database, yet data in each segment is available
across the entire network through a client/server scheme. Robustness and adequate
performance are achieved through replication and caching.

Programs called nameservers constitute the server half of DNS’s client/server mecha-
nism. Nameservers contain information about some segments of the database and
make that information available to clients, called resolvers. Resolvers are often just
library routines that create queries and send them across a network to a nameserver.

DNS Database

- ""
   - com
   - edu
      - berkeley
         - cs (this become cs.berkeley.edu, i.e., bottom-up)

   - gov
   - mil

UNIX Database

- /
   - etc
   - bin
   - usr
      - nfs
         - winken (this become /usr/nfs/winken, i.e., top-down)

   - system

Domain names ending with .edu will be managed by EDUCAUSE. But, Domain names
ending with berkeley.edu will be managed by U.C. Berkeley.

Hosts may also have one or more domain name aliases, which are simply pointers
from one domain name (the alias) to another (the official, or canonical, domain
name).

## Implementation

The first implementation of the Domain Name System was called JEEVES, written by
Paul Mockapetris himself. A later implementation was BIND, an acronym for Ber-
keley Internet Name Domain, written by Kevin Dunlap for Berkeley’s 4.3 BSD Unix.
BIND is now maintained by the Internet Systems Consortium.

## Must I Use DNS?

- If you’re connected to the Internet...
  - ...DNS is a must. Think of DNS as the lingua franca of the Internet: nearly
    all of the Internet’s network services use DNS. That includes the Web,
    electronic mail, remote terminal access, and file transfer.

- If you have your own TCP/IP-based internet...
  - ...you probably want DNS. By an internet, we don’t mean just a single
    Ethernet of workstations using TCP/IP (see the next section if you thought
    that was what we meant); we mean a fairly complex “network of networks.”
    Maybe you have several dozen Ethernet segments connected via routers, for
    example.

- If you have your own local area network or site network...
  - ...and that network isn’t connected to a larger network, you can probably
    get away without using DNS. You might consider using Microsoft’s Windows
    Inter- net Name Service (WINS), host tables, or Sun’s Network Information
    Service (NIS) product.