# COMpare - Highlighting Potential COM Hijacking Targets
[#] Scans HKLM and HKCU and compares to find entries that are in HKLM and not in HKCU. 

[#] Checks if associated EXE or DLL is present on the system

[#] Exports to HTML spreadsheet.

## CLI
<img width="1350" height="253" alt="Screen1" src="https://github.com/user-attachments/assets/5a035974-e838-4887-9424-f7a488589742" />

## Report
<img width="1882" height="858" alt="Report" src="https://github.com/user-attachments/assets/b8d1c2cd-6992-418d-bb02-37245ccf6fbd" />




# Background
There are several ways to achieve COM hijacking. One method involves partially missing COM entries. The HKEY_CLASSES_ROOT registry hive is a combination of two locations: HKEY_LOCAL_MACHINE\Software\Classes and HKEY_CURRENT_USER\Software\Classes. For processes running under a standard user context, entries in HKCU take precedence over those in HKLM. If a COM entry exists only in HKLM and not in HKCU, it can be hijacked by creating a corresponding entry in the HKCU hive for the same CLSID.

Another method involves broken COM registrations where the specified DLL or EXE is missing from disk, and the path is located in a user-writable directory. This often happens when third-party software is uninstalled but fails to clean up the COM entries it registered.
