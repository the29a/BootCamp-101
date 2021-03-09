# 10. Настройка сети

Обзор
----
Первичная настройка сети зачастую производится при установке системы, но в дальнейшем может потребоваться изменение параметров. 

Вариантов настройки есть два: указание параметров в конфигурационном файле напрямую или использование Network Manager.

Network Manger доступен как в системах с GUI, так и в терминале с помощью nmtui\nmcli.

Настройка сети в файлах конфигурации отличается в некоторых дистрибутивах и требует отключенного Network Manger.

Файлы конфигурации сети, одинаковые для семейств дистрибутивов Debian и Centos:
Конфигурация DNS-серверов - ```/etc/resolv.conf```
Статические DNS-записи - ```/etc/hosts```
Имя текущей машины - ```/etc/hostname```

Дистрибутивозависимые файлы:
----
Конфигруационный файл Centos 
```
/etc/sysconfig/network-scripts/ifcfg-<ifacename>
```
В Centos 8 по-умолчанию убрали поддержку настройки сети через конфигурационные скрипты, поэтому установите отдельно пакет network-scripts.

Конфигруационный файл Debian
```
/etc/network/interfaces
```

Настройка с помощью NetworkManager.
----
Настройка через NetworkManager не вызывает больших сложностей. В различных DE он настраивается через апплет, а для консольной настройки можно использовать nmtui, который имеет псевдо-графический интерфейс.

Ручная настройка в файлах конфигураци
----
Для ручной настройки требуется отключить и запретить NetworkManager:
```
systemctl disable NetworkManager
systemctl mask NetworkManager
```

В случае с Centos потребуется установить пакет network-scripts и запустить демон network.
```
systemctl enable network 
```
Пример настройки для Centos:
```
BOOTPROTO="static"
IPADDR=192.168.0.140
NETMASK=255.255.255.0
GATEWAY=192.168.0.130
DNS1=192.168.0.140
ONBOOT="yes"
PREFIX=24
DEFROUTE=yes
```
Пример настройки для Debian:
```
auto eth0
iface eth0 inet static
    address 192.168.0.140
    netmask 255.255.255.0
    gateway 192.168.0.130
```

Настройка DNS-серверов:

DNS-серверы указываются в файле ```/etc/resolv.conf``` 
Синтаксис конфигурации:
```
nameserver 1.1.1.1
```
Не забываем отключать NetworkManager, так как исправления, вносимые в resolv.conf, перезатираются сервисом им при рестарте, если используется DHCP.

Тестирование работоспособности сети:
----

После всех манипуляций стоит проверить, корректно ли была настроена сеть.

Проверяем корректность указаных настроек ip и маски:
```
ip a show
```
Проверяем пинг до шлюза:
```
ping 192.168.0.130
```
Проверяем пинг до наружных ресурсов по ip:
```
ping 8.8.8.8
```
Проверяем пинг до наружных ресурсов по доменному имени:
```
ping ya.ru
```

Дополнительные ссылки:
----
[NetworkManager на ArchWiki](https://wiki.archlinux.org/index.php/NetworkManager)
[Настройка сети в Debian](https://wiki.debian.org/ru/NetworkConfiguration)

[Red Hat Configuring and managing networking](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8/html-single/configuring_and_managing_networking/index)


