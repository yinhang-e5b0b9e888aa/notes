
# nextcloud

# install nextcloud on Linux Mint 18.3

1. 安装nginx
  1. apt-get install nginx
  2. (如果开了防火墙) ufw allow 80/tcp
  3. 配置ssl
    1. mkdir /etc/nginx/cert
    2. cp 证书.key 证书.pem to /etc/nginx/cert
    3. vi /etc/nginx/sites-available/<域名>
       内容:
   ```
   server {
       listen 63443;
       listen [::]:63443;
       server_name <域名>;
       ssl on;
       ssl_certificate /etc/nginx/cert/<证书>.pem;
       ssl_certificate_key /etc/nginx/cert/<证书>.key;
       ssl_session_timeout 5m;
       ssl_ciphers ECDHE-RSA-AES128-GCM-SHA256:ECDHE:ECDH:AES:HIGH:!NULL:!aNULL:!MD5:!ADH:!RC4;
       ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
       ssl_prefer_server_ciphers on;

            access_log /var/log/nginx/${server_name}_access.log;

            location / {
            proxy_redirect off;
            proxy_pass http://127.0.0.1:8755;
            proxy_set_header Host $http_host;
            add_header Strict-Transport-Security "max-age=15552000; includeSubDomains; preload" always;
            client_max_body_size 128M;
        }

            location = /.htaccess {
            return 404;
        }
    }
    ```
  4. ln -s /etc/nginx/sites-available/<域名> /etc/nginx/sites-enabled/<域名>
  5. rm /etc/nginx/sites-enabled/default
  6. nginx -t
  7. systemctl restart nginx

2. 安装docker
  1. apt-get install apt-transport-https ca-certificates curl software-properties-common
  2. curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
  3. sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu xenial stable"
  4. apt-get update
  5. apt-get install docker-ce

3. 安装docker-compose
  1. curl -L https://github.com/docker/compose/releases/download/1.21.2/docker-compose-$(uname -s)-$(uname -m) -o /usr/local/bin/docker-compose
  2. chmod +x /usr/local/bin/docker-compose
  
4. 安装nextcloud
  1. sudo docker network create ncnet
  2. vi docker-compose.yml
     内容:
  ```
  version: '2'
  services:
    db:
      container_name: cloud_db
      image: mariadb
      volumes:
        - /cloud/db:/var/lib/mysql"
      restart: always
      environment:
        - MYSQL_ROOT_PASSWORD=<mysql root 密码>
        - MYSQL_DATABASE=nextcloud
        - MYSQL_USER=nextcloud
        - MYSQL_PASSWORD=<mysql user 密码>
    app:
      container_name: cloud_app
      depends_on:
        - db
      image: nextcloud
      volumes:
        - /cloud/config:/var/www/html/config
        - /cloud/data:/var/www/html/data
        - /cloud/apps:/var/www/html/custom_apps
      environment:
        - MYSQL_DATABASE=nextcloud
        - MYSQL_USER=nextcloud
        - MYSQL_PASSWORD=<mysql user 密码>
        - MYSQL_HOST=db
      links:
        - db
      ports:
        - "8755:80"
      restart: always
  networks:
    default:
      external:
        name: ncnet
  ``` 
  3. docker-compose up -d

5. 开启两部验证
6. 直接更新文件系统目录之后同步到nextcloud:   docker exec --user www-data cloud_app php occ files:scan --all -v
或者：    docker-compose exec --user www-data cloud_app php occ files:scan --all -v
