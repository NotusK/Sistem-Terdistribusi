# Mencoba LXC

Nama    : Aditya Aulia Rohman  
NIM     : 1203210145

1. Download and Install "Ubuntu 22.04.3 LTS"
![Download Ubuntu!](Images/sister-local-Screenshot/1.png)

2. Enter your username and password

3. Now run this command to install the necessary packages

```
sudo apt install -y build-essential linux-headers-$(uname -r)
```

4. Change the ubuntu source list in to the code bellow

```
sudo nano /etc/apt/source.list"
```

```
deb http://archive.ubuntu.com/ubuntu/ jammy main restricted universe multiverse
deb-src http://archive.ubuntu.com/ubuntu/ jammy main restricted universe multiverse

deb http://archive.ubuntu.com/ubuntu/ jammy-updates main restricted universe multiverse
deb-src http://archive.ubuntu.com/ubuntu/ jammy-updates main restricted universe multiverse

deb http://archive.ubuntu.com/ubuntu/ jammy-security main restricted universe multiverse
deb-src http://archive.ubuntu.com/ubuntu/ jammy-security main restricted universe multiverse

deb http://archive.ubuntu.com/ubuntu/ jammy-backports main restricted universe multiverse
deb-src http://archive.ubuntu.com/ubuntu/ jammy-backports main restricted universe multiverse

deb http://archive.canonical.com/ubuntu/ jammy partner
deb-src http://archive.canonical.com/ubuntu/ jammy partner
```

5. Download and install all the latest packages

```
sudo apt update
```

```
sudo apt upgrade -y
```

6. Install lxc

```
sudo apt-get install lxc lxctl lxc-templates net-tools
```

7. Check the config and make sure everything in enabled

```
sudo lxc-checkconfig
```

![Check Config!](Images/sister-local-Screenshot/12.png)

8. Install nginx

```
sudo apt install nginx nginx-extras
```

9. Go to /etc/nginx/sites-enabled/ and copy paste default file as sister.local

```
cd /etc/nginx/sites-enabled
```

```
sudo cp default sister.local
```

10. Edit sister.local

```
sudo nano sister.local
```

```
server {
        listen 80;
        listen [::]:80;

        server_name sister.local;

        root/var/www/html;
        index index.html;

        location / {
            try_files $uri $uri/ =404
        }
}
```

11. Go to /var/www/html/ and copy paste index.nginx-debian.html as index.html

```
cd /var/www/html/
```

```
sudo cp index.nginx-debian.html index html
```

12. Edit index.html

```
sudo nano index.html
```

```
<!DOCTYPE html>
<html>
<head>
<title>Welcome to Sister!</title>
<style>
    body {
        width: 35em;
        margin: 0 auto;
        font-family: Tahoma, Verdana, Arial, sans-serif;
    }
</style>
</head>
<body>
<h1>Welcome to Sistem Terdistribusi Class!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>
<p>Aditya Aulia Rohman</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
```

13. Open notepad as administrator and open file called hosts located in "C:\Windows\System32\drivers\etc"

14. Add "127.0.0.1 sister.local" at the end of the text and save
![Edit Hosts!](Images/sister-local-Screenshot/19.png)

15. Try to open sister.local in a browser
![Try sister.local!](Images/sister-local-Screenshot/20.png)
