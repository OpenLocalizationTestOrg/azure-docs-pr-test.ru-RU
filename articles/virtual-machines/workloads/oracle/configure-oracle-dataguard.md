---
title: "aaaImplement Oracle Data Guard на виртуальной машине Azure Linux | Документы Microsoft"
description: "Быстрое создание и запуск Oracle Data Guard в среде Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: v-shiuma
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/10/2017
ms.author: rclaus
ms.openlocfilehash: 6bb530098737e3ca7dd8bab3f4306ecbb620f3f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="implement-oracle-data-guard-on-an-azure-linux-virtual-machine"></a>Реализация Oracle Data Guard на виртуальной машине Azure под управлением Linux 

Azure CLI является используется toocreate и управления ресурсами Azure hello командной строке или в сценариях. В этой статье описывается, как базы данных Azure CLI toouse toodeploy базы данных Oracle 12c из образа Azure Marketplace hello. В этой статье затем показано, шаг за шагом, как tooinstall и настроить Защитник данных на виртуальной машине Azure (ВМ).

Прежде чем начать, убедитесь, что установлен интерфейс командной строки Azure CLI. Дополнительные сведения см. в разделе hello [руководство по установке Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli).

## <a name="prepare-hello-environment"></a>Подготовка среды hello
### <a name="assumptions"></a>Предположения

tooinstall Oracle Data Guard необходимо toocreate две виртуальные машины Azure на hello одной группе доступности:

- Hello основной виртуальной Машины (myVM1) имеет работающего экземпляра Oracle.
- Здравствуйте, резервной ВМ (myVM2) имеет только установлено программное обеспечение Oracle hello.

Hello образа Marketplace использовать toocreate hello виртуальных машин — Oracle: Oracle-базы данных-Ee:12.1.0.2:latest.

### <a name="sign-in-tooazure"></a>Войдите в tooAzure 

