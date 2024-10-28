# Windows Registry Analysis

## What is the Registry?

The registry is a database of stored configuration information about
the users, hardware, and software on a Windows system.

Within the registry there are root folders also known as hives. There
are 5 registry hives which include:

- HKEY_USERS: contains all loaded user profiles
- HKEYCURRENT_USER: profile of the currently logged-on user
- HKEYCLASSES_ROOT: configuration information on the application used to open files
- HKEYCURRENT_CONFIG: hardware profile of the system startup
- HKEYLOCAL_MACHINE: configuration information including hardware and software settings

The registry has the 5 main hives listed above where each hive can contain various subkeys.
These subkeys contain descriptions and values where the values are often 0 or 1 indicating on
or off, but can also contain more complex information in some cases.
