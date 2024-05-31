### Setup Wireguard VPN on proxmox inside LXC Container

1. First you need to setup a container on proxmox, it is suggested to use ubuntu
2. After creating container login to the container and update it 
```
apt update && apt upgrade -y
```
3. After updating install wireguard in the container by using below command - Github for wireguard https://github.com/Nyr/wireguard-install
```
wget https://git.io/wireguard -O wireguard-install.sh && bash wireguard-install.s
```
