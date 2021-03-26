# 11. Настройка фаервола
-iptables   
-firewalld   

Просмотр правил:
 
```iptables -L```

Блокировка по IP:

```iptables -I INPUT -s 192.168.0.130 -j DROP```

Перенаправление портов:
```iptables -t nat -A PREROUTING -p tcp --dport 3000 -j REDIRECT --to-port 80```


Блокировка icmp:   
```iptables -A INPUT -p icmp -i enp0s3 -j DROP```

или:
```
iptables -A OUTPUT -p icmp --icmp-type echo-request -j DROP
iptables -A INPUT -p icmp --icmp-type echo-reply -j DROP
```


iptables на примере ssh
---
Чтобы открыть доступ к SSH серверу в IPTables необходимо добавить правило:   
```sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT```

Чтобы открыть доступ только конкретной сети, например 192.168.0.0/24:   
```sudo iptables -A INPUT -s 192.168.0.0/24 -p tcp --dport 22 -j ACCEPT```

Чтобы удалить правило укажем ту же команду, заменив -A на -D, например:   
```sudo iptables -D INPUT -p tcp --dport 22 -j ACCEPT```

Посмотреть список правил можно командой:   
```sudo iptables -nvL```

firewalld-
---
Просмотр имеющейся конфигурации для зоны по умолчанию   
```firewall-cmd --get-default-zone```
```firewall-cmd --list-all```

Просмотр правил для определенной зоны:   
```firewall-cmd --list-all --zone=external```

Список активных зон:  
```firewall-cmd --get-active-zones```

Cписок всех зон:   
```firewall-cmd --get-zones```

Список сервисов:   
```firewall-cmd --get-services```

Добавление сервиса к зоне:   
```firewall-cmd --zone=public --add-service=http```

Список сервисов зоны:
```firewall-cmd --zone=public --list-services```

Удаление сервиса из зоны:   
```fаirewall-cmd --permanent --zone=public --remove-service=http```

Заблокировать/разрешить ICMP ответы:
```
firewall-cmd --zone=public --add-icmp-block={echo-request,echo-reply}
firewall-cmd --list-all
firewall-cmd --zone=public --remove-icmp-block={echo-request,echo-reply}
firewall-cmd --list-all
```

Блокировка по IP:   

```firewall-cmd --add-rich-rule='rule family="ipv4" source address="192.168.100.130" reject'```

Удалить блокировку:   
```firewall-cmd --remove-rich-rule='rule family="ipv4" source address="192.168.100.130" reject'```