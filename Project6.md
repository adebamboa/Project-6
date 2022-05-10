## WEB SOLUTION WITH WORDPRESS

**WEB SERVER**

`lsblk`

![LSBLK.JPG](./images/WBS%20LSBLK.jpg)

`df -h`

![DF-H.G](./images/WBS%20DF-H.jpg)

`sudo gdisk /dev/xvdf`

`sudo gdisk /dev/xvdg`

`sudo gdisk /dev/xvdh`

`lsblk`

![NEWLY AVAILABLE PARTION.J](./images/WBS%20NEWLY%20AVAILABLE%20PARTION.jpg)

`sudo yum install lvm2`

`sudo lvmdiskscan`

`sudo pvcreate /dev/xvdf1`

`sudo pvcreate /dev/xvdg1`

`sudo pvcreate /dev/xvdh1`

`sudo pvs`

![PHYSICAL VOLUME.PNG](./images/WBS%20Pyhsical%20Volume%20created..jpg)

`sudo vgcreate webdata-vg /dev/xvdh1 /dev/xvdg1 /dev/xvdf1`

`sudo vgs`

![WBS.JPG](./images/WBS%20VGS.jpg)

`sudo lvcreate -n apps-lv -L 14G webdata-vg`

`sudo lvcreate -n logs-lv -L 14G webdata-vg`

`sudo lvs`

![LVGS.JPG](./images/WBS%20LVS.jpg)

`sudo lsblk `

![WHOLESETUP.JPG](./images/DTS%20WHOLE%20SET%20UP%20WORKING%20FINE.jpg)

`sudo mkfs -t ext4 /dev/webdata-vg/apps-lv`

`sudo mkfs -t ext4 /dev/webdata-vg/logs-lv`

`sudo mkdir -p /var/www/html`

`sudo mkdir -p /home/recovery/logs`

`sudo mount /dev/webdata-vg/apps-lv /var/www/html/`

`sudo rsync -av /var/log/. /home/recovery/logs/`

`sudo mount /dev/webdata-vg/logs-lv /var/log`

`sudo rsync -av /home/recovery/logs/. /var/log`

`sudo blkid`

![BLKID.JPG](./images/DTS%20BLKID%20.jpg)

`sudo vi /etc/fstab`

![FSTAB.JPG](./images/WBS%20UPDATED%20FSTAB.jpg)

`sudo mount -a`

`sudo systemctl daemon-reload`

`df -h`

![SETUP.JPG](./images/WBS%20SET%20UP%20AND%20RUNNING.jpg)

`sudo yum -y update`

`sudo yum -y install wget httpd php php-mysqlnd php-fpm php-json`

`sudo systemctl enable httpd`

`sudo systemctl start httpd`

`sudo yum install https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm`
`sudo yum install yum-utils http://rpms.remirepo.net/enterprise/remi-release-8.rpm`
`sudo yum module list php`
`sudo yum module reset php`
`sudo yum module enable php:remi-7.4`
`sudo yum install php php-opcache php-gd php-curl php-mysqlnd`
`sudo systemctl start php-fpm`
`sudo systemctl enable php-fpm`
`setsebool -P httpd_execmem 1`

`sudo systemctl restart httpd`

`mkdir wordpress`
`cd   wordpress`
`sudo wget http://wordpress.org/latest.tar.gz`
`sudo tar xzvf latest.tar.gz`
`sudo rm -rf latest.tar.gz`
`cp wordpress/wp-config-sample.php wordpress/wp-config.php`
`cp -R wordpress /var/www/html/`

`sudo chown -R apache:apache /var/www/html/wordpress`
`sudo chcon -t httpd_sys_rw_content_t /var/www/html/wordpress -R`
`sudo setsebool -P httpd_can_network_connect=1`

`sudo yum install mysql`

`sudo mysql -u admin -p -h <DB-Server-Private-IP-address>`

`SHOW DATABASES;`

![SHOWDATABASE.JPG](./images/WBS%20SHOW%20DATABASES%3B.jpg)

**DATABASE SERVER**

`lsblk`

![DISK ATTACHED.JPG](./images/DTS%20DISK%20ATTCHED..jpg)

`df -h`

![DF-H.JPG](./images/DTS%20DF%20-H.jpg)

`sudo gdisk /dev/xvdf`

`sudo gdisk /dev/xvdg`

`suso gdisk /dev/xvdh`

`sudo lvmdiskscan`

![AVAILABLE PARTION.JPG](./images/DTS%20Available%20partion.jpg)

` sudo yum install lvm2 -y`

`sudo pvcreate /dev/xvdf1 /dev/xvdg1 /dev/xvdh1`

`sudo pvs`

![PVCREATE.JPG](./images/DTS%20PVCREATE.jpg)

`sudo vgcreate vg-database /dev/xvdf1 /dev/xvdg1 /dev/xvdh1`

`sudo vgs`

![VGS.JPG](./images/DTS%20VGS%20.jpg)

`sudo lvcreate -n db-lv -L 20G vg-database`

`sudo lvs`

![LVG.JPG](./images/DTS%20LVG.jpg)

`sudo mkdir /db`

`sudo mkfs.ext4 /dev/vg-database/db-lv`

`sudo mount /dev/vg-database/db-lv /db`

` df -h`

![MOUNTED.JPG](./images/DTS%20MOUNTED%20.jpg)

`sudo blkid`

![BLKID.JPG](./images/DTS%20BLKID%20.jpg)

`sudo vi /etc/fstab`

`sudo mount -a`

`sudo systemctl daemon-reload`

`df -h`

![WHOLE SET-UP.JPG](./images/DTS%20WHOLE%20SET%20UP%20WORKING%20FINE.jpg)

`sudo yum update -y`

`sudo yum install mysql-server -y`

`sudo systemctl start mysqld`

`sudo systemctl enable mysqld`

` sudo mysql -u root -p`

`mysql> create database wordpress;`

`mysql> show databases;`

![SHOWDATABASES.JPG](./images/DTS%20SHOW%20DATABASES%3B.jpg)

`mysql> CREATE USER 'wordpress'@'%' IDENTIFIED WITH mysql_native_password BY 'wordpress';`

`mysql> GRANT ALL PRIVILEGES ON *.* TO 'wordpress'@'%' WITH GRANT OPTION;`

`mysql> FLUSH PRIVILEGES;`

![SQL USERS.JPG](./images/DTS%20SQL%20USERS.jpg)

**WORDPRESS**

![APACHE.JPG](./images/WBS%20APACHE%20WEB%20PAGE.jpg)

![WORDPRESS.JPG](./images/WORD%20PRESS%20.PNG.jpg)

![WORDPRESS.JPG](./images/word%20press%20installed..jpg)


![WORDPRESS.JPG](./images/Welcome%20to%20WordPress.jpg)