# CLI-PROJET-FINANCIAL-NETWORK

## Switch 2960 HR-SW

```
--configuration de base
en
conf t

hostname HR-SW

enable password cisco

line console 0
password cisco 
login
exit

banner motd #NO UNAUTHORISED ACCESS!!#

no ip domain lookup 

service password-encryption

--vlan
vlan 10
name DATA
vlan 120
name VOICE
exit

int range fa0/1-2
switchport mode trunk
exit

int range fa0/3-24
switchport mode access
switchport access vlan 10
switchport voice vlan 120
exit

do wr
```

## Switch 2960 CS-SW

```
en
conf t

hostname CS-SW

enable password cisco

line console 0
password cisco 
login
exit

banner motd #NO UNAUTHORISED ACCESS!!#

no ip domain lookup 

service password-encryption

--vlan
vlan 20
name DATA
vlan 120
name VOICE
exit

int range fa0/1-2
switchport mode trunk
exit

int range fa0/3-24
switchport mode access
switchport access vlan 20
switchport voice vlan 120
exit


do wr
```

## Switch 2960 MK-SW

```
en
conf t

hostname MK-SW

enable password cisco

line console 0
password cisco 
login
exit

banner motd #NO UNAUTHORISED ACCESS!!#

no ip domain lookup 

service password-encryption

--vlan
vlan 30
name DATA
vlan 120
name VOICE
exit

int range fa0/1-2
switchport mode trunk
exit

int range fa0/3-24
switchport mode access
switchport access vlan 30
switchport voice vlan 120
exit


do wr
```


## Switch 2960 LM-SW

```
en
conf t

hostname LM-SW

enable password cisco

line console 0
password cisco 
login
exit

banner motd #NO UNAUTHORISED ACCESS!!#

no ip domain lookup 

service password-encryption

--vlan
vlan 40
name DATA
vlan 120
name VOICE
exit

int range fa0/1-2
switchport mode trunk
exit

int range fa0/3-24
switchport mode access
switchport access vlan 40
switchport voice vlan 120
exit


do wr
```

## Switch 2960 IT-SW

```
en
conf t

hostname IT-SW

enable password cisco

line console 0
password cisco 
login
exit

banner motd #NO UNAUTHORISED ACCESS!!#

no ip domain lookup 

service password-encryption

--vlan
vlan 50
name DATA
vlan 120
name VOICE
exit

int range fa0/1-2
switchport mode trunk
exit

int range fa0/3-24
switchport mode access
switchport access vlan 50
switchport voice vlan 120
exit


do wr
```

## Switch 2960 SERVER-SIDE SW 

```
en
conf t

hostname SERVER-SIDE-SW

enable password cisco

line console 0
password cisco 
login
exit

banner motd #NO UNAUTHORISED ACCESS!!#

no ip domain lookup 

service password-encryption

do wr
```

## Switch Layer 3 3650 HQ-MSLW1

```
en
conf t

hostname HQ-MSLW1

enable password cisco

line console 0
password cisco 
login
exit

banner motd #NO UNAUTHORISED ACCESS!!#

no ip domain lookup 

service password-encryption

username cisco password cisco
ip domain-name cisco.com
crypto key generate rsa 
1024
ip ssh version 2
line vty 0 15
login local
transport input ssh
exit
--vlan 
int range gig1/0/2-7
switchport mode trunk
exit

vlan 10
name HR
vlan 20
name CS
vlan 30
name MK
vlan 40
name LM
vlan 50
name IT
vlan 120
name VOICE
exit

interface GigabitEthernet1/0/1
no switchport
ip add 192.168.21.17 255.255.255.252
no shut
do wr

ip routing
router ospf 10
router-id 1.1.1.1
network 10.10.10.0 0.0.0.255 area 0
network 192.168.21.16 0.0.0.3 area 0
network 192.168.20.0 0.0.0.255 area 0
exit

int vlan 10 
ip add 192.168.20.1 255.255.255.192
ip helper-address 192.168.21.5
exit

int vlan 20
ip add 192.168.20.65 255.255.255.192
ip helper-address 192.168.21.5
exit

int vlan 30
ip add 192.168.20.129 255.255.255.192
ip helper-address 192.168.21.5
exit

int vlan 40
ip add 192.168.20.193 255.255.255.224
ip helper-address 192.168.21.5
exit

int vlan 50
ip add 192.168.20.225 255.255.255.224
ip helper-address 192.168.21.5
exit


interface GigabitEthernet1/0/7
access-list 10 permit 192.168.20.224 0.0.0.31
access-list 10 deny any
line vty 0 15 
access-class 10 in
exit

do wr

```
## Switch Layer 3 3650 HQ-MSLW2