Войти в tooyour подписки Azure, используя hello [входа az](/cli/azure/#login) команды и выполните hello на экране инструкциям.

```azurecli
az login
```

### <a name="create-a-resource-group"></a>Создание группы ресурсов

Создание группы ресурсов с помощью hello [Создание группы az](/cli/azure/group#create) команды. Группа ресурсов Azure является логическим контейнером, в котором происходит развертывание ресурсов Azure и управление ими. 

Hello следующий пример создает группу ресурсов с именем `myResourceGroup` в hello `westus` расположение:

```azurecli
az group create --name myResourceGroup --location westus
```

### <a name="create-an-availability-set"></a>"Создать группу доступности"

Создавать группу доступности необязательно, но мы рекомендуем это сделать. Дополнительные сведения см. в статье [Рекомендации по группам доступности Azure для виртуальных машин Windows](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

### <a name="create-a-virtual-machine"></a>Создание виртуальной машины

Создайте виртуальную Машину с помощью hello [создания виртуальной машины az](/cli/azure/vm#create) команды. 

Hello следующий пример создает две виртуальные машины с именем `myVM1` и `myVM2`. Также создаются ключи SSH, если они не существуют в расположении ключей по умолчанию. toouse конкретный набор ключей, используйте hello `--ssh-key-value` параметр.

Создайте myVM1 (основная):
```azurecli
az vm create \
     --resource-group myResourceGroup \
     --name myVM1 \
     --availability-set myAvailabilitySet \
     --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
     --size Standard_DS1_v2  \
     --admin-username azureuser \
     --generate-ssh-keys \
```

После создания виртуальной Машины hello Azure CLI показано toohello аналогичные сведения, следующий пример. Обратите внимание значение hello `publicIpAddress`. Используется этот адрес tooaccess hello виртуальной Машины.

```azurecli
{
  "fqdns": "",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "westus",
  "macAddress": "00-0D-3A-36-2F-56",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "13.64.104.241",
  "resourceGroup": "myResourceGroup"
}
```

Создайте myVM2 (резервная):
```azurecli
az vm create \
     --resource-group myResourceGroup \
     --name myVM2 \
     --availability-set myAvailabilitySet \
     --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
     --size Standard_DS1_v2  \
     --admin-username azureuser \
     --generate-ssh-keys \
```

Обратите внимание значение hello `publicIpAddress` после создания myVM2.

### <a name="open-hello-tcp-port-for-connectivity"></a>Привет открыть TCP-порт для подключения к

Этот шаг позволяет настроить внешние конечные точки, которые позволяют базы данных Oracle toohello удаленного доступа.

Откройте порт hello для myVM1:

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVM1NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

Hello результат должен выглядеть примерно toohello следующий ответ:

```bash
{
  "access": "Allow",
  "description": null,
  "destinationAddressPrefix": "*",
  "destinationPortRange": "1521",
  "direction": "Inbound",
  "etag": "W/\"bd77dcae-e5fd-4bd6-a632-26045b646414\"",
  "id": "/subscriptions/<subscription-id>/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myVmNSG/securityRules/allow-oracle",
  "name": "allow-oracle",
  "priority": 999,
  "protocol": "Tcp",
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "sourceAddressPrefix": "*",
  "sourcePortRange": "*"
}
```

Откройте порт hello для myVM2:

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVM2NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

### <a name="connect-toohello-virtual-machine"></a>Подключение toohello виртуальной машины

Используйте hello следующая команда toocreate сеанс SSH с виртуальной машиной hello. Замените hello hello IP-адрес `publicIpAddress` значение для виртуальной машины.

```bash 
$ ssh azureuser@<publicIpAddress>
```

### <a name="create-hello-database-on-myvm1-primary"></a>Создать hello базы данных на myVM1 (основной)

Hello программное обеспечение Oracle уже установлен на образа Marketplace hello, поэтому hello следующим шагом является база данных tooinstall hello. 

Переключение toohello Oracle суперпользователя:

```bash
$ sudo su - oracle
```

Создайте базу данных hello:

```bash
$ dbca -silent \
   -createDatabase \
   -templateName General_Purpose.dbc \
   -gdbname cdb1 \
   -sid cdb1 \
   -responseFile NO_VALUE \
   -characterSet AL32UTF8 \
   -sysPassword OraPasswd1 \
   -systemPassword OraPasswd1 \
   -createAsContainerDatabase true \
   -numberOfPDBs 1 \
   -pdbName pdb1 \
   -pdbAdminPassword OraPasswd1 \
   -databaseType MULTIPURPOSE \
   -automaticMemoryManagement false \
   -storageType FS \
   -ignorePreReqs
```
Выходные данные должен выглядеть примерно toohello следующий ответ:

```bash
Copying database files
1% complete
2% complete
8% complete
13% complete
19% complete
27% complete
Creating and starting Oracle instance
29% complete
32% complete
33% complete
34% complete
38% complete
42% complete
43% complete
45% complete
Completing Database Creation
48% complete
51% complete
53% complete
62% complete
70% complete
72% complete
Creating Pluggable Databases
78% complete
100% complete
Look at hello log file "/u01/app/oracle/cfgtoollogs/dbca/cdb1/cdb1.log" for further details.
```

Задайте переменные ORACLE_SID и ORACLE_HOME hello.

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=cdb1; export ORACLE_SID
```

При необходимости можно добавить ORACLE_HOME и ORACLE_SID файла toohello /home/oracle/.bashrc, чтобы эти параметры сохраняются для будущих имен входа:

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
```

## <a name="configure-data-guard"></a>Настройка Data Guard

### <a name="enable-archive-log-mode-on-myvm1-primary"></a>Включение режима журнала архивирования на myVM1 (основная)

```bash
$ sqlplus / as sysdba
SQL> SELECT log_mode FROM v$database;

LOG_MODE
------------
NOARCHIVELOG

SQL> SHUTDOWN IMMEDIATE;
SQL> STARTUP MOUNT;
SQL> ALTER DATABASE ARCHIVELOG;
SQL> ALTER DATABASE OPEN;
```
Включите принудительное ведение журнала и убедитесь, что есть хотя бы один файл журнала:

```bash
SQL> ALTER DATABASE FORCE LOGGING;
SQL> ALTER SYSTEM SWITCH LOGFILE;
```

Создайте резервные журналы повторяемых операций:

```bash
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo01.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo02.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo03.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo04.log') SIZE 50M;
```

Включить переключение обратно (в результате восстановления намного проще) и задайте STANDBY\_ФАЙЛ\_tooauto УПРАВЛЕНИЯ. Затем выйдите из SQL*Plus.

```bash
SQL> ALTER DATABASE FLASHBACK ON;
SQL> ALTER SYSTEM SET STANDBY_FILE_MANAGEMENT=AUTO;
SQL> EXIT;
```

### <a name="set-up-service-on-myvm1-primary"></a>Настройка службы на myVM1 (основная)

Изменить или создать файл tnsnames.ora hello, который находится в папке ORACLE_HOME\network\admin hello $.

Добавьте hello следующие записи:

```bash
cdb1 =
  (DESCRIPTION =
    (ADDRESS_LIST =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM1)(PORT = 1521))
    )
    (CONNECT_DATA =
      (SID = cdb1)
    )
  )

cdb1_stby =
  (DESCRIPTION =
    (ADDRESS_LIST =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM2)(PORT = 1521))
    )
    (CONNECT_DATA =
      (SID = cdb1)
    )
  )
```

Изменить или создать файл listener.ora hello, который находится в папке ORACLE_HOME\network\admin hello $.

Добавьте hello следующие записи:

```bash
LISTENER =
  (DESCRIPTION_LIST =
    (DESCRIPTION =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM1)(PORT = 1521))
      (ADDRESS = (PROTOCOL = IPC)(KEY = EXTPROC1521))
    )
  )

SID_LIST_LISTENER =
  (SID_LIST =
    (SID_DESC =
      (GLOBAL_DBNAME = cdb1_DGMGRL)
      (ORACLE_HOME = /u01/app/oracle/product/12.1.0/dbhome_1)
      (SID_NAME = cdb1)
    )
  )

ADR_BASE_LISTENER = /u01/app/oracle
```

Включите брокер Data Guard:
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```
Запуск прослушивателя hello:

```bash
$ lsnrctl stop
$ lsnrctl start
```

### <a name="set-up-service-on-myvm2-standby"></a>Настройка службы на myVM2 (резервная)

SSH toomyVM2:

```bash 
$ ssh azureuser@<publicIpAddress>
```

Выполните вход в качестве пользователя Oracle:

```bash
$ sudo su - oracle
```

Изменить или создать файл tnsnames.ora hello, который находится в папке ORACLE_HOME\network\admin hello $.

Добавьте hello следующие записи:

```bash
cdb1 =
  (DESCRIPTION =
    (ADDRESS_LIST =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM1)(PORT = 1521))
    )
    (CONNECT_DATA =
      (SID = cdb1)
    )
  )

cdb1_stby =
  (DESCRIPTION =
    (ADDRESS_LIST =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM2)(PORT = 1521))
    )
    (CONNECT_DATA =
      (SID = cdb1)
    )
  )
