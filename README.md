# SpeckleSuite

This is an attempt to build a walkthrough for setting up a ubuntu 16.x droplet and installing:
  * speckleAdmin
  * speckleServer
  * speckleViewer

with a [NGINX](https://www.nginx.com/) reverse proxy server, and synchronized URL's


## Background

The steps for this are taken from [Digital Ocean](www.digitalocean.com) tutorials and modified to be lead directly to running a server exclusively for Speckle.


## Droplet

Im using a `Ubuntu 16.04.5 x64 1Gb 1vCPU 25 GB Standard Droplet`

Set it up with *SSH* from [PuttyGen](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html) and access it through [Putty](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html).

### Initial Server Setup
Set up a `Speck` ***super user*** with Admin privileges and get a `ufw` ***fire wall*** setup
[Digital Ocean initial server Setup](https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-16-04)

### install NGINX
install nginc and then get three ***server blocks*** up and running
[nginx instal](https://www.digitalocean.com/community/tutorials/how-to-install-nginx-on-ubuntu-16-04)

[nginx server blocks](https://www.digitalocean.com/community/tutorials/how-to-set-up-nginx-server-blocks-virtual-hosts-on-ubuntu-16-04)

### set up your DNS
not going to discuss here other than some basincs:
... ***domain*** is set to your IP address @ port 80 as an `A record`
... ***sub-domain*** can is a cname record set to @.

#####I need to look into this for a sec and see about the ports per different speck apps....

### set up https with Certbot

[Digital Ocean Certbot Tutorial](https://www.digitalocean.com/community/tutorials/how-to-secure-nginx-with-let-s-encrypt-on-ubuntu-16-04)


#Speckle install

ok, now on to the simplicity of getting the speckle suite running....

## Speckle Server


1) Install mongodb, redis servers and npm:

       $ sudo apt-get install mongodb redis npm

2) If you don't want both the redis and mongo servers running all the time (For ex. if you are just testing), disable both startup scripts (If you wish to leave both running automatically, skip to step 4):

       $ sudo systemctl disable mongodb
       $ sudo systemctl disable redis-server`

3) And stop both mongo and redis processes that were started automatically by apt-get:

       $ sudo systemctl stop mongodb
       $ sudo systemctl stop redis-server

4) Clone SpeckleServer and run npm to install the needed nodejs packages:

       $ git clone https://github.com/speckleworks/SpeckleServer.git
       $ cd SpeckleServer
       $ npm install

5) Follow the instructions in `.env-base` file to configure your server.

6) Start mongo (create a folder somewhere to store the db):

       $ mongodb --dbpath /path/to/some/folder

7) Start redis in another terminal:

       $ redis-server

8) Check that both mongo and redis are running OK and that you can connect to them with these two clients:

       $ mongo
       $ redis-cli

9) Start Speckle in a third terminal:

       $ node server.js

## Speckle Admin



```
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build
```

""

## Speckle Viewer
It is worth noting that registered users have access to a speckle viewer from their user page...
Having a personal Speckle Viewer hosted on a server may be of value for publicly accessible models?


# The End




example of md block code....
``` bash
# install dependencies
npm install

# serve with hot reload at localhost:9090
npm run dev

# build for production with minification
npm run build
```
