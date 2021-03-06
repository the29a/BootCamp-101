# 9. Поиск файлов и каталогов
Важность поиска
----

Очень важно уметь находить нужные нам файлы и папки. Как только мы получим доступ к системе на основе Linux, будет важно найти файлы конфигурации, сценарии, созданные пользователями или администратором, а также другие файлы и папки. Нам не нужно вручную просматривать каждую папку и проверять, были ли они изменены в последний раз. Есть некоторые инструменты, которые мы можем использовать, чтобы облегчить эту работу.

Which
----

Один из распространенных инструментов - which. Этот инструмент возвращает путь к файлу или ссылке, которую следует выполнить. Это позволяет нам определить, доступны ли в операционной системе определенные программы, такие как cURL, netcat, wget, python, gcc. Давайте воспользуемся им для поиска Python в нашем интерактивном экземпляре.
```
the29a@host[~]$ which python

/usr/bin/python
```
Если искомая программа не существует, результаты отображаться не будут.

Find
----

Еще один удобный инструмент - find. Помимо функции поиска файлов и папок, этот инструмент также содержит функцию фильтрации результатов. Мы можем использовать параметры фильтра, такие как размер файла или дату. Мы также можем указать, будем ли мы искать только файлы или папки.

Синтаксис:
```
the29a@host[~]$ find <location> <options>
```
Давайте посмотрим на примере того, как будет выглядеть такая команда с несколькими параметрами.
```
the29a@host[~]$ find / -type f -name *.conf -user root -size +20k -newermt 2020-03-03 -exec ls -al {} \; 2>/dev/null

-rw-r--r-- 1 root root 136392 Apr 25 20:29 /usr/src/linux-headers-5.5.0-1parrot1-amd64/include/config/auto.conf
-rw-r--r-- 1 root root 82290 Apr 25 20:29 /usr/src/linux-headers-5.5.0-1parrot1-amd64/include/config/tristate.conf
-rw-r--r-- 1 root root 95813 May  7 14:33 /usr/share/metasploit-framework/data/jtr/repeats32.conf
-rw-r--r-- 1 root root 60346 May  7 14:33 /usr/share/metasploit-framework/data/jtr/dynamic.conf
-rw-r--r-- 1 root root 96249 May  7 14:33 /usr/share/metasploit-framework/data/jtr/dumb32.conf
-rw-r--r-- 1 root root 54755 May  7 14:33 /usr/share/metasploit-framework/data/jtr/repeats16.conf
-rw-r--r-- 1 root root 22635 May  7 14:33 /usr/share/metasploit-framework/data/jtr/korelogic.conf
-rwxr-xr-x 1 root root 108534 May  7 14:33 /usr/share/metasploit-framework/data/jtr/john.conf
-rw-r--r-- 1 root root 55285 May  7 14:33 /usr/share/metasploit-framework/data/jtr/dumb16.conf
-rw-r--r-- 1 root root 21254 May  2 11:59 /usr/share/doc/sqlmap/examples/sqlmap.conf
-rw-r--r-- 1 root root 25086 Mar  4 22:04 /etc/dnsmasq.conf
-rw-r--r-- 1 root root 21254 May  2 11:59 /etc/sqlmap/sqlmap.conf
```

Теперь давайте более подробно рассмотрим параметры, которые мы использовали в предыдущей команде. Если навести указатель мыши на соответствующие параметры, появится небольшое окно с объяснением. Эти объяснения также можно найти в других модулях, которые должны нам помочь, если мы еще не знакомы с одним из инструментов.

Описание
-type f Таким образом, мы определяем тип искомого объекта. В этом случае «f» означает «файл».
-name \ *. conf С помощью '-name' мы указываем имя файла, который ищем. Звездочка (\ *) означает "все" файлы с расширением ".conf".
-user root Этот параметр фильтрует все файлы, владельцем которых является пользователь root.
-size + 20k Затем мы можем отфильтровать все обнаруженные файлы и указать, что мы хотим видеть только файлы, размер которых превышает 20 KiB.
-newermt 03.03.2020 С помощью этой опции мы устанавливаем дату. Будут представлены только файлы новее указанной даты.
-exec ls -al {} \; Эта опция выполняет указанную команду, используя фигурные скобки в качестве заполнителей для каждого результата. Обратная косая черта позволяет избежать интерпретации следующего символа оболочкой, поскольку в противном случае точка с запятой завершила бы команду и не добралась бы до перенаправления.
2> /dev/null Это перенаправление STDERR в «нулевое устройство», к которому мы вернемся в следующем разделе. Это перенаправление гарантирует, что в терминале не будут отображаться ошибки. Это перенаправление не должно быть опцией команды «find».

Locate
----
Поиск по всей системе наших файлов и каталогов для выполнения множества различных поисков займет много времени. Команда locate предлагает нам более быстрый способ поиска в системе. В отличие от команды find, locate работает с локальной базой данных, содержащей всю информацию о существующих файлах и папках. Мы можем обновить эту базу данных с помощью следующей команды.
```
the29a@host[~]$ sudo updatedb
```
Если мы теперь ищем все файлы с расширением «.conf», вы обнаружите, что этот поиск дает результаты намного быстрее, чем при использовании find.
```
the29a@host[~]$ locate *.conf

/etc/GeoIP.conf
/etc/NetworkManager/NetworkManager.conf
/etc/UPower/UPower.conf
/etc/adduser.conf
<SNIP>
```

Однако у этого инструмента не так много параметров фильтрации, которые мы могли бы использовать. Поэтому всегда стоит подумать, можем ли мы использовать команду locate или вместо нее использовать команду find. Это всегда зависит от того, что мы ищем.
