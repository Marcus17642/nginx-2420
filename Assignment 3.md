


# Install stuff

do this to install vim

Vim is a text editor that will allow you to edit text in a file
```
sudo pacman -S vim
```


do this to install nginx
nginx hosts your webserver so you'll need to install it
```
sudo pacman -S nginx

#enables nginx
sudo systemctl enable nginx
```

# Create paths

go to your root directory and make this directory. This will store your html file
```
mkdir -p web/html/nginx-2420

```



now go to /etc/nginx/
make this directory as we'll store the server block in this directory
```
mkdir available-sites
```

now cd available-sites


Now we will make the server block for the server

in /etc/nginx/available-sites

```
vim nginx-2420

```

write this in vim. Make sure to replace server_ip with your actual server_ip
```
server {

    listen 80;

    server_name server_ip;

  

    location / {

        root /web/html/nginx-2420;

        index index.html;

    }

}
```



because we're not putting the server block in nginx.conf we'll have to make a symbolic link


```

sudo mkdir /etc/nginx/sites-enabled
#make the sites enabled directory if you dont have a sites enabled directory

sudo ln -s /etc/nginx/sites-available/nginx-2420 /etc/nginx/sites-enabled/
#this make the symbolic link

```


Now you have to include sites enabled in the nginx.conf file

it should look like one of the pictures I uploaded in Github. Use that picture for reference

```
#it should kinda look like this but just look at #the picture
http {


	include /etc/nginx/sites-enabled/nginx-2420;
}

```

you can restart nginx

```
sudo systemctl restart nginx
```

you can test nginx to make sure it works with

```
sudo nginx -t
```


now make your html file if everything works

```
sudo vim /web/html/nginx-2420/index.html
```


put this in index.html file
```html
<!DOCTYPE html>

<html lang="en">

<head>

    <meta charset="UTF-8">

    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <title>2420</title>

    <style>

        * {

            color: #db4b4b;

            background: #16161e;

        }

        body {

            display: flex;

            align-items: center;

            justify-content: center;

            height: 100vh;

            margin: 0;

        }

        h1 {

            text-align: center;

            font-family: sans-serif;

        }

    </style>

</head>

<body>

    <h1>All your base are belong to us</h1>

</body>

</html>

```



now try visiting your website by typing your ip address in the browser

