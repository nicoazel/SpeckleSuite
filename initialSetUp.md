### 1.1 Initial Server Setup
Set up a `Speck` ***super user*** with Admin privileges and get a `ufw` ***fire wall*** setup
[Digital Ocean initial server Setup](https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-16-04)

```bash
#Add user
usermod -aG sudo speck
```

```bash
#switch user
su - speck
```
```bash
#create ssh directory
mkdir ~/.ssh
chmod 700 ~/.ssh
```
```bash
#create key file
nano ~/.ssh/authorized_keys
#past key from PuttyGen
#-y for yes
# enter for confirm
```
```bash
#restrict access
chmod 600 ~/.ssh/authorized_keys
```
```bash
# return to root
exit
```
```bash
#ssh daemon configure
sudo nano /etc/ssh/sshd_config
#Set the following to look like this:
#PasswordAuthentication no
#PubkeyAuthentication yes
#ChallengeResponseAuthentication no
```
```bash
# reload ssh daemon:
sudo systemctl reload sshd
```

Setting Up the basic UFW firewall
need to insure ssh access:

```bash
# current app with access - should see OpenSSH
sudo ufw app list
```

```bash
# allow open ssh
sudo ufw allow OpenSSH
```

```bash
#enable firewall
sudo ufw enable
#type "y" and press ENTER
```

```bash
# quick status check - oppenSSH allow
sudo ufw status
```

Thats the end of the inital setup of a super user and ssh firewall
