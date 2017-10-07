---
title: "aaaCreate базы данных Oracle на виртуальной Машине Azure | Документы Microsoft"
description: "Быстрое создание и запуск базы данных Oracle 12c в среде Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: rickstercdn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/17/2017
ms.author: rclaus
ms.openlocfilehash: 83205154c3275d5f57b46c8acfb0cb4e5c68a412
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-oracle-database-in-an-azure-vm"></a>Создание базы данных Oracle на виртуальной машине Azure

В этом руководстве рассматривается использование hello Azure CLI toodeploy виртуальной машине Azure из hello [образ из коллекции marketplace Oracle](https://azuremarketplace.microsoft.com/marketplace/apps/Oracle.OracleDatabase12102EnterpriseEdition?tab=Overview) чтобы toocreate базы данных Oracle 12 c. После развертывания сервера hello нужно будет подключиться по протоколу SSH в базе данных Oracle hello tooconfigure заказа. 

Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/?WT.mc_id=A261C142F), прежде чем начинать работу.

[!INCLUDE [cloud-shell-try-it.md](../../../../includes/cloud-shell-try-it.md)]

Если выбрать tooinstall и использовать hello CLI локально, краткого руководства требуется управлением hello Azure CLI версия 2.0.4 или более поздней версии. Запустите `az --version` версии toofind hello. Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).

## <a name="create-a-resource-group"></a>Создание группы ресурсов

