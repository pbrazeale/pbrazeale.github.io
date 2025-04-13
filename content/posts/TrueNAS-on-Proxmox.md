+++
tags = ['Home Lab', 'Virtual Environment', 'Linux', 'Articles']
title = 'TrueNas on Proxmox PVE'
date = 2025-04-12T23:01:07+01:00
draft = false
+++

## TrueNAS Download

1. First, visit the website: [https://www.TrueNAS.com/download-TrueNAS-scale/](https://www.TrueNAS.com/download-TrueNAS-scale/)
2. Signup, or click "No Thank you, I have already signed up".

   ![../images/../images/TrueNAS_01.png]

3. Copy the link for the stable version: (This is the stable version as of writing [24.10.2.1](https://download.sys.TrueNAS.net/TrueNAS-SCALE-ElectricEel/24.10.2.1/TrueNAS-SCALE-24.10.2.1.iso), but check for the latest stable version on the site.)
4. Inside Proxmox VE, select your local storage, then go to the ISO Images tab and click Download from URL.
5. Paste URL and Query URL, and then Download
   ![../images/../images/TrueNAS_03.png]
6. Grab a drink and wait for download to complete

## TrueNAS VM Setup

1. Still inside proxmox, select Create VM 1. Node: default 2. VM ID: use your numbering convention 3. Name: TrueNAS-SCALE 4. Enable Advanced Settings 1. Start at boot: check 5. Click Next
   ![../images/TrueNAS_04.png]
2. OS section
   1. ISO image: select TrueNAS
      - _If the ISO isn’t listed, verify it finished downloading._
   2. click Next
3. System section
   1. leave as default
   2. select Next
4. Disks 1. Make sure Advanced settings are enabled 1. SSD emulation: check
   ![../images/TrueNAS_05.png]
5. CPU
   1. Sockets: 1
   2. Cores: 4
   3. Type: host
   4. select Next

##### NOTE: I'm running an Intel E5-2680V3 with 12 cores, 24 threads. You may want to allocate less cores. Proxmox will allow for over allocation, but I would advise against allocating more than 200%.

![../images/TrueNAS_06.png] 6. Memory - Memory (MiB): 16384 - select Next

##### NOTE: I'm running 62.71GiB, [TrueNAS recommends](https://www.TrueNAS.com/docs/scale/22.12/gettingstarted/scalehardwareguide/#minimum-hardware-requirements) 8GB. But again Proxmox allows for over allocation.

> "At its most basic level, one GB is defined as 1000³ (1,000,000,000) bytes and one GiB as 1024³ (1,073,741,824) bytes. That means one GB equals 0.93 GiB."- [Source](https://massive.io/file-transfer/gb-vs-gib-whats-the-difference/#gb-vs-gib-so-what-is-the-difference) 7. Network

    - Default is fine
    - select Next

8. Confirm
   - check Start after created
   - select Finish

## TrueNAS Install

1. Select the VM "200 (TrueNAS-SCALE)" _(top right tab in Proxmox UI)_
   - Console
2. Installation GUI
   1. Install/Upgrade, select OK
   2. Should see 32GiB disk
      1. spacebar to select it
      2. select OK
   3. Warning, select Yes
   4. Web UI Authentication Method
      1. Down arrow "Configure using Web UI"
      2. select OK
   5. Legacy Boot
      1. Allow EFI, select Yes
         - older systems may require legacy boot.
   6. wait for install
   7. Installation Succeeded
      1. select OK
      2. down arrow to Reboot System
         1. select OK
         2. grab a drink and wait for reboot
3. When finished you'll see an IP address
   ![../images/TrueNAS_07.png]

## TrueNAS Web Interface

1. “In your web browser, go to the IP address displayed in the console (e.g., `http://192.168.1.161`)
   ![../images/TrueNAS_08.png]
2. Set a strong admin password
3. Return to Proxmox 1. select Proxmox instance 1. select Disks 2. Identify your disk(s) model and serial number
   ![../images/TrueNAS_09.png] 2. open Proxmox shell 1. type: `ls /dev/disk/by-id` 2. Copy disk IDs (they match model**\*serial number**) 1. ata-ST8000NC0002-1XX112**\*ZA19WJ59** 2. ata-ST8000NC0002-1XX112\_**ZA1AMANT** 3. Select TrueNAS VM 1. select Hardware 1. select CD/DVD 1. select remove 2. confirm 3. verify Hard Disk (scsi0) 4. open ProxMox shell 1. You're going to mount the disk(s) to TrueNAS VM. 2. Use the following syntax to attach each disk:

```bash
qm set <VM_ID> -scsi<X> /dev/disk/by-id/<DISK_ID>
```

- Replace `<VM_ID>` with the ID of your TrueNAS VM (e.g., `200`)
- Replace `<X>` with the SCSI slot (e.g., `1`, `2`, etc.)
- Replace `<DISK_ID>` with the disk identifier you copied earlier

**Example:**

```bash
qm set 200 -scsi1 /dev/disk/by-id/ata-ST8000NC0002-1XX112_ZA19WJ59
qm set 200 -scsi2 /dev/disk/by-id/ata-ST8000NC0002-1XX112_ZA1AMANT
```

- After running these commands, go back to **Proxmox > TrueNAS VM > Hardware**. You should now see the new SCSI drives listed.

![../images/TrueNAS_10.png]

4. Return to TrueNAS web portal 1. Select Storage 1. Disks 2. and we should see the new hard drives
   ![../images/TrueNAS_11.png] 2. Select Storage again 1. select Create pool 2. General Info 1. Name: `HDD8000` (use whatever works for you. I'm using 8TB so 8000) 2. select Next 3. Data 1. Layout: `Mirror` (use whatever works for you. I'm using 2X 8TB HDDs. I'd have done RAIDZ1 but couldn't get a third HDD. You can hover your mouse over each option for more information.) 2. select "Save And Go To Review" 4. Review 1. Verify MIRROR 2. select Create Pool 3. check Confirm 4. select Continue 3. Will automatically be sent to "Storage Dashboard"
   ![../images/TrueNAS_12.png] 4. Select Datasets (left panel) 1. Select Add Dataset 1. Name: `personal_backups` 2. select Save 3. graph will update to show new child dataset
   ![../images/TrueNAS_13.png] 4. This will allow for permission controls for network shares.

##### NOTE: "Add Zvol" is used for creating storage for VMs.
