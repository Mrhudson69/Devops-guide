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