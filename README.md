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
