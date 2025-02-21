![](../Attachments/Pasted%20image%2020230226151148.png)

## DEEL 1: maak de netwerkopstelling en initialiseer de toestellen

## DEEL 2: configureer alle toestellen en controleer de verbindingen

### Stap 1: configureer de IPv6 adressen op alle PC’s

![](../Attachments/Pasted%20image%2020230226152212.png)

### Stap 2: configureer de switchen

a. Maak DNS lookup ongedaan.
```
Switch(config)#no ip domain lookup
```
b. Configureer een hostname.
```
Switch(config)#hostname S1
```
c. Wijs volgende domeinnaam toe: ccna-lab.com
```
S1(config)#ip domain name ccna-lab.com
```
d. Encrypteer de plain-text paswoorden.
```
S1(config)#service password-encryption
```
e. Maak een MOTD-banner die de gebruikers waarschuwt: “Toegang voor onbevoegden is verboden”.
```
S1(config)#banner motd "Toegang voor onbevoegden is verboden"
```
f. Maak een lokale user database met een gebruikersnaam admin en paswoord classadm.
```
S1(config)#user admin password classadm
```
g. Configureer class als het privileged EXEC geëncrypteerd paswoord.
```
S1(config)#enable secret class
```
h. Configureer cisco als het console paswoord en maak login mogelijk.
```
S1(config)#line console 0
S1(config-line)#password cisco
S1(config-line)#login
```
i. Maak login op de VTY-lijnen mogelijk door gebruik te maken van de lokale database.
```
S1(config-line)#line vty 0 15
S1(config-line)#password cisco
S1(config-line)#login local
```
j. Genereer een crypto rsa key voor ssh, gebruik makend van een modulus grootte van 1024 bits.
```
S1(config)#crypto key generate rsa

The name for the keys will be: S1.ccna-lab.com

Choose the size of the key modulus in the range of 360 to 2048 for your

General Purpose Keys. Choosing a key modulus greater than 512 may take

a few minutes.

  

How many bits in the modulus [512]: 1024

% Generating 1024 bit RSA keys, keys will be non-exportable...[OK]
```
k. Verander de transport input op alle VTY-lijnen naar alleen SSH en Telnet.
```
S1(config)#line vty 0 15
S1(config-line)#transport input ssh
S1(config-line)#transport input telnet
```
l. Wijs een IPv6 adres toe aan VLAN 1 overeenkomstig de adrestabel.
Voeg hier tussen de runningconfiguration file van S1.
```
S1(config)#sdm prefer dual-ipv4-and-ipv6 default
S1#reload
S1(config)#interface vlan 1
S1(config-if)#ipv6 address 2001:DB8:ACAD:A::A/64
S1(config-if)#no shutdown
```

Voeg hier tussen de runningconfiguration file van S1.
```
S1#show run

Building configuration...

  

Current configuration : 1464 bytes

!

version 15.0

no service timestamps log datetime msec

no service timestamps debug datetime msec

service password-encryption

!

hostname S1

!

!

enable secret 5 $1$mERr$9cTjUIEqNGurQiFU.ZeCi1

!

!

!

no ip domain-lookup

ip domain-name ccna-lab.com

!

username admin privilege 1 password 7 0822404F1A0A04131F

!

!

!

spanning-tree mode pvst

spanning-tree extend system-id

!

interface FastEthernet0/1

!

interface FastEthernet0/2

!

interface FastEthernet0/3

!

interface FastEthernet0/4

!

interface FastEthernet0/5

!

interface FastEthernet0/6

!

interface FastEthernet0/7

!

interface FastEthernet0/8

!

interface FastEthernet0/9

!

interface FastEthernet0/10

!

interface FastEthernet0/11

!

interface FastEthernet0/12

!

interface FastEthernet0/13

!

interface FastEthernet0/14

!

interface FastEthernet0/15

!

interface FastEthernet0/16

!

interface FastEthernet0/17

!

interface FastEthernet0/18

!

interface FastEthernet0/19

!

interface FastEthernet0/20

!

interface FastEthernet0/21

!

interface FastEthernet0/22

!

interface FastEthernet0/23

!

interface FastEthernet0/24

!

interface GigabitEthernet0/1

!

interface GigabitEthernet0/2

!

interface Vlan1

no ip address

ipv6 address 2001:DB8:ACAD:A::A/64

shutdown

!

banner motd ^CToegang voor onbevoegden is verboden^C

!

!

!

!

!

line con 0

password 7 0822455D0A16

login

!

line vty 0 4

password 7 0822455D0A16

login local

transport input telnet

line vty 5 15

password 7 0822455D0A16

login local

transport input telnet

!

!

!

!

end
```

