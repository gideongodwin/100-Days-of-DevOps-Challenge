## Day 20 - Configure Nginx + PHP-FPM Using Unix Sock

## Task Details:

The Nautilus application development team is planning to launch a new PHP-based application, which they want to deploy on Nautilus infra in Stratos DC. 
The development team had a meeting with the production support team and they have shared some requirements regarding the infrastructure. Below are the requirements they shared:

- Install `nginx` on `app server 3` , configure it to use port `8094` and its document root should be `/var/www/html`

- Install `php-fpm` version `8.1` on `app server 3` it must use the unix socket `/var/run/php-fpm/default.sock` (create the parent directories if don't exist).

- Configure `php-fpm` and `nginx` to work together.

- Once configured correctly, you can test the website using `curl http://stapp03:8094/index.php` command from jump host.

  > We have copied two files, `index.php` and `info.php`, under `/var/www/html` as part of the PHP-based application setup. Please do not modify these files

## Steps

1. SSH into app server 3 and switch to root user
   ```
   ssh banner@stapp03
   ```
   ```
   sudo -i
   ```

2. Install nginx
   ```
   dnf install nginx -y
   ```

3. Install `php-fpm` 8.1
    ```
    # Install the EPEL and Remi repositories.
    dnf install https://dl.fedoraproject.org/pub/epel/epel-release-latest-9.noarch.rpm -y
    dnf install https://rpms.remirepo.net/enterprise/remi-release-9.rpm -y
    
    # Enable the CodeReady Builder (CRB) repository
    crb enable
    
    # Enable PHP 8.1 stream and install
    dnf module reset php -y
    dnf module enable php:remi-8.1 -y
    dnf install php php-cli php-fpm -y
    
    # Verify the installation
    php -v
    ```

4. Configure  to use port `8094` and Update the server block to configure `php-fpm` socket
    ```
    vi /etc/nginx/nginx.conf
    ```

5. Configure nginx to use port `8094` and Update the server block to configure `php-fpm` socket
    ```
    server {
        listen 8094;
        listen [::]:8094;
        server_name _;
    
        root /var/www/html;
        index index.html index.php info.php;
    
        include /etc/nginx/default.d/*.conf;
    
        location / {
            try_files $uri $uri/ =404;
        }
    
        error_page 404 /404.html;
        location = /404.html {}
    
        error_page 500 502 503 504 /50x.html;
        location = /50x.html {}
    
        location ~ \.php$ {
            fastcgi_pass unix:/var/run/php-fpm/default.sock;
            fastcgi_index index.php;
            include fastcgi.conf;
        }
    }
    ```

6. Check nginx configuration, then start both service
   ```
   nginx -t
   systemctl enable --now php-fpm
   systemctl enable --now nginx
   ```

7. Test from the Jump Host:
   ```
   exit
   exit
   curl http://stapp03:8094/index.php
   ```
