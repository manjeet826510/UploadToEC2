# UploadToEC2

manje@Manjeet_PC MINGW64 ~
$ cd Downloads/

manje@Manjeet_PC MINGW64 ~/Downloads
$ ssh -i "keyonemart.pem" ec2-user@ec2-xxxxxxxx.ap-south-1.compute.amazonaws.com

[ec2-user@ip-172-31-10-178 ~]$ sudo yum install nodejs

[ec2-user@ip-172-31-10-178 ~]$ sudo yum install npm

[ec2-user@ip-172-31-10-178 ~]$ sudo yum install git

[ec2-user@ip-172-31-10-178 ~]$ git clone https://github.com/manjeet826510/XXXX.git

[ec2-user@ip-172-31-10-178 ~]$ ls
XXXX

[ec2-user@ip-172-31-10-178 ~]$ cd OneMart/
[ec2-user@ip-172-31-10-178 OneMart]$ npm run build


[ec2-user@ip-172-31-10-178 OneMart]$ cd ..
[ec2-user@ip-172-31-10-178 ~]$ sudo yum install nginx

[ec2-user@ip-172-31-10-178 ~]$ sudo nano /etc/nginx/nginx.conf

http {
    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';

    access_log  /var/log/nginx/access.log  main;

    sendfile            on;
    tcp_nopush          on;
    keepalive_timeout   65;
    types_hash_max_size 4096;

    include             /etc/nginx/mime.types;
    default_type        application/octet-stream;

    # Load modular configuration files from the /etc/nginx/conf.d directory.
    # See http://nginx.org/en/docs/ngx_core_module.html#include
    # for more information.
    include /etc/nginx/conf.d/*.conf;

    server {
        listen       80;
        listen       [::]:80;
        server_name  _;
        root         /usr/share/nginx/html;

        # Load configuration files for the default server block.
        include /etc/nginx/default.d/*.conf;

        error_page 404 /404.html;
        location = /404.html {
        }

        error_page 500 502 503 504 /50x.html;
        location = /50x.html {
        }
    }

    server {
        listen 80;
        server_name xxxxx - ip address of ec2;  # Replace with your actual IP address or domain name, IP like 123.01.21.245 or domain name like onemart.com every time you change config file restart nginx

        location / {
            proxy_pass http://localhost:3000;  # Replace with the actual port of your Node.js backend
            proxy_http_version 1.1;
            proxy_set_header Upgrade $http_upgrade;
            proxy_set_header Connection 'upgrade';
            proxy_set_header Host $host;
            proxy_cache_bypass $http_upgrade;
        }
    }
}


[ec2-user@ip-172-31-10-178 ~]$ sudo service nginx restart

[ec2-user@ip-172-31-10-178 ~]$ cd OneMart/
[ec2-user@ip-172-31-10-178 OneMart]$ npm start

error =The `uri` parameter to `openUri()` must be a string, got "undefined". Make sure the first parameter to `mongoose.connect()` or `mongoose.createConnection()` is a string.
server is listening at :5000
 to overcome this error set mongodb uri as string "xxxxxxxxxxx" instead of process.env.MONGO_DB


 [ec2-user@ip-172-31-10-178 OneMart]$ npm start

> onemart@1.0.0 start
> node backend/server.js

undefined
server is listening at :5000
connected to db

hurray! The website is live on public ip provided by ec2