```

Изменить или создать файл listener.ora hello, который находится в папке ORACLE_HOME\network\admin hello $.

Добавьте hello следующие записи:

```bash
LISTENER =
  (DESCRIPTION_LIST =
    (DESCRIPTION =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM2)(PORT = 1521))
      (ADDRESS = (PROTOCOL = IPC)(KEY = EXTPROC1521))
    )
  )

SID_LIST_LISTENER =
  (SID_LIST =
    (SID_DESC =
      (GLOBAL_DBNAME = cdb1_DGMGRL)
      (ORACLE_HOME = /u01/app/oracle/product/12.1.0/dbhome_1)
      (SID_NAME = cdb1)
    )
  )

ADR_BASE_LISTENER = /u01/app/oracle
```

Запуск прослушивателя hello:

```bash
$ lsnrctl stop
$ lsnrctl start
```


### <a name="restore-hello-database-toomyvm2-standby"></a>Восстановление базы данных toomyVM2 hello (резервного)

Создайте файл /tmp/initcdb1_stby.ora hello параметр с hello после содержимого:
```bash
*.db_name='cdb1'
```

Создайте папки:

```bash
mkdir -p /u01/app/oracle/oradata/cdb1/pdbseed
mkdir -p /u01/app/oracle/oradata/cdb1/pdb1
mkdir -p /u01/app/oracle/fast_recovery_area/cdb1
mkdir -p /u01/app/oracle/admin/cdb1/adump
```

Создайте файл пароля:

```bash
$ orapwd file=/u01/app/oracle/product/12.1.0/dbhome_1/dbs/orapwcdb1 password=OraPasswd1 entries=10
```
Начало myVM2 hello базы данных:

```bash
$ export ORACLE_SID=cdb1
$ sqlplus / as sysdba

