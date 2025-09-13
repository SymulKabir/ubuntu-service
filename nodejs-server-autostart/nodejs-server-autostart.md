# Auto-Start NodeJS Server on Ubuntu Server Startup

This guide provides instructions on how to automatically start NodeJS server when an Ubuntu server boots up.

1. **Create a systemd service file**  
   Open a terminal and create a new service file:
   ```bash
   sudo nano /etc/systemd/system/nodejs-server-autostart.service
   ```
2. **Check the NodeJS files location**  
   Open a terminal and create a new service file:
   ```bash
   which node
   ```

3. **Add the following content:**
   ```ini
   [Unit]
   Description=My Node.js App
   After=network.target

   [Service]
   #ExecStart=/usr/bin/node /var/www/myNodeApp/server.js
   ExecStart=/root/.nvm/versions/node/v14.17.3/bin/node /var/www/myNodeApp/index.js
   WorkingDirectory=/var/www/myNodeApp
   Restart=always
   User=root
   Environment=NODE_ENV=production
   StandardOutput=syslog
   StandardError=syslog
   SyslogIdentifier=myNodeApp

   [Install]
   WantedBy=multi-user.target
   ```

4. **Reload systemd and enable the service:**
   ```bash
   sudo systemctl daemon-reload
   sudo systemctl enable nodejs-server-autostart.service
   ```

5. **Test the service manually (optional):**
   ```bash
   sudo systemctl start nodejs-server-autostart.service
   ```

6. **Reboot and check if it works:**
   ```bash
   sudo reboot
   ```
   After reboot, check the status:
   ```bash
   sudo systemctl status nodejs-server-autostart.service
   ```

This method ensures that NodeJS server are started automatically whenever the Ubuntu server boots up.

