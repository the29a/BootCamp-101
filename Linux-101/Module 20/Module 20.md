# 20. Монтирование внешних носителей и ресурсов

Подключаем диск и ищем его в списке дисков:
```sudo fdisk -l```

Создаем папку для точки монтирования и монтируем жесткий диск:
```
sudo mkdir /media/hdd1
sudo mount -t ntfs /dev/sdb1 /media/hdd1
```
И после этого смонтировать с полным доступом:
```sudo mount -t ntfs /dev/sdb1 /media/hdd1```

Отмонтировать можно так:
```sudo umount -t ntfs /dev/sdb1 /media/hdd1```

Возможные проблемы при монтировании ntfs
---
При монтировании может возникнуть следующая ошибка:
```

    The disk contains an unclean file system (0, 0).
    Metadata kept in Windows cache, refused to mount.
    Failed to mount ‘/dev/sdb1’: Операция не позволена
    The NTFS partition is in an unsafe state. Please resume and shutdown
    Windows fully (no hibernation or fast restarting), or mount the volume
    read-only with the ‘ro’ mount option.
```
Мможно смонтировать раздел в режиме только для чтения:
```sudo mount -t ntfs -o ro /dev/sdb1 /newhdd1```
Или исправить разделы:

```sudo ntfsfix /dev/sdb1```