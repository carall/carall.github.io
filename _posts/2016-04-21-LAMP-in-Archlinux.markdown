---
layout: post
---
# LAMP in Archlinux
*****
## 1. installation

	pacman -S php php-cgi mysql apache php-apache 

	pacman -Ss php-

*****
## 2. configuration
#### 2.1 php
* edit or uncomment the phrases below in */etc/php/php.ini*: 

	`date.timezone=Asia/Shanghai` & `display_error=on` & `extension=mysql.so` & `extension=pdo_mysql.so`
***

#### 2.2 Apache

* */etc/httpd/conf/http.conf*:`User http`&`Listen 80`
* `sudo systemctl enable httpd.service` and `sudo systemctl start httpd.service`

* change web dir if necessary like this:

	`DocumetRoot "/path/to/dir"` & `<Directory "/path/to/dir">` & `Require all granted` in http.conf,and then `chmod o+x /path/to/dir`

* **php configure**:  */etc/httpd/conf/httpd.conf*


	1. `#LoadModule mpm_event_module modules/mod_mpm_evert.so`& `LoadModule mpm_event_module modules/mod_mpm_prefork.so`

	2. `LoadModule php7_module modules/libphp7.so` **after** `mod_dir.so`

	3. `Include conf/extra/php7_module.conf` **end of** `Include` list

***
#### 2.3. Mysql/MariaDB

Almost nothing to configue,but see [here](https://wiki.archlinux.org/index.php?title=MySQL&redirect=no) for usage
