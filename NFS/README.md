# Настройка NFS шары
Установка:
```
sudo apt update -y
sudo apt install nfs-utils nfs-kernel-server -y
```
Проверим что порт 2049 прослушивается:
```
ss -l4nt
```
Создадим тестовую папку с файлами (в данном случае создаем папку в домашней директории):
```
mkdir data-nfs
touch data-nfs/file{1..3}
```

Отредактируем конфигурационный файл:
```
sudo nano /etc/exports

/home/user/data-nfs     192.168.0.110(rw,no_root_squash,subtree_check)
```

Применим конфигурацию:
```
sudo exportfs -av
sudo exportfs -s
```
Замонтируем нашу шару, чтобы протестировать что всё работает:
```
sudo mount 192.168.0.110:/home/user/data-nfs /mnt
ls -la /mnt
```