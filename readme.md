







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

```bash
http://192.168.61.112:3080/
```

![Screenshot](clipboard-202402161334-xrrgy.png)


# How to Create User Access on the GOCD Dashboard for a Specific Project

### Overview
This guide provides step-by-step instructions on how to create user access on the GOCD dashboard for a specific project.

### Steps

**Step 1:**  
Login to the GOCD server.

**Step 2:**  
Navigate to the configuration directory of GOCD server:
```
C:\Program Files (x86)\Go Server\config
```

**Step 3:**  
Edit the configuration file named `cruise-config.xml`.

**Step 4:**  
Add the desired user(s) to the configuration. For example:
```
<server id="media-man" ip="127.0.0.1" hostname="localhost">
  <filesystem/>
  <security>
    <passwordFile path="C:\Program Files (x86)\Go Server\Users\media-man.txt"/>
  </security>
</server>
<server id="pcx" ip="127.0.0.1" hostname="localhost">
  <filesystem/>
  <security>
    <passwordFile path="C:\Program Files (x86)\Go Server\Users\pcx.txt"/>
  </security>
</server>
```

**Step 5:**  
Restart the Go-server service.

**Step 6:**  
Go to [htpasswd-generator](https://hostingcanada.org/htpasswd-generator/) for password generation.

**Step 7:**  
Generate a password for the same username used for login, select bcrypt, and download the file.

**Step 8:**  
Navigate back to the server directory:
```
C:\Program Files (x86)\Go Server\Users
```

**Step 9:**  
Create a new text file and paste the generated password value into it. Save and exit.

**Step 10:**  
Access the GOCD dashboard: `http://<GOCD_SERVER_IP>:<PORT>/go/admin/security/auth_configs`

**Step 11:**  
Navigate to the authentication configuration.

**Step 12:**  
Click on "Add" to create a new authentication configuration.

**Step 13:**  
Fill in the details as shown below:
```
Name: <Auth_Config_Name>
Plugin ID: Password File
Options: Path=<Path_to_password_file_created>
```

**Step 14:**  
Done! Test the credentials by logging in incognito mode.
