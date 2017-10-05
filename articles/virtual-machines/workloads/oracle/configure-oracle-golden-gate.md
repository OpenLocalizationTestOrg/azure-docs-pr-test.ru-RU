---
title: "Реализация Oracle Golden Gate на виртуальной машине Azure под управлением Linux | Документация Майкрософт"
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
ms.openlocfilehash: a05711357d345267647c02e42336fd37c09e1bff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="implement-oracle-golden-gate-on-an-azure-linux-vm"></a><span data-ttu-id="e7c8a-103">Реализация Oracle Golden Gate на виртуальной машине Azure под управлением Linux</span><span class="sxs-lookup"><span data-stu-id="e7c8a-103">Implement Oracle Golden Gate on an Azure Linux VM</span></span> 

<span data-ttu-id="e7c8a-104">Azure CLI используется для создания ресурсов Azure и управления ими из командной строки или с помощью скриптов.</span><span class="sxs-lookup"><span data-stu-id="e7c8a-104">The Azure CLI is used to create and manage Azure resources from the command line or in scripts.</span></span> <span data-ttu-id="e7c8a-105">В этом руководстве описывается, как с помощью Azure CLI развернуть базу данных Oracle 12c, используя образ из коллекции Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="e7c8a-105">This guide details how to use the Azure CLI to deploy an Oracle 12c database from the Azure Marketplace gallery image.</span></span> 

<span data-ttu-id="e7c8a-106">В этом документе демонстрируется пошаговое создание, установка и настройка Oracle Golden Gate на виртуальной машине Azure.</span><span class="sxs-lookup"><span data-stu-id="e7c8a-106">This document shows you step-by-step how to create, install, and configure Oracle Golden Gate on an Azure VM.</span></span>