SQL> STARTUP NOMOUNT PFILE='/tmp/initcdb1_stby.ora';
SQL> EXIT;
```

Восстановление базы данных hello с помощью средства RMAN hello:

```bash
$ rman TARGET sys/OraPasswd1@cdb1 AUXILIARY sys/OraPasswd1@cdb1_stby
```

Выполните следующие команды в RMAN hello.
```bash
DUPLICATE TARGET DATABASE
  FOR STANDBY
  FROM ACTIVE DATABASE
  DORECOVER
  SPFILE
    SET db_unique_name='CDB1_STBY' COMMENT 'Is standby'
  NOFILENAMECHECK;
```

После завершения команды hello вы увидите примерно следующие toohello сообщений. Выйдите из RMAN.
```bash
media recovery complete, elapsed time: 00:00:00
Finished recover at 29-JUN-17
Finished Duplicate Db at 29-JUN-17

RMAN> EXIT;
```

При необходимости можно добавить ORACLE_HOME и ORACLE_SID файла toohello /home/oracle/.bashrc, чтобы эти параметры сохраняются для будущих имен входа:

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
```

Включите брокер Data Guard:
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```

### <a name="configure-data-guard-broker-on-myvm1-primary"></a>Настройка брокера Data Guard на myVM1 (основная)

Запустите диспетчер Data Guard и войдите, используя SYS и пароль. (Не используйте аутентификацию операционной системы.) Выполните следующие hello.

```bash
$ dgmgrl sys/OraPasswd1@cdb1
DGMGRL for Linux: Version 12.1.0.2.0 - 64bit Production

Copyright (c) 2000, 2013, Oracle. All rights reserved.

Welcome tooDGMGRL, type "help" for information.
Connected as SYSDBA.
DGMGRL> CREATE CONFIGURATION my_dg_config AS PRIMARY DATABASE IS cdb1 CONNECT IDENTIFIER IS cdb1;
Configuration "my_dg_config" created with primary database "cdb1"
DGMGRL> ADD DATABASE cdb1_stby AS CONNECT IDENTIFIER IS cdb1_stby MAINTAINED AS PHYSICAL;
Database "cdb1_stby" added
DGMGRL> ENABLE CONFIGURATION;
Enabled.
```

Проверить настройку hello:
```bash
DGMGRL> SHOW CONFIGURATION;

Configuration - my_dg_config

  Protection Mode: MaxPerformance
  Members:
  cdb1      - Primary database
    cdb1_stby - Physical standby database

Fast-Start Failover: DISABLED

