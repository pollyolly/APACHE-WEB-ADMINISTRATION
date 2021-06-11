### SETUP REMOTE LOCALHOST DEVELOPMENT
```
/* You need this to avoid changing the domain name in the Wordpress Database */
//Generate Selfsigned Certificate
$ sudo a2enmod rewrite
$ sudo a2enmod ssl
$ sudo a2enmod headers
$ sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/ssl/private/apache-selfsigned.key -out /etc/ssl/certs/apache-selfsigned.crt

//Setup webapp Vhost
<VirtualHost *:80>
        ServerName google.com
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

//In Windows OS hosts
10.40.23.789 google.com
202.40.23.789 google.com

//In CMD
ipconfig/flushdns

```
