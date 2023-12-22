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