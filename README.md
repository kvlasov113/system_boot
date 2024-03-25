# system_boot

## Способы восстановления доступа суперпользователя

### 1. init=/bin/sh.
Во время выбора ядра для заугрузки нажать <<e>>.
В строку начинающуюся с linux16 в конец добаить init=/bin/sh

См. криншоты 1.1 и 1.2

### 2. rd.break
Во время выбора ядра для заугрузки нажать <<e>>.
В строку начинающуюся с linux16 в конец добаить rd.break

[root@otuslinux ~]# mount -o remount,rw /sysroot
[root@otuslinux ~]# chroot /sysroot
[root@otuslinux ~]# passwd root
[root@otuslinux ~]# touch /.autorelabel

См. скриншот 2.1 2.2

