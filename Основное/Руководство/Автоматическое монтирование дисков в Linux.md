Чтобы автоматически подключать локальный диск при старте системы, нужно прописать его в **/etc/fstab**.

Узнаём универсальный идентификатор диска UUID (Universally Unique Identifier):
```
$ sudo blkid 
/dev/sda1: LABEL="st" UUID="36F20D4DF20D12B3" TYPE="ntfs" 
/dev/sda2: LABEL="SysWin" UUID="A4F20F67F20F3D54" TYPE="ntfs" 
/dev/sda5: UUID="1efdbdda-df38-4f60-bb2c-81996eff323c" TYPE="swap" 
/dev/sda6: UUID="1eab3a42-b6c3-44e5-9e18-2ff284ecfba3" TYPE="ext4" 
/dev/sda7: LABEL="Data" UUID="5F573D4D2CFD981F" TYPE="ntfs"
```

Для того чтобы подключить диск **Data**, который является 7-м разделом с файловой системой NTFS, редактируем /etc/fstab:
```
sudo gedit /etc/fstab &
```
### Раздел NTFS

Добавляем в fstab запись с соответствующим UUID:
```
UUID=5F573D4D2CFD981F /media/5F573D4D2CFD981F ntfs-3g rw,users,locale=ru_RU.UTF-8 0 0
```
Можно предварительно создать каталог (скажем, WinData), куда будем монтировать диск, и присвоить ему нужные права. Так, возможно, придётся поступить, если будем [расшаривать](https://www.sysadminwiki.ru/wiki/Samba "Samba") (создавать сетевой ресурс, предоставлять доступ к папкам по сети) папки с этого диска.
```
$ sudo su 
# mkdir /media/WinData 
# chmod 777 /media/WinData
```
Тогда добавляемая в fstab запись будет выглядеть так:
```
UUID=5F573D4D2CFD981F /media/WinData ntfs-3g rw,users,locale=ru_RU.UTF-8 0 0
```
### Раздел FAT и FAT32
Монтируем в каталог /media/Patition-FAT32, добавляя запись:
```
UUID=номер_UUID /media/Patition-FAT32 vfat shortname=mixed,codepage=850,umask=002,uid=1000,gid=100,noauto,user 0 0
```
### Раздел Ext4

Монтируем в каталог /media/Ubuntu20:
```
UUID=номер_UUID /media/Ubuntu20 ext4 rw,users 0 0
```
Теперь после перезагрузки указанные в fstab диски будут автоматически примонтированы и доступны для приложений.
## Работа над ошибками

Если несмотря на опцию rw файловая система Windows (ntfs, fat) подключается в режиме только для чтения (ro), то скорее всего Windows не закончила работу с файловой системой корректно. Для исправления нужно либо ещё раз загрузиться в Windows и завершить работу корректно, дождавшись завершения всех процессов, либо использовать утилиту **ntfsfix**. Подробнее читайте в описании команды **[mount](https://www.sysadminwiki.ru/wiki/Mount "Mount")**.