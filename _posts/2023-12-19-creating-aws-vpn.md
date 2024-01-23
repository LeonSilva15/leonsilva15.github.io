---
layout: post
title: Creating an AWS VPN
date: 2023-12-19
---

Recently I built my own desktop computer for my personal projects, but I didn't want to be sitted on my desktop all day while working on it and only using my laptop with its limited resources wasn't an option, so I decided to deploy a VPN to connect both my desktop and laptop computers to it and connect each other using ssh.

### 1. Select the EC2 service
First we selet the EC2 service **not** the EC2 Image Builder
![Select EC2 Service](/assets/2023-12-19/1.png "Select EC2 Service")

### 2. Click on Launch Instance
Launch the instance, this will take us to a form
![Launch Instance](/assets/2023-12-19/2.png "Click on Launch Instance")

### 3. Fill the form
First, add a name to your VPN server
![Server name](/assets/2023-12-19/3.png "Add Server Name")

In the OS Image input type **OpenVPN** and hit Enter to look for our image
![Server name](/assets/2023-12-19/4.png "Add Server Name")

Click on the AWS Marketplace AMIs tab and select the image named **OpenVPN Access Server** with no connected devices specified
![Select the image](/assets/2023-12-19/5.png "Select the Image")

Before clicking on continue make sure you have the Free tier elegible product
![Free tier image](/assets/2023-12-19/6.png "Continue with the Free tier Image")

Now select a Free tier instance type
![Free tier image](/assets/2023-12-19/7.png "Continue with the Free tier Image")

Then create a new Key pair for login, this will download a pem file used by the vpn
![Free tier image](/assets/2023-12-19/8.png "Continue with the Free tier Image")

Lastly, in the rigth menu click on Launch instance
![Launch instance](/assets/2023-12-19/9.png "Launch Instance")


### 4 Configure your VPN server
If AWS didn't take you directly to the connect section, go to the instances section in your EC2 dashboard
![Launch instance](/assets/2023-12-19/10.png "Launch Instance")

Then click on your instance id and in the following page click on "Connect"

Now follow the instructions in the SSH section. The steps will require you to modify the downloaded file permissions
```sh
chmod 400 <path to your .pem file>
```

Then you will be asked to connect to your server using ssh
```sh
ssh -i "<path to your .pem file>" root@ec2-<your-instance-ip>.compute-1.amazonaws.com
```
if you get any error, try connecting with openvpnas user
```sh
ssh -i "<path to your .pem file>" openvpnas@ec2-<your-instance-ip>.compute-1.amazonaws.com
```

Now click enter until requested the password for openvpn. If you missed it, just copy the default password provided in the terminal.

After doing this, in your browser go to your server ip address + `:943/admin` e.g. `http://<your-openvpn-ip>:943/admin`

Enter your credentials and sign in
![Enter the admin panel](/assets/2023-12-19/11.png "Enter the admin panel")

Go to your VPN Settings
Enter your credentials and sign in
![VPN settings](/assets/2023-12-19/12.png "VPN settings")

In the routing section
- Turn "Should client Internet traffic be routed through the VPN?" if you want a more secure navigation, although this would consume more bandwidth but we want to keep our service in the free tier, so let's leave it in No
- Turn "Should clients be allowed to access network services on the VPN gateway IP address?" if you want clients to communicate with each other
![Routing settings](/assets/2023-12-19/13.png "Routing settings")

### 5. Connect to your VPN server
Just open in your browser `https://<your-openvpn-ip>:943/?src=connect`.
There you can download the client or the vpn profile.
![VPN Client](/assets/2023-12-19/14.png "VPN Client")


#### Some useful resources:
- [Setup a FREE VPN server in the cloud (AWS)](https://www.youtube.com/watch?v=m-i2JBtG4FE)
- [OpenVPN Access Server Admin Web UI First Login](https://openvpn.net/access-server-manual/access-server-web-admin-ui-first-login/)
- [How do I connect a VPN client device to OpenVPN](https://openvpn.net/vpn-server-resources/connecting/)
