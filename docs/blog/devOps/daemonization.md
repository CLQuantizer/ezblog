## Set up git credentials

git config --global user.name "your_github_username"
git config --global user.password "your_github_token or password"

## nginx config for reverse proxy 
server {
    # Existing config 

    server_name javaisdeadbyezio.io;

    location / {
        try_files $uri $uri/ =404; 
    }

    location /api/ {
        proxy_pass http://localhost:8000;
        proxy_set_header Host $host;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for; 
        proxy_set_header X-Forwarded-Proto $scheme;
    }

    # SSL config
}

then: sudo systemctl restart nginx

## Then let's set up the systemd service
cd /etc/systemd/system
sudo touch javaisdeadbyezio.service

## say it is a fastapi service
[Unit]
Description=My FastAPI App
After=network.target

[Service]
Type=simple
User=maxTrump
WorkingDirectory=/root/[javaisdeadbyezio.io]
ExecStart=/root/.local/bin/poetry run uvicorn main:app
Restart=on-failure


