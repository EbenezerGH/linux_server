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



Sources:
https://www.udacity.com/account#!/development_environment
https://www.digitalocean.com/community/tutorials/how-to-deploy-a-flask-application-on-an-ubuntu-vps
https://www.digitalocean.com/community/tutorials/how-to-install-linux-apache-mysql-php-lamp-stack-on-ubuntu
https://www.stackoverflow.com/
https://ubuntuforums.org/
http://linuxcommand.org/
https://github.com/EbenezerGH/item-category/blob/master/database_setup.py
