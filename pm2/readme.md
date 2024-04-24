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