### Stap 3: configureer de basisinstellingen op alle routers

a. Maak DNS lookup ongedaan. 
```
Router(config)#no ip domain lookup
```
b. Configureer een hostname. 
```
Router(config)#hostname R1
```
c. Wijs volgende domeinnaam toe: ccna-lab.com. 
```
R1(config)#ip domain name ccna-lab.com
```
d. Encrypteer de plain-text paswoorden.
```
R1(config)#service password-encryption
```
e. Maak een MOTD-banner die de gebruikers waarschuwt: “Toegang voor onbevoegden is verboden”. 
```
R1(config)#banner motd "Toegang voor onbevoegden is verboden"
```
f. Maak een lokale user database met een gebruikersnaam admin en paswoord classadm. 
```
R1(config)#user admin password classadm
```
g. Configureer class als het privileged EXEC geëncrypteerd paswoord. 
```
R1(config)#enable secret class
```
h. Configureer cisco als het console paswoord en maak login mogelijk.
```
R1(config)#line console 0
R1(config-line)#password cisco
R1(config-line)#login
```
i. Maak login op de VTY-lijnen mogelijk door gebruik te maken van de lokale database. 
```
R1(config-line)#line vty 0 15
R1(config-line)#login local
```
j. Genereer een crypto rsa key voor ssh, gebruik makend van een modulus grootte van 1024 bits. k. Verander de transport input op alle VTY-lijnen naar alleen SSH en Telnet
```
R1(config)#crypto key generate rsa

The name for the keys will be: R1.ccna-lab.com

Choose the size of the key modulus in the range of 360 to 2048 for your

General Purpose Keys. Choosing a key modulus greater than 512 may take

a few minutes.

  

How many bits in the modulus [512]: 1024

% Generating 1024 bit RSA keys, keys will be non-exportable...[OK]
```
k. Verander de transport input op alle VTY-lijnen naar alleen SSH en Telnet
```
R1(config)#line vty 0 15
R1(config-line)#transport input ssh
R1(config-line)#transport input telnet
```

### Stap 4: configureer IPv6 instellingen op R1

a. Configureer de IPv6 unicast adressen op de volgende interfaces: G0/0, G0/1, S0/0/0 en S0/0/1. 
```
R1(config)#interface g0/0/0
R1(config-if)#ipv6 address 2001:DB8:ACAD:B::1/64
R1(config-if)#no shutdown
```
b. Configureer de IPv6 link-local adressen op de volgende interfaces: G0/0, G0/1, S0/0/0 en S0/0/1. Gebruik FE80::1 voor de link-local adressen op alle vier interfaces. 
```
R1(config-if)#ipv6 address FE80::1 link-local
```
c. Zet de clock rate op S0/0/0 op 128000. 
```
R1(config-if)#interface s0/1/0
R1(config-if)#clock rate 128000
```
d. Zorg ervoor dat de interfaces IPv6-pakketten kunnen versturen. 
```
R1(config-if)#no shutdown
```
e. Maak IPv6 unicast routing mogelijk:
```
R(config)# ipv6 unicast-routing
```
f. Configureer OSPFv3 op R1 en zorg dat de LAN-interfaces passieve interfaces zijn.
- Configuratie OSPFv3:
	```
	R(config)# ipv6 router ospf 10 
	R(config-rtr)# passive interface G0/0/0 (indien G0/0/0 de passieve interface is)
	```
- Dan op elke actieve interface:
	```
	R(config-if)#ipv6 ospf 10 area 0
	```

Voeg hier tussen de runningconfiguration file van R1.

Stap 5: configureer IPv6 instellingen op R2

