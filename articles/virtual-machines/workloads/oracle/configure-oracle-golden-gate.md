---
title: "aaaImplement Oracle золотые шлюза в виртуальной Машине Linux Azure | Документы Microsoft"
description: "Быстрое создание и запуск Oracle Golden Gate в среде Azure."
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
ms.date: 05/19/2017
ms.author: rclaus
ms.openlocfilehash: 320cafd5d23ee472f0af9f92577bc6f432f65778
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="implement-oracle-golden-gate-on-an-azure-linux-vm"></a><span data-ttu-id="9033a-103">Реализация Oracle Golden Gate на виртуальной машине Azure под управлением Linux</span><span class="sxs-lookup"><span data-stu-id="9033a-103">Implement Oracle Golden Gate on an Azure Linux VM</span></span> 

<span data-ttu-id="9033a-104">Hello Azure CLI — используется toocreate и управления ресурсами Azure hello командной строке или в сценариях.</span><span class="sxs-lookup"><span data-stu-id="9033a-104">hello Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="9033a-105">В этом руководстве рассматривается как toouse hello Azure CLI toodeploy Oracle 12c базы данных из коллекции образов Azure Marketplace hello.</span><span class="sxs-lookup"><span data-stu-id="9033a-105">This guide details how toouse hello Azure CLI toodeploy an Oracle 12c database from hello Azure Marketplace gallery image.</span></span> 

<span data-ttu-id="9033a-106">В данном документе описывается пошаговые как toocreate, установки и настройки шлюза золотые Oracle на Виртуальной машине Azure.</span><span class="sxs-lookup"><span data-stu-id="9033a-106">This document shows you step-by-step how toocreate, install, and configure Oracle Golden Gate on an Azure VM.</span></span>

