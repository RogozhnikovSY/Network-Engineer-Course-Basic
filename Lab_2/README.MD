## 2. Лабораторная работа. Просмотр таблицы MAC-адресов коммутатора
____

**Топология сети**

![](init-data-lab-2.png)

**Таблица адресации**
| Устройство | Интерфейс | IP-адрес        | Маска подсети |
| ---------- | --------- | --------------- | ------------- |
| S1         | VLAN 1    | 192.168.1.11    | 255.255.255.0 |
| S2         | VLAN 1    | 192.168.1.12    | 255.255.255.0 |
| PC-A       | NIC       | 192.168.1.1     | 255.255.255.0 |
| PC-B       | NIC       | 192.168.1.2     | 255.255.255.0 |

**Задачи лабораторной работы:**
1. Создание и настройка сети
2. Изучение таблицы MAC-адресов коммутатора
___

**1. Создадим и настроим сеть**

1.1. В соответствии с заданной топологией смоделируем сеть в Cisco Packet Tracer и подключим консольный кабель к коммутатору

1.2.1 Переименуем узел ПК PC-A, зададим IP адрес и маску подсети в соответствии с таблицей адресами

![](Img-2.png)

1.2.2 Повторим действия из п.1.2.1 со вторым узлом ПК

![](Img-3.png)

1.3 Так как работаем в виртуальный среде CPT выполнять инициализацию и перегрузку коммутаторов не требуется

1.4.1 Настроим базовые параметры коммутатора S1

```
Switch>
Switch>
Switch>en
Switch#conf terminal 
Enter configuration commands, one per line.  End with CNTL/Z.
Switch(config)#hostname S1
S1(config)#
S1(config)#	
S1(config)#int vlan 1
S1(config-if)#ip add 192.168.1.11 255.255.255.0
S1(config-if)#exit
S1(config)#
S1(config)#
S1(config)#service password-encryption 
S1(config)#enable secret class
S1(config)#no ip domain-lookup
S1(config)#banner motd #setap s1 for lab-2#
S1(config)#exit
S1#
%SYS-5-CONFIG_I: Configured from console by console

S1#
S1#
S1#conf terminal 
Enter configuration commands, one per line.  End with CNTL/Z.
S1(config)#line VTY 0 4
S1(config-line)#login
% Login disabled on line 1, until 'password' is set
% Login disabled on line 2, until 'password' is set
% Login disabled on line 3, until 'password' is set
% Login disabled on line 4, until 'password' is set
% Login disabled on line 5, until 'password' is set
S1(config-line)#password cisco
S1(config-line)#exit
S1(config)#exit
S1#
%SYS-5-CONFIG_I: Configured from console by console
```

1.4.2 Повторим действия для коммутатора S2, соединим узлы модели через интерфейс Ethernet и отобразим их

```
Switch>
Switch>
Switch>en
Switch#conf terminal 
Enter configuration commands, one per line.  End with CNTL/Z.
Switch(config)#hostname S2
S2(config)#
S2(config)#	
S2(config)#int vlan 1
S2(config-if)#ip add 192.168.1.12 255.255.255.0
S2(config-if)#exit
S2(config)#
S2(config)#
S2(config)#service password-encryption 
S2(config)#enable secret class
S2(config)#no ip domain-lookup
S2(config)#banner motd #setap s2 for lab-2#
S2(config)#exit
S2#
%SYS-5-CONFIG_I: Configured from console by console

S2#
S2#
S2#conf terminal 
Enter configuration commands, one per line.  End with CNTL/Z.
S2(config)#line VTY 0 4
S2(config-line)#login
% Login disabled on line 1, until 'password' is set
% Login disabled on line 2, until 'password' is set
% Login disabled on line 3, until 'password' is set
% Login disabled on line 4, until 'password' is set
% Login disabled on line 5, until 'password' is set
S2(config-line)#password cisco
S2(config-line)#exit
S2(config)#exit
S2#
%SYS-5-CONFIG_I: Configured from console by console
```
1.4.3 Полученная модель сети

![](Img-4.png)

**2. Изучим таблицы MAC-адресов коммутатора**

