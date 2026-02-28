## IPv6 Static Routing Lab with Cisco Packet Tracer
## 📋 Project Overview
This lab demonstrates the implementation of IPv6 static routing in a complex network topology using Cisco Packet Tracer. The network consists of multiple routers, switches, and end devices configured with IPv6 addressing and static routes to enable end-to-end connectivity.

## 🏗️ Network Topology
The network is divided into multiple subnets with the base IPv6 prefix: 2001:CAFE:ABCD::/64

## Subnet Allocation:
2001:CAFE:ABCD:0001::/64 - Connected to R-01 via SW-01
2001:CAFE:ABCD:0002::/64 - Connected to R-01 via SW-02
2001:CAFE:ABCD:0003::/64 - Connected to R-02 via SW-03
2001:CAFE:ABCD:0004::/64 - Connected to R-02 via SW-04
2001:CAFE:ABCD:0005::/64 - Point-to-point link between R-01 and R-02
2001:CAFE:ABCD:0006::/64 - Point-to-point link between R-02 and R-03
2001:CAFE:ABCD:0007::/64 - Point-to-point link between R-03 and R-04
2001:CAFE:ABCD:0008::/64 - Connected to R-04 via SW-05
2001:CAFE:ABCD:0009::/64 - Point-to-point link between R-03 and R-05
2001:CAFE:ABCD:000A::/64 - Connected to R-05 via SW-06
2001:CAFE:ABCD:000B::/64 - Connected to R-05 via SW-07

## 🔧 Device Configurations
## Router R-01
##
R-01>enable
R-01#show running-config
Building configuration...

Current configuration : 1367 bytes
!
version 15.4
no service timestamps log datetime msec
no service timestamps debug datetime msec
no service password-encryption
!
hostname R-01
!
!
!
!
!
!
!
!
ip cef
ipv6 unicast-routing
!
no ipv6 cef
!
!
!
!
!
!
!
!
!
!
!
!
spanning-tree mode pvst
!
!
!
!
!
!
interface GigabitEthernet0/0/0
 description SW-01-Link
 no ip address
 duplex auto
 speed auto
 ipv6 address 2001:CAFE:ABCD:1::1/64
!
interface GigabitEthernet0/0/1
 description SW-02-Link
 no ip address
 duplex auto
 speed auto
 ipv6 address 2001:CAFE:ABCD:2::1/64
!
interface GigabitEthernet0/0/2
 no ip address
 duplex auto
 speed auto
 shutdown
!
interface Serial0/1/0
 description R-02-Link
 no ip address
 ipv6 address 2001:CAFE:ABCD:5::1/64
 clock rate 64000
!
interface Serial0/1/1
 no ip address
 clock rate 2000000
!
interface Vlan1
 no ip address
 shutdown
!
ip classless
!
ip flow-export version 9
!
ipv6 route 2001:CAFE:ABCD:3::/64 2001:CAFE:ABCD:5::2
ipv6 route 2001:CAFE:ABCD:4::/64 2001:CAFE:ABCD:5::2
ipv6 route 2001:CAFE:ABCD:6::/64 2001:CAFE:ABCD:5::2
ipv6 route 2001:CAFE:ABCD:7::/64 2001:CAFE:ABCD:5::2
ipv6 route 2001:CAFE:ABCD:9::/64 2001:CAFE:ABCD:5::2
ipv6 route 2001:CAFE:ABCD:8::/64 2001:CAFE:ABCD:5::2
ipv6 route 2001:CAFE:ABCD:A::/64 2001:CAFE:ABCD:5::2
ipv6 route 2001:CAFE:ABCD:B::/64 2001:CAFE:ABCD:5::2
!
!
!
!
!
!
line con 0
!
line aux 0
!
line vty 0 4
 login
!
!
!
end


R-01#
## 
## Router R-02
R-02>enable
R-02#show running-config
Building configuration...

Current configuration : 1336 bytes
!
version 15.4
no service timestamps log datetime msec
no service timestamps debug datetime msec
no service password-encryption
!
hostname R-02
!
!
!
!
!
!
!
!
ip cef
ipv6 unicast-routing
!
no ipv6 cef
!
!
!
!
!
!
!
!
!
!
!
!
spanning-tree mode pvst
!
!
!
!
!
!
interface GigabitEthernet0/0/0
 description SW-03-Link
 no ip address
 duplex auto
 speed auto
 ipv6 address 2001:CAFE:ABCD:3::1/64
