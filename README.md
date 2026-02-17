# Splunk_SOC_Lab_Set_Up

## Objective

This project will focus on installation and configuration of Splunk on different OS platforms: Linux and Windows. It will also walkthrough the process of integrating log sources with use of listening ports or by installing forwarders.

### Skills Learned



### Tools Used



## Steps

Splunk supports multiple OS versions. In order to start we need to visit <a href="https://www.splunk.com/">splunk.com</a>, create account and then download the <a href="https://www.splunk.com/en_us/download/splunk-enterprise.html?locale=en_us">Splunk Enterprise</a> version we need.

<img width="1206" height="405" alt="image" src="https://github.com/user-attachments/assets/e7733aaa-89ef-45dc-bb18-7448e937adab" />

#### Setting up Splunk in Linux environment

1. Downloaded files are located in 'Downloads' directory. Change directory to the one below.

<img width="574" height="142" alt="image" src="https://github.com/user-attachments/assets/d2d31687-06de-4770-93fb-63a9a12c64ac" />

2. Elevate to root user by running the following command.

```
sudo su
```

3. To install Splunk we need to uncompress the installer file with the following command.

```
tar xvzf splunk_installer.tgz
```

4. After installation is finished new folder will appear in the directory.

<img width="485" height="58" alt="image" src="https://github.com/user-attachments/assets/6aa86c4c-bdeb-49fb-93b3-54c60a563551" />

5. Now we will move the new folder to /opt directory in order to configure the Splunk.

```
mv splunk /opt/
```

6. Now that all the necessary binaries are installed on the system, we will start the instance of Splunk. Change directory to /opt/splunk/bin/.

```
root@coffely:/opt/splunk/bin# cd /opt/splunk/bin/
root@coffely:/opt/splunk/bin# ./splunk start --accept-license

This appears to be your first time running this version of Splunk.

Splunk software must create an administrator account during startup. Otherwise, you cannot log in.
Create credentials for the administrator account.
Characters do not appear on the screen when you type in credentials.

Please enter an administrator username: splunkadmin
Password must contain at least:
   * 8 total printable ASCII character(s).
Please enter a new password: 
Please confirm new password: 
Copying '/opt/splunk/etc/openldap/ldap.conf.default' to '/opt/splunk/etc/openldap/ldap.conf'.
Generating RSA private key, 2048 bit long modulus

...
...
...

Waiting for web server at http://127.0.0.1:8000 to be available............... Done


If you get stuck, we're here to help.  
Look for answers here: http://docs.splunk.com

The Splunk web interface is at http://coffely:8000

root@coffely:/opt/splunk/bin# 

``` 
