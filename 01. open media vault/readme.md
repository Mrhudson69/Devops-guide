# openmediavault
How to setup openmedia vault proxmox step by step guide and creating a shared folder

Step 1 - First headover to your proxmox server and login with root and download

Step 2 - Go to website download stable build according to you need - https://www.openmediavault.org/?page_id=77

Step 3 - Upload it to your proxmox server and create VM , after creation strat the VM

Step 4 - Once the VM/the machine has been powered on with the bootable media, install

Step 5 - Select the preferred language.

Step 6 - Select your location.

Step 7 - Set the locales

Step 8 - Set the preferred keyboard layout.

Step 9 - The installer will load packages from the media.

Step 10 - Provide the hostname of the server. (By Default will work fine)

Step 11 - Set the domain name. (If you have a domain name set it up else local will work fine)

Step 12 - Set the root password. This password is for the shell login and not for the web interface.

Step 13 - Partition the disk.

Step 14 - Select the disk to be partitioned.

Step 15 - The installation will then start as shown below.

Step 16 - Next, set where you want the package manager to fetch packages. Remember to set a location near you.

Step 17 - Proceed and set the mirror server. (You can select deb.debian.org)

Step 18 - If you are using an HTTP proxy to access the internet, you need to provide the details. Otherwise, proceed by hitting Enter

Step 19 - Packages will be downloaded (If its failed it means you setup DNS incorrect cross-verify)

Step 20 - Once complete, you need to reboot the system.

Step 21 - Remember to eject the installation media to avoid booting into it again. The system will boot as below.

Step 22 - Login using the created root user credentials.

Step 23 - Obtain the IP address of the machine by typing **ipconfig**

**Configure OpenMediaVault NAS Storage Server**

Step 1 - Once installed using any of the above methods, access the OpenMediaVault web interface using the URL http://IP_Address/

Step 2 - Default credentials are **admin** and **openmediavault**

Step 3 - On successful login, you will be granted the dashboard.

Step 4 - Now we need to make several configurations on the OpenMediaVault NAS Storage Server. First, change the default admin password by navigating to General Settings ->Web Administrator Password

Step 5 - Enable FTP on OpenMediaVault by navigating to Services > FTP and enable by checking the box

Step 6 - Enable SMB / CIFS just with the same procedure; Services > SMB / CIFS and enable.You also need to save the changes made and apply them.

Step 7 - Create the data storage volume : First mount a hard disk on your proxmox machine via proxmox dashboard according to you need
![image](https://github.com/Mrhudson69/openmediavault/assets/78916631/616fa697-c2e3-4b42-b4de-3c2e65664da6)

Step 8 - Then go to storage disks > Select you disk and click on eraser button to wipe the data of it.
![image](https://github.com/Mrhudson69/openmediavault/assets/78916631/8650a307-8207-4159-81bc-5eade00cbe53)

Some steps are left I will update soon when I get some time

Need some improvements in this project I will startv working soon













