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