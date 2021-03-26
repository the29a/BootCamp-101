Mikrotik CLI

Некоторые примеры команд:

Пользователи.

По умолчанию для входа используется логин admin без пароля.
Добавление пользователя:
```use add name=имя password=пароль group=full```

Отключаемся чтобы зайти под новым пользователем:
```quit```

Отключение пользователя:
```user disable admin``

Просмотр пользователей:
```user print```

Интерфейсы.
---
Просмотр интерфесов:
```interface print```

Активация интерфейса:
```interface enable 0```

Назначение интерфейсу IP адреса:
```ip address add address 172.17.1.199/24 interface ether1```

Просмотр IP адресов:
```ip address print```

Изменение MTU интерфейсов:
```interface set 0,1,2 mtu=1500```

Изменение mac адреса интерфеса:
```/interface ethernet set ether1 mac-address=DE:AD:BE:FF:04:05```

Сброс mac адреса интерфеса:
```/interface ethernet reset-mac ether1```

Установка шлюза по умолчанию:
```ip route add gateway=10.0.10.1```

Просмотр маршрутов:
```ip route print```

Устанавливаем первичный и вторичный адреса DNS серверов:
```ip dns set primary-dns=1.1.1.1 secondary-dns=1.0.0.1 allow-remote-requests=yes```

Просмотр DNS параметров:
```ip dns print```

БЕСПРОВОДНЫЕ ИНТЕРФЕЙСЫ.
---
Просмотр беспроводных интерфейсов:
```/interface wireless print```

ВРЕМЯ.
---
Установка часового пояса:
```system clock set time-zone=+9```

Установка ip адреса ntp сервера с которым будет сверяться время:
```system ntp client set enabled=yes primary-ntp=88.147.254.230```

Просмотр времени:
```/system clock print```

ФАЕРВОЛ.
Настройка маскарадинга, чтобы чтобы внутренняя сеть не была видна с WAN порта:
```ip firewall nat add chain=srcnat action=masquerade out-interface=WAN```

Просмотр правил:
```ip firewall filter print```

Пример ограничения количества соединений с одного IP:
```/ip firewall rule forward add protocol=tcp tcp -options=syn-only connection-limit=5 action=drop```

Пример блокировки всех TCP пакетов идущих на порт 135:
```/ip firewall rule forward add dst -port=135 protocol=tcp action=drop```

Пример проброса портов:
```/ip firewall dst-nat add action=nat protocol=tcp dst-address=10.0.21.12/30:80 to-dst-address=192.168.0.4```

СИСТЕМА:
Просмотр стандартных настроек:
```/system default-configuration print```

Сброс настроек:
```/system reset-configuration```

Просмотр истории:
```/system history print```

СЛУЖБЫ.
Просмотр служб:
```/ip service print```

ПРОЧЕЕ.
Переход на уровень выше:
```/```

Выполнение команды из другого уровня без смены текущего:
Помощь:
```?```

Настройка маршрутизатора с помощью мастера настроек:
```setup```

Пинг:
```ping 1.1```

Ctrl+X — вход и выход из безопасного режима.