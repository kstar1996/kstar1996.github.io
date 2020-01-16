---
layout: post
title:  "Named Data Networking"
author: Eujin Kim
categories: [ computer networks ]
image: 
tags: [featured]
---

# Named Data Networking

## 1. Intro

Today I will tell you about **Named Data Networking**, a TCP/IP solution.

Let’s start by asking ourselves, what is Name Data Networking? Why should you care about it? Unlike traditional methods, NDN enables communications by named, secured data at the network layer. It was created to support the architectural mis-match of today’s Internet architecture and its actual usage.

## 2. Context and Vision

The Internet was originally designed to create a communication network between people with numeric addresses. However, in the last 15 years or so, how we use the internet has changed as well as why we use it. In the past, emails and chatting were common whereas now, websites like Netflix, Youtube, and Facebook are popular. Content is king and it has been estimated that about 80% of Internet traffic is content delivery.

Since the previous TCP/IP architecture has issues, a few experts decided to come up with a new approach to the Internet that basically optimized for a more "information-centric" network while allowing the use of almost all the properties of the Internet. NDN is an example of information centric networking, where addresses are just names where you send an "interest" for that name, and the closest entity like a router or endpoint returns data that is digitally signed.

## 3. NDN Architecture
Named data networking works by exchanging 2 types of packets. The interest packet and the data packet. The interest packet is created at the beginning. A consumer puts the name of the needed data into an Interest packet and sends it to the network. Routers use this name to forward the Interest toward the data producer. Once the Interest reaches a node that has the requested data, the node will return a Data packet that contains the name, content, and a signature by the producer’s key.

The content name is the most important part of the Interest and the Data packet. Before, with TCP/IP, we had to identify the IP address of the sending and receiving nodes in order to make a connection, but with data networking, you are able to use a hierarchical identifier. This hierarchical structure is useful for applications to represent relationships between pieces of data. For example, if I’m looking for Google’s website for recruiting, https://careers.google.com/, the identifier would be [com/google/careers] Name conventions are specific to applications but opaque to the network. For example, routers do not know the meaning of a name although they see a slash, which indicates a boundary between components. This allows each application to choose the naming scheme that fits its needs and allows the naming schemes to evolve in parallel with architecture development.

### 3-1 : Interest Packets  
Once an interest packet has been created, it follows a specific path through certain sections in a previously configured NDN router and there are three data structures. The content store, the pending interest table, and the forwarding information base. The content store is the first stop for the interest packet and this is where you are going to find interest packets that have been previously fulfilled. So once the interest packet has gone through this routing path, has been discovered and followed back, it’s going to be stored here. You will find commonly visited websites cached here. For example, if you visit google.com often, it would be sent back and stored in the CS so the next time you are searching for it, it’s easy to bring back up.

If the interest packet is not found in the content store, the router looks up the name in its pending interest table or PIT. If there is a matching entry, it records the incoming interface of this Interest in the PIT entry. So if you have sent out an interest packet for google.com but a data packet has not yet been received you are going to find it in the pending interest table.

Following the pending interest table, you’re going to see the forwarding information base or FIB. This is a routing protocol very similar to the currently used with tcp/Ip and it is the final step before the information is sent out to the web.

### 3-2 : Data Packets  
Once the information has been sent out to the web, it is returned in the form of a data packet. Data packets always take the reverse path of Interests, and goes back to the consumer. If there are no packet losses, one Interest packet results in one Data packet on each link, providing flow balance.

### 3-3 : Security  
1)  NDN solves the various networking and security issues in the tcp/ip architecture in a number of ways . In a TCP/IP connection based protocol, if a 3rd party is monitoring the packets being sent back and forth, they can use that information to get information on the IP address. Then, the 3rd party can issue false packets into the process that act like packets of the original source and gain access to the nodes.

The NDN solution to this is that there is no IP address required, but fetches data by using names as I mentioned before. A 3rd party can’t gain access to the content because NDN is not a connection based protocol.

2)  Another security issue associated with tcp/ip architecture, is the case of server attacks. Spoofing, which is one of these attacks, occurs when IP addresses associated with trusted sites are replaced with 3rd party sources. This diverts traffic to the 3rd party computer. For example. If you frequently visit google.com, and a 3rd party has diverted that IP address, the next time you access that site, they can gain access to your system. This can lead to many issues like viruses, data loss, and memory loss.

The NDN solution to this is an end-to-end data authenticity. Data producers digitally sign, and data consumers verify. For example, let’s say you were to visit your bank’s website, and you were led to log in using your username or password. If you were diverted to a 3rd party page, you could give them access to that information without even knowing it. In the case of NDN, you would be able to verify by looking at the the data packet that this is actually the website that you were diverted to.

## 4. ETC  
The NDN project is based on an application driven development approach and a number of applications are being developed to validate the architecture. Applications like video streaming, real-time conferencing, automation system, and vehicular networking have been developed and this has lead to the features like name space, trust model, and in-network storage which has been made into a library.

Finally, research on the routing and forwarding protocol is the most needed in the NDN protocol. Fortunately, the concept of the existing IP routing protocol can be reused by replacing IP prefixes with name prefixes.

To recap, NDN is one of several attempts to increase the efficiency of today’s Internet network protocols with the various kinds of distributed networks increasing. 
