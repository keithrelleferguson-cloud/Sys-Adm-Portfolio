# Lab 01 – Windows Server 2025 Virtual Machine Deployment

## Overview

After resolving the locked ISO issue, I rebuilt my homelab environment following industry best practices. To avoid future synchronization conflicts, I created a dedicated `C:\Homelab` directory outside of OneDrive and organized separate folders for ISO files, virtual machines, documentation, screenshots, PowerShell scripts, and GitHub project files.

The Windows Server 2025 Evaluation ISO was downloaded directly into the `C:\Homelab\ISOs` directory, providing a clean installation source for the virtual machine.

---

## Objectives

- Create a dedicated homelab directory structure
- Download a clean Windows Server 2025 Evaluation ISO
- Create the first virtual machine (`DC01`)
- Configure enterprise-style virtual hardware
- Successfully boot into the Windows Server installation environment

---

## Environment

### Host System

- Windows 11 Home (Version 25H2)
- Intel Core i5
- 16 GB RAM
- VMware Workstation Pro

### Virtual Machine

| Setting | Configuration |
|---------|---------------|
| Name | DC01 |
| Operating System | Windows Server 2025 |
| Firmware | UEFI |
| Secure Boot | Disabled |
| CPU | 1 Processor / 2 Cores |
| Memory | 4 GB |
| Disk | 80 GB |
| Network | NAT |
| Installation Media | Windows Server 2025 Evaluation ISO |

---

## Deployment Process

### 1. Prepared the Homelab Directory

To separate virtualization resources from cloud storage, I created a dedicated directory structure on the local `C:\` drive.

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

The Windows Server 2025 Evaluation ISO was downloaded directly into the `ISOs` folder.

---

### 2. Created the Virtual Machine

Using VMware Workstation Pro, I created my first virtual machine, **DC01**, which will serve as the primary Domain Controller for the enterprise homelab.

Instead of selecting VMware's default **Typical** installation, I used the **Custom (Advanced)** wizard to gain greater control over the virtual hardware configuration and to better understand the components involved in deploying an enterprise server.

The virtual machine was configured with:

- Latest VMware hardware compatibility
- Microsoft Windows operating system profile
- Windows Server 2025
- UEFI firmware
- New virtual hard disk

Secure Boot was intentionally left disabled during the initial deployment to simplify troubleshooting while maintaining a modern UEFI-based environment.

---

### 3. Configured Virtual Hardware

The virtual hardware was configured to balance performance with the available resources of the host system.

Configuration included:

- 1 virtual processor
- 2 CPU cores
- 4 GB RAM
- 80 GB virtual hard disk
- NAT virtual network adapter

The Windows Server 2025 Evaluation ISO was attached as the virtual DVD installation media.

---

### 4. Resolved Initial Boot Issue

During the first startup, VMware displayed an error indicating that it could not connect the virtual optical drive to a physical CD/DVD device on the host computer.

After reviewing the virtual machine configuration, I confirmed that the installation media was correctly mounted as an ISO image instead of a physical optical drive.

Once corrected, the virtual machine booted successfully.

The virtual machine initially entered the UEFI Boot Manager instead of automatically launching the installer. I manually selected the virtual SATA CD/DVD device, allowing Windows Server Setup to begin.

---

### 5. Installed Windows Server

After Windows Server Setup launched successfully, I retained the default regional settings for:

- Language
- Time and currency
- Keyboard layout

I selected **Windows Server 2025 Standard Evaluation (Desktop Experience)** as the operating system edition.

The Desktop Experience edition was chosen because it provides a graphical user interface that simplifies learning and administration while configuring:

- Active Directory Domain Services
- DNS
- DHCP
- Group Policy
- PowerShell
- Additional Windows Server roles and features

After confirming the installation options, Windows Server installation began successfully.

---

## Results

- ✅ Created a dedicated homelab directory outside OneDrive
- ✅ Downloaded a clean Windows Server 2025 Evaluation ISO
- ✅ Created the `DC01` virtual machine
- ✅ Configured enterprise-style virtual hardware
- ✅ Resolved VMware virtual optical drive issue
- ✅ Booted into Windows Server Setup
- ✅ Installed Windows Server 2025 Standard Evaluation (Desktop Experience)

---

## Lessons Learned

- Store virtualization resources outside cloud-synchronized folders.
- Use VMware's **Custom (Advanced)** installation for greater control over virtual hardware.
- Verify that installation media is mounted as an ISO image instead of a physical optical drive.
- Understand the UEFI boot process and manually select boot devices when necessary.
- Planning the virtual environment before deployment reduces troubleshooting later in the project.

---

## Skills Demonstrated

- VMware Workstation Pro
- Windows Server 2025 deployment
- Virtual machine configuration
- UEFI firmware configuration
- Virtual networking (NAT)
- Virtual hardware provisioning
- Windows Server installation
- Troubleshooting VMware boot issues
- Enterprise homelab design
- Technical documentation
