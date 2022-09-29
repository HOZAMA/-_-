IPMI
================

Сброс пароля
----------------

* Необходим доступ по ssh в систему на хосте где находится ipmi
* Заходим в систему, устанавливаем необходимые пакеты, откуда есть доступ.
* 
```console
yum install OpenIPMI OpenIPMI-tools
```

* Далее просмотр списка юзеров
```console
ipmitool user list 1
```

* Как правило admin это №2, далее меняем пароль

```console
ipmitool user set password 2
```

Ребут IPMI(помогает при ошибке с сессиями и зависаниями)
================
Можно делать удаленно с любого хоста, на терминале где установлены все необходимые пакеты 

```console
ipmitool -I lan -U admin -H {YOUR DESIRED IP} bmc reset cold
```
Доп.
===============
* Просмотреть сетевые настройки

```console
ipmitool -I lan -U admin -H {IPMI IP ADDR} lan print 1
```

* Пример изменения default gateway

```console
ipmitool -I lan -U admin -H {IPMI IP ADDR} lan set 1 defgw ipaddr {YOUR DESIRED Default Gateway IP}
ipmitool lan set 1 ipsrc static
ipmitool lan set 1 ipaddr {IP ADDR}
ipmitool lan set 1 netmask 255.255.240.0
```

IPMI DEBUG
================

Версия утилиты для Windows доступна по ссылке: <https://drive.depo.ru/s/ipmitool>
Версия утилит для Linux систем доступны по ссылкам:
deb пакет <https://drive.depo.ru/s/CkbWWBCCEM9GeDg>
rpm пакет <https://drive.depo.ru/s/Ep3Azk7S9iJzsRn> 

После скачивания, распакуйте содержимое архива в рабочую директорию и запустите из данного расположения утилиту в командной строке с ключами, описанными ниже. Для полноты информации, необходимо выгрузить все приведенные ниже команды, которые сформируют соответствующие текстовые файлы:
```console
ipmitool -I lanplus -H x.x.x.x -U admin -P password fru >fru.txt
ipmitool -I lanplus -H x.x.x.x -U admin -P password bmc info >bmc.txt
ipmitool -I lanplus -H x.x.x.x -U admin -P password sel elist >eipmitoollog.txt
ipmitool -I lanplus -H x.x.x.x -U admin -P password -v sel list >vipmitoollog.txt
ipmitool -I lanplus -H x.x.x.x -U admin -P password sdr elist all >eipmitoolsensor.txt
ipmitool -I lanplus -H x.x.x.x -U admin -P password -v sdr list >vipmitoolsensor.txt
ipmitool -I lanplus -H x.x.x.x -U admin -P password chassis status >chassis.txt
ipmitool -I lanplus -H x.x.x.x -U admin -P password raw 0x3c 0x03 >bios.txt
```

 
Где, x - ip-адрес IPMI-интерфейса сервера;
admin - имя пользователя IPMI;
password - пароль к нему

Также Вы можете собрать логи локально без параметров -I -H -U -P из ОС, установленной на сервере. Пример:

```console
ipmitool fru >fru.txt
```

На Windows необходимо будет предварительно установить IMBD драйвер, доступный по ссылке: <https://drive.depo.ru/s/Q9iiK8oWYAsi3oF>


