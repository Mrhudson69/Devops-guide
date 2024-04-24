# Configure Vertio-WIN on Ubuntu (GUI) Proxmox

## Install Proxmox QEMU Guest Agent on Ubuntu 22.04 | 20.04 | 18.04

Before installing and activating the QEMU guest agent on your Virtual Machine, information such as the IP address of the VM is not visible on the Proxmox VE “Summary”.

![Proxmox Summary](insert_link_to_image_1)

### Install Proxmox QEMU Guest Agent on Ubuntu

Login to your Virtual Machine running in Proxmox VE and update the package index:

```bash
sudo apt update
```

Once we confirm packages can be installed, proceed to download and install the QEMU guest agent on Ubuntu 22.04 | 20.04 | 18.04:

```bash
sudo apt install qemu-guest-agent
```

Enable the service to start automatically on system reboot.

```bash
sudo systemctl enable qemu-guest-agent
```
