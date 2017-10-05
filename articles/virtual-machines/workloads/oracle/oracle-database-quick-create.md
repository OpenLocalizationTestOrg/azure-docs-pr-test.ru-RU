---
title: "Создание базы данных Oracle на виртуальной машине Azure | Документация Майкрософт"
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
ms.openlocfilehash: 8683b016c4db2c66fb1dd994405b70c3d137a7fc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-oracle-database-in-an-azure-vm"></a><span data-ttu-id="7e502-103">Создание базы данных Oracle на виртуальной машине Azure</span><span class="sxs-lookup"><span data-stu-id="7e502-103">Create an Oracle Database in an Azure VM</span></span>

<span data-ttu-id="7e502-104">В этом руководстве объясняется, как с помощью Azure CLI развернуть виртуальную машину Azure, используя [образ из коллекции Oracle Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Oracle.OracleDatabase12102EnterpriseEdition?tab=Overview), чтобы создать базу данных Oracle 12c.</span><span class="sxs-lookup"><span data-stu-id="7e502-104">This guide details using the Azure CLI to deploy an Azure virtual machine from the [Oracle marketplace gallery image](https://azuremarketplace.microsoft.com/marketplace/apps/Oracle.OracleDatabase12102EnterpriseEdition?tab=Overview) in order to create an Oracle 12c database.</span></span> <span data-ttu-id="7e502-105">После развертывания сервера вы подключитесь к нему по протоколу SSH для настройки базы данных Oracle.</span><span class="sxs-lookup"><span data-stu-id="7e502-105">Once the server is deployed, you will connect via SSH in order to configure the Oracle database.</span></span> 

<span data-ttu-id="7e502-106">Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) , прежде чем начинать работу.</span><span class="sxs-lookup"><span data-stu-id="7e502-106">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="7e502-107">Если вы решили установить и использовать CLI локально, для выполнения инструкций в этом руководстве вам понадобится Azure CLI 2.0.4 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="7e502-107">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="7e502-108">Чтобы узнать версию, выполните команду `az --version`.</span><span class="sxs-lookup"><span data-stu-id="7e502-108">Run `az --version` to find the version.</span></span> <span data-ttu-id="7e502-109">Если вам необходимо выполнить установку или обновление, см. статью [Установка Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="7e502-109">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="7e502-110">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="7e502-110">Create a resource group</span></span>

<span data-ttu-id="7e502-111">Создайте группу ресурсов с помощью команды [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="7e502-111">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="7e502-112">Группа ресурсов Azure является логическим контейнером, в котором происходит развертывание ресурсов Azure и управление ими.</span><span class="sxs-lookup"><span data-stu-id="7e502-112">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="7e502-113">В следующем примере создается группа ресурсов с именем *myResourceGroup* в расположении *eastus*.</span><span class="sxs-lookup"><span data-stu-id="7e502-113">The following example creates a resource group named *myResourceGroup* in the *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```
## <a name="create-virtual-machine"></a><span data-ttu-id="7e502-114">Создание виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="7e502-114">Create virtual machine</span></span>

<span data-ttu-id="7e502-115">Чтобы создать виртуальную машину, выполните команду [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="7e502-115">To create a virtual machine (VM), use the [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="7e502-116">В следующем примере создается виртуальная машина `myVM`.</span><span class="sxs-lookup"><span data-stu-id="7e502-116">The following example creates a VM named `myVM`.</span></span> <span data-ttu-id="7e502-117">Также создаются ключи SSH, если они не существуют в расположении ключей по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="7e502-117">It also creates SSH keys, if they do not already exist in a default key location.</span></span> <span data-ttu-id="7e502-118">Чтобы использовать определенный набор ключей, используйте параметр `--ssh-key-value`.</span><span class="sxs-lookup"><span data-stu-id="7e502-118">To use a specific set of keys, use the `--ssh-key-value` option.</span></span>  

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
    --size Standard_DS2_v2 \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="7e502-119">После создания виртуальной машины в Azure CLI отображается информация следующего вида.</span><span class="sxs-lookup"><span data-stu-id="7e502-119">After you create the VM, Azure CLI displays information similar to the following example.</span></span> <span data-ttu-id="7e502-120">Обратите внимание на значение `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="7e502-120">Note the value for `publicIpAddress`.</span></span> <span data-ttu-id="7e502-121">Этот адрес используется для доступа к виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="7e502-121">You use this address to access the VM.</span></span>

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

## <a name="connect-to-the-vm"></a><span data-ttu-id="7e502-122">Подключение к виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="7e502-122">Connect to the VM</span></span>

<span data-ttu-id="7e502-123">Используйте следующую команду для создания сеанса SSH с виртуальной машиной.</span><span class="sxs-lookup"><span data-stu-id="7e502-123">To create an SSH session with the VM, use the following command.</span></span> <span data-ttu-id="7e502-124">Замените IP-адрес общедоступным IP-адресом виртуальной машины (значение `publicIpAddress`).</span><span class="sxs-lookup"><span data-stu-id="7e502-124">Replace the IP address with the `publicIpAddress` value for your VM.</span></span>

```bash 
ssh <publicIpAddress>
```

## <a name="create-the-database"></a><span data-ttu-id="7e502-125">Создание базы данных</span><span class="sxs-lookup"><span data-stu-id="7e502-125">Create the database</span></span>

<span data-ttu-id="7e502-126">Программное обеспечение Oracle уже установлено в образе Marketplace.</span><span class="sxs-lookup"><span data-stu-id="7e502-126">The Oracle software is already installed on the Marketplace image.</span></span> <span data-ttu-id="7e502-127">Создайте пример базы данных, как описано ниже.</span><span class="sxs-lookup"><span data-stu-id="7e502-127">Create a sample database as follows.</span></span> 

1.  <span data-ttu-id="7e502-128">Переключитесь на учетную запись суперпользователя *oracle* и инициализируйте прослушиватель для ведения журнала.</span><span class="sxs-lookup"><span data-stu-id="7e502-128">Switch to the *oracle* superuser, then initialize the listener for logging:</span></span>

    ```bash
    $ sudo su - oracle
    $ lsnrctl start
    ```

    <span data-ttu-id="7e502-129">Выход аналогичен приведенному ниже:</span><span class="sxs-lookup"><span data-stu-id="7e502-129">The output is similar to the following:</span></span>

    ```bash
    Copyright (c) 1991, 2014, Oracle.  All rights reserved.

    Starting /u01/app/oracle/product/12.1.0/dbhome_1/bin/tnslsnr: please wait...

    TNSLSNR for Linux: Version 12.1.0.2.0 - Production
    Log messages written to /u01/app/oracle/diag/tnslsnr/myVM/listener/alert/log.xml
    Listening on: (DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=myVM.twltkue3xvsujaz1bvlrhfuiwf.dx.internal.cloudapp.net)(PORT=1521)))

    Connecting to (ADDRESS=(PROTOCOL=tcp)(HOST=)(PORT=1521))
    STATUS of the LISTENER
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
    The listener supports no services
    The command completed successfully
    ```

2.  <span data-ttu-id="7e502-130">Создание базы данных</span><span class="sxs-lookup"><span data-stu-id="7e502-130">Create the database:</span></span>

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

    <span data-ttu-id="7e502-131">Создание базы данных занимает несколько минут.</span><span class="sxs-lookup"><span data-stu-id="7e502-131">It takes a few minutes to create the database.</span></span>

3. <span data-ttu-id="7e502-132">Задайте переменные Oracle.</span><span class="sxs-lookup"><span data-stu-id="7e502-132">Set Oracle variables</span></span>

<span data-ttu-id="7e502-133">Прежде чем подключиться, необходимо задать две переменные среды: *ORACLE_HOME* и *ORACLE_SID*.</span><span class="sxs-lookup"><span data-stu-id="7e502-133">Before you connect, you need to set two environment variables: *ORACLE_HOME* and *ORACLE_SID*.</span></span>

```bash
ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
ORACLE_SID=cdb1; export ORACLE_SID
```
<span data-ttu-id="7e502-134">При необходимости можно добавить переменные ORACLE_HOME и ORACLE_SID в BASHRC-файл.</span><span class="sxs-lookup"><span data-stu-id="7e502-134">You also can add ORACLE_HOME and ORACLE_SID variables to the .bashrc file.</span></span> <span data-ttu-id="7e502-135">Это позволит сохранить переменные среды для следующих входов в систему.</span><span class="sxs-lookup"><span data-stu-id="7e502-135">This would save the environment variables for future sign-ins.</span></span> <span data-ttu-id="7e502-136">Добавьте следующие инструкции в файл `~/.bashrc` с помощью любого редактора.</span><span class="sxs-lookup"><span data-stu-id="7e502-136">Confirm the following statements have been added to the `~/.bashrc` file using editor of your choice.</span></span>

```bash
# Add ORACLE_HOME. 
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1 
# Add ORACLE_SID. 
export ORACLE_SID=cdb1 
```

## <a name="oracle-em-express-connectivity"></a><span data-ttu-id="7e502-137">Подключение к Oracle EM Express</span><span class="sxs-lookup"><span data-stu-id="7e502-137">Oracle EM Express connectivity</span></span>

<span data-ttu-id="7e502-138">Мы включим в Oracle EM Express инструмент управления графическим интерфейсом пользователя, чтобы была возможность просматривать базу данных.</span><span class="sxs-lookup"><span data-stu-id="7e502-138">For a GUI management tool that you can use to explore the database, set up Oracle EM Express.</span></span> <span data-ttu-id="7e502-139">Для подключения к Oracle EM Express сначала необходимо настроить порт в Oracle.</span><span class="sxs-lookup"><span data-stu-id="7e502-139">To connect to Oracle EM Express, you must first set up the port in Oracle.</span></span> 

1. <span data-ttu-id="7e502-140">Подключитесь к базе данных с помощью SQL Plus.</span><span class="sxs-lookup"><span data-stu-id="7e502-140">Connect to your database using sqlplus:</span></span>

    ```bash
    sqlplus / as sysdba
    ```

2. <span data-ttu-id="7e502-141">После подключения задайте порт 5502 для EM Express.</span><span class="sxs-lookup"><span data-stu-id="7e502-141">Once connected, set the port 5502 for EM Express</span></span>

    ```bash
    exec DBMS_XDB_CONFIG.SETHTTPSPORT(5502);
    ```

3. <span data-ttu-id="7e502-142">Откройте контейнер PDB1, если вы еще не сделали этого, но сначала проверьте его состояние.</span><span class="sxs-lookup"><span data-stu-id="7e502-142">Open the container PDB1 if not already opened, but first check the status:</span></span>

    ```bash
    select con_id, name, open_mode from v$pdbs;
    ```

    <span data-ttu-id="7e502-143">Выход аналогичен приведенному ниже:</span><span class="sxs-lookup"><span data-stu-id="7e502-143">The output is similar to the following:</span></span>

    ```bash
      CON_ID NAME                           OPEN_MODE 
      ----------- ------------------------- ---------- 
      2           PDB$SEED                  READ ONLY 
      3           PDB1                      MOUNT
    ```

4. <span data-ttu-id="7e502-144">Если значение переменной OPEN_MODE для `PDB1` отличается от READ WRITE, выполните следующие команды, чтобы открыть PDB1.</span><span class="sxs-lookup"><span data-stu-id="7e502-144">If the OPEN_MODE for `PDB1` is not READ WRITE, then run the followings commands to open PDB1:</span></span>

   ```bash
    alter session set container=pdb1;
    alter database open;
   ```

<span data-ttu-id="7e502-145">Теперь введите команду `quit` для завершения сеанса sqlplus, а затем `exit` для завершения сеанса пользователя oracle.</span><span class="sxs-lookup"><span data-stu-id="7e502-145">You need to type `quit` to end the sqlplus session and type `exit` to logout of the oracle user.</span></span>

## <a name="automate-database-startup-and-shutdown"></a><span data-ttu-id="7e502-146">Автоматизация запуска и завершения работы базы данных</span><span class="sxs-lookup"><span data-stu-id="7e502-146">Automate database startup and shutdown</span></span>

<span data-ttu-id="7e502-147">По умолчанию база данных Oracle не запускается автоматически при перезапуске виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="7e502-147">The Oracle database by default doesn't automatically start when you restart the VM.</span></span> <span data-ttu-id="7e502-148">Чтобы база данных Oracle запускалась автоматически, войдите с правами привилегированного пользователя.</span><span class="sxs-lookup"><span data-stu-id="7e502-148">To set up the Oracle database to start automatically, first sign in as root.</span></span> <span data-ttu-id="7e502-149">Затем создайте и обновите некоторые системные файлы.</span><span class="sxs-lookup"><span data-stu-id="7e502-149">Then, create and update some system files.</span></span>

1. <span data-ttu-id="7e502-150">Войдите с правами привилегированного пользователя.</span><span class="sxs-lookup"><span data-stu-id="7e502-150">Sign on as root</span></span>
    ```bash
    sudo su -
    ```

2.  <span data-ttu-id="7e502-151">В любом удобном редакторе откройте файл `/etc/oratab` и замените значение по умолчанию `N` на `Y`:</span><span class="sxs-lookup"><span data-stu-id="7e502-151">Using your favorite editor, edit the file `/etc/oratab` and change the default `N` to `Y`:</span></span>

    ```bash
    cdb1:/u01/app/oracle/product/12.1.0/dbhome_1:Y
    ```

3.  <span data-ttu-id="7e502-152">Создайте файл с именем `/etc/init.d/dbora` и вставьте в него следующее содержимое:</span><span class="sxs-lookup"><span data-stu-id="7e502-152">Create a file named `/etc/init.d/dbora` and paste the following contents:</span></span>

    ```
    #!/bin/sh
    # chkconfig: 345 99 10
    # Description: Oracle auto start-stop script.
    #
    # Set ORA_HOME to be equivalent to $ORACLE_HOME.
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle

    case "$1" in
    'start')
        # Start the Oracle databases:
        # The following command assumes that the Oracle sign-in
        # will not prompt the user for any values.
        # Remove "&" if you don't want startup as a background process.
        su - $ORA_OWNER -c "$ORA_HOME/bin/dbstart $ORA_HOME" &
        touch /var/lock/subsys/dbora
        ;;

    'stop')
        # Stop the Oracle databases:
        # The following command assumes that the Oracle sign-in
        # will not prompt the user for any values.
        su - $ORA_OWNER -c "$ORA_HOME/bin/dbshut $ORA_HOME" &
        rm -f /var/lock/subsys/dbora
        ;;
    esac
    ```

4.  <span data-ttu-id="7e502-153">Измените разрешения для файлов с помощью команды *chmod*:</span><span class="sxs-lookup"><span data-stu-id="7e502-153">Change permissions on files with *chmod* as follows:</span></span>

    ```bash
    chgrp dba /etc/init.d/dbora
    chmod 750 /etc/init.d/dbora
    ```

5.  <span data-ttu-id="7e502-154">Создайте символьные ссылки для запуска и завершения работы:</span><span class="sxs-lookup"><span data-stu-id="7e502-154">Create symbolic links for startup and shutdown as follows:</span></span>

    ```bash
    ln -s /etc/init.d/dbora /etc/rc.d/rc0.d/K01dbora
    ln -s /etc/init.d/dbora /etc/rc.d/rc3.d/S99dbora
    ln -s /etc/init.d/dbora /etc/rc.d/rc5.d/S99dbora
    ```

6.  <span data-ttu-id="7e502-155">Чтобы проверить изменения, перезапустите виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="7e502-155">To test your changes, restart the VM:</span></span>

    ```bash
    reboot
    ```

## <a name="open-ports-for-connectivity"></a><span data-ttu-id="7e502-156">Открытие портов для подключения</span><span class="sxs-lookup"><span data-stu-id="7e502-156">Open ports for connectivity</span></span>

<span data-ttu-id="7e502-157">Последнее, что следует сделать, — настроить несколько внешних конечных точек.</span><span class="sxs-lookup"><span data-stu-id="7e502-157">The final task is to configure some external endpoints.</span></span> <span data-ttu-id="7e502-158">Чтобы настроить группу безопасности сети Azure, которая защищает виртуальную машину, сначала следует завершить сеанс SSH на виртуальной машине. (Завершение сеанса SSH должно был произойти при перезапуске на предыдущем шаге.)</span><span class="sxs-lookup"><span data-stu-id="7e502-158">To set up the Azure Network Security Group that protects the VM, first exit your SSH session in the VM (should have been kicked out of SSH when rebooting in previous step).</span></span> 

1.  <span data-ttu-id="7e502-159">Чтобы открыть конечную точку для удаленного доступа к базе данных Oracle, создайте правило группы безопасности сети с помощью команды [az network nsg rule create](/cli/azure/network/nsg/rule#create):</span><span class="sxs-lookup"><span data-stu-id="7e502-159">To open the endpoint that you use to access the Oracle database remotely, create a Network Security Group rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create) as follows:</span></span> 

    ```azurecli-interactive
    az network nsg rule create \
        --resource-group myResourceGroup\
        --nsg-name myVmNSG \
        --name allow-oracle \
        --protocol tcp \
        --priority 1001 \
        --destination-port-range 1521
    ```

2.  <span data-ttu-id="7e502-160">Чтобы открыть конечную точку для удаленного доступа к Oracle EM Express, создайте правило группы безопасности сети с помощью команды [az network nsg rule create](/cli/azure/network/nsg/rule#create):</span><span class="sxs-lookup"><span data-stu-id="7e502-160">To open the endpoint that you use to access Oracle EM Express remotely, create a Network Security Group rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create) as follows:</span></span>

    ```azurecli-interactive
    az network nsg rule create \
        --resource-group myResourceGroup \
        --nsg-name myVmNSG \
        --name allow-oracle-EM \
        --protocol tcp \
        --priority 1002 \
        --destination-port-range 5502
    ```

3. <span data-ttu-id="7e502-161">При необходимости получите общедоступный IP-адрес виртуальной машины еще раз с помощью команды [az network public-ip show](/cli/azure/network/public-ip#show):</span><span class="sxs-lookup"><span data-stu-id="7e502-161">If needed, obtain the public IP address of your VM again with [az network public-ip show](/cli/azure/network/public-ip#show) as follows:</span></span>

    ```azurecli-interactive
    az network public-ip show \
        --resource-group myResourceGroup \
        --name myVMPublicIP \
        --query [ipAddress] \
        --output tsv
    ```

4.  <span data-ttu-id="7e502-162">Подключите EM Express с помощью браузера.</span><span class="sxs-lookup"><span data-stu-id="7e502-162">Connect EM Express from your browser.</span></span> <span data-ttu-id="7e502-163">Убедитесь, что браузер совместим с EM Express (также необходимо установить Flash).</span><span class="sxs-lookup"><span data-stu-id="7e502-163">Make sure your browser is compatible with EM Express (Flash install is required):</span></span> 

    ```
    https://<VM ip address or hostname>:5502/em
    ```

<span data-ttu-id="7e502-164">Вы можете войти с помощью учетной записи **SYS** и установить флажок **as sysdba**.</span><span class="sxs-lookup"><span data-stu-id="7e502-164">You can log in by using the **SYS** account, and check the **as sysdba** checkbox.</span></span> <span data-ttu-id="7e502-165">Используйте пароль **OraPasswd1**, заданный во время установки.</span><span class="sxs-lookup"><span data-stu-id="7e502-165">Use the password **OraPasswd1** that you set during installation.</span></span> 

![Снимок экрана со страницей входа Oracle OEM Express](./media/oracle-quick-start/oracle_oem_express_login.png)

## <a name="clean-up-resources"></a><span data-ttu-id="7e502-167">Очистка ресурсов</span><span class="sxs-lookup"><span data-stu-id="7e502-167">Clean up resources</span></span>

<span data-ttu-id="7e502-168">Когда вы завершите изучение первой базы данных Oracle в Azure, вы можете удалить ненужную виртуальную машину, группу ресурсов и все связанные с ней ресурсы с помощью команды [az group delete](/cli/azure/group#delete).</span><span class="sxs-lookup"><span data-stu-id="7e502-168">Once you have finished exploring your first Oracle database on Azure and the VM is no longer needed, you can use the [az group delete](/cli/azure/group#delete) command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="7e502-169">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7e502-169">Next steps</span></span>

<span data-ttu-id="7e502-170">Узнайте о других [решениях Oracle в Azure](oracle-considerations.md).</span><span class="sxs-lookup"><span data-stu-id="7e502-170">Learn about other [Oracle solutions on Azure](oracle-considerations.md).</span></span> 

<span data-ttu-id="7e502-171">Ознакомьтесь с руководством по [установке и настройке Oracle ASM](configure-oracle-asm.md).</span><span class="sxs-lookup"><span data-stu-id="7e502-171">Try the [Installing and Configuring Oracle Automated Storage Management](configure-oracle-asm.md) tutorial.</span></span>