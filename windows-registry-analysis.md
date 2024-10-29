# Windows Registry Analysis

## What is the Registry?

The registry is a database of stored configuration information about
the users, hardware, and software on a Windows system.

Within the registry there are 5 main root folders also known as hives which
contain:

- HKEY_USERS: settings for all user profiles on system.
- HKEY_CURRENT_USER: settings specific to the currently logged-in user.
- HKEY_CLASSES_ROOT: manages file associations and COM objects, e.g. which application opens .txt files.
- HKEY_CURRENT_CONFIG: Tracks the current hardware profile.
- HKEY_LOCAL_MACHINE: configuration data for the local system.

Non-volatile hives include: HKLM, and HKU.

Volatile hives include: HKCR, HKCU, and HKCC.

Each hive listed above will contain various keys and subkeys which contain descriptions and values.
These values are often 0 or 1 indicating on or off, but can also contain more complex information
in some cases.

## Offline Analysis

Registry hives have supporting files that contain the respective registry data. These hives and their
supporting files are listed below:

- HKEY_CURRENT_CONFIG: SYSTEM
- HKEY_CURRENT_USER: NTUSER.DAT
- HKEY_USERS\\.DEFAULT: DEFAULT
- HKEY_LOCAL_MACHINE\SAM: SAM
- HKEY_LOCAL_MACHINE\SECURITY: SECURITY
- HKEY_LOCAL_MACHINE\SOFTWARE: SOFTWARE 
- HKEY_LOCAL_MACHINE\SYSTEM: SYSTEM

If we only have access to a disk image we need to know where these supporting files are located.
The supporting files: DEFAULT, SAM, SECURITY, SOFTWARE, and SYSTEM can be found within:

`C:\Windows\System32\config`

These files contain the following registry data:

- DEFAULT: default user settings.
- SAM (Security Account Manager): local user account and group membership information like passwords.
- SECURITY: information on the current user security policy.
- SOFTWARE: installed applications and their configuration settings.
- SYSTEM: configuration settings of hardware drivers and services.

NTUSER.DAT is instead found within:

`C:\Users\<user>\NTUSER.DAT`

This supporting file contains any user configurations where changes made are saved here during the
logout process.

## Registry Quick Find Chart

![registry quick find chart page 01](images/windows-registry-analysis/registry-chart-01.png)
![registry quick find chart page 02](images/windows-registry-analysis/registry-chart-02.png)
![registry quick find chart page 03](images/windows-registry-analysis/registry-chart-03.png)
![registry quick find chart page 04](images/windows-registry-analysis/registry-chart-04.png)
![registry quick find chart page 05](images/windows-registry-analysis/registry-chart-05.png)
![registry quick find chart page 06](images/windows-registry-analysis/registry-chart-06.png)
![registry quick find chart page 07](images/windows-registry-analysis/registry-chart-07.png)
![registry quick find chart page 08](images/windows-registry-analysis/registry-chart-08.png)
![registry quick find chart page 09](images/windows-registry-analysis/registry-chart-09.png)
![registry quick find chart page 10](images/windows-registry-analysis/registry-chart-10.png)
![registry quick find chart page 11](images/windows-registry-analysis/registry-chart-11.png)
![registry quick find chart page 12](images/windows-registry-analysis/registry-chart-12.png)
![registry quick find chart page 13](images/windows-registry-analysis/registry-chart-13.png)
![registry quick find chart page 14](images/windows-registry-analysis/registry-chart-14.png)
![registry quick find chart page 15](images/windows-registry-analysis/registry-chart-15.png)
![registry quick find chart page 16](images/windows-registry-analysis/registry-chart-16.png)
![registry quick find chart page 17](images/windows-registry-analysis/registry-chart-17.png)