<span data-ttu-id="e7c8a-107">Перед началом работы убедитесь, что вы установили Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="e7c8a-107">Before you start, make sure that the Azure CLI has been installed.</span></span> <span data-ttu-id="e7c8a-108">Дополнительные сведения см. в [руководстве по установке Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e7c8a-108">For more information, see [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="prepare-the-environment"></a><span data-ttu-id="e7c8a-109">Подготовка среды</span><span class="sxs-lookup"><span data-stu-id="e7c8a-109">Prepare the environment</span></span>

<span data-ttu-id="e7c8a-110">Чтобы выполнить установку Oracle Golden Gate, вам необходимо создать две виртуальные машины Azure в одной и той же группе доступности.</span><span class="sxs-lookup"><span data-stu-id="e7c8a-110">To perform the Oracle Golden Gate installation, you need to create two Azure VMs on the same availability set.</span></span> <span data-ttu-id="e7c8a-111">Образ Marketplace, который вы будете использовать для создания виртуальных машин, — **Oracle:Oracle-Database-Ee:12.1.0.2:latest**.</span><span class="sxs-lookup"><span data-stu-id="e7c8a-111">The Marketplace image you use to create the VMs is **Oracle:Oracle-Database-Ee:12.1.0.2:latest**.</span></span>

<span data-ttu-id="e7c8a-112">Кроме того, необходимо уметь работать с редактором Unix и иметь базовое представление об x11 (X Windows).</span><span class="sxs-lookup"><span data-stu-id="e7c8a-112">You also need to be familiar with Unix editor vi and have a basic understanding of x11 (X Windows).</span></span>

<span data-ttu-id="e7c8a-113">Ниже приводится сводка конфигурации среды.</span><span class="sxs-lookup"><span data-stu-id="e7c8a-113">The following is a summary of the environment configuration:</span></span>
> 
> |  | <span data-ttu-id="e7c8a-114">**Основной сайт**</span><span class="sxs-lookup"><span data-stu-id="e7c8a-114">**Primary site**</span></span> | <span data-ttu-id="e7c8a-115">**Сайт репликации**</span><span class="sxs-lookup"><span data-stu-id="e7c8a-115">**Replicate site**</span></span> |
> | --- | --- | --- |
> | <span data-ttu-id="e7c8a-116">**Версия Oracle**</span><span class="sxs-lookup"><span data-stu-id="e7c8a-116">**Oracle release**</span></span> |<span data-ttu-id="e7c8a-117">Версия 2 Oracle 12c — (12.1.0.2)</span><span class="sxs-lookup"><span data-stu-id="e7c8a-117">Oracle 12c Release 2 – (12.1.0.2)</span></span> |<span data-ttu-id="e7c8a-118">Версия 2 Oracle 12c — (12.1.0.2)</span><span class="sxs-lookup"><span data-stu-id="e7c8a-118">Oracle 12c Release 2 – (12.1.0.2)</span></span>|
> | <span data-ttu-id="e7c8a-119">**Имя компьютера**</span><span class="sxs-lookup"><span data-stu-id="e7c8a-119">**Machine name**</span></span> |<span data-ttu-id="e7c8a-120">myVM1</span><span class="sxs-lookup"><span data-stu-id="e7c8a-120">myVM1</span></span> |<span data-ttu-id="e7c8a-121">myVM2</span><span class="sxs-lookup"><span data-stu-id="e7c8a-121">myVM2</span></span> |
> | <span data-ttu-id="e7c8a-122">**Операционная система**</span><span class="sxs-lookup"><span data-stu-id="e7c8a-122">**Operating system**</span></span> |<span data-ttu-id="e7c8a-123">Oracle Linux 6.x</span><span class="sxs-lookup"><span data-stu-id="e7c8a-123">Oracle Linux 6.x</span></span> |<span data-ttu-id="e7c8a-124">Oracle Linux 6.x</span><span class="sxs-lookup"><span data-stu-id="e7c8a-124">Oracle Linux 6.x</span></span> |
> | <span data-ttu-id="e7c8a-125">**ИД безопасности Oracle**</span><span class="sxs-lookup"><span data-stu-id="e7c8a-125">**Oracle SID**</span></span> |<span data-ttu-id="e7c8a-126">CDB1</span><span class="sxs-lookup"><span data-stu-id="e7c8a-126">CDB1</span></span> |<span data-ttu-id="e7c8a-127">CDB1</span><span class="sxs-lookup"><span data-stu-id="e7c8a-127">CDB1</span></span> |
> | <span data-ttu-id="e7c8a-128">**Схема репликации**</span><span class="sxs-lookup"><span data-stu-id="e7c8a-128">**Replication schema**</span></span> |<span data-ttu-id="e7c8a-129">TEST</span><span class="sxs-lookup"><span data-stu-id="e7c8a-129">TEST</span></span>|<span data-ttu-id="e7c8a-130">TEST</span><span class="sxs-lookup"><span data-stu-id="e7c8a-130">TEST</span></span> |
> | <span data-ttu-id="e7c8a-131">**Владелец/репликация Golden Gate**</span><span class="sxs-lookup"><span data-stu-id="e7c8a-131">**Golden Gate owner/replicate**</span></span> |<span data-ttu-id="e7c8a-132">C##GGADMIN</span><span class="sxs-lookup"><span data-stu-id="e7c8a-132">C##GGADMIN</span></span> |<span data-ttu-id="e7c8a-133">REPUSER</span><span class="sxs-lookup"><span data-stu-id="e7c8a-133">REPUSER</span></span> |
> | <span data-ttu-id="e7c8a-134">**Процесс Golden Gate**</span><span class="sxs-lookup"><span data-stu-id="e7c8a-134">**Golden Gate process**</span></span> |<span data-ttu-id="e7c8a-135">EXTORA</span><span class="sxs-lookup"><span data-stu-id="e7c8a-135">EXTORA</span></span> |<span data-ttu-id="e7c8a-136">REPORA</span><span class="sxs-lookup"><span data-stu-id="e7c8a-136">REPORA</span></span>|


### <a name="sign-in-to-azure"></a><span data-ttu-id="e7c8a-137">Вход в Azure</span><span class="sxs-lookup"><span data-stu-id="e7c8a-137">Sign in to Azure</span></span> 

<span data-ttu-id="e7c8a-138">Войдите в подписку Azure, используя команду [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="e7c8a-138">Sign in to your Azure subscription with the [az login](/cli/azure/#login) command.</span></span> <span data-ttu-id="e7c8a-139">Затем выполните инструкции на экране.</span><span class="sxs-lookup"><span data-stu-id="e7c8a-139">Then follow the on-screen directions.</span></span>

```azurecli
az login
```

### <a name="create-a-resource-group"></a><span data-ttu-id="e7c8a-140">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="e7c8a-140">Create a resource group</span></span>

<span data-ttu-id="e7c8a-141">Создайте группу ресурсов с помощью команды [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="e7c8a-141">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="e7c8a-142">Группа ресурсов Azure является логическим контейнером, в котором происходит развертывание ресурсов Azure и управление ими.</span><span class="sxs-lookup"><span data-stu-id="e7c8a-142">An Azure resource group is a logical container into which Azure resources are deployed and from which they can be managed.</span></span> 

<span data-ttu-id="e7c8a-143">В следующем примере создается группа ресурсов с именем `myResourceGroup` в расположении `westus`.</span><span class="sxs-lookup"><span data-stu-id="e7c8a-143">The following example creates a resource group named `myResourceGroup` in the `westus` location.</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

### <a name="create-an-availability-set"></a><span data-ttu-id="e7c8a-144">"Создать группу доступности"</span><span class="sxs-lookup"><span data-stu-id="e7c8a-144">Create an availability set</span></span>

<span data-ttu-id="e7c8a-145">Следующий шаг необязателен, но мы рекомендуем его выполнить.</span><span class="sxs-lookup"><span data-stu-id="e7c8a-145">The following step is optional but recommended.</span></span> <span data-ttu-id="e7c8a-146">Дополнительные сведения см. в статье [Рекомендации по группам доступности Azure для виртуальных машин Windows](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).</span><span class="sxs-lookup"><span data-stu-id="e7c8a-146">For more information, see [Azure availability sets guide](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).</span></span>

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

### <a name="create-a-virtual-machine"></a><span data-ttu-id="e7c8a-147">Создание виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="e7c8a-147">Create a virtual machine</span></span>

<span data-ttu-id="e7c8a-148">Создайте виртуальную машину с помощью команды [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="e7c8a-148">Create a VM with the [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="e7c8a-149">В следующем примере создаются две виртуальные машины — `myVM1` и `myVM2`,</span><span class="sxs-lookup"><span data-stu-id="e7c8a-149">The following example creates two VMs named `myVM1` and `myVM2`.</span></span> <span data-ttu-id="e7c8a-150">а также ключи SSH, если они еще не существуют в расположении ключей по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="e7c8a-150">Create SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="e7c8a-151">Чтобы использовать определенный набор ключей, используйте параметр `--ssh-key-value`.</span><span class="sxs-lookup"><span data-stu-id="e7c8a-151">To use a specific set of keys, use the `--ssh-key-value` option.</span></span>

#### <a name="create-myvm1-primary"></a><span data-ttu-id="e7c8a-152">Создайте myVM1 (основная):</span><span class="sxs-lookup"><span data-stu-id="e7c8a-152">Create myVM1 (primary):</span></span>
```azurecli
az vm create \
     --resource-group myResourceGroup \
     --name myVM1 \
     --availability-set myAvailabilitySet \
     --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
     --size Standard_DS1_v2  \
     --generate-ssh-keys \
```

<span data-ttu-id="e7c8a-153">После создания виртуальной машины в Azure CLI отображается информация следующего вида.</span><span class="sxs-lookup"><span data-stu-id="e7c8a-153">After the VM has been created, the Azure CLI shows information similar to the following example.</span></span> <span data-ttu-id="e7c8a-154">(Запишите значение `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="e7c8a-154">(Take note of the `publicIpAddress`.</span></span> <span data-ttu-id="e7c8a-155">Этот адрес используется для доступа к виртуальной машине.)</span><span class="sxs-lookup"><span data-stu-id="e7c8a-155">This address is used to access the VM.)</span></span>

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

#### <a name="create-myvm2-replicate"></a><span data-ttu-id="e7c8a-156">Создайте myVM2 (репликация):</span><span class="sxs-lookup"><span data-stu-id="e7c8a-156">Create myVM2 (replicate):</span></span>
```azurecli
az vm create \
     --resource-group myResourceGroup \
     --name myVM2 \
     --availability-set myAvailabilitySet \
     --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
     --size Standard_DS1_v2  \
     --generate-ssh-keys \
```

<span data-ttu-id="e7c8a-157">Запишите `publicIpAddress` после его создания.</span><span class="sxs-lookup"><span data-stu-id="e7c8a-157">Take note of the `publicIpAddress` as well after it has been created.</span></span>

### <a name="open-the-tcp-port-for-connectivity"></a><span data-ttu-id="e7c8a-158">Открытие TCP-порта для возможности подключения</span><span class="sxs-lookup"><span data-stu-id="e7c8a-158">Open the TCP port for connectivity</span></span>

<span data-ttu-id="e7c8a-159">Следующий шаг — настройка внешних конечных точек, после чего вы сможете получить удаленный доступ к базе данных Oracle.</span><span class="sxs-lookup"><span data-stu-id="e7c8a-159">The next step is to configure external endpoints,  which enable you to access the Oracle database remotely.</span></span> <span data-ttu-id="e7c8a-160">Чтобы настроить внешние конечные точки, выполните следующие команды.</span><span class="sxs-lookup"><span data-stu-id="e7c8a-160">To configure the external endpoints, run the following commands.</span></span>

#### <a name="open-the-port-for-myvm1"></a><span data-ttu-id="e7c8a-161">Откройте порт для myVM1:</span><span class="sxs-lookup"><span data-stu-id="e7c8a-161">Open the port for myVM1:</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVm1NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

<span data-ttu-id="e7c8a-162">Результат должен выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="e7c8a-162">The results should look similar to the following response:</span></span>

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

#### <a name="open-the-port-for-myvm2"></a><span data-ttu-id="e7c8a-163">Откройте порт для myVM2:</span><span class="sxs-lookup"><span data-stu-id="e7c8a-163">Open the port for myVM2:</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVm2NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

### <a name="connect-to-the-virtual-machine"></a><span data-ttu-id="e7c8a-164">Подключение к виртуальной машине</span><span class="sxs-lookup"><span data-stu-id="e7c8a-164">Connect to the virtual machine</span></span>

<span data-ttu-id="e7c8a-165">Используйте следующую команду для создания сеанса SSH с виртуальной машиной.</span><span class="sxs-lookup"><span data-stu-id="e7c8a-165">Use the following command to create an SSH session with the virtual machine.</span></span> <span data-ttu-id="e7c8a-166">Замените IP-адрес общедоступным IP-адресом виртуальной машины (значение `publicIpAddress`).</span><span class="sxs-lookup"><span data-stu-id="e7c8a-166">Replace the IP address with the `publicIpAddress` of your virtual machine.</span></span>

```bash 
ssh <publicIpAddress>
```

### <a name="create-the-database-on-myvm1-primary"></a><span data-ttu-id="e7c8a-167">Создание базы данных на myVM1 (основная)</span><span class="sxs-lookup"><span data-stu-id="e7c8a-167">Create the database on myVM1 (primary)</span></span>

<span data-ttu-id="e7c8a-168">Программное обеспечение Oracle уже установлено в образе Marketplace, поэтому следующим шагом является установка базы данных.</span><span class="sxs-lookup"><span data-stu-id="e7c8a-168">The Oracle software is already installed on the Marketplace image, so the next step is to install the database.</span></span> 

<span data-ttu-id="e7c8a-169">Запустите программное обеспечение с правами суперпользователя oracle:</span><span class="sxs-lookup"><span data-stu-id="e7c8a-169">Run the software as the 'oracle' superuser:</span></span>

```bash
sudo su - oracle
```

<span data-ttu-id="e7c8a-170">Создание базы данных</span><span class="sxs-lookup"><span data-stu-id="e7c8a-170">Create the database:</span></span>

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
<span data-ttu-id="e7c8a-171">Результат должен выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="e7c8a-171">Outputs should look similar to the following response:</span></span>

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
Look at the log file "/u01/app/oracle/cfgtoollogs/dbca/cdb1/cdb1.log" for more details.
```

<span data-ttu-id="e7c8a-172">Задайте переменные ORACLE_SID и ORACLE_HOME.</span><span class="sxs-lookup"><span data-stu-id="e7c8a-172">Set the ORACLE_SID and ORACLE_HOME variables.</span></span>

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=gg1; export ORACLE_SID
$ LD_LIBRARY_PATH=ORACLE_HOME/lib; export LD_LIBRARY_PATH
```

<span data-ttu-id="e7c8a-173">При необходимости можно добавить ORACLE_HOME и ORACLE_SID в файл BASHRC, чтобы эти параметры сохранились для последующих входов в систему:</span><span class="sxs-lookup"><span data-stu-id="e7c8a-173">Optionally, you can add ORACLE_HOME and ORACLE_SID to the .bashrc file, so that these settings are saved for future sign-ins:</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=gg1
# add Oracle library path
export LD_LIBRARY_PATH=$ORACLE_HOME/lib
```

### <a name="start-oracle-listener"></a><span data-ttu-id="e7c8a-174">Запуск прослушивателя Oracle</span><span class="sxs-lookup"><span data-stu-id="e7c8a-174">Start Oracle listener</span></span>
```bash
$ sudo su - oracle
$ lsnrctl start
```

### <a name="create-the-database-on-myvm2-replicate"></a><span data-ttu-id="e7c8a-175">Создание базы данных на myVM2 (репликация)</span><span class="sxs-lookup"><span data-stu-id="e7c8a-175">Create the database on myVM2 (replicate)</span></span>

```bash
sudo su - oracle
```
<span data-ttu-id="e7c8a-176">Создание базы данных</span><span class="sxs-lookup"><span data-stu-id="e7c8a-176">Create the database:</span></span>

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
<span data-ttu-id="e7c8a-177">Задайте переменные ORACLE_SID и ORACLE_HOME.</span><span class="sxs-lookup"><span data-stu-id="e7c8a-177">Set the ORACLE_SID and ORACLE_HOME variables.</span></span>

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=cdb1; export ORACLE_SID
$ LD_LIBRARY_PATH=ORACLE_HOME/lib; export LD_LIBRARY_PATH
```

<span data-ttu-id="e7c8a-178">При необходимости можно добавить ORACLE_HOME и ORACLE_SID в файл BASHRC, чтобы эти параметры сохранились для последующих входов в систему.</span><span class="sxs-lookup"><span data-stu-id="e7c8a-178">Optionally, you can added ORACLE_HOME and ORACLE_SID to the .bashrc file, so that these settings are saved for future sign-ins.</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
# add Oracle library path
export LD_LIBRARY_PATH=$ORACLE_HOME/lib
```

### <a name="start-oracle-listener"></a><span data-ttu-id="e7c8a-179">Запуск прослушивателя Oracle</span><span class="sxs-lookup"><span data-stu-id="e7c8a-179">Start Oracle listener</span></span>
```bash
$ sudo su - oracle
$ lsnrctl start
```

## <a name="configure-golden-gate"></a><span data-ttu-id="e7c8a-180">Настройка Golden Gate</span><span class="sxs-lookup"><span data-stu-id="e7c8a-180">Configure Golden Gate</span></span> 
<span data-ttu-id="e7c8a-181">Чтобы настроить Golden Gate, выполните действия в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="e7c8a-181">To configure Golden Gate, take the steps in this section.</span></span>

### <a name="enable-archive-log-mode-on-myvm1-primary"></a><span data-ttu-id="e7c8a-182">Включение режима журнала архивирования на myVM1 (основная)</span><span class="sxs-lookup"><span data-stu-id="e7c8a-182">Enable archive log mode on myVM1 (primary)</span></span>

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
<span data-ttu-id="e7c8a-183">Включите принудительное ведение журнала и убедитесь, что есть хотя бы один файл журнала.</span><span class="sxs-lookup"><span data-stu-id="e7c8a-183">Enable force logging, and make sure at least one log file is present.</span></span>

```bash
SQL> ALTER DATABASE FORCE LOGGING;
SQL> ALTER SYSTEM SWITCH LOGFILE;
SQL> ALTER SYSTEM set enable_goldengate_replication=true;
SQL> ALTER PLUGGABLE DATABASE PDB1 OPEN;
SQL> ALTER SESSION SET CONTAINER=PDB1;
SQL> ALTER DATABASE ADD SUPPLEMENTAL LOG DATA;
SQL> EXIT;
```

### <a name="download-golden-gate-software"></a><span data-ttu-id="e7c8a-184">Загрузка программного обеспечения Golden Gate</span><span class="sxs-lookup"><span data-stu-id="e7c8a-184">Download Golden Gate software</span></span>
<span data-ttu-id="e7c8a-185">Чтобы загрузить и подготовить программное обеспечение Oracle Golden Gate, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="e7c8a-185">To download and prepare the Oracle Golden Gate software, complete the following steps:</span></span>

1. <span data-ttu-id="e7c8a-186">Загрузите файл **fbo_ggs_Linux_x64_shiphome.zip** из [страницы скачивания Oracle Golden Gate](http://www.oracle.com/technetwork/middleware/goldengate/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="e7c8a-186">Download the **fbo_ggs_Linux_x64_shiphome.zip** file from the [Oracle Golden Gate download page](http://www.oracle.com/technetwork/middleware/goldengate/downloads/index.html).</span></span> <span data-ttu-id="e7c8a-187">Под заголовком загрузки **12.x.x.x Oracle GoldenGate для Oracle Linux x86-64** должен быть набор ZIP-файлов, которые нужно загрузить.</span><span class="sxs-lookup"><span data-stu-id="e7c8a-187">Under the download title **Oracle GoldenGate 12.x.x.x for Oracle Linux x86-64**, there should be a set of .zip files to download.</span></span>

2. <span data-ttu-id="e7c8a-188">Загрузив ZIP-файлы на клиентском компьютере, скопируйте файлы на виртуальную машину по протоколу SCP.</span><span class="sxs-lookup"><span data-stu-id="e7c8a-188">After you download the .zip files to your client computer, use Secure Copy Protocol (SCP) to copy the files to your VM:</span></span>

  ```bash
  $ scp fbo_ggs_Linux_x64_shiphome.zip <publicIpAddress>:<folder>
  ```

3. <span data-ttu-id="e7c8a-189">Переместите ZIP-файлы в папку **/opt**.</span><span class="sxs-lookup"><span data-stu-id="e7c8a-189">Move the .zip files to the **/opt** folder.</span></span> <span data-ttu-id="e7c8a-190">Затем измените владельца файлов следующим образом:</span><span class="sxs-lookup"><span data-stu-id="e7c8a-190">Then change the owner of the files as follows:</span></span>

  ```bash
  $ sudo su -
  # mv <folder>/*.zip /opt
  ```

4. <span data-ttu-id="e7c8a-191">Распакуйте файлы (установите служебную программу Linux для распаковки, если она еще не установлена):</span><span class="sxs-lookup"><span data-stu-id="e7c8a-191">Unzip the files (install the Linux unzip utility if it's not already installed):</span></span>

  ```bash
  # yum install unzip
  # cd /opt
  # unzip fbo_ggs_Linux_x64_shiphome.zip
  ```

5. <span data-ttu-id="e7c8a-192">Измените разрешение:</span><span class="sxs-lookup"><span data-stu-id="e7c8a-192">Change permission:</span></span>

  ```bash
  # chown -R oracle:oinstall /opt/fbo_ggs_Linux_x64_shiphome
  ```

### <a name="prepare-the-client-and-vm-to-run-x11-for-windows-clients-only"></a><span data-ttu-id="e7c8a-193">Подготовка клиента и виртуальной машины для запуска X11 (только для клиентов Windows)</span><span class="sxs-lookup"><span data-stu-id="e7c8a-193">Prepare the client and VM to run x11 (for Windows clients only)</span></span>
<span data-ttu-id="e7c8a-194">Этот параметр является необязательным.</span><span class="sxs-lookup"><span data-stu-id="e7c8a-194">This is an optional step.</span></span> <span data-ttu-id="e7c8a-195">Если вы используете клиента Linux или уже установили x11, этот шаг можно пропустить.</span><span class="sxs-lookup"><span data-stu-id="e7c8a-195">You can skip this step if you are using a Linux client or already have x11 setup.</span></span>

1. <span data-ttu-id="e7c8a-196">Скачайте PuTTY и Xming на компьютер с Windows:</span><span class="sxs-lookup"><span data-stu-id="e7c8a-196">Download PuTTY and Xming to your Windows computer:</span></span>

  * <span data-ttu-id="e7c8a-197">[Скачать PuTTY](http://www.putty.org/).</span><span class="sxs-lookup"><span data-stu-id="e7c8a-197">[Download PuTTY](http://www.putty.org/)</span></span>
  * <span data-ttu-id="e7c8a-198">[Скачать Xming](https://xming.en.softonic.com/).</span><span class="sxs-lookup"><span data-stu-id="e7c8a-198">[Download Xming](https://xming.en.softonic.com/)</span></span>

2.  <span data-ttu-id="e7c8a-199">Установив PuTTY в папке PuTTY (например, C:\Program Files\PuTTY), запустите файл puttygen.exe (генератор ключей PuTTY).</span><span class="sxs-lookup"><span data-stu-id="e7c8a-199">After you install PuTTY, in the PuTTY folder (for example, C:\Program Files\PuTTY), run puttygen.exe (PuTTY Key Generator).</span></span>

3.  <span data-ttu-id="e7c8a-200">В генераторе ключей PuTTY сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="e7c8a-200">In PuTTY Key Generator:</span></span>

  - <span data-ttu-id="e7c8a-201">Чтобы создать ключ, нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="e7c8a-201">To generate a key, select the **Generate** button.</span></span>
  - <span data-ttu-id="e7c8a-202">Скопируйте содержимое ключа (**CTRL+C**).</span><span class="sxs-lookup"><span data-stu-id="e7c8a-202">Copy the contents of the key (**Ctrl+C**).</span></span>
  - <span data-ttu-id="e7c8a-203">Нажмите кнопку **Save private key** (Сохранить закрытый ключ).</span><span class="sxs-lookup"><span data-stu-id="e7c8a-203">Select the **Save private key** button.</span></span>
  - <span data-ttu-id="e7c8a-204">Игнорируйте предупреждение, появившееся на экране, и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="e7c8a-204">Ignore the warning that appears, and then select **OK**.</span></span>

    ![Снимок экрана со страницей генератора ключей PuTTY](./media/oracle-golden-gate/puttykeygen.png)

4.  <span data-ttu-id="e7c8a-206">В виртуальной машине выполните следующие команды:</span><span class="sxs-lookup"><span data-stu-id="e7c8a-206">In your VM, run these commands:</span></span>

  ```bash
  # sudo su - oracle
  $ mkdir .ssh (if not already created)
  $ cd .ssh
  ```

5. <span data-ttu-id="e7c8a-207">Создайте файл с именем **authorized_keys**.</span><span class="sxs-lookup"><span data-stu-id="e7c8a-207">Create a file named **authorized_keys**.</span></span> <span data-ttu-id="e7c8a-208">Вставьте содержимое ключа в этот файл и сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="e7c8a-208">Paste the contents of the key in this file, and then save the file.</span></span>

  > [!NOTE]
  > <span data-ttu-id="e7c8a-209">Ключ должен содержать строку `ssh-rsa`.</span><span class="sxs-lookup"><span data-stu-id="e7c8a-209">The key must contain the string `ssh-rsa`.</span></span> <span data-ttu-id="e7c8a-210">Кроме того, содержимое ключа должно быть одной строкой текста.</span><span class="sxs-lookup"><span data-stu-id="e7c8a-210">Also, the contents of the key must be a single line of text.</span></span>
  >  

6. <span data-ttu-id="e7c8a-211">Запустите PuTTY.</span><span class="sxs-lookup"><span data-stu-id="e7c8a-211">Start PuTTY.</span></span> <span data-ttu-id="e7c8a-212">В области **Категория** выберите **Подключение** > **SSH** > **Проверка подлинности**.</span><span class="sxs-lookup"><span data-stu-id="e7c8a-212">In the **Category** pane, select **Connection** > **SSH** > **Auth**.</span></span> <span data-ttu-id="e7c8a-213">В поле **Private key file for authentication** (Файл закрытого ключа для проверки подлинности) выберите созданный ранее ключ.</span><span class="sxs-lookup"><span data-stu-id="e7c8a-213">In the **Private key file for authentication** box, browse to the key that you generated earlier.</span></span>

  ![Снимок экрана со страницей настройки закрытого ключа](./media/oracle-golden-gate/setprivatekey.png)

7. <span data-ttu-id="e7c8a-215">В области **Категория** выберите **Подключение** > **SSH** > **X11**.</span><span class="sxs-lookup"><span data-stu-id="e7c8a-215">In the **Category** pane, select **Connection** > **SSH** > **X11**.</span></span> <span data-ttu-id="e7c8a-216">Установите флажок **Enable X11 forwarding** (Включить перенаправление X11).</span><span class="sxs-lookup"><span data-stu-id="e7c8a-216">Then select the **Enable X11 forwarding** box.</span></span>

  ![Снимок экрана со страницей включения X11](./media/oracle-golden-gate/enablex11.png)

8. <span data-ttu-id="e7c8a-218">В области **Категория** выберите **Сеанс**.</span><span class="sxs-lookup"><span data-stu-id="e7c8a-218">In the **Category** pane, go to **Session**.</span></span> <span data-ttu-id="e7c8a-219">Введите сведения об узле, а затем нажмите кнопку **Открыть**.</span><span class="sxs-lookup"><span data-stu-id="e7c8a-219">Enter the host information, and then select **Open**.</span></span>

  ![Снимок экрана со страницей "Сеанс"](./media/oracle-golden-gate/puttysession.png)

### <a name="install-golden-gate-software"></a><span data-ttu-id="e7c8a-221">Установка программного обеспечения Golden Gate</span><span class="sxs-lookup"><span data-stu-id="e7c8a-221">Install Golden Gate software</span></span>

<span data-ttu-id="e7c8a-222">Чтобы установить Oracle Golden Gate, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="e7c8a-222">To install Oracle Golden Gate, complete the following steps:</span></span>

1. <span data-ttu-id="e7c8a-223">Выполните вход в качестве пользователя oracle.</span><span class="sxs-lookup"><span data-stu-id="e7c8a-223">Sign in as oracle.</span></span> <span data-ttu-id="e7c8a-224">Вы сможете войти, не вводя пароль. Перед установкой убедитесь, что Xming работает.</span><span class="sxs-lookup"><span data-stu-id="e7c8a-224">(You should be able to sign in without being prompted for a password.) Make sure that Xming is running before you begin the installation.</span></span>
 
  ```bash
  $ cd /opt/fbo_ggs_Linux_x64_shiphome/Disk1
  $ ./runInstaller
  ```
2. <span data-ttu-id="e7c8a-225">Выберите Oracle GoldenGate for Oracle Database 12c (Oracle GoldenGate для базы данных Oracle 12c).</span><span class="sxs-lookup"><span data-stu-id="e7c8a-225">Select 'Oracle GoldenGate for Oracle Database 12c'.</span></span> <span data-ttu-id="e7c8a-226">Нажмите кнопку **Далее**, чтобы продолжить.</span><span class="sxs-lookup"><span data-stu-id="e7c8a-226">Then select **Next** to continue.</span></span>

  ![Снимок экрана со страницей выбора установки в установщике](./media/oracle-golden-gate/golden_gate_install_01.png)

3. <span data-ttu-id="e7c8a-228">Измените расположение программного обеспечения.</span><span class="sxs-lookup"><span data-stu-id="e7c8a-228">Change the software location.</span></span> <span data-ttu-id="e7c8a-229">Установите флажок **Start Manager** (Запустить диспетчер) и введите расположение базы данных.</span><span class="sxs-lookup"><span data-stu-id="e7c8a-229">Then select  the **Start Manager** box and enter the database location.</span></span> <span data-ttu-id="e7c8a-230">Нажмите кнопку **Далее**, чтобы продолжить.</span><span class="sxs-lookup"><span data-stu-id="e7c8a-230">Select **Next** to continue.</span></span>

  ![Снимок экрана со страницей выбора установки](./media/oracle-golden-gate/golden_gate_install_02.png)

4. <span data-ttu-id="e7c8a-232">Перейдите в каталог инвентаризации, а затем выберите **Далее**, чтобы продолжить.</span><span class="sxs-lookup"><span data-stu-id="e7c8a-232">Change the inventory directory, and then select **Next** to continue.</span></span>

  ![Снимок экрана со страницей выбора установки](./media/oracle-golden-gate/golden_gate_install_03.png)

5. <span data-ttu-id="e7c8a-234">На экране **Сводка** выберите **Установить**, чтобы продолжить.</span><span class="sxs-lookup"><span data-stu-id="e7c8a-234">On the **Summary** screen, select **Install** to continue.</span></span>

  ![Снимок экрана со страницей выбора установки в установщике](./media/oracle-golden-gate/golden_gate_install_04.png)

6. <span data-ttu-id="e7c8a-236">Может потребоваться выполнить скрипт в качестве корневого.</span><span class="sxs-lookup"><span data-stu-id="e7c8a-236">You might be prompted to run a script as 'root'.</span></span> <span data-ttu-id="e7c8a-237">В этом случае откройте отдельный сеанс, подключитесь к виртуальной машине по протоколу SSH, используйте sudo, чтобы сделать скрипт корневым, а затем выполните его.</span><span class="sxs-lookup"><span data-stu-id="e7c8a-237">If so, open a separate session, ssh to the VM, sudo to root, and then run the script.</span></span> <span data-ttu-id="e7c8a-238">Чтобы продолжить, нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="e7c8a-238">Select **OK** continue.</span></span>

  ![Снимок экрана со страницей выбора установки](./media/oracle-golden-gate/golden_gate_install_05.png)

7. <span data-ttu-id="e7c8a-240">По завершении установки нажмите кнопку **Закрыть**, чтобы завершить процесс.</span><span class="sxs-lookup"><span data-stu-id="e7c8a-240">When the installation has finished, select **Close** to complete the process.</span></span>

  ![Снимок экрана со страницей выбора установки](./media/oracle-golden-gate/golden_gate_install_06.png)

### <a name="set-up-service-on-myvm1-primary"></a><span data-ttu-id="e7c8a-242">Настройка службы на myVM1 (основная)</span><span class="sxs-lookup"><span data-stu-id="e7c8a-242">Set up service on myVM1 (primary)</span></span>

1. <span data-ttu-id="e7c8a-243">Создайте или обновите файл tnsnames.ora:</span><span class="sxs-lookup"><span data-stu-id="e7c8a-243">Create or update the tnsnames.ora file:</span></span>

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

2. <span data-ttu-id="e7c8a-244">Создайте учетные записи владельца и пользователя Golden Gate.</span><span class="sxs-lookup"><span data-stu-id="e7c8a-244">Create the Golden Gate owner and user accounts.</span></span>

  > [!NOTE]
  > <span data-ttu-id="e7c8a-245">Учетная запись владельца должна иметь префикс C##.</span><span class="sxs-lookup"><span data-stu-id="e7c8a-245">The owner account must have C## prefix.</span></span>
  >

    ```bash
    $ sqlplus / as sysdba
    SQL> CREATE USER C##GGADMIN identified by ggadmin;
    SQL> EXEC dbms_goldengate_auth.grant_admin_privilege('C##GGADMIN',container=>'ALL');
    SQL> GRANT DBA to C##GGADMIN container=all;
    SQL> connect C##GGADMIN/ggadmin
    SQL> ALTER SESSION SET CONTAINER=PDB1;
    SQL> EXIT;
    ```

3. <span data-ttu-id="e7c8a-246">Создайте тестовую учетную запись пользователя Golden Gate:</span><span class="sxs-lookup"><span data-stu-id="e7c8a-246">Create the Golden Gate test user account:</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ sqlplus system/OraPasswd1@pdb1
  SQL> CREATE USER test identified by test DEFAULT TABLESPACE USERS TEMPORARY TABLESPACE TEMP;
  SQL> GRANT connect, resource, dba TO test;
  SQL> ALTER USER test QUOTA 100M on USERS;
  SQL> connect test/test@pdb1
  SQL> @demo_ora_create
  SQL> @demo_ora_insert
  SQL> EXIT;
  ```

4. <span data-ttu-id="e7c8a-247">Настройте файл параметров извлечения.</span><span class="sxs-lookup"><span data-stu-id="e7c8a-247">Configure the extract parameter file.</span></span>

 <span data-ttu-id="e7c8a-248">Запустите интерфейс командной строки Golden Gate (ggsci):</span><span class="sxs-lookup"><span data-stu-id="e7c8a-248">Start the Golden gate command-line interface (ggsci):</span></span>

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
5. <span data-ttu-id="e7c8a-249">Добавьте следующий файл параметров EXTRACT (с помощью команды vi).</span><span class="sxs-lookup"><span data-stu-id="e7c8a-249">Add the following to the EXTRACT parameter file (by using vi commands).</span></span> <span data-ttu-id="e7c8a-250">Нажмите клавишу ESC, ":wq!"</span><span class="sxs-lookup"><span data-stu-id="e7c8a-250">Press Esc key, ':wq!'</span></span> <span data-ttu-id="e7c8a-251">чтобы сохранить файл.</span><span class="sxs-lookup"><span data-stu-id="e7c8a-251">to save file.</span></span> 

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
6. <span data-ttu-id="e7c8a-252">Зарегистрируйте извлечение, интегрированное с помощью EXTRACT:</span><span class="sxs-lookup"><span data-stu-id="e7c8a-252">Register extract--integrated extract:</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci

  GGSCI> dblogin userid C##GGADMIN, password ggadmin
  Successfully logged into database CDB$ROOT.

  GGSCI> REGISTER EXTRACT EXTORA DATABASE CONTAINER(pdb1)

  2017-05-23 15:58:34  INFO    OGG-02003  Extract EXTORA successfully registered with database at SCN 1821260.

  GGSCI> exit
  ```
7. <span data-ttu-id="e7c8a-253">Настройте контрольные точки извлечения и запустите извлечение в режиме реального времени:</span><span class="sxs-lookup"><span data-stu-id="e7c8a-253">Set up extract checkpoints and start real-time extract:</span></span>

  ```bash
  $ ./ggsci
  GGSCI>  ADD EXTRACT EXTORA, INTEGRATED TRANLOG, BEGIN NOW
  EXTRACT (Integrated) added.

  GGSCI>  ADD RMTTRAIL ./dirdat/rt, EXTRACT EXTORA, MEGABYTES 10
  RMTTRAIL added.

  GGSCI>  START EXTRACT EXTORA

  Sending START request to MANAGER ...
  EXTRACT EXTORA starting

  GGSCI > info all

  Program     Status      Group       Lag at Chkpt  Time Since Chkpt

  MANAGER     RUNNING
  EXTRACT     RUNNING     EXTORA      00:00:11      00:00:04
  ```
<span data-ttu-id="e7c8a-254">На этом шаге найдите начальный сайт SCN, который будет использоваться позже в другом разделе:</span><span class="sxs-lookup"><span data-stu-id="e7c8a-254">In this step, you find the starting SCN, which will be used later, in a different section:</span></span>

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

### <a name="set-up-service-on-myvm2-replicate"></a><span data-ttu-id="e7c8a-255">Настройка службы на myVM2 (репликация)</span><span class="sxs-lookup"><span data-stu-id="e7c8a-255">Set up service on myVM2 (replicate)</span></span>


1. <span data-ttu-id="e7c8a-256">Создайте или обновите файл tnsnames.ora:</span><span class="sxs-lookup"><span data-stu-id="e7c8a-256">Create or update the tnsnames.ora file:</span></span>

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

2. <span data-ttu-id="e7c8a-257">Создайте учетную запись репликации:</span><span class="sxs-lookup"><span data-stu-id="e7c8a-257">Create a replicate account:</span></span>

  ```bash
  $ sqlplus / as sysdba
  SQL> alter session set container = pdb1;
  SQL> create user repuser identified by rep_pass container=current;
  SQL> grant dba to repuser;
  SQL> exec dbms_goldengate_auth.grant_admin_privilege('REPUSER',container=>'PDB1');
  SQL> connect repuser/rep_pass@pdb1 
  SQL> EXIT;
  ```

3. <span data-ttu-id="e7c8a-258">Создайте тестовую учетную запись пользователя Golden Gate:</span><span class="sxs-lookup"><span data-stu-id="e7c8a-258">Create a Golden Gate test user account:</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ sqlplus system/OraPasswd1@pdb1
  SQL> CREATE USER test identified by test DEFAULT TABLESPACE USERS TEMPORARY TABLESPACE TEMP;
  SQL> GRANT connect, resource, dba TO test;
  SQL> ALTER USER test QUOTA 100M on USERS;
  SQL> connect test/test@pdb1
  SQL> @demo_ora_create
  SQL> EXIT;
  ```

4. <span data-ttu-id="e7c8a-259">Файл параметров REPLICAT для репликации изменений:</span><span class="sxs-lookup"><span data-stu-id="e7c8a-259">REPLICAT parameter file to replicate changes:</span></span> 

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  GGSCI> EDIT PARAMS REPORA  
  ```
  <span data-ttu-id="e7c8a-260">Содержимое файла параметров REPORA:</span><span class="sxs-lookup"><span data-stu-id="e7c8a-260">Content of REPORA parameter file:</span></span>

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

5. <span data-ttu-id="e7c8a-261">Настройте контрольную точку репликации:</span><span class="sxs-lookup"><span data-stu-id="e7c8a-261">Set up a replicat checkpoint:</span></span>

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

### <a name="set-up-the-replication-myvm1-and-myvm2"></a><span data-ttu-id="e7c8a-262">Настройка репликации (myVM1 и myVM2)</span><span class="sxs-lookup"><span data-stu-id="e7c8a-262">Set up the replication (myVM1 and myVM2)</span></span>

#### <a name="1-set-up-the-replication-on-myvm2-replicate"></a><span data-ttu-id="e7c8a-263">1. Настройка репликации на myVM2 (репликация)</span><span class="sxs-lookup"><span data-stu-id="e7c8a-263">1. Set up the replication on myVM2 (replicate)</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  GGSCI> EDIT PARAMS MGR
  ```
<span data-ttu-id="e7c8a-264">Обновите файл с использованием следующего содержимого:</span><span class="sxs-lookup"><span data-stu-id="e7c8a-264">Update the file with the following:</span></span>

  ```bash
  PORT 7809
  ACCESSRULE, PROG *, IPADDR *, ALLOW
  ```
<span data-ttu-id="e7c8a-265">Затем перезапустите службу диспетчера:</span><span class="sxs-lookup"><span data-stu-id="e7c8a-265">Then restart the Manager service:</span></span>

  ```bash
  GGSCI> STOP MGR
  GGSCI> START MGR
  GGSCI> EXIT
  ```

#### <a name="2-set-up-the-replication-on-myvm1-primary"></a><span data-ttu-id="e7c8a-266">2) Настройка репликации на myVM1 (основная)</span><span class="sxs-lookup"><span data-stu-id="e7c8a-266">2. Set up the replication on myVM1 (primary)</span></span>

<span data-ttu-id="e7c8a-267">Запустите начальную нагрузку и проверьте наличие ошибок:</span><span class="sxs-lookup"><span data-stu-id="e7c8a-267">Start the initial load and check for errors:</span></span>

```bash
$ cd /u01/app/oracle/product/12.1.0/oggcore_1
$ ./ggsci
GGSCI> START EXTRACT INITEXT
GGSCI> VIEW REPORT INITEXT
```
#### <a name="3-set-up-the-replication-on-myvm2-replicate"></a><span data-ttu-id="e7c8a-268">3. Настройка репликации на myVM2 (репликация)</span><span class="sxs-lookup"><span data-stu-id="e7c8a-268">3. Set up the replication on myVM2 (replicate)</span></span>

<span data-ttu-id="e7c8a-269">Измените номер SCN на полученный ранее номер:</span><span class="sxs-lookup"><span data-stu-id="e7c8a-269">Change the SCN number with the number you obtained before:</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  START REPLICAT REPORA, AFTERCSN 1857887
  ```
<span data-ttu-id="e7c8a-270">Репликация началась и вы можете протестировать ее, вставив новые записи в таблицы TEST.</span><span class="sxs-lookup"><span data-stu-id="e7c8a-270">The replication has begun, and you can test it by inserting new records to TEST tables.</span></span>


### <a name="view-job-status-and-troubleshooting"></a><span data-ttu-id="e7c8a-271">Просмотр состояния задания и устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="e7c8a-271">View job status and troubleshooting</span></span>

#### <a name="view-reports"></a><span data-ttu-id="e7c8a-272">Просмотр отчетов</span><span class="sxs-lookup"><span data-stu-id="e7c8a-272">View reports</span></span>
<span data-ttu-id="e7c8a-273">Чтобы просмотреть отчеты на myVM1, выполните следующие команды:</span><span class="sxs-lookup"><span data-stu-id="e7c8a-273">To view reports on myVM1, run the following commands:</span></span>

  ```bash
  GGSCI> VIEW REPORT EXTORA 
  ```
 
<span data-ttu-id="e7c8a-274">Чтобы просмотреть отчеты на myVM2, выполните следующие команды:</span><span class="sxs-lookup"><span data-stu-id="e7c8a-274">To view reports on myVM2, run the following commands:</span></span>

  ```bash
  GGSCI> VIEW REPORT REPORA
  ```

#### <a name="view-status-and-history"></a><span data-ttu-id="e7c8a-275">Просмотр сведений о состоянии и журналов</span><span class="sxs-lookup"><span data-stu-id="e7c8a-275">View status and history</span></span>
<span data-ttu-id="e7c8a-276">Чтобы просмотреть сведения о состоянии и журналы на myVM1, выполните следующие команды:</span><span class="sxs-lookup"><span data-stu-id="e7c8a-276">To view status and history on myVM1, run the following commands:</span></span>

  ```bash
  GGSCI> dblogin userid c##ggadmin, password ggadmin 
  GGSCI> INFO EXTRACT EXTORA, DETAIL
  ```

<span data-ttu-id="e7c8a-277">Чтобы просмотреть сведения о состоянии и журналы на myVM2, выполните следующие команды:</span><span class="sxs-lookup"><span data-stu-id="e7c8a-277">To view status and history on myVM2, run the following commands:</span></span>

  ```bash
  GGSCI> dblogin userid repuser@pdb1 password rep_pass 
  GGSCI> INFO REP REPORA, DETAIL
  ```
<span data-ttu-id="e7c8a-278">Теперь вы завершили установку и настройку Golden Gate на Oracle Linux.</span><span class="sxs-lookup"><span data-stu-id="e7c8a-278">This completes the installation and configuration of Golden Gate on Oracle linux.</span></span>


## <a name="delete-the-virtual-machine"></a><span data-ttu-id="e7c8a-279">Удаление виртуальной машины</span><span class="sxs-lookup"><span data-stu-id="e7c8a-279">Delete the virtual machine</span></span>

<span data-ttu-id="e7c8a-280">Вы можете удалить ставшие ненужными группу ресурсов, виртуальную машину и все связанные с ней ресурсы, использовав следующую команду.</span><span class="sxs-lookup"><span data-stu-id="e7c8a-280">When it's no longer needed, the following command can be used to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="e7c8a-281">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="e7c8a-281">Next steps</span></span>

<span data-ttu-id="e7c8a-282">Изучите [руководство по созданию высокодоступных виртуальных машин](../../linux/create-cli-complete.md).</span><span class="sxs-lookup"><span data-stu-id="e7c8a-282">[Create highly available virtual machines tutorial](../../linux/create-cli-complete.md)</span></span>

<span data-ttu-id="e7c8a-283">[Изучите примеры развертывания виртуальных машин с помощью интерфейса командной строки](../../linux/cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="e7c8a-283">[Explore VM deployment CLI samples](../../linux/cli-samples.md)</span></span>
