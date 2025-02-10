# Learn Ethical Hacking from Scratch

## Introduction 
This course focused on teaching students ethical hacking fundamentals. No prior knowledge was necessary, and by the end, it assisted in achieving a high intermediate level of computer system hacking in a manner like that of Black Hat hackers. In addition, I gained knowledge on how to protect systems from attacks. 
This was a very hands-on course that paid close attention to theory. In order for people to practice hacking safely and legally, it first clarified some terminology and showed how to set up the necessary software and create a penetration testing lab. Then came the penetration testing and network hacking sections, where I learned how networks operate, how devices communicate with one another, and how to take advantage of this method of communication to manipulate all the connections around us by breaking Wi-Fi encryption and obtaining Wi-Fi keys to access Wi-Fi networks. 
As previously mentioned, there were four sections in this course. These segments covered hacking of networks, gaining access, post-exploitation, and websites. In this report, I'll talk about accessing networks and hacking them. 
## Network Hacking 
The network consists of a number of clients that are linked to one another. Clients typically connect to a network to share data or resources. The Internet is a good example of a resource to access. To access the Internet, we constantly connected to Wi-Fi and wired networks. Now, the fundamentals of how wired and wireless networks operate are the same. A component that is regarded as a server in networks exists. Now, in a lot of situations, like in your home network, this server serves as our router. This is also referred to as an access point. Now, the resource can only be accessed by this router, server, or access point.  Therefore, despite connecting to the network, none of these clients can access the resource directly. The access point is their only means of gaining access to the resource. So, for illustration, let's use my client #1. Additionally, I have a cable or wireless connection to the internet and my home network. I then launch my browser and enter www.facebook.com. My computer will send an inquiry to accesspointasking.com as a result. In this case, the resource is the Internet, and the access point has access to it. As a result, it will search for facebook.com. As a result, I will see the website loading on my browser after it receives the response from google.com and forwards it to my computer. As a result, if I go to my home router and take a closer look at it, I'll see that it is physically connected to the wall with a cable at the back. It receives its Internet access in this manner. Since none of my computers are connected to your network, it is the only device that has direct access to the resource. Without the router, none of the networked computers can access the resource or the Internet, devoid of the access point. The resource must thus pass through the router for each of these connected clients. Currently, packets are used to transfer data between clients and access points. To understand these arrows, imagine them as a series of packets that are being sent as requests and responses between the client and the router. These packets are currently sent over Wi-Fi networks. if our computer has a wireless card. By utilizing a few tools, we will be able to track those packets.
![example of a network](https://github.com/ashiq4321/ethicalHacking/blob/99e44353150277fcee72c6214054f9fd8d9adcbb/example%20of%20a%20network.png)

### Prerequisite
1.	Installed VMware.
2.	Installed Kali Linux in it.
3.	I bought a wireless adapter and installed it in my VMware, named rtl8811cu.

### Wireless network configurations 
To keep myself anonymous, I changed my Mac address first. The steps are shown below.
1.	ifconfig (to see the interface) and choose “wlan0“wireless network
2.	Downing the adapter with: ifconfig wlan0 down (wlan0 is the adapter name)
3.	ifconfig wlan0 hw ether 00:11:22:33:44:55 (00:11:22:33:44:55 is the new mac address)
4.	ifconfig wlan0 up


### Packet Sniffing using airodump-ng
### Deauthentication Attack 
## Gaining WPA/WPA2 Network Access 
### WPS Pixie-Dust
### WPS Null PIN
### WPS PIN Attack 
### PMKID Capture and Cracking
### WPA Handshaking 
## Findings 
## Conclusion 
## Reference 
