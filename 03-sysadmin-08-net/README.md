Домашнее задание к занятию "3.7 Компьютерные сети, лекция 3"
----------------------------------------------------------
----------------------------------------------------------  
  
1. 
```bash
route-views>show ip route 62.33.159.134
Routing entry for 62.33.0.0/16
  Known via "bgp 6447", distance 20, metric 0
  Tag 2497, type external
  Last update from 202.232.0.2 05:48:16 ago
  Routing Descriptor Blocks:
  * 202.232.0.2, from 202.232.0.2, 05:48:16 ago
      Route metric is 0, traffic share count is 1
      AS Hops 2
      Route tag 2497
      MPLS label: none
route-views>
```
```bash
route-views>show bgp 62.33.159.134
BGP routing table entry for 62.33.0.0/16, version 2688253927
Paths: (20 available, best #17, table default)
```

2. Создал при помощи systemd.
```bash
vagrant@vagrant:~$ cat /etc/systemd/network/dummy0.network 
[Match]
Name=dummy0

[Network]
Address=10.2.2.2/32
vagrant@vagrant:~$ 
```

```bash
vagrant@vagrant:~$ cat /etc/systemd/network/dummy0.netdev 
[NetDev]
Name=dummy0
Kind=dummy
vagrant@vagrant:~$ 
```
dummy0 стал доступен и после перезагрузки. Пример таблицы маршрутов
```bash
agrant@vagrant:~$ sudo ip route add 192.168.0.0/16 dev dummy0
vagrant@vagrant:~$ sudo ip route add 192.168.0.0/16 dev dummy0 metric 100
vagrant@vagrant:~$ sudo ip route add 192.168.0.0/24 dev dummy0
vagrant@vagrant:~$ ip route
default via 10.0.2.2 dev eth0 proto dhcp src 10.0.2.15 metric 100 
10.0.2.0/24 dev eth0 proto kernel scope link src 10.0.2.15 
10.0.2.2 dev eth0 proto dhcp scope link src 10.0.2.15 metric 100 
192.168.0.0/24 dev dummy0 scope link 
192.168.0.0/16 dev dummy0 scope link 
192.168.0.0/16 dev dummy0 scope link metric 100 
```

3. Используем `ss -t -a` для TCP и `ss -u -a` для UDP
```bash
vagrant@vagrant:~$ ss -t -a
State            Recv-Q           Send-Q                       Local Address:Port                         Peer Address:Port            Process
LISTEN           0                4096                         127.0.0.53%lo:domain                            0.0.0.0:*
LISTEN           0                128                                0.0.0.0:ssh                               0.0.0.0:*
ESTAB            0                0                                10.0.2.15:ssh                              10.0.2.2:37740
LISTEN           0                128                                   [::]:ssh                                  [::]:*
```
4. и `ss -u -a` для UDP
```bash
vagrant@vagrant:~$ ss -u -a
State            Recv-Q           Send-Q                        Local Address:Port                         Peer Address:Port           Process
UNCONN           0                0                             127.0.0.53%lo:domain                            0.0.0.0:*
UNCONN           0                0                            10.0.2.15%eth0:bootpc                            0.0.0.0:*
```
протоколы, использующие порты: bootpc, ssh. Процессы и приложения, использующие порты в данных листингax отсутствуют.

5. D
