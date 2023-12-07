# xrdp-debian
In this wiki I will guide how to setup xrdp on debian 12 container on proxmox

```
sudo apt install xfce4
sudo apt install xrdp
dpkg -L xrdp
sudo adduser xrdp ssl-cert
sudo systemctl restart xrdp
ls -l /etc/alternatives/x-session-manager
sudo update-alternatives --config x-session-manager
```
Select 3 and restart the xrdp and done 
```
sudo systemctl restart xrdp
```
