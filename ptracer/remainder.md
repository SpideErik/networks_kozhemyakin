# Моя шпаргалка для команд настройки

## Как вводить

* Можно быстро через paste сразу несколько команд
* Обычно надо вводить в `Router(config)#`
    * если приглашение `Router>` надо ввести ena
    * если приглашение `Router#` надо ввести conf t


## Настройка ip для 3 интерфейсов роутера 1841

* Третий интерфейс WIC-1ENET

```
int fa 0/0
ip addr 172.16.0.1 255.255.254.0
no shutdown
exit
int fa 0/1
ip addr 172.16.2.1 255.255.255.0
no shutdown
exit
int et 0/1/0
ip addr 172.16.3.250 255.255.255.252
no shutdown
exit
```

## Настройка DHCP сервера на роутере 1841

* здесь сразу для двух интерфейсов
* еще исключен сервер и он назначен dns

```
ip dhcp excluded-address 172.16.0.1
ip dhcp excluded-address 172.16.0.11
ip dhcp excluded-address 172.16.2.1
ip dhcp pool POOL1
net 172.16.0.0 255.255.254.0
default-router 172.16.0.1
dns-server 172.16.0.11
exit
ip dhcp pool POOL2
net 172.16.2.0 255.255.255.0
default-router 172.16.2.1
dns-server 172.16.0.11
exit
```


## Настройка NAT сервера на роутере 1841

* Третий интерфейс WIC-1ENET смотрит наружу а маска задется сразу для двух интерефейсов, но можно добавить еще один acc

```
int fa 0/0
ip nat in
exit
int fa 0/1
ip nat in
exit
int et 0/1/0
ip nat out
exit
acc 1 perm 172.16.0.0 0.0.3.255
ip nat in sou li 1 int et 0/1/0 ov
```

## таблица mac в switch

```
show mac-address-table
```

