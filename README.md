# wings
You can run this software on any machine to get that machine to communicate with the panel.
## Installation

1.  **Create the configuration directory:**
    ```bash
    sudo mkdir -p /etc/phoenixpanel
    ```

2.  **Download the latest release:**
    ```bash
    curl -L -o /usr/local/bin/wings "https://github.com/phoenixpanel/wings/releases/latest/download/wings_linux_$([[ "$(uname -m)" == "x86_64" ]] && echo "amd64" || echo "arm64")"
    ```

3.  **Make the binary executable:**
    ```bash
    sudo chmod u+x /usr/local/bin/wings
    ```

4.  **Configure Wings:**
    You will need to create a `config.yml` file in `/etc/phoenixpanel`. Refer to the panel documentation for configuration details.

5.  **Run Wings:**
    ```bash
    sudo /usr/local/bin/wings
    ```
## Running as a Service (systemd)

To run Wings as a background service using systemd:

1.  **Create the systemd service file:**
    Create a file named `/etc/systemd/system/wings.service` with the following content:

    ```ini
    [Unit]
    Description=PhoenixPanel Wings Daemon
    After=docker.service
    Requires=docker.service
    PartOf=docker.service

    [Service]
    User=root
    WorkingDirectory=/etc/phoenixpanel
    LimitNOFILE=4096
    PIDFile=/var/run/wings/daemon.pid
    ExecStart=/usr/local/bin/wings
    Restart=on-failure
    StartLimitInterval=180
    StartLimitBurst=30
    RestartSec=5s

    [Install]
    WantedBy=multi-user.target
    ```

2.  **Create the PID directory:**
    ```bash
    sudo mkdir -p /var/run/wings
    ```

3.  **Enable and start the service:**
    ```bash
    sudo systemctl enable --now wings.service
    ```

4.  **Check the status:**
    ```bash
    sudo systemctl status wings.service
    ```
