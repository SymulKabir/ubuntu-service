### Create Flask application 
Go to you application folder locaiton
```bash
cd /var/website/simple-api
```

Create app.py file and pest this code:

```bash
from flask import Flask

app = Flask(__name__)

@app.route("/")
def hello():
    return "Hello World"

if __name__ == "__main__":
    app.run(debug=True)

```

### Install vertual environment package

```bash
sudo apt update
sudo apt install python3-venv -y
```

### Create and activate virtual environment 

```bash
python3 -m venv venv
source venv/bin/activate
```
After activation, your prompt will look like:

```bash
(venv) root@ubuntuv24:/var/website/simple-api#
```

### Install required packages

```bash
pip install flask 
```

### Test test the app is working

```bash
python app.py
```
### Install and run Gunicorn

```bash
pip install gunicorn
```
Then run:
```bash
gunicorn --bind 0.0.0.0:5000 app:app
```
OR

```bash
gunicorn --workers 4 --bind 0.0.0.0:5000 app:app
```

### Deactive vertual environment

```bash
deactivate
```

### Use systemd service to keep Gunicorn running

```bash
[Unit]
Description=Gunicorn instance to serve simple-api
After=network.target

[Service]
User=root
Group=www-data
WorkingDirectory=/var/website/simple-api
Environment="PATH=/var/website/simple-api/venv/bin"
ExecStart=/var/website/simple-api/venv/bin/gunicorn --workers 4 --bind 0.0.0.0:5000 app:app

[Install]
WantedBy=multi-user.target

```
Enable and start it:

```bash
systemctl daemon-reload
systemctl enable simple-api
systemctl start simple-api
```



