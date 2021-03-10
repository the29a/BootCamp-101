# 17.   Управление сервисами и процессами


В общем, существует два типа служб: внутренние, соответствующие службы, которые требуются при запуске системы, например, для выполнения задач, связанных с оборудованием, и службы, устанавливаемые пользователем, которые обычно включают в себя все серверные службы. Такие службы работают в фоновом режиме без какого-либо взаимодействия с пользователем. Они также называются демонами и обозначаются буквой «d» в конце имени программы, например sshd или systemd.

Большинство дистрибутивов Linux теперь перешли на systemd. Этот демон представляет собой процесс Init, который запускается первым и поэтому имеет идентификатор процесса (PID) 1. Этот демон отслеживает и заботится о правильном запуске и остановке других служб.

Всем процессам назначен PID, который можно просмотреть в /proc/ с соответствующим номером. Такой процесс может иметь идентификатор родительского процесса (PPID), известный как дочерний процесс.

Помимо systemctl мы также можем использовать update-rc.d для управления ссылками на сценарий инициализации SysV. Давайте посмотрим на несколько примеров. В этих примерах мы будем использовать сервер OpenSSH. Если он не установлен, установите его, прежде чем переходить к этому разделу.

Получить список выполняемых процессов:

```the29a@host[~]$ ps```
В терминале увидите приерно такой результат:
```
PID TTY          TIME CMD
8199 pts/0    00:00:01 bash
1623 pts/0    00:00:00 ps
```
Мы получили номер процесса (PID), терминал откуда процесс был запущен (pts/0), 
затраченное процессорное время и команду, запустившую процесс.


Systemctl
---
После установки OpenSSH на нашу виртуальную машину мы можем запустить службу с помощью следующей команды.
```the29a@host[~]$ systemctl start ssh```

После того, как мы запустили службу, теперь мы можем проверить, работает ли она без ошибок.

```
 ssh.service - OpenBSD Secure Shell server
   Loaded: loaded (/lib/systemd/system/ssh.service; enabled; vendor preset: enabled)
   Active: active (running) since Thu 2020-05-14 15:08:23 CEST; 24h ago
   Main PID: 846 (sshd)
   Tasks: 1 (limit: 4681)
   CGroup: /system.slice/ssh.service
           └─846 /usr/sbin/sshd -D the29a@host[/~]$ systemctl status ssh
```        
Чтобы добавить OpenSSH в сценарий SysV, чтобы система запускала эту службу после запуска, мы можем связать ее с помощью следующей команды:
```
the29a@host[/~]$ systemctl enable ssh

Synchronizing state of ssh.service with SysV service script with /lib/systemd/systemd-sysv-install.
Executing: /lib/systemd/systemd-sysv-install enable ssh
```
После перезагрузки системы автоматически запустится сервер OpenSSH. Мы можем проверить это с помощью инструмента ps.
```
the29a@host[~]$ ps -aux | grep ssh

root       846  0.0  0.1  72300  5660 ?        Ss   Mai14   0:00 /usr/sbin/sshd -D
```
Мы также можем использовать systemctl для вывода списка всех сервисов.
```
the29a@host[~]$ > systemctl list-units --type=service

UNIT                                                       LOAD   ACTIVE SUB     DESCRIPTION              
accounts-daemon.service                                    loaded active running Accounts Service         
acpid.service                                              loaded active running ACPI event daemon        
apache2.service                                            loaded active running The Apache HTTP Server   
apparmor.service                                           loaded active exited  AppArmor initialization  
apport.service                                             loaded active exited  LSB: automatic crash repor
avahi-daemon.service                                       loaded active running Avahi mDNS/DNS-SD Stack  
bolt.service                                               loaded active running Thunderbolt system service
```
Вполне возможно, что сервисы не запускаются из-за ошибки. Чтобы увидеть проблему, мы можем использовать инструмент journalctl для просмотра журналов.
```
the29a@host[~]$ journalctl -u ssh.service --no-pager

-- Logs begin at Wed 2020-05-13 17:30:52 CEST, end at Fri 2020-05-15 16:00:14 CEST. --
Mai 13 20:38:44 inlane systemd[1]: Starting OpenBSD Secure Shell server...
Mai 13 20:38:44 inlane sshd[2722]: Server listening on 0.0.0.0 port 22.
Mai 13 20:38:44 inlane sshd[2722]: Server listening on :: port 22.
Mai 13 20:38:44 inlane systemd[1]: Started OpenBSD Secure Shell server.
Mai 13 20:39:06 inlane sshd[3939]: Connection closed by 10.22.2.1 port 36444 [preauth]
Mai 13 20:39:27 inlane sshd[3942]: Accepted password for master from 10.22.2.1 port 36452 ssh2
Mai 13 20:39:27 inlane sshd[3942]: pam_unix(sshd:session): session opened for user master by (uid=0)
Mai 13 20:39:28 inlane sshd[3942]: pam_unix(sshd:session): session closed for user master
Mai 14 02:04:49 inlane sshd[2722]: Received signal 15; terminating.
Mai 14 02:04:49 inlane systemd[1]: Stopping OpenBSD Secure Shell server...
Mai 14 02:04:49 inlane systemd[1]: Stopped OpenBSD Secure Shell server.
-- Reboot --
```
Процесс может находиться в следующих состояниях:
    Running
    Waiting (ожидание события или системного ресурса)
    Stopped
    Zombie (остановлен, но все еще есть запись в таблице процессов).
    