!
interface GigabitEthernet0/0/1
 description SW-04-Link
 no ip address
 duplex auto
 speed auto
 ipv6 address 2001:CAFE:ABCD:4::1/64
!
interface GigabitEthernet0/0/2
 no ip address
 duplex auto
 speed auto
 shutdown
!
interface Serial0/1/0
 description R-01-Link
 no ip address
 ipv6 address 2001:CAFE:ABCD:5::2/64
!
interface Serial0/1/1
 description R-03-Link
 no ip address
 ipv6 address 2001:CAFE:ABCD:6::2/64
!
interface Vlan1
 no ip address
 shutdown
!
ip classless
!
ip flow-export version 9
!
ipv6 route 2001:CAFE:ABCD:7::/64 2001:CAFE:ABCD:6::1
ipv6 route 2001:CAFE:ABCD:8::/64 2001:CAFE:ABCD:6::1
ipv6 route 2001:CAFE:ABCD:9::/64 2001:CAFE:ABCD:6::1
ipv6 route 2001:CAFE:ABCD:A::/64 2001:CAFE:ABCD:6::1
ipv6 route 2001:CAFE:ABCD:B::/64 2001:CAFE:ABCD:6::1
ipv6 route 2001:CAFE:ABCD:1::/64 2001:CAFE:ABCD:5::1
ipv6 route 2001:CAFE:ABCD:2::/64 2001:CAFE:ABCD:5::1
!
!
!
!
!
!
line con 0
!
line aux 0
!
line vty 0 4
 login
!
!
!
end


R-02#

## Router R-03

R-03>
R-03>enable
R-03#show running-config
Building configuration...

Current configuration : 1514 bytes
!
version 16.6.4
no service timestamps log datetime msec
no service timestamps debug datetime msec
no service password-encryption
!
hostname R-03
!
!
!
!
!
!
!
!
no ip cef
ipv6 unicast-routing
!
no ipv6 cef
!
!
!
!
!
!
!
!
!
!
!
!
spanning-tree mode pvst
!
!
!
!
!
!
interface GigabitEthernet0/0/0
 no ip address
 duplex auto
 speed auto
 shutdown
!
interface GigabitEthernet0/0/1
 no ip address
 duplex auto
 speed auto
 shutdown
!
interface GigabitEthernet0/0/2
 no ip address
 duplex auto
 speed auto
 shutdown
!
interface Serial0/1/0
 no ip address
 clock rate 2000000
 shutdown
!
interface Serial0/1/1
 description R-02-Link
 no ip address
 ipv6 address 2001:CAFE:ABCD:6::1/64
 clock rate 64000
!
interface Serial0/2/0
 description R-04-Link
 no ip address
 ipv6 address 2001:CAFE:ABCD:7::1/64
 clock rate 64000
!
interface Serial0/2/1
 description R-05-Link
 no ip address
 ipv6 address 2001:CAFE:ABCD:9::1/64
 clock rate 64000
!
interface Vlan1
 no ip address
 shutdown
!
ip classless
!
ip flow-export version 9
!
ipv6 route 2001:CAFE:ABCD:1::/64 2001:CAFE:ABCD:6::2
ipv6 route 2001:CAFE:ABCD:2::/64 2001:CAFE:ABCD:6::2
ipv6 route 2001:CAFE:ABCD:5::/64 2001:CAFE:ABCD:6::2
ipv6 route 2001:CAFE:ABCD:3::/64 2001:CAFE:ABCD:6::2
ipv6 route 2001:CAFE:ABCD:4::/64 2001:CAFE:ABCD:6::2
ipv6 route 2001:CAFE:ABCD:8::/64 2001:CAFE:ABCD:7::2
ipv6 route 2001:CAFE:ABCD:A::/64 2001:CAFE:ABCD:9::2
ipv6 route 2001:CAFE:ABCD:B::/64 2001:CAFE:ABCD:9::2
!
!
!
!
!
!
line con 0
!
line aux 0
!
line vty 0 4
 login
!
!
!
end


R-03#

## Router R-04
R-04>enable
R-04#show running-config
Building configuration...

Current configuration : 1504 bytes
!
version 16.6.4
no service timestamps log datetime msec
no service timestamps debug datetime msec
no service password-encryption
!
hostname R-04
!
!
!
!
!
!
!
!
no ip cef
ipv6 unicast-routing
!
no ipv6 cef
!
!
!
!
!
!
!
!
!
!
!
!
spanning-tree mode pvst
!
!
!
!
!
!
interface GigabitEthernet0/0/0
 description SW-05-Link
 no ip address
 duplex auto
 speed auto
 ipv6 address 2001:CAFE:ABCD:8::1/64
