# Lab-VLAN
## Part 1: Build the Network and Configure Basic Device 
![alt-текст](https://github.com/DanilChery/CiscoProjectsVLAN/blob/main/Lab-Vlan-schema.jpg "Текст заголовка логотипа 1")  
### •	Configure basic settings for the router.
hostname R1  
!  
boot-start-marker  
boot-end-marker  
!  
!  
enable password 7 110A15040401  
!  
username cisco password 7 02050D480809  
no aaa new-model  
clock timezone PST -8 0  
no ip domain-lookup  
  
line vty 0 4  
 password 7 121A0C041104  
 login local  
line vty 5 15  
 password 7 121A0C041104  
 login local  
!  
!  

S1(config)#banner motd 1  
Enter TEXT message.  End with the character '1'.  
anyone accessing the device that unauthorized access is prohibited.  
1  
### •	Configure basic settings for each switch.  
  
hostname S2  
!  
boot-start-marker  
boot-end-marker  
!  
!  
enable password 7 110A15040401  
!  
username cisco password 7 02050D480809  
no aaa new-model  
clock timezone PST -8 0  
!  
!  
!  
!  
!  
!  
!  
!  
no ip domain-lookup  
line vty 0 4  
 password 7 121A0C041104  
 login local  
line vty 5 15  
 password 7 121A0C041104  
 login local  
!  
!  
  
S1(config)#banner motd 1  
Enter TEXT message.  End with the character '1'.  
anyone accessing the device that unauthorized access is prohibited.  
1  
##Create VLANs and Assign Switch Ports  
###•	Assign VLANs to the correct switch interfaces.  
  
VLAN Name                             Status    Ports  
---- -------------------------------- --------- -------------------------------  
1    default                          active  
3    Mangement                        active    Gi0/2  
4    Operations                       active  
7    ParkingLot                       active    Gi0/3, Gi1/0, Gi1/1, Gi1/2  
                                                Gi1/3  
8    Native                           active  
1002 fddi-default                     act/unsup  
1003 token-ring-default               act/unsup  
1004 fddinet-default                  act/unsup  
1005 trnet-default                    act/unsup  
##Configure an 802.1Q Trunk Between the Switches  
###•	Manually configure trunk interface F0/1.  
Port        Mode             Encapsulation  Status        Native vlan  
Gi0/0       on               802.1q         trunking      1  
Gi0/1       on               802.1q         trunking      1  
  
Port        Vlans allowed on trunk  
Gi0/0       1,3-4,7-8  
Gi0/1       1,3-4,7  
  
Port        Vlans allowed and active in management domain  
Gi0/0       1,3-4,7-8  
Gi0/1       1,3-4,7  
  
Port        Vlans in spanning tree forwarding state and not pruned  
Gi0/0       1,3-4,7-8  
Gi0/1       1,3-4,7  
## •	Configure Inter-VLAN Routing on the Router  
Interface                  IP-Address      OK? Method Status                Protocol  
GigabitEthernet0/0         unassigned      YES NVRAM  up                    up    
GigabitEthernet0/0.3       192.168.3.1     YES NVRAM  up                    up    
GigabitEthernet0/0.4       192.168.4.1     YES NVRAM  up                    up    
GigabitEthernet0/0.8       unassigned      YES unset  up                    up    
GigabitEthernet0/1         unassigned      YES NVRAM  administratively down down  
GigabitEthernet0/2         unassigned      YES NVRAM  administratively down down  
GigabitEthernet0/3         unassigned      YES NVRAM  administratively down down  
## •	Verify Inter-VLAN Routing is Working  
### •	Complete the following tests from PC-A. All should be successful.  
•	Ping from PC-A to its default gateway.  
•	Ping from PC-A to PC-B  
•	Ping from PC-A to S2  
  
VPCS>  
VPCS> ping 192.168.3.1  
  
84 bytes from 192.168.3.1 icmp_seq=1 ttl=255 time=6.837 ms  
84 bytes from 192.168.3.1 icmp_seq=2 ttl=255 time=4.090 ms  
84 bytes from 192.168.3.1 icmp_seq=3 ttl=255 time=4.635 ms  
84 bytes from 192.168.3.1 icmp_seq=4 ttl=255 time=3.413 ms  
^C  
VPCS> ping 192.168.4.1  
  
84 bytes from 192.168.4.1 icmp_seq=1 ttl=255 time=2.618 ms  
84 bytes from 192.168.4.1 icmp_seq=2 ttl=255 time=4.370 ms  
84 bytes from 192.168.4.1 icmp_seq=3 ttl=255 time=4.225 ms  
^C  
VPCS> ping 192.168.3.12  
  
84 bytes from 192.168.3.12 icmp_seq=1 ttl=255 time=4.785 ms  
84 bytes from 192.168.3.12 icmp_seq=2 ttl=255 time=4.973 ms  
^C  
VPCS>  
### •	Complete the following test from PC-B.  
From the command prompt on PC-B, issue the tracert command to the address of PC-A.  
  
VPCS> ping 192.168.3.3  
  
84 bytes from 192.168.3.3 icmp_seq=1 ttl=63 time=19.451 ms  
84 bytes from 192.168.3.3 icmp_seq=2 ttl=63 time=9.397 ms  
84 bytes from 192.168.3.3 icmp_seq=3 ttl=63 time=8.609 ms  
84 bytes from 192.168.3.3 icmp_seq=4 ttl=63 time=9.333 ms  
84 bytes from 192.168.3.3 icmp_seq=5 ttl=63 time=7.219 ms  

[R1-Config](https://github.com/DanilChery/CiscoProjectsVLAN/blob/main/Lab-Vlan-R1-Config.txt "")  
[S1-Config](https://github.com/DanilChery/CiscoProjectsVLAN/blob/main/Lab-Vlan-S1-Config.txt "")  
[S2-Config](https://github.com/DanilChery/CiscoProjectsVLAN/blob/main/Lab-Vlan-S2-Config.txt "")  
