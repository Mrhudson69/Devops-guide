# Elasticsearch Exporter Installation Guide

This guide provides step-by-step instructions for installing and setting up the Elasticsearch Exporter for Prometheus. The Elasticsearch Exporter is a tool that enables Prometheus to scrape and collect metrics from an Elasticsearch instance.

## Installation of Elasticsearch Exporter

1. **Download the Elasticsearch Exporter**
    ```sh
    wget https://github.com/prometheus-community/elasticsearch_exporter/releases/download/v1.7.0/elasticsearch_exporter-1.7.0.linux-amd64.tar.gz
    ```
    This command downloads the specified version (`v1.7.0`) of the Elasticsearch Exporter from the official GitHub releases page.

2. **Extract the Downloaded Archive**
    ```sh
    tar -xvzf elasticsearch_exporter-1.7.0.linux-amd64.tar.gz 
    ```
    This command extracts the contents of the downloaded tar.gz file.

3. **Navigate to the Extracted Directory**
    ```sh
    cd elasticsearch_exporter-1.7.0.linux-amd64
    ```
    This command changes the current directory to the directory containing the extracted files.

4. **Copy the Elasticsearch Exporter Binary to a System Path**
    ```sh
    cp elasticsearch_exporter /usr/local/bin/
    ```
    This command copies the `elasticsearch_exporter` binary to `/usr/local/bin/`, making it accessible system-wide.

5. **Create a System User for Elasticsearch Exporter**
    ```sh
    useradd --no-create-home --shell /bin/false elastic_search
    ```
    This command creates a new system user named `elastic_search` without a home directory and with no login shell. This user will run the Elasticsearch Exporter.

6. **Set Ownership of the Elasticsearch Exporter Binary**
    ```sh
    chown elastic_search:elastic_search /usr/local/bin/elasticsearch_exporter 
    ```
    This command changes the ownership of the `elasticsearch_exporter` binary to the `elastic_search` user and group.

7. **Create a Systemd Service File for Elasticsearch Exporter**
    ```sh
    nano /etc/systemd/system/elasticsearch_exporter.service
    ```
    This command opens a text editor to create a new service file for the Elasticsearch Exporter.

    Paste the following configuration into the file:
    ```
    [Unit]
    Description=Prometheus ES_exporter
    After=local-fs.target network-online.target network.target
    Wants=local-fs.target network-online.target network.target

    [Service]
    User=elastic_search
    Nice=10
    ExecStart=/usr/local/bin/elasticsearch_exporter --es.uri=http://elastic_search@localhost:9200 --es.all --es.indices --es.timeout 20s
    ExecStop=/usr/bin/killall elasticsearch_exporter

    [Install]
    WantedBy=default.target
    ```

    - **[Unit]**: Defines metadata and dependencies.
      - `Description`: A short description of the service.
      - `After`: Specifies the order of service start-up.
      - `Wants`: Indicates the dependencies that should be started alongside.

    - **[Service]**: Describes the service runtime parameters.
      - `User`: Specifies the user to run the service (`elastic_search`).
      - `Nice`: Adjusts the scheduling priority of the service.
      - `ExecStart`: Command to start the service with options for Elasticsearch URI, metrics to scrape, and timeout.
      - `ExecStop`: Command to stop the service.

    - **[Install]**: Defines how the service should be installed.
      - `WantedBy`: Specifies the target unit to pull in this service.

8. **Reload Systemd Manager Configuration**
    ```sh
    systemctl daemon-reload
    ```
    This command reloads the systemd manager configuration to recognize the new service file.

9. **Enable Elasticsearch Exporter Service**
    ```sh
    systemctl enable elasticsearch_exporter
    ```
    This command enables the Elasticsearch Exporter service to start on boot.

10. **Start Elasticsearch Exporter Service**
    ```sh
    systemctl start elasticsearch_exporter
    ```
    This command starts the Elasticsearch Exporter service immediately.

11. **Check the Status of Elasticsearch Exporter Service**
    ```sh
    systemctl status elasticsearch_exporter
    ```
    This command checks and displays the status of the Elasticsearch Exporter service to ensure it is running correctly.

By following these steps, you will have the Elasticsearch Exporter installed, configured, and running as a systemd service on your system. This setup allows Prometheus to scrape metrics from your Elasticsearch instance.