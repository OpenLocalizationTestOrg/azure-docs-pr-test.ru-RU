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
# <a name="implement-oracle-data-guard-on-an-azure-linux-virtual-machine"></a><span data-ttu-id="2cc5d-103">Реализация Oracle Data Guard на виртуальной машине Azure под управлением Linux</span><span class="sxs-lookup"><span data-stu-id="2cc5d-103">Implement Oracle Data Guard on an Azure Linux virtual machine</span></span> 

<span data-ttu-id="2cc5d-104">Azure CLI является используется toocreate и управления ресурсами Azure hello командной строке или в сценариях.</span><span class="sxs-lookup"><span data-stu-id="2cc5d-104">Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="2cc5d-105">В этой статье описывается, как базы данных Azure CLI toouse toodeploy базы данных Oracle 12c из образа Azure Marketplace hello.</span><span class="sxs-lookup"><span data-stu-id="2cc5d-105">This article describes how toouse Azure CLI toodeploy an Oracle Database 12c database from hello Azure Marketplace image.</span></span> <span data-ttu-id="2cc5d-106">В этой статье затем показано, шаг за шагом, как tooinstall и настроить Защитник данных на виртуальной машине Azure (ВМ).</span><span class="sxs-lookup"><span data-stu-id="2cc5d-106">This article then shows you, step by step, how tooinstall and configure Data Guard on an Azure virtual machine (VM).</span></span>

