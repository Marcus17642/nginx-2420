### 1. Install UFW 

  
```bash
sudo pacman -Syu
#update

sudo pacman -S ufw
#install

sudo systemctl enable --now ufw.service
#enable 


sudo ufw status 
#to check the status of ufw
```

  

### 2. Configure Firewall

  

```bash
sudo ufw allow http 

sudo ufw allow https

sudo ufw enable

sudo ufw status

```


###  3. Transfer and Run the Backend Binary

transfer hello-server onto your digital ocean server

# put hello-server

```
sftp -i C:\Users\user\.ssh\do-key marcus@209.38.136.224
  
put hello-server
```

```
sudo mv /path to hello-server /usr/local/bin/
```


Create a new systemd service file:

  
```bash

sudo vim /etc/systemd/system/backend.service

```


Add the following content:

```systemd

[Unit]

Description=Backend Service

After=network.target

  

[Service]

ExecStart=/usr/local/bin/hello-server

Restart=always

  

[Install]

WantedBy=multi-user.target

```

  


# 4. start backend

```bash

sudo systemctl enable backend

sudo systemctl start backend



```



### 5. Configure Nginx as a Reverse Proxy

  

```bash

sudo vim /etc/nginx/sites-available/default

```

  

Add the following lines inside the `server` block:

  

```nginx
server {
    listen 80;
    server_name your_domain_or_IP;

location /hey {
    proxy_pass http://127.0.0.1:8080;

}


```

  
Test the Nginx configuration and reload Nginx:

```bash

sudo nginx -t

sudo systemctl reload nginx

```

  
### 6. Verify Configuration

  

Test your backend using curl or postman



  

