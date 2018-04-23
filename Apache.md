# Apache
## Config
```
/usr/local/etc/httpd/httpd.conf
```
## Create virtual host
1. Make sure the following is uncommented in `/usr/local/etc/httpd/httpd.conf`
    ```
    # Virtual hosts
    Include /usr/local/etc/httpd/extra/httpd-vhosts.conf # include this
    ```
1. Add this in `/usr/local/etc/httpd/extra`
    ```
    <VirtualHost *:80>
        ServerName example.test
        ServerAlias www.example.test
        DocumentRoot "/Users/ezzat/Sites/example.test/public"
        ErrorLog "/Users/ezzat/Sites/example.test/example.test-error_log"
        CustomLog "/Users/ezzat/Sites/example.test/example.test-access_log" common
            <Directory "/Users/ezzat/Sites/example.test">
                Options Indexes FollowSymLinks
                AllowOverride All
                Order allow,deny
                Allow from all
            </Directory>
    </VirtualHost>
    ```
1. Add this in host file
    ```
    127.0.0.1		example.test
    ```
1.  Restart Apache
    ```
    sudo apachectl stop
    sudo apachectl start
    ```
## Nice sites
1. https://getgrav.org/blog/macos-sierra-apache-multiple-php-versions

