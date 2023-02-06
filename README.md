# Компьютерная сеть организации с информационной инфраструктурой
***
Моделирование компьютерной сети в Cisco Packet Tracer производится следующим образом:
1) Размещение необходимого сетевого оборудования и конечных устройств;
2) Создание подсетей на коммутаторах L2 и присваивание им имен. Пример создания vlan 10 на коммутаторе Switch1:
```
Switch(config)# vlan 10
Switch(config-vlan)# name ANI
Switch(config-vlan)# exit
```

3) Назначение trunk и access портов. Пример назначения портов на комму-таторе Switch1:
```
Switch (config)# interface range f 0/1-17
Switch (config-if)# switchport mode access
Switch (config-if)# switchport access vlan 10
Switch (config-if)# no shutdown
Switch (config-if)# exit
Switch (config)# interface range g 0/1-2
Switch (config-if)# switchport mode trunk
Switch (config-if)# switchport trunk allowed vlan 1,10
Switch (config-if)# no shutdown
Switch (config-if)# exit
```
4) Проверка правильность настроек при помощи команд show run и show vlan brief. .

 ![error](![image](https://user-images.githubusercontent.com/124536839/216854582-49853fa8-3afb-45ed-9c28-ea3d93bba130.png)
)

Результат выполнения команд на Switch1

5) Создание подсетей на коммутаторах L3 и присваивание им имен. При-мер создания vlan 10 на коммутаторе Multilayer Switch1:
```
Switch(config)# vlan 10
Switch(config-vlan)# name ANI
Switch(config-vlan)# exit
```
6) Назначение trunk портов. Пример назначения портов на коммутаторе Multilayer Switch1:
```
Switch (config)# interface g 1/0/3
Switch (config-if)# switchport mode trunk encapsulation dot1q
Switch (config-if)# switchport trunk allowed vlan 1,20,90
Switch (config-if)# no shutdown
Switch (config-if)# exit
```
7) Назначение ip-адресов интерфейсов. Пример назначения ip-адресов для интерфейса vlan 10 коммутаторf Multilayer Switch1:
```
Switch (config)#int vlan 10
Switch (config-if)#ip address 192.168.19.0 255.255.255.224
Switch (config-if)# exit
```
8) Перевод интерфейса, подключаемого к маршрутизатору, в режим рабо-ты третьего уровня и назначение ему ip-адреса. На примере Multilayer Switch1:
```
Switch (config)#interface g 1/0/10
Switch (config-if)# no switchport
Switch (config-if)# ip address 192.168.20.242 255.255.255.248
Switch (config-if)# no shutdown
```
9) Настройка маршрута по умолчанию. На примере Multilayer Switch1:
```
Switch (config) ip route 0.0.0.0 0.0.0.0 192.168.20.241
```
10) Настройка пересылки протокола DHCP. На примере интерфейса vlan 10 Multilayer Switch1:
```
Switch (config)# int vlan 10
Switch (config)# ip helper-address 192.168.19.169
Switch (config)# exit
```
11) Настройка протокола динамической маршрутизации OSPF. На приме-ре Multilayer Switch1:
```
Switch (config)#router ospf 1
Switch (config-router)#network 192.168.19.0 0.0.0.31 area 1
Switch (config-router)#network 192.168.19.32 0.0.0.31 area 1
Switch (config-router)#network 192.168.19.64 0.0.0.31 area 1
Switch (config-router)#network 192.168.19.96 0.0.0.31 area 1
Switch (config-router)#network 192.168.19.128 0.0.0.31 area 1
Switch (config-router)#network 192.168.19.160 0.0.0.15 area 1
Switch (config-router)#network 192.168.19.176 0.0.0.15 area 1
Switch (config-router)#network 192.168.19.192 0.0.0.15 area 1
Switch (config-router)#network 192.168.19.208 0.0.0.15 area 1
Switch (config-router)#network 192.168.19.224 0.0.0.15 area 1
```
12) Настройка агрегирования каналов с помощью протокола LACP. На примере Multilayer Switch1:
```
Switch(config)#interface g 1/0/1-2
Switch(config-if-range)#shutdown
Switch(config-if-range)#channel-group 1 mode on
Switch(config-if-range)#no shutdown
```
13) Настройка ACP для каждой подсети. На примере Multilayer Switch1:
```
Switch(config)# ip access-list extended VLAN60
Switch(config-ext-nacl)#permit ip any host 192.168.19.169
Switch(config-ext-nacl)#permit ip any host 192.168.19.164
Switch(config-ext-nacl)#permit ip any host 192.168.19.165
Switch(config-ext-nacl)#permit ip any host 192.168.19.167
Switch(config-ext-nacl)#permit ip 192.168.19.128 0.0.0.31 host 192.168.19.163
Switch(config-ext-nacl)#permit ip 192.168.19.224 0.0.0.15 host 192.168.19.163
Switch(config-ext-nacl)#permit ip 192.168.19.224 0.0.0.15 host 192.168.19.166
Switch(config-ext-nacl)#permit ip 192.168.19.224 0.0.0.15 host 192.168.19.168
Switch(config-ext-nacl)#permit ip 192.168.19.160 0.0.0.15 any
Switch(config-ext-nacl)#permit ip 192.168.19.176 0.0.0.15 host 192.168.19.168
Switch(config-ext-nacl)#permit ip 192.168.19.192 0.0.0.15 host 192.168.19.166
Switch(config-ext-nacl)#permit ip 192.168.19.208 0.0.0.15 host 192.168.19.166
Switch(config-if-range)#exit
Switch(config)# interface vlan 60
Switch (config-if)# ip access-group VLAN60 out
Switch(config-if)#exit
```
14) Проверка правильность настроек. Результат выполнения команды show vlan brief на Multilayer Switch1представлен на рисунке 8.

 