2.1 Команда на PC-A ***ipconfig /all***\
Введем команду на PC-A ***ipconfig /all***\
И увидим конфигурацию. IP адрес, MAC адрес устройства, маску подсети, и также адрес и префикс IPv6
```
C:\>ipconfig /all

FastEthernet0 Connection:(default port)

   Connection-specific DNS Suffix..: 
   Physical Address................: 00D0.58E8.5E5C
   Link-local IPv6 Address.........: FE80::2D0:58FF:FEE8:5E5C
   IPv6 Address....................: ::
   IPv4 Address....................: 192.168.1.1
   Subnet Mask.....................: 255.255.255.0
   Default Gateway.................: ::
                                     0.0.0.0
   DHCP Servers....................: 0.0.0.0
   DHCPv6 IAID.....................: 
   DHCPv6 Client DUID..............: 00-01-00-01-CD-34-95-8B-00-D0-58-E8-5E-5C
   DNS Servers.....................: ::
                                     0.0.0.0
```
Такую же процедуру проведем с хостом PC-В
```
C:\>ipconfig /all

FastEthernet0 Connection:(default port)

   Connection-specific DNS Suffix..: 
   Physical Address................: 00D0.D3CA.3934
   Link-local IPv6 Address.........: FE80::2D0:D3FF:FECA:3934
   IPv6 Address....................: ::
   IPv4 Address....................: 192.168.1.2
   Subnet Mask.....................: 255.255.255.0
   Default Gateway.................: ::
                                     0.0.0.0
   DHCP Servers....................: 0.0.0.0
   DHCPv6 IAID.....................: 
   DHCPv6 Client DUID..............: 00-01-00-01-08-D6-62-89-00-D0-D3-CA-39-34
   DNS Servers.....................: ::
                                     0.0.0.0
```
Подключимся через консоль и введем команду ***show interface F0/1***
```
setup s1 for Lab-2

S1>show interface F0/1
FastEthernet0/1 is up, line protocol is up (connected)
  Hardware is Lance, address is 000a.f38c.3101 (bia 000a.f38c.3101)
 BW 100000 Kbit, DLY 1000 usec,
     reliability 255/255, txload 1/255, rxload 1/255
  Encapsulation ARPA, loopback not set
  Keepalive set (10 sec)
  Full-duplex, 100Mb/s
  input flow-control is off, output flow-control is off
  ARP type: ARPA, ARP Timeout 04:00:00
  Last input 00:00:08, output 00:00:05, output hang never
  Last clearing of "show interface" counters never
  Input queue: 0/75/0/0 (size/max/drops/flushes); Total output drops: 0
  Queueing strategy: fifo
  Output queue :0/40 (size/max)
  5 minute input rate 0 bits/sec, 0 packets/sec
  5 minute output rate 0 bits/sec, 0 packets/sec
     956 packets input, 193351 bytes, 0 no buffer
     Received 956 broadcasts, 0 runts, 0 giants, 0 throttles
     0 input errors, 0 CRC, 0 frame, 0 overrun, 0 ignored, 0 abort
     0 watchdog, 0 multicast, 0 pause input
     0 input packets with dribble condition detected
     2357 packets output, 263570 bytes, 0 underruns
     0 output errors, 0 collisions, 10 interface resets
     0 babbles, 0 late collision, 0 deferred
     0 lost carrier, 0 no carrier
     0 output buffer failures, 0 output buffers swapped out
```
Такую же процедуру проведем с коммутатором S2
```
setup s2 for lab-2

S2>show interface F0/1
FastEthernet0/1 is up, line protocol is up (connected)
  Hardware is Lance, address is 0001.c794.6701 (bia 0001.c794.6701)
 BW 100000 Kbit, DLY 1000 usec,
     reliability 255/255, txload 1/255, rxload 1/255
  Encapsulation ARPA, loopback not set
  Keepalive set (10 sec)
  Full-duplex, 100Mb/s
  input flow-control is off, output flow-control is off
  ARP type: ARPA, ARP Timeout 04:00:00
  Last input 00:00:08, output 00:00:05, output hang never
  Last clearing of "show interface" counters never
  Input queue: 0/75/0/0 (size/max/drops/flushes); Total output drops: 0
  Queueing strategy: fifo
  Output queue :0/40 (size/max)
  5 minute input rate 0 bits/sec, 0 packets/sec
  5 minute output rate 0 bits/sec, 0 packets/sec
     956 packets input, 193351 bytes, 0 no buffer
     Received 956 broadcasts, 0 runts, 0 giants, 0 throttles
     0 input errors, 0 CRC, 0 frame, 0 overrun, 0 ignored, 0 abort
     0 watchdog, 0 multicast, 0 pause input
     0 input packets with dribble condition detected
     2357 packets output, 263570 bytes, 0 underruns
     0 output errors, 0 collisions, 10 interface resets
     0 babbles, 0 late collision, 0 deferred
     0 lost carrier, 0 no carrier
     0 output buffer failures, 0 output buffers swapped out
```
Первая строка **FastEthernet0/1 is up, line protocol is up (connected)** означает, что интерфейсы обоих коммутаторов работают нормально и имеют состояние UP.

