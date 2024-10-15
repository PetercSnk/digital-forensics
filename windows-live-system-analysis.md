# Windows Live System Analysis

## Processes

To check which processes are running on a system we can
use the following methods:

- The task manager is a system monitor program built into
Windows systems that provides information about running
processes and applications. 
    - `taskmgr.exe`
- The command tasklist can be used to display a list of 
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
- The command sc/sc.exe can be used to display information
about a specified service, driver, type of service, or
type of driver.
[[documentation](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/sc-query)]
    - `sc query`
- The command tasklist can also used to list all service
information for each process.
    - `tasklist /svc`

## Registry Keys