<span data-ttu-id="2cc5d-107">Прежде чем начать, убедитесь, что установлен интерфейс командной строки Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="2cc5d-107">Before you start, make sure that Azure CLI is installed.</span></span> <span data-ttu-id="2cc5d-108">Дополнительные сведения см. в разделе hello [руководство по установке Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="2cc5d-108">For more information, see hello [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="prepare-hello-environment"></a><span data-ttu-id="2cc5d-109">Подготовка среды hello</span><span class="sxs-lookup"><span data-stu-id="2cc5d-109">Prepare hello environment</span></span>
### <a name="assumptions"></a><span data-ttu-id="2cc5d-110">Предположения</span><span class="sxs-lookup"><span data-stu-id="2cc5d-110">Assumptions</span></span>

<span data-ttu-id="2cc5d-111">tooinstall Oracle Data Guard необходимо toocreate две виртуальные машины Azure на hello одной группе доступности:</span><span class="sxs-lookup"><span data-stu-id="2cc5d-111">tooinstall Oracle Data Guard, you need toocreate two Azure VMs on hello same availability set:</span></span>

- <span data-ttu-id="2cc5d-112">Hello основной виртуальной Машины (myVM1) имеет работающего экземпляра Oracle.</span><span class="sxs-lookup"><span data-stu-id="2cc5d-112">hello primary VM (myVM1) has a running Oracle instance.</span></span>
- <span data-ttu-id="2cc5d-113">Здравствуйте, резервной ВМ (myVM2) имеет только установлено программное обеспечение Oracle hello.</span><span class="sxs-lookup"><span data-stu-id="2cc5d-113">hello standby VM (myVM2) has hello Oracle software installed only.</span></span>

<span data-ttu-id="2cc5d-114">Hello образа Marketplace использовать toocreate hello виртуальных машин — Oracle: Oracle-базы данных-Ee:12.1.0.2:latest.</span><span class="sxs-lookup"><span data-stu-id="2cc5d-114">hello Marketplace image that you use toocreate hello VMs is Oracle:Oracle-Database-Ee:12.1.0.2:latest.</span></span>

### <a name="sign-in-tooazure"></a><span data-ttu-id="2cc5d-115">Войдите в tooAzure</span><span class="sxs-lookup"><span data-stu-id="2cc5d-115">Sign in tooAzure</span></span> 

<span data-ttu-id="2cc5d-116">Войти в tooyour подписки Azure, используя hello [входа az](/cli/azure/#login) команды и выполните hello на экране инструкциям.</span><span class="sxs-lookup"><span data-stu-id="2cc5d-116">Sign in tooyour Azure subscription by using hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span>

```azurecli
az login
```

### <a name="create-a-resource-group"></a><span data-ttu-id="2cc5d-117">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="2cc5d-117">Create a resource group</span></span>

<span data-ttu-id="2cc5d-118">Создание группы ресурсов с помощью hello [Создание группы az](/cli/azure/group#create) команды.</span><span class="sxs-lookup"><span data-stu-id="2cc5d-118">Create a resource group by using hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="2cc5d-119">Группа ресурсов Azure является логическим контейнером, в котором происходит развертывание ресурсов Azure и управление ими.</span><span class="sxs-lookup"><span data-stu-id="2cc5d-119">An Azure resource group is a logical container in which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="2cc5d-120">Hello следующий пример создает группу ресурсов с именем `myResourceGroup` в hello `westus` расположение:</span><span class="sxs-lookup"><span data-stu-id="2cc5d-120">hello following example creates a resource group named `myResourceGroup` in hello `westus` location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

### <a name="create-an-availability-set"></a><span data-ttu-id="2cc5d-121">"Создать группу доступности"</span><span class="sxs-lookup"><span data-stu-id="2cc5d-121">Create an availability set</span></span>

<span data-ttu-id="2cc5d-122">Создавать группу доступности необязательно, но мы рекомендуем это сделать.</span><span class="sxs-lookup"><span data-stu-id="2cc5d-122">Creating an availability set is optional, but we recommend it.</span></span> <span data-ttu-id="2cc5d-123">Дополнительные сведения см. в статье [Рекомендации по группам доступности Azure для виртуальных машин Windows](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).</span><span class="sxs-lookup"><span data-stu-id="2cc5d-123">For more information, see [Azure availability sets guidelines](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).</span></span>

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

### <a name="create-a-virtual-machine"></a><span data-ttu-id="2cc5d-124">Создание виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="2cc5d-124">Create a virtual machine</span></span>

<span data-ttu-id="2cc5d-125">Создайте виртуальную Машину с помощью hello [создания виртуальной машины az](/cli/azure/vm#create) команды.</span><span class="sxs-lookup"><span data-stu-id="2cc5d-125">Create a VM by using hello [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="2cc5d-126">Hello следующий пример создает две виртуальные машины с именем `myVM1` и `myVM2`.</span><span class="sxs-lookup"><span data-stu-id="2cc5d-126">hello following example creates two VMs named `myVM1` and `myVM2`.</span></span> <span data-ttu-id="2cc5d-127">Также создаются ключи SSH, если они не существуют в расположении ключей по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="2cc5d-127">It also creates SSH keys, if they do not already exist in a default key location.</span></span> <span data-ttu-id="2cc5d-128">toouse конкретный набор ключей, используйте hello `--ssh-key-value` параметр.</span><span class="sxs-lookup"><span data-stu-id="2cc5d-128">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>

<span data-ttu-id="2cc5d-129">Создайте myVM1 (основная):</span><span class="sxs-lookup"><span data-stu-id="2cc5d-129">Create myVM1 (primary):</span></span>
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

<span data-ttu-id="2cc5d-130">После создания виртуальной Машины hello Azure CLI показано toohello аналогичные сведения, следующий пример.</span><span class="sxs-lookup"><span data-stu-id="2cc5d-130">After you create hello VM, Azure CLI shows information similar toohello following example.</span></span> <span data-ttu-id="2cc5d-131">Обратите внимание значение hello `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="2cc5d-131">Note hello value of `publicIpAddress`.</span></span> <span data-ttu-id="2cc5d-132">Используется этот адрес tooaccess hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="2cc5d-132">You use this address tooaccess hello VM.</span></span>

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

<span data-ttu-id="2cc5d-133">Создайте myVM2 (резервная):</span><span class="sxs-lookup"><span data-stu-id="2cc5d-133">Create myVM2 (standby):</span></span>
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

<span data-ttu-id="2cc5d-134">Обратите внимание значение hello `publicIpAddress` после создания myVM2.</span><span class="sxs-lookup"><span data-stu-id="2cc5d-134">Note hello value of `publicIpAddress` after you create myVM2.</span></span>

### <a name="open-hello-tcp-port-for-connectivity"></a><span data-ttu-id="2cc5d-135">Привет открыть TCP-порт для подключения к</span><span class="sxs-lookup"><span data-stu-id="2cc5d-135">Open hello TCP port for connectivity</span></span>

<span data-ttu-id="2cc5d-136">Этот шаг позволяет настроить внешние конечные точки, которые позволяют базы данных Oracle toohello удаленного доступа.</span><span class="sxs-lookup"><span data-stu-id="2cc5d-136">This step configures external endpoints, which allow remote access toohello Oracle database.</span></span>

<span data-ttu-id="2cc5d-137">Откройте порт hello для myVM1:</span><span class="sxs-lookup"><span data-stu-id="2cc5d-137">Open hello port for myVM1:</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVM1NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

<span data-ttu-id="2cc5d-138">Hello результат должен выглядеть примерно toohello следующий ответ:</span><span class="sxs-lookup"><span data-stu-id="2cc5d-138">hello result should look similar toohello following response:</span></span>

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

<span data-ttu-id="2cc5d-139">Откройте порт hello для myVM2:</span><span class="sxs-lookup"><span data-stu-id="2cc5d-139">Open hello port for myVM2:</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVM2NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

### <a name="connect-toohello-virtual-machine"></a><span data-ttu-id="2cc5d-140">Подключение toohello виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="2cc5d-140">Connect toohello virtual machine</span></span>

<span data-ttu-id="2cc5d-141">Используйте hello следующая команда toocreate сеанс SSH с виртуальной машиной hello.</span><span class="sxs-lookup"><span data-stu-id="2cc5d-141">Use hello following command toocreate an SSH session with hello virtual machine.</span></span> <span data-ttu-id="2cc5d-142">Замените hello hello IP-адрес `publicIpAddress` значение для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="2cc5d-142">Replace hello IP address with hello `publicIpAddress` value for your virtual machine.</span></span>

```bash 
$ ssh azureuser@<publicIpAddress>
```

### <a name="create-hello-database-on-myvm1-primary"></a><span data-ttu-id="2cc5d-143">Создать hello базы данных на myVM1 (основной)</span><span class="sxs-lookup"><span data-stu-id="2cc5d-143">Create hello database on myVM1 (primary)</span></span>

<span data-ttu-id="2cc5d-144">Hello программное обеспечение Oracle уже установлен на образа Marketplace hello, поэтому hello следующим шагом является база данных tooinstall hello.</span><span class="sxs-lookup"><span data-stu-id="2cc5d-144">hello Oracle software is already installed on hello Marketplace image, so hello next step is tooinstall hello database.</span></span> 

<span data-ttu-id="2cc5d-145">Переключение toohello Oracle суперпользователя:</span><span class="sxs-lookup"><span data-stu-id="2cc5d-145">Switch toohello Oracle superuser:</span></span>

```bash
$ sudo su - oracle
```

<span data-ttu-id="2cc5d-146">Создайте базу данных hello:</span><span class="sxs-lookup"><span data-stu-id="2cc5d-146">Create hello database:</span></span>

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
<span data-ttu-id="2cc5d-147">Выходные данные должен выглядеть примерно toohello следующий ответ:</span><span class="sxs-lookup"><span data-stu-id="2cc5d-147">Outputs should look similar toohello following response:</span></span>

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

<span data-ttu-id="2cc5d-148">Задайте переменные ORACLE_SID и ORACLE_HOME hello.</span><span class="sxs-lookup"><span data-stu-id="2cc5d-148">Set hello ORACLE_SID and ORACLE_HOME variables:</span></span>

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=cdb1; export ORACLE_SID
```

<span data-ttu-id="2cc5d-149">При необходимости можно добавить ORACLE_HOME и ORACLE_SID файла toohello /home/oracle/.bashrc, чтобы эти параметры сохраняются для будущих имен входа:</span><span class="sxs-lookup"><span data-stu-id="2cc5d-149">Optionally, you can add ORACLE_HOME and ORACLE_SID toohello /home/oracle/.bashrc file, so that these settings are saved for future logins:</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
```

## <a name="configure-data-guard"></a><span data-ttu-id="2cc5d-150">Настройка Data Guard</span><span class="sxs-lookup"><span data-stu-id="2cc5d-150">Configure Data Guard</span></span>

### <a name="enable-archive-log-mode-on-myvm1-primary"></a><span data-ttu-id="2cc5d-151">Включение режима журнала архивирования на myVM1 (основная)</span><span class="sxs-lookup"><span data-stu-id="2cc5d-151">Enable archive log mode on myVM1 (primary)</span></span>

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
<span data-ttu-id="2cc5d-152">Включите принудительное ведение журнала и убедитесь, что есть хотя бы один файл журнала:</span><span class="sxs-lookup"><span data-stu-id="2cc5d-152">Enable force logging, and make sure at least one log file is present:</span></span>

```bash
SQL> ALTER DATABASE FORCE LOGGING;
SQL> ALTER SYSTEM SWITCH LOGFILE;
```

<span data-ttu-id="2cc5d-153">Создайте резервные журналы повторяемых операций:</span><span class="sxs-lookup"><span data-stu-id="2cc5d-153">Create standby redo logs:</span></span>

```bash
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo01.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo02.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo03.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo04.log') SIZE 50M;
```

<span data-ttu-id="2cc5d-154">Включить переключение обратно (в результате восстановления намного проще) и задайте STANDBY\_ФАЙЛ\_tooauto УПРАВЛЕНИЯ.</span><span class="sxs-lookup"><span data-stu-id="2cc5d-154">Turn on Flashback (which makes recovery a lot easier) and set STANDBY\_FILE\_MANAGEMENT tooauto.</span></span> <span data-ttu-id="2cc5d-155">Затем выйдите из SQL*Plus.</span><span class="sxs-lookup"><span data-stu-id="2cc5d-155">Exit SQL*Plus after that.</span></span>

```bash
SQL> ALTER DATABASE FLASHBACK ON;
SQL> ALTER SYSTEM SET STANDBY_FILE_MANAGEMENT=AUTO;
SQL> EXIT;
```

### <a name="set-up-service-on-myvm1-primary"></a><span data-ttu-id="2cc5d-156">Настройка службы на myVM1 (основная)</span><span class="sxs-lookup"><span data-stu-id="2cc5d-156">Set up service on myVM1 (primary)</span></span>

<span data-ttu-id="2cc5d-157">Изменить или создать файл tnsnames.ora hello, который находится в папке ORACLE_HOME\network\admin hello $.</span><span class="sxs-lookup"><span data-stu-id="2cc5d-157">Edit or create hello tnsnames.ora file, which is in hello $ORACLE_HOME\network\admin folder.</span></span>

<span data-ttu-id="2cc5d-158">Добавьте hello следующие записи:</span><span class="sxs-lookup"><span data-stu-id="2cc5d-158">Add hello following entries:</span></span>

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

<span data-ttu-id="2cc5d-159">Изменить или создать файл listener.ora hello, который находится в папке ORACLE_HOME\network\admin hello $.</span><span class="sxs-lookup"><span data-stu-id="2cc5d-159">Edit or create hello listener.ora file, which is in hello $ORACLE_HOME\network\admin folder.</span></span>

<span data-ttu-id="2cc5d-160">Добавьте hello следующие записи:</span><span class="sxs-lookup"><span data-stu-id="2cc5d-160">Add hello following entries:</span></span>

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

<span data-ttu-id="2cc5d-161">Включите брокер Data Guard:</span><span class="sxs-lookup"><span data-stu-id="2cc5d-161">Enable Data Guard Broker:</span></span>
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```
<span data-ttu-id="2cc5d-162">Запуск прослушивателя hello:</span><span class="sxs-lookup"><span data-stu-id="2cc5d-162">Start hello listener:</span></span>

```bash
$ lsnrctl stop
$ lsnrctl start
```

### <a name="set-up-service-on-myvm2-standby"></a><span data-ttu-id="2cc5d-163">Настройка службы на myVM2 (резервная)</span><span class="sxs-lookup"><span data-stu-id="2cc5d-163">Set up service on myVM2 (standby)</span></span>

<span data-ttu-id="2cc5d-164">SSH toomyVM2:</span><span class="sxs-lookup"><span data-stu-id="2cc5d-164">SSH toomyVM2:</span></span>

```bash 
$ ssh azureuser@<publicIpAddress>
```

<span data-ttu-id="2cc5d-165">Выполните вход в качестве пользователя Oracle:</span><span class="sxs-lookup"><span data-stu-id="2cc5d-165">Log in as Oracle:</span></span>

```bash
$ sudo su - oracle
```

<span data-ttu-id="2cc5d-166">Изменить или создать файл tnsnames.ora hello, который находится в папке ORACLE_HOME\network\admin hello $.</span><span class="sxs-lookup"><span data-stu-id="2cc5d-166">Edit or create hello tnsnames.ora file, which is in hello $ORACLE_HOME\network\admin folder.</span></span>

<span data-ttu-id="2cc5d-167">Добавьте hello следующие записи:</span><span class="sxs-lookup"><span data-stu-id="2cc5d-167">Add hello following entries:</span></span>

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

<span data-ttu-id="2cc5d-168">Изменить или создать файл listener.ora hello, который находится в папке ORACLE_HOME\network\admin hello $.</span><span class="sxs-lookup"><span data-stu-id="2cc5d-168">Edit or create hello listener.ora file, which is in hello $ORACLE_HOME\network\admin folder.</span></span>

<span data-ttu-id="2cc5d-169">Добавьте hello следующие записи:</span><span class="sxs-lookup"><span data-stu-id="2cc5d-169">Add hello following entries:</span></span>

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

<span data-ttu-id="2cc5d-170">Запуск прослушивателя hello:</span><span class="sxs-lookup"><span data-stu-id="2cc5d-170">Start hello listener:</span></span>

```bash
$ lsnrctl stop
$ lsnrctl start
```


### <a name="restore-hello-database-toomyvm2-standby"></a><span data-ttu-id="2cc5d-171">Восстановление базы данных toomyVM2 hello (резервного)</span><span class="sxs-lookup"><span data-stu-id="2cc5d-171">Restore hello database toomyVM2 (standby)</span></span>

<span data-ttu-id="2cc5d-172">Создайте файл /tmp/initcdb1_stby.ora hello параметр с hello после содержимого:</span><span class="sxs-lookup"><span data-stu-id="2cc5d-172">Create hello parameter file /tmp/initcdb1_stby.ora with hello following contents:</span></span>
```bash
*.db_name='cdb1'
```

<span data-ttu-id="2cc5d-173">Создайте папки:</span><span class="sxs-lookup"><span data-stu-id="2cc5d-173">Create folders:</span></span>

```bash
mkdir -p /u01/app/oracle/oradata/cdb1/pdbseed
mkdir -p /u01/app/oracle/oradata/cdb1/pdb1
mkdir -p /u01/app/oracle/fast_recovery_area/cdb1
mkdir -p /u01/app/oracle/admin/cdb1/adump
```

<span data-ttu-id="2cc5d-174">Создайте файл пароля:</span><span class="sxs-lookup"><span data-stu-id="2cc5d-174">Create a password file:</span></span>

```bash
$ orapwd file=/u01/app/oracle/product/12.1.0/dbhome_1/dbs/orapwcdb1 password=OraPasswd1 entries=10
```
<span data-ttu-id="2cc5d-175">Начало myVM2 hello базы данных:</span><span class="sxs-lookup"><span data-stu-id="2cc5d-175">Start hello database on myVM2:</span></span>

```bash
$ export ORACLE_SID=cdb1
$ sqlplus / as sysdba

SQL> STARTUP NOMOUNT PFILE='/tmp/initcdb1_stby.ora';
SQL> EXIT;
```

<span data-ttu-id="2cc5d-176">Восстановление базы данных hello с помощью средства RMAN hello:</span><span class="sxs-lookup"><span data-stu-id="2cc5d-176">Restore hello database by using hello RMAN tool:</span></span>

```bash
$ rman TARGET sys/OraPasswd1@cdb1 AUXILIARY sys/OraPasswd1@cdb1_stby
```

<span data-ttu-id="2cc5d-177">Выполните следующие команды в RMAN hello.</span><span class="sxs-lookup"><span data-stu-id="2cc5d-177">Run hello following commands in RMAN:</span></span>
```bash
DUPLICATE TARGET DATABASE
  FOR STANDBY
  FROM ACTIVE DATABASE
  DORECOVER
  SPFILE
    SET db_unique_name='CDB1_STBY' COMMENT 'Is standby'
  NOFILENAMECHECK;
```

<span data-ttu-id="2cc5d-178">После завершения команды hello вы увидите примерно следующие toohello сообщений.</span><span class="sxs-lookup"><span data-stu-id="2cc5d-178">You should see messages similar toohello following when hello command is completed.</span></span> <span data-ttu-id="2cc5d-179">Выйдите из RMAN.</span><span class="sxs-lookup"><span data-stu-id="2cc5d-179">Exit RMAN.</span></span>
```bash
media recovery complete, elapsed time: 00:00:00
Finished recover at 29-JUN-17
Finished Duplicate Db at 29-JUN-17

RMAN> EXIT;
```

<span data-ttu-id="2cc5d-180">При необходимости можно добавить ORACLE_HOME и ORACLE_SID файла toohello /home/oracle/.bashrc, чтобы эти параметры сохраняются для будущих имен входа:</span><span class="sxs-lookup"><span data-stu-id="2cc5d-180">Optionally, you can add ORACLE_HOME and ORACLE_SID toohello /home/oracle/.bashrc file, so that these settings are saved for future logins:</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
```

<span data-ttu-id="2cc5d-181">Включите брокер Data Guard:</span><span class="sxs-lookup"><span data-stu-id="2cc5d-181">Enable Data Guard Broker:</span></span>
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```

### <a name="configure-data-guard-broker-on-myvm1-primary"></a><span data-ttu-id="2cc5d-182">Настройка брокера Data Guard на myVM1 (основная)</span><span class="sxs-lookup"><span data-stu-id="2cc5d-182">Configure Data Guard Broker on myVM1 (primary)</span></span>

<span data-ttu-id="2cc5d-183">Запустите диспетчер Data Guard и войдите, используя SYS и пароль.</span><span class="sxs-lookup"><span data-stu-id="2cc5d-183">Start Data Guard Manager and log in by using SYS and a password.</span></span> <span data-ttu-id="2cc5d-184">(Не используйте аутентификацию операционной системы.) Выполните следующие hello.</span><span class="sxs-lookup"><span data-stu-id="2cc5d-184">(Do not use OS authentication.) Perform hello following:</span></span>

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

<span data-ttu-id="2cc5d-185">Проверить настройку hello:</span><span class="sxs-lookup"><span data-stu-id="2cc5d-185">Review hello configuration:</span></span>
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

<span data-ttu-id="2cc5d-186">После завершения установки Oracle Data Guard hello.</span><span class="sxs-lookup"><span data-stu-id="2cc5d-186">You've completed hello Oracle Data Guard setup.</span></span> <span data-ttu-id="2cc5d-187">Hello следующем разделе показано, как tootest hello подключения и переключиться.</span><span class="sxs-lookup"><span data-stu-id="2cc5d-187">hello next section shows you how tootest hello connectivity and switch over.</span></span>

### <a name="connect-hello-database-from-hello-client-machine"></a><span data-ttu-id="2cc5d-188">Подключение базы данных hello из hello клиентского компьютера</span><span class="sxs-lookup"><span data-stu-id="2cc5d-188">Connect hello database from hello client machine</span></span>

<span data-ttu-id="2cc5d-189">Обновить или создать файл tnsnames.ora hello на клиентском компьютере.</span><span class="sxs-lookup"><span data-stu-id="2cc5d-189">Update or create hello tnsnames.ora file on your client machine.</span></span> <span data-ttu-id="2cc5d-190">Этот файл обычно находится в папке $ORACLE_HOME\network\admin.</span><span class="sxs-lookup"><span data-stu-id="2cc5d-190">This file is usually in $ORACLE_HOME\network\admin.</span></span>

<span data-ttu-id="2cc5d-191">Замените hello IP-адресов с вашей `publicIpAddress` значения myVM1 и myVM2:</span><span class="sxs-lookup"><span data-stu-id="2cc5d-191">Replace hello IP addresses with your `publicIpAddress` values for myVM1 and myVM2:</span></span>

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

<span data-ttu-id="2cc5d-192">Запустите SQL*Plus:</span><span class="sxs-lookup"><span data-stu-id="2cc5d-192">Start SQL*Plus:</span></span>

```bash
$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```
## <a name="test-hello-data-guard-configuration"></a><span data-ttu-id="2cc5d-193">Конфигурация Data Guard hello теста</span><span class="sxs-lookup"><span data-stu-id="2cc5d-193">Test hello Data Guard configuration</span></span>

### <a name="switch-over-hello-database-on-myvm1-primary"></a><span data-ttu-id="2cc5d-194">Переключить базу данных hello на myVM1 (основной)</span><span class="sxs-lookup"><span data-stu-id="2cc5d-194">Switch over hello database on myVM1 (primary)</span></span>

<span data-ttu-id="2cc5d-195">tooswitch из первичного toostandby (cdb1 toocdb1_stby):</span><span class="sxs-lookup"><span data-stu-id="2cc5d-195">tooswitch from primary toostandby (cdb1 toocdb1_stby):</span></span>

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

<span data-ttu-id="2cc5d-196">Теперь можно подключиться toohello резервной базы данных.</span><span class="sxs-lookup"><span data-stu-id="2cc5d-196">You can now connect toohello standby database.</span></span>

<span data-ttu-id="2cc5d-197">Запустите SQL*Plus:</span><span class="sxs-lookup"><span data-stu-id="2cc5d-197">Start SQL*Plus:</span></span>

```bash

$ sqlplus sys/OraPasswd1@cdb1_stby
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

### <a name="switch-over-hello-database-on-myvm2-standby"></a><span data-ttu-id="2cc5d-198">Переключить базу данных hello на myVM2 (резервного)</span><span class="sxs-lookup"><span data-stu-id="2cc5d-198">Switch over hello database on myVM2 (standby)</span></span>

<span data-ttu-id="2cc5d-199">tooswitch, выполните следующие hello на myVM2:</span><span class="sxs-lookup"><span data-stu-id="2cc5d-199">tooswitch over, run hello following on myVM2:</span></span>
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

<span data-ttu-id="2cc5d-200">Опять же теперь должен быть доступ tooconnect toohello базы данных-источника.</span><span class="sxs-lookup"><span data-stu-id="2cc5d-200">Once again, you should now be able tooconnect toohello primary database.</span></span>

<span data-ttu-id="2cc5d-201">Запустите SQL*Plus:</span><span class="sxs-lookup"><span data-stu-id="2cc5d-201">Start SQL*Plus:</span></span>

```bash

$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

<span data-ttu-id="2cc5d-202">После завершения установки hello и настройки защиты данных в Oracle Linux.</span><span class="sxs-lookup"><span data-stu-id="2cc5d-202">You've finished hello installation and configuration of Data Guard on Oracle Linux.</span></span>


## <a name="delete-hello-virtual-machine"></a><span data-ttu-id="2cc5d-203">Удалить виртуальную машину hello</span><span class="sxs-lookup"><span data-stu-id="2cc5d-203">Delete hello virtual machine</span></span>

<span data-ttu-id="2cc5d-204">При hello ВМ больше не нужна, можно использовать следующие команды tooremove hello группы ресурсов, виртуальная машина и все связанные ресурсы hello:</span><span class="sxs-lookup"><span data-stu-id="2cc5d-204">When you no longer need hello VM, you can use hello following command tooremove hello resource group, VM, and all related resources:</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="2cc5d-205">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2cc5d-205">Next steps</span></span>

[<span data-ttu-id="2cc5d-206">Создание полной среды Linux с помощью Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="2cc5d-206">Tutorial: Create highly available virtual machines</span></span>](../../linux/create-cli-complete.md)

<span data-ttu-id="2cc5d-207">[Примеры Azure CLI для виртуальных машин Linux](../../linux/cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="2cc5d-207">[Explore VM deployment Azure CLI samples](../../linux/cli-samples.md)</span></span>