Configuration Status:
SUCCESS   (status updated 26 seconds ago)
```

После завершения установки Oracle Data Guard hello. Hello следующем разделе показано, как tootest hello подключения и переключиться.

### <a name="connect-hello-database-from-hello-client-machine"></a>Подключение базы данных hello из hello клиентского компьютера

Обновить или создать файл tnsnames.ora hello на клиентском компьютере. Этот файл обычно находится в папке $ORACLE_HOME\network\admin.

Замените hello IP-адресов с вашей `publicIpAddress` значения myVM1 и myVM2:

```bash
cdb1=
  (DESCRIPTION=
    (ADDRESS=
      (PROTOCOL=TCP)
      (HOST=<myVM1 IP address>)
      (PORT=1521)
    )
    (CONNECT_DATA=
      (SERVER=dedicated)
      (SERVICE_NAME=cdb1)
    )
  )

cdb1_stby=
  (DESCRIPTION=
    (ADDRESS=
      (PROTOCOL=TCP)
      (HOST=<myVM2 IP address>)
      (PORT=1521)
    )
    (CONNECT_DATA=
      (SERVER=dedicated)
      (SERVICE_NAME=cdb1_stby)
    )
  )
```

Запустите SQL*Plus:

```bash
$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```
## <a name="test-hello-data-guard-configuration"></a>Конфигурация Data Guard hello теста

### <a name="switch-over-hello-database-on-myvm1-primary"></a>Переключить базу данных hello на myVM1 (основной)

tooswitch из первичного toostandby (cdb1 toocdb1_stby):

```bash
$ dgmgrl sys/OraPasswd1@cdb1
DGMGRL for Linux: Version 12.1.0.2.0 - 64bit Production

Copyright (c) 2000, 2013, Oracle. All rights reserved.

Welcome tooDGMGRL, type "help" for information.
Connected as SYSDBA.
DGMGRL> SWITCHOVER toocdb1_stby;
Performing switchover NOW, please wait...
Operation requires a connection tooinstance "cdb1" on database "cdb1_stby"
Connecting tooinstance "cdb1"...
Connected as SYSDBA.
New primary database "cdb1_stby" is opening...
Operation requires start up of instance "cdb1" on database "cdb1"
Starting instance "cdb1"...
ORACLE instance started.
Database mounted.
Switchover succeeded, new primary is "cdb1_stby"
DGMGRL>
```

Теперь можно подключиться toohello резервной базы данных.

Запустите SQL*Plus:

```bash

$ sqlplus sys/OraPasswd1@cdb1_stby
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

### <a name="switch-over-hello-database-on-myvm2-standby"></a>Переключить базу данных hello на myVM2 (резервного)

tooswitch, выполните следующие hello на myVM2:
```bash
$ dgmgrl sys/OraPasswd1@cdb1_stby
DGMGRL for Linux: Version 12.1.0.2.0 - 64bit Production

Copyright (c) 2000, 2013, Oracle. All rights reserved.

Welcome tooDGMGRL, type "help" for information.
Connected as SYSDBA.
DGMGRL> SWITCHOVER toocdb1;
Performing switchover NOW, please wait...
Operation requires a connection tooinstance "cdb1" on database "cdb1"
Connecting tooinstance "cdb1"...
Connected as SYSDBA.
New primary database "cdb1" is opening...
Operation requires start up of instance "cdb1" on database "cdb1_stby"
Starting instance "cdb1"...
ORACLE instance started.
Database mounted.
Switchover succeeded, new primary is "cdb1"
```

Опять же теперь должен быть доступ tooconnect toohello базы данных-источника.

Запустите SQL*Plus:

```bash

$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

После завершения установки hello и настройки защиты данных в Oracle Linux.


## <a name="delete-hello-virtual-machine"></a>Удалить виртуальную машину hello

При hello ВМ больше не нужна, можно использовать следующие команды tooremove hello группы ресурсов, виртуальная машина и все связанные ресурсы hello:

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Дальнейшие действия

[Создание полной среды Linux с помощью Azure CLI 2.0](../../linux/create-cli-complete.md)

[Примеры Azure CLI для виртуальных машин Linux](../../linux/cli-samples.md).
