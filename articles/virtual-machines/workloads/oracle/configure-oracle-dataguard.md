---
title: "Реализация Oracle Data Guard на виртуальной машине Azure под управлением Linux | Документация Майкрософт"
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
ms.openlocfilehash: 11492b85e95ddb39489e36c572af2a168b4c7af8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="implement-oracle-data-guard-on-an-azure-linux-virtual-machine"></a><span data-ttu-id="f9437-103">Реализация Oracle Data Guard на виртуальной машине Azure под управлением Linux</span><span class="sxs-lookup"><span data-stu-id="f9437-103">Implement Oracle Data Guard on an Azure Linux virtual machine</span></span> 

<span data-ttu-id="f9437-104">Azure CLI используется для создания ресурсов Azure и управления ими из командной строки или с помощью сценариев.</span><span class="sxs-lookup"><span data-stu-id="f9437-104">Azure CLI is used to create and manage Azure resources from the command line or in scripts.</span></span> <span data-ttu-id="f9437-105">В этой статье описывается, как с помощью Azure CLI развернуть базу данных Oracle Database 12c из образа Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="f9437-105">This article describes how to use Azure CLI to deploy an Oracle Database 12c database from the Azure Marketplace image.</span></span> <span data-ttu-id="f9437-106">В этой статье представлено пошаговое руководство по установке и настройке Data Guard на виртуальной машине Azure.</span><span class="sxs-lookup"><span data-stu-id="f9437-106">This article then shows you, step by step, how to install and configure Data Guard on an Azure virtual machine (VM).</span></span>

