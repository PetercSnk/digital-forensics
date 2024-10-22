# Volatility

## Basics

We can use a memory image with volatility by setting the
-f option.

`volatility.exe -f <image file> <arguments>`

## Image Information

To gather more information about the memory dump we can
specify **imageinfo** as an argument. This should allow
us to identify the machines OS and when the image was
taken.

`volatility.exe -f <image file> imageinfo`

To use various other arguments the OS should be provided
as an additional option.

`volatility.exe -f <image file> --profile=<OS> <arguments>`

## Processes 

To view processes that were running on the system at
the time of imaging **pslist** can be used. This will
contain processes that are reporting to the OS as
normal. Hidden and unlinked processes will not be shown.

This command walks the doubly-linked list pointed to by
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
command **psxview** can be used. Here we can view and compare
what is reported by various other sources of process listings.

A False in any column indicates that the respective process is
missing. Processes that appear in every column except pslist
can be considered suspicious.

`volatility.exe -f <image file> --profile=<OS> psxview`

## Network


