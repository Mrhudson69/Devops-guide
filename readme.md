
[Setting Up OpenMediaVault on Proxmox - Step by Step Guide](# Setting Up OpenMediaVault on Proxmox - Step by Step Guide)



# Setting Up OpenMediaVault on Proxmox - Step by Step Guide

Follow these steps to set up OpenMediaVault on Proxmox:

## Step 1: Download OpenMediaVault

1. Head over to your Proxmox server and log in with root.
2. Download the stable build from the official website: [OpenMediaVault Download](https://www.openmediavault.org/?page_id=77).

## Step 2: Create a VM in Proxmox

1. Upload the downloaded OpenMediaVault ISO to your Proxmox server.
2. Create a VM, and after creation, start the VM.

## Step 3: Install OpenMediaVault

1. Once the VM is powered on with the bootable media, proceed with the installation steps:

   - Select the preferred language.
   - Select your location.
   - Set the locales.
   - Set the preferred keyboard layout.

2. Provide the hostname of the server (default will work fine).
3. Set the domain name (use "local" if you don't have a domain).
4. Set the root password (for shell login, not the web interface).
5. Partition the disk and select the disk to be partitioned.
6. The installation will start.

## Step 4: Configure Package Manager

1. Set the package manager location.
2. Set the mirror server (you can select deb.debian.org).
3. If using an HTTP proxy, provide the details; otherwise, proceed.

## Step 5: Reboot and Login

1. Reboot the system.
2. Eject the installation media.
3. Login using the created root user credentials.
4. Obtain the machine's IP address by typing `ipconfig`.

## Configure OpenMediaVault NAS Storage Server

1. Access the OpenMediaVault web interface: http://IP_Address/
2. Default credentials are `admin` and `openmediavault`.
3. On successful login, you will see the dashboard.

## Step 6: Change Admin Password

1. Change the default admin password: navigate to General Settings -> Web Administrator Password.

## Step 7: Enable FTP and SMB/CIFS

1. Enable FTP: navigate to Services > FTP and enable by checking the box.
2. Enable SMB/CIFS: same procedure, navigate to Services > SMB / CIFS and enable.

## Step 8: Create Data Storage Volume

1. Mount a hard disk on your Proxmox machine via the Proxmox dashboard.
   ![Mount Disk](https://github.com/Mrhudson69/openmediavault/assets/78916631/616fa697-c2e3-4b42-b4de-3c2e65664da6)
2. Go to Storage Disks, select your disk, and click on the eraser button to wipe the data.
   ![Wipe Data](https://github.com/Mrhudson69/openmediavault/assets/78916631/8650a307-8207-4159-81bc-5eade00cbe53)

Some steps are left I will update soon when I get some time




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




# Setting Up Elasticsearch on Debian 12

Follow these steps to set up Elasticsearch on Debian 12:

1. **Normal Debian Updates, User Creation, and SSH Enable:**
   - Perform regular Debian updates:
     ```bash
     apt update && apt upgrade
     ```
   - Create a user (replace `<username>` with your desired username):
     ```bash
     adduser <username>
     ```
   - Enable SSH access if not already enabled.

2. **Install Dependencies and Add Elasticsearch Repository:**
   ```bash
   apt install gnupg
   sudo apt-get install apt-transport-https
   wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -
   echo "deb https://artifacts.elastic.co/packages/7.x/apt stable main" | sudo tee /etc/apt/sources.list.d/elastic-7.x.list
   sudo apt-get update && sudo apt-get install elasticsearch
   ```

3. **Configure Elasticsearch JVM Options:**
   ```bash
   nano /etc/elasticsearch/jvm.options
   ```
   Add the following lines or customize according to your needs:
   ```ini
   node.name: Coolr-Demo
   network.host: 0.0.0.0
   http.port: 9200
   bootstrap.memory_lock: true
   discovery.type: single-node
   ```

4. **Edit Elasticsearch Configuration:**
   ```bash
   nano /etc/elasticsearch/elasticsearch.yml
   ```
   Uncomment the following lines and set limits based on your requirements:
   ```yaml
   -Xms4g
   -Xmx4g
   ```

   Save the file.

5. **Done!**
   You have completed the setup of Elasticsearch on Debian 12. Make sure to start and enable the Elasticsearch service using appropriate commands for your system. Adjust configurations further based on your specific use case and requirements.



# Installing Jenkins on Debian Container (Proxmox)

To install Jenkins on a Debian container in Proxmox, follow these steps:

1. **Update and install required packages:**
   ```bash
   sudo apt update
   sudo apt install fontconfig openjdk-17-jre
   java -version
   ```
   Ensure that Java is installed correctly. The version should be similar to what is shown in the provided example.

2. **Download Jenkins GPG key:**
   ```bash
   sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
     https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
   ```
   Download the Jenkins GPG key.

3. **Add Jenkins repository:**
   ```bash
   echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
     https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
     /etc/apt/sources.list.d/jenkins.list > /dev/null
   sudo apt-get update
   sudo apt-get install jenkins
   ```
   Add the Jenkins repository and install Jenkins.

4. **Edit Jenkins service configuration:**
   ```bash
   systemctl edit jenkins
   ```
   Add the following lines:
   ```ini
   [Service]
   Environment="JAVA_OPTS=-Xmx2048M -Djava.awt.headless=true"
   ```

5. **Reload the systemd daemon:**
   ```bash
   systemctl daemon-reload
   ```

6. **Edit Jenkins default configuration:**
   ```bash
   sudo nano /etc/default/jenkins
   ```
   Add the following line, adjusting the RAM allocation according to your needs:
   ```bash
   JAVA_ARGS="-Djava.awt.headless=true -Xmx2048m -Xms2048m"
   ```

7. **Done!**
   That's all for setting up Jenkins on a Debian container in Proxmox. You have successfully installed and configured Jenkins on your system.


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


# Setting Up SQL Server 2022 on Ubuntu

Follow these commands to set up SQL Server 2022 on Ubuntu:

1. **Add Microsoft SQL Server repository:**
   ```bash
   sudo add-apt-repository "$(wget -qO- https://packages.microsoft.com/config/ubuntu/20.04/mssql-server-2022.list)"
   ```
   This command adds the Microsoft SQL Server repository to your system.

2. **Install software-properties-common:**
   ```bash
   sudo apt install software-properties-common
   ```
   Ensure that the required software properties are installed.

3. **Download Microsoft GPG key:**
   ```bash
   wget -qO- https://packages.microsoft.com/keys/microsoft.asc | sudo tee /etc/apt/trusted.gpg.d/microsoft.asc
   ```
   Download and add the Microsoft GPG key to the trusted keys.

4. **Update package repositories:**
   ```bash
   sudo apt update
   ```
   Update the package repositories with the new SQL Server repository.

5. **Install SQL Server:**
   ```bash
   sudo apt-get install mssql-server
   ```
   Install Microsoft SQL Server on your Ubuntu machine.

6. **Run SQL Server setup:**
   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```
   Follow the setup process. For the developer edition, generate a strong password from a password generator (e.g., passbolt) for the 'sa' user.

## Firewall Setup

Configure the firewall to allow necessary ports:

```bash
ufw enable
ufw allow 22
ufw allow 1433
ufw status
```
Enable the firewall, allow SSH (port 22), and allow SQL Server port (1433).

## Create User for SSH and Logins

Create a new user for SSH and logins:

```bash
useradd rohan_sirohi
passwd rohan_sirohi
usermod -aG sudo rohan_sirohi
```
Replace 'rohan_sirohi' with your desired username. This command creates a new user, sets the password, and adds the user to the sudo group.

### Accessing the Database

Try accessing the database from Server Management Studio or Azure Data Studio using the default username 'sa.' Use the generated strong password for authentication.



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



# How to Create a New Site (PM2)

Table of Contents

1. [Login to the Server](#login-to-the-server)
2. [Create Directory](#create-directory)
3. [Clone Git Repo](#clone-git-repo)
4. [Navigate to Cloned Directory](#navigate-to-cloned-directory)
5. [Navigate to Nginx Sites Directory](#navigate-to-nginx-sites-directory)
6. [Copy Configuration Files](#copy-configuration-files)
7. [Configure Copied File](#configure-copied-file)
8. [Create a Symbolic Link](#create-a-symbolic-link)
9. [Verify the Installation](#verify-the-installation)
10. [Domain Mapping](#domain-mapping)
11. [Test Site](#test-site)
12. [Generate Certbot if Required](#generate-certbot-if-required)
13. [Reload Nginx](#reload-nginx)
14. [Follow Installation Steps](#follow-installation-steps)
15. [Build and Add to PM2](#build-and-add-to-pm2)
16. [Port Issue Guide](#port-issue-guide)

## Login to the Server

```bash
cd /opt
```

## Create Directory

Replace *mediaman2* with your preferred domain name (create a folder like subdomain.stream4.tech).

```bash
mkdir mediaman2.stream4.tech
```

## Clone Git Repo

Replace *localhost:3000* with your local host and */JamLabs/media-managemnet.git* with your git repo location. It will ask for your username and password. Enter your git username and password to clone the code with the help of a developer.

```bash
git clone http://localhost:3000/JamLabs/media-managemnet.git
```

## Navigate to Cloned Directory

```bash
cd media-management/
```

## Navigate to Nginx Sites Directory

```bash
cd /etc/nginx/sites-available
```

## Copy Configuration Files

Copy the files of the previous project accordingly. If it's a Node project, copy a Node project. Use Storeman if it's a NextJS project.

```bash
sudo cp mediaman.stream4.tech mediaman2.stream4.tech
```

## Configure Copied File

```bash
cd /etc/nginx/sites-available/
sudo nano mediaman2.stream4.tech
```

## Create a Symbolic Link

```bash
sudo ln -s /etc/nginx/sites-available/mediaman2.stream4.tech /etc/nginx/sites-enabled/
```

## Verify the Installation

```bash
sudo nginx -t
```

## Domain Mapping

Make sure the domain is mapped in Godaddy or Azure.

## Test Site

Test that the site is loading with http.

## Generate Certbot if Required

```bash
sudo certbot --nginx
```

## Reload Nginx

```bash
sudo service nginx reload
```

## Follow Installation Steps

Follow the installation steps from README.md file (In this case, run `sudo yarn install`).

```bash
sudo yarn install
```

## Build and Add to PM2

```bash
sudo yarn build
```

Add it to PM2 so it runs permanently. Replace *“npm run dev”* with the project main file name and *“Media Manager (3007)”* with your preferred display name in pm2 service. Make sure to add the port.

```bash
pm2 start “npm run dev” —name “Media Manager (3007)”
```


If making a dev server from a live project:

1. Copy the file from the live server.

2. Make a directory for the new project (e.g., visitor-dev.stream4.tech).

3. Copy backend .env.local file and frontend .env.local file and paste it somewhere in notepad.

4. Make changes in port and add DB if required.

5. Run yarn command and yarn build in the project folder - frontend and backend accordingly.

6. Add in pm2 list both front-end and back-end using the below command. Make sure to change the directory location and name.

```bash
pm2 start Visitor_Backend/src/index.js --name="Visitor Dev Backend(8011)"
```


# Restoring PM2 Services on Linux Restart

If you lose your PM2 services after restarting the Linux machine, use the following three commands to restore all PM2 services:

1. **Detect init system and configure PM2 to boot on startup:**
   ```bash
   pm2 startup
   ```
   This command detects the init system and generates the necessary configurations to ensure PM2 starts on system boot.

2. **Save the current process list:**
   ```bash
   pm2 save
   ```
   This command saves the current list of running processes managed by PM2.

3. **Resurrect previously saved processes:**
   ```bash
   pm2 resurrect
   ```
   Use this command to restore the previously saved processes, bringing back all PM2-managed services.

# Creating a PM2 Service

To create a service for a PM2-managed process, use the following command:

```bash
pm2 start "controllers/index.js" --name "UniqueName"
```

Replace `"controllers/index.js"` with the path to your script and `"UniqueName"` with a name that will identify the service in the PM2 list.

# Listing All Running PM2 Services

To view a list of all running PM2 services, use the following command:

```bash
pm2 list
```

This command provides information about each running process managed by PM2.

# Checking PM2 Service Configuration

To check the configuration of a specific PM2 service, use the following command:

```bash
pm2 show 0
```

Replace `0` with the serial number of the PM2 service you want to inspect. This command displays detailed information about the specified PM2 process.

These commands help you manage and monitor PM2 services on your Linux machine, ensuring that they persist through system restarts and allowing you to check their configurations when needed.

# Installing NVM (Node Version Manager)

To install and set up NVM for managing Node.js versions, follow these commands:

1. **Install 'curl' if not already installed:**
   ```bash
   apt install curl
   ```
   This command installs the 'curl' tool, which is needed to download NVM.

2. **Download and run the NVM installation script:**
   ```bash
   curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.38.0/install.sh | bash
   ```
   This command downloads and executes the NVM installation script from the specified URL. Adjust the version number in the URL as needed.

3. **Source the bash configuration file:**
   ```bash
   source ~/.bashrc
   ```
   This command reloads the bash configuration, making NVM available in the current terminal session.

4. **Check the installed NVM version:**
   ```bash
   nvm -v
   ```
   Verify that NVM is installed by checking its version.

# Installing Node.js via NVM

To install Node.js using NVM, use the following command:

```bash
nvm install node
```

This command installs the latest version of Node.js. You can specify a particular version if needed.

# Managing Node.js Versions via NVM

NVM allows you to manage multiple Node.js versions on your system. Here are some common commands:

- **List installed Node.js versions:**
  ```bash
  nvm ls
  ```
  This command displays a list of installed Node.js versions.

- **Switch to a specific Node.js version:**
  ```bash
  nvm use <version>
  ```
  Replace `<version>` with the desired Node.js version. This sets the selected version as the active one.

- **Set the default Node.js version:**
  ```bash
  nvm alias default <version>
  ```
  Replace `<version>` with the Node.js version you want to set as the default.

- **Uninstall a specific Node.js version:**
  ```bash
  nvm uninstall <version>
  ```
  Replace `<version>` with the Node.js version you want to uninstall.

These commands help you manage Node.js versions efficiently, allowing you to switch between them based on your project requirements.


# Changing the Repository URL in Git

If you need to update the URL of your Git repository, follow these commands:

1. **Remove the existing remote named 'origin':**
   ```bash
   git remote remove origin
   ```
   This command removes the remote named 'origin' from your repository configuration.

2. **Add the new repository URL as the remote 'origin':**
   ```bash
   git remote add origin <Your complete URL here>
   ```
   Replace `<Your complete URL here>` with the URL of the new repository. This sets the new URL as the remote named 'origin.'

3. **Verify the new remote URL:**
   ```bash
   git remote -v
   ```
   This command displays the configured remote repositories. Ensure that the 'origin' remote now points to the new URL.

4. **Set the upstream branch to track changes from 'origin/dev/main':**
   ```bash
   git branch --set-upstream-to=origin/dev/main
   ```
   This sets the upstream branch to track changes from the 'dev/main' branch on the 'origin' remote.

5. **Stash your changes (if needed):**
   ```bash
   git stash
   ```
   Use this command to temporarily save your local changes in case they conflict with incoming changes from the new repository URL.

6. **Pull the latest changes from the new URL:**
   ```bash
   git pull
   ```
   Finally, run this command to fetch and merge the latest changes from the updated repository URL. This ensures your local branch is synchronized with the remote.

These commands are useful when you need to switch the remote URL of your Git repository and align your local branch with the changes from the new repository location.



| Protocol | Port Number | Full Form                           |
|----------|-------------|-------------------------------------|
| DNS      | 53 (UDP/TCP)| Domain Name System                  |
| DHCP     | 67 (UDP, server) <br> 68 (UDP, client) | Dynamic Host Configuration Protocol |
| SSH      | 22 (TCP)    | Secure Shell                        |
| FTP      | 20 (TCP, data transfer) <br> 21 (TCP, control) | File Transfer Protocol              |
| Telnet   | 23 (TCP)    | Telecommunication Network            |
| SMTP     | 25 (TCP)    | Simple Mail Transfer Protocol       |
| TFTP     | 69 (UDP)    | Trivial File Transfer Protocol      |
| HTTP     | 80 (TCP)    | Hypertext Transfer Protocol         |
| HTTPS    | 443 (TCP)   | Hypertext Transfer Protocol Secure  |
| POP3     | 110 (TCP)   | Post Office Protocol version 3      |
| IMAP4    | 143 (TCP)   | Internet Message Access Protocol    |
| SNMP     | 161 (UDP) (SNMP) <br> 162 (UDP) (SNMP traps) | Simple Network Management Protocol |
| NTP      | 123 (UDP)   | Network Time Protocol               |


### DHCP (Dynamic Host Configuration Protocol)

- **Port Number:** DHCP typically uses UDP ports 67 (server) and 68 (client).

- **DORA:** DHCP involves a four-step process known as DORA: 
  - **Discover:** The client broadcasts a request for IP address allocation.
  - **Offer:** The server responds with an offer of an IP address.
  - **Request:** The client formally requests the offered IP address.
  - **Acknowledge:** The server acknowledges the request and assigns the IP address to the client.

- **APIPA (Automatic Private IP Addressing):** If a DHCP client fails to obtain an IP address, it may assign itself an address from the reserved range 169.254.0.1 to 169.254.255.254.

- **Lease Time:** DHCP leases IP addresses to clients for a specific duration called the lease time.

- **Renew Time:** When a lease approaches expiration, the client attempts to renew the lease by contacting the DHCP server.

- **Unicast and Multicast:** DHCP communication can occur via unicast (between a client and server) or multicast (broadcasting to multiple clients simultaneously).


### DNS (Domain Name System)

- **Port Number:** DNS typically uses UDP and TCP port 53.

- **Query Types:** DNS supports various query types including:
  - **A:** Returns the IPv4 address associated with a domain name.
  - **AAAA:** Returns the IPv6 address associated with a domain name.
  - **CNAME:** Returns the canonical name for an alias.
  - **MX:** Returns the mail exchange servers for a domain.
  - **NS:** Returns the authoritative name servers for a domain.
  - **PTR:** Performs reverse DNS lookup, mapping an IP address to a domain name.
  - **TXT:** Returns text records associated with a domain.
  - **SOA:** Returns the start of authority record for a zone.

- **Records:** DNS stores various types of records to map domain names to IP addresses and perform other functions. Some common records include:
  - **A Record:** Maps a domain name to an IPv4 address.
  - **AAAA Record:** Maps a domain name to an IPv6 address.
  - **CNAME Record:** Creates an alias for a domain name.
  - **MX Record:** Specifies the mail servers responsible for receiving email on behalf of a domain.
  - **NS Record:** Specifies the authoritative name servers for a domain.
  - **PTR Record:** Maps an IP address to a domain name for reverse DNS lookups.
  - **TXT Record:** Stores arbitrary text information associated with a domain.

- **Zones:** DNS divides the domain name space into zones, which are administrative units managed by specific name servers. Each zone consists of one or more domain names and their associated records. Zones can be authoritative (primary or secondary) or caching (resolver) zones.


### TCP (Transmission Control Protocol)

#### Functions and Features:
- **Reliable Data Transmission:** TCP ensures reliable delivery of data by using acknowledgments, sequence numbers, and retransmissions.
- **Flow Control:** TCP regulates the flow of data between sender and receiver to prevent congestion and ensure efficient transmission.
- **Connection-Oriented:** TCP establishes a connection before data transfer and ensures orderly termination of the connection afterward.
- **Error Detection and Correction:** TCP uses checksums to detect errors in transmitted data and can request retransmission of corrupted segments.
- **Full Duplex Communication:** TCP supports simultaneous data transfer in both directions.
- **Multiplexing:** TCP allows multiple applications on a host to use the network simultaneously.

#### TCP Header:
The TCP header contains several fields, including source and destination port numbers, sequence and acknowledgment numbers, TCP flags, window size, checksum, and urgent pointer.

#### TCP Flags:
TCP flags, also known as control bits, include:
- SYN: Synchronize sequence numbers for connection establishment.
- ACK: Acknowledge received data.
- FIN: Indicates the sender has finished sending data.
- RST: Reset the connection.
- URG: Indicates urgent data.
- PSH: Push function, which requests immediate data delivery without buffering.
- CWR and ECE: Congestion window reduced and ECN-Echo, related to congestion control.

#### TCP Timer:
TCP uses several timers, including retransmission timers (for retransmitting lost segments), persist timers (for retransmitting zero-window probes), and keep-alive timers (to check if the connection is still alive).

#### Window Size:
The window size indicates the amount of data that can be sent before receiving an acknowledgment. It helps regulate the flow of data and prevents congestion.

#### Checksum:
The TCP checksum is used for error detection. It covers the TCP header and data payload to ensure data integrity during transmission.

#### Urgent Pointer:
The urgent pointer is used to indicate the presence of urgent data in a segment.

#### Options and Padding:
TCP options include Maximum Segment Size (MSS), Window Scaling, Selective Acknowledgment (SACK), and Timestamps. Padding is used to ensure that the TCP header ends on a 32-bit boundary.

#### Three-Way Handshake:
1. Client sends a SYN packet to the server.
2. Server responds with SYN-ACK, acknowledging the client's SYN.
3. Client sends an ACK packet, acknowledging the server's SYN-ACK. At this point, the connection is established.

#### Four-Way Handshake:
1. Initiator sends FIN packet to initiate termination.
2. Responder sends ACK to acknowledge the FIN.
3. Responder sends its own FIN packet to initiate termination from its end.
4. Initiator sends ACK to acknowledge the FIN.

#### MTU (Maximum Transmission Unit):
MTU is the maximum size of a single packet that can be transmitted on a network. It is important in TCP/IP networking for efficient data transmission.

#### Congestion Control:
TCP uses various mechanisms to handle congestion, including:
- **Three Duplicate ACKs:** Indicates network congestion, prompting TCP to reduce its transmission rate.
- **Retransmission Timeout:** Occurs when a segment is not acknowledged within a certain time, indicating congestion, leading to retransmission.
- **Congestion Avoidance:** TCP reduces its transmission rate upon congestion detection, gradually increasing it to find the optimal rate.

#### Action Taken upon Congestion:
- **Mild Action:** Reduce the transmission rate by a small factor.
- **Strong Action:** Drastically reduce the transmission rate or temporarily halt data transmission to alleviate congestion.


### SMTP (Simple Mail Transfer Protocol)
- **Port Number:** SMTP typically uses TCP port 25.
- **Working:** SMTP is a protocol used for sending email messages between servers. When you send an email, your email client communicates with your email server using SMTP. The email server then relays the message to the recipient's email server, which is also done via SMTP. Finally, the recipient's email server stores the message until the recipient retrieves it.

### POP3 (Post Office Protocol version 3)
- **Port Number:** POP3 typically uses TCP port 110.
- **Working:** POP3 is a protocol used for retrieving email messages from an email server to a client device. When you check your email using a POP3 client (like Outlook or Thunderbird), the client connects to the email server and downloads any new messages to your device. By default, POP3 downloads the messages to your device and typically deletes them from the server, although there are options to keep copies on the server.

### IMAP (Internet Message Access Protocol)
- **Port Number:** IMAP typically uses TCP port 143.
- **Working:** IMAP is also used for retrieving email messages from an email server to a client device, similar to POP3. However, IMAP offers more advanced features compared to POP3. With IMAP, emails are stored on the server rather than being downloaded to the client device. This allows for easier access to emails from multiple devices since the emails remain synchronized across devices. IMAP also supports organizing emails into folders on the server, allowing for better management of email messages.


### SSL (Secure Sockets Layer) and TLS (Transport Layer Security)

#### Working:
- **SSL and TLS** are cryptographic protocols designed to provide secure communication over a computer network.
- They establish an encrypted connection between a client (such as a web browser) and a server (such as a website).
- SSL was the predecessor of TLS, and TLS is the more modern and secure version.
- These protocols ensure confidentiality, integrity, and authenticity of data transmitted over the network.

#### SSL Handshake (TLS Handshake):
- **ClientHello:** The client sends a message containing supported SSL/TLS versions, supported cipher suites, and other parameters.
- **ServerHello:** The server responds with the chosen SSL/TLS version, selected cipher suite, and other parameters.
- **Key Exchange:** The server sends its public key or certificate to the client, and the client verifies the certificate.
- **Client Authentication (Optional):** If required, the client may authenticate itself to the server using a certificate.
- **Pre-master Secret:** The client generates a random pre-master secret, encrypts it with the server's public key, and sends it to the server.
- **Session Keys Generation:** Both client and server use the pre-master secret to independently generate session keys for encrypting and decrypting data.
- **Finished Messages:** Both parties exchange "finished" messages to confirm that the handshake is complete and that subsequent communication will be encrypted.

#### Symmetric Encryption:
- **Symmetric encryption** uses the same key for both encryption and decryption.
- It's fast and efficient for encrypting large amounts of data.
- Common symmetric encryption algorithms include AES (Advanced Encryption Standard) and DES (Data Encryption Standard).

#### Asymmetric Encryption and Formation of Key:
- **Asymmetric encryption** uses a pair of keys: a public key for encryption and a private key for decryption.
- The public key can be freely distributed, while the private key is kept secret.
- To form a key using asymmetric encryption, one party (e.g., the client) generates a public-private key pair and shares the public key with the other party (e.g., the server).
- The other party uses the received public key to encrypt a message and sends it back.
- The original party decrypts the message using its private key.

#### Hash Function:
- **Hash functions** are cryptographic algorithms that generate a fixed-size hash value from input data of any size.
- They are used for data integrity verification and digital signatures.
- Hash functions should produce a unique hash value for each unique input.
- Common hash functions include SHA-256 (Secure Hash Algorithm 256-bit) and MD5 (Message Digest Algorithm 5).


### Hub:
- **Functionality:** A hub is a basic networking device that operates at the physical layer (Layer 1) of the OSI model.
- **Operation:** It receives data from one device and broadcasts it to all other devices connected to the hub.
- **Collision Domain:** All devices connected to a hub share the same collision domain, leading to collisions and reduced network efficiency.
- **Not Common:** Hubs are not commonly used in modern networks due to their limitations in performance and collision handling.

### Router:
- **Functionality:** A router is a networking device that operates at the network layer (Layer 3) of the OSI model.
- **Operation:** It forwards data packets between different networks based on IP addresses.
- **Routing Table:** Maintains a routing table to determine the best path for data transmission.
- **NAT:** Can perform Network Address Translation (NAT) to allow multiple devices on a local network to share a single public IP address.
- **Firewall:** Often includes firewall capabilities for network security.

### Switch:
- **Functionality:** A switch is a networking device that operates at the data link layer (Layer 2) of the OSI model.
- **Operation:** It forwards data packets between devices within the same network based on MAC addresses.
- **MAC Table:** Maintains a MAC address table to determine the port to which a packet should be forwarded.
- **Collision Domain:** Each port on a switch has its collision domain, leading to improved network performance compared to hubs.
- **VLAN:** Supports Virtual LAN (VLAN) segmentation for network organization and security.

### Bridge:
- **Functionality:** A bridge is a networking device that operates at the data link layer (Layer 2) of the OSI model.
- **Operation:** It connects multiple network segments and forwards data between them based on MAC addresses.
- **Similarity to Switch:** Bridges are similar to switches in functionality, but they typically have fewer ports and are used to connect smaller network segments.
- **MAC Table:** Like switches, bridges maintain a MAC address table for packet forwarding.

### Key Differences:
- **Layer of Operation:** Hubs operate at Layer 1, switches and bridges at Layer 2, and routers at Layer 3.
- **Forwarding Mechanism:** Hubs broadcast data to all connected devices, switches and bridges forward data based on MAC addresses within the same network, while routers forward data based on IP addresses between different networks.
- **Collision Handling:** Hubs have a single collision domain, switches and bridges have per-port collision domains, and routers do not have collision domains as they operate at Layer 3.


### ARP (Address Resolution Protocol):
- **Functionality:** ARP is used to map IP addresses to MAC addresses within a local network.
- **Operation:** When a device needs to communicate with another device on the same network, it uses ARP to discover the MAC address corresponding to the IP address.
- **Request-Reply Mechanism:** A device sends an ARP request broadcast containing the IP address it wants to reach, and the device with that IP address replies with its MAC address.
- **ARP Cache:** Devices maintain an ARP cache to store recently resolved IP-to-MAC mappings for faster future communication.

### Types of ARP:
1. **ARP:** Standard Address Resolution Protocol used to resolve IPv4 addresses to MAC addresses.
2. **RARP (Reverse ARP):** Used to resolve MAC addresses to IP addresses, primarily in diskless workstation environments. Less common nowadays due to DHCP.
3. **Proxy ARP:** A technique where a device responds to ARP requests on behalf of another device, typically used in network address translation (NAT) scenarios.
4. **Gratuitous ARP (GARP):** An unsolicited ARP message where a device announces its own IP-to-MAC mapping to update the ARP caches of other devices.

### Gratuitous ARP (GARP):
- **Functionality:** GARP is used to update the ARP caches of other devices on the network with a new MAC address mapping for an IP address.
- **Usage:** It can be used for network redundancy, IP address conflicts resolution, or updating ARP caches after network reconfiguration.
- **Difference from ARP:** Unlike ARP, which is initiated when a device needs to resolve an IP address, GARP is sent proactively by a device to inform other devices of its own IP-to-MAC mapping changes.

### Inverse ARP (InARP):
- **Functionality:** Inverse ARP is used in Frame Relay and ATM networks to resolve network layer addresses (IP addresses) from data link layer addresses (DLCIs in Frame Relay or VPI/VCI in ATM).
- **Operation:** InARP messages are sent between the router and the switch or access device to map DLCIs or VPI/VCI to IP addresses.
- **Purpose:** It allows routers in Frame Relay or ATM networks to dynamically learn the mapping between network layer addresses and data link layer addresses without manual configuration.

### IP Addressing (IPv4)
- **Classification:** IPv4 addresses are classified into five classes: A, B, C, D, and E. Each class has a range of addresses determined by the first few bits of the address.
- **Broadcast Domain:** A broadcast domain is a network segment within which broadcast messages can reach all devices. In IPv4, devices in the same subnet (determined by the subnet mask) belong to the same broadcast domain.
- **Finding Broadcast Domain:** To find the broadcast domain in IPv4, determine the network address using bitwise AND operation between the IP address and subnet mask. Then, the broadcast address is the network address with all host bits set to 1. All devices with IP addresses within this range are in the same broadcast domain.

### How to find network ID's
To find the network ID of an IPv4 address, you perform a bitwise AND operation between the IP address and its subnet mask. This operation preserves the network portion of the address and sets the host portion to 0, giving you the network ID.

### NAT (Network Address Translation):
- **Usage:** NAT is used to translate private IP addresses of devices within a local network into a single public IP address for communication over the internet.
- **Purpose:** It allows multiple devices within a local network to share a single public IP address, conserving IPv4 address space and providing an additional layer of security by hiding internal IP addresses from external networks.
- **Operation:** NAT works by modifying the source and/or destination IP addresses in IP packets as they traverse a NAT-enabled router or firewall.
- **Types:** 
  - **Static NAT:** Maps a private IP address to a specific public IP address, typically used for hosting servers.
  - **Dynamic NAT:** Maps private IP addresses to public IP addresses from a pool of available addresses dynamically.
  - **PAT (Port Address Translation):** A form of dynamic NAT where multiple private IP addresses are mapped to a single public IP address using different port numbers.

### PAT (Port Address Translation):
- **Usage:** PAT, also known as NAT overload, is a variation of NAT commonly used in home and small office networks.
- **Purpose:** It allows multiple devices within a local network to share a single public IP address by using different port numbers to distinguish between connections.
- **Operation:** PAT maps each private IP address and port number combination to a unique public IP address and port number, enabling multiple devices to establish simultaneous connections over the internet.
- **Benefits:** PAT conserves public IP addresses, enhances security by masking internal IP addresses, and facilitates communication for devices within the local network.

## VLSM
VLSM, or Variable Length Subnet Masking, allows for the allocation of IP addresses more efficiently by permitting different subnets to have varying subnet mask lengths. This flexibility enables the creation of subnets tailored to specific requirements, optimizing IP address utilization. 

## ACL
ACLs, or Access Control Lists, are used to control network traffic by defining rules that either permit or deny packets based on specified criteria. These criteria typically include factors like source/destination IP addresses, protocols, port numbers, and interface directions. ACLs enhance network security and performance by regulating traffic flow at network devices such as routers, switches, and firewalls.

## SUPERNETTING
Supernetting, also known as route aggregation, involves combining multiple contiguous subnets into a single larger subnet. This process reduces the size of routing tables by summarizing several subnets as a single entry. By aggregating subnets, supernetting conserves memory and processing resources in routers, decreases routing table size, and improves routing scalability.


### Fragmentation and Segmentation

**Fragmentation:**
- **Definition:** Fragmentation occurs when a large data packet is broken into smaller fragments to fit within the Maximum Transmission Unit (MTU) size of the network.
- **Usage:** Fragmentation is typically performed by routers when forwarding packets between networks with different MTU sizes.
- **Result:** Each fragment retains a portion of the original packet's data and a fragment header to indicate its position within the original packet.
- **Purpose:** Fragmentation ensures that data can be transmitted across networks with varying MTU sizes while adhering to size constraints.

**Segmentation:**
- **Definition:** Segmentation involves dividing a large data stream into smaller segments at the transport layer of the OSI model.
- **Usage:** Segmentation is performed by transport layer protocols such as TCP to optimize data transmission and manage flow control.
- **Result:** Each segment contains a portion of the original data along with transport layer headers for routing and sequencing.
- **Purpose:** Segmentation improves network performance by efficiently transmitting data in smaller, manageable units and allows for reliable data delivery through features like sequence numbering and acknowledgment.

**Difference:**
- **Fragmentation** occurs at the network layer (Layer 3) and is primarily performed by routers to accommodate differing MTU sizes between networks, whereas **segmentation** occurs at the transport layer (Layer 4) and is performed by transport layer protocols to optimize data transmission and manage flow control.
- Fragmentation breaks large packets into smaller fragments for transmission across networks, while segmentation divides data streams into smaller segments for efficient transport and reliable delivery within a network.

### HTTP (Hypertext Transfer Protocol)
- **Port Number:** HTTP typically uses TCP port 80.
- **Usage:** HTTP is a protocol used for transmitting hypertext documents, such as HTML files, over the internet.
- **Security:** HTTP does not provide encryption for data transmission, making it vulnerable to interception and manipulation by malicious actors.
- **Example:** `http://www.example.com` 

### HTTPS (HTTP Secure)
- **Port Number:** HTTPS typically uses TCP port 443.
- **Usage:** HTTPS is a secure version of HTTP that uses encryption to ensure secure communication between a client and a server.
- **Security:** HTTPS encrypts data transmitted between the client and server, preventing eavesdropping and tampering.
- **Example:** `https://www.example.com`

**Difference:**
- The main difference between HTTP and HTTPS is the security aspect. HTTP transmits data in plaintext, while HTTPS encrypts data using SSL/TLS protocols, providing secure communication over the internet.
- HTTPS is preferred for transmitting sensitive information such as passwords, credit card numbers, and personal data, as it ensures confidentiality and integrity of data during transmission.


### OSPF (Open Shortest Path First)
 OSPF is a dynamic routing protocol used to determine the shortest path to destinations within an IP network. It employs various mechanisms such as AD values, DR/BDR election, packet types, and LSAs to maintain network connectivity and provide efficient routing.

#### Administrative Distance (AD) Value:
- **Definition:** OSPF assigns a default administrative distance (AD) value of 110 to its routes.
- **Usage:** AD is used by routers to determine the preferred route when multiple routing protocols are present.
- **Example:** If OSPF and another routing protocol advertise routes to the same destination, the router will prefer the OSPF route due to its lower AD value.

#### DR (Designated Router) and BDR (Backup Designated Router) Election:
- **Purpose:** In multi-access network segments (e.g., Ethernet), OSPF elects a DR and BDR to reduce OSPF overhead and optimize network efficiency.
- **Operation:** OSPF routers on the segment elect a DR and BDR based on their Router ID (RID). The DR and BDR are responsible for sending and receiving OSPF updates on behalf of the network segment.
- **Example:** In a LAN segment with multiple OSPF routers, the router with the highest priority or highest RID becomes the DR, and the router with the second-highest priority becomes the BDR.

#### OSPF Broadcast Network Types:
- **Definition:** OSPF supports several network types, including broadcast, point-to-point, point-to-multipoint, and non-broadcast multi-access (NBMA).
- **Usage:** The broadcast network type is commonly used for Ethernet LANs where OSPF routers can communicate with each other through broadcast messages.
- **Example:** OSPF routers on an Ethernet LAN use OSPF hello packets to discover neighbors and elect a DR and BDR.

#### OSPF IP Addresses:
- **Usage:** OSPF uses IP addresses for router identification (RID) and neighbor identification.
- **Example:** Each OSPF router is assigned a unique RID, typically the highest IP address on a loopback interface, to identify itself within the OSPF domain.

#### OSPF Packet Types:
- **Hello Packets:** Used for neighbor discovery, adjacency formation, and DR/BDR election.
- **Database Description (DBD) Packets:** Used to exchange information about the OSPF link-state database during adjacency formation.
- **Link State Request (LSR) Packets:** Used to request specific link-state advertisements (LSAs) from OSPF neighbors.
- **Link State Update (LSU) Packets:** Used to advertise new or updated LSAs to OSPF neighbors.
- **Link State Acknowledgment (LSAck) Packets:** Used to acknowledge received LSAs.

#### OSPF Packet with LSA (Link State Advertisement) and Types:
- **LSA Definition:** LSAs contain information about the state of OSPF routers and links within an OSPF area.
- **LSA Types:**
  - **Router LSA (Type 1):** Advertises router information, including the router's own link-state and the state of its interfaces.
  - **Network LSA (Type 2):** Advertises information about multi-access networks, including the DR and connected routers.
  - **Summary LSA (Type 3, 4, and 5):** Advertises routes from one area to another.
  - **AS External LSA (Type 5):** Advertises routes external to the OSPF domain.
  - **Link Local LSA (Type 9):** Advertises IPv6 link-local addresses.
  - **Intra-Area-Prefix LSA (Type 9):** Advertises IPv6 prefixes within an OSPF area.

Certainly!

### EIGRP (Enhanced Interior Gateway Routing Protocol)
EIGRP is known for its efficient use of bandwidth, fast convergence, and support for multiple network technologies. By using advanced algorithms and packet types, EIGRP ensures reliable and scalable routing in complex network environments.

#### Administrative Distance (AD) Value:
- **Definition:** EIGRP assigns a default administrative distance (AD) value of 90 to its routes.
- **Usage:** AD is used by routers to determine the preferred route when multiple routing protocols are present.
- **Example:** If EIGRP and another routing protocol advertise routes to the same destination, the router will prefer the EIGRP route due to its lower AD value.

#### Working:
- **Operation:** EIGRP is an advanced distance-vector routing protocol that uses a combination of Diffusing Update Algorithm (DUAL) and distance-vector algorithms.
- **Features:** EIGRP maintains a topology table, routing table, and neighbor table to exchange routing information and calculate the best routes.
- **DUAL Algorithm:** Ensures loop-free and fast convergence by providing loop prevention and route calculation mechanisms.
- **Convergence:** EIGRP supports fast convergence by sending partial updates and using feasible successors for backup routes.

#### EIGRP Packet Types:
- **Hello Packets:** Used for neighbor discovery and to maintain neighbor relationships.
- **Update Packets:** Used to exchange routing information, including reachable destinations and associated metrics.
- **Query Packets:** Sent by a router when it loses a route and queries neighboring routers for an alternative path.
- **Reply Packets:** Sent in response to query packets to provide information about alternative routes.


# GOCD Linux PM2 Setup with GOCD Agent

## GOCD Linux PM2 Setup

### 1. Login into Linux Machine

### 2. Install curl if not already installed on the machine using the following command:

```bash
sudo apt install curl
```

### 3. Check connectivity of GOCD Server from VM (Agent):

```bash
curl http://88.198.21.22:9353/go
sudo apt update
```

### 4. Install Node:

```bash
curl -fsSL https://deb.nodesource.com/setup_16.x | sudo -E bash -
```

### 5. Check Node/NPM installed:

```bash
node -v
npm -v
```

### 6. Install git:

```bash
sudo apt install git
```

Verify git installation:

```bash
git --version
```

### 7. Create a directory:

```bash
sudo mkdir -p /var/www/.pm2
export PM2_HOME=/var/www/.pm2
```

### 8. Create a group PM2:

```bash
sudo groupadd pm2
```

### 9. Add your user to the pm2 group (replace 'pramod' with your user):

```bash
sudo usermod -aG pm2 pramod
```

### 10. Give permissions to the PM2 group for the created folder:

```bash
sudo chown -R :pm2 /var/www/.pm2
```

### 11. Install PM2:

```bash
sudo npm install pm2 -g
```

### 12. Set PM2_HOME directory to the created folder and check PM2 status:

```bash
PM2_HOME=/var/www/.pm2 pm2 status
```

### 13. Edit etc/bash.bashrc file and add `export PM2_HOME=/var/www/.pm2` at the end:

```bash
sudo nano /etc/bash.bashrc
```

### 14. Update env path (replace 'pramod' with your user):

```bash
sudo env PATH=$PATH:/usr/bin /usr/lib/node_modules/pm2/bin/pm2 startup systemd -u pramod --hp /home/pramod
```

### 15. Update /etc/systemd/system/pm2-pramod.service (replace 'pramod' with your user) and Add this line: `export PM2_HOME=/var/www/.pm2`

```bash
sudo nano /etc/systemd/system/pm2-pramod.service
exit
```

### 16. Correct path of PM2 Environment and PIDFile:

```bash
cd /etc/systemd/system
sudo nano pm2-pramod.service
```

Edit these lines:

```ini
Environment=PM2_HOME=/var/www/.pm2
PIDFile=/var/www/.pm2/pm2.pid
```

Save and exit from this file.

### 17. Run the following commands to give permission to PM2 group (user pramod):

```bash
sudo usermod -g pm2 pramod
sudo usermod -g pm2
sudo usermod pramod -g pm2
id pramod
sudo usermod -aG pm2 go
id go
sudo systemctl stop pm2-pramod
sudo systemctl daemon-reload
sudo systemctl start pm2-pramod
sudo systemctl status pm2-pramod
sudo chmod -R 777 /var/www/.pm2
sudo systemctl restart pm2-pramod
sudo systemctl status pm2-pramod
```

## GOCD Agent Installation

```bash
sudo install -m 0755 -d /etc/apt/keyrings
curl https://download.gocd.org/GOCD-GPG-KEY.asc | sudo gpg --dearmor -o /etc/apt/keyrings/gocd.gpg
sudo chmod a+r /etc/apt/keyrings/gocd.gpg
echo "deb [signed-by=/etc/apt/keyrings/gocd.gpg] https://download.gocd.org /" | sudo tee /etc/apt/sources.list.d/gocd.list
sudo apt-get update
sudo apt-get install go-agent
```

```bash
cd /usr/share/go-agent
sudo chmod -R 777 wrapper-config/
```

Open /usr/share/go-agent/wrapper-config/wrapper-properties.conf in your favorite text editor.

Replace this line with your go-agent URL 'wrapper.app.parameter.101=http://localhost:8153/go':

```bash
wrapper.app.parameter.101=http://localhost:8153/go
```

Save the file and exit.

Start your agent:

```bash
sudo systemctl start go-agent
```

## Environment Variables Changes for PM2

### 1. Add Environment variable in pipeline stage:

```bash
PM2_HOME=/var/www/.pm2
```

### 2. Restart your agent again:

```bash
sudo service go-agent restart
```

## Adding a Service using PM2

1. Go to your app folder (Example - /var/lib/go-agent/pipelines/coolr-reporting).
2. Run the following command to add the app to PM2:

```bash
pm2 start index.mjs --name coolr-reporting-test
```

```bash
pm2 save
```



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


# How to upgrade node in aws linux to a specific version

```bash
wget -nv https://d3rnber7ry90et.cloudfront.net/linux-x86_64/node-v18.17.1.tar.gz
mkdir /usr/local/lib/node
tar -xf node-v18.17.1.tar.gz
mv node-v18.17.1 /usr/local/lib/node/nodejs
### Unload NVM, use the new node in the path, then install some items globally.
echo "export NVM_DIR=''" >> /home/ec2-user/.bashrc
echo "export NODEJS_HOME=/usr/local/lib/node/nodejs" >> /home/ec2-user/.bashrc
echo "export PATH=\$NODEJS_HOME/bin:\$PATH" >> /home/ec2-user/.bashrc
### Reload environment
. /home/ec2-user/.bashrc
### Verify NodeJS v18.x is operating
node -e "console.log('Running Node.js ' + process.version)" 
```


# How to setup reporting tool in docker

## Pre-requisites 

1. Container Linux Preferred (Ubuntu 22.04)
2. Access to [Coolr Reporting Project](https://github.com/Coolr/coolr-reporting.git)
3. Database access: username, password, IP

## Setup Docker

### Install Docker using the apt repository

1. Set up Docker's apt repository.

```bash
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```

2. Install the Docker packages.

```bash
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

3. Verify Docker Engine installation by running the hello-world image.

```bash
sudo docker run hello-world
```

## Setup Portainer

1. Create Docker Volume.

```bash
docker volume create portainer_data
```

2. Install Portainer Server.

```bash
docker run -d -p 8000:8000 -p 9443:9443 --name portainer \
--restart=always \
-v /var/run/docker.sock:/var/run/docker.sock \
-v portainer_data:/data \
portainer/portainer-ce:2.9.3
```

3. Access Portainer Dashboard.

Portainer UI is accessible through a browser at:
- [192.168.13.xx:9443](http://192.168.13.xx:9443)
- [localhost:9443](http://localhost:9443)

## Project setup for internal reporting

1. Navigate to the desired folder.

```bash
cd /opt/
```

2. Clone the project.

```bash
git clone https://github.com/Coolr/coolr-reporting.git
```

3. Go to the project folder.

```bash
cd coolr-reporting
```

4. Create a Dockerfile.

```bash
nano Dockerfile
```

5. Inside the Dockerfile, add instructions for running the project using Docker.

```Dockerfile
# Specify node version you want to use
FROM node:18

# Working directory
WORKDIR /opt/coolr-reporting

# Copy package.json files
COPY package*.json ./

# Install project dependencies
RUN npm install

# Copy source files
COPY . .

# Command to start the project
CMD [ "node", "index.mjs" ]
```

6. Create .dockerignore file.

```bash
node_modules
build
npm-debug.log
.vscode
```

7. Build the Docker container.

```bash
docker build /opt/coolr-reporting/ -t coolr-reporting:latest
```

8. Start the container.

```bash
docker run -d \
  --name coolr-reporting \
  --env-file /opt/coolr-reporting/.env.local \
  -p 3080:3080 \
  coolr-reporting:latest
```

9. Check logs for errors.

```bash
docker logs coolr-reporting
```

10. Test the internal reporting site in a browser using the URL with port.

```
http://192.168.61.112:3080/
```

![Screenshot](clipboard-202402161334-xrrgy.png)
```