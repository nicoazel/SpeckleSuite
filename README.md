# SpeckleSuite

This is an attempt to build a consolidated walkthrough for setting up a ubuntu 16.04 droplet and installing:
  * speckleAdmin
  * speckleServer
  * speckleViewer

with a [NGINX](https://www.nginx.com/) reverse proxy server, and synchronized URL's

#### Background

The steps for this are taken from [Digital Ocean](www.digitalocean.com) tutorials and [Speckle](https://speckle.works) documents. I have modified them or outlined them to focus on running a server exclusively for Speckle. This is intended for myself and other novice developers/users.

While I have been using digitalocean for their costs and excellent noob friendly tutorials, these steps should work on any Virtual Privat Server (VPS)

___

## 1. Droplet

Im using a `Ubuntu 16.04.5 x64 1Gb 1vCPU 25 GB Standard Droplet`

Set it up with *SSH* from [PuttyGen](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html) and access it through [Putty](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html).

### 1.1 Initial Server Setup
Set up a `Speck` ***super user*** with Admin privileges and get a `ufw` ***fire wall*** setup

* [My Quick Summary](/initialsetup.md)
* [Digital Ocean Initial Server Setup](https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-16-04)

### 1.2 Install Nginx

Install and get running [NGINX](https://www.nginx.com/) as a ***reverse proxy server***, for three ***server blocks***

* [Digital Ocean Nginx Install](https://www.digitalocean.com/community/tutorials/how-to-install-nginx-on-ubuntu-16-04)
* [Digital Ocean Nginx Server Blocks](https://www.digitalocean.com/community/tutorials/how-to-set-up-nginx-server-blocks-virtual-hosts-on-ubuntu-16-04)

### 1.3 Set Up DNS
not going to discuss here other than some basics:
* ***domain*** is an `A` record set to your IP address on port 80
* ***sub-domain*** can is a `cname` record set to @.

###### I need to look into this for a sec and see about the ports per different speck apps....

### 1.4 Set Up HTTPS with Certbot
Set up SSL for encrypted connections, its free and its comforting to see the lock up in the corner.
its also crazy easy to do:
[Digital Ocean Certbot Tutorial](https://www.digitalocean.com/community/tutorials/how-to-secure-nginx-with-let-s-encrypt-on-ubuntu-16-04)


___




# 2. Speckle Apps

ok, now on to the simplicity of getting the speckle suite running....

Getting the speckle server is straight forward but I still don't actually know where the other apps are supposed to be installed. Im sure its documented out there somewhere...




### 2.1 Speckle Server


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




### 2.2. Speckle Admin



```
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build
```


### 2.3 Speckle Viewer
It is worth noting that registered users have access to a speckle viewer from their user page...
Having a personal Speckle Viewer hosted on a server may be of value for publicly accessible models?

```bash
# install dependencies
npm install

# serve with hot reload at localhost:8888 (8080 is taken by the local speckle server instance 💯)
npm run dev

# build for production with minification
npm run build
```

You will need to modify the `./dist/config.js` file to fit your deployment details. It’s rather self-descriptive, it just exports a global object with info:
```js
var SpkAppConfig = {
  serverUrl: 'http://localhost:8080',
  allowGuestAccess: true,
  logoUrl: 'https://company.png'
}

window.SpkAppConfig = SpkAppConfig
```

# Credits

I'm an aspiring developer but this is really pointing to other peoples work.
a big thanks goes to Dimitrie A. Stefanescu and the Speckle Project Contributors.

Also a thanks to digital ocean for providing excellent tutorials and documentation to help get novice backend developers familiar with the basics.

# The End
