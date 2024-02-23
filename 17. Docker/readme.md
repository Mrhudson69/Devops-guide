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