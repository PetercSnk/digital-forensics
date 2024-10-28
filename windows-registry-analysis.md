# Windows Registry Analysis

## What is the Registry?

The registry is a database of stored configuration information about
the users, hardware, and software on a Windows system.

Within the registry there are root folders also known as hives. There
are 5 registry hives which include:

- HKEY_USERS: contains settings for all user profiles on system.
- HKEY_CURRENT_USER: settings specific to the currently logged-in user.
- HKEY_CLASSES_ROOT: manages file associations and COM objects, i.e. which application opens .txt files.
- HKEY_CURRENT_CONFIG: Tracks the current hardware profile.
- HKEY_LOCAL_MACHINE: Contains configuration data for the local system.

The registry has the 5 main hives listed above where each hive can contain various subkeys.
These subkeys contain descriptions and values where the values are often 0 or 1 indicating on
or off, but can also contain more complex information in some cases.
