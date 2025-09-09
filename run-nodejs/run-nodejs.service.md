
### Step 1. Set up NodeJS project

```bash
git clone ssh://repository_link myapp
cd myapp
npm install
```

### Step 2. Create a service file

```bash
sudo nano /etc/systemd/system/myapp.service
```

Add this config (adjust paths and names): 

```bash
[Unit]
Description=My Node.js App
After=network.target

[Service]
ExecStart=/usr/bin/node /var/www/your-node-project/index.js
WorkingDirectory=/var/www/your-node-project
Restart=always
User=nobody
Environment=PORT=3000 NODE_ENV=production

[Install]
WantedBy=multi-user.target
```

### Step 3. Enable & Start Service

```bash
sudo systemctl daemon-reload
sudo systemctl enable myapp
sudo systemctl start myapp
```

Check status:

```bash
sudo systemctl status myapp
```

Check status:

```bash
journalctl -u myapp -f
```
