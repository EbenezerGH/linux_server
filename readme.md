# Ebenezer Ackon
# Project 7 - Linux Configuration Server

##server configurations:
35.167.206.80
http://ec2-35-167-206-80.us-west-2.compute.amazonaws.com/
port 2200


1) download private key

2) mv udacity_key.rsa ~/.ssh

3) chmod 600 ~/.ssh/udacity_key.rsa

4) ssh -i ~/.ssh/udacity_key.rsa root@35.167.206.80

5) sudo adduser grader

6) sudo visudo - enter grader ALL=(ALL:ALL) ALL

7) sudo nano /etc/sudoers

8) touch /etc/sudoers.d/grader

9) sudo nano /etc/sudoers.d/grader enter grader ALL=(ALL:ALL) ALL

10) sudo apt-get update

11) sudo apt-get upgrade

12) sudo nano /etc/ssh/sshd_config

13) change port to 2200

14) change PasswordAuthentication to yes

15) change PermitRootLogin without-password to PermitRootLogin no to disallow root login

16) add AllowUsers grader to the file

17) sudo service ssh reload

18) ssh-keygen

19) ssh-copy-id grader@35.167.206.80 -p 2200

20) ssh -v grader@35.167.206.80 -p 2200

21) sudo nano /etc/ssh/sshd_config

22) change PasswordAuthentication no

23) sudo service ssh restart

24) sudo ufw default allow outgoing

25) sudo ufw default deny incoming

26) sudo ufw allow 2200/tcp

27) sudo ufw allow 80/tcp

28) sudo ufw allow 123/udp

29) sudo ufw enable

30) sudo dpkg-reconfigure tzdata

31) sudo apt-get install apache2

32) sudo apt-get install python-setuptools libapache2-mod-wsgi

33) sudo service apache2 restart

34) sudo apt-get install git

35) git config --global user.name EbenezerGH

36) git config --global user.email eackon714@gmail.com

37) cd /var/www

38) sudo mkdir category_app

39) cd category_app

40) sudo mkdir category_app

41) cd category_app

42) sudo mkdir static

43) sudo mkdir templates

44) sudo nano __init__.py

45) add this to the file:

`from flask import Flas
app = Flask(__name__)
@app.route("/")
def hello():
    return "Hello, I love Digital Ocean!"
if __name__ == "__main__":
    app.run()`

46) sudo apt-get install python-pip

47) sudo pip install virtualenv

48) sudo virtualenv venv

49) source venv/bin/activate

50) sudo pip install Flask

51) sudo nano /etc/hosts

52) add 127.0.1.1 ip-10-20-63-33

53) sudo python __init__.py

54) test on http://localhost:5000/  NOT WORKING  <---

56)deactivate

57)sudo nano /etc/apache2/sites-available/category_app

58)sudo nano /etc/apache2/sites-available/category_app.conf

59)update both with:

`<VirtualHost *:80>
                ServerName 35.167.206.80
                ServerAdmin Ebenezer
                WSGIScriptAlias / /var/www/category_app/category_app.wsgi
                <Directory /var/www/category_app/category_app/>
                        Order allow,deny
                        Allow from all
                </Directory>
                Alias /static /var/www/category_app/category_app/static
                <Directory /var/www/categoryapp/category_app/static/>
                        Order allow,deny
                        Allow from all
                </Directory>
                ErrorLog ${APACHE_LOG_DIR}/error.log
                LogLevel warn
                CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>`

60) service apache2 reload

61) sudo a2ensite category_app_file

62) sudo nano category_app.wsgi

63) add this to the file:

`#!/usr/bin/python
import sys
import logging
logging.basicConfig(stream=sys.stderr)
sys.path.insert(0,"/var/www/category_app/")

from category_app import app as application
application.secret_key = 'Add your secret key'`

64) sudo service apache2 restart




Sources:
https://www.udacity.com/account#!/development_environment
https://www.digitalocean.com/community/tutorials/how-to-deploy-a-flask-application-on-an-ubuntu-vps
https://www.digitalocean.com/community/tutorials/how-to-install-linux-apache-mysql-php-lamp-stack-on-ubuntu
https://www.stackoverflow.com/
https://ubuntuforums.org/
http://linuxcommand.org/
https://github.com/EbenezerGH/item-category/blob/master/database_setup.py
https://forums.aws.amazon.com/message.jspa?messageID=495274
