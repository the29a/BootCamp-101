# 15. Управление пользователями

Управление пользователями - важная часть администрирования Linux. Иногда нам нужно создать новых пользователей или добавить других пользователей в определенные группы. Другая возможность - выполнять команды от имени другого пользователя.

В конце концов, не так уж редко пользователи одной конкретной группы имеют разрешения на просмотр или редактирование определенных файлов или каталогов. 

Основные файлы, которые содержат информацию о пользователях и группах:

```/etc/passwd``` - список пользователей 
```/etc/group```  - список групп 
```/etc/shadow``` - БД паролей и параметров безопасности

Давайте посмотрим на следующий пример того, как выполнять код от имени другого пользователя.

Выполняем от user:
```
the29a@host[~]$ cat /etc/shadow
cat: /etc/shadow: Permission denied
```

Выполняем от root
```
the29a@host[~]$ sudo cat /etc/shadow
root:<SNIP>:18395:0:99999:7:::
daemon:*:17737:0:99999:7:::
bin:*:17737:0:99999:7:::
```
Вот список команд, который поможет нам лучше понять и разобраться с управлением пользователями.

| Команда | описание |
| ------ | ------ |
| sudo | Выполнить команду от имени другого пользователя |
| su | Утилита su запрашивает соответствующие учетные данные пользователя через PAM и переключается на этот идентификатор пользователя (пользователь по умолчанию - суперпользователь). Затем выполняется оболочка. |
| useradd | Создает нового пользователя или обновляет информацию о новом пользователе по умолчанию. |
| userdel | Удаляет учетную запись пользователя и связанные файлы |
| usermod | Изменяет учетную запись пользователя |
| addgroup | Добавляет группу в систему |
| delgroup | Удаляет группу из системы |
| passwd | Изменяет пароль пользователя |
| chage | изменение срока жизни пароля и др. параметров |

Разберем на примерах:
Создание нового пользователя или обновление информации о новом пользователе по умолчанию: 
```
the29a@host[~]$ useradd test
```
Удаление учетной записи пользователя и связанные файлы
```
the29a@host[~]$ userdel test
```
Принадлежность к группам:
```
the29a@host[~]$ usermod -G group1 -g test test
```
Установка домашнего каталога:
```
the29a@host[~]$ usermod -d /home/test test
```
Добавление новой группы:
```
the29a@host[~]$ groupadd group1
```
Изменение пароля пользователя:
```
the29a@host[~]$ passwd test
```
Блокировка:
```
the29a@host[~]$ passwd -l test
```
Чтобы снять блокировку можно задать новый пароль.

Проверка:
```
the29a@host[~]$ id test
```
Управление пользователями необходимо в любой операционной системе, и лучший способ познакомиться с ним - это попробовать отдельные команды в сочетании с их различными параметрами.
