# Prepare Fedora Server 38 for use as Nginx Web Server.

https://docs.fedoraproject.org/en-US/fedora-server/virtualization/vm-install-diskimg-fedoraserver/

## SELinux
First you'll need to disable SELinux.
Edit `/etc/selinux/config` and revert to "permissive" behavior.
```
SELINUX=permissive
```
Then run this command:
```
sudo setenforce 0
```



## Install Required Software
Now you'll need to install the necessary components.
```
sudo dnf install nginx php-fpm php-mysqlnd mariadb-server php-pear php-devel redis phpmyadmin
```



## Disable Apache (if enabled)
```
sudo systemctl disable httpd.service
sudo systemctl stop httpd.service
```


## Enable Services
```
sudo systemctl enable nginx.service php-fpm.service mariadb.service redis.service
sudo systemctl start nginx.service php-fpm.service mariadb.service redis.service
```


## Open Firewall Ports
```
sudo firewall-cmd --permanent --add-service=http
sudo firewall-cmd --permanent --add-service=https
sudo firewall-cmd --reload
```
