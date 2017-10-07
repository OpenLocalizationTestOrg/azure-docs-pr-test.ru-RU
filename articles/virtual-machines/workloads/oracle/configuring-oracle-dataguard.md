---
title: "aaaImplement Oracle Data Guard на виртуальной Машине Linux Azure | Документы Microsoft"
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
ms.openlocfilehash: 101196b2f50dfca64d3eb1b4be56ff0c108693e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="implement-oracle-data-guard-on-azure-linux-vm"></a><span data-ttu-id="ce9fa-103">Реализация Oracle Data Guard на виртуальной машине Azure под управлением Linux</span><span class="sxs-lookup"><span data-stu-id="ce9fa-103">Implement Oracle Data Guard on Azure Linux VM</span></span> 

<span data-ttu-id="ce9fa-104">Hello Azure CLI — используется toocreate и управления ресурсами Azure hello командной строке или в сценариях.</span><span class="sxs-lookup"><span data-stu-id="ce9fa-104">hello Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="ce9fa-105">В этом руководстве рассматривается использование hello Azure CLI toodeploy Oracle 12c базы данных из коллекции образов hello Marketplace.</span><span class="sxs-lookup"><span data-stu-id="ce9fa-105">This guide details using hello Azure CLI toodeploy an Oracle 12c Database from hello Marketplace gallery image.</span></span> <span data-ttu-id="ce9fa-106">После создания базы данных Oracle hello в этом документе показано, как пошаговое tooinstall и настроить Защитник данных на виртуальной Машине Azure.</span><span class="sxs-lookup"><span data-stu-id="ce9fa-106">Once hello Oracle database is created, this document shows you step-by-step how tooinstall and configure Data Guard on Azure VM.</span></span>

