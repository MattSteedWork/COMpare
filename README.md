# COMpare - Highlighting Potential COM Hijacking Targets
# COMpare

**COMpare** is a Windows tool that scans the system’s registered COM objects and highlights potential **COM hijacking opportunities**.  
It compares `HKLM\Software\Classes\CLSID` entries against `HKCU` overrides, and generates a clean **HTML report** (`report.html`) with pagination (100 results per page).  

---

## 🔎 Features
- Enumerates all COM CLSIDs under HKLM  
- Detects `LocalServer32` (EXE) and `InprocServer32` (DLL) registrations  
- Highlights missing executables or DLLs (potential hijack points)  
- Identifies CLSIDs with **AppID** or **TreatAs** keys  
- Outputs results into an interactive **HTML report**  

---

## ⚙️ Switches
You can refine results with the following options:

| Switch            | Description                                                   |
|-------------------|---------------------------------------------------------------|
| `--exe`           | Show only CLSIDs with **LocalServer32** (EXE-based COMs)      |
| `--exe --missing` | Show only EXE-based CLSIDs where the file is **missing**      |
| `--dll`           | Show only CLSIDs with **InprocServer32** (DLL-based COMs)     |
| `--dll --missing` | Show only DLL-based CLSIDs where the file is **missing**      |
| `--appid`         | Show only CLSIDs that have an **AppID** key                   |
| `--treatas`       | Show only CLSIDs that have a **TreatAs** key                  |

Switches can be combined, for example:

```powershell
COMpare.exe --dll --missing --appid
```
This shows only DLL-based COM objects where the DLL file is missing and the CLSID has an AppID.

## 📄 Report

The tool generates an HTML report (`report.html`) with:

- Dark theme  
- Highlighted risky entries  
- Pagination (**100 results per page**)  
- Easy filtering and readability  

## CLI
<img width="1125" height="727" alt="stack" src="https://github.com/user-attachments/assets/e43b5de9-b683-43dc-9fb5-34a65c3c4274" />

## Report
<img width="1827" height="687" alt="Report" src="https://github.com/user-attachments/assets/97a5590d-c877-4fd8-ae3c-9b8048a51dba" />

# Background
There are several ways to achieve COM hijacking. One method involves partially missing COM entries. The HKEY_CLASSES_ROOT registry hive is a combination of two locations: HKEY_LOCAL_MACHINE\Software\Classes and HKEY_CURRENT_USER\Software\Classes. For processes running under a standard user context, entries in HKCU take precedence over those in HKLM. If a COM entry exists only in HKLM and not in HKCU, it can be hijacked by creating a corresponding entry in the HKCU hive for the same CLSID.

Another method involves broken COM registrations where the specified DLL or EXE is missing from disk, and the path is located in a user-writable directory. This often happens when third-party software is uninstalled but fails to clean up the COM entries it registered.
