### GENERATE SELF-SIGNED FOR VHOST
```
$ sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/apache-selfsigned.key -out /etc/ssl/certs/apache-selfsigned.crt

//Setup Vhost
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
```
