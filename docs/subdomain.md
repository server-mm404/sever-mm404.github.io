mm404.com မှ server-mm404.com ကို subdomain အနေနဲ့ တွဲသုံးမယ်ဆိုရင်DNS Configuration မှန်မှန်ပြုလုပ်ဖို့ လိုပါတယ်။


---

Step 1: Subdomain ကို DNS တွင် Set Up လုပ်ခြင်း

mm404.com ကို domain provider (Cloudflare, Namecheap, GoDaddy, etc.) မှာ register လုပ်ထားတယ်ဆိုပါစို့။

1. DNS Settings ထဲကို ဝင်ပါ။


2. New Record ထပ်ထည့်ပါ။

Type: A Record (သို့မဟုတ် CNAME)

Name: server (server-mm404.com မှ server ကို subdomain name အနေနဲ့ သုံးမယ်)

Value (IPv4 Address): သင့် server IP (e.g., 192.168.1.1 or DigitalOcean, AWS, etc.)

TTL: Automatic or 3600 (1 hour)




✔ Example:
| Type | Name    | Value (Server IP) | TTL  |
|------|--------|------------------|------|
| A  | server | 123.456.78.90  | Auto |


---

Step 2: Server-side Configuration

1. Apache/Nginx မှာ Virtual Host သတ်မှတ်ခြင်း (Linux Server)

🔹 Apache (Ubuntu)

sudo nano /etc/apache2/sites-available/server-mm404.conf

<VirtualHost *:80>
    ServerName server-mm404.com
    DocumentRoot /var/www/server-mm404
</VirtualHost>

sudo a2ensite server-mm404
sudo systemctl restart apache2

🔹 Nginx

sudo nano /etc/nginx/sites-available/server-mm404

server {
    listen 80;
    server_name server-mm404.com;
    root /var/www/server-mm404;
}

sudo ln -s /etc/nginx/sites-available/server-mm404 /etc/nginx/sites-enabled/
sudo systemctl restart nginx


---

Step 3: SSL Certificates (HTTPS Secure Setup)

Cloudflare သို့မဟုတ် Let's Encrypt SSL (Certbot) ကိုအသုံးပြုနိုင်ပါတယ်။

sudo apt install certbot python3-certbot-nginx
sudo certbot --nginx -d server-mm404.com


---

Step 4: Testing

1. server-mm404.com ကို browser ထဲမှာ လှမ်းကြည့်ပါ။


2. ping server-mm404.com command ဖြင့် DNS propagation စစ်ဆေးပါ။


3. Server logs (/var/log/nginx/access.log or /var/log/apache2/error.log) ကို ကြည့်ပါ။




---

✔ သင့်ရဲ့ mm404.com ထဲမှာ server-mm404.com ကို subdomain အနေနဲ့ တိုးချဲ့ပြီး တွဲသုံးနိုင်ပါပြီ။
❓ Backend Server, API, Database များထည့်သွင်းဖို့ လိုသေးလား?
