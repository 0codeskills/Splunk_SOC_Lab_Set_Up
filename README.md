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

6. Now that all the necessary binaries are installed on the system, we will start the instance of Splunk. Change directory to /opt/splunk/bin/. Run command to initiate the Splunk instance, you will be asked to creata administrator account and password. When completed you will be presented with output similar to the one below.

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

7. Now we can access Splunk in web browser by going to http://coffely:8000

<img width="1253" height="675" alt="image" src="https://github.com/user-attachments/assets/c86e7d71-8f57-4b62-aaad-63b9d09895e1" />

#### Interacting with Splunk CLI

To interact with Splunk CLI we need to change directory to /opt/splunk/

```
#Command to start all the necessary Splunk processes and enabling the server to accept incoming data
./bin/splunk start

#Command to stop the Splunk server
./bin/splunk stop

#Command to restart the Splunk server
./bin/splunk restart

#Command to check the status of the Splunk server
./bin/splunk status

#Command to add a single event to the Splunk index. Good for testing purposes
./bin/splunk add oneshot

#Command to search for specific events or perfor, more complex searches using Splunk's search language
./bin/splunk search coffely

#Command provides all the help options
./bin/splunk help
```

#### Data ingestion in Splunk

Configuring data ingestion is crucial part of Splunk. It allows data to be normalized, indexed and searchable by users. Splunk accepts data from different sources including Operating System logs, Web Applications, Inrusion Detection logs, Osquery logs, etc. In this task we will use forwarders to ingest Linux logs into Splunk instance. 
There are 2 types of forwarders:
- Heavy forwarders - used when we need to apply filter, analuze or make changes to the logs at source before sending them to the destination
- Universal frowarders - lightweight agent installed on the target host to forwards the logs to the Splunk instance

We will be using universal forwarders in the task. They can be downloaded from <a href="https://www.splunk.com/en_us/download/universal-forwarder.html?locale=en_us">Splunk website</a>

<img width="1245" height="438" alt="image" src="https://github.com/user-attachments/assets/314e7e48-0264-4bb0-98da-02d5d72728a9" />

1. After downloading the forwarder installer we will change directory to /home/ubuntu/Downloads/splunk/ and from there wil will run the command to install the forwarders.

```
tar xvzf splunkforwarder.tgz
```

2. We will no move the created 'splunkforwarder' folder to /opt/ directory.

```
mv splunkforwarder /opt/
```

3. Next we will change directory to /opt/splunkforwarder/ and will run the Splunk forwarder instance. We will be asked to create a user and password.

```
root@coffely:/opt/splunkforwarder# ./bin/splunk start --accept-license

This appears to be your first time running this version of Splunk.

Splunk software must create an administrator account during startup. Otherwise, you cannot log in.
Create credentials for the administrator account.
Characters do not appear on the screen when you type in credentials.

Please enter an administrator username: splunkadmin
Password must contain at least:
   * 8 total printable ASCII character(s).
Please enter a new password: 
Please confirm new password: 
Creating unit file...
Failed to auto-set default user.
Failed to create the unit file. Please do it manually later.


Splunk> Another one.

Checking prerequisites...
	Checking mgmt port [8089]: not available
ERROR: mgmt port [8089] - port is already bound.  Splunk needs to use this port.
Would you like to change ports? [y/n]: y
Enter a new mgmt port: 8090
Setting mgmt to port: 8090
The server's splunkd port has been changed.
	Checking mgmt port [8090]: open
Starting splunk server daemon (splunkd)...  
Done
```

#### Configuring Splunk forwarder on Linux

1. We will log into Splunk and Go to Settings -> Forward and receiving as below.

<img width="1274" height="563" alt="image" src="https://github.com/user-attachments/assets/f68a35db-8f60-4b7d-8624-b2e8130e59af" />

2. As we want to configure receiving we select COnfigure receiving and on the next page select New Receiving Port

<img width="1262" height="432" alt="image" src="https://github.com/user-attachments/assets/ae7e2d3b-846e-45b0-baef-c30bf62f41c5" />

<img width="1274" height="258" alt="image" src="https://github.com/user-attachments/assets/f0792024-47b3-4b99-9504-42465b6048c2" />

3. We will configure Splunk to listen on port 9997 and select Save.

<img width="1263" height="410" alt="image" src="https://github.com/user-attachments/assets/cb2c0221-bb14-4555-a822-43f966c58c0a" />
 
4. Listening port is now enabled

<img width="1263" height="449" alt="image" src="https://github.com/user-attachments/assets/3eaff79a-d3f9-4213-8d6c-ead6f0b5dca1" />

5. Now we need to create an index which will store all the received data, if we won't set it up by default Splunk will use main index.

<img width="1271" height="613" alt="image" src="https://github.com/user-attachments/assets/c76b54dd-08ff-4417-ab43-7db7f481e115" />

6. On the indexes page select New Index.

<img width="1270" height="206" alt="image" src="https://github.com/user-attachments/assets/8e3786fa-73d6-4d63-b932-93adcad66a38" />

7. On the New Index window fill out the Index Name field and click Save

<img width="791" height="737" alt="image" src="https://github.com/user-attachments/assets/3a19168b-5804-4997-a78b-000c4e160363" />

8. Now we will configure forwarder to ensure it sends the data to the correct destination. Back in Linux terminal, go to the /opt/splunkforwarder/bin directory

```
root@coffely:/opt/splunkforwarder/bin# ./splunk add forward-server SERVER_IP_ADDRESS:9997
Splunk username: splunkadmin
Password: 
Added forwarding to: SERVER_IP_ADDRESS:9997.
root@coffely:/opt/splunkforwarder/bin# 
```
9. Linux logs are stored in /var/log directory

<img width="879" height="324" alt="image" src="https://github.com/user-attachments/assets/126c2232-c12b-40d2-bcaf-9c0f66342ef2" />

10. We will now ingest syslog into Splunk

<img width="859" height="73" alt="image" src="https://github.com/user-attachments/assets/ffa21d94-4928-40e9-8a9a-3c1840bc2307" />

11. To confirm the configuration we can check the inputs.conf file in /opt/splunkforwarder/etc/apps/search/local directory

```
root@coffely:/opt/splunkforwarder/bin# cd /opt/splunkforwarder/etc/apps/search/local
root@coffely:/opt/splunkforwarder/etc/apps/search/local# ls
inputs.conf
root@coffely:/opt/splunkforwarder/etc/apps/search/local# cat inputs.conf 
[monitor:///var/log/syslog]
disabled = false
index = Linux_host
root@coffely:/opt/splunkforwarder/etc/apps/search/local# 
```

12. Now we will use Logger a built-in command line tool to create test logs added to syslog file and we will search Splunk for those logs.

```
logger "coffely-has-the-best-coffee-in-town"
tail -1 /var/log/syslog
Feb 17 20:50:28 coffely ubuntu: coffely-has-the-best-coffee-in-town
```

<img width="1274" height="733" alt="image" src="https://github.com/user-attachments/assets/8d37e2fd-b5c7-4b6f-87a8-3640118cc0d7" />