!
interface GigabitEthernet0/0/1
 no ip address
 duplex auto
 speed auto
 shutdown
!
interface GigabitEthernet0/0/2
 no ip address
 duplex auto
 speed auto
 shutdown
!
interface Serial0/1/0
 no ip address
 clock rate 2000000
 shutdown
!
interface Serial0/1/1
 no ip address
 clock rate 2000000
 shutdown
!
interface Serial0/2/0
 description R-03-Link
 no ip address
 ipv6 address 2001:CAFE:ABCD:7::2/64
!
interface Serial0/2/1
 no ip address
 clock rate 2000000
 shutdown
!
interface Vlan1
 no ip address
 shutdown
!
ip classless
!
ip flow-export version 9
!
ipv6 route 2001:CAFE:ABCD:1::/64 2001:CAFE:ABCD:7::1
ipv6 route 2001:CAFE:ABCD:2::/64 2001:CAFE:ABCD:7::1
ipv6 route 2001:CAFE:ABCD:5::/64 2001:CAFE:ABCD:7::1
ipv6 route 2001:CAFE:ABCD:3::/64 2001:CAFE:ABCD:7::1
ipv6 route 2001:CAFE:ABCD:4::/64 2001:CAFE:ABCD:7::1
ipv6 route 2001:CAFE:ABCD:6::/64 2001:CAFE:ABCD:7::1
ipv6 route 2001:CAFE:ABCD:9::/64 2001:CAFE:ABCD:7::1
ipv6 route 2001:CAFE:ABCD:A::/64 2001:CAFE:ABCD:7::1
ipv6 route 2001:CAFE:ABCD:B::/64 2001:CAFE:ABCD:7::1
!
!
!
!
!
!
line con 0
!
line aux 0
!
line vty 0 4
 login
!
!
!
end


R-04#

## Router R-05
R-05>
R-05>enable
R-05#show running-config
Building configuration...

Current configuration : 1502 bytes
!
version 16.6.4
no service timestamps log datetime msec
no service timestamps debug datetime msec
no service password-encryption
!
hostname R-05
!
!
!
!
!
!
!
!
no ip cef
ipv6 unicast-routing
!
no ipv6 cef
!
!
!
!
!
!
!
!
!
!
!
!
spanning-tree mode pvst
!
!
!
!
!
!
interface GigabitEthernet0/0/0
 description SW-06-Link
 no ip address
 duplex auto
 speed auto
 ipv6 address 2001:CAFE:ABCD:A::1/64
!
interface GigabitEthernet0/0/1
 description SW-07-Link
 no ip address
 duplex auto
 speed auto
 ipv6 address 2001:CAFE:ABCD:B::1/64
!
interface GigabitEthernet0/0/2
 no ip address
 duplex auto
 speed auto
 shutdown
!
interface Serial0/1/0
 no ip address
 clock rate 2000000
 shutdown
!
interface Serial0/1/1
 no ip address
 clock rate 2000000
 shutdown
!
interface Serial0/2/0
 no ip address
 clock rate 2000000
 shutdown
!
interface Serial0/2/1
 description R-03-Link
 no ip address
 ipv6 address 2001:CAFE:ABCD:9::2/64
!
interface Vlan1
 no ip address
 shutdown
!
ip classless
!
ip flow-export version 9
!
ipv6 route 2001:CAFE:ABCD:1::/64 2001:CAFE:ABCD:9::1
ipv6 route 2001:CAFE:ABCD:2::/64 2001:CAFE:ABCD:9::1
ipv6 route 2001:CAFE:ABCD:3::/64 2001:CAFE:ABCD:9::1
ipv6 route 2001:CAFE:ABCD:5::/64 2001:CAFE:ABCD:9::1
ipv6 route 2001:CAFE:ABCD:4::/64 2001:CAFE:ABCD:9::1
ipv6 route 2001:CAFE:ABCD:6::/64 2001:CAFE:ABCD:9::1
ipv6 route 2001:CAFE:ABCD:7::/64 2001:CAFE:ABCD:9::1
ipv6 route 2001:CAFE:ABCD:8::/64 2001:CAFE:ABCD:9::1
!
!
!
!
!
!
line con 0
!
line aux 0
!
line vty 0 4
 login
