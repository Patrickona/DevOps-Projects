## LAMP STACK IMPLEMENTATION ##
### Setting up LAMP STACK using EC2 instance ###
To do this, we need the following 
- An account on AWS.
- We create our virtual machine (EC2 instance). We will be using **Ubuntu server 20.04 LTS** from Amazon Machine Image (free tier)

Steps to create a virtual machine (EC2 instance), Click here [(https://github.com/Patrickona/DevOps-Projects/blob/main/Lamp%20Stack/Creating%20_Server_on_AWS.md)](./Creating_Server_on_AWS)

This launches us into our instance as show in below screenshot

![instance reference](Images/EC2_instance.png)

Then we open our terminal, enter into the directory we have our **.PEM** file saved and **ssh** into our virtual server

![Reference screenshot for location of pem file and ssh into server](Images/PEM_key.png)

![Reference screenshot for ssh into virtual server](Images/ssh_EC2_instance.png)

### Apache2 Web Server Setup ###

In our virtual server, we run the below command to install **apache2** 

`$ sudo apt install apache2`

![Reference to install apache2](Images/apache2.png)

To verify **apache2** is now running as a service, use the below command. 

`$ sudo  systemctl status apache2`

>[!Note]
>You should have a green notification show active (running)

![Below screenshot as reference](Images/apache2_install.png)

Once that is done, we copy the url (use the public IP from our instance) and paste on our browser to ensure our apache server is working. 
>[!Note]
>You should be able to launch the public ip on any web browser.

![Reference to get public IP for instance](Images/apache_ec2.png)

![Reference of apache2 http reachable](Images/apache_html.png)

### My SQL Database Server setup ###

In our terminal, we run the below command to install **mysql server**

`$ sudo apt install mysql-server`

when prompted, confirm installation by typing `Y` and the `Enter`

![Below screenshot for reference](Images/sqlserver_install.png)

After installation, log into the server using the command

`$ sudo mysql`

This will connect to the MYSQL server as the administrative database user **root** which is inferred by the use of sudo. The below output will be seen.

![Below reference](Images/sql_login.png)

To set password as `"PassWord.1"` for the **root** user, we run the below command

`ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'PassWord.1'`

![Below screenshot as reference](Images/mysql_password.png)

Then we "exit" mysql and run the below command to start the interactive script

![Below for reference](Images/sql_interactive.png)

![Below reference](Images/sql_interactive2.png)

Log into mysql server with new password using the below command.

`$ sudo mysql -p`

![Below reference](Images/sql_test.png)

### Installing PHP ###

To setup PHP we run the below command

`$ sudo apt install php libapache2-mod-php php-mysql`

![Reference](Images/php_install.png)

To check version, run the command

`$ php -v`

![Reference](Images/php_version.png)

### Setting up a Virtual Host for Apache ###

To create a virtual for our website, we first create a directory "projectlamp" using the below command

`$ sudo mkdir /var/www/projectlamp`

Then we change ownership to our current environment using the below command

`$ sudo chown -R $USER:$USER /var/www/projectlamp`

![Below screenshot reference](Images/dir.png)

Then we create and open a new configuration file in Apache's **sites available** directory using the below command

`$ sudo vi /etc/apache2/sites-available/projectlamp.conf`

This will bring us into a blank file, paste the below after hitting the ***i*** to insert and paste the text

![Reference scrrenshot below](Images/php_apache.png)

To save and close the file:
- Hit the ***esc***
- Type **:**
- Type ***wq*** to write and quit
- Hit ***enter*** to save the file

To list the new file in the **sites-available** directory, we run the below command

`$ sudo ls /etc/apache2/sites-available`

![Below screenshot reference](Images/ls_apache.png)

By default setting, index.html file will always precedence over an index.php file, to change this behavior, we have to change order in which the file is listed placing the ***.php*** file before the ***.html*** file. We use the below command to achieve this

`$ sudo vim /etc/apache2/mods-enabled/dir.conf`

![See below reference](Images/index.png)

To enable the new virtual host, run the below

`$ sudo a2ensite projectlamp`

To disable the default website that comes with apache, run the below

`$ sudo a2dissite 000-default`

To make sure our configuration files does not contain syntax error:

`$ sudo apache2ctl configtest`

To reload the apache webserver

`$ sudo systemctl reload apache2`

We create a file in /var/www/projectlamp named “index.html”

`$ touch /var/www/projectlamp/index.html`

We then redirect these data into the file:

`$ echo 'Hello LAMP from hostname' $(curl -s http://169.254.169.254/latest/meta-data/public-hostname) 'with public IP' $(curl -s http://169.254.169.254/latest/meta-data/public-ipv4) > /var/www/projectlamp/index.html`

![See below reference](Images/apache_test.png)

Then we refresh our browser to see the echo message sent

![See below reference](Images/php_test.png)

To test our Apache is able to handle ***.php*** scripts we create another file in the **projectlamp** folder and call it **index.php** using the below command

`$ touch /var/www/projectlamp/index.pnp`

`$ vim /var/www/projectlamp/index.php`

A blank file will be opened,we modify with the below information, save and refresh our browser

![Screenshot for reference](Images/phpinfo.png)

![Screenshot for reference](Images/php_html.png)

To remove the ***.php*** file created, after our test we use the below 

`$ sudo rm /var/www/projectlamp/index.php`

## We have successfully deployed a LAMP STACK website in the cloud ## 
