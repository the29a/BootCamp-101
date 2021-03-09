# 13. Git

Теперь, когда у нас установлен git, мы можем использовать его для загрузки полезных инструментов с Github. Один из таких проектов называется «Нишанг». Самым проектом мы займемся и поработаем позже. Во-первых, нам нужно перейти в репозиторий проекта и скопировать ссылку Github, прежде чем использовать git для его загрузки.

Тем не менее, прежде чем мы загрузим проект, его скрипты и списки, мы должны создать определенную папку.
```
the29a@host[~]$ mkdir /opt/nishang/ && git clone https://github.com/samratashok/nishang.git /opt/nishang

Cloning into '/opt/nishang/'...
remote: Enumerating objects: 15, done.
remote: Counting objects: 100% (15/15), done.
remote: Compressing objects: 100% (13/13), done.
remote: Total 1691 (delta 4), reused 6 (delta 2), pack-reused 1676
Receiving objects: 100% (1691/1691), 7.84 MiB | 4.86 MiB/s, done.
Resolving deltas: 100% (1055/1055), done.
```

Мы также можем скачать программы и инструменты из репозиториев отдельно. В этом примере мы загружаем strace для Ubuntu 18.04 LTS.
```
the29a@host[~]$ wget http://archive.ubuntu.com/ubuntu/pool/main/s/strace/strace_4.21-1ubuntu1_amd64.deb

--2020-05-15 03:27:17--  http://archive.ubuntu.com/ubuntu/pool/main/s/strace/strace_4.21-1ubuntu1_amd64.deb
Resolving archive.ubuntu.com (archive.ubuntu.com)... 91.189.88.142, 91.189.88.152, 2001:67c:1562::18, ...
Connecting to archive.ubuntu.com (archive.ubuntu.com)|91.189.88.142|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 333388 (326K) [application/x-debian-package]
Saving to: ‘strace_4.21-1ubuntu1_amd64.deb’

strace_4.21-1ubuntu1_amd64.deb       100%[===================================================================>] 325,57K  --.-KB/s    in 0,1s    

2020-05-15 03:27:18 (2,69 MB/s) - ‘strace_4.21-1ubuntu1_amd64.deb’ saved [333388/333388]
```
Кроме того, теперь мы можем использовать как apt, так и dpkg для установки пакета. Поскольку мы уже работали с apt, в следующем примере мы обратимся к dpkg.
```
he29a@host[~]$ dpkg -i strace_4.21-1ubuntu1_amd64.deb

(Reading database ... 154680 files and directories currently installed.)
Preparing to unpack strace_4.21-1ubuntu1_amd64.deb ...
Unpacking strace (4.21-1ubuntu1) over (4.21-1ubuntu1) ...
Setting up strace (4.21-1ubuntu1) ...
Processing triggers for man-db (2.8.3-2ubuntu0.1) ...
```