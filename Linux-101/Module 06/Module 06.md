# 6. Работа с файлами и каталогами

Создание, перемещение и копирование
----
Затем давайте поработаем с файлами и каталогами и узнаем, как создавать, переименовывать, перемещать, копировать и удалять. Сначала создадим пустой файл и каталог. Мы можем использовать touch для создания пустого файла и mkdir для создания каталога.

Синтаксис для этого следующий:
```
the29a@host[~]$ touch <name>
the29a@host[~]$ mkdir <name>
```
В этом примере мы называем файл info.txt и каталог Storage. Чтобы создать их, мы следуем командам и их синтаксису, показанным выше.

- Создать пустой файл
```
the29a@host[~]$ touch info.txt
```
- Создать каталог
```
the29a@host[~]$ mkdir Storage
```
Мы можем захотеть иметь определенные каталоги в каталоге, и создание этой команды для каждого отдельного каталога потребует очень много времени. У команды mkdir есть опция с пометкой -p для добавления родительских каталогов.
```
the29a@host[~]$ mkdir -p Storage/local/user/documents
```
Мы можем посмотреть на всю структуру после создания родительских каталогов с помощью утилиты tree.
```
the29a@host[~]$ tree .

.
├── info.txt
└── Storage
    └── local
        └── user
            └── documents
```

4 directories, 1 file

Мы также можем создавать файлы прямо в каталогах, указав путь, по которому файл должен храниться. Хитрость заключается в том, чтобы использовать одну точку (.), Чтобы сообщить системе, что мы хотим начать с текущего каталога. Итак, команда для создания еще одного пустого файла выглядит так:
Создайте userinfo.txt

```
the29a@host[~]$ touch ./Storage/local/user/userinfo.txt
the29a@host[~]$ tree .

.
├── info.txt
└── Storage
    └── local
        └── user
            ├── documents
            └── userinfo.txt

4 directories, 2 files
```
С помощью команды mv мы можем перемещать, а также переименовывать файлы и каталоги. Синтаксис для этого выглядит так:
```
the29a@host[~]$ mv <file/directory> <renamed file/directory>
```
Сначала переименуем файл info.txt в information.txt, а затем переместим его в каталог Storage.

- Переименовать файл
```
the29a@host[~]$ mv info.txt information.txt
```
Теперь давайте создадим файл с именем readme.txt в текущем каталоге, а затем скопируем файлы information.txt и readme.txt в каталог Storage /.

создать readme.txt
```
the29a@host[~]$ touch readme.txt 
```
Переместить файлы в определенный каталог
```
the29a@host[~]$ mv information.txt readme.txt Storage/
he29a@host[~]$ tree .

.
└── Storage
    ├── information.txt
    ├── local
    │   └── user
    │       ├── documents
    │       └── userinfo.txt
    └── readme.txt

4 directories, 3 files
```
Предположим, мы хотим, чтобы файл readme.txt находился в каталоге local /. Затем мы можем скопировать их туда с указанными путями.

Скопируйте readme.txt
```
the29a@host[~]$ cp Storage/readme.txt Storage/local/
```
Теперь мы можем проверить, используя утилиту tree.
```
the29a@host[~]$ tree .

.
└── Storage
    ├── information.txt
    ├── local
    │   ├── readme.txt
    │   └── user
    │       ├── documents
    │       └── userinfo.txt
    └── readme.txt

4 directories, 4 files
```