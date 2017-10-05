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
ms.openlocfilehash: fe8b635936c74c5154ec83d34160b9aae61c45e9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="implement-oracle-data-guard-on-azure-linux-vm"></a><span data-ttu-id="95662-103">Реализация Oracle Data Guard на виртуальной машине Azure под управлением Linux</span><span class="sxs-lookup"><span data-stu-id="95662-103">Implement Oracle Data Guard on Azure Linux VM</span></span> 

<span data-ttu-id="95662-104">Azure CLI используется для создания ресурсов Azure и управления ими из командной строки или с помощью скриптов.</span><span class="sxs-lookup"><span data-stu-id="95662-104">The Azure CLI is used to create and manage Azure resources from the command line or in scripts.</span></span> <span data-ttu-id="95662-105">В данном руководстве описывается, как с помощью Azure CLI развернуть базу данных Oracle 12c, используя образ из коллекции Marketplace.</span><span class="sxs-lookup"><span data-stu-id="95662-105">This guide details using the Azure CLI to deploy an Oracle 12c Database from the Marketplace gallery image.</span></span> <span data-ttu-id="95662-106">В этом документе показано пошаговое руководство по установке и настройке Data Guard на виртуальной машине Azure после создания базы данных Oracle.</span><span class="sxs-lookup"><span data-stu-id="95662-106">Once the Oracle database is created, this document shows you step-by-step how to install and configure Data Guard on Azure VM.</span></span>

