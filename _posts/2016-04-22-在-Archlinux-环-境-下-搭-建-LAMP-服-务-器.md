---
layout: post
---
# LAMP in Archlinux
*****

## 0. 简介：

LAMP即**Linux+Apache+Mysql+Php**构成的网络服务器环境。当然，各个软件都有相应的替代品，如Nginx、Mariadb等等。

## 1.安装

几乎所有的软件都存在于Archlinux的official repo中，直接安装就可以：

	pacman -S php php-cgi mariadb apache php-apache 

* Sun被Oracle收购之后，大部分linux发行版不在支持mysql，而改为mariadb，所以 mysql现在已经不在official repo中了，不过可以在AUR中下载：`yaourt -S mysql`,两者操作基本一致。	
* php-cgi和php-apache都是php配合apache使用的软件包。php-cgi为[cgi接口](https://www.w3.org/CGI/)。	


*****
## 2.配置和使用 

### 2.1 [php](https://wiki.archlinux.org/index.php/PHP)
 
###### 最主要的配置文件是 */etc/php/php.ini*

*	`date.timezone=Asia/Shanghai`
	`display_error=on` 
	
	在php.ini中修改以上两行来设置时区和启用错误提示功能。

*	`extension=mysql.so`  `extension=pdo_mysql.so`

	取消以上两行的注释来启用mysql接口插件PDO。
***

### 2.2 [Apache](https://wiki.archlinux.org/index.php/Apache_HTTP_Server)

###### Apache 的配置文件是 */etc/httpd/conf/http.conf*
* 设置默认账户和监听端口: `User http` `Listen 80`
* 设置Apache开机启动: `sudo systemctl enable httpd.service`
* 启动 Apache: `sudo systemctl start httpd.service`

* 更改网站的存放位置（默认存放位置为/srv/http） 

	更改 http.conf 中的设置: `DocumetRoot "/path/to/dir"`  `<Directory "/path/to/dir">`  `Require all granted`

	并确认新更改的目录是具有被用户 http 访问的权限（x权限）`chmod o+x /path/to/dir`

* 启用php 设置:  

```

	1. 注释掉：#LoadModule mpm_event_module modules/mod_mpm_evert.so
	    取消注释：LoadModule mpm_event_module modules/mod_mpm_prefork.so

	2. 添加 LoadModule php7_module modules/libphp7.so 在 mod_dir.so 之后。

	3. 添加 Include conf/extra/php7_module.conf 在 Include list 结尾的地方。

```

###### 注意任何更改之后都要重启 httpd.service 才能生效。

***

### 2.3  [Mysql/MariaDB](https://wiki.archlinux.org/index.php?title=MySQL&redirect=no)

* 设置用户、目录等信息：`mysql_install_db --user=mysql --basedir=/usr --datadir=/var/lib/mysql`

* 启用mysql服务：`sudo systemctl enable mysqld.service`	`sudo systemctl start mysqld.service`

* 使用前的设置：`mysql_secure_installation` 按照提示设置密码（默认密码为空）、数据库等等信息