<span data-ttu-id="9033a-107">Прежде чем начать, убедитесь, что hello Azure CLI был установлен.</span><span class="sxs-lookup"><span data-stu-id="9033a-107">Before you start, make sure that hello Azure CLI has been installed.</span></span> <span data-ttu-id="9033a-108">Дополнительные сведения см. в [руководстве по установке Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="9033a-108">For more information, see [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="prepare-hello-environment"></a><span data-ttu-id="9033a-109">Подготовка среды hello</span><span class="sxs-lookup"><span data-stu-id="9033a-109">Prepare hello environment</span></span>

<span data-ttu-id="9033a-110">Установка шлюза золотые Oracle tooperform hello, необходимо toocreate две виртуальные машины Azure на hello одной группе доступности.</span><span class="sxs-lookup"><span data-stu-id="9033a-110">tooperform hello Oracle Golden Gate installation, you need toocreate two Azure VMs on hello same availability set.</span></span> <span data-ttu-id="9033a-111">— использовать toocreate hello ВМ образа Marketplace Hello **Oracle: Oracle-базы данных-Ee:12.1.0.2:latest**.</span><span class="sxs-lookup"><span data-stu-id="9033a-111">hello Marketplace image you use toocreate hello VMs is **Oracle:Oracle-Database-Ee:12.1.0.2:latest**.</span></span>

<span data-ttu-id="9033a-112">Также требуется знание Unix редактор vi toobe и иметь базовое понимание x11 (X Windows).</span><span class="sxs-lookup"><span data-stu-id="9033a-112">You also need toobe familiar with Unix editor vi and have a basic understanding of x11 (X Windows).</span></span>

<span data-ttu-id="9033a-113">Hello ниже приводится сводка hello среды конфигурации:</span><span class="sxs-lookup"><span data-stu-id="9033a-113">hello following is a summary of hello environment configuration:</span></span>
> 
> |  | <span data-ttu-id="9033a-114">**Основной сайт**</span><span class="sxs-lookup"><span data-stu-id="9033a-114">**Primary site**</span></span> | <span data-ttu-id="9033a-115">**Сайт репликации**</span><span class="sxs-lookup"><span data-stu-id="9033a-115">**Replicate site**</span></span> |
> | --- | --- | --- |
> | <span data-ttu-id="9033a-116">**Версия Oracle**</span><span class="sxs-lookup"><span data-stu-id="9033a-116">**Oracle release**</span></span> |<span data-ttu-id="9033a-117">Версия 2 Oracle 12c — (12.1.0.2)</span><span class="sxs-lookup"><span data-stu-id="9033a-117">Oracle 12c Release 2 – (12.1.0.2)</span></span> |<span data-ttu-id="9033a-118">Версия 2 Oracle 12c — (12.1.0.2)</span><span class="sxs-lookup"><span data-stu-id="9033a-118">Oracle 12c Release 2 – (12.1.0.2)</span></span>|
> | <span data-ttu-id="9033a-119">**Имя компьютера**</span><span class="sxs-lookup"><span data-stu-id="9033a-119">**Machine name**</span></span> |<span data-ttu-id="9033a-120">myVM1</span><span class="sxs-lookup"><span data-stu-id="9033a-120">myVM1</span></span> |<span data-ttu-id="9033a-121">myVM2</span><span class="sxs-lookup"><span data-stu-id="9033a-121">myVM2</span></span> |
> | <span data-ttu-id="9033a-122">**Операционная система**</span><span class="sxs-lookup"><span data-stu-id="9033a-122">**Operating system**</span></span> |<span data-ttu-id="9033a-123">Oracle Linux 6.x</span><span class="sxs-lookup"><span data-stu-id="9033a-123">Oracle Linux 6.x</span></span> |<span data-ttu-id="9033a-124">Oracle Linux 6.x</span><span class="sxs-lookup"><span data-stu-id="9033a-124">Oracle Linux 6.x</span></span> |
> | <span data-ttu-id="9033a-125">**ИД безопасности Oracle**</span><span class="sxs-lookup"><span data-stu-id="9033a-125">**Oracle SID**</span></span> |<span data-ttu-id="9033a-126">CDB1</span><span class="sxs-lookup"><span data-stu-id="9033a-126">CDB1</span></span> |<span data-ttu-id="9033a-127">CDB1</span><span class="sxs-lookup"><span data-stu-id="9033a-127">CDB1</span></span> |
> | <span data-ttu-id="9033a-128">**Схема репликации**</span><span class="sxs-lookup"><span data-stu-id="9033a-128">**Replication schema**</span></span> |<span data-ttu-id="9033a-129">TEST</span><span class="sxs-lookup"><span data-stu-id="9033a-129">TEST</span></span>|<span data-ttu-id="9033a-130">TEST</span><span class="sxs-lookup"><span data-stu-id="9033a-130">TEST</span></span> |
> | <span data-ttu-id="9033a-131">**Владелец/репликация Golden Gate**</span><span class="sxs-lookup"><span data-stu-id="9033a-131">**Golden Gate owner/replicate**</span></span> |<span data-ttu-id="9033a-132">C##GGADMIN</span><span class="sxs-lookup"><span data-stu-id="9033a-132">C##GGADMIN</span></span> |<span data-ttu-id="9033a-133">REPUSER</span><span class="sxs-lookup"><span data-stu-id="9033a-133">REPUSER</span></span> |
> | <span data-ttu-id="9033a-134">**Процесс Golden Gate**</span><span class="sxs-lookup"><span data-stu-id="9033a-134">**Golden Gate process**</span></span> |<span data-ttu-id="9033a-135">EXTORA</span><span class="sxs-lookup"><span data-stu-id="9033a-135">EXTORA</span></span> |<span data-ttu-id="9033a-136">REPORA</span><span class="sxs-lookup"><span data-stu-id="9033a-136">REPORA</span></span>|


### <a name="sign-in-tooazure"></a><span data-ttu-id="9033a-137">Войдите в tooAzure</span><span class="sxs-lookup"><span data-stu-id="9033a-137">Sign in tooAzure</span></span> 

<span data-ttu-id="9033a-138">Войдите в подписку Azure совместно с hello tooyour [входа az](/cli/azure/#login) команды.</span><span class="sxs-lookup"><span data-stu-id="9033a-138">Sign in tooyour Azure subscription with hello [az login](/cli/azure/#login) command.</span></span> <span data-ttu-id="9033a-139">Затем выполните hello на экране инструкциям.</span><span class="sxs-lookup"><span data-stu-id="9033a-139">Then follow hello on-screen directions.</span></span>

```azurecli
az login
```

### <a name="create-a-resource-group"></a><span data-ttu-id="9033a-140">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="9033a-140">Create a resource group</span></span>

<span data-ttu-id="9033a-141">Создание группы ресурсов с hello [Создание группы az](/cli/azure/group#create) команды.</span><span class="sxs-lookup"><span data-stu-id="9033a-141">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="9033a-142">Группа ресурсов Azure является логическим контейнером, в котором происходит развертывание ресурсов Azure и управление ими.</span><span class="sxs-lookup"><span data-stu-id="9033a-142">An Azure resource group is a logical container into which Azure resources are deployed and from which they can be managed.</span></span> 

<span data-ttu-id="9033a-143">Hello следующий пример создает группу ресурсов с именем `myResourceGroup` в hello `westus` расположение.</span><span class="sxs-lookup"><span data-stu-id="9033a-143">hello following example creates a resource group named `myResourceGroup` in hello `westus` location.</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

### <a name="create-an-availability-set"></a><span data-ttu-id="9033a-144">Создать группу доступности</span><span class="sxs-lookup"><span data-stu-id="9033a-144">Create an availability set</span></span>

<span data-ttu-id="9033a-145">Привет, даст необязательно, но рекомендуется.</span><span class="sxs-lookup"><span data-stu-id="9033a-145">hello following step is optional but recommended.</span></span> <span data-ttu-id="9033a-146">Дополнительные сведения см. в статье [Рекомендации по группам доступности Azure для виртуальных машин Windows](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).</span><span class="sxs-lookup"><span data-stu-id="9033a-146">For more information, see [Azure availability sets guide](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).</span></span>

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

### <a name="create-a-virtual-machine"></a><span data-ttu-id="9033a-147">Создание виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="9033a-147">Create a virtual machine</span></span>

<span data-ttu-id="9033a-148">Создайте виртуальную Машину с hello [создания виртуальной машины az](/cli/azure/vm#create) команды.</span><span class="sxs-lookup"><span data-stu-id="9033a-148">Create a VM with hello [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="9033a-149">Hello следующий пример создает две виртуальные машины с именем `myVM1` и `myVM2`.</span><span class="sxs-lookup"><span data-stu-id="9033a-149">hello following example creates two VMs named `myVM1` and `myVM2`.</span></span> <span data-ttu-id="9033a-150">а также ключи SSH, если они еще не существуют в расположении ключей по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="9033a-150">Create SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="9033a-151">toouse конкретный набор ключей, используйте hello `--ssh-key-value` параметр.</span><span class="sxs-lookup"><span data-stu-id="9033a-151">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>

#### <a name="create-myvm1-primary"></a><span data-ttu-id="9033a-152">Создайте myVM1 (основная):</span><span class="sxs-lookup"><span data-stu-id="9033a-152">Create myVM1 (primary):</span></span>
```azurecli
az vm create \
     --resource-group myResourceGroup \
     --name myVM1 \
     --availability-set myAvailabilitySet \
     --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
     --size Standard_DS1_v2  \
     --generate-ssh-keys \
```

<span data-ttu-id="9033a-153">После hello создания виртуальной Машины hello Azure CLI показано toohello аналогичные сведения, следующий пример.</span><span class="sxs-lookup"><span data-stu-id="9033a-153">After hello VM has been created, hello Azure CLI shows information similar toohello following example.</span></span> <span data-ttu-id="9033a-154">(Обратите внимание hello `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="9033a-154">(Take note of hello `publicIpAddress`.</span></span> <span data-ttu-id="9033a-155">Этот адрес будет hello используется tooaccess виртуальной Машины.)</span><span class="sxs-lookup"><span data-stu-id="9033a-155">This address is used tooaccess hello VM.)</span></span>

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

#### <a name="create-myvm2-replicate"></a><span data-ttu-id="9033a-156">Создайте myVM2 (репликация):</span><span class="sxs-lookup"><span data-stu-id="9033a-156">Create myVM2 (replicate):</span></span>
```azurecli
az vm create \
     --resource-group myResourceGroup \
     --name myVM2 \
     --availability-set myAvailabilitySet \
     --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
     --size Standard_DS1_v2  \
     --generate-ssh-keys \
```

<span data-ttu-id="9033a-157">Запишите hello `publicIpAddress` также после его создания.</span><span class="sxs-lookup"><span data-stu-id="9033a-157">Take note of hello `publicIpAddress` as well after it has been created.</span></span>

### <a name="open-hello-tcp-port-for-connectivity"></a><span data-ttu-id="9033a-158">Привет открыть TCP-порт для подключения к</span><span class="sxs-lookup"><span data-stu-id="9033a-158">Open hello TCP port for connectivity</span></span>

<span data-ttu-id="9033a-159">Hello следующим шагом является tooconfigure внешних конечных точек, которые позволяют базы данных Oracle hello tooaccess удаленно.</span><span class="sxs-lookup"><span data-stu-id="9033a-159">hello next step is tooconfigure external endpoints,  which enable you tooaccess hello Oracle database remotely.</span></span> <span data-ttu-id="9033a-160">tooconfigure hello внешние конечные точки, запустите следующие команды hello.</span><span class="sxs-lookup"><span data-stu-id="9033a-160">tooconfigure hello external endpoints, run hello following commands.</span></span>

#### <a name="open-hello-port-for-myvm1"></a><span data-ttu-id="9033a-161">Откройте порт hello для myVM1:</span><span class="sxs-lookup"><span data-stu-id="9033a-161">Open hello port for myVM1:</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVm1NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

<span data-ttu-id="9033a-162">Hello результаты должны выглядеть примерно toohello следующий ответ:</span><span class="sxs-lookup"><span data-stu-id="9033a-162">hello results should look similar toohello following response:</span></span>

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

#### <a name="open-hello-port-for-myvm2"></a><span data-ttu-id="9033a-163">Откройте порт hello для myVM2:</span><span class="sxs-lookup"><span data-stu-id="9033a-163">Open hello port for myVM2:</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVm2NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

### <a name="connect-toohello-virtual-machine"></a><span data-ttu-id="9033a-164">Подключение toohello виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="9033a-164">Connect toohello virtual machine</span></span>

<span data-ttu-id="9033a-165">Используйте hello следующая команда toocreate сеанс SSH с виртуальной машиной hello.</span><span class="sxs-lookup"><span data-stu-id="9033a-165">Use hello following command toocreate an SSH session with hello virtual machine.</span></span> <span data-ttu-id="9033a-166">Замените hello hello IP-адрес `publicIpAddress` вашей виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="9033a-166">Replace hello IP address with hello `publicIpAddress` of your virtual machine.</span></span>

```bash 
ssh <publicIpAddress>
```

### <a name="create-hello-database-on-myvm1-primary"></a><span data-ttu-id="9033a-167">Создать hello базы данных на myVM1 (основной)</span><span class="sxs-lookup"><span data-stu-id="9033a-167">Create hello database on myVM1 (primary)</span></span>

<span data-ttu-id="9033a-168">Hello программное обеспечение Oracle уже установлен на образа Marketplace hello, поэтому hello следующим шагом является база данных tooinstall hello.</span><span class="sxs-lookup"><span data-stu-id="9033a-168">hello Oracle software is already installed on hello Marketplace image, so hello next step is tooinstall hello database.</span></span> 

<span data-ttu-id="9033a-169">Запустите программное обеспечение hello как суперпользователь «oracle» hello:</span><span class="sxs-lookup"><span data-stu-id="9033a-169">Run hello software as hello 'oracle' superuser:</span></span>

```bash
sudo su - oracle
```

<span data-ttu-id="9033a-170">Создайте базу данных hello:</span><span class="sxs-lookup"><span data-stu-id="9033a-170">Create hello database:</span></span>

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
<span data-ttu-id="9033a-171">Выходные данные должен выглядеть примерно toohello следующий ответ:</span><span class="sxs-lookup"><span data-stu-id="9033a-171">Outputs should look similar toohello following response:</span></span>

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
Look at hello log file "/u01/app/oracle/cfgtoollogs/dbca/cdb1/cdb1.log" for more details.
```

<span data-ttu-id="9033a-172">Установка переменных ORACLE_SID и ORACLE_HOME hello.</span><span class="sxs-lookup"><span data-stu-id="9033a-172">Set hello ORACLE_SID and ORACLE_HOME variables.</span></span>

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=gg1; export ORACLE_SID
$ LD_LIBRARY_PATH=ORACLE_HOME/lib; export LD_LIBRARY_PATH
```

<span data-ttu-id="9033a-173">При необходимости можно добавить ORACLE_HOME и ORACLE_SID файла toohello .bashrc, чтобы эти параметры сохраняются для будущих входа в систему:</span><span class="sxs-lookup"><span data-stu-id="9033a-173">Optionally, you can add ORACLE_HOME and ORACLE_SID toohello .bashrc file, so that these settings are saved for future sign-ins:</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=gg1
# add Oracle library path
export LD_LIBRARY_PATH=$ORACLE_HOME/lib
```

### <a name="start-oracle-listener"></a><span data-ttu-id="9033a-174">Запуск прослушивателя Oracle</span><span class="sxs-lookup"><span data-stu-id="9033a-174">Start Oracle listener</span></span>
```bash
$ sudo su - oracle
$ lsnrctl start
```

### <a name="create-hello-database-on-myvm2-replicate"></a><span data-ttu-id="9033a-175">Создание базы данных hello на myVM2 (репликация)</span><span class="sxs-lookup"><span data-stu-id="9033a-175">Create hello database on myVM2 (replicate)</span></span>

```bash
sudo su - oracle
```
<span data-ttu-id="9033a-176">Создайте базу данных hello:</span><span class="sxs-lookup"><span data-stu-id="9033a-176">Create hello database:</span></span>

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
<span data-ttu-id="9033a-177">Установка переменных ORACLE_SID и ORACLE_HOME hello.</span><span class="sxs-lookup"><span data-stu-id="9033a-177">Set hello ORACLE_SID and ORACLE_HOME variables.</span></span>

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=cdb1; export ORACLE_SID
$ LD_LIBRARY_PATH=ORACLE_HOME/lib; export LD_LIBRARY_PATH
```

<span data-ttu-id="9033a-178">При необходимости можно добавлены ORACLE_HOME и ORACLE_SID toohello .bashrc файла, чтобы эти параметры сохраняются для будущих входа в систему.</span><span class="sxs-lookup"><span data-stu-id="9033a-178">Optionally, you can added ORACLE_HOME and ORACLE_SID toohello .bashrc file, so that these settings are saved for future sign-ins.</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
# add Oracle library path
export LD_LIBRARY_PATH=$ORACLE_HOME/lib
```

### <a name="start-oracle-listener"></a><span data-ttu-id="9033a-179">Запуск прослушивателя Oracle</span><span class="sxs-lookup"><span data-stu-id="9033a-179">Start Oracle listener</span></span>
```bash
$ sudo su - oracle
$ lsnrctl start
```

## <a name="configure-golden-gate"></a><span data-ttu-id="9033a-180">Настройка Golden Gate</span><span class="sxs-lookup"><span data-stu-id="9033a-180">Configure Golden Gate</span></span> 
<span data-ttu-id="9033a-181">tooconfigure золотые шлюзом, примите меры hello в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="9033a-181">tooconfigure Golden Gate, take hello steps in this section.</span></span>

### <a name="enable-archive-log-mode-on-myvm1-primary"></a><span data-ttu-id="9033a-182">Включение режима журнала архивирования на myVM1 (основная)</span><span class="sxs-lookup"><span data-stu-id="9033a-182">Enable archive log mode on myVM1 (primary)</span></span>

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
<span data-ttu-id="9033a-183">Включите принудительное ведение журнала и убедитесь, что есть хотя бы один файл журнала.</span><span class="sxs-lookup"><span data-stu-id="9033a-183">Enable force logging, and make sure at least one log file is present.</span></span>

```bash
SQL> ALTER DATABASE FORCE LOGGING;
SQL> ALTER SYSTEM SWITCH LOGFILE;
SQL> ALTER SYSTEM set enable_goldengate_replication=true;
SQL> ALTER PLUGGABLE DATABASE PDB1 OPEN;
SQL> ALTER SESSION SET CONTAINER=PDB1;
SQL> ALTER DATABASE ADD SUPPLEMENTAL LOG DATA;
SQL> EXIT;
```

### <a name="download-golden-gate-software"></a><span data-ttu-id="9033a-184">Загрузка программного обеспечения Golden Gate</span><span class="sxs-lookup"><span data-stu-id="9033a-184">Download Golden Gate software</span></span>
<span data-ttu-id="9033a-185">toodownload и подготовки программного обеспечения Oracle золотые шлюза hello, полный hello, следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="9033a-185">toodownload and prepare hello Oracle Golden Gate software, complete hello following steps:</span></span>

1. <span data-ttu-id="9033a-186">Загрузите hello **fbo_ggs_Linux_x64_shiphome.zip** файл из hello [страницу скачивания шлюза золотые Oracle](http://www.oracle.com/technetwork/middleware/goldengate/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="9033a-186">Download hello **fbo_ggs_Linux_x64_shiphome.zip** file from hello [Oracle Golden Gate download page](http://www.oracle.com/technetwork/middleware/goldengate/downloads/index.html).</span></span> <span data-ttu-id="9033a-187">Разделе hello Загрузите заголовок **12.x.x.x Oracle GoldenGate для Oracle Linux x86-64**, должен быть набором toodownload файлы .zip.</span><span class="sxs-lookup"><span data-stu-id="9033a-187">Under hello download title **Oracle GoldenGate 12.x.x.x for Oracle Linux x86-64**, there should be a set of .zip files toodownload.</span></span>

2. <span data-ttu-id="9033a-188">После загрузки hello .zip файлы tooyour клиентского компьютера, используйте протокол Secure копии (SCP) toocopy hello файлы tooyour виртуальной Машины:</span><span class="sxs-lookup"><span data-stu-id="9033a-188">After you download hello .zip files tooyour client computer, use Secure Copy Protocol (SCP) toocopy hello files tooyour VM:</span></span>

  ```bash
  $ scp fbo_ggs_Linux_x64_shiphome.zip <publicIpAddress>:<folder>
  ```

3. <span data-ttu-id="9033a-189">Перемещение файлов toohello hello .zip **/ opt** папки.</span><span class="sxs-lookup"><span data-stu-id="9033a-189">Move hello .zip files toohello **/opt** folder.</span></span> <span data-ttu-id="9033a-190">Затем измените владельца hello hello файлов следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9033a-190">Then change hello owner of hello files as follows:</span></span>

  ```bash
  $ sudo su -
  # mv <folder>/*.zip /opt
  ```

4. <span data-ttu-id="9033a-191">Распакуйте файлы hello (hello установки Linux Распакуйте программы, если она еще не установлена):</span><span class="sxs-lookup"><span data-stu-id="9033a-191">Unzip hello files (install hello Linux unzip utility if it's not already installed):</span></span>

  ```bash
  # yum install unzip
  # cd /opt
  # unzip fbo_ggs_Linux_x64_shiphome.zip
  ```

5. <span data-ttu-id="9033a-192">Измените разрешение:</span><span class="sxs-lookup"><span data-stu-id="9033a-192">Change permission:</span></span>

  ```bash
  # chown -R oracle:oinstall /opt/fbo_ggs_Linux_x64_shiphome
  ```

### <a name="prepare-hello-client-and-vm-toorun-x11-for-windows-clients-only"></a><span data-ttu-id="9033a-193">Подготовить клиент hello и ВМ toorun x11 (только для клиентов Windows)</span><span class="sxs-lookup"><span data-stu-id="9033a-193">Prepare hello client and VM toorun x11 (for Windows clients only)</span></span>
<span data-ttu-id="9033a-194">Этот параметр является необязательным.</span><span class="sxs-lookup"><span data-stu-id="9033a-194">This is an optional step.</span></span> <span data-ttu-id="9033a-195">Если вы используете клиента Linux или уже установили x11, этот шаг можно пропустить.</span><span class="sxs-lookup"><span data-stu-id="9033a-195">You can skip this step if you are using a Linux client or already have x11 setup.</span></span>

1. <span data-ttu-id="9033a-196">Загрузите компьютер Windows tooyour PuTTY и Xming:</span><span class="sxs-lookup"><span data-stu-id="9033a-196">Download PuTTY and Xming tooyour Windows computer:</span></span>

  * <span data-ttu-id="9033a-197">[Скачать PuTTY](http://www.putty.org/).</span><span class="sxs-lookup"><span data-stu-id="9033a-197">[Download PuTTY](http://www.putty.org/)</span></span>
  * <span data-ttu-id="9033a-198">[Скачать Xming](https://xming.en.softonic.com/).</span><span class="sxs-lookup"><span data-stu-id="9033a-198">[Download Xming](https://xming.en.softonic.com/)</span></span>

2.  <span data-ttu-id="9033a-199">После установки PuTTY в hello PuTTY папку (например, C:\Program Files\PuTTY), запустите puttygen.exe (генератор ключа PuTTY).</span><span class="sxs-lookup"><span data-stu-id="9033a-199">After you install PuTTY, in hello PuTTY folder (for example, C:\Program Files\PuTTY), run puttygen.exe (PuTTY Key Generator).</span></span>

3.  <span data-ttu-id="9033a-200">В генераторе ключей PuTTY сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="9033a-200">In PuTTY Key Generator:</span></span>

  - <span data-ttu-id="9033a-201">toogenerate ключей, выберите hello **формирования** кнопки.</span><span class="sxs-lookup"><span data-stu-id="9033a-201">toogenerate a key, select hello **Generate** button.</span></span>
  - <span data-ttu-id="9033a-202">Скопируйте содержимое hello hello ключа (**Ctrl + C**).</span><span class="sxs-lookup"><span data-stu-id="9033a-202">Copy hello contents of hello key (**Ctrl+C**).</span></span>
  - <span data-ttu-id="9033a-203">Выберите hello **Сохранить закрытый ключ** кнопки.</span><span class="sxs-lookup"><span data-stu-id="9033a-203">Select hello **Save private key** button.</span></span>
  - <span data-ttu-id="9033a-204">Игнорируйте сообщения hello появится, а затем выберите **ОК**.</span><span class="sxs-lookup"><span data-stu-id="9033a-204">Ignore hello warning that appears, and then select **OK**.</span></span>

    ![Снимок экрана со страницей hello PuTTY генератор ключей](./media/oracle-golden-gate/puttykeygen.png)

4.  <span data-ttu-id="9033a-206">В виртуальной машине выполните следующие команды:</span><span class="sxs-lookup"><span data-stu-id="9033a-206">In your VM, run these commands:</span></span>

  ```bash
  # sudo su - oracle
  $ mkdir .ssh (if not already created)
  $ cd .ssh
  ```

5. <span data-ttu-id="9033a-207">Создайте файл с именем **authorized_keys**.</span><span class="sxs-lookup"><span data-stu-id="9033a-207">Create a file named **authorized_keys**.</span></span> <span data-ttu-id="9033a-208">Вставьте содержимое hello hello ключ в этом файле, а затем сохраните файл hello.</span><span class="sxs-lookup"><span data-stu-id="9033a-208">Paste hello contents of hello key in this file, and then save hello file.</span></span>

  > [!NOTE]
  > <span data-ttu-id="9033a-209">Hello ключ должен содержать строку hello `ssh-rsa`.</span><span class="sxs-lookup"><span data-stu-id="9033a-209">hello key must contain hello string `ssh-rsa`.</span></span> <span data-ttu-id="9033a-210">Кроме того содержимое hello hello ключа должно быть одну строку текста.</span><span class="sxs-lookup"><span data-stu-id="9033a-210">Also, hello contents of hello key must be a single line of text.</span></span>
  >  

6. <span data-ttu-id="9033a-211">Запустите PuTTY.</span><span class="sxs-lookup"><span data-stu-id="9033a-211">Start PuTTY.</span></span> <span data-ttu-id="9033a-212">В hello **категории** выберите **подключения** > **SSH** > **Auth**. В hello **файла закрытого ключа для проверки подлинности** поле, найдите toohello ключ, который был создан ранее.</span><span class="sxs-lookup"><span data-stu-id="9033a-212">In hello **Category** pane, select **Connection** > **SSH** > **Auth**. In hello **Private key file for authentication** box, browse toohello key that you generated earlier.</span></span>

  ![Снимок экрана со страницей hello задать закрытый ключ](./media/oracle-golden-gate/setprivatekey.png)

7. <span data-ttu-id="9033a-214">В hello **категории** выберите **подключения** > **SSH** > **X11**.</span><span class="sxs-lookup"><span data-stu-id="9033a-214">In hello **Category** pane, select **Connection** > **SSH** > **X11**.</span></span> <span data-ttu-id="9033a-215">Затем выберите hello **включить X11 пересылку** поле.</span><span class="sxs-lookup"><span data-stu-id="9033a-215">Then select hello **Enable X11 forwarding** box.</span></span>

  ![Снимок экрана со страницей Enable X11 hello](./media/oracle-golden-gate/enablex11.png)

8. <span data-ttu-id="9033a-217">В hello **категории** панели перейдите слишком**сеанса**.</span><span class="sxs-lookup"><span data-stu-id="9033a-217">In hello **Category** pane, go too**Session**.</span></span> <span data-ttu-id="9033a-218">Введите сведения об узле hello, а затем выберите **откройте**.</span><span class="sxs-lookup"><span data-stu-id="9033a-218">Enter hello host information, and then select **Open**.</span></span>

  ![Снимок экрана: страница приветствия сеанса](./media/oracle-golden-gate/puttysession.png)

### <a name="install-golden-gate-software"></a><span data-ttu-id="9033a-220">Установка программного обеспечения Golden Gate</span><span class="sxs-lookup"><span data-stu-id="9033a-220">Install Golden Gate software</span></span>

<span data-ttu-id="9033a-221">tooinstall шлюзом золотые Oracle, полный hello, следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="9033a-221">tooinstall Oracle Golden Gate, complete hello following steps:</span></span>

1. <span data-ttu-id="9033a-222">Выполните вход в качестве пользователя oracle.</span><span class="sxs-lookup"><span data-stu-id="9033a-222">Sign in as oracle.</span></span> <span data-ttu-id="9033a-223">(Вы должны иметь доступ toosign в без необходимости вводить пароль.) Убедитесь, что запущен Xming перед началом установки hello.</span><span class="sxs-lookup"><span data-stu-id="9033a-223">(You should be able toosign in without being prompted for a password.) Make sure that Xming is running before you begin hello installation.</span></span>
 
  ```bash
  $ cd /opt/fbo_ggs_Linux_x64_shiphome/Disk1
  $ ./runInstaller
  ```
2. <span data-ttu-id="9033a-224">Выберите Oracle GoldenGate for Oracle Database 12c (Oracle GoldenGate для базы данных Oracle 12c).</span><span class="sxs-lookup"><span data-stu-id="9033a-224">Select 'Oracle GoldenGate for Oracle Database 12c'.</span></span> <span data-ttu-id="9033a-225">Выберите **Далее** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="9033a-225">Then select **Next** toocontinue.</span></span>

  ![Снимок экрана: страница установки выберите установщик hello](./media/oracle-golden-gate/golden_gate_install_01.png)

3. <span data-ttu-id="9033a-227">Изменить расположение hello программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="9033a-227">Change hello software location.</span></span> <span data-ttu-id="9033a-228">Затем выберите hello **запустить диспетчер** и введите расположение базы данных hello.</span><span class="sxs-lookup"><span data-stu-id="9033a-228">Then select  hello **Start Manager** box and enter hello database location.</span></span> <span data-ttu-id="9033a-229">Выберите **Далее** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="9033a-229">Select **Next** toocontinue.</span></span>

  ![Снимок экрана: страница приветствия выберите установки](./media/oracle-golden-gate/golden_gate_install_02.png)

4. <span data-ttu-id="9033a-231">Измените каталог инвентаризации hello, а затем выберите **Далее** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="9033a-231">Change hello inventory directory, and then select **Next** toocontinue.</span></span>

  ![Снимок экрана: страница приветствия выберите установки](./media/oracle-golden-gate/golden_gate_install_03.png)

5. <span data-ttu-id="9033a-233">На hello **Сводка** выберите **установить** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="9033a-233">On hello **Summary** screen, select **Install** toocontinue.</span></span>

  ![Снимок экрана: страница установки выберите установщик hello](./media/oracle-golden-gate/golden_gate_install_04.png)

6. <span data-ttu-id="9033a-235">Запрос toorun сценарий может быть как «root».</span><span class="sxs-lookup"><span data-stu-id="9033a-235">You might be prompted toorun a script as 'root'.</span></span> <span data-ttu-id="9033a-236">В этом случае откройте отдельный сеанс, ssh toohello ВМ sudo tooroot и запустите сценарий hello.</span><span class="sxs-lookup"><span data-stu-id="9033a-236">If so, open a separate session, ssh toohello VM, sudo tooroot, and then run hello script.</span></span> <span data-ttu-id="9033a-237">Чтобы продолжить, нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="9033a-237">Select **OK** continue.</span></span>

  ![Снимок экрана: страница приветствия выберите установки](./media/oracle-golden-gate/golden_gate_install_05.png)

7. <span data-ttu-id="9033a-239">По завершении установки hello выберите **закрыть** toocomplete hello процесса.</span><span class="sxs-lookup"><span data-stu-id="9033a-239">When hello installation has finished, select **Close** toocomplete hello process.</span></span>

  ![Снимок экрана: страница приветствия выберите установки](./media/oracle-golden-gate/golden_gate_install_06.png)

### <a name="set-up-service-on-myvm1-primary"></a><span data-ttu-id="9033a-241">Настройка службы на myVM1 (основная)</span><span class="sxs-lookup"><span data-stu-id="9033a-241">Set up service on myVM1 (primary)</span></span>

1. <span data-ttu-id="9033a-242">Создать или обновить файл tnsnames.ora hello:</span><span class="sxs-lookup"><span data-stu-id="9033a-242">Create or update hello tnsnames.ora file:</span></span>

  ```bash
  $ cd $ORACLE_HOME/network/admin
  $ vi tnsnames.ora

  cdb1=
    (DESCRIPTION=
      (ADDRESS=
        (PROTOCOL=TCP)
        (HOST=localhost)
        (PORT=1521)
      )
      (CONNECT_DATA=
        (SERVER=dedicated)
        (SERVICE_NAME=cdb1)
      )
    )

  pdb1=
    (DESCRIPTION=
      (ADDRESS=
        (PROTOCOL=TCP)
        (HOST=localhost)
        (PORT=1521)
      )
      (CONNECT_DATA=
        (SERVER=dedicated)
        (SERVICE_NAME=pdb1)
      )
    )
  ```

2. <span data-ttu-id="9033a-243">Создайте hello шлюза золотые владельца и учетные записи пользователей.</span><span class="sxs-lookup"><span data-stu-id="9033a-243">Create hello Golden Gate owner and user accounts.</span></span>

  > [!NOTE]
  > <span data-ttu-id="9033a-244">Учетная запись владельца Hello должна иметь префикс C ##.</span><span class="sxs-lookup"><span data-stu-id="9033a-244">hello owner account must have C## prefix.</span></span>
  >

    ```bash
    $ sqlplus / as sysdba
    SQL> CREATE USER C##GGADMIN identified by ggadmin;
    SQL> EXEC dbms_goldengate_auth.grant_admin_privilege('C##GGADMIN',container=>'ALL');
    SQL> GRANT DBA tooC##GGADMIN container=all;
    SQL> connect C##GGADMIN/ggadmin
    SQL> ALTER SESSION SET CONTAINER=PDB1;
    SQL> EXIT;
    ```

3. <span data-ttu-id="9033a-245">Создайте шлюз золотые hello тестовую учетную запись пользователя:</span><span class="sxs-lookup"><span data-stu-id="9033a-245">Create hello Golden Gate test user account:</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ sqlplus system/OraPasswd1@pdb1
  SQL> CREATE USER test identified by test DEFAULT TABLESPACE USERS TEMPORARY TABLESPACE TEMP;
  SQL> GRANT connect, resource, dba tootest;
  SQL> ALTER USER test QUOTA 100M on USERS;
  SQL> connect test/test@pdb1
  SQL> @demo_ora_create
  SQL> @demo_ora_insert
  SQL> EXIT;
  ```

4. <span data-ttu-id="9033a-246">Настройте файл параметров извлечения hello.</span><span class="sxs-lookup"><span data-stu-id="9033a-246">Configure hello extract parameter file.</span></span>

 <span data-ttu-id="9033a-247">Запуск командной строки золотой шлюза hello (ggsci):</span><span class="sxs-lookup"><span data-stu-id="9033a-247">Start hello Golden gate command-line interface (ggsci):</span></span>

  ```bash
  $ sudo su - oracle
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  GGSCI> DBLOGIN USERID test@pdb1, PASSWORD test
  Successfully logged into database  pdb1
  GGSCI>  ADD SCHEMATRANDATA pdb1.test
  2017-05-23 15:44:25  INFO    OGG-01788  SCHEMATRANDATA has been added on schema test.
  2017-05-23 15:44:25  INFO    OGG-01976  SCHEMATRANDATA for scheduling columns has been added on schema test.

  GGSCI> EDIT PARAMS EXTORA
  ```
5. <span data-ttu-id="9033a-248">Добавьте следующий параметр ИЗВЛЕЧЬ toohello файлов (с помощью команды vi) hello.</span><span class="sxs-lookup"><span data-stu-id="9033a-248">Add hello following toohello EXTRACT parameter file (by using vi commands).</span></span> <span data-ttu-id="9033a-249">Нажмите клавишу ESC, ":wq!"</span><span class="sxs-lookup"><span data-stu-id="9033a-249">Press Esc key, ':wq!'</span></span> <span data-ttu-id="9033a-250">файл toosave.</span><span class="sxs-lookup"><span data-stu-id="9033a-250">toosave file.</span></span> 

  ```bash
  EXTRACT EXTORA
  USERID C##GGADMIN, PASSWORD ggadmin
  RMTHOST 10.0.0.5, MGRPORT 7809
  RMTTRAIL ./dirdat/rt  
  DDL INCLUDE MAPPED
  DDLOPTIONS REPORT 
  LOGALLSUPCOLS
  UPDATERECORDFORMAT COMPACT
  TABLE pdb1.test.TCUSTMER;
  TABLE pdb1.test.TCUSTORD;
  ```
6. <span data-ttu-id="9033a-251">Зарегистрируйте извлечение, интегрированное с помощью EXTRACT:</span><span class="sxs-lookup"><span data-stu-id="9033a-251">Register extract--integrated extract:</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci

  GGSCI> dblogin userid C##GGADMIN, password ggadmin
  Successfully logged into database CDB$ROOT.

  GGSCI> REGISTER EXTRACT EXTORA DATABASE CONTAINER(pdb1)

  2017-05-23 15:58:34  INFO    OGG-02003  Extract EXTORA successfully registered with database at SCN 1821260.

  GGSCI> exit
  ```
7. <span data-ttu-id="9033a-252">Настройте контрольные точки извлечения и запустите извлечение в режиме реального времени:</span><span class="sxs-lookup"><span data-stu-id="9033a-252">Set up extract checkpoints and start real-time extract:</span></span>

  ```bash
  $ ./ggsci
  GGSCI>  ADD EXTRACT EXTORA, INTEGRATED TRANLOG, BEGIN NOW
  EXTRACT (Integrated) added.

  GGSCI>  ADD RMTTRAIL ./dirdat/rt, EXTRACT EXTORA, MEGABYTES 10
  RMTTRAIL added.

  GGSCI>  START EXTRACT EXTORA

  Sending START request tooMANAGER ...
  EXTRACT EXTORA starting

  GGSCI > info all

  Program     Status      Group       Lag at Chkpt  Time Since Chkpt

  MANAGER     RUNNING
  EXTRACT     RUNNING     EXTORA      00:00:11      00:00:04
  ```
<span data-ttu-id="9033a-253">На этом шаге найти hello начиная уведомлений SCN, который будет использоваться позже в другом разделе:</span><span class="sxs-lookup"><span data-stu-id="9033a-253">In this step, you find hello starting SCN, which will be used later, in a different section:</span></span>

  ```bash
  $ sqlplus / as sysdba
  SQL> alter session set container = pdb1;
  SQL> SELECT current_scn from v$database;
  CURRENT_SCN
  -----------
      1857887
  SQL> EXIT;
  ```

  ```bash
  $ ./ggsci
  GGSCI> EDIT PARAMS INITEXT
  ```

  ```bash
  EXTRACT INITEXT
  USERID C##GGADMIN, PASSWORD ggadmin
  RMTHOST 10.0.0.5, MGRPORT 7809
  RMTTASK REPLICAT, GROUP INITREP
  TABLE pdb1.test.*, SQLPREDICATE 'AS OF SCN 1857887'; 
  ```

  ```bash
  GGSCI> ADD EXTRACT INITEXT, SOURCEISTABLE
  ```

### <a name="set-up-service-on-myvm2-replicate"></a><span data-ttu-id="9033a-254">Настройка службы на myVM2 (репликация)</span><span class="sxs-lookup"><span data-stu-id="9033a-254">Set up service on myVM2 (replicate)</span></span>


1. <span data-ttu-id="9033a-255">Создать или обновить файл tnsnames.ora hello:</span><span class="sxs-lookup"><span data-stu-id="9033a-255">Create or update hello tnsnames.ora file:</span></span>

  ```bash
  $ cd $ORACLE_HOME/network/admin
  $ vi tnsnames.ora

  cdb1=
    (DESCRIPTION=
      (ADDRESS=
        (PROTOCOL=TCP)
        (HOST=localhost)
        (PORT=1521)
      )
      (CONNECT_DATA=
        (SERVER=dedicated)
        (SERVICE_NAME=cdb1)
      )
    )

  pdb1=
    (DESCRIPTION=
      (ADDRESS=
        (PROTOCOL=TCP)
        (HOST=localhost)
        (PORT=1521)
      )
      (CONNECT_DATA=
        (SERVER=dedicated)
        (SERVICE_NAME=pdb1)
      )
    )
  ```

2. <span data-ttu-id="9033a-256">Создайте учетную запись репликации:</span><span class="sxs-lookup"><span data-stu-id="9033a-256">Create a replicate account:</span></span>

  ```bash
  $ sqlplus / as sysdba
  SQL> alter session set container = pdb1;
  SQL> create user repuser identified by rep_pass container=current;
  SQL> grant dba toorepuser;
  SQL> exec dbms_goldengate_auth.grant_admin_privilege('REPUSER',container=>'PDB1');
  SQL> connect repuser/rep_pass@pdb1 
  SQL> EXIT;
  ```

3. <span data-ttu-id="9033a-257">Создайте тестовую учетную запись пользователя Golden Gate:</span><span class="sxs-lookup"><span data-stu-id="9033a-257">Create a Golden Gate test user account:</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ sqlplus system/OraPasswd1@pdb1
  SQL> CREATE USER test identified by test DEFAULT TABLESPACE USERS TEMPORARY TABLESPACE TEMP;
  SQL> GRANT connect, resource, dba tootest;
  SQL> ALTER USER test QUOTA 100M on USERS;
  SQL> connect test/test@pdb1
  SQL> @demo_ora_create
  SQL> EXIT;
  ```

4. <span data-ttu-id="9033a-258">Изменения tooreplicate файл параметров REPLICAT:</span><span class="sxs-lookup"><span data-stu-id="9033a-258">REPLICAT parameter file tooreplicate changes:</span></span> 

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  GGSCI> EDIT PARAMS REPORA  
  ```
  <span data-ttu-id="9033a-259">Содержимое файла параметров REPORA:</span><span class="sxs-lookup"><span data-stu-id="9033a-259">Content of REPORA parameter file:</span></span>

  ```bash
  REPLICAT REPORA
  ASSUMETARGETDEFS
  DISCARDFILE ./dirrpt/repora.dsc, PURGE, MEGABYTES 100
  DDL INCLUDE MAPPED
  DDLOPTIONS REPORT
  DBOPTIONS INTEGRATEDPARAMS(parallelism 6)
  USERID repuser@pdb1, PASSWORD rep_pass
  MAP pdb1.test.*, TARGET pdb1.test.*;
  ```

5. <span data-ttu-id="9033a-260">Настройте контрольную точку репликации:</span><span class="sxs-lookup"><span data-stu-id="9033a-260">Set up a replicat checkpoint:</span></span>

  ```bash
  GGSCI> ADD REPLICAT REPORA, INTEGRATED, EXTTRAIL ./dirdat/rt
  GGSCI> EDIT PARAMS INITREP

  ```

  ```bash
  REPLICAT INITREP
  ASSUMETARGETDEFS
  DISCARDFILE ./dirrpt/tcustmer.dsc, APPEND
  USERID repuser@pdb1, PASSWORD rep_pass
  MAP pdb1.test.*, TARGET pdb1.test.*;   
  ```

  ```bash
  GGSCI> ADD REPLICAT INITREP, SPECIALRUN
  ```

### <a name="set-up-hello-replication-myvm1-and-myvm2"></a><span data-ttu-id="9033a-261">Настройка репликации hello (myVM1 и myVM2)</span><span class="sxs-lookup"><span data-stu-id="9033a-261">Set up hello replication (myVM1 and myVM2)</span></span>

#### <a name="1-set-up-hello-replication-on-myvm2-replicate"></a><span data-ttu-id="9033a-262">1. Настройка репликации hello на myVM2 (репликация)</span><span class="sxs-lookup"><span data-stu-id="9033a-262">1. Set up hello replication on myVM2 (replicate)</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  GGSCI> EDIT PARAMS MGR
  ```
<span data-ttu-id="9033a-263">Обновите файл hello hello следующее:</span><span class="sxs-lookup"><span data-stu-id="9033a-263">Update hello file with hello following:</span></span>

  ```bash
  PORT 7809
  ACCESSRULE, PROG *, IPADDR *, ALLOW
  ```
<span data-ttu-id="9033a-264">Затем перезапустите службу диспетчера hello:</span><span class="sxs-lookup"><span data-stu-id="9033a-264">Then restart hello Manager service:</span></span>

  ```bash
  GGSCI> STOP MGR
  GGSCI> START MGR
  GGSCI> EXIT
  ```

#### <a name="2-set-up-hello-replication-on-myvm1-primary"></a><span data-ttu-id="9033a-265">2. Настройка репликации hello на myVM1 (основной)</span><span class="sxs-lookup"><span data-stu-id="9033a-265">2. Set up hello replication on myVM1 (primary)</span></span>

<span data-ttu-id="9033a-266">Запуск начальной загрузки hello и проверьте наличие ошибок:</span><span class="sxs-lookup"><span data-stu-id="9033a-266">Start hello initial load and check for errors:</span></span>

```bash
$ cd /u01/app/oracle/product/12.1.0/oggcore_1
$ ./ggsci
GGSCI> START EXTRACT INITEXT
GGSCI> VIEW REPORT INITEXT
```
#### <a name="3-set-up-hello-replication-on-myvm2-replicate"></a><span data-ttu-id="9033a-267">3. Настройка репликации hello на myVM2 (репликация)</span><span class="sxs-lookup"><span data-stu-id="9033a-267">3. Set up hello replication on myVM2 (replicate)</span></span>

<span data-ttu-id="9033a-268">Изменить hello SCN номер с номером hello получен до:</span><span class="sxs-lookup"><span data-stu-id="9033a-268">Change hello SCN number with hello number you obtained before:</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  START REPLICAT REPORA, AFTERCSN 1857887
  ```
<span data-ttu-id="9033a-269">начало репликации Hello и протестируйте его путем вставки новых записей tooTEST таблиц.</span><span class="sxs-lookup"><span data-stu-id="9033a-269">hello replication has begun, and you can test it by inserting new records tooTEST tables.</span></span>


### <a name="view-job-status-and-troubleshooting"></a><span data-ttu-id="9033a-270">Просмотр состояния задания и устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="9033a-270">View job status and troubleshooting</span></span>

#### <a name="view-reports"></a><span data-ttu-id="9033a-271">Просмотр отчетов</span><span class="sxs-lookup"><span data-stu-id="9033a-271">View reports</span></span>
<span data-ttu-id="9033a-272">tooview сообщает myVM1, запустите следующие команды hello.</span><span class="sxs-lookup"><span data-stu-id="9033a-272">tooview reports on myVM1, run hello following commands:</span></span>

  ```bash
  GGSCI> VIEW REPORT EXTORA 
  ```
 
<span data-ttu-id="9033a-273">tooview сообщает myVM2, запустите следующие команды hello.</span><span class="sxs-lookup"><span data-stu-id="9033a-273">tooview reports on myVM2, run hello following commands:</span></span>

  ```bash
  GGSCI> VIEW REPORT REPORA
  ```

#### <a name="view-status-and-history"></a><span data-ttu-id="9033a-274">Просмотр сведений о состоянии и журналов</span><span class="sxs-lookup"><span data-stu-id="9033a-274">View status and history</span></span>
<span data-ttu-id="9033a-275">tooview состояние и журнал на myVM1, запустите hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="9033a-275">tooview status and history on myVM1, run hello following commands:</span></span>

  ```bash
  GGSCI> dblogin userid c##ggadmin, password ggadmin 
  GGSCI> INFO EXTRACT EXTORA, DETAIL
  ```

<span data-ttu-id="9033a-276">tooview состояние и журнал на myVM2, запустите hello, следующие команды:</span><span class="sxs-lookup"><span data-stu-id="9033a-276">tooview status and history on myVM2, run hello following commands:</span></span>

  ```bash
  GGSCI> dblogin userid repuser@pdb1 password rep_pass 
  GGSCI> INFO REP REPORA, DETAIL
  ```
<span data-ttu-id="9033a-277">На этом завершается hello установки и настройки шлюза золотые в Oracle linux.</span><span class="sxs-lookup"><span data-stu-id="9033a-277">This completes hello installation and configuration of Golden Gate on Oracle linux.</span></span>


## <a name="delete-hello-virtual-machine"></a><span data-ttu-id="9033a-278">Удалить виртуальную машину hello</span><span class="sxs-lookup"><span data-stu-id="9033a-278">Delete hello virtual machine</span></span>

<span data-ttu-id="9033a-279">Когда оно больше не нужно, может быть hello следующую команду, группа ресурсов используется tooremove hello, виртуальных Машин и все связанные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="9033a-279">When it's no longer needed, hello following command can be used tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="9033a-280">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9033a-280">Next steps</span></span>

<span data-ttu-id="9033a-281">Изучите [руководство по созданию высокодоступных виртуальных машин](../../linux/create-cli-complete.md).</span><span class="sxs-lookup"><span data-stu-id="9033a-281">[Create highly available virtual machines tutorial](../../linux/create-cli-complete.md)</span></span>

<span data-ttu-id="9033a-282">[Изучите примеры развертывания виртуальных машин с помощью интерфейса командной строки](../../linux/cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="9033a-282">[Explore VM deployment CLI samples](../../linux/cli-samples.md)</span></span>
