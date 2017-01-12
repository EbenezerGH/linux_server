# Ebenezer Ackon
# Project 7 - Linux Configuration Server

##server configurations:
35.167.63.158
http://ec2-35-167-63-158.us-west-2.compute.amazonaws.com/
port 2200

1) download private key

2) mv udacity_key.rsa ~/.ssh

3) chmod 600 ~/.ssh/udacity_key.rsa

4) ssh -i ~/.ssh/udacity_key.rsa root@35.167.63.158

5) sudo adduser grader

6) sudo visudo - enter grader ALL=(ALL:ALL) ALL

7) sudo cd /etc/sudoers

8) touch /etc/sudoers.d/grader

9) sudo nano /etc/sudoers.d/grader enter grader ALL=(ALL:ALL) ALL

10) sudo apt-get update

11) sudo apt-get upgrade

12) sudo nano /etc/ssh/sshd_config

13) change port to 2200

14) change PasswordAuthentication to yes

15) change PermitRootLogin no

16) add AllowUsers grader to the file

17) sudo service ssh reload

51) sudo nano /etc/hosts

52) add 127.0.1.1 ip-10-20-30-62

18) ssh-keygen

19) ssh-copy-id grader@35.167.63.158 -p 2200

20) ssh -v grader@35.167.63.158 -p 2200

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

37) sudo a2enmod wsgi

38) cd /var/www

39) sudo mkdir FlaskApp

40) cd FlaskApp

41) sudo mkdir FlaskApp

42) cd FlaskApp

43) sudo mkdir static

44) sudo mkdir templates

45) sudo nano __init__.py

46) add this to the file:

from flask import Flask
app = Flask(__name__)
@app.route("/")
def hello():
    return "Hello, I love Digital Ocean!"
if __name__ == "__main__":
    app.run()

47) sudo apt-get install python-pip

48) sudo pip install virtualenv

49) sudo chmod -R 777 venv

50) sudo virtualenv venv

51) source venv/bin/activate

52) sudo pip install Flask

53) sudo python __init__.py

54) test on http://localhost:5000/

55)deactivate

56)sudo nano /etc/apache2/sites-available/FlaskApp

57)sudo nano /etc/apache2/sites-available/category_app.conf

58)update both with:

<VirtualHost *:80>
                ServerName 35.167.63.158
                ServerAdmin Ebenezer
                WSGIScriptAlias / /var/www/FlaskApp/flaskapp.wsgi
                <Directory /var/www/FlaskApp/FlaskApp/>
                        Order allow,deny
                        Allow from all
                </Directory>
                Alias /static /var/www/FlaskApp/FlaskApp/static
                <Directory /var/www/FlaskApp/FlaskApp/static/>
                        Order allow,deny
                        Allow from all
                </Directory>
                ErrorLog ${APACHE_LOG_DIR}/error.log
                LogLevel warn
                CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>

59) sudo a2ensite FlaskApp

60) service apache2 reload

61)cd /var/www/FlaskApp

62)sudo nano flaskapp.wsgi

63) add this to the file: #!/usr/bin/python
import sys
import logging
logging.basicConfig(stream=sys.stderr)
sys.path.insert(0,"/var/www/FlaskApp/")

from FlaskApp import app as application
application.secret_key = 'Add your secret key'

64)sudo service apache2 restart

65) sudo apt-get update

66) sudo apt-get install postgresql postgresql-contrib

67) sudo su - postgres

68) psql

69) CREATE DATABASE category;

70) CREATE USER category;

71) ALTER ROLE category WITH PASSWORD 'password';

72) GRANT ALL PRIVILEGES ON DATABASE category TO category;

73) \q

74) exit

75) sudo apt-get install git

76) sudo git clone https://github.com/EbenezerGH/item-category.git

77) sudo mv item-category/[everything in here] sudo mv /FlaskApp

78) sudo rm -r item-category

79) sudo mv main.py __init__.py

80) go into files and replace engine = create engine calls with:
engine = create_engine('postgresql:///category:password@localhost/category')

81) source venv/bin/activate

82) sudo pip install flask

83) sudo apt-get install python-psycopg2

84) pip install sqlalchemy

85) sudo pip install --upgrade oauth2client

86) pip install httplib2

87) pip install requests

88) apt-get install python-setuptools

89) sudo easy_install psycopg2

90) pip install --upgrade oauth2client

91) sudo mv flaskapp.wsgi FlaskApp/

92) sudo service apache2 restart

93) ServerAlias HOSTNAME http://ec2-35-167-63-158.us-west-2.compute.amazonaws.com/

Error:
Nothing is displaying on page

### useful personal commands:
/etc/apache2/sites-available
pip list


Sources:
https://www.udacity.com/account#!/development_environment
https://www.digitalocean.com/community/tutorials/how-to-deploy-a-flask-application-on-an-ubuntu-vps
https://www.digitalocean.com/community/tutorials/how-to-install-linux-apache-mysql-php-lamp-stack-on-ubuntu
https://www.stackoverflow.com/
https://ubuntuforums.org/
http://linuxcommand.org/
https://github.com/EbenezerGH/item-category/blob/master/database_setup.py
https://forums.aws.amazon.com/message.jspa?messageID=495274
https://www.digitalocean.com/community/tutorials/how-to-secure-postgresql-on-an-ubuntu-vps
http://stackoverflow.com/questions/20414015/no-module-named-flask-using-virtualenv
http://stackoverflow.com/questions/12728004/error-no-module-named-psycopg2-extensions