```
en
conf t

hostname HQ-MSLW2

enable password cisco

line console 0
password cisco 
login
exit

banner motd #NO UNAUTHORISED ACCESS!!#

no ip domain lookup 

service password-encryption

username cisco password cisco
ip domain-name cisco.com
crypto key generate rsa 
1024
ip ssh version 2
line vty 0 15
login local
transport input ssh
exit

--vlan
int range gig1/0/2-6
switchport mode trunk
exit

vlan 10
name HR
vlan 20
name CS
vlan 30
name MK
vlan 40
name LM
vlan 50
name IT
vlan 120
name VOICE
exit

interface GigabitEthernet1/0/1
no switchport
ip add 192.168.21.21 255.255.255.252
no shut

ip routing
router ospf 10
router-id 2.2.2.2
network 10.10.10.0 0.0.0.255 area 0
network 192.168.21.20 0.0.0.3 area 0
network 192.168.20.0 0.0.0.255 area 0
exit


int vlan 10
ip add 192.168.20.2 255.255.255.192
exit
int vlan 20
ip add 192.168.20.66 255.255.255.192
exit
int vlan 30
ip add 192.168.20.130 255.255.255.192
exit
int vlan 40
ip add 192.168.20.194 255.255.255.224
exit
int vlan 50
ip add 192.168.20.226 255.255.255.224
exit


do wr
```


## Router 2911 HQ-Router

```
en
conf t

hostname HQ-Router

enable password cisco

line console 0
password cisco 
login
exit

banner motd #NO UNAUTHORISED ACCESS!!#

no ip domain lookup 

service password-encryption

username cisco password cisco
ip domain-name cisco.com
crypto key generate rsa 
1024
ip ssh version 2
line vty 0 15
login local
transport input ssh
exit

router ospf 10
router-id 4.4.4.4
network 190.200.100.0 0.0.0.3 area 0
network 190.200.100.4 0.0.0.3 area 0
network 192.168.21.16 0.0.0.3 area 0
network 192.168.21.20 0.0.0.3 area 0
exit

access-list 10 permit 192.168.20.224 0.0.0.31
access-list 10 deny any
line vty 0 15 
access-class 10 in


int range gig0/0-1
ip nat inside
exit

int se0/2/0
ip nat outside
int se0/2/1
ip nat outside
exit

access-list 50 permit 192.168.20.0 0.0.0.255
ip nat inside source list 50 interface se0/2/0 overload
ip nat inside source list 50 interface se0/2/1 overload

license boot module c2900 technology-package securityk9
do reload


access-list 110 permit ip 192.168.20.0 0.0.0.255 192.168.21.0 0.0.0.15

crypto isakmp policy 10
encryption aes 256
authentication pre-share
group 5
exit
crypto isakmp key vpnpa55 address 190.200.100.1
crypto ipsec transform-net VPN-SET esp-aes esp-sha-hmac
crypto map VPN-MAP 10 ipsec-isakmp
description VPN connection to HQ-NETWORK
set peer 190.200.100.9
set transform-set VPN-SET
match address 110
exit

interface S0/2/0
crypto map VPN-MAP

exit

do wr
```

## Router 2911 Server-Side-Router

