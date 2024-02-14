## WEB STACK IMPLEMENTATION ##
### Setting up LEMP STACK using EC2 instance ###
To do this, we need the following 
- An account on AWS.
- We create our virtual machine (EC2 instance). We will be using **Ubuntu server 20.04 LTS** from Amazon Machine Image (free tier)

Steps to create a virtual machine (EC2 instance), Click here [(https://github.com/Patrickona/DevOps-Projects/blob/main/Lamp%20Stack/Creating%20_Server_on_AWS.md)](./Creating_Server_on_AWS)

This launches us into our instance as show in below screenshot

![Screenshot below of our instance](Images/EC2_instance.png)

Then we open our terminal, enter into the directory we have our **.PEM** file saved and **ssh** into our virtual server

`ssh -i <private-key.pem> ubuntu@<EC2-Public-IP-address>`

![Below screenshot for reference](Images/Ubuntu_VC.png)

### Installing Nginx Web Server ###

Run the below command to install nginx in our remote server

`$ sudo apt update`
`$ sudo apt install nginx`

 Then we run the below command to confirm it has been properly installed. You should see a green notification saying **Actively running** to signify it is properly installed.

`$ sudo systemctl status nginx`

 ![Below screenshot for reference](Images/nginx_install.png)

 Copy our EC2 instance public IP address and paste on a web browser to test our Nginx server.

 ![Below screenshot for reference](Images/Web_browser.png)

 ### Installing MySql Server ###

 In our terminal, we run the below command to install **mysql server**

`$ sudo apt install mysql-server`

when prompted, confirm installation by typing `Y` and the `Enter`

![Below screenshot for reference](Images/mysql_install.png)

After installation, log into the server using the command

`$ sudo mysql`

This will connect to the MYSQL server as the administrative database user **root** which is inferred by the use of sudo. The below output will be seen.

To set password as `"PassWord.1"` for the **root** user, we run the below command

`ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'PassWord.1'`

Then we "exit" mysql and run the below command to start the interactive script

`$ sudo mysql_secure_installation`

![Below screenshot for reference](Images/My_secure.png)

Log into mysql server with new password using the below command.

`$ sudo mysql -p`

![Below reference](Images/sql_test.png)

 