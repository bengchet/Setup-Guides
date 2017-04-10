# Laravel Setup

## Setup LAMP on Ubuntu
Refer to this [url](https://www.digitalocean.com/community/tutorials/how-to-install-lamp-on-ubuntu-14-04-quickstart)

### Disable apache server on boot startup
sudo update-rc.d -f apache2 remove

### Enable or disable apache server manually
sudo service apache2 start/restart/stop

### Enable permissions for user visiting the apache server
* Add yourself to the www-data group
```sudo adduser $USER www-data```
* Change the ownership of the files in /var/www
```sudo chown -R www-data:www-data /var/www```
* Change the umask, so newly created files by Apache grants write permissions to the group too. Add umask 007 to /etc/apache2/envvars.
* Grant yourself (technically, the group www-data) write permissions
```sudo chmod -R g+w /var/www``` **Or** ```sudo chmod 755 -R /var/www```

### Allow access to .htaccess file
* ```sudo nano /etc/apache2/apache2.conf```
* At section /var/www
- Change line AllowOverride None to AllowOverride All

## Install Laravel framework
* Refer [here](https://www.howtoforge.com/tutorial/install-laravel-on-ubuntu-for-apache/)

### Install latest laravel requires php v5.6 and above
* ```sudo add-apt-repository ppa:ondrej/php5-5.6```
* ```sudo apt-get update```
* ```sudo apt-get install python-software-properties```
* ```sudo apt-get install php5```
> More info refer [here](https://www.dev-metal.com/install-setup-php-5-6-ubuntu-14-04-lts/)

### Install php5.6 packages
* ```sudo apt-get install php5.6-mbstring```
* ```sudo apt-get install php5.6-xml```
* ```sudo apt-get install php5.6-mcrypt```
* ```sudo apt-get install php5.6-mysql```

### Enable php module
* ```sudo phpenmod mcrypt```
* ```sudo phpenmod mbstring```

### Check php version
* ```php -v // show version```
* ```php -m // show modules```

### Finishing and get started
* Follow the last few steps from https://www.howtoforge.com/tutorial/install-laravel-on-ubuntu-for-apache/

```php artisan key:generate```

