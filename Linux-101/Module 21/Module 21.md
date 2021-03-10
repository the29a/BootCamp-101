# 21.  Безопасность Linux

Всем компьютерным системам присущ риск вторжения. Некоторые представляют больший риск, чем другие, например, доступный в Интернет веб-сервер, на котором размещено несколько сложных веб-приложений. Системы Linux также менее подвержены вирусам, поражающим операционные системы Windows, и не представляют такой большой площади для атак, как узлы, присоединенные к домену Active Directory. Тем не менее, важно иметь определенные основы для защиты любой системы Linux.

Одной из наиболее важных мер безопасности операционных систем Linux является своевременное обновление ОС и установленных пакетов. Этого можно добиться с помощью такой команды, как:
```
the29a@host[~] $ apt update && apt dist-upgrade
```
Если правила брандмауэра не установлены должным образом на уровне сети, мы можем использовать брандмауэр Linux и/или iptables для ограничения входящего и исходящего трафика на хост.

Если на сервере открыт SSH, конфигурация должна быть настроена так, чтобы запретить вход по паролю и запретить пользователю root вход через SSH. Также важно по возможности избегать входа в систему и администрирования системы как пользователя root, а также адекватно управлять контролем доступа. Доступ пользователей должен определяться по принципу наименьших привилегий. Например, если пользователю необходимо запустить команду от имени пользователя root, эта команда должна быть указана в конфигурации sudoers вместо предоставления им полных прав sudo. Другой распространенный механизм защиты, который можно использовать, - это fail2ban. Этот инструмент подсчитывает количество неудачных попыток входа в систему, и, если пользователь достиг максимального числа, хост, который пытался подключиться, будет обработан в соответствии с настройками.

Также важно периодически проверять систему, чтобы убедиться, что не существует проблем, которые могут способствовать повышению привилегий, таких как устаревшее ядро, проблемы с разрешениями пользователей, файлы, доступные для записи всем, и неправильно настроенные задания cron или неправильно настроенные службы. Многие администраторы забывают о возможности обновления некоторых версий ядра вручную.

Вариант для дальнейшей блокировки систем Linux - Linux с усиленной безопасностью (SELinux) или AppArmor. Это модуль безопасности ядра, который можно использовать для политик управления безопасным доступом. В SELinux каждому процессу, файлу, каталогу и системному объекту присваивается метка. Правила политики создаются для управления доступом между этими помеченными процессами и объектами и применяются ядром. Это означает, что можно настроить доступ, чтобы контролировать, какие пользователи и приложения могут получить доступ к каким ресурсам. SELinux обеспечивает очень детальный контроль доступа, например, указание, кто может добавлять или перемещать файл.

Кроме того, существуют различные приложения и службы, такие как Snort, chkrootkit, rkhunter, Lynis и другие, которые могут способствовать безопасности Linux. Кроме того, следует выполнить некоторые настройки безопасности, например:

    Удаление или отключение всех ненужных сервисов и программного обеспечения
    Удаление всех сервисов, использующих незашифрованные механизмы аутентификации.
    Убедитесь, что NTP включен и Syslog запущен
    Убедитесь, что у каждого пользователя есть собственная учетная запись
    Принудительно используйте надежные пароли
    Настройте устаревание пароля и ограничьте использование предыдущих паролей
    Блокировка учетных записей пользователей после сбоев входа в систему
    Отключите все нежелательные двоичные файлы SUID / SGID

Этот список неполный, поскольку безопасность - это не продукт, а процесс. Это означает, что всегда необходимо предпринимать определенные шаги для лучшей защиты систем, и это зависит от администраторов, насколько хорошо они знают свои операционные системы. Чем лучше администраторы знакомы с системой и чем больше они обучены, тем лучше и безопаснее будут их меры безопасности и меры безопасности.