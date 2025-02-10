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
1. **Check the interface:**
   ```bash
   ifconfig
choose “wlan0“ wireless network

2. **Downing the adapters**
   ```bash
   ifconfig wlan0 down
wlan0 is the adapter name

3. **set new mac address**
   ```bash
   ifconfig wlan0 hw ether 00:11:22:33:44:55
   
00:11:22:33:44:55 is the new mac address

4. **Active the adapters**
   ```bash
   ifconfig wlan0 up
![wireless network adapter ‘wlan0‘configuration](https://github.com/ashiq4321/ethicalHacking/blob/8242a99dffa9017388de4353c73f51522739fe27/wireless%20network%20adapter%20%E2%80%98wlan0%E2%80%98configuration.png)

To capture packets (even if it sent another device), I changed the wireless mode into monitor mode. The steps are shown below.

1. **Active the adapters**
   ```bash
   ifconfig wlan0 down
   airmon-ng check kill
   iwconfig wlan0 mode monitor
   Ifconfig wlan0 up
![changed the wireless mode into monitor mode!](https://github.com/ashiq4321/ethicalHacking/blob/8242a99dffa9017388de4353c73f51522739fe27/changed%20the%20wireless%20mode%20into%20monitor%20mode.png)

### Packet Sniffing using airodump-ng
check the available network with band 2.4GHz near me! 

1. **Available network with band 2.4GHz**
   ```bash
   airodump-ng wlan0

2. **Available network with band 5GHz**
   ```bash
   airodump-ng --band a wlan0

3. **Available network with both band 5GHz**
   ```bash
   airodump-ng --band abg wlan0

![available networks](https://github.com/ashiq4321/ethicalHacking/blob/8242a99dffa9017388de4353c73f51522739fe27/available%20networks.png)

selected the below network for further attack:
| BSSID             | PWR | Beacon | #Data | #/s | CH | MB  | ENC  | CIPHER | AUTH | ESSID       |
|-------------------|-----|--------|-------|-----|----|-----|------|--------|------|-------------|
| 64:64:4A:91:5A:D6 | -48 | 16     | 4     | 0   | 1  | 130 | WPA2 | CCMP   | PSK  | Xiaomi_5AD5 |

4. **dump all client to the network  64:64:4A:91:5A:D6**
   ```bash
   airodump-ng --bssid 64:64:4A:91:5A:D6 --channel 1 --write test wlan0

![available client to the network  64:64:4A:91:5A:D6](https://github.com/ashiq4321/ethicalHacking/blob/55f7c83fe408f4a494054c0807f6c3616829c0d5/available%20Clients%20in%20network%20%E2%80%9C64-64-4A-91-5A-D6%E2%80%9D.png)

| Avaialble Clients |
|-------------------|
| E8:FB:1C:DC:1A:E1 |
| 5C:E9:1E:8F:49:3E |

### Deauthentication Attack
Client “5C:E9:1E:8F:49:3E” is selected to disconnect from the network. Lets start the Deauthentication Attack 
1. **Dump all the available clients**
   ```bash
   airodump-ng --bssid 64:64:4A:91:5A:D6 --channel 1 wlan0

2. **active the replay attack**
   ```bash
   aireplay-ng --deauth 10000000 -a 64:64:4A:91:5A:D6 -c 76:6C:6D:84:BB:AE wlan0

Finally, client “5C:E9:1E:8F:49:3E” disconnected from the network.

![Client “5C:E9:1E:8F:49:3E” disconnected from the network](https://github.com/ashiq4321/ethicalHacking/blob/c9bb4301a24d1811f755578a2384c00fb11f458e/Client%20%E2%80%9C5C-E9-1E-8F-49-3E%E2%80%9D%20disconnected%20from%20the%20network.png)

We can access/create the handshake by performing deauth attack and packet sniffing command simultaneously. In that case , the packet only includes the data of the handshake. The handshake doesn’t contain data that helps to recover the key, but it can be used if a key is valid or not.


## Reference 
1.	Course link: [Couser link](https://concordia.udemy.com/course/learn-ethical-hacking-from-scratch/)
2.	Video that helped to install Kali in M2 arm-64 MacBook: [install kali in MacBook] (https://www.youtube.com/watch?v=tA50zg7D4mg)
3.	Video that helped to install Adapter in VM:[install adapter](https://www.youtube.com/watch?v=hEXwOkyYNL0)

# To be Continued
## Gaining WPA/WPA2 Network Access 
### WPS Pixie-Dust
### WPS Null PIN
### WPS PIN Attack 
### PMKID Capture and Cracking
### WPA Handshaking 
## Findings 
## Conclusion 

