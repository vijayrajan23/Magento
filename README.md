###Magento 

##Prerequisites

1)Apache
2)PHP and dependencies
3)MySQL
4)Composer
5)Elasticsearch


I) Apache config

$ sudo apt install apache2
$ sudo systemctl start apache2
$ sudo systemctl enable apache2

II) Create a new Apache virtual host and configure

$ sudo vim /etc/apache2/sites-available/magento.conf


 <VirtualHost *:80>
     ServerAdmin admin@domain.com
     DocumentRoot /var/www/html/magento/
     ServerName domain.com
     ServerAlias www.domain.com

     <Directory /var/www/html/magento/>
        Options Indexes FollowSymLinks MultiViews
        AllowOverride All
        Order allow,deny
        allow from all
     </Directory>

     ErrorLog ${APACHE_LOG_DIR}/magento_error.log
     CustomLog ${APACHE_LOG_DIR}/magento_access.log combined
 </VirtualHost>

$ sudo a2ensite magento.conf
$ sudo a2enmod rewrite

III) Installing PHP and dependencies

# apt-get install software-properties-common

# add-apt-repository ppa:ondrej/php

# apt-get update


# apt-get install -y php7.3

# apt-get install -y php7.3 libapache2-mod-php7.3 php7.3-curl php7.3-gmp php7.3-mbstring php7.3-phpdbg php7.3-sqlite3 php7.3-zip php7.3-bcmath php7.3-dba php7.3-imap php7.3-pspell php7.3-sybase php7.3-bz2 php7.3-dev php7.3-interbase php7.3-mysql php7.3-readline php7.3-tidy php7.3-cgi php7.3-enchant php7.3-intl php7.3-odbc php7.3-recode php7.3-xml php7.3-cli php7.3-fpm php7.3-json php7.3-opcache php7.3-snmp php7.3-xmlrpc php7.3-common php7.3-gd php7.3-ldap php7.3-pgsql php7.3-soap php7.3-xsl php7.3-mongo

IV) Installing Mysql-server

# apt-get install mysql-server

# mysql_secure_installation

# mysql -u root -p

CREATE DATABASE magento;
CREATE USER 'magento'@'localhost' IDENTIFIED BY 'magento123';
CREATE USER 'magento'@'%' IDENTIFIED BY 'magento123';

FLUSH PRIVILEGES;
EXIT;

V) Installing Composer
# apt-get install composer



VI) Installing Elasticsearch 

# wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -

# apt-get install apt-transport-https

# echo "deb https://artifacts.elastic.co/packages/7.x/apt stable main" | sudo tee /etc/apt/sources.list.d/elastic-7.x.list

# apt-get update && sudo apt-get install elasticsearch

# service elasticsearch start

# systemctl enable elasticsearch.service

# Verify elastisearch
# curl localhost:9200

VII) Magento file move apache Docment path

# unzip magento-ce-2.4.0-2020-07-24-11-08-21.zip  -d /var/www/html/magento/

VIII) Given Permission

# chmod -R 755 magento

# chown -R www-data:www-data magento/

IX) Install Magento 

# cd /var/www/html/magento/

# chmod -R 777 var pub generated app

# php bin/magento setup:install --base-url=http://Host-WAN-IP/magento/ --db-host=localhost --db-name=magento --db-user=magento --db-password=magento123 --admin-firstname=test --admin-lastname=test --admin-email=test@example.com --admin-user=admin --admin-password=admin123 --language=en_US --currency=USD --timezone=America/Chicago --use-rewrites=1 --search-engine=elasticsearch7 --elasticsearch-host=localhost --elasticsearch-port=9200


X) Enable developer mode
# bin/magento deploy:mode:set developer 

XI) Run setup:upgrade, setup:di:compile and cache:clean command
# bin/magento se:up && bin/magento se:d:c && bin/magento c:c

Admin Password changes

# cd /var/www/html/magento/

# php bin/magento admin:user:create --admin-user aditya --admin-password Lemon@11  --admin-email aditya94cloud@gmail.com --admin-firstname aditya --admin-lastname cloud

# php bin/magento module:disable Magento_TwoFactorAuth

# php bin/magento cache:flush


# php bin/magento deploy:mode:set developer

# php bin/magento se:up && bin/magento se:d:c && bin/magento c:c 

# chmod -R 777 var/
# chmod -R 777 app/
# chmod -R 777 pub/
# chmod -R 777 vendor/
# chmod -R 777 generated/


# php bin/magento indexer:reindex












