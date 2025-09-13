# Auto-Start Docker Containers on Ubuntu Server Startup

This guide provides instructions on how to automatically start stopped Docker containers when an Ubuntu server boots up.

## Method 1: Using systemd Service (Recommended)

1. **Create a systemd service file**  
   Open a terminal and create a new service file:
   ```bash
   sudo nano /etc/systemd/system/docker-containers-autostart.service
   ```

2. **Add the following content:**
   ```ini
   [Unit]
   Description=Start stopped Docker containers on boot
   After=network.target docker.service
   Requires=docker.service

   [Service]
   Type=oneshot
   ExecStart=/bin/bash /bin/startserver.sh
   RemainAfterExit=true

   [Install]
   WantedBy=multi-user.target
   ```

   Replace `/path/to/start_stopped_containers.sh` with the actual path of your script.

3. **Reload systemd and enable the service:**
   ```bash
   sudo systemctl daemon-reload
   sudo systemctl enable docker-containers-autostart.service
   ```

4. **Test the service manually (optional):**
   ```bash
   sudo systemctl start docker-containers-autostart.service
   ```

5. **Reboot and check if it works:**
   ```bash
   sudo reboot
   ```
   After reboot, check the status:
   ```bash
   sudo systemctl status docker-containers-autostart.service
   ```

This method ensures that all stopped Docker containers are started automatically whenever the Ubuntu server boots up.

