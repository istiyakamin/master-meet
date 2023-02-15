# master-meet
Master Meet - Secure, Simple and Scalable Video Conferences that you use as a standalone app or embed in your web application.

## Setup

```
sudo apt-get update
sudo apt-get upgrade
sudo apt install apt-transport-https
sudo apt-add-repository universe
```

### Domain of your server and set up DNS
Decide what domain your server will use. For example, meet.master.com.bd.

Set a DNS A record for that domain, using:

 - your server's public IP address, if it has its own public IP; or
 - the public IP address of your router, if your server has a private (RFC1918) IP address (e.g. 192.168.1.2) and connects through your router via Network Address Translation (NAT).


### SET HOSTNAME 
```
sudo hostnamectl set-hostname meet.master.com.bd
```

### Add the Prosody package repository
```
echo deb http://packages.prosody.im/debian $(lsb_release -sc) main | sudo tee -a /etc/apt/sources.list
wget https://prosody.im/files/prosody-debian-packages.key -O- | sudo apt-key add -
apt install lua5.2
```

### Add the Jitsi package repository
```
curl https://download.jitsi.org/jitsi-key.gpg.key | sudo sh -c 'gpg --dearmor > /usr/share/keyrings/jitsi-keyring.gpg'
echo 'deb [signed-by=/usr/share/keyrings/jitsi-keyring.gpg] https://download.jitsi.org stable/' | sudo tee /etc/apt/sources.list.d/jitsi-stable.list > /dev/null
```

### Setup and configure your firewall
The following ports need to be open in your firewall, to allow traffic to the Jitsi Meet server:

 - 80 TCP => For SSL certificate verification / renewal with Let's Encrypt. Required
 - 443 TCP => For general access to Jitsi Meet. Required
 - 10000 UDP => For General Network Audio/Video Meetings. Required
 - 22 TCP => For Accessing your Server using SSH (change the port accordingly if it's not 22). Required
 - 3478 UDP => For querying the stun server (coturn, optional, needs config.js change to enable it).
 - 5349 TCP => For fallback network video/audio communications over TCP (when UDP is blocked for example), served by coturn. Required
 
 ```
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp
sudo ufw allow 10000/udp
sudo ufw allow 22/tcp
sudo ufw allow 3478/udp
sudo ufw allow 5349/tcp
sudo ufw enable
```
#### N.B: IF YOU'RE USING AWS OR ANY CLOUD INFASTRUCTION MUST CHECK YOUR FIREWALE FROM CLOUD END;

### Check Firewall 
```
sudo ufw status verbose
```

### TLS Certificate
WILL BE UPDATE SOON

### Install Jitsi Meet
If you are already running Nginx on port 443 on the same machine, turnserver configuration will be skipped as it will conflict with your current port 443.
```
sudo apt install jitsi-meet
```

Launch a web browser (such as Firefox, Chrome or Safari) and enter the hostname or IP address from the previous step into the address bar.

If you used a self-signed certificate (as opposed to using Let's Encrypt), your web browser will ask you to confirm that you trust the certificate.

### CHEERS!!!