!
!
!
end


R-05#

## ✅ Verification Results
## Successful Ping Tests:
## 1. PC-08 to PC-01 - Successful (ICMP)
C:\>ping 2001:CAFE:ABCD:1::2

Pinging 2001:CAFE:ABCD:1::2 with 32 bytes of data:

Reply from 2001:CAFE:ABCD:1::2: bytes=32 time=3ms TTL=124
Reply from 2001:CAFE:ABCD:1::2: bytes=32 time=3ms TTL=124
Reply from 2001:CAFE:ABCD:1::2: bytes=32 time=3ms TTL=124
Reply from 2001:CAFE:ABCD:1::2: bytes=32 time=31ms TTL=124

Ping statistics for 2001:CAFE:ABCD:1::2:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 3ms, Maximum = 31ms, Average = 10ms
C:\>

## 2.PC-02 to DNS-Server - Successful (ICMP)
Cisco Packet Tracer SERVER Command Line 1.0
C:\>ping 2001:CAFE:ABCD:1::3

Pinging 2001:CAFE:ABCD:1::3 with 32 bytes of data:

Reply from 2001:CAFE:ABCD:1::3: bytes=32 time=3ms TTL=124
Reply from 2001:CAFE:ABCD:1::3: bytes=32 time=3ms TTL=124
Reply from 2001:CAFE:ABCD:1::3: bytes=32 time=3ms TTL=124
Reply from 2001:CAFE:ABCD:1::3: bytes=32 time=3ms TTL=124

Ping statistics for 2001:CAFE:ABCD:1::3:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 3ms, Maximum = 3ms, Average = 3ms

C:\>

## 3.PC-04 to PC-05 - Successful (ICMP)
Cisco Packet Tracer PC Command Line 1.0
C:\>ping 2001:CAFE:ABCD:3::2

Pinging 2001:CAFE:ABCD:3::2 with 32 bytes of data:

Reply from 2001:CAFE:ABCD:3::2: bytes=32 time=1ms TTL=126
Reply from 2001:CAFE:ABCD:3::2: bytes=32 time=10ms TTL=126
Reply from 2001:CAFE:ABCD:3::2: bytes=32 time=1ms TTL=126
Reply from 2001:CAFE:ABCD:3::2: bytes=32 time=17ms TTL=126

Ping statistics for 2001:CAFE:ABCD:3::2:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 1ms, Maximum = 17ms, Average = 7ms

C:\>

## 🎯 Learning Outcomes
IPv6 addressing and subnetting
Static routing configuration on Cisco routers
Point-to-point serial link configuration
Network troubleshooting using ping and traceroute
Understanding of routing tables and path selection
IPv6 unicast routing enablement

## 🛠️ Requirements
Cisco Packet Tracer 7.0 or higher
Basic understanding of IPv6 addressing
Knowledge of Cisco IOS commands

## 📁 Repository Structure
ipv6-static-routing-lab/
├── README.md
├── topology.pkt (Packet Tracer file)
├── configurations/
│   ├── R-01_config.txt
│   ├── R-02_config.txt
│   ├── R-03_config.txt
│   ├── R-04_config.txt
│   └── R-05_config.txt
└── screenshots/
    ├── ping_verification_1.png
    ├── ping_verification_2.png
    └── network_topology.png

## 🚀 How to Use
Clone this repository
Open the .pkt file in Cisco Packet Tracer
Explore device configurations
Test connectivity using ping commands
Modify routing tables to experiment with different paths

## 📝 Notes
All routers have IPv6 unicast routing enabled
Serial interfaces on one end require clock rate configuration
Static routes are used throughout (no dynamic routing protocols)
Network uses /64 subnets as per IPv6 best practices

## 🤝 Contributing
Feel free to fork this project and enhance it with:
Dynamic routing protocols (OSPFv3, EIGRP for IPv6)
Additional security features
VLAN configurations
IPv6 access-lists
## 📝 My Contact

**Name:**  Nimesha Ridmi

**GitHub:** https://github.com/ridmi762

**Note:** This is my personal learning project. I built it entirely on my own to develop my networking skills.


## ⭐ Thank You for Checking Out My Project!

I'm proud of what I built and learned through this project. If you have any questions or suggestions, feel free to reach out!

<div align="center">
  <sub>Built by me using Cisco Packet Tracer | Self-learning project</sub>
  <br>
  <sub>© 2024 [Your Name]</sub>
</div>


## Happy Networking! 🌐
