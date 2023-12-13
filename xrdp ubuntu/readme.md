# xrdp-ubunutu
In this guide I will show you how to install xrdp on ubuntu

Just normally upgrade and update your repo's
```
sudo apt update && sudo apt upgrade
```
Install XRDP
```
sudo apt install xrdp
dpkg -L xrdp
```
Check status of xrdp
```
sudo systemctl status xrdp
```
Add Xrdp user as ssl-cert
```
sudo adduser xrdp ssl-cert
```
Restart the xrdp services
```
sudo systemctl restart xrdp
```