a. Configureer de IPv6 unicast adressen op de volgende interfaces: Lo1, S0/0/0 en S0/0/1. 
b. Configureer de IPv6 link-local adressen op de volgende interfaces: S0/0/0 en S0/0/1. Gebruik FE80::2 voor de link-local adressen op alle twee interfaces. 
c. Zet de clock rate op S0/0/1 op 128000. 
d. Zorg ervoor dat de interfaces IPv6-pakketten kunnen versturen. 
e. Maak IPv6 unicast routing mogelijk.
f. Maak een default route die gebruik maakt van de loopback interface Lo1 (deze dient ter simulatie van een internetconnectie).
```
R(config)# ipv6 route ::/0 Lo1
```
g. Configureer OSPFv3 op R2 en zorg dat de default route doorgegeven wordt op de andere routers van het domein.
- Configuratie zie R1 en voeg een lijn toe, onder:
```
R(config)# ipv6 router ospf 10 
R(config-rtr)# passive-interface G0/0/0 (indien G0/0/0 de passieve interface is) 
R(config-rtr)#default-information originate
```

Voeg hier tussen de runningconfiguration file van R2.
```
R1#show run

Building configuration...

  

Current configuration : 1504 bytes

!

version 15.4

no service timestamps log datetime msec

no service timestamps debug datetime msec

service password-encryption

!

hostname R1

!

!

!

enable secret 5 $1$mERr$9cTjUIEqNGurQiFU.ZeCi1

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

username admin password 7 0822404F1A0A04131F

!

!

!

!

!

!

!

!

no ip domain-lookup

ip domain-name ccna-lab.com

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

ipv6 address FE80::1 link-local

ipv6 address 2001:DB8:ACAD:B::1/64

!

interface GigabitEthernet0/0/1

no ip address

duplex auto

speed auto

ipv6 address FE80::1 link-local

ipv6 address 2001:DB8:ACAD:A::1/64

!

interface GigabitEthernet0/0/2

no ip address

duplex auto

speed auto

shutdown

!

interface Serial0/1/0

no ip address

ipv6 address FE80::1 link-local

ipv6 address 2001:DB8:AAAA:1::1/64

ipv6 enable

ipv6 ospf 10 area 0

clock rate 128000

!

interface Serial0/1/1

no ip address

ipv6 address FE80::1 link-local

ipv6 address 2001:DB8:AAAA:3::1/64

ipv6 ospf 10 area 0

!

interface Vlan1

no ip address

shutdown

!

ipv6 router ospf 10

log-adjacency-changes

passive-interface GigabitEthernet0/0/0

passive-interface GigabitEthernet0/0/1

!

ip classless

!

ip flow-export version 9

!

!

!

banner motd ^CToegang voor onbevoegden is verboden^C

!

!

!

!

line con 0

password 7 0822455D0A16

login

!

line aux 0

!

line vty 0 4

login local

transport input telnet

line vty 5 15

login local

transport input telnet

!

!

!

end
```

### Stap 5: configureer IPv6 instellingen op R2

a. Configureer de IPv6 unicast adressen op de volgende interfaces: Lo1, S0/0/0 en S0/0/1. 
```
R2(config)#interface s0/1/1
R2(config-if)#ipv6 address 2001:DB8:AAAA:2::2/64
R2(config-if)#no shutdown
```
b. Configureer de IPv6 link-local adressen op de volgende interfaces: S0/0/0 en S0/0/1. Gebruik FE80::2 voor de link-local adressen op alle twee interfaces. 
```
R2(config-if)#ipv6 address FE80::2 link-local
```
c. Zet de clock rate op S0/0/1 op 128000. 
```
R2(config-if)#interface s0/1/1
R2(config-if)#clock rate 128000
```
d. Zorg ervoor dat de interfaces IPv6-pakketten kunnen versturen. 
```
R2(config-if)#no shutdown
```
e. Maak IPv6 unicast routing mogelijk.
```
R2(config)#ipv6 unicast-routing
```
f. Maak een default route die gebruik maakt van de loopback interface Lo1 (deze dient ter simulatie van een internetconnectie).
```
R(config)# ipv6 route ::/0 Lo1
```
g. Configureer OSPFv3 op R2 en zorg dat de default route doorgegeven wordt op de andere routers van het domein.
- Configuratie zie R1 en voeg een lijn toe, onder:
```
R(config)# ipv6 router ospf 10 
R(config-rtr)# passive interface G0/0/0 (indien G0/0/0 de passieve interface is) 
R(config-rtr)#default-information originate
```

