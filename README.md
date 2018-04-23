# Docs

This repo contains my personal snippets, notes, and documentations. Some snippets below might not work in your environment.

## Apache
### Config
```
/usr/local/etc/httpd/httpd.conf
```
### Create virtual host
- Make sure the following is uncommented in `/usr/local/etc/httpd/httpd.conf`
```
# Virtual hosts
Include /usr/local/etc/httpd/extra/httpd-vhosts.conf # include this
```

- Add this in `/usr/local/etc/httpd/extra`
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

- Add this in host file
```
127.0.0.1		example.test
```

- Restart Apache
```
sudo apachectl stop
sudo apachectl start
```

### Nice sites
- https://getgrav.org/blog/macos-sierra-apache-multiple-php-versions

## Node

### Update all locals node modules
```
ncu
ncu -u
```

### Update all global node modules
```
ncu -g
npm install -g [package1 package2 …]
```

### Upgrade node to the latest LTS
```
sudo npm cache clean -f
sudo npm install -g n
sudo n 4.4.2
```

### Running a project-local bin
```
npm i -D webpack		# install
npx webpack			    # run
```

## MySQL
### Login
```
mysql -u [username/root] -p

```
### Create user
```
CREATE USER 'ezzat'@'localhost' IDENTIFIED BY 'password';

```
### Sufficient user privileges for Wordpress
https://wordpress.stackexchange.com/questions/6424/mysql-database-user-which-privileges-are-needed
```
I've found at least one article that claims the MySQL user only needs:

SELECT
INSERT
UPDATE

Digging deeper, I found that in order to operate fully (automated updates, plug-in installation/uninstallation, etc.), WordPress requires some additional permissions:

DELETE
CREATE TABLE
DROP TABLE
ALTER (for updates)

Also, not referenced but it makes sense:

INDEX

```
Make sure the database previleges are also on.

## Node

### Good Plugins

- Easy WP SMTP
