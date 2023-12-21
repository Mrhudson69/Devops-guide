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