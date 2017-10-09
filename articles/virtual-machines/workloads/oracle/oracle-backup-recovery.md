---
title: "aaaBack копирование и восстановление базы данных Oracle 12c базы данных на виртуальной машине Azure Linux | Документы Microsoft"
description: "Узнайте, как tooback копирование и восстановление базы данных Oracle 12c базы данных в среде Azure."
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
ms.date: 5/17/2017
ms.author: rclaus
ms.openlocfilehash: 68846f4efce5eabdb71cd71772e003838154e93b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-and-recover-an-oracle-database-12c-database-on-an-azure-linux-virtual-machine"></a>Создание резервных копий и восстановление базы данных Oracle Database 12c на виртуальной машине Linux в Azure

Можно использовать toocreate Azure CLI и настраивать ресурсы Azure, в командной строке или с помощью скриптов. В этой статье мы используем toodeploy Azure CLI скриптов базы данных Oracle 12c базы данных из коллекции образов Azure Marketplace.

Прежде чем начать, убедитесь, что установлен Azure CLI. Дополнительные сведения см. в разделе hello [руководство по установке Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli).

## <a name="prepare-hello-environment"></a>Подготовка среды hello

### <a name="step-1-prerequisites"></a>Шаг 1. Предварительные требования

*   tooperform hello резервного копирования и восстановления, необходимо сначала создать ВМ Linux, который имеет установленный экземпляр базы данных Oracle 12c. образа Marketplace Hello использовать ВМ называется hello toocreate *Oracle: Oracle-базы данных-Ee:12.1.0.2:latest*.

    toolearn toocreate базы данных Oracle, в статье hello [Oracle создать быстрый запуск базы данных](https://docs.microsoft.com/azure/virtual-machines/workloads/oracle/oracle-database-quick-create).


### <a name="step-2-connect-toohello-vm"></a>Шаг 2: Подключение toohello виртуальной Машины

*   toocreate Secure Shell (SSH) сеанс с hello виртуальной Машины, используйте следующую команду hello. Замените hello hello IP-адреса и именем сайта hello `publicIpAddress` значение для виртуальной Машины.

    ```bash 
    ssh <publicIpAddress>
    ```

### <a name="step-3-prepare-hello-database"></a>Шаг 3: Подготовка базы данных hello

1.  Чтобы перейти к выполнению этого шага, у вас должен быть экземпляр Oracle (cdb1), выполняющийся на виртуальной машине с именем *myVM*.

    Запустите hello *oracle* корневой суперпользователя, а затем инициализировать прослушиватель hello:

    ```bash
    $ sudo su - oracle
    $ lsnrctl start
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

2.  (Необязательно) Убедитесь, что hello база данных находится в режиме журнала архива:

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
    SQL> ALTER SYSTEM SWITCH LOGFILE;
    ```
3.  (Необязательно) Создайте фиксации hello tootest таблицы:

    ```bash
    SQL> alter session set "_ORACLE_SCRIPT"=true ;
    Session altered.
    SQL> create user scott identified by tiger;
    User created.
    SQL> grant create session tooscott;
    Grant succeeded.
    SQL> grant create table tooscott;
    Grant succeeded.
    SQL> alter user scott quota 100M on users;
    User altered.
    SQL> connect scott/tiger
    SQL> create table scott_table(col1 number, col2 varchar2(50));
    Table created.
    SQL> insert into scott_Table VALUES(1,'Line 1');
    1 row created.
    SQL> commit;
    Commit complete.
    ```
4.  Проверить или изменить размер и расположение файла резервной копии hello:

    ```bash
    $ sqlplus / as sysdba
    SQL> show parameter db_recovery
    NAME                                 TYPE        VALUE
    ------------------------------------ ----------- ------------------------------
    db_recovery_file_dest                string      /u01/app/oracle/fast_recovery_area
    db_recovery_file_dest_size           big integer 4560M
    ```
5. Используйте диспетчер восстановления Oracle (RMAN) tooback hello базы данных:

    ```bash
    $ rman target /
    RMAN> backup database plus archivelog;
    ```

### <a name="step-4-application-consistent-backup-for-linux-vms"></a>Шаг 4. Согласованное с приложениями резервное копирование для виртуальных машин Linux

Согласованное с приложениями резервное копирование — это новая функция в службе Azure Backup. Можно создать и выбрать tooexecute скрипты до и после моментального снимка виртуальной Машины hello (перед созданием моментального снимка и после создания моментального снимка).

1. Загрузите файл JSON hello.

    Скачайте файл VMSnapshotScriptPluginConfig.json со страницы https://github.com/MicrosoftAzureBackup/VMSnapshotPluginConfig. содержимое файла Hello выглядеть аналогично toohello следующее:

    ```azurecli
    {
        "pluginName" : "ScriptRunner",
        "preScriptLocation" : "",
        "postScriptLocation" : "",
        "preScriptParams" : ["", ""],
        "postScriptParams" : ["", ""],
        "preScriptNoOfRetries" : 0,
        "postScriptNoOfRetries" : 0,
        "timeoutInSeconds" : 30,
        "continueBackupOnFailure" : true,
        "fsFreezeEnabled" : true
    }
    ```

2. Создайте папку /etc/azure hello на hello виртуальной Машины:

    ```bash
    $ sudo su -
    # mkdir /etc/azure
    # cd /etc/azure
    ```

3. Скопируйте файл JSON hello.

    Скопируйте папку /etc/azure toohello VMSnapshotScriptPluginConfig.json.

4. Измените файл JSON hello.

    Изменение файла tooinclude hello VMSnapshotScriptPluginConfig.json hello `PreScriptLocation` и `PostScriptlocation` параметров. Например:

    ```azurecli
    {
        "pluginName" : "ScriptRunner",
        "preScriptLocation" : "/etc/azure/pre_script.sh",
        "postScriptLocation" : "/etc/azure/post_script.sh",
        "preScriptParams" : ["", ""],
        "postScriptParams" : ["", ""],
        "preScriptNoOfRetries" : 0,
        "postScriptNoOfRetries" : 0,
        "timeoutInSeconds" : 30,
        "continueBackupOnFailure" : true,
        "fsFreezeEnabled" : true
    }
    ```

5. Создайте hello файлы скриптов перед созданием моментального снимка и после моментального снимка.

    Вот пример скриптов, выполняемых до и после создания моментальных снимков, для холодного резервного копирования (автономное резервное копирование с завершением работы и перезагрузкой):

    Для /etc/azure/pre_script.sh:

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "$ORA_HOME/bin/dbshut $ORA_HOME" > /etc/azure/pre_script_$v_date.log
    ```

    Для /etc/azure/post_script.sh:

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "$ORA_HOME/bin/dbstart $ORA_HOME" > /etc/azure/post_script_$v_date.log
    ```

    Вот пример скриптов, выполняемых до и после создания моментальных снимков, для горячего резервного копирования (оперативное резервное копирование):

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "sqlplus / as sysdba @/etc/azure/pre_script.sql" > /etc/azure/pre_script_$v_date.log
    ```

    Для /etc/azure/post_script.sh:

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "sqlplus / as sysdba @/etc/azure/post_script.sql" > /etc/azure/pre_script_$v_date.log
    ```

    Для /etc/azure/pre_script.sql измените содержимое hello hello файла в соответствии с требованиями вашей:

    ```bash
    alter tablespace SYSTEM begin backup;
    ...
    ...
    alter system switch logfile;
    alter system archive log stop;
    ```

    Для /etc/azure/post_script.sql измените содержимое hello hello файла в соответствии с требованиями вашей:

    ```bash
    alter tablespace SYSTEM end backup;
    ...
    ...
    alter system archive log start;
    ```

6. Измените разрешения файла:

    ```bash
    # chmod 600 /etc/azure/VMSnapshotScriptPluginConfig.json
    # chmod 700 /etc/azure/pre_script.sh
    # chmod 700 /etc/azure/post_script.sh
    ```

7. Тестировать сценарии hello.

    сценарии tootest hello, во-первых, войдите как корень. Затем убедитесь, что отсутствуют ошибки:

    ```bash
    # /etc/azure/pre_script.sh
    # /etc/azure/post_script.sh
    ```

Дополнительные сведения см. в записи блога [Announcing application consistent backup for Linux VMs using Azure Backup](https://azure.microsoft.com/en-us/blog/announcing-application-consistent-backup-for-linux-vms-using-azure-backup/) (Объявление согласованного с приложениями резервного копирования для виртуальных машин Linux).


### <a name="step-5-use-azure-recovery-services-vaults-tooback-up-hello-vm"></a>Шаг 5: Использование служб восстановления Azure хранилищ tooback копирование hello виртуальной Машины

1.  В hello портал Azure, поиск **хранилищ служб восстановления**.

    ![Страница хранилищ служб восстановления](./media/oracle-backup-recovery/recovery_service_01.png)

2.  На hello **хранилищ служб восстановления** колонке tooadd новое хранилище, нажмите кнопку **добавить**.

    ![Страница добавления хранилищ служб восстановления](./media/oracle-backup-recovery/recovery_service_02.png)

3.  toocontinue, нажмите кнопку **myVault**.

    ![Страница сведений о хранилищах служб восстановления](./media/oracle-backup-recovery/recovery_service_03.png)

4.  На hello **myVault** колонка, щелкните **резервного копирования**.

    ![Страница резервного копирования хранилищ служб восстановления](./media/oracle-backup-recovery/recovery_service_04.png)

5.  На hello **цель резервного копирования** колонке использовать значения по умолчанию hello объекта **Azure** и **виртуальной машины**. Нажмите кнопку **ОК**.

    ![Страница сведений о хранилищах служб восстановления](./media/oracle-backup-recovery/recovery_service_05.png)

6.  Для **политики резервного копирования** используйте параметр **DefaultPolicy** или выберите **Создание новой политики**. Нажмите кнопку **ОК**.

    ![Страница сведений о политике резервного копирования хранилищ служб восстановления](./media/oracle-backup-recovery/recovery_service_06.png)

7.  На hello **выберите виртуальные машины** колонки, выберите hello **myVM1** флажок и нажмите кнопку **ОК**. Нажмите кнопку hello **Enable backup** кнопки.

    ![Восстановление службы хранилищ элементов toohello резервного копирования сведений страницы](./media/oracle-backup-recovery/recovery_service_07.png)

    > [!IMPORTANT]
    > После нажатия кнопки **Enable backup**, процесс резервного копирования hello не начинается до hello запланированное время истечения срока действия. tooset копирование однократную архивацию, полный hello следующий шаг.

8.  На hello **myVault - резервное копирование элементов** колонки в разделе **резервного КОПИРОВАНИЯ число ЭЛЕМЕНТОВ**, выберите число hello резервного копирования элементов.

    ![Страница сведений о хранилище myVault в хранилищах служб восстановления](./media/oracle-backup-recovery/recovery_service_08.png)

9.  На hello **резервное копирование элементов (виртуальная машина Azure)** колонке hello правой части страницы приветствия нажмите кнопку с многоточием hello (**...** ), а затем нажмите **Архивировать сейчас**.

    ![Команда "Создать резервную копию" в хранилищах служб восстановления](./media/oracle-backup-recovery/recovery_service_09.png)

10. Нажмите кнопку hello **резервного копирования** кнопки. Дождитесь hello toofinish процесс резервного копирования. Перейдите слишком[шаг 6: удалите файлы базы данных hello](#step-6-remove-the-database-files).

    состояние hello tooview hello задание резервного копирования, нажмите кнопку **задания**.

    ![Страница задания в хранилищах служб восстановления](./media/oracle-backup-recovery/recovery_service_10.png)

    Hello состояние задания резервного копирования hello отображается в hello после изображения:

    ![Страница задания в хранилищах служб восстановления с отображением состояния](./media/oracle-backup-recovery/recovery_service_11.png)

11. Для резервного копирования согласованных на уровне приложения устраните все ошибки в файле журнала hello. Hello файл журнала находится в /var/log/azure/Microsoft.Azure.RecoveryServices.VMSnapshotLinux/1.0.9114.0.

### <a name="step-6-remove-hello-database-files"></a>Шаг 6: Удалите файлы базы данных hello 
Далее в этой статье вы узнаете, как tootest hello процесса восстановления. Перед запуском процесса восстановления hello имеются файлы базы данных tooremove hello.

1.  Удаление файлов hello табличное пространство и резервного копирования:

    ```bash
    $ sudo su - oracle
    $ cd /u01/app/oracle/oradata/cdb1
    $ rm -f *.dbf
    $ cd /u01/app/oracle/fast_recovery_area/CDB1/backupset
    $ rm -rf *
    ```
    
2.  (Необязательно) Завершение работы экземпляра Oracle hello.

    ```bash
    $ sqlplus / as sysdba
    SQL> shutdown abort
    ORACLE instance shut down.
    ```

## <a name="restore-hello-deleted-files-from-hello-recovery-services-vaults"></a>Восстановите файлы hello удален из приветствия хранилищ служб восстановления
toorestore hello удаленные файлы, полный hello, следующие шаги:

1. Hello портал Azure, для поиска hello *myVault* элемента хранилищ служб восстановления. На hello **Обзор** колонки в разделе **резервное копирование элементов**, выберите hello число элементов.

    ![Элементы архивации хранилища myVault в хранилищах служб восстановления](./media/oracle-backup-recovery/recovery_service_12.png)

2. В разделе **количество ЭЛЕМЕНТОВ для резервного КОПИРОВАНИЯ**, выберите hello число элементов.

    ![Число элементов архивации виртуальной машины Azure в хранилищах служб восстановления](./media/oracle-backup-recovery/recovery_service_13.png)

3. На hello **myvm1** колонка, щелкните **восстановления файлов (Предварительная версия)**.

    ![Снимок экрана: hello службы восстановления хранилищ файл восстановления страницы](./media/oracle-backup-recovery/recovery_service_14.png)

4. На hello **восстановления файлов (Предварительная версия)** области, нажмите кнопку **загрузить скрипт**. Сохраните hello (.sh) файл tooa папки загрузки на клиентском компьютере hello.

    ![Параметры сохранения файла скачивания сценария](./media/oracle-backup-recovery/recovery_service_15.png)

5. Скопируйте hello .sh файл toohello виртуальной Машины.

    Hello в следующем примере показано, как toouse toomove команда безопасного копирования (scp) hello toohello файл виртуальной Машины. Также можно скопировать hello содержимое toohello буфер обмена и затем вставить содержимое hello в новый файл, который настраивается на hello виртуальной Машины.

    > [!IMPORTANT]
    > В следующем примере hello убедитесь, что обновлены значения hello IP адрес и папки. Hello значений необходимо сопоставить toohello папку для сохранения файла hello.

    ```bash
    $ scp Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh <publicIpAddress>:/<folder>
    ```
6. Измените файл hello, чтобы он принадлежит корневой hello.

    В следующем примере hello измените файл hello, чтобы он принадлежит корневой hello. Затем измените разрешения.

    ```bash 
    $ ssh <publicIpAddress>
    $ sudo su -
    # chown root:root /<folder>/Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh
    # chmod 755 /<folder>/Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh
    # /<folder>/Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh
    ```
    Hello пример должна появиться после запуска hello предшествующий скрипта. При запросе toocontinue, введите **Y**.

    ```bash
    Microsoft Azure VM Backup - File Recovery
    ______________________________________________
    hello script requires 'open-iscsi' and 'lshw' toorun.
    Do you want us tooinstall 'open-iscsi' and 'lshw' on this machine?
    Please press 'Y' toocontinue with installation, 'N' tooabort hello operation. : Y
    Installing 'open-iscsi'....
    Installing 'lshw'....

    Connecting toorecovery point using ISCSI service...

    Connection succeeded!

    Please wait while we attach volumes of hello recovery point toothis machine...

    ************ Volumes of hello recovery point and their mount paths on this machine ************

    Sr.No.  |  Disk  |  Volume  |  MountPath

    1)  | /dev/sde  |  /dev/sde1  |  /root/myVM-20170517093913/Volume1

    2)  | /dev/sde  |  /dev/sde2  |  /root/myVM-20170517093913/Volume2

    ************ Open File Explorer toobrowse for files. ************

    After recovery, tooremove hello disks and close hello connection toohello recovery point, please click 'Unmount Disks' in step 3 of hello portal.

    Please enter 'q/Q' tooexit...
    ```

7. Подтверждено доступа toohello подключенных томов.

    tooexit, введите **q**и выполните поиск hello подключенных томов. добавлен список hello томов, в командной строке введите toocreate **df -k**.

    ![Команда -k df Hello](./media/oracle-backup-recovery/recovery_service_16.png)

8. Hello используйте следующий сценарий toocopy hello отсутствуют файлы задней toohello папки:

    ```bash
    # cd /root/myVM-2017XXXXXXX/Volume2/u01/app/oracle/fast_recovery_area/CDB1/backupset/2017_xx_xx
    # cp *.bkp /u01/app/oracle/fast_recovery_area/CDB1/backupset/2017_xx_xx
    # cd /u01/app/oracle/fast_recovery_area/CDB1/backupset/2017_xx_xx
    # chown oracle:oinstall *.bkp
    # cd /root/myVM-2017XXXXXXX/Volume2/u01/app/oracle/oradata/cdb1
    # cp *.dbf /u01/app/oracle/oradata/cdb1
    # cd /u01/app/oracle/oradata/cdb1
    # chown oracle:oinstall *.dbf
    ```
9. В hello следующий скрипт использование RMAN toorecover hello, базы данных:

    ```bash
    # sudo su - oracle
    $ rman target /
    RMAN> startup mount;
    RMAN> restore database;
    RMAN> recover database;
    RMAN> alter database open resetlogs;
    RMAN> SELECT * FROM scott.scott_table;
    ```
    
10. Отключите диск hello.

    В hello в hello портала Azure **восстановления файлов (Предварительная версия)** колонка, щелкните **отключить диски**.

    ![Команда отключения дисков](./media/oracle-backup-recovery/recovery_service_17.png)

## <a name="restore-hello-entire-vm"></a>Восстановление hello всю виртуальную Машину

Вместо восстановления hello удалить файлы из hello хранилищами служб восстановления, можно восстановить hello всю виртуальную Машину.

### <a name="step-1-delete-myvm"></a>Ша 1. Удаление myVM

*   В hello портал Azure, перейдите toohello **myVM1** в хранилище, а затем выберите **удалить**.

    ![Команда удаления хранилища](./media/oracle-backup-recovery/recover_vm_01.png)

### <a name="step-2-recover-hello-vm"></a>Шаг 2: Восстановление hello виртуальной Машины

1.  Go слишком**хранилищ служб восстановления**, а затем выберите **myVault**.

    ![Запись myVault](./media/oracle-backup-recovery/recover_vm_02.png)

2.  На hello **Обзор** колонки в разделе **резервное копирование элементов**, выберите hello число элементов.

    ![Элементы архивации myVault](./media/oracle-backup-recovery/recover_vm_03.png)

3.  На hello **резервное копирование элементов (виртуальная машина Azure)** колонке выберите **myvm1**.

    ![Страница восстановления виртуальной машины](./media/oracle-backup-recovery/recover_vm_04.png)

4.  На hello **myvm1** колонке нажмите кнопку с многоточием hello (**...** ), а затем нажмите **восстановления виртуальной Машины**.

    ![Команда восстановления виртуальной машины](./media/oracle-backup-recovery/recover_vm_05.png)

5.  На hello **выберите точку восстановления** колонки, выберите hello элемент, toorestore и нажмите кнопку **ОК**.

    ![Точка восстановления выберите hello](./media/oracle-backup-recovery/recover_vm_06.png)

    Если выбрано согласованное с приложениями резервное копирование, появится вертикальная синяя полоска.

6.  На hello **восстановление конфигурации** колонке выберите hello имя виртуальной машины, выберите группу ресурсов hello и нажмите кнопку **ОК**.

    ![Значения восстановления конфигурации](./media/oracle-backup-recovery/recover_vm_07.png)

7.  hello toorestore виртуальной Машины, нажмите кнопку hello **восстановить** кнопки.

8.  состояние hello tooview hello процесс восстановления, нажмите кнопку **заданий**, а затем нажмите кнопку **заданий резервного копирования**.

    ![Команда состояния заданий резервного копирования](./media/oracle-backup-recovery/recover_vm_08.png)

    Hello на этом рисунке показано состояние процесса восстановления hello hello:

    ![Состояние процесса восстановления hello](./media/oracle-backup-recovery/recover_vm_09.png)

### <a name="step-3-set-hello-public-ip-address"></a>Шаг 3: Настройка hello общедоступный IP-адрес
После hello восстановленной виртуальной Машины настройте hello общедоступный IP-адрес.

1.  Введите в поле поиска hello, **общедоступный IP-адрес**.

    ![Список общедоступных IP-адресов](./media/oracle-backup-recovery/create_ip_00.png)

2.  На hello **открытый IP-адреса** колонка, щелкните **добавить**. На hello **создать общедоступный IP-адрес** колонке для **имя**выберите hello открытый IP-имя. Для параметра **Группа ресурсов** выберите **Использовать существующий**. Затем щелкните **Создать**.

    ![Создание IP-адреса](./media/oracle-backup-recovery/create_ip_01.png)

3.  Найдите tooassociate hello общедоступный IP-адрес с сетевым интерфейсом hello для hello виртуальной Машины или выберите **myVMip**. Щелкните **Сопоставить**.

    ![Связывание IP-адреса](./media/oracle-backup-recovery/create_ip_02.png)

4.  Для **Тип ресурса** выберите **Сетевой интерфейс**. Выберите hello сетевого интерфейса, который используется экземпляром myVM hello и нажмите кнопку **ОК**.

    ![Выбор значений типа ресурса и сетевого интерфейса](./media/oracle-backup-recovery/create_ip_03.png)

5.  Найти и открыть экземпляр hello myVM, будет перенесена с портала hello. Hello IP-адрес, связанный с виртуальной Машины hello отображается на hello myVM **Обзор** колонку.

    ![Значение IP-адреса](./media/oracle-backup-recovery/create_ip_04.png)

### <a name="step-4-connect-toohello-vm"></a>Шаг 4: Подключение toohello виртуальной Машины

*   tooconnect toohello виртуальной Машины, используйте следующий сценарий hello:

    ```bash 
    ssh <publicIpAddress>
    ```

### <a name="step-5-test-whether-hello-database-is-accessible"></a>Шаг 5: Проверка hello база данных доступна
*   доступность tootest hello используйте следующий сценарий:

    ```bash 
    $ sudo su - oracle
    $ sqlplus / as sysdba
    SQL> startup
    ```

    > [!IMPORTANT]
    > Если hello в базу данных **запуска** команда приводит к возникновению ошибки, база данных toorecover hello см. в разделе [шаг 6: база данных hello toorecover использование RMAN](#step-6-optional-use-rman-to-recover-the-database).

### <a name="step-6-optional-use-rman-toorecover-hello-database"></a>Шаг 6. (Необязательно) используйте RMAN toorecover hello, базы данных
*   toorecover hello базы данных hello используйте следующий сценарий:

    ```bash
    # sudo su - oracle
    $ rman target /
    RMAN> startup mount;
    RMAN> restore database;
    RMAN> recover database;
    RMAN> alter database open resetlogs;
    RMAN> SELECT * FROM scott.scott_table;
    ```

Hello резервное копирование и восстановление hello базы данных Oracle 12c и базы данных на виртуальной Машине Linux Azure завершен.

## <a name="delete-hello-vm"></a>Удалить hello виртуальной Машины

При hello ВМ больше не нужна, можно использовать следующие команды tooremove hello группы ресурсов, hello виртуальной Машины и все связанные ресурсы hello:

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Дальнейшие действия

Изучите [руководство по созданию высокодоступных виртуальных машин](../../linux/create-cli-complete.md).

[Изучите примеры развертывания виртуальных машин с помощью интерфейса командной строки](../../linux/cli-samples.md).