Создание группы ресурсов с hello [Создание группы az](/cli/azure/group#create) команды. Группа ресурсов Azure является логическим контейнером, в котором происходит развертывание ресурсов Azure и управление ими. 

Hello следующий пример создает группу ресурсов с именем *myResourceGroup* в hello *eastus* расположение.

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```
## <a name="create-virtual-machine"></a>Создание виртуальной машины

toocreate виртуальной машины (VM), использовать hello [создания виртуальной машины az](/cli/azure/vm#create) команды. 

Hello следующий пример создает Виртуальную машину с именем `myVM`. Также создаются ключи SSH, если они не существуют в расположении ключей по умолчанию. toouse конкретный набор ключей, используйте hello `--ssh-key-value` параметр.  

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
    --size Standard_DS2_v2 \
    --admin-username azureuser \
    --generate-ssh-keys
```

После создания виртуальной Машины hello Azure CLI отображает toohello аналогичные сведения, следующий пример. Запомните значение hello для `publicIpAddress`. Используется этот адрес tooaccess hello виртуальной Машины.

```azurecli
{
  "fqdns": "",
  "id": "/subscriptions/{snip}/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "westus",
  "macAddress": "00-0D-3A-36-2F-56",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "13.64.104.241",
  "resourceGroup": "myResourceGroup"
}
```

## <a name="connect-toohello-vm"></a>Подключение toohello виртуальной Машины

toocreate сеанс SSH с hello виртуальной Машины, используйте следующую команду hello. Замените hello hello IP-адрес `publicIpAddress` значение для виртуальной Машины.

```bash 
ssh <publicIpAddress>
```

## <a name="create-hello-database"></a>Создание базы данных hello

Hello программное обеспечение Oracle уже установлены на образа Marketplace hello. Создайте пример базы данных, как описано ниже. 

1.  Переключение toohello *oracle* суперпользователя, а затем инициализировать прослушиватель hello для ведения журнала:

    ```bash
    $ sudo su - oracle
    $ lsnrctl start
    ```

    Hello выходные данные выглядят аналогично toohello следующее:

    ```bash
    Copyright (c) 1991, 2014, Oracle.  All rights reserved.

    Starting /u01/app/oracle/product/12.1.0/dbhome_1/bin/tnslsnr: please wait...

    TNSLSNR for Linux: Version 12.1.0.2.0 - Production
    Log messages written too/u01/app/oracle/diag/tnslsnr/myVM/listener/alert/log.xml
    Listening on: (DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=myVM.twltkue3xvsujaz1bvlrhfuiwf.dx.internal.cloudapp.net)(PORT=1521)))

    Connecting too(ADDRESS=(PROTOCOL=tcp)(HOST=)(PORT=1521))
    STATUS of hello LISTENER
    ------------------------
    Alias                     LISTENER
    Version                   TNSLSNR for Linux: Version 12.1.0.2.0 - Production
    Start Date                23-MAR-2017 15:32:08
    Uptime                    0 days 0 hr. 0 min. 0 sec
    Trace Level               off
    Security                  ON: Local OS Authentication
    SNMP                      OFF
    Listener Log File         /u01/app/oracle/diag/tnslsnr/myVM/listener/alert/log.xml
    Listening Endpoints Summary...
    (DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=myVM.twltkue3xvsujaz1bvlrhfuiwf.dx.internal.cloudapp.net)(PORT=1521)))
    hello listener supports no services
    hello command completed successfully
    ```

2.  Создайте базу данных hello:

    ```bash
    dbca -silent \
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

    Он принимает несколько баз данных hello toocreate минут.

3. Задайте переменные Oracle.

Перед подключением необходимо tooset двух переменных среды: *ORACLE_HOME* и *ORACLE_SID*.

```bash
ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
ORACLE_SID=cdb1; export ORACLE_SID
```
Также можно добавить ORACLE_HOME и ORACLE_SID файл .bashrc toohello переменных. Это может сэкономить hello переменные среды для будущих входа в систему. Подтвердите hello следующие операторы были добавлены toohello `~/.bashrc` файла с помощью редактора по своему усмотрению.

```bash
# Add ORACLE_HOME. 
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1 
# Add ORACLE_SID. 
export ORACLE_SID=cdb1 
```

## <a name="oracle-em-express-connectivity"></a>Подключение к Oracle EM Express

Средства управления графического интерфейса пользователя, который можно использовать tooexplore hello базы данных, настроить Oracle EM Express. tooOracle tooconnect EM Express, необходимо сначала настроить порт hello в Oracle. 

1. Подключение базы данных tooyour, с помощью sqlplus:

    ```bash
    sqlplus / as sysdba
    ```

2. После подключения задайте порт hello 5502 для EM, экспресс-выпуск

    ```bash
    exec DBMS_XDB_CONFIG.SETHTTPSPORT(5502);
    ```

3. Привет открыть контейнер PDB1 случае hello уже открыт, но сначала проверить его состояние:

    ```bash
    select con_id, name, open_mode from v$pdbs;
    ```

    Hello выходные данные выглядят аналогично toohello следующее:

    ```bash
      CON_ID NAME                           OPEN_MODE 
      ----------- ------------------------- ---------- 
      2           PDB$SEED                  READ ONLY 
      3           PDB1                      MOUNT
    ```

4. Если hello OPEN_MODE для `PDB1` не чтения и записи, затем запустите hello следующие команды tooopen PDB1:

   ```bash
    alter session set container=pdb1;
    alter database open;
   ```

Требуется tootype `quit` tooend hello sqlplus сеанса и тип `exit` toologout пользователя oracle hello.

## <a name="automate-database-startup-and-shutdown"></a>Автоматизация запуска и завершения работы базы данных

Hello базы данных Oracle по умолчанию не запускается автоматически при перезагрузке hello виртуальной Машины. tooset копирование toostart базы данных Oracle hello автоматически, выполните вход как корень. Затем создайте и обновите некоторые системные файлы.

1. Войдите с правами привилегированного пользователя.
    ```bash
    sudo su -
    ```

2.  Используя текстовый редактор, измените файл hello `/etc/oratab` и изменить по умолчанию hello `N` слишком`Y`:

    ```bash
    cdb1:/u01/app/oracle/product/12.1.0/dbhome_1:Y
    ```

3.  Создайте файл с именем `/etc/init.d/dbora` и вставить hello содержимое:

    ```
    #!/bin/sh
    # chkconfig: 345 99 10
    # Description: Oracle auto start-stop script.
    #
    # Set ORA_HOME toobe equivalent too$ORACLE_HOME.
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle

    case "$1" in
    'start')
        # Start hello Oracle databases:
        # hello following command assumes that hello Oracle sign-in
        # will not prompt hello user for any values.
        # Remove "&" if you don't want startup as a background process.
        su - $ORA_OWNER -c "$ORA_HOME/bin/dbstart $ORA_HOME" &
        touch /var/lock/subsys/dbora
        ;;

    'stop')
        # Stop hello Oracle databases:
        # hello following command assumes that hello Oracle sign-in
        # will not prompt hello user for any values.
        su - $ORA_OWNER -c "$ORA_HOME/bin/dbshut $ORA_HOME" &
        rm -f /var/lock/subsys/dbora
        ;;
    esac
    ```

4.  Измените разрешения для файлов с помощью команды *chmod*:

    ```bash
    chgrp dba /etc/init.d/dbora
    chmod 750 /etc/init.d/dbora
    ```

5.  Создайте символьные ссылки для запуска и завершения работы:

    ```bash
    ln -s /etc/init.d/dbora /etc/rc.d/rc0.d/K01dbora
    ln -s /etc/init.d/dbora /etc/rc.d/rc3.d/S99dbora
    ln -s /etc/init.d/dbora /etc/rc.d/rc5.d/S99dbora
    ```

6.  tootest изменения, перезапустите hello виртуальной Машины:

    ```bash
    reboot
    ```

## <a name="open-ports-for-connectivity"></a>Открытие портов для подключения

Последняя задача Hello является tooconfigure некоторые внешние конечные точки. tooset копирование hello Azure сетевой группы безопасности, защищающий hello ВМ, сначала закрыть сеанс SSH в hello виртуальной Машины (должен был запущен вне SSH при перезагрузке в предыдущем шаге). 

1.  tooopen конечную точку hello удаленно, использовании базы данных Oracle hello tooaccess, создайте правило группы безопасности сети с [создать правило nsg сети az](/cli/azure/network/nsg/rule#create) следующим образом: 

    ```azurecli-interactive
    az network nsg rule create \
        --resource-group myResourceGroup\
        --nsg-name myVmNSG \
        --name allow-oracle \
        --protocol tcp \
        --priority 1001 \
        --destination-port-range 1521
    ```

2.  tooopen конечную точку hello удаленно, используйте tooaccess Oracle EM Express, создайте правило группы безопасности сети с [создать правило nsg сети az](/cli/azure/network/nsg/rule#create) следующим образом:

    ```azurecli-interactive
    az network nsg rule create \
        --resource-group myResourceGroup \
        --nsg-name myVmNSG \
        --name allow-oracle-EM \
        --protocol tcp \
        --priority 1002 \
        --destination-port-range 5502
    ```

3. При необходимости получить hello общедоступный IP-адрес виртуальной Машины с [az сети public-ip show](/cli/azure/network/public-ip#show) следующим образом:

    ```azurecli-interactive
    az network public-ip show \
        --resource-group myResourceGroup \
        --name myVMPublicIP \
        --query [ipAddress] \
        --output tsv
    ```

4.  Подключите EM Express с помощью браузера. Убедитесь, что браузер совместим с EM Express (также необходимо установить Flash). 

    ```
    https://<VM ip address or hostname>:5502/em
    ```

Вы можете войти с помощью hello **SYS** учетную запись, а также проверьте hello **как sysdba** флажок. Использовать пароль hello **OraPasswd1** , заданным во время установки. 

![Снимок экрана со страницей входа Oracle OEM Express hello](./media/oracle-quick-start/oracle_oem_express_login.png)

## <a name="clean-up-resources"></a>Очистка ресурсов

Когда Вы завершили изучение первой базы данных Oracle в Azure и hello ВМ больше не нужен, можно использовать hello [удаление группы az](/cli/azure/group#delete) команд группы ресурсов tooremove hello, виртуальных Машин и все связанные ресурсы.

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Дальнейшие действия

Узнайте о других [решениях Oracle в Azure](oracle-considerations.md). 

Повторите hello [Установка и настройка управления хранением автоматических Oracle](configure-oracle-asm.md) учебника.