```
en
conf t

hostname Server-Side-Router

enable password cisco

line console 0
password cisco 
login
exit

banner motd #NO UNAUTHORISED ACCESS!!#

no ip domain lookup 

service password-encryption

username cisco password cisco
ip domain-name cisco.com
crypto key generate rsa 
1024
ip ssh version 2
line vty 0 15
login local
transport input ssh
exit

int range fa0/2-5
switchport mode access
switchport port-security
switchport port-security maximum 1
switchport port-security mac-address sticky
switchport port-security violation shutdown
int range fa0/6-24, gig 0/1-2
switchport mode access
switchport access vlan 99
shutdown
exit

router ospf 10
router-id 7.7.7.7
network 192.168.21.0 0.0.0.15 area 0
network 190.200.100.8 0.0.0.3 area 0
network 190.200.100.12 0.0.0.3 area 0
exit

interface GigabitEthernet0/0
ip address 192.168.21.1 255.255.255.240
no shutdown
exit

interface Serial0/0/0
ip address 190.200.100.9 255.255.255.252
no shutdown
exit

interface Serial0/0/1
ip address 190.200.100.13 255.255.255.252
no shutdown
exit

access-list 10 permit 192.168.20.224 0.0.0.31
access-list 10 deny any
line vty 0 15 
access-class 10 in
exit

license boot module c2900 technology-package securityk9
do reload

do wr
```


## Router 2911 Safaricorm 

```
en
conf t

hostname Safaricorm

enable password cisco

line console 0
password cisco 
login
exit

banner motd #NO UNAUTHORISED ACCESS!!#

no ip domain lookup 

service password-encryption

username cisco password cisco
ip domain-name cisco.com
crypto key generate rsa 
1024
ip ssh version 2
line vty 0 15
login local
transport input ssh
exit

router ospf 10
router-id 5.5.5.5
network 190.200.100.0 0.0.0.3 area 0
network 190.200.100.8 0.0.0.3 area 0
exit


access-list 10 permit 192.168.20.224 0.0.0.31
access-list 10 deny any
line vty 0 15 
access-class 10 in
exit

do wr
```


## Router 2911 JTL-IS

```
en
conf t

hostname JTL-ISP

enable password cisco

line console 0
password cisco 
login
exit

banner motd #NO UNAUTHORISED ACCESS!!#

no ip domain lookup 

service password-encryption

username cisco password cisco
ip domain-name cisco.com
crypto key generate rsa 
1024
ip ssh version 2
line vty 0 15
login local
transport input ssh
exit

router ospf 10
router-id 6.6.6.6
network 190.200.100.4 0.0.0.3 area 0
network 190.200.100.12 0.0.0.3 area 0
exit

access-list 10 permit 192.168.20.224 0.0.0.31
access-list 10 deny any
line vty 0 15 
access-class 10 in
exit
do wr
```

## ROUTER 2811 HQ VOIP 


```
en
conf t
int fa 0/0
no sh
ip add 10.10.10.1 255.255.255.0
exit
int fa 0/0
no ip address
int fa 0/0.120
encapsulation dot1Q 120
ip add 10.10.10.1 255.255.255.0
exit

router ospf 10 
router-id 3.3.3.3
network 10.10.10.0 0.0.0.255 area 0

exit

service dhcp
ip dhcp pool VOICE
network 10.10.10.0 255.255.255.0
default-router 10.10.10.1
option 150 ip 10.10.10.1
dns-server 10.10.10.1
ip dhcp excluded-address 10.10.10.1
telephony-service
max-ephones
max-ephones 20
max-dn 20
ip source-address 10.10.10.1 port 2000
auto assign 1 to 20
exit
ephone-dn 1
number 401
ex
ephone-dn 2
number 402
ex
ephone-dn 3
number 403
ex
ephone-dn 4
number 404
ex
ephone-dn 5
number 405
ex
ephone-dn 6
number 406
ex
ephone-dn 7
number 407
ex
ephone-dn 8
ephone-dn 8
number 408
ex
ephone-dn 9
number 409
ephone-dn 10
number 410
ex
exit

access-list 10 permit 192.168.20.224 0.0.0.31
access-list 10 deny any
line vty 0 15 
access-class 10 in
exit

do wr
```
