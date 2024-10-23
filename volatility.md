# Volatility

## General

Refer to the links below for extra information on
volatility commands.

- [Windows Core](https://github.com/volatilityfoundation/volatility/wiki/Command-Reference)

- [Windows Malware](https://github.com/volatilityfoundation/volatility/wiki/Command-Reference-Mal)

Note that we are working with volatility 2 and the commands
will differ from volatility 3.

We can use a memory image with volatility by setting the
-f option.

`volatility.exe -f <image file> <arguments>`

## Image Information

To gather more information about the memory dump we can
use the plugin **imageinfo**. This should allow us to identify
the OS of the machine and when the image was taken.

`volatility.exe -f <image file> imageinfo`

To use various other plugins the OS should be provided
as an additional option.

`volatility.exe -f <image file> --profile=<OS> <arguments>`

## Processes 

To view processes that were running on the system at
the time of imaging **pslist** can be used. This will
contain processes that are reporting to the OS as
normal. Hidden and unlinked processes will not be shown.

This plugin walks the doubly-linked list pointed to by
PsActiveProcessHead. Note that processes that have 0
threads and handles, and a non-empty exit time may not
actually still be active.

`volatility.exe -f <image file> --profile=<OS> pslist`

Additionally **pstree** can be used to show the process
trees.

`volatility.exe -f <image file> --profile=<OS> pstree`

In order to find previously terminated, hidden or unlinked
processes **psscan** can be used. This will enumerate
processes using pool tag scanning, unfortunately rootkits
can still hide processes by overwriting the pool tag
values.

`volatility.exe -f <image file> --profile=<OS> psscan`

To find processes that are trying to hide themselves the 
plugin **psxview** can be used. Here we can view and compare
what is reported by various other sources of process listings.

A False in any column indicates that the respective process is
missing. Processes that appear in every column except pslist
are usually considered suspicious.

`volatility.exe -f <image file> --profile=<OS> psxview`

## Networking

With the plugin **connscan** we can find artifacts from
previous TCP connections that were active in addition to
ones that have been terminated. Note that in some cases the
output may have partially overwritten fields thus causing
false postives. 

`volatility.exe -f <image file> --profile=<OS> connscan`

In order to detect listening sockets for any protocol the
plugin **sockets** can be used. This walks a singly-linked
list of socket structures which is pointed to by a non-exported
symbol in the tcpip.sys module.

`volatility.exe -f <image file> --profile=<OS> sockets`

A non-exported symbol is a kernel symbol that is not visible,
neither available to any loadable module.

The system file tcpip.sys is responsible for handling network
related operations. It is used by the TCP/IP protocol which
is the standard communication protocol used for internet
connectivity. Whenever a connection is made to the internet,
your computer relies on tcpip.sys to establish and maintain
the connection. It handles tasks such as IP address
assignment, data transmission, are error handling.

To scan for network artifacts on 32/64 bit Windows Vista,
Windows 2008 Server, and Windows 7, the plugin **netscan**
can be used. This will scan for connections and sockets.

`volatility.exe -f <image file> --profile=<OS> netscan`

## Commands

We can use **cmdline** to display process command line
arguments. Commands entered into cmd.exe are processed
by conhost.exe (csrss.exe before Windows 7), so even if
cmd.exe is killed before a memory dump takes place there
is still a chance to retrieve the commands entered from
conhost.exe's memory.

`volatility.exe -f <image fie> --profile=<OS> cmdline`

We can also specify a process ID to see what command was
run to execute that process.

`volatility.exe -f <image file> --profile=<OS> -p <PID> cmdline`

The plugins **cmdscan** and **consoles** work a little 
different as they extract command history by scanning for
_COMMAND_HISTORY and _CONSOLE_INFORMATION respectively.

`volatility.exe -f <image file> --profile=<OS> cmdscan`

`volatility.exe -f <image file> --profile=<OS> consoles`

## DLLs

To display a processes loaded DLLs **dlllist** is used. DLLs
are automatically added to this list when a process calls
LoadLibrary and they are not removed until FreeLibrary is
called and the reference count reaches 0.

`volatility.exe -f <image file> --profile=<OS> -p <PID> dlllist`

## Dumping Executables

In order to figure out what a processes executable is we
can dump the executable with **procdump**. Note that some
malware will intentionally forge size fields in the PE 
header so that memory dumping tools fail.

`volatility.exe -f <image file> --profile=<OS> -p <PID> procdump --dump-dir <directory>`

To extract all memory resident pages in a process into a 
single file we can use **memdump**.

`volatility.exe -f <image file> --profile=<OS> -p <PID> memdump --dump-dir <directory>`
