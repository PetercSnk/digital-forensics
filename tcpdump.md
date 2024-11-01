# Tcpdump

## General

This document is not extensive and many commands and options have been
left out, refer to the [documentation](https://www.tcpdump.org/manpages/tcpdump.1.html)
for additional information.

Before network traffic can be captured we need to know what network
interface our system is using. This can be done with the linux command *ifconfig*.

    user@system:~$ ifconfig
    eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
            inet 192.168.1.175  netmask 255.255.255.0  broadcast 192.168.1.255
            ether 04:d4:c4:52:d8:ef  (Ethernet)
            RX packets 0  bytes 0 (0.0 B)
            RX errors 0  dropped 0  overruns 0  frame 0
            TX packets 0  bytes 0 (0.0 B)
            TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

If we do not specify a network interface, tcpdump will pick one by default which
may not be the one we want. To view all network interfaces that are available to
tcpdump the *-D* option can be used.

    user@system:~$ tcpdump -D
    1.eth0 [Up, Running]
    2.eth1 [Up, Running]
    3.any (Pseudo-device that captures on all interfaces) [Up, Running]
    4.lo [Up, Running, Loopback]
    5.eth2 [Running]
    6.bluetooth-monitor (Bluetooth Linux Monitor) [Wireless]
    7.dbus-system (D-Bus system bus) [none]
    8.dbus-session (D-Bus session bus) [none]

## Capture Commands

|Option|Example|Description|
|------|-------|-----------|
|-i any|tcpdump -i any|Captures from all interfaces|
|-i *interface*|tcpdump -i *interface*|Captures from the specified interface|
|-c *count*|tcpdump -i *interface* -c *count*|Captures only *count* packets|
|-r *pcap*|tcpdump -i *interface* -r *pcap*|Reads the given pcap file|
|*protocol*|tcpdump -i *interface* *protocol*|Captures only the specified protocol|
|-s|tcpdump -i *interface* -s *bytes*|Captures the specified number of bytes|

### Protocols

The protocols that can be used in the above capture commands include: tcp, udp
icmp, ip (IPv4), ip6, arp, rarp, and slip.

## Filter Commands

|Filter|Description|
|------|-----------|
|src host *ip*|Filters by source IP address|
|dst host *ip*|Filters by destination IP address|
|host *ip*|Filter by source or destination IP address|
|ether src|Filter by source MAC address|
|ether dst|Filter by destination MAC address|
|ether host *ip*|Filter by source or destination MAC address|
|net *ip/subnet*|Filter by subnet|
|src port *port*|Filter by source port|
|dst port *port*|Filter by destination port|
|port *port*|Filter by source or destination port|
|src portrange *start-end*|Filter by a range of source ports|
|dst portrange *start-end*|Filter by a range of destination ports|
|portrange *start-end*|Filter by a range of source or destination ports|
|ether broadcast|Filter by ethernet broadcasts|
|ip broadcast|Filter by IPv4 broadcasts|
|ether multicast|Filter by ethernet multicasts|
|ip multicast|Filter by IPv4 multicasts|
|ip6 multicast|Filter by IPv6 multicasts|
|ip src host *name*|Filter by IPv4 hostname|

## Display Commands

|Option|Example|Description|
|------|-------|-----------|
|-A|tcpdump -i *interface* -A|Displays each packet in ASCII|
|-D|tcpdump -D|Displays all available network interfaces|
|-e|tcpdump -i *interface* -e|Displays the link-level header|
|-F *config*|tcpdump -i *interface* -F *config*|Reads a .conf file as input for filter expressions|
|-n|tcpdump -i *interface* -n|Does not resolve addresses to host names|
|-S|tcpdump -i *interface* -S|Displays absolute sequence numbers instead of relative|
|-t|tcpdump -i *interface* -t|Omits timestamps|
|-tt|tcpdump -i *interface* -tt|Displays timestamps (UNIX Epoch)|
|-l|tcpdump -i *interface* -l|Displays in line-readable output|
|-v|tcpdump -i *interface* -v|Displays verbose output, vv and vvv can be used for additional verbosity|
|-L|tcpdump -i *interface* -L|Displays data link types for the interface|
|-q|tcpdump -i *interface* -q|Displays less protocol information|

## Output Commands

|Option|Example|Description|
|------|-------|-----------|
|-w *pcap*|tcpdump -i *interface* -w *pcap*|Writes the output to a pcap file|
|-U|tcpdump -i *interface* -U -w *pcap*|Writes each packet to the pcap file in real time|

## Operators

|Operator|Description|
|--------|-----------|
|and, &&|Match all of the filtering options|
|or, \|\||Match any of the filtering options|
|not, !|Negate a filtering option|
|less, <, <=|Show packets shorter than the length specified|
|greater, >, >=|Show packets longer than the length specified|
|=, ==|Show packets equal to the length specified|

