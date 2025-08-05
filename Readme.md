Steps incolved in setting up infra

launch the EC2 machine with ubuntu

to update teh repository
sudo apt update 

install the apache2
sudo apt install apache2

now clone this repository to default web server file path
cd /var/www/

<img width="721" height="205" alt="image" src="https://github.com/user-attachments/assets/648737f3-28c2-42d4-b57d-a29aa506b65a" />

by default the user will be root need to cahnge the web directory permission

chown -R www-data:www-data /var/www/E-Commerswebsite/

Execute the below command to give file permission.
chmod -R 755 E-Commerswebsite/

now you need to create the virtual host (config file)
the default config path will -- /etc/apache2/sites-available

now create the new config file

vi  /etc/apache2/sites-available/E-Commerswebsite

<VirtualHost *:80>
	ServerAdmin admin@.com
	DocumentRoot /var/www/E-Commerswebsite
	ServerName ec2-13-215-46-95.ap-southeast-1.compute.amazonaws.com
	Serveralias www.ec2-13-215-46-95.ap-southeast-1.compute.amazonaws.com
	<Directory /var/www/E-Commerswebsite/>
		Options +FollowSymlinks
		AllowOverride All
		Require all granted
	</Directory>
	ErrorLog ${APACHE_LOG_DIR}/error.log
	CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>

:wq!

after this run below command to enable the site
a2ensite E-Commerswebsite.conf 

by default read write permission will be there for apache but we executing again

a2enmod rewrite

then restart the apache2

systemctl restart apache2

after this try hitting the site using ec2-13-215-46-95.ap-southeast-1.compute.amazonaws.com
below page will appear

<img width="1876" height="943" alt="image" src="https://github.com/user-attachments/assets/05175e7f-38a3-4c99-8ba7-58feb0e7ecd4" />



