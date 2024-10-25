# Windows Live System Analysis

## Important

When using command line utilities the output provided to
the console may be very large. To improve readability we
can try piping our output into more or findstr.

The command more will only display one screen of output
at a time.

`<command> | more`

The command findstr will only display lines where a match
is found.

`<command> | findstr <string>`

When a program with a .exe or .msc extension is mentioned
we can run it by pressing win+r and entering the name.ext.
In addition to this we can run the program by entering 
just the name into a terminal.

## Processes

To check which processes are running on a system we can
use the following methods:

- The Task Manager is a system monitor program built into
Windows systems that provides information about running
processes and applications. 
    - `taskmgr.exe`
- The command **tasklist** can be used to display a list of 
running processes on a local or remote system. 
[[documentation](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/tasklist)]
    - `tasklist /v`
- The WMIC utility provides a command line interface for
Windows Management Instrumentation. It allows certain
components of Windows to be managed where information
regarding the OS and hardware can be get and set.
[[documentation](https://learn.microsoft.com/en-us/windows/win32/wmisdk/wmic)]
[[about](https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-2000-server/bb742610(v=technet.10)?redirectedfrom=MSDN)]
    - `wmic process list full`

## Services

To check which services are running on a system we can
use the following methods:

- Windows has a built in services GUI that provides
information on active and dead services.
    - `services.msc`
- The command **sc** can be used to display information
about a specified service, driver, type of service, or
type of driver.
[[documentation](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/sc-query)]
    - `sc query`
- The command **tasklist** can also used to list all service
information for each process.
    - `tasklist /svc`

## Registry Keys

Processes and services may be started from the Run,
RunOnce, and RunOnceEx registry keys. Using the Registry
Editor we can find these registry keys in the following
locations:

- HKLM\Software\Microsoft\Windows\CurrentVersion\Run
- HKLM\Software\Microsoft\Windows\CurrentVersion\Runonce
- HKLM\Software\Microsoft\Windows\CurrentVersion\RunonceEx

HKLM will be the local machine, HKCU can also be used to
view start-up processes for the current user.

The command **reg query** will also perform the same task as
above.

`reg query <registry key location>`

## Network Usage

To analyse system network usage the netstat tool can be
used. This command line utility will display statistics
for all network connections. An example and the various
options that can be used are provided below:

`netstat -<options>`

|Option|Description|
|------|-----------|
|n|Numerical IP addresses instead of names|
|n seconds|Refreshes after chosen number of seconds|
|a|Active and inactive connections|
|b|Executables associated with connections|
|e|Network interface statistics|
|f|Fully qualified domain names|
|o|Process IDs for each connection|
|p protocol|Connections for chosen protocol|
|q|Listening and non-listening ports|
|s|Statistics by protocol|
|r|Current network routing table|

## Accounts

All local users and groups can be viewed from the manager
console. This can be done by opening run with win+r and 
entering lusrmgr.msc. Here all users and groups are 
displayed, where by looking in the administrators group
we can see who has these privileges.

Viewing the users within the administrator group can
also be done on the command line with the following:

`net localgroup administrators`

## Log Entries

Windows has a built in GUI called Event Viewer that can
be used to view events and logs for the current system.
We can also view the current settings of policies with
secpol.msc. If we go to Local Policies -> Audit Policy
-> Audit Logon Events, we can see that logon events are
not logged by default, this can be changed to log both
successful and failed attempts within its properties.
