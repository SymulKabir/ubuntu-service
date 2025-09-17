### 1. Create Flask application 
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

### 2. Install vertual environment package

```bash
sudo apt update
sudo apt install python3-venv -y
```

### 3. Create and activate virtual environment 

```bash
python3 -m venv venv
source venv/bin/activate
```
After activation, your prompt will look like:

```bash
(venv) root@ubuntuv24:/var/website/simple-api#
```

### 4. Install required packages

```bash
pip install flask 
```

### 5. Test test the app is working

```bash
python app.py
```
### 6. Install and run Gunicorn

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
### 7. Use systemd service to keep Gunicorn running

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