Рисунок 8 – Результат выполнения команд на Multilayer Switch1
Результат выполнения команды show interfaces trunk на Multilayer Switch1представлен на рисунке 9.

 

Рисунок 9 – Результат выполнения команд на Multilayer Switch1

Результат выполнения команды show ip route на Multilayer Switch1представлен на рисунке 10.

 

Рисунок 10 – Результат выполнения команд на Multilayer Switch1

Результат выполнения команды show etherchannel summary на Multilayer Switch1представлен на рисунке 11.


 

Рисунок 11 – Результат выполнения команд на Multilayer Switch1

Результат выполнения команды show access-list summary на Multilayer Switch1представлен на рисунке 12.

 

Рисунок 12 – Результат выполнения команд на Multilayer Switch1

15) Подключение сетевое оборудования и конечные устройства.
16) Настройка серверного оборудования. Настройка Email сервера пред-ставлена на рисунке 13.

 

Рисунок 13 – Настройка Email сервера
Настройка DHCP сервера представлена на рисунке 14.

 

Рисунок 14 – Настройка DHCP сервера

Настройка FTP сервера представлена на рисунке 15.

 

Рисунок 15 – Настройка FTP сервера

Настройка DNS сервера представлена на рисунке 16.

 

Рисунок 16 – Настройка DNS сервера

Настройка HTTP сервера представлена на рисунке 17.

 

Рисунок 17 – Настройка HTTP сервера

Аналогичным образом настраиваются Video и 1С сервера.
17) Настройка NAT на маршрутизаторе. Интерфейсы маршрутизатора Router0 Gig 0/1 и Gig 0/2 являются внутренними, а интерфейс Gig 0/0 – внешним.
```
Router(config)#interface g 0/0
Router(config-if)#ip address 192.168.20.241 255.255.255.248
Router(config-if)#no shut
Router(config-if)#exit
Router(config)#interface g 0/1
Router(config-if)#ip address 192.168.19.241 255.255.255.0
Router(config-if)#no shut
Router(config-if)#exit
Router(config)#interface g 0/2
Router(config-if)#ip address 192.168.21.241 255.255.255.0
Router(config-if)#no shut
Router(config-if)#exit
Router (config)# ip access-list NAT
Router (config-ext-nacl)#permit 192.168.19.0 0.0.0.31
Router (config-ext-nacl)#permit 192.168.19.32 0.0.0.31
Router (config-ext-nacl)#permit 192.168.19.64 0.0.0.31
Router (config-ext-nacl)#permit 192.168.19.96 0.0.0.31
Router (config-ext-nacl)#permit 192.168.19.160 0.0.0.15
Router (config-ext-nacl)#permit 192.168.19.176 0.0.0.15
Router (config-ext-nacl)#permit 192.168.19.192 0.0.0.15
Router (config-ext-nacl)#permit 192.168.19.224 0.0.0.15
Router(config-ext-nacl)#exit
Router(config)#interface g 0/0
Router(config-if)#ip nat outside
Router(config-if)#exit
Router(config)#interface g 0/1
Router(config-if)#ip nat inside
Router(config-if)#exit
Router(config)#interface g 0/2
Router(config-if)#ip nat inside
Router(config-if)#exit
Router(config)#ip nat inside source list NAT interface g 0/0 overload
Router(config-if)#end
```
18) Проверка работоспособности сети. Проверка доступа к глобальной се-ти с компьютера, имеющего доступ к ней представлена на рисунке 18

 

Рисунок 18 – Проверка доступа к глобальной сети

19) Проверка доступа к серверу 1С с компьютера, не имеющего доступ к нему представлена на рисунке 19

 

Рисунок 19 – Проверка доступа к серверу 1С

На основании проведенной проверки был сделан вывод что настройка сети выполнена правильно.
