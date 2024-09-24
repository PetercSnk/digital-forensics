Clean (non-compromised) utilities need to be used in case the target machine has been 
tampered with. The Sleuth Kit is a library of such utilities and will be used for this
example. In most cases this is stored on a USB which will need mounting. The following
command will mount the USB to /mnt in read only and permit execution of executables:

`mount -ro,exec /dev/sdb1 /mnt`

Change the current directory to /mnt with:

`cd /mnt`

At this point we have a minimal footprint on the target system, in order to maintain
this only the utilities on the USB should be used from now on. To execute files in the 
current directory ./ can be used before the file name. Many default linux commands are
included in Sleuth Kits utilities such as ls which will list the contents of the USB.

Find the ip address of the targets machine with:

`./ifconfig`

A static ip address can also be set with ifconfig. Make a note of what network device
was shown when running the command on its own as this will be requried, it will likely 
be eno, ens, or eth. The following is an example where the ip address is set to
192.168.1.2:

`./ifconfig ens33 192.168.1.2 netmask 255.255.255.0`

The connection to the target can be tested by pinging your host machine, the following
pings the ip address 192.168.1.10:

`./ping 192.168.1.10`

As this is a remote acquisition we need a method where we can send data from the 
targets machine to our host machine. A tool called netcat is exactly what is needed here.
Before netcat is used we must remove any rules in iptables on our host machine, iptables 
is a utility that controls incoming and outgoing traffic. Removing all rules ensures all
network packets can pass through, this can be done with the following command:

`iptables -F`

On our host machine we setup netcat to listen for any incoming connections. The following
command makes netcat listen on port 31337 and redirect all output to a file called memdump:

`nc -l -p 31337 > memdump`

Now on the target machine we can execute Sleuth Kits memdump and pipe it to netcat. This
time netcat needs to send data to the ip address 192.168.1.10 on port 31337 where our 
host is listening. This can be done with the command below:

`./memdump | ./nc 192.168.1.10 31337`

Note that netcat will stay connected so once the file memdump stops growing in size stop
netcat with ctrl-c. We now have a memory image from the target machine.

On the target machine we can now use lsof to examine open files and the processes that
use them. This command has a wide range of options and some examples are shown below.
Note that the output from lsof is piped to less as it displays it in a more readable
format.

The following will display files access by the network:

`./lsof -i | ./less`

The following stops network numbers being converted to host names for network files:

`./lsof -n | ./less`

Inspecting log files can also be very useful, the majority of log files in linux are
found within the /var/log directory. For example authentication logs can be found
with the below command and location:

`./less /var/log/auth.log`

We can create a timeline with mac-robber and mactime in the same way we created a 
memory image with netcat. The mac-robber utility collects metadata from allocated 
files in a mounted filesystem, and mactime puts this data into a timeline.

On the host machine with the ip address 192.168.1.10 run:

`nc -l -p 31337 > bodyfile.mac`

On the target machine run:

`./mac-robber / | ./nc 192.168.1.10 31337`

This will result in a bodyfile which mactime can be used on:

`mactime -b bodyfile.mac > comp-timeline.txt`

Read this timeline file with less:

`less comp-timeline.txt`
