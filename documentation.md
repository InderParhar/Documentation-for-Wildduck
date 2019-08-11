

# How to install Windduck and Wildduck-mta to your server. 

## Introduction 
WildDuck is a scalable no-SPOF IMAP/POP3 mail server. WildDuck uses a distributed database (sharded + replicated MongoDB) as a backend for storing all data, including emails.
WildDuck tries to follow Gmail in product design. If there's a decision to be made then usually the answer is to do whatever Gmail has done.

## Prerequisites

1. Information about the server, including the private key.
2. Putty software - It will be an intermediate between your system and the server. 
3. Get links to the wildduck and WildDuck-mta repositories
4. Python.
5. MongoDB to store all data
6. Redis for pubsub and counters
7. Node.js at least version 8.0.0


## Step 1 - Installing Putty. 

- **Note - You need to have information about the server by this time, this will be provided to you by the User.**



1. Download Putty as per your system's Configuration by going to this link [Putty](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html (Putty.exe))

2. Install the putty software on your system.

## Step 2 - Gaining access to the server.

1. Open the putty configuration window. 
2. Enter the Hostname or the IP address provided to you by the User like ( example.com or 198.54.63.65)
3. After that look for SSH under the connection category.
4. On expanding SSH, look for Auth, in there you will see a window  to browse and upload the Private key provided to you by the User ( It will a .SSH file )
5. Once you open that file, it will open a window that will ask you to log in.
6. Log in as root, then it will authenticate your private key with the public key and if the provided information is correct, you will gain access to their server.

## Step 3 - Installing Python. 

- **Note - Create a directory and make it a working directory using commands - mkdir and cd**

1. Using apt command install python 
    
    - apt install python
    - this will install python globally throughout the server and can be used in any directory 

## Step 4 - Installing Nodejs using NVM

- *Use of **Nodejs** - Node.js is primarily used for non-blocking, event-driven servers, due to its single-threaded nature. It's used for traditional web sites and back-end API services, but was designed with real-time, push-based architectures in mind.*

- ***nvm** stands for Node Version Manager. As the name suggests, it helps you manage and switch between different Node versions with ease. It provides a command line interface where you can install different versions with a single command, set a default, switch between them*
1. Run Nvm installer using 
    - curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.34.0/install.sh | bash
    - wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.34.0/install.sh | bash

2. To verify Installation use 
    - command -v nvm (expected outcome - nvm)
3. To check what versions of Node are currently installed use(if any):
    - nvm ls
4. Install latest version of Nodejs (Current version - v10.16.2)
    - nvm install v10.16.2

## Step 5 - Installing MongoDB. 

- *Use of **MongoDB** - MongoDB is a DB server which uses nosql, It is used to implement a data store that provides high performance, high availability, and automatic scaling. MongoDB uses JSON or BSON documents to store data.* 

1. Use this command to synchronize the package index files from their sources again.
    - apt update
2. Install Mongo using :
    - apt install mongodb 

## Step 6 - Installing Redis. 

- *Use of **Redis** - It is  an open-source, in-memory, data structure server is frequently used as a distributed shared cache (in addition to being used as a message broker or database) because it enables true statelessness for an applications' processes while reducing duplication of data or requests to external data sources.*

1.  Use this command to synchronize the package index files from their sources again
    - apt update
2. Install Redis using :
    - apt install redis-server
3. run 
    - nano /etc/redis/redis.conf (make changes in your config file as per your system)
        - supervised directive is set to No by default, change it to systemd.
4. Restart redis after changes
    - systemctl restart redis.service
5. To check if it has been successfully installed run 
    - systemctl status redis


## Step 7 - Cloning both repositories. 

1. Open the Git repositories on your web browser and copy the git HTTPS link.
2. Clone using : 
    - git clone https://github.com/nodemailer/wildduck.git (for Wildduck)
    - git clone https://github.com/nodemailer/wildduck-mta.git (for Wildduck-mta)

- **Note - If you try to run your repositories before instaling MongoDB then you will see that it shows a requirement on port 27017, which means that MongoDB is not installed.**

## Step 8 - Install Dependencies in Wildduck.

- **Note - Change directory to wildduck using cd**

1. Installing all dependencies in package.json in wildduck repository
    -  npm install --production  or npm i --production

## Step 9 - Install pm2.
- *Use of **Pm2** - PM2 is a production process manager for Node.js applications with a built-in load balancer. It allows you to keep applications alive forever, to reload them without the downtime and to facilitate common system admin tasks. This will help us run the project in the background.*

1. Run 
    - npm i pm2 -g (g will install pm2 globally ie it can be accessed by other directories as well.)
2. pm2 commands 
    1. list all process
        - pm2 list
    2. log 
        - pm2 log
## Step 10 - Run Wildduck.
1. Run using pm2:
    - pm2 start . --name wildduck -i 1( 1 for the number of clusters to run in)
2. To check if it has activated
    - pm2 list
3. Check Logs
    - pm2 log

## Step 11 - Run Wildduck-mta

- **Note - Run this after you have successfully installed Wilduck**

1. Run using pm2:
    - pm2 start . --name wildduck-mta -i 1( 1 for the number of clusters to run in)
2. To check if it has activated
    - pm2 list
3. Check Logs
    - pm2 log

**Installation of WildDuck and WildDuck-mta completed**
********************************************
********************************************


