### Go to applicaiton directory

```bash
cd /var/python_apps/simple-api
```

### Create and activate vertula environment

```bash
apt install python3.10-venv  #Install venv package if not installed
python3 -m venv .venv
source .venv/bin/activate
```
You will show like this in terminal:

```bash
(.venv) root@micple:/var/python_apps/simple-api#
```

### Install Django cli environment

```bash
pip install Django
```
### Create Django application

```bash
django-admin startproject myApp
```
### Go to created app directory

```bash
cd myApp
```

### Run this command check the application 

```bash
python manage.py runserver
```
### Install Gunicorn

```bash
pip install gunicorn
```

### Run the application with Gunicorn

```bash
../.venv/bin/gunicorn --bind 0.0.0.0:8000 myApp.wsgi:application

# OR
../.venv/bin/gunicorn --workers 3 --bind 0.0.0.0:8000 myApp.wsgi:application
```
### Deactive vertual environment

```bash
deactivate
```
### Create a systemd service file

```bash
nano /etc/systemd/system/myApp.service
```
Then:

```bash
[Unit]
Description=Gunicorn instance to serve Django myApp
After=network.target

[Service]
User=root
Group=www-data
WorkingDirectory=/var/python_apps/simple-api/myApp
ExecStart=/var/python_apps/simple-api/.venv/bin/gunicorn \
          --workers 3 \
          --bind 0.0.0.0:8000 \
          myApp.wsgi:application

Restart=always

[Install]
WantedBy=multi-user.target

```

### Reload systemd and enable service

```bash
systemctl daemon-reload
systemctl enable myApp
systemctl start myApp
```

### Check status

```bash
systemctl status myApp
```



