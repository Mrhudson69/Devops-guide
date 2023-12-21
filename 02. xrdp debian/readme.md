# Setting Up XRDP on Debian 12 Container (Proxmox)

Follow these steps to set up XRDP on a Debian 12 container in Proxmox:

1. **Install XFCE4 and XRDP:**
   ```bash
   sudo apt install xfce4
   sudo apt install xrdp
   dpkg -L xrdp
   ```
   Install the XFCE4 desktop environment and XRDP.

2. **Add XRDP User as ssl-cert:**
   ```bash
   sudo adduser xrdp ssl-cert
   ```
   Add the user 'xrdp' to the 'ssl-cert' group.

3. **Restart XRDP:**
   ```bash
   sudo systemctl restart xrdp
   ```
   Restart the XRDP service.

4. **Check XRDP Session Manager:**
   ```bash
   ls -l /etc/alternatives/x-session-manager
   ```
   Check the XRDP session manager.

5. **Configure XRDP Session Manager:**
   ```bash
   sudo update-alternatives --config x-session-manager
   ```
   Select option 3 and restart XRDP:
   ```bash
   sudo systemctl restart xrdp
   ```

6. **Done!**
   XRDP is set up on your Debian 12 container in Proxmox. You can now use an RDP client to connect to your Debian container with XRDP. Ensure that your firewall allows connections to the XRDP port (default is 3389) if you are connecting from a remote machine. Adjust firewall settings accordingly.