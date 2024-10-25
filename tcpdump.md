# Tcpdump

## General

This document is not extensive and many commands and options have been
left out, refer to the [documentation](https://www.tcpdump.org/manpages/tcpdump.1.html)
for additional information.

Before network traffic can be captured we need to know what network
interface our system is using. This can be done with the linux command
**ifconfig**.

If we do not specify a network interface tcpdump will pick one by default which
may not be the one we want. We can view all the network interfaces tcpdump can
use with the **-D** option.

`tcpdump -D`

We can now tell tcpdump which network interface we want to capture traffic on with
the **-i** option. The **any** option can also be used to capture traffic on all network
interfaces simultaneously.

`tcpdump -i <interface>`

`tcpdump -i any`

## Display Commands

|Option|Example|Description|
|------|-------|-----------|
|-A|tcpdump -i *interface* -A|Displays each packet in ASCII|
|-D|tcpdump -D|Lists available network interfaces|
|-e|tcpdump -i *interface* -e|Displays the link-level header|
|-F *config*|tcpdump -i *interface* -F *config*|Reads a .conf file as input for filter expressions|
|-n|tcpdump -i *interface* -n|Does not resolve addresses to host names|
|-S|tcpdump -i *interface* -S|Uses absolute sequence numbers instead of relative|
|-t|tcpdump -i *interface* -t|Omits timestamps|
|-l|tcpdump -i *interface* -l|Line-readable output|
|-v|tcpdump -i *interface* -v|Verbose output|


## Capture Commands

|Option|Example|Description|
|------|-------|-----------|
|-i any|tcpdump -i any|Captures from all interfaces|
|-i *interface*|tcpdump -i *interface*|Captures from specified interface|
|-c *count*|tcpdump -i *interface* -c *count*|Captures *count* packets|
|-r *pcap*|tcpdump -i *interface* -r *pcap*|Reads the given pcap capture file|
|*protocol*|tcpdump -i *interface* *protocol*|Captures only the specified protocol|
|-s|tcpdump -i *interface* -s *bytes*|Captures the specified number of bytes|



### Protocols

The protocols that can be used in the above capture commands include: tcp, udp
icmp, ip (IPv4), ip6, arp, rarp, and slip.
