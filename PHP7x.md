

#Install PHP 7.3 on Ubuntu

PHP 7.2 stable version has been released. Use the following set of commands to enable PPA for PHP 7.2 in your Ubuntu system and install it. You can use this version for production use also.

      sudo apt-get install software-properties-common
      sudo add-apt-repository ppa:ondrej/php
      sudo apt-get update
      sudo apt-get install -y php7.3
      Now use the following command to check installed php version on your system.
      php -v 



#Install PHP 7.2 on Ubuntu

PHP 7.2 stable version has been released. Use the following set of commands to enable PPA for PHP 7.2 in your Ubuntu system and install it. You can use this version for production use also.

      sudo apt-get install software-properties-common
      sudo add-apt-repository ppa:ondrej/php
      sudo apt-get update
      sudo apt-get install -y php7.2
      Now use the following command to check installed php version on your system.

      php -v 






#Install PHP 7.1 on Ubuntu

Use the following set of commands to add PPA for PHP 7 in your Ubuntu system and install PHP 7.1 version.

      sudo apt-get install software-properties-common
      sudo add-apt-repository ppa:ondrej/php
      sudo apt-get update
      sudo apt-get install -y php7.1
      php -v 



## Install PHP 7.0 on Ubuntu

Use the following set of commands to add PPA for PHP 7 in your Ubuntu system and install PHP 7.0 version.

        sudo apt-get install python-software-properties
        sudo add-apt-repository ppa:ondrej/php
        sudo apt-get update
        sudo apt-get install -y php7.0
        Now use the following command to check installed php version on your system.
        php -v 


## How to change the PHP version?

            $ sudo update-alternatives --config php
            or
            $ sudo update-alternatives -set php /usr/bin/php7.2
            
            
## Host Multiple Websites with different PHP Versions on Ubuntu 18.04 VPS


- Install PHP 7.0 and PHP 7.2 with PHP-FPM. First, you will need to add PHP repository to your server to install multiple versions of PHP. You can add Ondrej PHP repository with the following command:

            apt-get install software-properties-common -y
            add-apt-repository ppa:ondrej/php
Next, update the repository with the following command:

            apt-get update -y
Once the repository is up to date, install PHP 7.0, PHP 7.2 and PHP-FPM with the following command:

             apt-get install php7.0 php7.0-fpm php7.2 php7.2-fpm -y

Once the installation has been completed, check the status of PHP-FPM with the following command:

                  systemctl status php7.0-fpm
                  systemctl status php7.2-fpm
                  Create Website1 and Website2
Next, create a document root directory for Website1 and Website2 with the following command:

                  mkdir /var/www/html/site1.example.com
                  mkdir /var/www/html/site2.example.com
Next, create a sample index.php file for website site1.example.com:

                        nano /var/www/html/site1.example.com/index.php
Add the following lines:

      <?php
      phpinfo();
      ?>
Save and close the file. Then, create an index.php file for site2.example.com:

            nano /var/www/html/site2.example.com/index.php
Add the following lines:

            <?php
            phpinfo();
            ?>
Save and close the file. Then, change the ownership of both websites to www-data:

            chown -R www-data:www-data /var/www/html/site1.example.com
            chown -R www-data:www-data /var/www/html/site2.example.com
Configure Nginx
Next, you will need to create an Nginx virtual host file for domain site1.linuxbuz.com that uses PHP 7.0. You can do it with the following command:

            nano /etc/nginx/sites-available/site1.example.com.conf
Add the following lines:

                  server {
                     listen 80;
                     root /var/www/html/site1.example.com/;
                     index index.php;
                     server_name site1.example.com;
                     location / {
                        try_files $uri $uri/ =404;
                     }
                     location ~ \.php$ {
                        try_files $uri =404;
                        fastcgi_split_path_info ^(.+\.php)(/.+)$;
                        fastcgi_pass unix:/var/run/php/php7.0-fpm.sock;
                        fastcgi_index index.php;
                        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
                        include fastcgi_params;
                     }
                  }
Save and close the file.

Next, create an Nginx virtual host file for domain site2.example.com that uses PHP 7.2.

            nano /etc/nginx/sites-available/site2.example.com.conf
            
Add the following lines:

            server {
               listen 80;

               root /var/www/html/site2.example.com/;
               index index.php;

               server_name site2.example.com;

               location / {
                  try_files $uri $uri/ =404;
               }

               location ~ \.php$ {
                  try_files $uri =404;
                  fastcgi_split_path_info ^(.+\.php)(/.+)$;
                  fastcgi_pass unix:/var/run/php/php7.2-fpm.sock;
                  fastcgi_index index.php;
                  fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
                  include fastcgi_params;
               }
            }
Save and close the file. Then, enable both virtual host files with the following command:

            ln -s /etc/nginx/sites-available/site1.example.com.conf /etc/nginx/sites-enabled/
            ln -s /etc/nginx/sites-available/site2.example.com.conf /etc/nginx/sites-enabled/
Finally, restart Nginx and PHP-FPM service to apply all the configuration changes:

            systemctl restart nginx
            systemctl restart php7.0-fpm
            systemctl restart php7.2-fpm
Test Both Websites
Both websites are now installed and configured run with multiple versions of PHP.

Now, open your web browser and type the URL http://site1.example.com. 
You will get the following page that indicates that your Website1 is running with PHP 7.0.
Next, open your web browser and type the URL http://site2.example.com.
You will get the following page that indicates that your Website2 is running with PHP 7.2.