Процессами можно управлять с помощью kill, pkill, pgrep и killall. Чтобы взаимодействовать с процессом, мы должны послать ему сигнал. Мы можем просмотреть все сигналы с помощью следующей команды:
```
the29a@htb[~]$ kill -l
1) SIGHUP       2) SIGINT       3) SIGQUIT      4) SIGILL       5) SIGTRAP
 1) SIGABRT      7) SIGBUS       8) SIGFPE       9) SIGKILL     10) SIGUSR1
2)  SIGSEGV     12) SIGUSR2     13) SIGPIPE     14) SIGALRM     15) SIGTERM
3)  SIGSTKFLT   17) SIGCHLD     18) SIGCONT     19) SIGSTOP     20) SIGTSTP
4)  SIGTTIN     22) SIGTTOU     23) SIGURG      24) SIGXCPU     25) SIGXFSZ
5)  SIGVTALRM   27) SIGPROF     28) SIGWINCH    29) SIGIO       30) SIGPWR
6)  SIGSYS      34) SIGRTMIN    35) SIGRTMIN+1  36) SIGRTMIN+2  37) SIGRTMIN+3
7)  SIGRTMIN+4  39) SIGRTMIN+5  40) SIGRTMIN+6  41) SIGRTMIN+7  42) SIGRTMIN+8
8)  SIGRTMIN+9  44) SIGRTMIN+10 45) SIGRTMIN+11 46) SIGRTMIN+12 47) SIGRTMIN+13
9)  SIGRTMIN+14 49) SIGRTMIN+15 50) SIGRTMAX-14 51) SIGRTMAX-13 52) SIGRTMAX-12
10) SIGRTMAX-11 54) SIGRTMAX-10 55) SIGRTMAX-9  56) SIGRTMAX-8  57) SIGRTMAX-7
11) SIGRTMAX-6  59) SIGRTMAX-5  60) SIGRTMAX-4  61) SIGRTMAX-3  62) SIGRTMAX-2
12) SIGRTMAX-1  64) SIGRTMAX
```
Чаще всего используются:
Сигнал Описание 
1 	SIGHUP - Он отправляется процессу, когда терминал, который его контролирует, закрывается.
2 	SIGINT - Отправляется, когда пользователь нажимает [Ctrl] + C в управляющем терминале, чтобы прервать процесс.
3 	SIGQUIT - Отправляется, когда пользователь нажимает [Ctrl] + D для выхода.
9 	SIGKILL - Немедленно завершает процесс без операций очистки.
15 	SIGTERM - Прекращение действия программы.
19 	SIGSTOP -  сигнал, посылаемый для принудительной приостановки выполнения процесса.
20 	SIGTSTP - Отправляется, когда пользователь нажимает [Ctrl] + Z, чтобы запросить приостановку службы. Пользователь может с этим процессом работать позже.

Например, если программа зависла, мы могли принудительно убить ее с помощью следующей команды:
```the29a@host[~]$ kill 9 <PID> ```