<span data-ttu-id="f9437-107">Прежде чем начать, убедитесь, что установлен интерфейс командной строки Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="f9437-107">Before you start, make sure that Azure CLI is installed.</span></span> <span data-ttu-id="f9437-108">Дополнительные сведения см. в [руководстве по установке Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="f9437-108">For more information, see the [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="prepare-the-environment"></a><span data-ttu-id="f9437-109">Подготовка среды</span><span class="sxs-lookup"><span data-stu-id="f9437-109">Prepare the environment</span></span>
### <a name="assumptions"></a><span data-ttu-id="f9437-110">Предположения</span><span class="sxs-lookup"><span data-stu-id="f9437-110">Assumptions</span></span>

<span data-ttu-id="f9437-111">Чтобы установить Oracle Data Guard, необходимо создать две виртуальные машины Azure в одной группе доступности:</span><span class="sxs-lookup"><span data-stu-id="f9437-111">To install Oracle Data Guard, you need to create two Azure VMs on the same availability set:</span></span>

- <span data-ttu-id="f9437-112">На основной виртуальной машине (myVM1) выполняется экземпляр Oracle.</span><span class="sxs-lookup"><span data-stu-id="f9437-112">The primary VM (myVM1) has a running Oracle instance.</span></span>
- <span data-ttu-id="f9437-113">На резервной виртуальной машине (myVM2) установлено только программное обеспечение Oracle.</span><span class="sxs-lookup"><span data-stu-id="f9437-113">The standby VM (myVM2) has the Oracle software installed only.</span></span>

<span data-ttu-id="f9437-114">Образ Marketplace, который вы будете использовать для создания виртуальных машин, — Oracle:Oracle-Database-Ee:12.1.0.2:latest.</span><span class="sxs-lookup"><span data-stu-id="f9437-114">The Marketplace image that you use to create the VMs is Oracle:Oracle-Database-Ee:12.1.0.2:latest.</span></span>

### <a name="sign-in-to-azure"></a><span data-ttu-id="f9437-115">Вход в Azure</span><span class="sxs-lookup"><span data-stu-id="f9437-115">Sign in to Azure</span></span> 

<span data-ttu-id="f9437-116">Войдите в подписку Azure с помощью команды [az login](/cli/azure/#login) и следуйте инструкциям на экране.</span><span class="sxs-lookup"><span data-stu-id="f9437-116">Sign in to your Azure subscription by using the [az login](/cli/azure/#login) command and follow the on-screen directions.</span></span>

```azurecli
az login
```

### <a name="create-a-resource-group"></a><span data-ttu-id="f9437-117">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="f9437-117">Create a resource group</span></span>

<span data-ttu-id="f9437-118">Создайте группу ресурсов с помощью команды [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="f9437-118">Create a resource group by using the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="f9437-119">Группа ресурсов Azure является логическим контейнером, в котором происходит развертывание ресурсов Azure и управление ими.</span><span class="sxs-lookup"><span data-stu-id="f9437-119">An Azure resource group is a logical container in which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="f9437-120">В следующем примере создается группа ресурсов с именем `myResourceGroup` в расположении `westus`:</span><span class="sxs-lookup"><span data-stu-id="f9437-120">The following example creates a resource group named `myResourceGroup` in the `westus` location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

### <a name="create-an-availability-set"></a><span data-ttu-id="f9437-121">"Создать группу доступности"</span><span class="sxs-lookup"><span data-stu-id="f9437-121">Create an availability set</span></span>

<span data-ttu-id="f9437-122">Создавать группу доступности необязательно, но мы рекомендуем это сделать.</span><span class="sxs-lookup"><span data-stu-id="f9437-122">Creating an availability set is optional, but we recommend it.</span></span> <span data-ttu-id="f9437-123">Дополнительные сведения см. в статье [Рекомендации по группам доступности Azure для виртуальных машин Windows](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).</span><span class="sxs-lookup"><span data-stu-id="f9437-123">For more information, see [Azure availability sets guidelines](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).</span></span>

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

### <a name="create-a-virtual-machine"></a><span data-ttu-id="f9437-124">Создание виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="f9437-124">Create a virtual machine</span></span>

<span data-ttu-id="f9437-125">Создайте виртуальную машину с помощью команды [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="f9437-125">Create a VM by using the [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="f9437-126">В следующем примере создаются две виртуальные машины — `myVM1` и `myVM2`,</span><span class="sxs-lookup"><span data-stu-id="f9437-126">The following example creates two VMs named `myVM1` and `myVM2`.</span></span> <span data-ttu-id="f9437-127">Также создаются ключи SSH, если они не существуют в расположении ключей по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="f9437-127">It also creates SSH keys, if they do not already exist in a default key location.</span></span> <span data-ttu-id="f9437-128">Чтобы использовать определенный набор ключей, используйте параметр `--ssh-key-value`.</span><span class="sxs-lookup"><span data-stu-id="f9437-128">To use a specific set of keys, use the `--ssh-key-value` option.</span></span>

<span data-ttu-id="f9437-129">Создайте myVM1 (основная):</span><span class="sxs-lookup"><span data-stu-id="f9437-129">Create myVM1 (primary):</span></span>
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

<span data-ttu-id="f9437-130">После создания виртуальной машины в Azure CLI отображается информация следующего вида.</span><span class="sxs-lookup"><span data-stu-id="f9437-130">After you create the VM, Azure CLI shows information similar to the following example.</span></span> <span data-ttu-id="f9437-131">Запишите значение `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="f9437-131">Note the value of `publicIpAddress`.</span></span> <span data-ttu-id="f9437-132">Этот адрес используется для доступа к виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="f9437-132">You use this address to access the VM.</span></span>

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

<span data-ttu-id="f9437-133">Создайте myVM2 (резервная):</span><span class="sxs-lookup"><span data-stu-id="f9437-133">Create myVM2 (standby):</span></span>
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

<span data-ttu-id="f9437-134">После создания виртуальной машины myVM2 запишите значение `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="f9437-134">Note the value of `publicIpAddress` after you create myVM2.</span></span>

### <a name="open-the-tcp-port-for-connectivity"></a><span data-ttu-id="f9437-135">Открытие TCP-порта для возможности подключения</span><span class="sxs-lookup"><span data-stu-id="f9437-135">Open the TCP port for connectivity</span></span>

<span data-ttu-id="f9437-136">На этом шаге настраиваются внешние конечные точки, которые обеспечивают удаленный доступ к базе данных Oracle.</span><span class="sxs-lookup"><span data-stu-id="f9437-136">This step configures external endpoints, which allow remote access to the Oracle database.</span></span>

<span data-ttu-id="f9437-137">Откройте порт для myVM1:</span><span class="sxs-lookup"><span data-stu-id="f9437-137">Open the port for myVM1:</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVM1NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

<span data-ttu-id="f9437-138">Результат должен выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="f9437-138">The result should look similar to the following response:</span></span>

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

<span data-ttu-id="f9437-139">Откройте порт для myVM2:</span><span class="sxs-lookup"><span data-stu-id="f9437-139">Open the port for myVM2:</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVM2NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

### <a name="connect-to-the-virtual-machine"></a><span data-ttu-id="f9437-140">Подключение к виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="f9437-140">Connect to the virtual machine</span></span>

<span data-ttu-id="f9437-141">Используйте следующую команду для создания сеанса SSH с виртуальной машиной.</span><span class="sxs-lookup"><span data-stu-id="f9437-141">Use the following command to create an SSH session with the virtual machine.</span></span> <span data-ttu-id="f9437-142">Замените IP-адрес общедоступным IP-адресом виртуальной машины (значение `publicIpAddress`).</span><span class="sxs-lookup"><span data-stu-id="f9437-142">Replace the IP address with the `publicIpAddress` value for your virtual machine.</span></span>

```bash 
$ ssh azureuser@<publicIpAddress>
```

### <a name="create-the-database-on-myvm1-primary"></a><span data-ttu-id="f9437-143">Создание базы данных на myVM1 (основная)</span><span class="sxs-lookup"><span data-stu-id="f9437-143">Create the database on myVM1 (primary)</span></span>

<span data-ttu-id="f9437-144">Программное обеспечение Oracle уже установлено в образе Marketplace, поэтому следующим шагом является установка базы данных.</span><span class="sxs-lookup"><span data-stu-id="f9437-144">The Oracle software is already installed on the Marketplace image, so the next step is to install the database.</span></span> 

<span data-ttu-id="f9437-145">Переключитесь на суперпользователя Oracle:</span><span class="sxs-lookup"><span data-stu-id="f9437-145">Switch to the Oracle superuser:</span></span>

```bash
$ sudo su - oracle
```

<span data-ttu-id="f9437-146">Создание базы данных</span><span class="sxs-lookup"><span data-stu-id="f9437-146">Create the database:</span></span>

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
<span data-ttu-id="f9437-147">Результат должен выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="f9437-147">Outputs should look similar to the following response:</span></span>

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
Look at the log file "/u01/app/oracle/cfgtoollogs/dbca/cdb1/cdb1.log" for further details.
```

<span data-ttu-id="f9437-148">Задайте переменные ORACLE_SID и ORACLE_HOME:</span><span class="sxs-lookup"><span data-stu-id="f9437-148">Set the ORACLE_SID and ORACLE_HOME variables:</span></span>

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=cdb1; export ORACLE_SID
```

<span data-ttu-id="f9437-149">При необходимости можно добавить ORACLE_HOME и ORACLE_SID в файл /home/oracle/.bashrc, чтобы эти параметры сохранились для последующих входов в систему:</span><span class="sxs-lookup"><span data-stu-id="f9437-149">Optionally, you can add ORACLE_HOME and ORACLE_SID to the /home/oracle/.bashrc file, so that these settings are saved for future logins:</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
```

## <a name="configure-data-guard"></a><span data-ttu-id="f9437-150">Настройка Data Guard</span><span class="sxs-lookup"><span data-stu-id="f9437-150">Configure Data Guard</span></span>

### <a name="enable-archive-log-mode-on-myvm1-primary"></a><span data-ttu-id="f9437-151">Включение режима журнала архивирования на myVM1 (основная)</span><span class="sxs-lookup"><span data-stu-id="f9437-151">Enable archive log mode on myVM1 (primary)</span></span>

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
<span data-ttu-id="f9437-152">Включите принудительное ведение журнала и убедитесь, что есть хотя бы один файл журнала:</span><span class="sxs-lookup"><span data-stu-id="f9437-152">Enable force logging, and make sure at least one log file is present:</span></span>

```bash
SQL> ALTER DATABASE FORCE LOGGING;
SQL> ALTER SYSTEM SWITCH LOGFILE;
```

<span data-ttu-id="f9437-153">Создайте резервные журналы повторяемых операций:</span><span class="sxs-lookup"><span data-stu-id="f9437-153">Create standby redo logs:</span></span>

```bash
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo01.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo02.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo03.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo04.log') SIZE 50M;
```

<span data-ttu-id="f9437-154">Включите переключение базы данных (FLASHBACK), что значительно упростит восстановление, и задайте для параметра STANDBY\_FILE\_MANAGEMENT значение AUTO.</span><span class="sxs-lookup"><span data-stu-id="f9437-154">Turn on Flashback (which makes recovery a lot easier) and set STANDBY\_FILE\_MANAGEMENT to auto.</span></span> <span data-ttu-id="f9437-155">Затем выйдите из SQL*Plus.</span><span class="sxs-lookup"><span data-stu-id="f9437-155">Exit SQL*Plus after that.</span></span>

```bash
SQL> ALTER DATABASE FLASHBACK ON;
SQL> ALTER SYSTEM SET STANDBY_FILE_MANAGEMENT=AUTO;
SQL> EXIT;
```

### <a name="set-up-service-on-myvm1-primary"></a><span data-ttu-id="f9437-156">Настройка службы на myVM1 (основная)</span><span class="sxs-lookup"><span data-stu-id="f9437-156">Set up service on myVM1 (primary)</span></span>

<span data-ttu-id="f9437-157">Измените файл tnsnames.ora, расположенный в папке $ORACLE_HOME\network\admin, или создайте его.</span><span class="sxs-lookup"><span data-stu-id="f9437-157">Edit or create the tnsnames.ora file, which is in the $ORACLE_HOME\network\admin folder.</span></span>

<span data-ttu-id="f9437-158">Добавьте следующие записи:</span><span class="sxs-lookup"><span data-stu-id="f9437-158">Add the following entries:</span></span>

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

<span data-ttu-id="f9437-159">Измените файл listener.ora, расположенный в папке $ORACLE_HOME\network\admin, или создайте его.</span><span class="sxs-lookup"><span data-stu-id="f9437-159">Edit or create the listener.ora file, which is in the $ORACLE_HOME\network\admin folder.</span></span>

<span data-ttu-id="f9437-160">Добавьте следующие записи:</span><span class="sxs-lookup"><span data-stu-id="f9437-160">Add the following entries:</span></span>

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

<span data-ttu-id="f9437-161">Включите брокер Data Guard:</span><span class="sxs-lookup"><span data-stu-id="f9437-161">Enable Data Guard Broker:</span></span>
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```
<span data-ttu-id="f9437-162">Запустите прослушиватель:</span><span class="sxs-lookup"><span data-stu-id="f9437-162">Start the listener:</span></span>

```bash
$ lsnrctl stop
$ lsnrctl start
```

### <a name="set-up-service-on-myvm2-standby"></a><span data-ttu-id="f9437-163">Настройка службы на myVM2 (резервная)</span><span class="sxs-lookup"><span data-stu-id="f9437-163">Set up service on myVM2 (standby)</span></span>

<span data-ttu-id="f9437-164">Подключитесь к виртуальной машине myVM2 по протоколу SSH:</span><span class="sxs-lookup"><span data-stu-id="f9437-164">SSH to myVM2:</span></span>

```bash 
$ ssh azureuser@<publicIpAddress>
```

<span data-ttu-id="f9437-165">Выполните вход в качестве пользователя Oracle:</span><span class="sxs-lookup"><span data-stu-id="f9437-165">Log in as Oracle:</span></span>

```bash
$ sudo su - oracle
```

<span data-ttu-id="f9437-166">Измените файл tnsnames.ora, расположенный в папке $ORACLE_HOME\network\admin, или создайте его.</span><span class="sxs-lookup"><span data-stu-id="f9437-166">Edit or create the tnsnames.ora file, which is in the $ORACLE_HOME\network\admin folder.</span></span>

<span data-ttu-id="f9437-167">Добавьте следующие записи:</span><span class="sxs-lookup"><span data-stu-id="f9437-167">Add the following entries:</span></span>

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

<span data-ttu-id="f9437-168">Измените файл listener.ora, расположенный в папке $ORACLE_HOME\network\admin, или создайте его.</span><span class="sxs-lookup"><span data-stu-id="f9437-168">Edit or create the listener.ora file, which is in the $ORACLE_HOME\network\admin folder.</span></span>

<span data-ttu-id="f9437-169">Добавьте следующие записи:</span><span class="sxs-lookup"><span data-stu-id="f9437-169">Add the following entries:</span></span>

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

<span data-ttu-id="f9437-170">Запустите прослушиватель:</span><span class="sxs-lookup"><span data-stu-id="f9437-170">Start the listener:</span></span>

```bash
$ lsnrctl stop
$ lsnrctl start
```


### <a name="restore-the-database-to-myvm2-standby"></a><span data-ttu-id="f9437-171">Восстановление базы данных на myVM2 (резервная)</span><span class="sxs-lookup"><span data-stu-id="f9437-171">Restore the database to myVM2 (standby)</span></span>

<span data-ttu-id="f9437-172">Создайте файл параметров /tmp/initcdb1_stby.ora со следующим содержимым:</span><span class="sxs-lookup"><span data-stu-id="f9437-172">Create the parameter file /tmp/initcdb1_stby.ora with the following contents:</span></span>
```bash
*.db_name='cdb1'
```

<span data-ttu-id="f9437-173">Создайте папки:</span><span class="sxs-lookup"><span data-stu-id="f9437-173">Create folders:</span></span>

```bash
mkdir -p /u01/app/oracle/oradata/cdb1/pdbseed
mkdir -p /u01/app/oracle/oradata/cdb1/pdb1
mkdir -p /u01/app/oracle/fast_recovery_area/cdb1
mkdir -p /u01/app/oracle/admin/cdb1/adump
```

<span data-ttu-id="f9437-174">Создайте файл пароля:</span><span class="sxs-lookup"><span data-stu-id="f9437-174">Create a password file:</span></span>

```bash
$ orapwd file=/u01/app/oracle/product/12.1.0/dbhome_1/dbs/orapwcdb1 password=OraPasswd1 entries=10
```
<span data-ttu-id="f9437-175">Запустите базу данных на myVM2:</span><span class="sxs-lookup"><span data-stu-id="f9437-175">Start the database on myVM2:</span></span>

```bash
$ export ORACLE_SID=cdb1
$ sqlplus / as sysdba

SQL> STARTUP NOMOUNT PFILE='/tmp/initcdb1_stby.ora';
SQL> EXIT;
```

<span data-ttu-id="f9437-176">Восстановите базу данных с помощью инструмента RMAN:</span><span class="sxs-lookup"><span data-stu-id="f9437-176">Restore the database by using the RMAN tool:</span></span>

```bash
$ rman TARGET sys/OraPasswd1@cdb1 AUXILIARY sys/OraPasswd1@cdb1_stby
```

<span data-ttu-id="f9437-177">Выполните следующие команды в RMAN:</span><span class="sxs-lookup"><span data-stu-id="f9437-177">Run the following commands in RMAN:</span></span>
```bash
DUPLICATE TARGET DATABASE
  FOR STANDBY
  FROM ACTIVE DATABASE
  DORECOVER
  SPFILE
    SET db_unique_name='CDB1_STBY' COMMENT 'Is standby'
  NOFILENAMECHECK;
```

<span data-ttu-id="f9437-178">После выполнения команды должны отобразиться сообщения, аналогичные приведенным ниже.</span><span class="sxs-lookup"><span data-stu-id="f9437-178">You should see messages similar to the following when the command is completed.</span></span> <span data-ttu-id="f9437-179">Выйдите из RMAN.</span><span class="sxs-lookup"><span data-stu-id="f9437-179">Exit RMAN.</span></span>
```bash
media recovery complete, elapsed time: 00:00:00
Finished recover at 29-JUN-17
Finished Duplicate Db at 29-JUN-17

RMAN> EXIT;
```

<span data-ttu-id="f9437-180">При необходимости можно добавить ORACLE_HOME и ORACLE_SID в файл /home/oracle/.bashrc, чтобы эти параметры сохранились для последующих входов в систему:</span><span class="sxs-lookup"><span data-stu-id="f9437-180">Optionally, you can add ORACLE_HOME and ORACLE_SID to the /home/oracle/.bashrc file, so that these settings are saved for future logins:</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
```

<span data-ttu-id="f9437-181">Включите брокер Data Guard:</span><span class="sxs-lookup"><span data-stu-id="f9437-181">Enable Data Guard Broker:</span></span>
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```

### <a name="configure-data-guard-broker-on-myvm1-primary"></a><span data-ttu-id="f9437-182">Настройка брокера Data Guard на myVM1 (основная)</span><span class="sxs-lookup"><span data-stu-id="f9437-182">Configure Data Guard Broker on myVM1 (primary)</span></span>

<span data-ttu-id="f9437-183">Запустите диспетчер Data Guard и войдите, используя SYS и пароль.</span><span class="sxs-lookup"><span data-stu-id="f9437-183">Start Data Guard Manager and log in by using SYS and a password.</span></span> <span data-ttu-id="f9437-184">(Не используйте аутентификацию операционной системы.) Выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="f9437-184">(Do not use OS authentication.) Perform the following:</span></span>

```bash
$ dgmgrl sys/OraPasswd1@cdb1
DGMGRL for Linux: Version 12.1.0.2.0 - 64bit Production

Copyright (c) 2000, 2013, Oracle. All rights reserved.

Welcome to DGMGRL, type "help" for information.
Connected as SYSDBA.
DGMGRL> CREATE CONFIGURATION my_dg_config AS PRIMARY DATABASE IS cdb1 CONNECT IDENTIFIER IS cdb1;
Configuration "my_dg_config" created with primary database "cdb1"
DGMGRL> ADD DATABASE cdb1_stby AS CONNECT IDENTIFIER IS cdb1_stby MAINTAINED AS PHYSICAL;
Database "cdb1_stby" added
DGMGRL> ENABLE CONFIGURATION;
Enabled.
```

<span data-ttu-id="f9437-185">Проверьте конфигурацию:</span><span class="sxs-lookup"><span data-stu-id="f9437-185">Review the configuration:</span></span>
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

<span data-ttu-id="f9437-186">Настройка Oracle Data Guard завершена.</span><span class="sxs-lookup"><span data-stu-id="f9437-186">You've completed the Oracle Data Guard setup.</span></span> <span data-ttu-id="f9437-187">В следующем разделе показано, как проверить подключение и переключение.</span><span class="sxs-lookup"><span data-stu-id="f9437-187">The next section shows you how to test the connectivity and switch over.</span></span>

### <a name="connect-the-database-from-the-client-machine"></a><span data-ttu-id="f9437-188">Подключение базы данных с клиентского компьютера</span><span class="sxs-lookup"><span data-stu-id="f9437-188">Connect the database from the client machine</span></span>

<span data-ttu-id="f9437-189">Обновите файл tnsnames.ora на клиентском компьютере или создайте его.</span><span class="sxs-lookup"><span data-stu-id="f9437-189">Update or create the tnsnames.ora file on your client machine.</span></span> <span data-ttu-id="f9437-190">Этот файл обычно находится в папке $ORACLE_HOME\network\admin.</span><span class="sxs-lookup"><span data-stu-id="f9437-190">This file is usually in $ORACLE_HOME\network\admin.</span></span>

<span data-ttu-id="f9437-191">Замените IP-адреса своими значениями `publicIpAddress` для myVM1 и myVM2:</span><span class="sxs-lookup"><span data-stu-id="f9437-191">Replace the IP addresses with your `publicIpAddress` values for myVM1 and myVM2:</span></span>

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

<span data-ttu-id="f9437-192">Запустите SQL*Plus:</span><span class="sxs-lookup"><span data-stu-id="f9437-192">Start SQL*Plus:</span></span>

```bash
$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With the Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```
## <a name="test-the-data-guard-configuration"></a><span data-ttu-id="f9437-193">Проверка конфигурации Data Guard</span><span class="sxs-lookup"><span data-stu-id="f9437-193">Test the Data Guard configuration</span></span>

### <a name="switch-over-the-database-on-myvm1-primary"></a><span data-ttu-id="f9437-194">Переключение базы данных на виртуальной машине myVM1 (основная)</span><span class="sxs-lookup"><span data-stu-id="f9437-194">Switch over the database on myVM1 (primary)</span></span>

<span data-ttu-id="f9437-195">Переключитесь с основной базы данных на резервную (с cdb1 на cdb1_stby):</span><span class="sxs-lookup"><span data-stu-id="f9437-195">To switch from primary to standby (cdb1 to cdb1_stby):</span></span>

```bash
$ dgmgrl sys/OraPasswd1@cdb1
DGMGRL for Linux: Version 12.1.0.2.0 - 64bit Production

Copyright (c) 2000, 2013, Oracle. All rights reserved.

Welcome to DGMGRL, type "help" for information.
Connected as SYSDBA.
DGMGRL> SWITCHOVER TO cdb1_stby;
Performing switchover NOW, please wait...
Operation requires a connection to instance "cdb1" on database "cdb1_stby"
Connecting to instance "cdb1"...
Connected as SYSDBA.
New primary database "cdb1_stby" is opening...
Operation requires start up of instance "cdb1" on database "cdb1"
Starting instance "cdb1"...
ORACLE instance started.
Database mounted.
Switchover succeeded, new primary is "cdb1_stby"
DGMGRL>
```

<span data-ttu-id="f9437-196">Теперь можно подключиться к резервной базе данных.</span><span class="sxs-lookup"><span data-stu-id="f9437-196">You can now connect to the standby database.</span></span>

<span data-ttu-id="f9437-197">Запустите SQL*Plus:</span><span class="sxs-lookup"><span data-stu-id="f9437-197">Start SQL*Plus:</span></span>

```bash

$ sqlplus sys/OraPasswd1@cdb1_stby
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With the Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

### <a name="switch-over-the-database-on-myvm2-standby"></a><span data-ttu-id="f9437-198">Переключение базы данных на виртуальной машине myVM2 (резервная)</span><span class="sxs-lookup"><span data-stu-id="f9437-198">Switch over the database on myVM2 (standby)</span></span>

<span data-ttu-id="f9437-199">Чтобы переключиться обратно, на виртуальной машине myVM2 выполните следующее:</span><span class="sxs-lookup"><span data-stu-id="f9437-199">To switch over, run the following on myVM2:</span></span>
```bash
$ dgmgrl sys/OraPasswd1@cdb1_stby
DGMGRL for Linux: Version 12.1.0.2.0 - 64bit Production

Copyright (c) 2000, 2013, Oracle. All rights reserved.

Welcome to DGMGRL, type "help" for information.
Connected as SYSDBA.
DGMGRL> SWITCHOVER TO cdb1;
Performing switchover NOW, please wait...
Operation requires a connection to instance "cdb1" on database "cdb1"
Connecting to instance "cdb1"...
Connected as SYSDBA.
New primary database "cdb1" is opening...
Operation requires start up of instance "cdb1" on database "cdb1_stby"
Starting instance "cdb1"...
ORACLE instance started.
Database mounted.
Switchover succeeded, new primary is "cdb1"
```

<span data-ttu-id="f9437-200">Теперь вы снова имеете возможность подключиться к основной базе данных.</span><span class="sxs-lookup"><span data-stu-id="f9437-200">Once again, you should now be able to connect to the primary database.</span></span>

<span data-ttu-id="f9437-201">Запустите SQL*Plus:</span><span class="sxs-lookup"><span data-stu-id="f9437-201">Start SQL*Plus:</span></span>

```bash

$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With the Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

<span data-ttu-id="f9437-202">Вы завершили установку и настройку Data Guard на Oracle Linux.</span><span class="sxs-lookup"><span data-stu-id="f9437-202">You've finished the installation and configuration of Data Guard on Oracle Linux.</span></span>


## <a name="delete-the-virtual-machine"></a><span data-ttu-id="f9437-203">Удаление виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="f9437-203">Delete the virtual machine</span></span>

<span data-ttu-id="f9437-204">Вы можете удалить ставшие ненужными группу ресурсов, виртуальную машину и все связанные с ней ресурсы, использовав следующую команду:</span><span class="sxs-lookup"><span data-stu-id="f9437-204">When you no longer need the VM, you can use the following command to remove the resource group, VM, and all related resources:</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="f9437-205">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f9437-205">Next steps</span></span>

[<span data-ttu-id="f9437-206">Создание полной среды Linux с помощью Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="f9437-206">Tutorial: Create highly available virtual machines</span></span>](../../linux/create-cli-complete.md)

<span data-ttu-id="f9437-207">[Примеры Azure CLI для виртуальных машин Linux](../../linux/cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="f9437-207">[Explore VM deployment Azure CLI samples](../../linux/cli-samples.md)</span></span>