Voeg hier tussen de runningconfiguration file van R2.
```
R2#show run

Building configuration...

  

Current configuration : 1463 bytes

!

version 15.4

no service timestamps log datetime msec

no service timestamps debug datetime msec

service password-encryption

!

hostname R2

!

!

!

enable secret 5 $1$mERr$9cTjUIEqNGurQiFU.ZeCi1

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

username admin password 7 0822404F1A0A04131F

!

!

!

!

!

!

!

!

no ip domain-lookup

ip domain-name ccna-lab.com

!

!

spanning-tree mode pvst

!

!

!

!

!

!

interface Loopback1

no ip address

ipv6 address 2001:DB8:AAAA:4::1/64

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

ipv6 address FE80::2 link-local

ipv6 address 2001:DB8:AAAA:1::2/64

ipv6 ospf 10 area 0

!

interface Serial0/1/1

no ip address

ipv6 address FE80::2 link-local

ipv6 address 2001:DB8:AAAA:2::2/64

ipv6 ospf 10 area 0

clock rate 128000

!

interface Vlan1

no ip address

shutdown

!

ipv6 router ospf 10

default-information originate

log-adjacency-changes

passive-interface GigabitEthernet0/0/1

!

ip classless

!

ip flow-export version 9

!

ipv6 route ::/0 Loopback1

!

!

banner motd ^CToegang voor onbevoegden is verboden^C

!

!

!

!

line con 0

password 7 0822455D0A16

login

!

line aux 0

!

line vty 0 4

login local

transport input telnet

line vty 5 15

login local

transport input telnet

!

!

!

end
```

### Stap 6: configureer IPv6 instellingen op R3

a. Configureer de IPv6 unicast adressen op de volgende interfaces: G0/1, S0/0/0 en S0/0/1. 
```
R3(config)#interface g0/0/1
R3(config-if)#ipv6 address 2001:DB8:CAFE:C::1/64
```
b. Configureer de IPv6 link-local adressen op de volgende interfaces: G0/1, S0/0/0 en S0/0/1. Gebruik FE80::3 voor de link-local adressen op alle drie interfaces. 
```
R3(config-if)#ipv6 address FE80::3 link-local
```
c. Zet de clock rate op S0/0/0 op 128000. 
```
R3(config-if)#clock rate 128000
```
d. Zorg ervoor dat de interfaces IPv6-pakketten kunnen versturen. 
```
R3(config-if)#no shutdown
```
e. Maak IPv6 unicast routing mogelijk. 
```
R3(config)#ipv6 unicast-routing
```
f. Configureer OSPFv3 op R3 en maak van de LAN-interface een passieve interface.
```
R3(config-rtr)#int s0/1/0
R3(config-if)#ipv6 ospf 10 area 0
R3(config-if)#int s0/1/1
R3(config-if)#ipv6 ospf 10 area 0
R3(config)#ipv6 router ospf 10
R3(config-rtr)#passive-interface g0/0/1
```

Voeg hier tussen de runningconfiguration file van R3.
```
R3#show run

Building configuration...

  

Current configuration : 1392 bytes

!

version 15.4

no service timestamps log datetime msec

no service timestamps debug datetime msec

service password-encryption

!

hostname R3

!

!

!

enable secret 5 $1$mERr$9cTjUIEqNGurQiFU.ZeCi1

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

username admin password 7 0822404F1A0A04131F

!

!

!

!

!

!

!

!

no ip domain-lookup

ip domain-name ccna-lab.com

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

ipv6 address FE80::3 link-local

ipv6 address 2001:DB8:CAFE:C::1/64

!

interface GigabitEthernet0/0/2

no ip address

duplex auto

speed auto

shutdown

!

interface Serial0/1/0

no ip address

ipv6 address FE80::3 link-local

ipv6 address 2001:DB8:AAAA:3::2/64

ipv6 ospf 10 area 0

clock rate 128000

!

interface Serial0/1/1

no ip address

ipv6 address FE80::3 link-local

ipv6 address 2001:DB8:AAAA:2::1/64

ipv6 ospf 10 area 0

!

interface Vlan1

no ip address

shutdown

!

ipv6 router ospf 10

log-adjacency-changes

passive-interface GigabitEthernet0/0/1

!

ip classless

!

ip flow-export version 9

!

!

!

banner motd ^CToegang voor onbevoegden is verboden^C

!

!

!

!

line con 0

password 7 0822455D0A16

login

!

line aux 0

!

line vty 0 4

login local

transport input telnet

line vty 5 15

login local

transport input telnet

!

!

!

end
```