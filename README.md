# system_boot

## Способы восстановления доступа суперпользователя

### 1. init=/bin/sh.
Во время выбора ядра для заугрузки нажать <<e>>.
В строку начинающуюся с linux16 в конец добаить init=/bin/sh

### скриншоты 1_1, 1_2

### 2. rd.break
Во время выбора ядра для заугрузки нажать <<e>>.
В строку начинающуюся с linux16 в конец добаить rd.break

[root@otuslinux ~]# mount -o remount,rw /sysroot
[root@otuslinux ~]# chroot /sysroot
[root@otuslinux ~]# passwd root
[root@otuslinux ~]# touch /.autorelabel

### скриншоты 2_1, 2_2

### 3. init=/sysroot/bin/sh

Во время выбора ядра для заугрузки нажать <<e>>.
В строке начинающейся с linux16 заменāем ro на rw init=/sysroot/bin/sh
Файловая система сразу смотнтирована в ржим Read-Write

### скришоты 3_1, 3_2

## Переименовать VG

[root@otuslinux ~]# vgrename VolGroup00 OtusRoot

Правим /etc/fstab, /etc/default/grub, /boot/grub2/grub.cfg.

Пример использвоания sed
[root@lvm vagrant]# sed -i "s/VolGroup00/OtusRoot/g" /etc/default/grub 

[root@otuslinux ~]# mkinitrd -f -v /boot/initramfs-$(uname -r).img $(uname -r)

### См. changeVG.log

## Добавить модуль в initrd

Создадим директорию для скриптов модуля 
[root@otuslinux ~]# mkdir /usr/lib/dracut/modules.d/01test

### Скрипты и лог в приложении.

[root@otuslinux ~]# mkinitrd -f -v /boot/initramfs-$(uname -r).img $(uname -r)
или
[root@otuslinux ~]# dracut -f -v


