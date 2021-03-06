# Ebenezer Ackon
# Project 7 - Linux Configuration Server

##server configurations:
IP: 35.160.242.132
AWS: http://ec2-35-160-242-132.us-west-2.compute.amazonaws.com/
SSH PORT: port 2200

1) download private key

2) mv udacity_key.rsa ~/.ssh

3) chmod 600 ~/.ssh/udacity_ssh/udacity_key.rsa

4) ssh -i ~/.ssh/udacity_ssh/udacity_key.rsa root@35.160.242.132

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

18) sudo nano /etc/hosts

19) add 127.0.1.1 ip-10-20-30-62

20) ssh-keygen - locally

21) su - grader

22) mkdir .ssh

23) touch .ssh/authorized_keys

24) nano .ssh/authorized_keys

25) chmod 700 .ssh

26) chmod 644 .ssh/authorized_keys

27) ssh -i .ssh/udacity_ssh/id_rsa grader@35.160.242.132 -p 2200

28) sudo nano /etc/ssh/sshd_config

29) change PasswordAuthentication no

30) sudo service ssh restart

31) sudo ufw default allow outgoing

32) sudo ufw default deny incoming

33) sudo ufw allow 2200/tcp

34) sudo ufw allow 80/tcp

35) sudo ufw allow 123/udp

36) sudo ufw enable

37) sudo dpkg-reconfigure tzdata

38) sudo apt-get install apache2

39) sudo apt-get install python-setuptools libapache2-mod-wsgi

40) sudo service apache2 restart

41) sudo apt-get install git

42) git config --global user.name EbenezerGH

43) git config --global user.email eackon714@gmail.com

44) sudo a2enmod wsgi

45) cd /var/www

46) sudo mkdir FlaskApp

47) cd FlaskApp

48) sudo mkdir FlaskApp

49) cd FlaskApp

50) sudo mkdir static

51) sudo mkdir templates

52) sudo nano __init__.py

53) add this to the file:

from flask import Flask
app = Flask(__name__)
@app.route("/")
def hello():
    return "Hello, I love Digital Ocean!"
if __name__ == "__main__":
    app.run()

54) sudo apt-get install python-pip

55) sudo pip install virtualenv

56) sudo virtualenv venv

57) sudo chmod -R 777 venv

58) source venv/bin/activate

59) sudo pip install Flask

60) sudo python __init__.py

61) test on http://localhost:5000/

62)deactivate

63)sudo nano /etc/apache2/sites-available/FlaskApp

64)sudo nano /etc/apache2/sites-available/flask_app.conf

65)update both with:

<VirtualHost *:80>
                ServerName 35.160.242.132
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

66) sudo a2ensite FlaskApp

67) service apache2 reload

68)cd /var/www/FlaskApp

69)sudo nano flaskapp.wsgi

70) add this to the file: #!/usr/bin/python
import sys
import logging
logging.basicConfig(stream=sys.stderr)
sys.path.insert(0,"/var/www/FlaskApp/")

from FlaskApp import app as application
application.secret_key = 'Add your secret key'

71)sudo service apache2 restart

**AT THIS POINT GOING TO 35.160.242.132 DISPLAYS THE CORRECT SAMPLE TEXT!

72) sudo apt-get update

73) sudo apt-get install postgresql postgresql-contrib

74) sudo su - postgres

75) psql

76) CREATE DATABASE category;

77) CREATE USER category;

78) ALTER ROLE category WITH PASSWORD 'password';

79) GRANT ALL PRIVILEGES ON DATABASE category TO category;

80) \q

81) exit

82) sudo apt-get install git

83) sudo git clone https://github.com/EbenezerGH/item-category.git

84) sudo mv item-category/[everything in here] sudo mv /FlaskApp

85) sudo rm -r item-category

86) sudo mv main.py __init__.py

87) go into files and replace engine = create engine calls with:
engine = create_engine('postgresql://category:password@localhost/category')

88) source venv/bin/activate

89) sudo pip install flask

90) sudo apt-get install python-psycopg2

91) pip install sqlalchemy

92) pip install --upgrade oauth2client

92) pip install httplib2

93) pip install requests

94) sudo apt-get install python-setuptools

95) sudo easy_install psycopg2

96) sudopip install --upgrade oauth2client

97) create Category Directories with the same file structure as FlaskApp directories

98) insert this in category.wsgi

99) sudo service apache2 restart

100) sudo service apache2 reload

101) sudo service postgresql restart

102) paste this in category.conf
ServerAlias HOSTNAME http://ec2-35-160-242-132-us-west-2.compute.amazonaws.com/

103) add 35.160.242.132 and http://ec2-35-160-242-132.us-west-2.compute.amazonaws.com/ to google credentials


from flask import Flask
app = Flask(__name__)
@app.route("/")
def hello():
    return "JUST WORK!!"
if __name__ == "__main__":
    app.run()

101) Create sudo nano /etc/apache2/sites-available/category.conf and paste this in

<VirtualHost *:80>
    ServerName 35.160.242.132
    ServerAdmin eackon714@gmail.com
    ServerAlias http://ec2-35-160-242-132.us-west-2.compute.amazonaws.com/
    WSGIScriptAlias / /var/www/Category/category.wsgi
    <Directory /var/www/Category/Category/>
        Order allow,deny
        Allow from all
    </Directory>
    Alias /static /var/www/Category/Category/static
    <Directory /var/www/Category/Category/static/>
        Order allow,deny
        Allow from all
    </Directory>
    ErrorLog ${APACHE_LOG_DIR}/error.log
    LogLevel warn
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>

101) ServerAlias http://ec2-35-160-242-132.us-west-2.compute.amazonaws.com/

### useful personal commands:
/etc/apache2/sites-available
pip list
sudo tail -10 /var/log/apache2/error.log

###Resources:
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
http://stackoverflow.com/questions/10572498/importerror-no-module-named-sqlalchemy
https://www.digitalocean.com/community/tutorials/how-to-set-up-ssh-keys--2
http://unix.stackexchange.com/questions/3568/how-to-switch-between-users-on-one-terminal
http://stackoverflow.com/questions/11919391/postgresql-error-fatal-role-username-does-not-exist
http://snipplr.com/view/15626/apache2--enabling-and-disabling-sites/
http://stackoverflow.com/questions/12201928/python-open-method-ioerror-errno-2-no-such-file-or-directory