<span data-ttu-id="95662-107">Перед началом работы убедитесь, что вы установили Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="95662-107">Before you start, make sure that the Azure CLI has been installed.</span></span> <span data-ttu-id="95662-108">Дополнительные сведения см. в [руководстве по установке Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="95662-108">For more information, see [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="prepare-the-environment"></a><span data-ttu-id="95662-109">Подготовка среды</span><span class="sxs-lookup"><span data-stu-id="95662-109">Prepare the environment</span></span>
### <a name="assumptions"></a><span data-ttu-id="95662-110">Предположения</span><span class="sxs-lookup"><span data-stu-id="95662-110">Assumptions</span></span>

<span data-ttu-id="95662-111">Чтобы выполнить установку Oracle Data Guard, вам необходимо создать две виртуальные машины Azure в одной и той же группе доступности.</span><span class="sxs-lookup"><span data-stu-id="95662-111">To perform the Oracle Data Guard install, you need to create two Azure VMs on the same availability set.</span></span> <span data-ttu-id="95662-112">Образ Marketplace, который вы будете использовать для создания виртуальных машин, — "Oracle:Oracle-Database-Ee:12.1.0.2:latest".</span><span class="sxs-lookup"><span data-stu-id="95662-112">The Marketplace image you use to create the VMs is "Oracle:Oracle-Database-Ee:12.1.0.2:latest".</span></span>

<span data-ttu-id="95662-113">На основной виртуальной машине (myVM1) выполняется экземпляр Oracle.</span><span class="sxs-lookup"><span data-stu-id="95662-113">The primary VM (myVM1) has a running Oracle instance.</span></span>

<span data-ttu-id="95662-114">На резервной виртуальной машине (myVM2) установлено только программное обеспечение Oracle.</span><span class="sxs-lookup"><span data-stu-id="95662-114">The standby VM (myVM2) has the Oracle software installed only.</span></span>

### <a name="log-in-to-azure"></a><span data-ttu-id="95662-115">Вход в Azure</span><span class="sxs-lookup"><span data-stu-id="95662-115">Log in to Azure</span></span> 

<span data-ttu-id="95662-116">Войдите в подписку Azure с помощью команды [az login](/cli/azure/#login) и следуйте инструкциям на экране.</span><span class="sxs-lookup"><span data-stu-id="95662-116">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions.</span></span>

```azurecli
az login
```

### <a name="create-a-resource-group"></a><span data-ttu-id="95662-117">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="95662-117">Create a resource group</span></span>

<span data-ttu-id="95662-118">Создайте группу ресурсов с помощью команды [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="95662-118">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="95662-119">Группа ресурсов Azure является логическим контейнером, в котором происходит развертывание ресурсов Azure и управление ими.</span><span class="sxs-lookup"><span data-stu-id="95662-119">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="95662-120">В следующем примере создается группа ресурсов с именем `myResourceGroup` в расположении `westus`.</span><span class="sxs-lookup"><span data-stu-id="95662-120">The following example creates a resource group named `myResourceGroup` in the `westus` location.</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

### <a name="create-availability-set"></a><span data-ttu-id="95662-121">Создание группы доступности</span><span class="sxs-lookup"><span data-stu-id="95662-121">Create availability set</span></span>

<span data-ttu-id="95662-122">Этот шаг необязателен, но мы советуем его выполнить.</span><span class="sxs-lookup"><span data-stu-id="95662-122">This step is optional, but is recommended.</span></span> <span data-ttu-id="95662-123">Дополнительные сведения см. в статье [Рекомендации по группам доступности Azure для виртуальных машин Windows](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).</span><span class="sxs-lookup"><span data-stu-id="95662-123">see [Azure availability sets guide](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines) for more information.</span></span>

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

### <a name="create-virtual-machine"></a><span data-ttu-id="95662-124">Создание виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="95662-124">Create virtual machine</span></span>

<span data-ttu-id="95662-125">Создайте виртуальную машину с помощью команды [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="95662-125">Create a VM with the [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="95662-126">В следующем примере создаются 2 виртуальные машины — `myVM1` и `myVM2`,</span><span class="sxs-lookup"><span data-stu-id="95662-126">The following example creates 2 VMs named `myVM1` and `myVM2`.</span></span> <span data-ttu-id="95662-127">а также ключи SSH, если они еще не существуют в расположении ключей по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="95662-127">Creates SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="95662-128">Чтобы использовать определенный набор ключей, используйте параметр `--ssh-key-value`.</span><span class="sxs-lookup"><span data-stu-id="95662-128">To use a specific set of keys, use the `--ssh-key-value` option.</span></span>

<span data-ttu-id="95662-129">Создайте myVM1 (основная):</span><span class="sxs-lookup"><span data-stu-id="95662-129">Create myVM1 (primary)</span></span>
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

<span data-ttu-id="95662-130">После создания виртуальной машины в Azure CLI отображается информация, как показано ниже. Запишите значение `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="95662-130">Once the VM has been created, the Azure CLI shows information similar to the following example: Take note of the `publicIpAddress`.</span></span> <span data-ttu-id="95662-131">Этот адрес используется для доступа к виртуальной машине.</span><span class="sxs-lookup"><span data-stu-id="95662-131">This address is used to access the VM.</span></span>

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

<span data-ttu-id="95662-132">Создайте myVM2 (резервная):</span><span class="sxs-lookup"><span data-stu-id="95662-132">Create myVM2 (standby)</span></span>
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

<span data-ttu-id="95662-133">Также запишите значение `publicIpAddress` после его создания.</span><span class="sxs-lookup"><span data-stu-id="95662-133">Take note of the `publicIpAddress` as well once it created.</span></span>

### <a name="open-the-tcp-port-for-connectivity"></a><span data-ttu-id="95662-134">Открытие TCP-порта для возможности подключения</span><span class="sxs-lookup"><span data-stu-id="95662-134">Open the TCP port for connectivity</span></span>

<span data-ttu-id="95662-135">На этом шаге настраиваются внешние конечные точки, которые позволяют осуществлять удаленный доступ к базе данных Oracle. Вам нужно выполнить следующую команду.</span><span class="sxs-lookup"><span data-stu-id="95662-135">The step is to configure external endpoints, which allows accessing the Oracle DB remotely, you execute the following command.</span></span>

<span data-ttu-id="95662-136">Откройте порт для myVM1:</span><span class="sxs-lookup"><span data-stu-id="95662-136">Open port for myVM1</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVmN1SG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

<span data-ttu-id="95662-137">Результат должен выглядеть следующим образом.</span><span class="sxs-lookup"><span data-stu-id="95662-137">Result should look similar to the following response:</span></span>

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

<span data-ttu-id="95662-138">Откройте порт для myVM2:</span><span class="sxs-lookup"><span data-stu-id="95662-138">Open port for myVM2</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVm2N1SG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

### <a name="connect-to-virtual-machine"></a><span data-ttu-id="95662-139">Подключение к виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="95662-139">Connect to virtual machine</span></span>

<span data-ttu-id="95662-140">Используйте следующую команду для создания сеанса SSH с виртуальной машиной.</span><span class="sxs-lookup"><span data-stu-id="95662-140">Use the following command to create an SSH session with the virtual machine.</span></span> <span data-ttu-id="95662-141">Замените IP-адрес общедоступным IP-адресом виртуальной машины (значение `publicIpAddress`).</span><span class="sxs-lookup"><span data-stu-id="95662-141">Replace the IP address with the `publicIpAddress` of your virtual machine.</span></span>

```bash 
ssh azureuser@<publicIpAddress>
```

### <a name="create-database-on-myvm1-primary"></a><span data-ttu-id="95662-142">Создание базы данных на myVM1 (основная)</span><span class="sxs-lookup"><span data-stu-id="95662-142">Create Database on myVM1 (Primary)</span></span>

<span data-ttu-id="95662-143">Программное обеспечение Oracle уже установлено в образе Marketplace, поэтому следующим шагом является установка базы данных.</span><span class="sxs-lookup"><span data-stu-id="95662-143">The Oracle software is already installed on the Marketplace image, so the next step is to install the database.</span></span> <span data-ttu-id="95662-144">Сначала необходимо войти как суперпользователь oracle.</span><span class="sxs-lookup"><span data-stu-id="95662-144">the first step is running as the 'oracle' superuser.</span></span>

```bash
sudo su - oracle
```

<span data-ttu-id="95662-145">Создайте базу данных:</span><span class="sxs-lookup"><span data-stu-id="95662-145">create the database:</span></span>

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
<span data-ttu-id="95662-146">Результат должен выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="95662-146">Outputs should look similar to the following response:</span></span>

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

<span data-ttu-id="95662-147">Задайте переменные ORACLE_SID и ORACLE_HOME:</span><span class="sxs-lookup"><span data-stu-id="95662-147">Set the ORACLE_SID and ORACLE_HOME variables</span></span>

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=cdb1; export ORACLE_SID
```

<span data-ttu-id="95662-148">При необходимости можно добавить ORACLE_HOME и ORACLE_SID в файл BASHRC, чтобы эти параметры сохранились для последующих входов в систему.</span><span class="sxs-lookup"><span data-stu-id="95662-148">Optionally, You can added ORACLE_HOME and ORACLE_SID to the .bashrc file, so that these settings are saved for future logins.</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
```

## <a name="data-guard-configurations"></a><span data-ttu-id="95662-149">Настройка Data Guard</span><span class="sxs-lookup"><span data-stu-id="95662-149">Data Guard Configurations</span></span>

### <a name="enable-archive-log-mode-on-myvm1-primary"></a><span data-ttu-id="95662-150">Включение режима журнала архивирования на myVM1 (основная)</span><span class="sxs-lookup"><span data-stu-id="95662-150">Enable Archive log mode on myVM1 (primary)</span></span>

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
<span data-ttu-id="95662-151">Включите принудительное ведение журнала и убедитесь, что имеется хотя бы один файл журнала:</span><span class="sxs-lookup"><span data-stu-id="95662-151">Enable force logging, and make sure at least one logfile is present.</span></span>

```bash
SQL> ALTER DATABASE FORCE LOGGING;
SQL> ALTER SYSTEM SWITCH LOGFILE;
```

<span data-ttu-id="95662-152">Создайте резервные журналы повторяемых операций:</span><span class="sxs-lookup"><span data-stu-id="95662-152">Create standby redo logs</span></span>

```bash
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo01.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo02.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo03.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo04.log') SIZE 50M;
```

<span data-ttu-id="95662-153">Включите переключение базы данных (в результате чего восстановление начнется намного раньше) и задайте для параметра STANDBY_FILE_MANAGEMENT значение AUTO:</span><span class="sxs-lookup"><span data-stu-id="95662-153">Turn on Flashback (which made the recovery a lot earlier) and set STANDBY_FILE_MANAGEMENT to auto</span></span>

```bash
SQL> ALTER DATABASE FLASHBACK ON;
SQL> ALTER SYSTEM SET STANDBY_FILE_MANAGEMENT=AUTO;
```

### <a name="service-setup-on-myvm1-primary"></a><span data-ttu-id="95662-154">Настройка службы на myVM1 (основная)</span><span class="sxs-lookup"><span data-stu-id="95662-154">Service setup on myVM1 (primary)</span></span>

<span data-ttu-id="95662-155">Измените файл tnsnames.ora, расположенный в папке $ORACLE_HOME\network\admin, или создайте его.</span><span class="sxs-lookup"><span data-stu-id="95662-155">Edit or create the tnsnames.ora file, which is located at $ORACLE_HOME\network\admin folder</span></span>

<span data-ttu-id="95662-156">Добавьте следующие записи:</span><span class="sxs-lookup"><span data-stu-id="95662-156">Add the following entries</span></span>

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

<span data-ttu-id="95662-157">Измените файл listener.ora, расположенный в папке $ORACLE_HOME\network\admin, или создайте его.</span><span class="sxs-lookup"><span data-stu-id="95662-157">Edit or create the listener.ora file, which is located at $ORACLE_HOME\network\admin folder</span></span>

<span data-ttu-id="95662-158">Добавьте следующие записи:</span><span class="sxs-lookup"><span data-stu-id="95662-158">Add the following entries</span></span>

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

<span data-ttu-id="95662-159">Запустите прослушиватель:</span><span class="sxs-lookup"><span data-stu-id="95662-159">Start the listener</span></span>

```bash
$ lsnrctl stop
$ lsnrctl start
```

### <a name="service-setup-on-myvm2-standby"></a><span data-ttu-id="95662-160">Настройка службы на myVM2 (резервная)</span><span class="sxs-lookup"><span data-stu-id="95662-160">Service setup on myVM2 (Standby)</span></span>

<span data-ttu-id="95662-161">Измените файл tnsnames.ora, расположенный в папке $ORACLE_HOME\network\admin, или создайте его.</span><span class="sxs-lookup"><span data-stu-id="95662-161">Edit or create the tnsnames.ora file, which is located at $ORACLE_HOME\network\admin folder</span></span>

<span data-ttu-id="95662-162">Добавьте следующие записи:</span><span class="sxs-lookup"><span data-stu-id="95662-162">Add the following entries</span></span>

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

<span data-ttu-id="95662-163">Измените файл listener.ora, расположенный в папке $ORACLE_HOME\network\admin, или создайте его.</span><span class="sxs-lookup"><span data-stu-id="95662-163">Edit or create the listener.ora file, which is located at $ORACLE_HOME\network\admin folder</span></span>

<span data-ttu-id="95662-164">Добавьте следующие записи:</span><span class="sxs-lookup"><span data-stu-id="95662-164">Add the following entries</span></span>

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

<span data-ttu-id="95662-165">Запустите прослушиватель:</span><span class="sxs-lookup"><span data-stu-id="95662-165">Start the listener</span></span>

```bash
$ lsnrctl stop
$ lsnrctl start
```

<span data-ttu-id="95662-166">Включите брокер Data Guard:</span><span class="sxs-lookup"><span data-stu-id="95662-166">Enable Data Guard Broker</span></span>
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```

### <a name="restore-database-to-myvm2-standby"></a><span data-ttu-id="95662-167">Восстановление базы данных на myVM2 (резервная)</span><span class="sxs-lookup"><span data-stu-id="95662-167">Restore database to myVM2 (Standby)</span></span>

<span data-ttu-id="95662-168">Создайте файл параметров /tmp/initcdb1_stby.ora со следующим содержимым:</span><span class="sxs-lookup"><span data-stu-id="95662-168">Create a parameter file '/tmp/initcdb1_stby.ora' with the followings contents</span></span>
```bash
*.db_name='cdb1'
```

<span data-ttu-id="95662-169">Создайте папки:</span><span class="sxs-lookup"><span data-stu-id="95662-169">Create folders</span></span>

```bash
mkdir -p /u01/app/oracle/oradata/cdb1/pdbseed
mkdir -p /u01/app/oracle/oradata/cdb1/pdb1
mkdir -p /u01/app/oracle/fast_recovery_area/cdb1
mkdir -p /u01/app/oracle/admin/cdb1/adump
```

<span data-ttu-id="95662-170">Создайте файл пароля:</span><span class="sxs-lookup"><span data-stu-id="95662-170">Create password file</span></span>

```bash
$ orapwd file=/u01/app/oracle/product/12.1.0.2/db_1/dbs/orapwcdb1 password=OraPasswd1 entries=10
```
<span data-ttu-id="95662-171">Запустите базу данных на myVM2:</span><span class="sxs-lookup"><span data-stu-id="95662-171">Start up database on myVM2</span></span>

```bash
$ export ORACLE_SID=cdb1
$ sqlplus / as sysdba

SQL> STARTUP NOMOUNT PFILE='/tmp/initcdb1_stby.ora';
SQL> EXIT;
```

<span data-ttu-id="95662-172">Восстановите базу данных с помощью служебной программы RMAN:</span><span class="sxs-lookup"><span data-stu-id="95662-172">Restore database using RMAN utility</span></span>

```bash
$ rman TARGET sys/OraPasswd1@cdb1 AUXILIARY sys/OraPasswd1@cdb1_stby
```

<span data-ttu-id="95662-173">Выполните следующие команды RMAN:</span><span class="sxs-lookup"><span data-stu-id="95662-173">Execute the following commands in RMAN</span></span>
```bash
DUPLICATE TARGET DATABASE
  FOR STANDBY
  FROM ACTIVE DATABASE
  DORECOVER
  SPFILE
    SET db_unique_name='CDB1_STBY' COMMENT 'Is standby'
  NOFILENAMECHECK;
```

<span data-ttu-id="95662-174">Включите брокер Data Guard:</span><span class="sxs-lookup"><span data-stu-id="95662-174">Enable Data Guard Broker</span></span>
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```

### <a name="configure-data-guard-broker-on-myvm1-primary"></a><span data-ttu-id="95662-175">Настройка брокера Data Guard на myVM1 (основная)</span><span class="sxs-lookup"><span data-stu-id="95662-175">Configure Data Guard broker on myVM1 (primary)</span></span>

<span data-ttu-id="95662-176">Запустите диспетчер Data Guard и войдите, используя SYS и пароль (не используйте проверку подлинности операционной системы).</span><span class="sxs-lookup"><span data-stu-id="95662-176">Start the Data Guard manager and login using SYS and password (do not using OS authentication).</span></span> <span data-ttu-id="95662-177">Выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="95662-177">Perform the followings</span></span>

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

<span data-ttu-id="95662-178">Проверьте конфигурацию:</span><span class="sxs-lookup"><span data-stu-id="95662-178">Review the configuration</span></span>
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

<span data-ttu-id="95662-179">Настройка Oracle Data Guard завершена.</span><span class="sxs-lookup"><span data-stu-id="95662-179">This completed the Oracle Data Guard setup.</span></span> <span data-ttu-id="95662-180">В следующем разделе показано, как проверить подключение и переключение.</span><span class="sxs-lookup"><span data-stu-id="95662-180">The next section shows you how to test the connectivity and switching over</span></span>

### <a name="connect-database-from-client-machine"></a><span data-ttu-id="95662-181">Подключение базы данных с клиентского компьютера</span><span class="sxs-lookup"><span data-stu-id="95662-181">Connect database from client machine</span></span>

<span data-ttu-id="95662-182">Обновите файл tnsnames.ora на клиентском компьютере, который обычно находится в папке $ORACLE_HOME\network\admin, или создайте его.</span><span class="sxs-lookup"><span data-stu-id="95662-182">Update or create the tnsnames.ora file on your client machine which usually is located at $ORACLE_HOME\network\admin.</span></span>

<span data-ttu-id="95662-183">Замените IP-адрес вашим `publicIpAddress` для myVM1 и myVM2:</span><span class="sxs-lookup"><span data-stu-id="95662-183">Replace the IP with your `publicIpAddress` for myVM1 and myVM2</span></span>

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

<span data-ttu-id="95662-184">Запустите sqlplus:</span><span class="sxs-lookup"><span data-stu-id="95662-184">Start sqlplus</span></span>

```bash
$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With the Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```
## <a name="test-data-guard-configuration"></a><span data-ttu-id="95662-185">Проверка конфигурации Data Guard</span><span class="sxs-lookup"><span data-stu-id="95662-185">Test Data Guard configuration</span></span>

### <a name="database-switchover-on-myvm1-primary"></a><span data-ttu-id="95662-186">Переключение базы данных на myVM1 (основная)</span><span class="sxs-lookup"><span data-stu-id="95662-186">Database switchover on myVM1 (primary)</span></span>

<span data-ttu-id="95662-187">Для переключения с базы данных-источника на резервную (с cdb1 на cdb1_stby):</span><span class="sxs-lookup"><span data-stu-id="95662-187">To switch from primary to standby (cdb1 to cdb1_stby)</span></span>

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

<span data-ttu-id="95662-188">Теперь вы можете подключиться к резервной базе данных:</span><span class="sxs-lookup"><span data-stu-id="95662-188">You should now be able to connect to the standby database</span></span>

<span data-ttu-id="95662-189">Запустите sqlplus:</span><span class="sxs-lookup"><span data-stu-id="95662-189">Start sqlplus</span></span>

```bash

$ sqlplus sys/OraPasswd1@cdb1_stby
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With the Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

### <a name="database-switch-back-on-myvm2-standby"></a><span data-ttu-id="95662-190">Переключение базы данных обратно на myVM2 (резервная)</span><span class="sxs-lookup"><span data-stu-id="95662-190">Database switch back on myVM2 (standby)</span></span>

<span data-ttu-id="95662-191">Чтобы переключиться обратно, выполните следующее на myVM2:</span><span class="sxs-lookup"><span data-stu-id="95662-191">To switch back, run the followings on myVM2</span></span>
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

<span data-ttu-id="95662-192">Опять же, теперь вы имеете возможность подключиться к базе данных-источнику.</span><span class="sxs-lookup"><span data-stu-id="95662-192">Once again, You should now be able to connect to the primary database</span></span>

<span data-ttu-id="95662-193">Запустите sqlplus:</span><span class="sxs-lookup"><span data-stu-id="95662-193">Start sqlplus</span></span>

```bash

$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With the Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

<span data-ttu-id="95662-194">Теперь вы завершили установку и настройку Data Guard на Oracle Linux.</span><span class="sxs-lookup"><span data-stu-id="95662-194">This completed the installation and configuration of Data Guard on Oracle linux.</span></span>


## <a name="delete-virtual-machine"></a><span data-ttu-id="95662-195">Удаление виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="95662-195">Delete virtual machine</span></span>

<span data-ttu-id="95662-196">Можно удалить ставшие ненужными группу ресурсов, виртуальную машину и все связанные с ней ресурсы, использовав следующую команду.</span><span class="sxs-lookup"><span data-stu-id="95662-196">When no longer needed, the following command can be used to remove the Resource Group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="95662-197">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="95662-197">Next steps</span></span>

<span data-ttu-id="95662-198">Изучите [руководство по созданию высокодоступных виртуальных машин](../../linux/create-cli-complete.md).</span><span class="sxs-lookup"><span data-stu-id="95662-198">[Create highly available virtual machines tutorial](../../linux/create-cli-complete.md)</span></span>

<span data-ttu-id="95662-199">[Изучите примеры развертывания виртуальных машин с помощью интерфейса командной строки](../../linux/cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="95662-199">[Explore VM deployment CLI samples](../../linux/cli-samples.md)</span></span>
