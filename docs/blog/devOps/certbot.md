## set up certbot
sudo apt install certbot python3-certbot-nginx

sudo systemctl stop nginx

sudo certbot --nginx -d javaisdeadbyezio.io,

sudo certbot --nginx -d api.javaisdeadbyezio.io

sudo certbot renew --dry-run

sudo systemctl start nginx


## certbot is great, but it doesn't auto-renew.
## So we need to set up a cron job to do it for us.

but this is pretty well integrated with nginx, so it's not too bad.
