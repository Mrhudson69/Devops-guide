# Installing MySQL Workbench on Ubuntu 22.04

To install MySQL Workbench on Ubuntu 22.04, first, you need to install the MySQL server. Follow these steps:

## Install MySQL Server

```bash
sudo apt update
sudo apt install mysql-server
sudo systemctl start mysql.service
```

This set of commands updates the package repositories, installs the MySQL server, and starts the MySQL service.

## Install MySQL Workbench

1. **Install wget (if not already installed):**
   ```bash
   sudo apt install wget
   ```
   Install wget, a tool for downloading files from the internet.

2. **Download the MySQL APT configuration file:**
   ```bash
   wget https://dev.mysql.com/get/mysql-apt-config_0.8.28-1_all.deb
   ```
   Download the MySQL APT configuration file.

3. **Install the MySQL APT configuration file:**
   ```bash
   sudo apt install ./mysql-apt-config_0.8.28-1_all.deb
   ```
   This command installs the MySQL APT configuration file. A pop-up window will appear asking which MySQL product to install; select the required product, scroll down to 'Ok,' and hit Enter to continue.

![MySQL APT Configuration](https://github.com/Mrhudson69/mysql-workbench/assets/78916631/21454b4a-7694-47e3-b884-6494874629c0)

Wait for the installation to complete, then update the apt cache:

```bash
sudo apt update
```

Finally, install MySQL Workbench:

```bash
sudo apt install mysql-workbench-community
```

This completes the installation of MySQL Workbench on your Ubuntu 22.04 system. You can now use MySQL Workbench to manage your MySQL databases.