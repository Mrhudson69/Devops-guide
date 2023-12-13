# mysql-workbench
In this guide I will show you how to install mysql-workbench in ubuntu 22.04

**In order to install mysql-workbench first you need to install mysql server**

## First install mysql server

```
sudo apt update
sudo apt install mysql-server
sudo systemctl start mysql.service
```

## Now Install Mysql-workbench

Download package file from - https://dev.mysql.com/downloads/repo/apt/ (You can download it using wget)

```
sudo apt install wget
wget https://dev.mysql.com/get/mysql-apt-config_0.8.28-1_all.deb
sudo apt install ./mysql-apt-config_0.8.28-1_all.deb
```
A pop-up window appears asking which MySQL product to install. As the required product is preselected, scroll down to Ok and hit Enter to continue installing.

![image](https://github.com/Mrhudson69/mysql-workbench/assets/78916631/21454b4a-7694-47e3-b884-6494874629c0)

Wait for the installation to complete.

![image](https://github.com/Mrhudson69/mysql-workbench/assets/78916631/d3b0e6e4-269d-4386-8e91-9c951f81085e)

Then, update the apt cache to add the new repository source:
```
sudo apt update
```
Finally, install MySQL Workbench by running:
```
sudo apt install mysql-workbench-community
```

Done That's all for installing mysql-workbench
