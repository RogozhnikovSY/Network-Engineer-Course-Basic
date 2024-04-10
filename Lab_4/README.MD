## 4. Лабораторная работа. Настройка IPv6-адресов на сетевых устройствах
____

**Топология**

![](Img-2.png)) [//]: # (ПРИКРЕПИТЬ СКРИН ТОПОЛОГИИ)

**Таблица адресации**
| Устройство | Интерфейс | IPv6-адрес        | Длина префикса | Шлюз по умолчанию |
| ---------- | --------- | --------------- | ------------- | ------------- |
| R1         | G0/0/0    | 2001:db8:acad:a::1    | 64 | - |
|            | G0/0/1    | 2001:db8:acad:1::1    | 64 | - |
| S1         | VLAN 1    | 2001:db8:acad:1::b    | 64 | - |
| PC-A       | NIC       | 2001:db8:acad:1::3    | 64 | fe80::1 |
| PC-B       | NIC       | 2001:db8:acad:a::3    | 64 | fe80::1 |

**Задачи лабораторной работы:**
1. Настройка топологии конфигурации основных параметров маршрутизатор и коммутатора
2. Ручная настройка IPv6-адресов
3. Проверка сквозного соединения

___

**1. Создадим и настроим сеть**

В соответствии с заданной топологией смоделируем сеть в Cisco Packet Tracer

1.1. Настроим маршрутизатор\
Назначим имя хоста и настроим основные параметры устройства

```
Switch>en
Switch#conf term
Enter configuration commands, one per line.  End with CNTL/Z.
Switch(config)#hostname S1
S1(config)#service password-encryption
S1(config)#enable secret class
S1(config)#exit
S1#
%SYS-5-CONFIG_I: Configured from console by console
wr
Building configuration...
[OK]
S1#
```

1.2. Настроим коммутатор\
Назначим имя хоста и настроим основные параметры устройства
```
Router>en
Router#conf term
Enter configuration commands, one per line.  End with CNTL/Z.
Router(config)#hostname R1
R1(config)#service password-encryption
R1(config)#enable secret class
R1(config)#exit
R1#
%SYS-5-CONFIG_I: Configured from console by console
wr
Building configuration...
[OK]
R1#
```

