# MySQL
## Login
```
mysql -u [username/root] -p
```
## Create user
```sql
CREATE USER 'ezzat'@'localhost' IDENTIFIED BY 'password';
```
## Sufficient user privileges for Wordpress
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

https://wordpress.stackexchange.com/questions/6424/mysql-database-user-which-privileges-are-needed