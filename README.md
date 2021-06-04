### SETUP REMOTE LOCALHOST DEVELOPMENT
```
//Generate Selfsigned Certificate
$ sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/apache-selfsigned.key -out /etc/ssl/certs/apache-selfsigned.crt

//Setup webapp Vhost
<VirtualHost *:80>
        ServerName ilc.upd.edu.ph
        DocumentRoot /var/www/html/webapp
</VirtualHost>
<IfModule mod_ssl.c>
<VirtualHost *:443>
        ServerName google.com
        ServerAlias google.com *.google.com
        DocumentRoot /var/www/html/webapp/
        #Redirect permanent / https://yahoo.com
        <Directory /var/www/html/webapp>
            Options -Indexes +FollowSymlinks +MultiViews
            AllowOverride All
            Require all granted
        </Directory>
        ErrorLog ${APACHE_LOG_DIR}/dev_webapp_error.log
        CustomLog ${APACHE_LOG_DIR}/dev_webapp_access.log combined

        SSLEngine on

        SSLCertificateFile      /etc/ssl/certs/apache-selfsigned.crt
        SSLCertificateKeyFile /etc/ssl/private/apache-selfsigned.key

</VirtualHost>
</IfModule>

//In Windows hosts
remote-server-publicip-address google.com
remote-server-privateip-address google.com

//In CMD
ipconfig/flushdns

```
