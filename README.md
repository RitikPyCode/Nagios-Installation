# Nagios-Installation
## Nagios-Installation-configuration

Installing and configuring **Nagios** can be a complex process, but I can provide you with a general guide for installing and configuring Nagios on a Linux system. However, for detailed information, it's always best to refer to the official Nagios documentation.

### Here's a simplified step-by-step guide:

*****************CODE USED FOR INSTALLATION*******************

## Pre-requisite:
```
Make sure your system meets the following requirements:

1- httpd (brower)

2- php (Dashboard)

3- gcc & gd (compiler to convert)

4- make file ( to build)

5- perl ( script)
```

Step-1: **Install Pre-requisites** software you _EC2 machine_ prior to Nagios installation **like: Apache, php, gcc compiler and gd development libraries**:

```
sudo su
yum install httpd php
yum install gcc glibc glibc-common
yum install gd gd-devel
```

Step: 2
Create Account information you need to **setup a nagios user Run** the following commands.

```
adduser -m nagios
passwd nagios
```
Now it ask to enter **new passwd give** whatever you want ex: 12345


```
groupadd nagioscmd
usermod -a -G nagioscmd nagios
usermod -a -G nagioscmd apache
```

Step-3: **Download nagios core and plugins, create a directory** for storing the downloads.
```
mkdir ~/downloads
cd ~/downloads
```

**Download the source code tarball of both nagios and nagios plugins.**
```
wget http://prdownloads.sourceforge.net/sourceforge/nagios/nagios-4.4.10.tar.gz
wget http://nagios-plugins.org/download/nagios-plugins-2.4.6.tar.gz
```

Step-4: **Compile and install Nagios extrac**t the Nagios source code tarball.
```
tar zxvf nagios-4.4.10.tar.gz
cd nagios-4.4.10
```
**Run the below configuration script with the name of the group** which you have created in the above step.
```
./configure --with-command-group=nagioscmd
```

**Note: if you are getting error after executing the above command:**
```
error: 
...
checking for type of socket size... size_t
checking for SSL headers... SSL headers found in /usr
checking for SSL libraries... configure: error: Cannot find ssl libraries
```

_Then install the open ssl-devel then re-execute the above config script_
```
yum install openssl-devel
```

**Compile the nagios source code.**
```
make all
```

Install **binaries, init script, sample config files and set permissions on the external commands** directly.
```
make install
make install-init
make install-config
make install-commandmode
```

Step-5: Confirgure the **web interface**.
```
make install-webconf
```

Step-6: **Create a nagiosadmin account** for login into the nagios **web interface set the password as well**.
```
htpasswd -c /usr/local/nagios/etc/htpasswd.users nagiosadmin
Asking for the password, set a new passwd and keep it memorable.
```

**Restart** the service.

```
service httpd restart
```

Step-7: **Compile and install the nagios and nagios plugins**, extract the Nagios plugins source code tarball.
```
cd ~/downloads
tar zxvf nagios-plugins-2.4.6.tar.gz
cd nagios-plugins-2.4.6
./configure --with-nagios-user=nagios --with-nagios-group=nagios
```

```
make
make install
```

Step-8: **Start Nagios add Nagios to the list of the system service and have it automatically start when the system boots.**
```
chkconfig --add nagios (if you are not able to add go for next step, no problem)
chkconfig nagios on
```

**Verify the sample Nagios config files**-

```
/usr/local/nagios/bin/nagios -v /usr/local/nagios/etc/nagios.cfg
```

Step-9: If there are **no errors start the Nagio**s.
```
service nagios start
service httpd restart
```

****************************END OF CODE *******************************

Step-10 : Copy the **public IP address of EC2 instance** and paste in you local browser in give way.
```
http://52.15.50.246/nagios/
```

# Successfully install and configration of the Nagios 

FIG-1


![image](https://github.com/RitikPyCode/Nagios-Installation/assets/69500530/a6c9825f-1627-414c-baca-4903949a324c)





FIG-2


![Capture1](https://github.com/RitikPyCode/Nagios-Installation/assets/69500530/3eb71500-5918-46ec-add2-8d6609ebc65b)



FIG-3



![Capture2](https://github.com/RitikPyCode/Nagios-Installation/assets/69500530/5beceef1-cb03-40f1-b814-8ccffd7d3b18)






## If you have successfully set up the rewrite rules for Nagios and can access the application without any issues, that's great news! 



![Capture3](https://github.com/RitikPyCode/Nagios-Installation/assets/69500530/b9ee03d2-e094-48e2-a35b-f12d42882842)



**You can give credit and share this with your peers and follow me on LinkedIn for more..**

### https://www.linkedin.com/in/ritikktiwari/

