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