Зашитый **адрес BIA** на коммутаторе **S1** - **000a.f38c.3101**\
Зашитый **адрес BIA** на коммутаторе **S1** - **0001.c794.6701**

2.2 Просмотрим таблицу MAC-адресов коммутатора\

Подключимся к коммутатору S2 через консоль и просмотрим таблицу MAC-адресов
```
S2>en
Password: 
S2#show mac address-table
          Mac Address Table
-------------------------------------------

Vlan    Mac Address       Type        Ports
----    -----------       --------    -----

   1    000a.f38c.3101    DYNAMIC     Fa0/1
S2#
```
В таблице мы видим MAC-адрес 000a.f38c.3101 привязанный к порту Fa0/1

2.3 Очистка таблицы MAC-адресов\
В привелегированном режиме EXEC введем команду ***clear Mac address-table dymnamic*** затем обновим данные по уже знакомой команде ***show Mac address-table***\
Посмотрим новый отчет по MAC-адресам\
И затем снова введем команду ***show Mac address-table***\
```
S2#clear mac address-table dynamic
S2#show mac address-table
          Mac Address Table
-------------------------------------------

Vlan    Mac Address       Type        Ports
----    -----------       --------    -----

S2#
S2#show mac address-table
          Mac Address Table
-------------------------------------------

Vlan    Mac Address       Type        Ports
----    -----------       --------    -----

   1    000a.f38c.3101    DYNAMIC     Fa0/1
S2#
```
Мы можем увидеть что таблица MAC адресов сначала очистилась, потом обновилась и MAC-вдрес вновь записался

2.4 Эхо-запросы
Введем в командной строке на хосте PC-B команду ***arp -a***\
Изначально какие либо записи отсутствуют

Отправим с командной строки хоста PC-B эхо запрос на узел PC-A
```
C:\>ping 192.168.1.1

Pinging 192.168.1.1 with 32 bytes of data:

Reply from 192.168.1.1: bytes=32 time<1ms TTL=128
Reply from 192.168.1.1: bytes=32 time=1ms TTL=128
Reply from 192.168.1.1: bytes=32 time<1ms TTL=128
Reply from 192.168.1.1: bytes=32 time<1ms TTL=128

Ping statistics for 192.168.1.1:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 1ms, Average = 0ms
```
на узел S2

```
C:\>ping 192.168.1.12

Pinging 192.168.1.12 with 32 bytes of data:

Request timed out.
Request timed out.
Request timed out.
Request timed out.

Ping statistics for 192.168.1.12:
    Packets: Sent = 4, Received = 0, Lost = 4 (100% loss),
```
на узел S1

```
C:\>ping 192.168.1.11

Pinging 192.168.1.11 with 32 bytes of data:

Request timed out.
Request timed out.
Request timed out.
Request timed out.

Ping statistics for 192.168.1.11:
    Packets: Sent = 4, Received = 0, Lost = 4 (100% loss),
```
Видно, что зхо запросы приходят только на узел PC-A IP 192.168.1.1\
Запросы на узлы S1 и S2 остались без ответа

Обновим команду ***arp -a***\
Теперь у нас есть информация по MAC адрес устройства PC-A
```
C:\>arp -a
  Internet Address      Physical Address      Type
  192.168.1.1           00d0.58e8.5e5c        dynamic
```