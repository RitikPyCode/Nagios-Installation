# Nagios-Installation
Nagios-Installation-configuration

*****************CODE USED FOR INSTALLATION*******************

sudo su
yum install httpd php
yum install gcc glibc glibc-common
yum install gd gd-devel

''
adduser -m nagios
passwd nagios

''

groupadd nagioscmd
usermod -a -G nagioscmd nagios
usermod -a -G nagioscmd apache

mkdir ~/downloads
cd ~/downloads

wget http://prdownloads.sourceforge.net/sourceforge/nagios/nagios-4.4.10.tar.gz
wget http://nagios-plugins.org/download/nagios-plugins-2.4.6.tar.gz

tar zxvf nagios-4.4.10.tar.gz
cd nagios-4.4.10

./configure --with-command-group=nagioscmd

if you are getting error after executing the above command  
error: 
...
checking for type of socket size... size_t
checking for SSL headers... SSL headers found in /usr
checking for SSL libraries... configure: error: Cannot find ssl libraries

yum install openssl-devel

make all

make install
make install-init
make install-config
make install-commandmode

make install-webconf

htpasswd -c /usr/local/nagios/etc/htpasswd.users nagiosadmin
service httpd restart


cd ~/downloads
tar zxvf nagios-plugins-2.4.6.tar.gz
cd nagios-plugins-2.4.6

./configure --with-nagios-user=nagios --with-nagios-group=nagios
make
make install


chkconfig --add nagios (if you are not able to add go for next step, no problem)
chkconfig nagios on

/usr/local/nagios/bin/nagios -v /usr/local/nagios/etc/nagios.cfg

service nagios start
service httpd restart

****************************END OF CODE *******************************

Paste the DNS public ip:
http://52.15.50.246/nagios/

![Capture1](https://github.com/RitikPyCode/Nagios-Installation/assets/69500530/3eb71500-5918-46ec-add2-8d6609ebc65b)


![Capture2](https://github.com/RitikPyCode/Nagios-Installation/assets/69500530/5beceef1-cb03-40f1-b814-8ccffd7d3b18)



Finally sucsfully we can access the Nagios Application.

![Capture3](https://github.com/RitikPyCode/Nagios-Installation/assets/69500530/b9ee03d2-e094-48e2-a35b-f12d42882842)



