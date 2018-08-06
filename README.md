# SpeckleSuite

This is an attempt to build a walkthrough for setting up a ubuntu 16.x droplet and installing:
  * speckleAdmin
  * speckleServer
  * speckleViewer

with a [NGINX](https://www.nginx.com/) reverse proxy server, and synchronized URL's


## Background

The steps for this are taken from [Digital Ocean](www.digitalocean.com) tutorials and modified to focus on running a server exclusively for Speckle.


## 1. Droplet

Im using a `Ubuntu 16.04.5 x64 1Gb 1vCPU 25 GB Standard Droplet`

Set it up with *SSH* from [PuttyGen](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html) and access it through [Putty](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html).

### 1.1 Initial Server Setup
Set up a `Speck` ***super user*** with Admin privileges and get a `ufw` ***fire wall*** setup
[Digital Ocean initial server Setup](https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-16-04)

### 1.2 install NGINX
install [nginx](https://www.nginx.com/) and then get three ***server blocks*** up and running

[nginx install](https://www.digitalocean.com/community/tutorials/how-to-install-nginx-on-ubuntu-16-04)

[nginx server blocks](https://www.digitalocean.com/community/tutorials/how-to-set-up-nginx-server-blocks-virtual-hosts-on-ubuntu-16-04)

### 1.3 set up your DNS
not going to discuss here other than some basincs:
... ***domain*** is set to your IP address @ port 80 as an `A record`
... ***sub-domain*** can is a cname record set to @.

##### I need to look into this for a sec and see about the ports per different speck apps....

### 1.4 set up https with Certbot

[Digital Ocean Certbot Tutorial](https://www.digitalocean.com/community/tutorials/how-to-secure-nginx-with-let-s-encrypt-on-ubuntu-16-04)




# 2. Speckle install

ok, now on to the simplicity of getting the speckle suite running....

## 2.1 Speckle Server


1) Install mongodb, redis servers and npm:

       $ sudo apt-get install mongodb redis npm

2) Clone SpeckleServer and run npm to install the needed nodejs packages:

       $ git clone https://github.com/speckleworks/SpeckleServer.git
       $ cd SpeckleServer
       $ npm install

3) Follow the instructions in `.env-base` file to configure your server.

4) Start mongo (create a folder somewhere to store the db):

       $ mongodb --dbpath /path/to/some/folder

5) Start redis in another terminal:

       $ redis-server

6) Check that both mongo and redis are running OK and that you can connect to them with these two clients:

       $ mongo
       $ redis-cli

7) Start Speckle in a third terminal:

       $ node server.js

## 2.2. Speckle Admin



```
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build
```

""

## 2.3 Speckle Viewer
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
