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