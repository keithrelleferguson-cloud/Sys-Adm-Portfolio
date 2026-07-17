# Troubleshooting a Locked Windows Server 2025 ISO

## Overview

While preparing my Windows Server 2025 Active Directory homelab, I encountered an issue after accidentally moving the Windows Server 2025 Evaluation ISO into a newly created `Homelab` directory within my OneDrive folder while the file was still downloading.

The browser eventually reported that the download had been removed, but the ISO remained on disk. Any attempt to delete the file resulted in Windows reporting that the file was still in use.

**Windows Explorer**

> "The action can't be completed because the file is open in System."

**Command Prompt / PowerShell**

```text
The process cannot access the file because it is being used by another process.
```

---

## Troubleshooting Process

I followed a structured troubleshooting process to determine what was locking the file.

### 1. Verified the Download Status

The browser confirmed that the download had already been removed and no active downloads were running.

**Result:** The browser was not responsible for the file lock.

---

### 2. Attempted File Deletion

I attempted to delete the ISO using:

- Windows Explorer
- Command Prompt
- PowerShell

Each method returned the same error indicating the file was still being used by another process.

**Result:** Confirmed the issue was not related to file permissions.

---

### 3. Checked Running Processes

Using Task Manager, I verified that:

- The web browser was closed
- VMware Workstation was not running
- No applications appeared to be accessing the ISO

**Result:** No obvious user process was responsible.

---

### 4. Investigated Open File Handles

I searched for the ISO using:

- Windows Resource Monitor
- Microsoft Sysinternals Process Explorer

Both utilities returned no associated file handles.

**Result:** No process could be identified as locking the file.

---

### 5. Investigated OneDrive

Using the `attrib` command, I inspected the file attributes.

```cmd
attrib "<ISO Path>"
```

Output:

```text
A U
```

The `U` attribute indicated that the file was managed through OneDrive Files On-Demand.

I then:

- Paused OneDrive synchronization
- Closed OneDrive completely
- Retried deletion using administrative Command Prompt and PowerShell

**Result:** The file remained locked.

---

### 6. Booted into Safe Mode

After exhausting conventional troubleshooting methods, I suspected the lock was being maintained by a lower-level system component.

Before enabling Safe Mode, Windows displayed a BitLocker warning indicating that changes to the boot configuration could require the BitLocker recovery key. I retrieved and verified my recovery key from my Microsoft account before proceeding.

After booting into Safe Mode, I navigated to the ISO location and successfully deleted the file.

---

## Root Cause

The issue was caused by moving an ISO file into a OneDrive-synchronized directory while it was still downloading. The interrupted download created a stale filesystem lock that persisted even after the browser abandoned the download.

Because neither Resource Monitor nor Process Explorer could identify the locking process, the issue was likely maintained by a lower-level system or filesystem component. Booting into Safe Mode prevented the responsible service from loading, allowing the file to be deleted successfully.

---

## Resolution

The issue was resolved by:

- Booting Windows into Safe Mode
- Deleting the locked ISO
- Restarting Windows normally

To prevent similar issues, I moved my homelab outside of OneDrive and created the following directory structure:

```text
C:\
└── Homelab
    ├── ISOs
    ├── VMware
    ├── Documentation
    ├── Screenshots
    ├── PowerShell
    └── GitHub
```

---

## Lessons Learned

- Avoid storing virtual machines and ISO files inside cloud-synchronized folders such as OneDrive.
- Do not move large installation files while they are still downloading.
- Use a structured troubleshooting methodology before assuming corruption or permissions issues.
- Resource Monitor and Process Explorer are valuable diagnostic tools, but they cannot identify every type of filesystem lock.
- Verify BitLocker recovery information before modifying Windows boot settings.
- Safe Mode can resolve file locks that are not visible through standard Windows monitoring tools.

---

## Skills Demonstrated

- Windows troubleshooting
- Windows Server deployment preparation
- OneDrive synchronization analysis
- Resource Monitor
- Sysinternals Process Explorer
- PowerShell
- Command Prompt
- Safe Mode recovery
- BitLocker recovery procedures
- Root cause analysis
- Technical documentation
