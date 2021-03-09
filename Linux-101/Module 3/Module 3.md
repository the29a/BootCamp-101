Встроенная документация и man-pages
=======
* whatis
* man
* -h
* apropos

Мы всегда будем сталкиваться с инструментами, необязательные параметры которых мы не знаем из памяти, или с инструментами, которых мы никогда раньше не видели. Поэтому очень важно знать, как мы можем помочь себе познакомиться с этими инструментами. Первые два способа - это страницы руководства и функции справки.

Всегда полезно сначала ознакомиться с инструментом, который мы хотим попробовать. Мы также узнаем некоторые возможные уловки с некоторыми инструментами, которые, как нам казалось, были невозможны. На страницах руководства мы найдем подробные руководства с подробными объяснениями.

whatis
-----
Краткое описание команды мы может получить с помощью whatis

Синтаксис:
the29a@host[~]$ whatis <tool>

Пример:
```
the29a@host:[~}$ whatis curl
curl (1)             - transfer a URL
```

man
-----
Синтаксис:
the29a@host[~]$ man <tool>

Давайте посмотрим на пример:
Пример:
```
the29a@host[~]$ man curl
AME
       curl - transfer a URL

SYNOPSIS
       curl [options / URLs]

DESCRIPTION
       curl  is  a  tool  to  transfer data from or to a server, using one of the supported protocols (DICT, FILE, FTP, FTPS, GOPHER, HTTP, HTTPS,
       IMAP, IMAPS, LDAP, LDAPS, MQTT, POP3, POP3S, RTMP, RTMPS, RTSP, SCP, SFTP, SMB, SMBS, SMTP, SMTPS, TELNET and TFTP).  The  command  is  de‐
       signed to work without user interaction.
```

Посмотрев несколько примеров, мы также можем быстро просмотреть дополнительные параметры, не просматривая всю документацию. У нас есть несколько способов сделать это.

-h
-----
Синтаксис:
the29a@host[~]$ <tool> --help

Пример:
````
the29a@host[~]$ curl --help


Usage: curl [options...] <url>
     --abstract-unix-socket <path> Connect via abstract Unix domain socket
     --anyauth       Pick any authentication method
 -a, --append        Append to target file when uploading
     --basic         Use HTTP Basic Authentication
     --cacert <file> CA certificate to verify peer against
     --capath <dir>  CA directory to verify peer against
 -E, --cert <certificate[:password]> Client certificate file and password
```
Вы также можете использовать его сокращенную версию:
Синтаксис:

the29a@host[~]$  <tool> -h

Пример:
```
the29a@host[~]$ curl -h

Usage: curl [options...] <url>
     --abstract-unix-socket <path> Connect via abstract Unix domain socket
     --anyauth       Pick any authentication method
 -a, --append        Append to target file when uploading
     --basic         Use HTTP Basic Authentication
     --cacert <file> CA certificate to verify peer against
     --capath <dir>  CA directory to verify peer against
 -E, --cert <certificate[:password]> Client certificate file and password
 ````

 Как видим, результаты друг от друга в этом примере не отличаются. Другой инструмент, который может пригодиться вначале, - это apropos. На каждой странице руководства есть краткое описание. Этот инструмент ищет в описаниях экземпляры данного ключевого слова.
Синтаксис:

apropos
-----

```
the29a@host[~]$ apropos <keyword>

Пример:
the29a@host[~]$ apropos sudo
sudo (8)             - execute a command as another user
sudo.conf (5)        - configuration for sudo front end
sudo_plugin (8)      - Sudo Plugin API
sudo_root (8)        - How to run administrative commands
sudoedit (8)         - execute a command as another user
sudoers (5)          - default sudo security policy plugin
sudoreplay (8)       - replay sudo session logs
visudo (8)           - edit the sudoers file
````
Еще один полезный ресурс для получения помощи, если у нас есть проблемы с пониманием длинной команды: https://explainshell.com/