<span data-ttu-id="ce9fa-107">Прежде чем начать, убедитесь, что hello Azure CLI был установлен.</span><span class="sxs-lookup"><span data-stu-id="ce9fa-107">Before you start, make sure that hello Azure CLI has been installed.</span></span> <span data-ttu-id="ce9fa-108">Дополнительные сведения см. в [руководстве по установке Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="ce9fa-108">For more information, see [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="prepare-hello-environment"></a><span data-ttu-id="ce9fa-109">Подготовка среды hello</span><span class="sxs-lookup"><span data-stu-id="ce9fa-109">Prepare hello environment</span></span>
### <a name="assumptions"></a><span data-ttu-id="ce9fa-110">Предположения</span><span class="sxs-lookup"><span data-stu-id="ce9fa-110">Assumptions</span></span>

<span data-ttu-id="ce9fa-111">tooperform hello Oracle Data Guard установки, необходимо toocreate две виртуальные машины Azure на hello одной группе доступности.</span><span class="sxs-lookup"><span data-stu-id="ce9fa-111">tooperform hello Oracle Data Guard install, you need toocreate two Azure VMs on hello same availability set.</span></span> <span data-ttu-id="ce9fa-112">— использовать toocreate hello ВМ образа Marketplace Hello» Oracle: Oracle-базы данных-Ee:12.1.0.2:latest».</span><span class="sxs-lookup"><span data-stu-id="ce9fa-112">hello Marketplace image you use toocreate hello VMs is "Oracle:Oracle-Database-Ee:12.1.0.2:latest".</span></span>

<span data-ttu-id="ce9fa-113">Hello основной виртуальной Машины (myVM1) имеет работающего экземпляра Oracle.</span><span class="sxs-lookup"><span data-stu-id="ce9fa-113">hello primary VM (myVM1) has a running Oracle instance.</span></span>

<span data-ttu-id="ce9fa-114">Здравствуйте, резервной ВМ (myVM2) имеет только установлено программное обеспечение Oracle hello.</span><span class="sxs-lookup"><span data-stu-id="ce9fa-114">hello standby VM (myVM2) has hello Oracle software installed only.</span></span>

### <a name="log-in-tooazure"></a><span data-ttu-id="ce9fa-115">Войдите в tooAzure</span><span class="sxs-lookup"><span data-stu-id="ce9fa-115">Log in tooAzure</span></span> 

<span data-ttu-id="ce9fa-116">Войдите в подписку Azure совместно с hello tooyour [входа az](/cli/azure/#login) команды и выполните hello на экране инструкциям.</span><span class="sxs-lookup"><span data-stu-id="ce9fa-116">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span>

```azurecli
az login
```

### <a name="create-a-resource-group"></a><span data-ttu-id="ce9fa-117">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="ce9fa-117">Create a resource group</span></span>

<span data-ttu-id="ce9fa-118">Создание группы ресурсов с hello [Создание группы az](/cli/azure/group#create) команды.</span><span class="sxs-lookup"><span data-stu-id="ce9fa-118">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="ce9fa-119">Группа ресурсов Azure является логическим контейнером, в котором происходит развертывание ресурсов Azure и управление ими.</span><span class="sxs-lookup"><span data-stu-id="ce9fa-119">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="ce9fa-120">Hello следующий пример создает группу ресурсов с именем `myResourceGroup` в hello `westus` расположение.</span><span class="sxs-lookup"><span data-stu-id="ce9fa-120">hello following example creates a resource group named `myResourceGroup` in hello `westus` location.</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

### <a name="create-availability-set"></a><span data-ttu-id="ce9fa-121">Создание группы доступности</span><span class="sxs-lookup"><span data-stu-id="ce9fa-121">Create availability set</span></span>

<span data-ttu-id="ce9fa-122">Этот шаг необязателен, но мы советуем его выполнить.</span><span class="sxs-lookup"><span data-stu-id="ce9fa-122">This step is optional, but is recommended.</span></span> <span data-ttu-id="ce9fa-123">Дополнительные сведения см. в статье [Рекомендации по группам доступности Azure для виртуальных машин Windows](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).</span><span class="sxs-lookup"><span data-stu-id="ce9fa-123">see [Azure availability sets guide](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines) for more information.</span></span>

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

### <a name="create-virtual-machine"></a><span data-ttu-id="ce9fa-124">Создание виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="ce9fa-124">Create virtual machine</span></span>

<span data-ttu-id="ce9fa-125">Создайте виртуальную Машину с hello [создания виртуальной машины az](/cli/azure/vm#create) команды.</span><span class="sxs-lookup"><span data-stu-id="ce9fa-125">Create a VM with hello [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="ce9fa-126">Hello следующий пример создает 2 виртуальные машины с именем `myVM1` и `myVM2`.</span><span class="sxs-lookup"><span data-stu-id="ce9fa-126">hello following example creates 2 VMs named `myVM1` and `myVM2`.</span></span> <span data-ttu-id="ce9fa-127">а также ключи SSH, если они еще не существуют в расположении ключей по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="ce9fa-127">Creates SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="ce9fa-128">toouse конкретный набор ключей, используйте hello `--ssh-key-value` параметр.</span><span class="sxs-lookup"><span data-stu-id="ce9fa-128">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>

<span data-ttu-id="ce9fa-129">Создайте myVM1 (основная):</span><span class="sxs-lookup"><span data-stu-id="ce9fa-129">Create myVM1 (primary)</span></span>
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

<span data-ttu-id="ce9fa-130">Один раз hello, будет создана виртуальная машина, hello Azure CLI показано toohello аналогичные сведения, следующий пример: внимание Take hello `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="ce9fa-130">Once hello VM has been created, hello Azure CLI shows information similar toohello following example: Take note of hello `publicIpAddress`.</span></span> <span data-ttu-id="ce9fa-131">Этот адрес будет hello используется tooaccess виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="ce9fa-131">This address is used tooaccess hello VM.</span></span>

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

<span data-ttu-id="ce9fa-132">Создайте myVM2 (резервная):</span><span class="sxs-lookup"><span data-stu-id="ce9fa-132">Create myVM2 (standby)</span></span>
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

<span data-ttu-id="ce9fa-133">Запишите hello `publicIpAddress` также после его создания.</span><span class="sxs-lookup"><span data-stu-id="ce9fa-133">Take note of hello `publicIpAddress` as well once it created.</span></span>

### <a name="open-hello-tcp-port-for-connectivity"></a><span data-ttu-id="ce9fa-134">Привет открыть TCP-порт для подключения к</span><span class="sxs-lookup"><span data-stu-id="ce9fa-134">Open hello TCP port for connectivity</span></span>

<span data-ttu-id="ce9fa-135">шаг Hello tooconfigure внешние конечные точки, разрешающее удаленный доступ к hello база данных Oracle, выполните следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="ce9fa-135">hello step is tooconfigure external endpoints, which allows accessing hello Oracle DB remotely, you execute hello following command.</span></span>

<span data-ttu-id="ce9fa-136">Откройте порт для myVM1:</span><span class="sxs-lookup"><span data-stu-id="ce9fa-136">Open port for myVM1</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVmN1SG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

<span data-ttu-id="ce9fa-137">Результат должен выглядеть примерно toohello следующий ответ:</span><span class="sxs-lookup"><span data-stu-id="ce9fa-137">Result should look similar toohello following response:</span></span>

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

<span data-ttu-id="ce9fa-138">Откройте порт для myVM2:</span><span class="sxs-lookup"><span data-stu-id="ce9fa-138">Open port for myVM2</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVm2N1SG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

### <a name="connect-toovirtual-machine"></a><span data-ttu-id="ce9fa-139">Подключиться к компьютеру toovirtual</span><span class="sxs-lookup"><span data-stu-id="ce9fa-139">Connect toovirtual machine</span></span>

<span data-ttu-id="ce9fa-140">Используйте hello следующая команда toocreate сеанс SSH с виртуальной машиной hello.</span><span class="sxs-lookup"><span data-stu-id="ce9fa-140">Use hello following command toocreate an SSH session with hello virtual machine.</span></span> <span data-ttu-id="ce9fa-141">Замените hello hello IP-адрес `publicIpAddress` вашей виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="ce9fa-141">Replace hello IP address with hello `publicIpAddress` of your virtual machine.</span></span>

```bash 
ssh azureuser@<publicIpAddress>
```

### <a name="create-database-on-myvm1-primary"></a><span data-ttu-id="ce9fa-142">Создание базы данных на myVM1 (основная)</span><span class="sxs-lookup"><span data-stu-id="ce9fa-142">Create Database on myVM1 (Primary)</span></span>

<span data-ttu-id="ce9fa-143">Hello программное обеспечение Oracle уже установлен на образа Marketplace hello, поэтому hello следующим шагом является база данных tooinstall hello.</span><span class="sxs-lookup"><span data-stu-id="ce9fa-143">hello Oracle software is already installed on hello Marketplace image, so hello next step is tooinstall hello database.</span></span> <span data-ttu-id="ce9fa-144">Первым шагом Hello работает как суперпользователь «oracle» hello.</span><span class="sxs-lookup"><span data-stu-id="ce9fa-144">hello first step is running as hello 'oracle' superuser.</span></span>

```bash
sudo su - oracle
```

<span data-ttu-id="ce9fa-145">Создайте базу данных hello:</span><span class="sxs-lookup"><span data-stu-id="ce9fa-145">create hello database:</span></span>

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
<span data-ttu-id="ce9fa-146">Выходные данные должен выглядеть примерно toohello следующий ответ:</span><span class="sxs-lookup"><span data-stu-id="ce9fa-146">Outputs should look similar toohello following response:</span></span>

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

<span data-ttu-id="ce9fa-147">Установка переменных ORACLE_SID и ORACLE_HOME hello</span><span class="sxs-lookup"><span data-stu-id="ce9fa-147">Set hello ORACLE_SID and ORACLE_HOME variables</span></span>

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=cdb1; export ORACLE_SID
```

<span data-ttu-id="ce9fa-148">При необходимости можно добавлены ORACLE_HOME и ORACLE_SID toohello .bashrc файла, чтобы эти параметры сохраняются для будущих подключений.</span><span class="sxs-lookup"><span data-stu-id="ce9fa-148">Optionally, You can added ORACLE_HOME and ORACLE_SID toohello .bashrc file, so that these settings are saved for future logins.</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
```

## <a name="data-guard-configurations"></a><span data-ttu-id="ce9fa-149">Настройка Data Guard</span><span class="sxs-lookup"><span data-stu-id="ce9fa-149">Data Guard Configurations</span></span>

### <a name="enable-archive-log-mode-on-myvm1-primary"></a><span data-ttu-id="ce9fa-150">Включение режима журнала архивирования на myVM1 (основная)</span><span class="sxs-lookup"><span data-stu-id="ce9fa-150">Enable Archive log mode on myVM1 (primary)</span></span>

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
<span data-ttu-id="ce9fa-151">Включите принудительное ведение журнала и убедитесь, что имеется хотя бы один файл журнала:</span><span class="sxs-lookup"><span data-stu-id="ce9fa-151">Enable force logging, and make sure at least one logfile is present.</span></span>

```bash
SQL> ALTER DATABASE FORCE LOGGING;
SQL> ALTER SYSTEM SWITCH LOGFILE;
```

<span data-ttu-id="ce9fa-152">Создайте резервные журналы повторяемых операций:</span><span class="sxs-lookup"><span data-stu-id="ce9fa-152">Create standby redo logs</span></span>

```bash
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo01.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo02.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo03.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo04.log') SIZE 50M;
```

<span data-ttu-id="ce9fa-153">Включить переключение обратно (который сделан восстановления hello намного раньше) и задайте STANDBY_FILE_MANAGEMENT tooauto</span><span class="sxs-lookup"><span data-stu-id="ce9fa-153">Turn on Flashback (which made hello recovery a lot earlier) and set STANDBY_FILE_MANAGEMENT tooauto</span></span>

```bash
SQL> ALTER DATABASE FLASHBACK ON;
SQL> ALTER SYSTEM SET STANDBY_FILE_MANAGEMENT=AUTO;
```

### <a name="service-setup-on-myvm1-primary"></a><span data-ttu-id="ce9fa-154">Настройка службы на myVM1 (основная)</span><span class="sxs-lookup"><span data-stu-id="ce9fa-154">Service setup on myVM1 (primary)</span></span>

<span data-ttu-id="ce9fa-155">Изменить или создать файл tnsnames.ora hello, который расположен в папке $ORACLE_HOME\network\admin</span><span class="sxs-lookup"><span data-stu-id="ce9fa-155">Edit or create hello tnsnames.ora file, which is located at $ORACLE_HOME\network\admin folder</span></span>

<span data-ttu-id="ce9fa-156">Добавить следующие записи hello</span><span class="sxs-lookup"><span data-stu-id="ce9fa-156">Add hello following entries</span></span>

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

<span data-ttu-id="ce9fa-157">Изменить или создать файл listener.ora hello, который расположен в папке $ORACLE_HOME\network\admin</span><span class="sxs-lookup"><span data-stu-id="ce9fa-157">Edit or create hello listener.ora file, which is located at $ORACLE_HOME\network\admin folder</span></span>

<span data-ttu-id="ce9fa-158">Добавить следующие записи hello</span><span class="sxs-lookup"><span data-stu-id="ce9fa-158">Add hello following entries</span></span>

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

<span data-ttu-id="ce9fa-159">Запуск прослушивателя hello</span><span class="sxs-lookup"><span data-stu-id="ce9fa-159">Start hello listener</span></span>

```bash
$ lsnrctl stop
$ lsnrctl start
```

### <a name="service-setup-on-myvm2-standby"></a><span data-ttu-id="ce9fa-160">Настройка службы на myVM2 (резервная)</span><span class="sxs-lookup"><span data-stu-id="ce9fa-160">Service setup on myVM2 (Standby)</span></span>

<span data-ttu-id="ce9fa-161">Изменить или создать файл tnsnames.ora hello, который расположен в папке $ORACLE_HOME\network\admin</span><span class="sxs-lookup"><span data-stu-id="ce9fa-161">Edit or create hello tnsnames.ora file, which is located at $ORACLE_HOME\network\admin folder</span></span>

<span data-ttu-id="ce9fa-162">Добавить следующие записи hello</span><span class="sxs-lookup"><span data-stu-id="ce9fa-162">Add hello following entries</span></span>

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

<span data-ttu-id="ce9fa-163">Изменить или создать файл listener.ora hello, который расположен в папке $ORACLE_HOME\network\admin</span><span class="sxs-lookup"><span data-stu-id="ce9fa-163">Edit or create hello listener.ora file, which is located at $ORACLE_HOME\network\admin folder</span></span>

<span data-ttu-id="ce9fa-164">Добавить следующие записи hello</span><span class="sxs-lookup"><span data-stu-id="ce9fa-164">Add hello following entries</span></span>

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

<span data-ttu-id="ce9fa-165">Запуск прослушивателя hello</span><span class="sxs-lookup"><span data-stu-id="ce9fa-165">Start hello listener</span></span>

```bash
$ lsnrctl stop
$ lsnrctl start
```

<span data-ttu-id="ce9fa-166">Включите брокер Data Guard:</span><span class="sxs-lookup"><span data-stu-id="ce9fa-166">Enable Data Guard Broker</span></span>
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```

### <a name="restore-database-toomyvm2-standby"></a><span data-ttu-id="ce9fa-167">Восстановление базы данных toomyVM2 (Standby)</span><span class="sxs-lookup"><span data-stu-id="ce9fa-167">Restore database toomyVM2 (Standby)</span></span>

<span data-ttu-id="ce9fa-168">Создайте файл параметров "/ tmp/initcdb1_stby.ora" с содержимым hello следующие действия</span><span class="sxs-lookup"><span data-stu-id="ce9fa-168">Create a parameter file '/tmp/initcdb1_stby.ora' with hello followings contents</span></span>
```bash
*.db_name='cdb1'
```

<span data-ttu-id="ce9fa-169">Создайте папки:</span><span class="sxs-lookup"><span data-stu-id="ce9fa-169">Create folders</span></span>

```bash
mkdir -p /u01/app/oracle/oradata/cdb1/pdbseed
mkdir -p /u01/app/oracle/oradata/cdb1/pdb1
mkdir -p /u01/app/oracle/fast_recovery_area/cdb1
mkdir -p /u01/app/oracle/admin/cdb1/adump
```

<span data-ttu-id="ce9fa-170">Создайте файл пароля:</span><span class="sxs-lookup"><span data-stu-id="ce9fa-170">Create password file</span></span>

```bash
$ orapwd file=/u01/app/oracle/product/12.1.0.2/db_1/dbs/orapwcdb1 password=OraPasswd1 entries=10
```
<span data-ttu-id="ce9fa-171">Запустите базу данных на myVM2:</span><span class="sxs-lookup"><span data-stu-id="ce9fa-171">Start up database on myVM2</span></span>

```bash
$ export ORACLE_SID=cdb1
$ sqlplus / as sysdba

SQL> STARTUP NOMOUNT PFILE='/tmp/initcdb1_stby.ora';
SQL> EXIT;
```

<span data-ttu-id="ce9fa-172">Восстановите базу данных с помощью служебной программы RMAN:</span><span class="sxs-lookup"><span data-stu-id="ce9fa-172">Restore database using RMAN utility</span></span>

```bash
$ rman TARGET sys/OraPasswd1@cdb1 AUXILIARY sys/OraPasswd1@cdb1_stby
```

<span data-ttu-id="ce9fa-173">Выполните следующие команды в RMAN hello</span><span class="sxs-lookup"><span data-stu-id="ce9fa-173">Execute hello following commands in RMAN</span></span>
```bash
DUPLICATE TARGET DATABASE
  FOR STANDBY
  FROM ACTIVE DATABASE
  DORECOVER
  SPFILE
    SET db_unique_name='CDB1_STBY' COMMENT 'Is standby'
  NOFILENAMECHECK;
```

<span data-ttu-id="ce9fa-174">Включите брокер Data Guard:</span><span class="sxs-lookup"><span data-stu-id="ce9fa-174">Enable Data Guard Broker</span></span>
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```

### <a name="configure-data-guard-broker-on-myvm1-primary"></a><span data-ttu-id="ce9fa-175">Настройка брокера Data Guard на myVM1 (основная)</span><span class="sxs-lookup"><span data-stu-id="ce9fa-175">Configure Data Guard broker on myVM1 (primary)</span></span>

<span data-ttu-id="ce9fa-176">Запустите диспетчер Data Guard hello и имя входа с помощью SYS и пароль (вы не используете проверку подлинности операционной системы).</span><span class="sxs-lookup"><span data-stu-id="ce9fa-176">Start hello Data Guard manager and login using SYS and password (do not using OS authentication).</span></span> <span data-ttu-id="ce9fa-177">Выполните следующие действия hello</span><span class="sxs-lookup"><span data-stu-id="ce9fa-177">Perform hello followings</span></span>

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

<span data-ttu-id="ce9fa-178">Проверить настройку hello</span><span class="sxs-lookup"><span data-stu-id="ce9fa-178">Review hello configuration</span></span>
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

<span data-ttu-id="ce9fa-179">Это действие выполнить установки Oracle Data Guard hello.</span><span class="sxs-lookup"><span data-stu-id="ce9fa-179">This completed hello Oracle Data Guard setup.</span></span> <span data-ttu-id="ce9fa-180">Hello следующем разделе показано, как tootest hello подключения и выполняется переключение</span><span class="sxs-lookup"><span data-stu-id="ce9fa-180">hello next section shows you how tootest hello connectivity and switching over</span></span>

### <a name="connect-database-from-client-machine"></a><span data-ttu-id="ce9fa-181">Подключение базы данных с клиентского компьютера</span><span class="sxs-lookup"><span data-stu-id="ce9fa-181">Connect database from client machine</span></span>

<span data-ttu-id="ce9fa-182">Обновить или создать файл tnsnames.ora hello на компьютере клиента, которая обычно находится в $ORACLE_HOME\network\admin.</span><span class="sxs-lookup"><span data-stu-id="ce9fa-182">Update or create hello tnsnames.ora file on your client machine which usually is located at $ORACLE_HOME\network\admin.</span></span>

<span data-ttu-id="ce9fa-183">Замените hello IP-адрес с вашей `publicIpAddress` myVM1 и myVM2</span><span class="sxs-lookup"><span data-stu-id="ce9fa-183">Replace hello IP with your `publicIpAddress` for myVM1 and myVM2</span></span>

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

<span data-ttu-id="ce9fa-184">Запустите sqlplus:</span><span class="sxs-lookup"><span data-stu-id="ce9fa-184">Start sqlplus</span></span>

```bash
$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```
## <a name="test-data-guard-configuration"></a><span data-ttu-id="ce9fa-185">Проверка конфигурации Data Guard</span><span class="sxs-lookup"><span data-stu-id="ce9fa-185">Test Data Guard configuration</span></span>

### <a name="database-switchover-on-myvm1-primary"></a><span data-ttu-id="ce9fa-186">Переключение базы данных на myVM1 (основная)</span><span class="sxs-lookup"><span data-stu-id="ce9fa-186">Database switchover on myVM1 (primary)</span></span>

<span data-ttu-id="ce9fa-187">tooswitch из первичного toostandby (cdb1 toocdb1_stby)</span><span class="sxs-lookup"><span data-stu-id="ce9fa-187">tooswitch from primary toostandby (cdb1 toocdb1_stby)</span></span>

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

<span data-ttu-id="ce9fa-188">Теперь вы должны может tooconnect резервной toohello базы данных.</span><span class="sxs-lookup"><span data-stu-id="ce9fa-188">You should now be able tooconnect toohello standby database</span></span>

<span data-ttu-id="ce9fa-189">Запустите sqlplus:</span><span class="sxs-lookup"><span data-stu-id="ce9fa-189">Start sqlplus</span></span>

```bash

$ sqlplus sys/OraPasswd1@cdb1_stby
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

### <a name="database-switch-back-on-myvm2-standby"></a><span data-ttu-id="ce9fa-190">Переключение базы данных обратно на myVM2 (резервная)</span><span class="sxs-lookup"><span data-stu-id="ce9fa-190">Database switch back on myVM2 (standby)</span></span>

<span data-ttu-id="ce9fa-191">tooswitch обратно, выполнить следующие действия hello на myVM2</span><span class="sxs-lookup"><span data-stu-id="ce9fa-191">tooswitch back, run hello followings on myVM2</span></span>
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

<span data-ttu-id="ce9fa-192">Опять же можно будет tooconnect toohello базы данных-источника</span><span class="sxs-lookup"><span data-stu-id="ce9fa-192">Once again, You should now be able tooconnect toohello primary database</span></span>

<span data-ttu-id="ce9fa-193">Запустите sqlplus:</span><span class="sxs-lookup"><span data-stu-id="ce9fa-193">Start sqlplus</span></span>

```bash

$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

<span data-ttu-id="ce9fa-194">Это действие выполнить hello установку и настройку защиты данных в Oracle linux.</span><span class="sxs-lookup"><span data-stu-id="ce9fa-194">This completed hello installation and configuration of Data Guard on Oracle linux.</span></span>


## <a name="delete-virtual-machine"></a><span data-ttu-id="ce9fa-195">Удаление виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="ce9fa-195">Delete virtual machine</span></span>

<span data-ttu-id="ce9fa-196">Когда отпадает необходимость hello следующую команду может быть используется tooremove hello группы ресурсов виртуальной Машины, и все связанные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="ce9fa-196">When no longer needed, hello following command can be used tooremove hello Resource Group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="ce9fa-197">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ce9fa-197">Next steps</span></span>

<span data-ttu-id="ce9fa-198">Изучите [руководство по созданию высокодоступных виртуальных машин](../../linux/create-cli-complete.md).</span><span class="sxs-lookup"><span data-stu-id="ce9fa-198">[Create highly available virtual machines tutorial](../../linux/create-cli-complete.md)</span></span>

<span data-ttu-id="ce9fa-199">[Изучите примеры развертывания виртуальных машин с помощью интерфейса командной строки](../../linux/cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="ce9fa-199">[Explore VM deployment CLI samples](../../linux/cli-samples.md)</span></span>
