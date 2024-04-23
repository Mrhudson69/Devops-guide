# Installing XRDP on Ubuntu

This guide demonstrates how to install XRDP on Ubuntu. Follow these steps:

1. **Upgrade and update your repositories:**
   ```bash
   sudo apt update && sudo apt upgrade
   ```
   This command updates and upgrades your package repositories.

2. **Install XRDP:**
   ```bash
   sudo apt install xrdp
   dpkg -L xrdp
   ```
   The first command installs XRDP, and the second command lists the files installed by XRDP.

3. **Check the status of XRDP:**
   ```bash
   sudo systemctl status xrdp
   ```
   Use this command to verify the current status of the XRDP service.

4. **Add the XRDP user as ssl-cert:**
   ```bash
   sudo adduser xrdp ssl-cert
   ```
   This command adds the user 'xrdp' to the 'ssl-cert' group.

5. **Restart the XRDP services:**
   ```bash
   sudo systemctl restart xrdp
   ```
   Use this command to restart the XRDP services, applying the changes made.

Now, XRDP should be installed and configured on your Ubuntu system. You can use remote desktop protocols to connect to your Ubuntu machine.

Note: Ensure that your firewall allows connections to the XRDP port (default is 3389) if you are connecting from a remote machine. Adjust firewall settings accordingly.

