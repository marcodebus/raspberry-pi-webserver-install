sudo apt update
sudo apt upgrade
sudo apt update

sudo apt install apache2

sudo chown -R pi:www-data /var/www/html/
sudo chmod -R 770 /var/www/html/

sudo apt install php php-mbstring

sudo rm /var/www/html/index.html
echo "<?php phpinfo ();?>" > /var/www/html/index.php


sudo apt install mariadb-server php-mysql

sudo mysql --user=root



DROP USER 'root'@'localhost';
CREATE USER 'root'@'localhost' IDENTIFIED BY '';
GRANT ALL PRIVILEGES ON *.* TO 'root'@'localhost' WITH GRANT OPTION;

CREATE USER 'marco'@'localhost' IDENTIFIED BY 'Auditt8n';
GRANT ALL PRIVILEGES ON *.* TO 'root'@'localhost' WITH GRANT OPTION;

exit



sudo apt install phpmyadmin

sudo phpenmod mysqli
sudo /etc/init.d/apache2 restart

sudo ln -s /usr/share/phpmyadmin /var/www/html/phpmyadmin

sudo service apache2 restart






Firstly, backup sql.lib.php before editing.

sudo cp /usr/share/phpmyadmin/libraries/sql.lib.php /usr/share/phpmyadmin/libraries/sql.lib.php.bak
Edit sql.lib.php in nano.

sudo nano /usr/share/phpmyadmin/libraries/sql.lib.php
Press CTRL + W and search for (count($analyzed_sql_results['select_expr'] == 1)
Replace it with ((count($analyzed_sql_results['select_expr']) == 1)

Save file and exit. (Press CTRL + X, press Y and then press ENTER)

Import/Export issues
If you are also getting an error Warning in ./libraries/plugin_interface.lib.php#551 under import and export tabs:

Backup plugin_interface.lib.php

sudo cp /usr/share/phpmyadmin/libraries/plugin_interface.lib.php /usr/share/phpmyadmin/libraries/plugin_interface.lib.php.bak
Edit plugin_interface.lib.php

sudo nano /usr/share/phpmyadmin/libraries/plugin_interface.lib.php
Press CTRL + W and search for if (! is_null($options) && count($options) > 0) {

If not found, try search for if ($options != null && count($options) > 0)

Replace with if (! is_null($options) && count((array)$options) > 0) {

Save file and exit. (Press CTRL + X, press Y and then press ENTER)
