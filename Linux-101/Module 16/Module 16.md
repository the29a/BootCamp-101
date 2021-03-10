# 16. Система инициализации (SystemV, systemd)

- SystemV
- systemd

SystemV (не используется):
----

Использует директорию /etc/init.d для хранения скриптов загрузки сервисов
Директории /etc/rc*.d - содержат линки на скрипты в init.d.
| ------ | ------ |
| Runlevel 0 |   остановка системы |
| Runlevel 1 |  однопользовательский режим |
| Runlevel 3 | режим нормальной работы сервера без графики |
| Runlevel 5 | режим нормальной работы сервера с графикой |
| Runlevel 6 | перезагрузка системы |


systemd:
----
Актуальная система загрузки. Использует понятия unit, target.

Основная команда - systemctl

| Runlevel | Target Units |	Description |
| ------ | ------ | ------ |
| 0 | runlevel0.target, poweroff.target	| Shut down and power off the system. |
| 1 | runlevel1.target, rescue.target	|	Set up a rescue shell. |
| 2 | runlevel2.target, multi-user.target |	Set up a non-graphical multi-user system. |
| 3 | runlevel3.target, multi-user.target |	Set up a non-graphical multi-user system. |
| 4	| runlevel4.target, multi-user.target |	Set up a non-graphical multi-user system. |
| 5	| runlevel5.target, graphical.target |Set up a graphical multi-user system.|
| 6	| runlevel6.target, reboot.target |	Shut down and reboot the system. |

Изменение target:
```systemctl isolate multi-user.target```
```systemctl isolate graphical.target```

Изменение default.target:

```systemctl set-default multi-user.target```