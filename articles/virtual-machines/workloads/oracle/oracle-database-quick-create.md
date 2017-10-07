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
# <a name="create-an-oracle-database-in-an-azure-vm"></a><span data-ttu-id="2347f-103">Создание базы данных Oracle на виртуальной машине Azure</span><span class="sxs-lookup"><span data-stu-id="2347f-103">Create an Oracle Database in an Azure VM</span></span>

<span data-ttu-id="2347f-104">В этом руководстве рассматривается использование hello Azure CLI toodeploy виртуальной машине Azure из hello [образ из коллекции marketplace Oracle](https://azuremarketplace.microsoft.com/marketplace/apps/Oracle.OracleDatabase12102EnterpriseEdition?tab=Overview) чтобы toocreate базы данных Oracle 12 c.</span><span class="sxs-lookup"><span data-stu-id="2347f-104">This guide details using hello Azure CLI toodeploy an Azure virtual machine from hello [Oracle marketplace gallery image](https://azuremarketplace.microsoft.com/marketplace/apps/Oracle.OracleDatabase12102EnterpriseEdition?tab=Overview) in order toocreate an Oracle 12c database.</span></span> <span data-ttu-id="2347f-105">После развертывания сервера hello нужно будет подключиться по протоколу SSH в базе данных Oracle hello tooconfigure заказа.</span><span class="sxs-lookup"><span data-stu-id="2347f-105">Once hello server is deployed, you will connect via SSH in order tooconfigure hello Oracle database.</span></span> 

<span data-ttu-id="2347f-106">Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/?WT.mc_id=A261C142F), прежде чем начинать работу.</span><span class="sxs-lookup"><span data-stu-id="2347f-106">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="2347f-107">Если выбрать tooinstall и использовать hello CLI локально, краткого руководства требуется управлением hello Azure CLI версия 2.0.4 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="2347f-107">If you choose tooinstall and use hello CLI locally, this quickstart requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="2347f-108">Запустите `az --version` версии toofind hello.</span><span class="sxs-lookup"><span data-stu-id="2347f-108">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="2347f-109">Если требуется tooinstall или обновления, см. раздел [установить CLI Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="2347f-109">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="2347f-110">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="2347f-110">Create a resource group</span></span>

<span data-ttu-id="2347f-111">Создание группы ресурсов с hello [Создание группы az](/cli/azure/group#create) команды.</span><span class="sxs-lookup"><span data-stu-id="2347f-111">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="2347f-112">Группа ресурсов Azure является логическим контейнером, в котором происходит развертывание ресурсов Azure и управление ими.</span><span class="sxs-lookup"><span data-stu-id="2347f-112">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="2347f-113">Hello следующий пример создает группу ресурсов с именем *myResourceGroup* в hello *eastus* расположение.</span><span class="sxs-lookup"><span data-stu-id="2347f-113">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```
## <a name="create-virtual-machine"></a><span data-ttu-id="2347f-114">Создание виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="2347f-114">Create virtual machine</span></span>

<span data-ttu-id="2347f-115">toocreate виртуальной машины (VM), использовать hello [создания виртуальной машины az](/cli/azure/vm#create) команды.</span><span class="sxs-lookup"><span data-stu-id="2347f-115">toocreate a virtual machine (VM), use hello [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="2347f-116">Hello следующий пример создает Виртуальную машину с именем `myVM`.</span><span class="sxs-lookup"><span data-stu-id="2347f-116">hello following example creates a VM named `myVM`.</span></span> <span data-ttu-id="2347f-117">Также создаются ключи SSH, если они не существуют в расположении ключей по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="2347f-117">It also creates SSH keys, if they do not already exist in a default key location.</span></span> <span data-ttu-id="2347f-118">toouse конкретный набор ключей, используйте hello `--ssh-key-value` параметр.</span><span class="sxs-lookup"><span data-stu-id="2347f-118">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>  

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
    --size Standard_DS2_v2 \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="2347f-119">После создания виртуальной Машины hello Azure CLI отображает toohello аналогичные сведения, следующий пример.</span><span class="sxs-lookup"><span data-stu-id="2347f-119">After you create hello VM, Azure CLI displays information similar toohello following example.</span></span> <span data-ttu-id="2347f-120">Запомните значение hello для `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="2347f-120">Note hello value for `publicIpAddress`.</span></span> <span data-ttu-id="2347f-121">Используется этот адрес tooaccess hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="2347f-121">You use this address tooaccess hello VM.</span></span>

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

## <a name="connect-toohello-vm"></a><span data-ttu-id="2347f-122">Подключение toohello виртуальной Машины</span><span class="sxs-lookup"><span data-stu-id="2347f-122">Connect toohello VM</span></span>

<span data-ttu-id="2347f-123">toocreate сеанс SSH с hello виртуальной Машины, используйте следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="2347f-123">toocreate an SSH session with hello VM, use hello following command.</span></span> <span data-ttu-id="2347f-124">Замените hello hello IP-адрес `publicIpAddress` значение для виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="2347f-124">Replace hello IP address with hello `publicIpAddress` value for your VM.</span></span>

```bash 
ssh <publicIpAddress>
```

## <a name="create-hello-database"></a><span data-ttu-id="2347f-125">Создание базы данных hello</span><span class="sxs-lookup"><span data-stu-id="2347f-125">Create hello database</span></span>

<span data-ttu-id="2347f-126">Hello программное обеспечение Oracle уже установлены на образа Marketplace hello.</span><span class="sxs-lookup"><span data-stu-id="2347f-126">hello Oracle software is already installed on hello Marketplace image.</span></span> <span data-ttu-id="2347f-127">Создайте пример базы данных, как описано ниже.</span><span class="sxs-lookup"><span data-stu-id="2347f-127">Create a sample database as follows.</span></span> 

1.  <span data-ttu-id="2347f-128">Переключение toohello *oracle* суперпользователя, а затем инициализировать прослушиватель hello для ведения журнала:</span><span class="sxs-lookup"><span data-stu-id="2347f-128">Switch toohello *oracle* superuser, then initialize hello listener for logging:</span></span>

    ```bash
    $ sudo su - oracle
    $ lsnrctl start
    ```

    <span data-ttu-id="2347f-129">Hello выходные данные выглядят аналогично toohello следующее:</span><span class="sxs-lookup"><span data-stu-id="2347f-129">hello output is similar toohello following:</span></span>

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

2.  <span data-ttu-id="2347f-130">Создайте базу данных hello:</span><span class="sxs-lookup"><span data-stu-id="2347f-130">Create hello database:</span></span>

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

    <span data-ttu-id="2347f-131">Он принимает несколько баз данных hello toocreate минут.</span><span class="sxs-lookup"><span data-stu-id="2347f-131">It takes a few minutes toocreate hello database.</span></span>

3. <span data-ttu-id="2347f-132">Задайте переменные Oracle.</span><span class="sxs-lookup"><span data-stu-id="2347f-132">Set Oracle variables</span></span>

<span data-ttu-id="2347f-133">Перед подключением необходимо tooset двух переменных среды: *ORACLE_HOME* и *ORACLE_SID*.</span><span class="sxs-lookup"><span data-stu-id="2347f-133">Before you connect, you need tooset two environment variables: *ORACLE_HOME* and *ORACLE_SID*.</span></span>

```bash
ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
ORACLE_SID=cdb1; export ORACLE_SID
```
<span data-ttu-id="2347f-134">Также можно добавить ORACLE_HOME и ORACLE_SID файл .bashrc toohello переменных.</span><span class="sxs-lookup"><span data-stu-id="2347f-134">You also can add ORACLE_HOME and ORACLE_SID variables toohello .bashrc file.</span></span> <span data-ttu-id="2347f-135">Это может сэкономить hello переменные среды для будущих входа в систему. Подтвердите hello следующие операторы были добавлены toohello `~/.bashrc` файла с помощью редактора по своему усмотрению.</span><span class="sxs-lookup"><span data-stu-id="2347f-135">This would save hello environment variables for future sign-ins. Confirm hello following statements have been added toohello `~/.bashrc` file using editor of your choice.</span></span>

```bash
# Add ORACLE_HOME. 
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1 
# Add ORACLE_SID. 
export ORACLE_SID=cdb1 
```

## <a name="oracle-em-express-connectivity"></a><span data-ttu-id="2347f-136">Подключение к Oracle EM Express</span><span class="sxs-lookup"><span data-stu-id="2347f-136">Oracle EM Express connectivity</span></span>

<span data-ttu-id="2347f-137">Средства управления графического интерфейса пользователя, который можно использовать tooexplore hello базы данных, настроить Oracle EM Express.</span><span class="sxs-lookup"><span data-stu-id="2347f-137">For a GUI management tool that you can use tooexplore hello database, set up Oracle EM Express.</span></span> <span data-ttu-id="2347f-138">tooOracle tooconnect EM Express, необходимо сначала настроить порт hello в Oracle.</span><span class="sxs-lookup"><span data-stu-id="2347f-138">tooconnect tooOracle EM Express, you must first set up hello port in Oracle.</span></span> 

1. <span data-ttu-id="2347f-139">Подключение базы данных tooyour, с помощью sqlplus:</span><span class="sxs-lookup"><span data-stu-id="2347f-139">Connect tooyour database using sqlplus:</span></span>

    ```bash
    sqlplus / as sysdba
    ```

2. <span data-ttu-id="2347f-140">После подключения задайте порт hello 5502 для EM, экспресс-выпуск</span><span class="sxs-lookup"><span data-stu-id="2347f-140">Once connected, set hello port 5502 for EM Express</span></span>

    ```bash
    exec DBMS_XDB_CONFIG.SETHTTPSPORT(5502);
    ```

3. <span data-ttu-id="2347f-141">Привет открыть контейнер PDB1 случае hello уже открыт, но сначала проверить его состояние:</span><span class="sxs-lookup"><span data-stu-id="2347f-141">Open hello container PDB1 if not already opened, but first check hello status:</span></span>

    ```bash
    select con_id, name, open_mode from v$pdbs;
    ```

    <span data-ttu-id="2347f-142">Hello выходные данные выглядят аналогично toohello следующее:</span><span class="sxs-lookup"><span data-stu-id="2347f-142">hello output is similar toohello following:</span></span>

    ```bash
      CON_ID NAME                           OPEN_MODE 
      ----------- ------------------------- ---------- 
      2           PDB$SEED                  READ ONLY 
      3           PDB1                      MOUNT
    ```

4. <span data-ttu-id="2347f-143">Если hello OPEN_MODE для `PDB1` не чтения и записи, затем запустите hello следующие команды tooopen PDB1:</span><span class="sxs-lookup"><span data-stu-id="2347f-143">If hello OPEN_MODE for `PDB1` is not READ WRITE, then run hello followings commands tooopen PDB1:</span></span>

   ```bash
    alter session set container=pdb1;
    alter database open;
   ```

<span data-ttu-id="2347f-144">Требуется tootype `quit` tooend hello sqlplus сеанса и тип `exit` toologout пользователя oracle hello.</span><span class="sxs-lookup"><span data-stu-id="2347f-144">You need tootype `quit` tooend hello sqlplus session and type `exit` toologout of hello oracle user.</span></span>

## <a name="automate-database-startup-and-shutdown"></a><span data-ttu-id="2347f-145">Автоматизация запуска и завершения работы базы данных</span><span class="sxs-lookup"><span data-stu-id="2347f-145">Automate database startup and shutdown</span></span>

<span data-ttu-id="2347f-146">Hello базы данных Oracle по умолчанию не запускается автоматически при перезагрузке hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="2347f-146">hello Oracle database by default doesn't automatically start when you restart hello VM.</span></span> <span data-ttu-id="2347f-147">tooset копирование toostart базы данных Oracle hello автоматически, выполните вход как корень.</span><span class="sxs-lookup"><span data-stu-id="2347f-147">tooset up hello Oracle database toostart automatically, first sign in as root.</span></span> <span data-ttu-id="2347f-148">Затем создайте и обновите некоторые системные файлы.</span><span class="sxs-lookup"><span data-stu-id="2347f-148">Then, create and update some system files.</span></span>

1. <span data-ttu-id="2347f-149">Войдите с правами привилегированного пользователя.</span><span class="sxs-lookup"><span data-stu-id="2347f-149">Sign on as root</span></span>
    ```bash
    sudo su -
    ```

2.  <span data-ttu-id="2347f-150">Используя текстовый редактор, измените файл hello `/etc/oratab` и изменить по умолчанию hello `N` слишком`Y`:</span><span class="sxs-lookup"><span data-stu-id="2347f-150">Using your favorite editor, edit hello file `/etc/oratab` and change hello default `N` too`Y`:</span></span>

    ```bash
    cdb1:/u01/app/oracle/product/12.1.0/dbhome_1:Y
    ```

3.  <span data-ttu-id="2347f-151">Создайте файл с именем `/etc/init.d/dbora` и вставить hello содержимое:</span><span class="sxs-lookup"><span data-stu-id="2347f-151">Create a file named `/etc/init.d/dbora` and paste hello following contents:</span></span>

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

4.  <span data-ttu-id="2347f-152">Измените разрешения для файлов с помощью команды *chmod*:</span><span class="sxs-lookup"><span data-stu-id="2347f-152">Change permissions on files with *chmod* as follows:</span></span>

    ```bash
    chgrp dba /etc/init.d/dbora
    chmod 750 /etc/init.d/dbora
    ```

5.  <span data-ttu-id="2347f-153">Создайте символьные ссылки для запуска и завершения работы:</span><span class="sxs-lookup"><span data-stu-id="2347f-153">Create symbolic links for startup and shutdown as follows:</span></span>

    ```bash
    ln -s /etc/init.d/dbora /etc/rc.d/rc0.d/K01dbora
    ln -s /etc/init.d/dbora /etc/rc.d/rc3.d/S99dbora
    ln -s /etc/init.d/dbora /etc/rc.d/rc5.d/S99dbora
    ```

6.  <span data-ttu-id="2347f-154">tootest изменения, перезапустите hello виртуальной Машины:</span><span class="sxs-lookup"><span data-stu-id="2347f-154">tootest your changes, restart hello VM:</span></span>

    ```bash
    reboot
    ```

## <a name="open-ports-for-connectivity"></a><span data-ttu-id="2347f-155">Открытие портов для подключения</span><span class="sxs-lookup"><span data-stu-id="2347f-155">Open ports for connectivity</span></span>

<span data-ttu-id="2347f-156">Последняя задача Hello является tooconfigure некоторые внешние конечные точки.</span><span class="sxs-lookup"><span data-stu-id="2347f-156">hello final task is tooconfigure some external endpoints.</span></span> <span data-ttu-id="2347f-157">tooset копирование hello Azure сетевой группы безопасности, защищающий hello ВМ, сначала закрыть сеанс SSH в hello виртуальной Машины (должен был запущен вне SSH при перезагрузке в предыдущем шаге).</span><span class="sxs-lookup"><span data-stu-id="2347f-157">tooset up hello Azure Network Security Group that protects hello VM, first exit your SSH session in hello VM (should have been kicked out of SSH when rebooting in previous step).</span></span> 

1.  <span data-ttu-id="2347f-158">tooopen конечную точку hello удаленно, использовании базы данных Oracle hello tooaccess, создайте правило группы безопасности сети с [создать правило nsg сети az](/cli/azure/network/nsg/rule#create) следующим образом:</span><span class="sxs-lookup"><span data-stu-id="2347f-158">tooopen hello endpoint that you use tooaccess hello Oracle database remotely, create a Network Security Group rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create) as follows:</span></span> 

    ```azurecli-interactive
    az network nsg rule create \
        --resource-group myResourceGroup\
        --nsg-name myVmNSG \
        --name allow-oracle \
        --protocol tcp \
        --priority 1001 \
        --destination-port-range 1521
    ```

2.  <span data-ttu-id="2347f-159">tooopen конечную точку hello удаленно, используйте tooaccess Oracle EM Express, создайте правило группы безопасности сети с [создать правило nsg сети az](/cli/azure/network/nsg/rule#create) следующим образом:</span><span class="sxs-lookup"><span data-stu-id="2347f-159">tooopen hello endpoint that you use tooaccess Oracle EM Express remotely, create a Network Security Group rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create) as follows:</span></span>

    ```azurecli-interactive
    az network nsg rule create \
        --resource-group myResourceGroup \
        --nsg-name myVmNSG \
        --name allow-oracle-EM \
        --protocol tcp \
        --priority 1002 \
        --destination-port-range 5502
    ```

3. <span data-ttu-id="2347f-160">При необходимости получить hello общедоступный IP-адрес виртуальной Машины с [az сети public-ip show](/cli/azure/network/public-ip#show) следующим образом:</span><span class="sxs-lookup"><span data-stu-id="2347f-160">If needed, obtain hello public IP address of your VM again with [az network public-ip show](/cli/azure/network/public-ip#show) as follows:</span></span>

    ```azurecli-interactive
    az network public-ip show \
        --resource-group myResourceGroup \
        --name myVMPublicIP \
        --query [ipAddress] \
        --output tsv
    ```

4.  <span data-ttu-id="2347f-161">Подключите EM Express с помощью браузера.</span><span class="sxs-lookup"><span data-stu-id="2347f-161">Connect EM Express from your browser.</span></span> <span data-ttu-id="2347f-162">Убедитесь, что браузер совместим с EM Express (также необходимо установить Flash).</span><span class="sxs-lookup"><span data-stu-id="2347f-162">Make sure your browser is compatible with EM Express (Flash install is required):</span></span> 

    ```
    https://<VM ip address or hostname>:5502/em
    ```

<span data-ttu-id="2347f-163">Вы можете войти с помощью hello **SYS** учетную запись, а также проверьте hello **как sysdba** флажок.</span><span class="sxs-lookup"><span data-stu-id="2347f-163">You can log in by using hello **SYS** account, and check hello **as sysdba** checkbox.</span></span> <span data-ttu-id="2347f-164">Использовать пароль hello **OraPasswd1** , заданным во время установки.</span><span class="sxs-lookup"><span data-stu-id="2347f-164">Use hello password **OraPasswd1** that you set during installation.</span></span> 

![Снимок экрана со страницей входа Oracle OEM Express hello](./media/oracle-quick-start/oracle_oem_express_login.png)

## <a name="clean-up-resources"></a><span data-ttu-id="2347f-166">Очистка ресурсов</span><span class="sxs-lookup"><span data-stu-id="2347f-166">Clean up resources</span></span>

<span data-ttu-id="2347f-167">Когда Вы завершили изучение первой базы данных Oracle в Azure и hello ВМ больше не нужен, можно использовать hello [удаление группы az](/cli/azure/group#delete) команд группы ресурсов tooremove hello, виртуальных Машин и все связанные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="2347f-167">Once you have finished exploring your first Oracle database on Azure and hello VM is no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="2347f-168">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2347f-168">Next steps</span></span>

<span data-ttu-id="2347f-169">Узнайте о других [решениях Oracle в Azure](oracle-considerations.md).</span><span class="sxs-lookup"><span data-stu-id="2347f-169">Learn about other [Oracle solutions on Azure](oracle-considerations.md).</span></span> 

<span data-ttu-id="2347f-170">Повторите hello [Установка и настройка управления хранением автоматических Oracle](configure-oracle-asm.md) учебника.</span><span class="sxs-lookup"><span data-stu-id="2347f-170">Try hello [Installing and Configuring Oracle Automated Storage Management](configure-oracle-asm.md) tutorial.</span></span>
