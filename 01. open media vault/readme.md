# Setting Up OpenMediaVault on Proxmox - Step by Step Guide

Follow these steps to set up OpenMediaVault on Proxmox:

## Step 1: Download OpenMediaVault

1. Head over to your Proxmox server and log in with root.
2. Download the stable build from the official website: [OpenMediaVault Download](https://www.openmediavault.org/?page_id=77).

## Step 2: Create a VM in Proxmox

1. Upload the downloaded OpenMediaVault ISO to your Proxmox server.
2. Create a VM, and after creation, start the VM.

## Step 3: Install OpenMediaVault

1. Once the VM is powered on with the bootable media, proceed with the installation steps:

   - Select the preferred language.
   - Select your location.
   - Set the locales.
   - Set the preferred keyboard layout.

2. Provide the hostname of the server (default will work fine).
3. Set the domain name (use "local" if you don't have a domain).
4. Set the root password (for shell login, not the web interface).
5. Partition the disk and select the disk to be partitioned.
6. The installation will start.

## Step 4: Configure Package Manager

1. Set the package manager location.
2. Set the mirror server (you can select deb.debian.org).
3. If using an HTTP proxy, provide the details; otherwise, proceed.

## Step 5: Reboot and Login

1. Reboot the system.
2. Eject the installation media.
3. Login using the created root user credentials.
4. Obtain the machine's IP address by typing `ipconfig`.

## Configure OpenMediaVault NAS Storage Server

1. Access the OpenMediaVault web interface: http://IP_Address/
2. Default credentials are `admin` and `openmediavault`.
3. On successful login, you will see the dashboard.

## Step 6: Change Admin Password

1. Change the default admin password: navigate to General Settings -> Web Administrator Password.

## Step 7: Enable FTP and SMB/CIFS

1. Enable FTP: navigate to Services > FTP and enable by checking the box.
2. Enable SMB/CIFS: same procedure, navigate to Services > SMB / CIFS and enable.

## Step 8: Create Data Storage Volume

1. Mount a hard disk on your Proxmox machine via the Proxmox dashboard.
   ![Mount Disk](https://github.com/Mrhudson69/openmediavault/assets/78916631/616fa697-c2e3-4b42-b4de-3c2e65664da6)
2. Go to Storage Disks, select your disk, and click on the eraser button to wipe the data.
   ![Wipe Data](https://github.com/Mrhudson69/openmediavault/assets/78916631/8650a307-8207-4159-81bc-5eade00cbe53)

Some steps are left I will update soon when I get some time













