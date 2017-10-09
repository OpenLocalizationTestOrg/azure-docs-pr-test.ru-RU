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
# <a name="back-up-and-recover-an-oracle-database-12c-database-on-an-azure-linux-virtual-machine"></a><span data-ttu-id="a262b-103">Создание резервных копий и восстановление базы данных Oracle Database 12c на виртуальной машине Linux в Azure</span><span class="sxs-lookup"><span data-stu-id="a262b-103">Back up and recover an Oracle Database 12c database on an Azure Linux virtual machine</span></span>

<span data-ttu-id="a262b-104">Можно использовать toocreate Azure CLI и настраивать ресурсы Azure, в командной строке или с помощью скриптов.</span><span class="sxs-lookup"><span data-stu-id="a262b-104">You can use Azure CLI toocreate and manage Azure resources at a command prompt, or use scripts.</span></span> <span data-ttu-id="a262b-105">В этой статье мы используем toodeploy Azure CLI скриптов базы данных Oracle 12c базы данных из коллекции образов Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="a262b-105">In this article, we use Azure CLI scripts toodeploy an Oracle Database 12c database from an Azure Marketplace gallery image.</span></span>

<span data-ttu-id="a262b-106">Прежде чем начать, убедитесь, что установлен Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="a262b-106">Before you begin, make sure that Azure CLI is installed.</span></span> <span data-ttu-id="a262b-107">Дополнительные сведения см. в разделе hello [руководство по установке Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a262b-107">For more information, see hello [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="prepare-hello-environment"></a><span data-ttu-id="a262b-108">Подготовка среды hello</span><span class="sxs-lookup"><span data-stu-id="a262b-108">Prepare hello environment</span></span>

### <a name="step-1-prerequisites"></a><span data-ttu-id="a262b-109">Шаг 1. Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a262b-109">Step 1: Prerequisites</span></span>

*   <span data-ttu-id="a262b-110">tooperform hello резервного копирования и восстановления, необходимо сначала создать ВМ Linux, который имеет установленный экземпляр базы данных Oracle 12c.</span><span class="sxs-lookup"><span data-stu-id="a262b-110">tooperform hello backup and recovery process, you must first create a Linux VM that has an installed instance of Oracle Database 12c.</span></span> <span data-ttu-id="a262b-111">образа Marketplace Hello использовать ВМ называется hello toocreate *Oracle: Oracle-базы данных-Ee:12.1.0.2:latest*.</span><span class="sxs-lookup"><span data-stu-id="a262b-111">hello Marketplace image you use toocreate hello VM is named *Oracle:Oracle-Database-Ee:12.1.0.2:latest*.</span></span>

    <span data-ttu-id="a262b-112">toolearn toocreate базы данных Oracle, в статье hello [Oracle создать быстрый запуск базы данных](https://docs.microsoft.com/azure/virtual-machines/workloads/oracle/oracle-database-quick-create).</span><span class="sxs-lookup"><span data-stu-id="a262b-112">toolearn how toocreate an Oracle database, see hello [Oracle create database quickstart](https://docs.microsoft.com/azure/virtual-machines/workloads/oracle/oracle-database-quick-create).</span></span>


### <a name="step-2-connect-toohello-vm"></a><span data-ttu-id="a262b-113">Шаг 2: Подключение toohello виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="a262b-113">Step 2: Connect toohello VM</span></span>

*   <span data-ttu-id="a262b-114">toocreate Secure Shell (SSH) сеанс с hello виртуальной Машины, используйте следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="a262b-114">toocreate a Secure Shell (SSH) session with hello VM, use hello following command.</span></span> <span data-ttu-id="a262b-115">Замените hello hello IP-адреса и именем сайта hello `publicIpAddress` значение для виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="a262b-115">Replace hello IP address and hello host name combination with hello `publicIpAddress` value for your VM.</span></span>

    ```bash 
    ssh <publicIpAddress>
    ```

### <a name="step-3-prepare-hello-database"></a><span data-ttu-id="a262b-116">Шаг 3: Подготовка базы данных hello</span><span class="sxs-lookup"><span data-stu-id="a262b-116">Step 3: Prepare hello database</span></span>

1.  <span data-ttu-id="a262b-117">Чтобы перейти к выполнению этого шага, у вас должен быть экземпляр Oracle (cdb1), выполняющийся на виртуальной машине с именем *myVM*.</span><span class="sxs-lookup"><span data-stu-id="a262b-117">This step assumes that you have an Oracle instance (cdb1) that is running on a VM named *myVM*.</span></span>

    <span data-ttu-id="a262b-118">Запустите hello *oracle* корневой суперпользователя, а затем инициализировать прослушиватель hello:</span><span class="sxs-lookup"><span data-stu-id="a262b-118">Run hello *oracle* superuser root, and then initialize hello listener:</span></span>

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

2.  <span data-ttu-id="a262b-119">(Необязательно) Убедитесь, что hello база данных находится в режиме журнала архива:</span><span class="sxs-lookup"><span data-stu-id="a262b-119">(Optional) Make sure hello database is in archive log mode:</span></span>

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
3.  <span data-ttu-id="a262b-120">(Необязательно) Создайте фиксации hello tootest таблицы:</span><span class="sxs-lookup"><span data-stu-id="a262b-120">(Optional) Create a table tootest hello commit:</span></span>

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
4.  <span data-ttu-id="a262b-121">Проверить или изменить размер и расположение файла резервной копии hello:</span><span class="sxs-lookup"><span data-stu-id="a262b-121">Verify or change hello backup file location and size:</span></span>

    ```bash
    $ sqlplus / as sysdba
    SQL> show parameter db_recovery
    NAME                                 TYPE        VALUE
    ------------------------------------ ----------- ------------------------------
    db_recovery_file_dest                string      /u01/app/oracle/fast_recovery_area
    db_recovery_file_dest_size           big integer 4560M
    ```
5. <span data-ttu-id="a262b-122">Используйте диспетчер восстановления Oracle (RMAN) tooback hello базы данных:</span><span class="sxs-lookup"><span data-stu-id="a262b-122">Use Oracle Recovery Manager (RMAN) tooback up hello database:</span></span>

    ```bash
    $ rman target /
    RMAN> backup database plus archivelog;
    ```

### <a name="step-4-application-consistent-backup-for-linux-vms"></a><span data-ttu-id="a262b-123">Шаг 4. Согласованное с приложениями резервное копирование для виртуальных машин Linux</span><span class="sxs-lookup"><span data-stu-id="a262b-123">Step 4: Application-consistent backup for Linux VMs</span></span>

<span data-ttu-id="a262b-124">Согласованное с приложениями резервное копирование — это новая функция в службе Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="a262b-124">Application-consistent backups is a new feature in Azure Backup.</span></span> <span data-ttu-id="a262b-125">Можно создать и выбрать tooexecute скрипты до и после моментального снимка виртуальной Машины hello (перед созданием моментального снимка и после создания моментального снимка).</span><span class="sxs-lookup"><span data-stu-id="a262b-125">You can create and select scripts tooexecute before and after hello VM snapshot (pre-snapshot and post-snapshot).</span></span>

1. <span data-ttu-id="a262b-126">Загрузите файл JSON hello.</span><span class="sxs-lookup"><span data-stu-id="a262b-126">Download hello JSON file.</span></span>

    <span data-ttu-id="a262b-127">Скачайте файл VMSnapshotScriptPluginConfig.json со страницы https://github.com/MicrosoftAzureBackup/VMSnapshotPluginConfig.</span><span class="sxs-lookup"><span data-stu-id="a262b-127">Download VMSnapshotScriptPluginConfig.json from https://github.com/MicrosoftAzureBackup/VMSnapshotPluginConfig.</span></span> <span data-ttu-id="a262b-128">содержимое файла Hello выглядеть аналогично toohello следующее:</span><span class="sxs-lookup"><span data-stu-id="a262b-128">hello file contents look similar toohello following:</span></span>

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

2. <span data-ttu-id="a262b-129">Создайте папку /etc/azure hello на hello виртуальной Машины:</span><span class="sxs-lookup"><span data-stu-id="a262b-129">Create hello /etc/azure folder on hello VM:</span></span>

    ```bash
    $ sudo su -
    # mkdir /etc/azure
    # cd /etc/azure
    ```

3. <span data-ttu-id="a262b-130">Скопируйте файл JSON hello.</span><span class="sxs-lookup"><span data-stu-id="a262b-130">Copy hello JSON file.</span></span>

    <span data-ttu-id="a262b-131">Скопируйте папку /etc/azure toohello VMSnapshotScriptPluginConfig.json.</span><span class="sxs-lookup"><span data-stu-id="a262b-131">Copy VMSnapshotScriptPluginConfig.json toohello /etc/azure folder.</span></span>

4. <span data-ttu-id="a262b-132">Измените файл JSON hello.</span><span class="sxs-lookup"><span data-stu-id="a262b-132">Edit hello JSON file.</span></span>

    <span data-ttu-id="a262b-133">Изменение файла tooinclude hello VMSnapshotScriptPluginConfig.json hello `PreScriptLocation` и `PostScriptlocation` параметров.</span><span class="sxs-lookup"><span data-stu-id="a262b-133">Edit hello VMSnapshotScriptPluginConfig.json file tooinclude hello `PreScriptLocation` and `PostScriptlocation` parameters.</span></span> <span data-ttu-id="a262b-134">Например:</span><span class="sxs-lookup"><span data-stu-id="a262b-134">For example:</span></span>

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

5. <span data-ttu-id="a262b-135">Создайте hello файлы скриптов перед созданием моментального снимка и после моментального снимка.</span><span class="sxs-lookup"><span data-stu-id="a262b-135">Create hello pre-snapshot and post-snapshot script files.</span></span>

    <span data-ttu-id="a262b-136">Вот пример скриптов, выполняемых до и после создания моментальных снимков, для холодного резервного копирования (автономное резервное копирование с завершением работы и перезагрузкой):</span><span class="sxs-lookup"><span data-stu-id="a262b-136">Here's an example of pre-snapshot and post-snapshot scripts for a "cold backup" (an offline backup, with shutdown and restart):</span></span>

    <span data-ttu-id="a262b-137">Для /etc/azure/pre_script.sh:</span><span class="sxs-lookup"><span data-stu-id="a262b-137">For /etc/azure/pre_script.sh:</span></span>

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "$ORA_HOME/bin/dbshut $ORA_HOME" > /etc/azure/pre_script_$v_date.log
    ```

    <span data-ttu-id="a262b-138">Для /etc/azure/post_script.sh:</span><span class="sxs-lookup"><span data-stu-id="a262b-138">For /etc/azure/post_script.sh:</span></span>

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "$ORA_HOME/bin/dbstart $ORA_HOME" > /etc/azure/post_script_$v_date.log
    ```

    <span data-ttu-id="a262b-139">Вот пример скриптов, выполняемых до и после создания моментальных снимков, для горячего резервного копирования (оперативное резервное копирование):</span><span class="sxs-lookup"><span data-stu-id="a262b-139">Here's an example of pre-snapshot and post-snapshot scripts for a "hot backup" (an online backup):</span></span>

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "sqlplus / as sysdba @/etc/azure/pre_script.sql" > /etc/azure/pre_script_$v_date.log
    ```

    <span data-ttu-id="a262b-140">Для /etc/azure/post_script.sh:</span><span class="sxs-lookup"><span data-stu-id="a262b-140">For /etc/azure/post_script.sh:</span></span>

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "sqlplus / as sysdba @/etc/azure/post_script.sql" > /etc/azure/pre_script_$v_date.log
    ```

    <span data-ttu-id="a262b-141">Для /etc/azure/pre_script.sql измените содержимое hello hello файла в соответствии с требованиями вашей:</span><span class="sxs-lookup"><span data-stu-id="a262b-141">For /etc/azure/pre_script.sql, modify hello contents of hello file per your requirements:</span></span>

    ```bash
    alter tablespace SYSTEM begin backup;
    ...
    ...
    alter system switch logfile;
    alter system archive log stop;
    ```

    <span data-ttu-id="a262b-142">Для /etc/azure/post_script.sql измените содержимое hello hello файла в соответствии с требованиями вашей:</span><span class="sxs-lookup"><span data-stu-id="a262b-142">For /etc/azure/post_script.sql, modify hello contents of hello file per your requirements:</span></span>

    ```bash
    alter tablespace SYSTEM end backup;
    ...
    ...
    alter system archive log start;
    ```

6. <span data-ttu-id="a262b-143">Измените разрешения файла:</span><span class="sxs-lookup"><span data-stu-id="a262b-143">Change file permissions:</span></span>

    ```bash
    # chmod 600 /etc/azure/VMSnapshotScriptPluginConfig.json
    # chmod 700 /etc/azure/pre_script.sh
    # chmod 700 /etc/azure/post_script.sh
    ```

7. <span data-ttu-id="a262b-144">Тестировать сценарии hello.</span><span class="sxs-lookup"><span data-stu-id="a262b-144">Test hello scripts.</span></span>

    <span data-ttu-id="a262b-145">сценарии tootest hello, во-первых, войдите как корень.</span><span class="sxs-lookup"><span data-stu-id="a262b-145">tootest hello scripts, first, sign in as root.</span></span> <span data-ttu-id="a262b-146">Затем убедитесь, что отсутствуют ошибки:</span><span class="sxs-lookup"><span data-stu-id="a262b-146">Then, ensure that there are no errors:</span></span>

    ```bash
    # /etc/azure/pre_script.sh
    # /etc/azure/post_script.sh
    ```

<span data-ttu-id="a262b-147">Дополнительные сведения см. в записи блога [Announcing application consistent backup for Linux VMs using Azure Backup](https://azure.microsoft.com/en-us/blog/announcing-application-consistent-backup-for-linux-vms-using-azure-backup/) (Объявление согласованного с приложениями резервного копирования для виртуальных машин Linux).</span><span class="sxs-lookup"><span data-stu-id="a262b-147">For more information, see [Application-consistent backup for Linux VMs](https://azure.microsoft.com/en-us/blog/announcing-application-consistent-backup-for-linux-vms-using-azure-backup/).</span></span>


### <a name="step-5-use-azure-recovery-services-vaults-tooback-up-hello-vm"></a><span data-ttu-id="a262b-148">Шаг 5: Использование служб восстановления Azure хранилищ tooback копирование hello виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="a262b-148">Step 5: Use Azure Recovery Services vaults tooback up hello VM</span></span>

1.  <span data-ttu-id="a262b-149">В hello портал Azure, поиск **хранилищ служб восстановления**.</span><span class="sxs-lookup"><span data-stu-id="a262b-149">In hello Azure portal, search for **Recovery Services vaults**.</span></span>

    ![Страница хранилищ служб восстановления](./media/oracle-backup-recovery/recovery_service_01.png)

2.  <span data-ttu-id="a262b-151">На hello **хранилищ служб восстановления** колонке tooadd новое хранилище, нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="a262b-151">On hello **Recovery Services vaults** blade, tooadd a new vault, click **Add**.</span></span>

    ![Страница добавления хранилищ служб восстановления](./media/oracle-backup-recovery/recovery_service_02.png)

3.  <span data-ttu-id="a262b-153">toocontinue, нажмите кнопку **myVault**.</span><span class="sxs-lookup"><span data-stu-id="a262b-153">toocontinue, click **myVault**.</span></span>

    ![Страница сведений о хранилищах служб восстановления](./media/oracle-backup-recovery/recovery_service_03.png)

4.  <span data-ttu-id="a262b-155">На hello **myVault** колонка, щелкните **резервного копирования**.</span><span class="sxs-lookup"><span data-stu-id="a262b-155">On hello **myVault** blade, click **Backup**.</span></span>

    ![Страница резервного копирования хранилищ служб восстановления](./media/oracle-backup-recovery/recovery_service_04.png)

5.  <span data-ttu-id="a262b-157">На hello **цель резервного копирования** колонке использовать значения по умолчанию hello объекта **Azure** и **виртуальной машины**.</span><span class="sxs-lookup"><span data-stu-id="a262b-157">On hello **Backup Goal** blade, use hello default values of **Azure** and **Virtual machine**.</span></span> <span data-ttu-id="a262b-158">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="a262b-158">Click **OK**.</span></span>

    ![Страница сведений о хранилищах служб восстановления](./media/oracle-backup-recovery/recovery_service_05.png)

6.  <span data-ttu-id="a262b-160">Для **политики резервного копирования** используйте параметр **DefaultPolicy** или выберите **Создание новой политики**.</span><span class="sxs-lookup"><span data-stu-id="a262b-160">For **Backup policy**, use **DefaultPolicy**, or select **Create New policy**.</span></span> <span data-ttu-id="a262b-161">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="a262b-161">Click **OK**.</span></span>

    ![Страница сведений о политике резервного копирования хранилищ служб восстановления](./media/oracle-backup-recovery/recovery_service_06.png)

7.  <span data-ttu-id="a262b-163">На hello **выберите виртуальные машины** колонки, выберите hello **myVM1** флажок и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="a262b-163">On hello **Select virtual machines** blade, select hello **myVM1** check box, and then click **OK**.</span></span> <span data-ttu-id="a262b-164">Нажмите кнопку hello **Enable backup** кнопки.</span><span class="sxs-lookup"><span data-stu-id="a262b-164">Click hello **Enable backup** button.</span></span>

    ![Восстановление службы хранилищ элементов toohello резервного копирования сведений страницы](./media/oracle-backup-recovery/recovery_service_07.png)

    > [!IMPORTANT]
    > <span data-ttu-id="a262b-166">После нажатия кнопки **Enable backup**, процесс резервного копирования hello не начинается до hello запланированное время истечения срока действия.</span><span class="sxs-lookup"><span data-stu-id="a262b-166">After you click **Enable backup**, hello backup process doesn't start until hello scheduled time expires.</span></span> <span data-ttu-id="a262b-167">tooset копирование однократную архивацию, полный hello следующий шаг.</span><span class="sxs-lookup"><span data-stu-id="a262b-167">tooset up an immediate backup, complete hello next step.</span></span>

8.  <span data-ttu-id="a262b-168">На hello **myVault - резервное копирование элементов** колонки в разделе **резервного КОПИРОВАНИЯ число ЭЛЕМЕНТОВ**, выберите число hello резервного копирования элементов.</span><span class="sxs-lookup"><span data-stu-id="a262b-168">On hello **myVault - Backup items** blade, under **BACKUP ITEM COUNT**, select hello backup item count.</span></span>

    ![Страница сведений о хранилище myVault в хранилищах служб восстановления](./media/oracle-backup-recovery/recovery_service_08.png)

9.  <span data-ttu-id="a262b-170">На hello **резервное копирование элементов (виртуальная машина Azure)** колонке hello правой части страницы приветствия нажмите кнопку с многоточием hello (**...** ), а затем нажмите **Архивировать сейчас**.</span><span class="sxs-lookup"><span data-stu-id="a262b-170">On hello **Backup Items (Azure Virtual Machine)** blade, on hello right side of hello page, click hello ellipsis (**...**) button, and then click **Backup now**.</span></span>

    ![Команда "Создать резервную копию" в хранилищах служб восстановления](./media/oracle-backup-recovery/recovery_service_09.png)

10. <span data-ttu-id="a262b-172">Нажмите кнопку hello **резервного копирования** кнопки.</span><span class="sxs-lookup"><span data-stu-id="a262b-172">Click hello **Backup** button.</span></span> <span data-ttu-id="a262b-173">Дождитесь hello toofinish процесс резервного копирования.</span><span class="sxs-lookup"><span data-stu-id="a262b-173">Wait for hello backup process toofinish.</span></span> <span data-ttu-id="a262b-174">Перейдите слишком[шаг 6: удалите файлы базы данных hello](#step-6-remove-the-database-files).</span><span class="sxs-lookup"><span data-stu-id="a262b-174">Then, go too[Step 6: Remove hello database files](#step-6-remove-the-database-files).</span></span>

    <span data-ttu-id="a262b-175">состояние hello tooview hello задание резервного копирования, нажмите кнопку **задания**.</span><span class="sxs-lookup"><span data-stu-id="a262b-175">tooview hello status of hello backup job, click **Jobs**.</span></span>

    ![Страница задания в хранилищах служб восстановления](./media/oracle-backup-recovery/recovery_service_10.png)

    <span data-ttu-id="a262b-177">Hello состояние задания резервного копирования hello отображается в hello после изображения:</span><span class="sxs-lookup"><span data-stu-id="a262b-177">hello status of hello backup job appears in hello following image:</span></span>

    ![Страница задания в хранилищах служб восстановления с отображением состояния](./media/oracle-backup-recovery/recovery_service_11.png)

11. <span data-ttu-id="a262b-179">Для резервного копирования согласованных на уровне приложения устраните все ошибки в файле журнала hello.</span><span class="sxs-lookup"><span data-stu-id="a262b-179">For an application-consistent backup, address any errors in hello log file.</span></span> <span data-ttu-id="a262b-180">Hello файл журнала находится в /var/log/azure/Microsoft.Azure.RecoveryServices.VMSnapshotLinux/1.0.9114.0.</span><span class="sxs-lookup"><span data-stu-id="a262b-180">hello log file is located at /var/log/azure/Microsoft.Azure.RecoveryServices.VMSnapshotLinux/1.0.9114.0.</span></span>

### <a name="step-6-remove-hello-database-files"></a><span data-ttu-id="a262b-181">Шаг 6: Удалите файлы базы данных hello</span><span class="sxs-lookup"><span data-stu-id="a262b-181">Step 6: Remove hello database files</span></span> 
<span data-ttu-id="a262b-182">Далее в этой статье вы узнаете, как tootest hello процесса восстановления.</span><span class="sxs-lookup"><span data-stu-id="a262b-182">Later in this article, you'll learn how tootest hello recovery process.</span></span> <span data-ttu-id="a262b-183">Перед запуском процесса восстановления hello имеются файлы базы данных tooremove hello.</span><span class="sxs-lookup"><span data-stu-id="a262b-183">Before you can test hello recovery process, you have tooremove hello database files.</span></span>

1.  <span data-ttu-id="a262b-184">Удаление файлов hello табличное пространство и резервного копирования:</span><span class="sxs-lookup"><span data-stu-id="a262b-184">Remove hello tablespace and backup files:</span></span>

    ```bash
    $ sudo su - oracle
    $ cd /u01/app/oracle/oradata/cdb1
    $ rm -f *.dbf
    $ cd /u01/app/oracle/fast_recovery_area/CDB1/backupset
    $ rm -rf *
    ```
    
2.  <span data-ttu-id="a262b-185">(Необязательно) Завершение работы экземпляра Oracle hello.</span><span class="sxs-lookup"><span data-stu-id="a262b-185">(Optional) Shut down hello Oracle instance:</span></span>

    ```bash
    $ sqlplus / as sysdba
    SQL> shutdown abort
    ORACLE instance shut down.
    ```

## <a name="restore-hello-deleted-files-from-hello-recovery-services-vaults"></a><span data-ttu-id="a262b-186">Восстановите файлы hello удален из приветствия хранилищ служб восстановления</span><span class="sxs-lookup"><span data-stu-id="a262b-186">Restore hello deleted files from hello Recovery Services vaults</span></span>
<span data-ttu-id="a262b-187">toorestore hello удаленные файлы, полный hello, следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="a262b-187">toorestore hello deleted files, complete hello following steps:</span></span>

1. <span data-ttu-id="a262b-188">Hello портал Azure, для поиска hello *myVault* элемента хранилищ служб восстановления.</span><span class="sxs-lookup"><span data-stu-id="a262b-188">In hello Azure portal, search for hello *myVault* Recovery Services vaults item.</span></span> <span data-ttu-id="a262b-189">На hello **Обзор** колонки в разделе **резервное копирование элементов**, выберите hello число элементов.</span><span class="sxs-lookup"><span data-stu-id="a262b-189">On hello **Overview** blade, under **Backup items**, select hello number of items.</span></span>

    ![Элементы архивации хранилища myVault в хранилищах служб восстановления](./media/oracle-backup-recovery/recovery_service_12.png)

2. <span data-ttu-id="a262b-191">В разделе **количество ЭЛЕМЕНТОВ для резервного КОПИРОВАНИЯ**, выберите hello число элементов.</span><span class="sxs-lookup"><span data-stu-id="a262b-191">Under **BACKUP ITEM COUNT**, select hello number of items.</span></span>

    ![Число элементов архивации виртуальной машины Azure в хранилищах служб восстановления](./media/oracle-backup-recovery/recovery_service_13.png)

3. <span data-ttu-id="a262b-193">На hello **myvm1** колонка, щелкните **восстановления файлов (Предварительная версия)**.</span><span class="sxs-lookup"><span data-stu-id="a262b-193">On hello **myvm1** blade, click **File Recovery (Preview)**.</span></span>

    ![Снимок экрана: hello службы восстановления хранилищ файл восстановления страницы](./media/oracle-backup-recovery/recovery_service_14.png)

4. <span data-ttu-id="a262b-195">На hello **восстановления файлов (Предварительная версия)** области, нажмите кнопку **загрузить скрипт**.</span><span class="sxs-lookup"><span data-stu-id="a262b-195">On hello **File Recovery (Preview)** pane, click **Download Script**.</span></span> <span data-ttu-id="a262b-196">Сохраните hello (.sh) файл tooa папки загрузки на клиентском компьютере hello.</span><span class="sxs-lookup"><span data-stu-id="a262b-196">Then, save hello download (.sh) file tooa folder on hello client computer.</span></span>

    ![Параметры сохранения файла скачивания сценария](./media/oracle-backup-recovery/recovery_service_15.png)

5. <span data-ttu-id="a262b-198">Скопируйте hello .sh файл toohello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="a262b-198">Copy hello .sh file toohello VM.</span></span>

    <span data-ttu-id="a262b-199">Hello в следующем примере показано, как toouse toomove команда безопасного копирования (scp) hello toohello файл виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="a262b-199">hello following example shows how you toouse a secure copy (scp) command toomove hello file toohello VM.</span></span> <span data-ttu-id="a262b-200">Также можно скопировать hello содержимое toohello буфер обмена и затем вставить содержимое hello в новый файл, который настраивается на hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="a262b-200">You also can copy hello contents toohello clipboard, and then paste hello contents in a new file that is set up on hello VM.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="a262b-201">В следующем примере hello убедитесь, что обновлены значения hello IP адрес и папки.</span><span class="sxs-lookup"><span data-stu-id="a262b-201">In hello following example, ensure that you update hello IP address and folder values.</span></span> <span data-ttu-id="a262b-202">Hello значений необходимо сопоставить toohello папку для сохранения файла hello.</span><span class="sxs-lookup"><span data-stu-id="a262b-202">hello values must map toohello folder where hello file is saved.</span></span>

    ```bash
    $ scp Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh <publicIpAddress>:/<folder>
    ```
6. <span data-ttu-id="a262b-203">Измените файл hello, чтобы он принадлежит корневой hello.</span><span class="sxs-lookup"><span data-stu-id="a262b-203">Change hello file, so that it's owned by hello root.</span></span>

    <span data-ttu-id="a262b-204">В следующем примере hello измените файл hello, чтобы он принадлежит корневой hello.</span><span class="sxs-lookup"><span data-stu-id="a262b-204">In hello following example, change hello file so that it's owned by hello root.</span></span> <span data-ttu-id="a262b-205">Затем измените разрешения.</span><span class="sxs-lookup"><span data-stu-id="a262b-205">Then, change permissions.</span></span>

    ```bash 
    $ ssh <publicIpAddress>
    $ sudo su -
    # chown root:root /<folder>/Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh
    # chmod 755 /<folder>/Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh
    # /<folder>/Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh
    ```
    <span data-ttu-id="a262b-206">Hello пример должна появиться после запуска hello предшествующий скрипта.</span><span class="sxs-lookup"><span data-stu-id="a262b-206">hello following example shows what you should see after you run hello preceding script.</span></span> <span data-ttu-id="a262b-207">При запросе toocontinue, введите **Y**.</span><span class="sxs-lookup"><span data-stu-id="a262b-207">When you're prompted toocontinue, enter **Y**.</span></span>

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

7. <span data-ttu-id="a262b-208">Подтверждено доступа toohello подключенных томов.</span><span class="sxs-lookup"><span data-stu-id="a262b-208">Access toohello mounted volumes is confirmed.</span></span>

    <span data-ttu-id="a262b-209">tooexit, введите **q**и выполните поиск hello подключенных томов.</span><span class="sxs-lookup"><span data-stu-id="a262b-209">tooexit, enter **q**, and then search for hello mounted volumes.</span></span> <span data-ttu-id="a262b-210">добавлен список hello томов, в командной строке введите toocreate **df -k**.</span><span class="sxs-lookup"><span data-stu-id="a262b-210">toocreate a list of hello added volumes, at a command prompt, enter **df -k**.</span></span>

    ![Команда -k df Hello](./media/oracle-backup-recovery/recovery_service_16.png)

8. <span data-ttu-id="a262b-212">Hello используйте следующий сценарий toocopy hello отсутствуют файлы задней toohello папки:</span><span class="sxs-lookup"><span data-stu-id="a262b-212">Use hello following script toocopy hello missing files back toohello folders:</span></span>

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
9. <span data-ttu-id="a262b-213">В hello следующий скрипт использование RMAN toorecover hello, базы данных:</span><span class="sxs-lookup"><span data-stu-id="a262b-213">In hello following script, use RMAN toorecover hello database:</span></span>

    ```bash
    # sudo su - oracle
    $ rman target /
    RMAN> startup mount;
    RMAN> restore database;
    RMAN> recover database;
    RMAN> alter database open resetlogs;
    RMAN> SELECT * FROM scott.scott_table;
    ```
    
10. <span data-ttu-id="a262b-214">Отключите диск hello.</span><span class="sxs-lookup"><span data-stu-id="a262b-214">Unmount hello disk.</span></span>

    <span data-ttu-id="a262b-215">В hello в hello портала Azure **восстановления файлов (Предварительная версия)** колонка, щелкните **отключить диски**.</span><span class="sxs-lookup"><span data-stu-id="a262b-215">In hello Azure portal, on hello **File Recovery (Preview)** blade, click **Unmount Disks**.</span></span>

    ![Команда отключения дисков](./media/oracle-backup-recovery/recovery_service_17.png)

## <a name="restore-hello-entire-vm"></a><span data-ttu-id="a262b-217">Восстановление hello всю виртуальную Машину</span><span class="sxs-lookup"><span data-stu-id="a262b-217">Restore hello entire VM</span></span>

<span data-ttu-id="a262b-218">Вместо восстановления hello удалить файлы из hello хранилищами служб восстановления, можно восстановить hello всю виртуальную Машину.</span><span class="sxs-lookup"><span data-stu-id="a262b-218">Instead of restoring hello deleted files from hello Recovery Services vaults, you can restore hello entire VM.</span></span>

### <a name="step-1-delete-myvm"></a><span data-ttu-id="a262b-219">Ша 1. Удаление myVM</span><span class="sxs-lookup"><span data-stu-id="a262b-219">Step 1: Delete myVM</span></span>

*   <span data-ttu-id="a262b-220">В hello портал Azure, перейдите toohello **myVM1** в хранилище, а затем выберите **удалить**.</span><span class="sxs-lookup"><span data-stu-id="a262b-220">In hello Azure portal, go toohello **myVM1** vault, and then select **Delete**.</span></span>

    ![Команда удаления хранилища](./media/oracle-backup-recovery/recover_vm_01.png)

### <a name="step-2-recover-hello-vm"></a><span data-ttu-id="a262b-222">Шаг 2: Восстановление hello виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="a262b-222">Step 2: Recover hello VM</span></span>

1.  <span data-ttu-id="a262b-223">Go слишком**хранилищ служб восстановления**, а затем выберите **myVault**.</span><span class="sxs-lookup"><span data-stu-id="a262b-223">Go too**Recovery Services vaults**, and then select **myVault**.</span></span>

    ![Запись myVault](./media/oracle-backup-recovery/recover_vm_02.png)

2.  <span data-ttu-id="a262b-225">На hello **Обзор** колонки в разделе **резервное копирование элементов**, выберите hello число элементов.</span><span class="sxs-lookup"><span data-stu-id="a262b-225">On hello **Overview** blade, under **Backup items**, select hello number of items.</span></span>

    ![Элементы архивации myVault](./media/oracle-backup-recovery/recover_vm_03.png)

3.  <span data-ttu-id="a262b-227">На hello **резервное копирование элементов (виртуальная машина Azure)** колонке выберите **myvm1**.</span><span class="sxs-lookup"><span data-stu-id="a262b-227">On hello **Backup Items (Azure Virtual Machine)** blade, select **myvm1**.</span></span>

    ![Страница восстановления виртуальной машины](./media/oracle-backup-recovery/recover_vm_04.png)

4.  <span data-ttu-id="a262b-229">На hello **myvm1** колонке нажмите кнопку с многоточием hello (**...** ), а затем нажмите **восстановления виртуальной Машины**.</span><span class="sxs-lookup"><span data-stu-id="a262b-229">On hello **myvm1** blade, click hello ellipsis (**...**) button,  and then click **Restore VM**.</span></span>

    ![Команда восстановления виртуальной машины](./media/oracle-backup-recovery/recover_vm_05.png)

5.  <span data-ttu-id="a262b-231">На hello **выберите точку восстановления** колонки, выберите hello элемент, toorestore и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="a262b-231">On hello **Select restore point** blade, select hello item that you want toorestore, and then click **OK**.</span></span>

    ![Точка восстановления выберите hello](./media/oracle-backup-recovery/recover_vm_06.png)

    <span data-ttu-id="a262b-233">Если выбрано согласованное с приложениями резервное копирование, появится вертикальная синяя полоска.</span><span class="sxs-lookup"><span data-stu-id="a262b-233">If you have enabled application-consistent backup, a vertical blue bar appears.</span></span>

6.  <span data-ttu-id="a262b-234">На hello **восстановление конфигурации** колонке выберите hello имя виртуальной машины, выберите группу ресурсов hello и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="a262b-234">On hello **Restore configuration** blade, select hello virtual machine name, select hello resource group, and then click **OK**.</span></span>

    ![Значения восстановления конфигурации](./media/oracle-backup-recovery/recover_vm_07.png)

7.  <span data-ttu-id="a262b-236">hello toorestore виртуальной Машины, нажмите кнопку hello **восстановить** кнопки.</span><span class="sxs-lookup"><span data-stu-id="a262b-236">toorestore hello VM, click hello **Restore** button.</span></span>

8.  <span data-ttu-id="a262b-237">состояние hello tooview hello процесс восстановления, нажмите кнопку **заданий**, а затем нажмите кнопку **заданий резервного копирования**.</span><span class="sxs-lookup"><span data-stu-id="a262b-237">tooview hello status of hello restore process, click **Jobs**, and then click **Backup Jobs**.</span></span>

    ![Команда состояния заданий резервного копирования](./media/oracle-backup-recovery/recover_vm_08.png)

    <span data-ttu-id="a262b-239">Hello на этом рисунке показано состояние процесса восстановления hello hello:</span><span class="sxs-lookup"><span data-stu-id="a262b-239">hello following figure shows hello status of hello restore process:</span></span>

    ![Состояние процесса восстановления hello](./media/oracle-backup-recovery/recover_vm_09.png)

### <a name="step-3-set-hello-public-ip-address"></a><span data-ttu-id="a262b-241">Шаг 3: Настройка hello общедоступный IP-адрес</span><span class="sxs-lookup"><span data-stu-id="a262b-241">Step 3: Set hello public IP address</span></span>
<span data-ttu-id="a262b-242">После hello восстановленной виртуальной Машины настройте hello общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="a262b-242">After hello VM is restored, set up hello public IP address.</span></span>

1.  <span data-ttu-id="a262b-243">Введите в поле поиска hello, **общедоступный IP-адрес**.</span><span class="sxs-lookup"><span data-stu-id="a262b-243">In hello search box, enter **public IP address**.</span></span>

    ![Список общедоступных IP-адресов](./media/oracle-backup-recovery/create_ip_00.png)

2.  <span data-ttu-id="a262b-245">На hello **открытый IP-адреса** колонка, щелкните **добавить**.</span><span class="sxs-lookup"><span data-stu-id="a262b-245">On hello **Public IP addresses** blade, click **Add**.</span></span> <span data-ttu-id="a262b-246">На hello **создать общедоступный IP-адрес** колонке для **имя**выберите hello открытый IP-имя.</span><span class="sxs-lookup"><span data-stu-id="a262b-246">On hello **Create public IP address** blade, for **Name**, select hello public IP name.</span></span> <span data-ttu-id="a262b-247">Для параметра **Группа ресурсов** выберите **Использовать существующий**.</span><span class="sxs-lookup"><span data-stu-id="a262b-247">For **Resource group**, select **Use existing**.</span></span> <span data-ttu-id="a262b-248">Затем щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="a262b-248">Then, click **Create**.</span></span>

    ![Создание IP-адреса](./media/oracle-backup-recovery/create_ip_01.png)

3.  <span data-ttu-id="a262b-250">Найдите tooassociate hello общедоступный IP-адрес с сетевым интерфейсом hello для hello виртуальной Машины или выберите **myVMip**.</span><span class="sxs-lookup"><span data-stu-id="a262b-250">tooassociate hello public IP address with hello network interface for hello VM, search for and select **myVMip**.</span></span> <span data-ttu-id="a262b-251">Щелкните **Сопоставить**.</span><span class="sxs-lookup"><span data-stu-id="a262b-251">Then, click **Associate**.</span></span>

    ![Связывание IP-адреса](./media/oracle-backup-recovery/create_ip_02.png)

4.  <span data-ttu-id="a262b-253">Для **Тип ресурса** выберите **Сетевой интерфейс**.</span><span class="sxs-lookup"><span data-stu-id="a262b-253">For **Resource type**, select **Network interface**.</span></span> <span data-ttu-id="a262b-254">Выберите hello сетевого интерфейса, который используется экземпляром myVM hello и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="a262b-254">Select hello network interface that is used by hello myVM instance, and then click **OK**.</span></span>

    ![Выбор значений типа ресурса и сетевого интерфейса](./media/oracle-backup-recovery/create_ip_03.png)

5.  <span data-ttu-id="a262b-256">Найти и открыть экземпляр hello myVM, будет перенесена с портала hello.</span><span class="sxs-lookup"><span data-stu-id="a262b-256">Search for and open hello instance of myVM that is ported from hello portal.</span></span> <span data-ttu-id="a262b-257">Hello IP-адрес, связанный с виртуальной Машины hello отображается на hello myVM **Обзор** колонку.</span><span class="sxs-lookup"><span data-stu-id="a262b-257">hello IP address that is associated with hello VM appears on hello myVM **Overview** blade.</span></span>

    ![Значение IP-адреса](./media/oracle-backup-recovery/create_ip_04.png)

### <a name="step-4-connect-toohello-vm"></a><span data-ttu-id="a262b-259">Шаг 4: Подключение toohello виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="a262b-259">Step 4: Connect toohello VM</span></span>

*   <span data-ttu-id="a262b-260">tooconnect toohello виртуальной Машины, используйте следующий сценарий hello:</span><span class="sxs-lookup"><span data-stu-id="a262b-260">tooconnect toohello VM, use hello following script:</span></span>

    ```bash 
    ssh <publicIpAddress>
    ```

### <a name="step-5-test-whether-hello-database-is-accessible"></a><span data-ttu-id="a262b-261">Шаг 5: Проверка hello база данных доступна</span><span class="sxs-lookup"><span data-stu-id="a262b-261">Step 5: Test whether hello database is accessible</span></span>
*   <span data-ttu-id="a262b-262">доступность tootest hello используйте следующий сценарий:</span><span class="sxs-lookup"><span data-stu-id="a262b-262">tootest accessibility, use hello following script:</span></span>

    ```bash 
    $ sudo su - oracle
    $ sqlplus / as sysdba
    SQL> startup
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="a262b-263">Если hello в базу данных **запуска** команда приводит к возникновению ошибки, база данных toorecover hello см. в разделе [шаг 6: база данных hello toorecover использование RMAN](#step-6-optional-use-rman-to-recover-the-database).</span><span class="sxs-lookup"><span data-stu-id="a262b-263">If hello database **startup** command generates an error, toorecover hello database, see [Step 6: Use RMAN toorecover hello database](#step-6-optional-use-rman-to-recover-the-database).</span></span>

### <a name="step-6-optional-use-rman-toorecover-hello-database"></a><span data-ttu-id="a262b-264">Шаг 6. (Необязательно) используйте RMAN toorecover hello, базы данных</span><span class="sxs-lookup"><span data-stu-id="a262b-264">Step 6: (Optional) Use RMAN toorecover hello database</span></span>
*   <span data-ttu-id="a262b-265">toorecover hello базы данных hello используйте следующий сценарий:</span><span class="sxs-lookup"><span data-stu-id="a262b-265">toorecover hello database, use hello following script:</span></span>

    ```bash
    # sudo su - oracle
    $ rman target /
    RMAN> startup mount;
    RMAN> restore database;
    RMAN> recover database;
    RMAN> alter database open resetlogs;
    RMAN> SELECT * FROM scott.scott_table;
    ```

<span data-ttu-id="a262b-266">Hello резервное копирование и восстановление hello базы данных Oracle 12c и базы данных на виртуальной Машине Linux Azure завершен.</span><span class="sxs-lookup"><span data-stu-id="a262b-266">hello backup and recovery of hello Oracle Database 12c database on an Azure Linux VM is now finished.</span></span>

## <a name="delete-hello-vm"></a><span data-ttu-id="a262b-267">Удалить hello виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="a262b-267">Delete hello VM</span></span>

<span data-ttu-id="a262b-268">При hello ВМ больше не нужна, можно использовать следующие команды tooremove hello группы ресурсов, hello виртуальной Машины и все связанные ресурсы hello:</span><span class="sxs-lookup"><span data-stu-id="a262b-268">When you no longer need hello VM, you can use hello following command tooremove hello resource group, hello VM, and all related resources:</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="a262b-269">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a262b-269">Next steps</span></span>

<span data-ttu-id="a262b-270">Изучите [руководство по созданию высокодоступных виртуальных машин](../../linux/create-cli-complete.md).</span><span class="sxs-lookup"><span data-stu-id="a262b-270">[Tutorial: Create highly available VMs](../../linux/create-cli-complete.md)</span></span>

<span data-ttu-id="a262b-271">[Изучите примеры развертывания виртуальных машин с помощью интерфейса командной строки](../../linux/cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="a262b-271">[Explore VM deployment Azure CLI samples](../../linux/cli-samples.md)</span></span>



