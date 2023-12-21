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