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

### Enable QEMU Guest Agent on Proxmox VE

After installing the package, enable it on the Proxmox VE Web interface (GUI). This is done under VM > Options section. You can see it’s disabled in our instance. Double click to open the dialog used to enable the feature.

![Enable QEMU Guest Agent](insert_link_to_image_2)

Tick the checkbox to enable QEMU Agent for your VM.

![Enable QEMU Guest Agent Checkbox](insert_link_to_image_3)

QEMU Guest Agent will be enabled but a manual instance stop and start procedure is required.

### Stop and Start VM Instance

Choose the instance and click on the dropdown list under “Shutdown”.

![Shutdown VM Instance](insert_link_to_image_4)

Confirm you want the Virtual Machine stopped.

![Confirm Shutdown](insert_link_to_image_5)

Wait for it to go down then use the “Start” button to bring the instance up.

![Start VM Instance](insert_link_to_image_6)

Once it’s live, you’ll see “QEMU Guest Agent” is fully “Enabled”.

![Enabled QEMU Guest Agent](insert_link_to_image_7)

Virtual Machine details such as IP address will appear on the Proxmox VE web interface.

![VM Details on Proxmox VE](insert_link_to_image_8)