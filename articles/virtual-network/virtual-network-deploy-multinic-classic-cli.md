---
title: "Создание виртуальных машин (классическая модель) с несколькими сетевыми картами (Azure CLI 1.0) | Документация Майкрософт"
description: "Узнайте, как создать виртуальную машину (классическая модель) с несколькими сетевыми картами с помощью интерфейса командной строки Azure (CLI) версии 1.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: b436e41e-866c-439f-a7c7-7b4b041725ef
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b62421b7289650818748d0016dccfdf42ef0a768
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-classic-with-multiple-nics-using-the-azure-cli-10"></a><span data-ttu-id="5a993-103">Создание виртуальных машин (классическая модель) с несколькими сетевыми картами с помощью Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="5a993-103">Create a VM (Classic) with multiple NICs using the Azure CLI 1.0</span></span>

[!INCLUDE [virtual-network-deploy-multinic-classic-selectors-include.md](../../includes/virtual-network-deploy-multinic-classic-selectors-include.md)]

<span data-ttu-id="5a993-104">Можно создать виртуальные машины в Azure и подключить к каждой из них несколько сетевых карт.</span><span class="sxs-lookup"><span data-stu-id="5a993-104">You can create virtual machines (VMs) in Azure and attach multiple network interfaces (NICs) to each of your VMs.</span></span> <span data-ttu-id="5a993-105">Применение нескольких сетевых карт дает возможность разделять типы трафика между сетевыми картами.</span><span class="sxs-lookup"><span data-stu-id="5a993-105">Multiple NICs enable separation of traffic types across NICs.</span></span> <span data-ttu-id="5a993-106">Например, одна сетевая карта может обмениваться данными с Интернетом, а другая — только с внутренними ресурсами, не подключенными к Интернету.</span><span class="sxs-lookup"><span data-stu-id="5a993-106">For example, one NIC might communicate with the Internet, while another communicates only with internal resources not connected to the Internet.</span></span> <span data-ttu-id="5a993-107">Возможность разделения сетевого трафика между несколькими сетевыми картами требуется для работы многих виртуальных сетевых устройств, таких как решения для доставки приложений и оптимизации глобальной сети.</span><span class="sxs-lookup"><span data-stu-id="5a993-107">The ability to separate network traffic across multiple NICs is required for many network virtual appliances, such as application delivery and WAN optimization solutions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5a993-108">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Resource Manager и классическая модель](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="5a993-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="5a993-109">В этой статье рассматривается использование классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="5a993-109">This article covers using the classic deployment model.</span></span> <span data-ttu-id="5a993-110">Для большинства новых развертываний Майкрософт рекомендует использовать модель диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="5a993-110">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="5a993-111">Действия для модели развертывания с помощью Resource Manager см. в [этой статье](virtual-network-deploy-multinic-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="5a993-111">Learn how to perform these steps using the [Resource Manager deployment model](virtual-network-deploy-multinic-arm-cli.md).</span></span>

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="5a993-112">В приведенных ниже действиях используются следующие группы ресурсов: *IaaSStory* для веб-серверов и *IaaSStory-BackEnd* для серверов базы данных.</span><span class="sxs-lookup"><span data-stu-id="5a993-112">The following steps use a resource group named *IaaSStory* for the WEB servers and a resource group named *IaaSStory-BackEnd* for the DB servers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5a993-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="5a993-113">Prerequisites</span></span>
<span data-ttu-id="5a993-114">Перед созданием серверов базы данных необходимо создать группу ресурсов *IaaSStory* со всеми ресурсами, необходимыми для этого сценария.</span><span class="sxs-lookup"><span data-stu-id="5a993-114">Before you can create the DB servers, you need to create the *IaaSStory* resource group with all the necessary resources for this scenario.</span></span> <span data-ttu-id="5a993-115">Чтобы создать эти ресурсы, выполните приведенные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="5a993-115">To create these resources, complete the steps that follow.</span></span> <span data-ttu-id="5a993-116">Создайте виртуальную сеть, следуя инструкциям в [этой статье](virtual-networks-create-vnet-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="5a993-116">Create a virtual network by following the steps in the [Create a virtual network](virtual-networks-create-vnet-classic-cli.md) article.</span></span>

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="deploy-the-back-end-vms"></a><span data-ttu-id="5a993-117">Развертывание внутренних виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="5a993-117">Deploy the back-end VMs</span></span>
<span data-ttu-id="5a993-118">Внутренние виртуальные машины зависят от создания следующих ресурсов:</span><span class="sxs-lookup"><span data-stu-id="5a993-118">The back-end VMs depend on the creation of the following resources:</span></span>

* <span data-ttu-id="5a993-119">**Учетная запись хранения для дисков данных**.</span><span class="sxs-lookup"><span data-stu-id="5a993-119">**Storage account for data disks**.</span></span> <span data-ttu-id="5a993-120">Для повышения производительности для дисков данных на серверах баз данных будет использоваться технология твердотельного накопителя (SSD), которая требует наличия учетной записи хранения класса Premium.</span><span class="sxs-lookup"><span data-stu-id="5a993-120">For better performance, the data disks on the database servers will use solid state drive (SSD) technology, which requires a premium storage account.</span></span> <span data-ttu-id="5a993-121">Расположение Azure, в которое выполняется развертывание, должно поддерживать хранилище класса Premium.</span><span class="sxs-lookup"><span data-stu-id="5a993-121">Make sure the Azure location you deploy to support premium storage.</span></span>
* <span data-ttu-id="5a993-122">**Сетевые карты**.</span><span class="sxs-lookup"><span data-stu-id="5a993-122">**NICs**.</span></span> <span data-ttu-id="5a993-123">У каждой виртуальной машины будет две сетевые карты: одна для доступа к базе данных, другая — для управления.</span><span class="sxs-lookup"><span data-stu-id="5a993-123">Each VM will have two NICs, one for database access, and one for management.</span></span>
* <span data-ttu-id="5a993-124">**Группа доступности**.</span><span class="sxs-lookup"><span data-stu-id="5a993-124">**Availability set**.</span></span> <span data-ttu-id="5a993-125">Все серверы баз данных будут добавлены в одну группу доступности, чтобы гарантировать, что как минимум одна из виртуальных машин будет запущена и доступна во время обслуживания.</span><span class="sxs-lookup"><span data-stu-id="5a993-125">All database servers will be added to a single availability set, to ensure at least one of the VMs is up and running during maintenance.</span></span>

### <a name="step-1---start-your-script"></a><span data-ttu-id="5a993-126">Шаг 1. Запуск сценария</span><span class="sxs-lookup"><span data-stu-id="5a993-126">Step 1 - Start your script</span></span>
<span data-ttu-id="5a993-127">Полный сценарий Bash можно скачать [здесь](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-cli.sh).</span><span class="sxs-lookup"><span data-stu-id="5a993-127">You can download the full bash script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-cli.sh).</span></span> <span data-ttu-id="5a993-128">Чтобы изменить скрипт для работы в вашей среде, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="5a993-128">Complete the following steps to change the script to work in your environment:</span></span>

1. <span data-ttu-id="5a993-129">Измените значения следующих переменных в зависимости от существующей группы ресурсов, развернутой в соответствии с инструкциями в разделе [Предварительные требования](#Prerequisites)выше.</span><span class="sxs-lookup"><span data-stu-id="5a993-129">Change the values of the variables below based on your existing resource group deployed above in [Prerequisites](#Prerequisites).</span></span>

    ```azurecli
    location="useast2"
    vnetName="WTestVNet"
    backendSubnetName="BackEnd"
    ```
2. <span data-ttu-id="5a993-130">Измените значения следующих переменных на основе значений, которые нужно использовать для внутреннего развертывания.</span><span class="sxs-lookup"><span data-stu-id="5a993-130">Change the values of the variables below based on the values you want to use for your backend deployment.</span></span>

    ```azurecli
    backendCSName="IaaSStory-Backend"
    prmStorageAccountName="iaasstoryprmstorage"
    image="0b11de9248dd4d87b18621318e037d37__RightImage-Ubuntu-14.04-x64-v14.2.1"
    avSetName="ASDB"
    vmSize="Standard_DS3"
    diskSize=127
    vmNamePrefix="DB"
    osDiskName="osdiskdb"
    dataDiskPrefix="db"
    dataDiskName="datadisk"
    ipAddressPrefix="192.168.2."
    username='adminuser'
    password='adminP@ssw0rd'
    numberOfVMs=2
    ```

### <a name="step-2---create-necessary-resources-for-your-vms"></a><span data-ttu-id="5a993-131">Шаг 2. Создание необходимых ресурсов для виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="5a993-131">Step 2 - Create necessary resources for your VMs</span></span>
1. <span data-ttu-id="5a993-132">Создайте облачную службу для всех внутренних виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="5a993-132">Create a new cloud service for all backend VMs.</span></span> <span data-ttu-id="5a993-133">Обратите внимание, что используется переменная `$backendCSName` для имени группы ресурсов и `$location` для региона Azure.</span><span class="sxs-lookup"><span data-stu-id="5a993-133">Notice the use of the `$backendCSName` variable for the resource group name, and `$location` for the Azure region.</span></span>

    ```azurecli
    azure service create --serviceName $backendCSName \
        --location $location
    ```

2. <span data-ttu-id="5a993-134">Создайте учетную запись хранения класса Premium для дисков операционной системы и данных для виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="5a993-134">Create a premium storage account for the OS and data disks to be used by yours VMs.</span></span>

    ```azurecli
    azure storage account create $prmStorageAccountName \
        --location $location \
        --type PLRS
    ```

### <a name="step-3---create-vms-with-multiple-nics"></a><span data-ttu-id="5a993-135">Шаг 3. Создание виртуальных машин с несколькими сетевыми картами</span><span class="sxs-lookup"><span data-stu-id="5a993-135">Step 3 - Create VMs with multiple NICs</span></span>
1. <span data-ttu-id="5a993-136">Запустите цикл для создания нескольких виртуальных машин на основе переменных `numberOfVMs`.</span><span class="sxs-lookup"><span data-stu-id="5a993-136">Start a loop to create multiple VMs, based on the `numberOfVMs` variables.</span></span>

    ```azurecli
    for ((suffixNumber=1;suffixNumber<=numberOfVMs;suffixNumber++));
    do
    ```

2. <span data-ttu-id="5a993-137">Укажите имя и IP-адрес каждой сетевой карты для каждой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="5a993-137">For each VM, specify the name and IP address of each of the two NICs.</span></span>

    ```azurecli
    nic1Name=$vmNamePrefix$suffixNumber-DA
    x=$((suffixNumber+3))
    ipAddress1=$ipAddressPrefix$x

    nic2Name=$vmNamePrefix$suffixNumber-RA
    x=$((suffixNumber+53))
    ipAddress2=$ipAddressPrefix$x
    ```

3. <span data-ttu-id="5a993-138">Создайте виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="5a993-138">Create the VM.</span></span> <span data-ttu-id="5a993-139">Обратите внимание, что использован параметр `--nic-config`, содержащий список всех сетевых карт с именем, подсетью и IP-адресом.</span><span class="sxs-lookup"><span data-stu-id="5a993-139">Notice the usage of the `--nic-config` parameter, containing a list of all NICs with name, subnet, and IP address.</span></span>

    ```azurecli
    azure vm create $backendCSName $image $username $password \
        --connect $backendCSName \
        --vm-name $vmNamePrefix$suffixNumber \
        --vm-size $vmSize \
        --availability-set $avSetName \
        --blob-url $prmStorageAccountName.blob.core.windows.net/vhds/$osDiskName$suffixNumber.vhd \
        --virtual-network-name $vnetName \
        --subnet-names $backendSubnetName \
        --nic-config $nic1Name:$backendSubnetName:$ipAddress1::,$nic2Name:$backendSubnetName:$ipAddress2::
    ```

4. <span data-ttu-id="5a993-140">Создайте по два диска данных для каждой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="5a993-140">For each VM, create two data disks.</span></span>

    ```azurecli
    azure vm disk attach-new $vmNamePrefix$suffixNumber \
        $diskSize \
        vhds/$dataDiskPrefix$suffixNumber$dataDiskName-1.vhd

    azure vm disk attach-new $vmNamePrefix$suffixNumber \
        $diskSize \
        vhds/$dataDiskPrefix$suffixNumber$dataDiskName-2.vhd
    done
    ```

### <a name="step-4---run-the-script"></a><span data-ttu-id="5a993-141">Шаг 4. Запуск сценария</span><span class="sxs-lookup"><span data-stu-id="5a993-141">Step 4 - Run the script</span></span>
<span data-ttu-id="5a993-142">Теперь, когда вы скачали и изменили сценарий в соответствии со своими потребностями, запустите сценарий для создания виртуальных машин внутренней базы данных с несколькими сетевыми картами.</span><span class="sxs-lookup"><span data-stu-id="5a993-142">Now that you downloaded and changed the script based on your needs, run the script to create the back end database VMs with multiple NICs.</span></span>

1. <span data-ttu-id="5a993-143">Сохраните сценарий и запустите его в терминале **Bash** .</span><span class="sxs-lookup"><span data-stu-id="5a993-143">Save your script and run it from your **Bash** terminal.</span></span> <span data-ttu-id="5a993-144">Вы увидите начальный вывод сценария, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="5a993-144">You will see the initial output, as shown below.</span></span>

        info:    Executing command service create
        info:    Creating cloud service
        data:    Cloud service name IaaSStory-Backend
        info:    service create command OK
        info:    Executing command storage account create
        info:    Creating storage account
        info:    storage account create command OK
        info:    Executing command vm create
        info:    Looking up image 0b11de9248dd4d87b18621318e037d37__RightImage-Ubuntu-14.04-x64-v14.2.1
        info:    Looking up virtual network
        info:    Looking up cloud service
        info:    Getting cloud service properties
        info:    Looking up deployment
        info:    Creating VM

2. <span data-ttu-id="5a993-145">Через несколько минут выполнение завершится и отобразится остальной вывод, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="5a993-145">After a few minutes, the execution will end and you will see the rest of the output as shown below.</span></span>

        info:    OK
        info:    vm create command OK
        info:    Executing command vm disk attach-new
        info:    Getting virtual machines
        info:    Adding Data-Disk
        info:    vm disk attach-new command OK
        info:    Executing command vm disk attach-new
        info:    Getting virtual machines
        info:    Adding Data-Disk
        info:    vm disk attach-new command OK
        info:    Executing command vm create
        info:    Looking up image 0b11de9248dd4d87b18621318e037d37__RightImage-Ubuntu-14.04-x64-v14.2.1
        info:    Looking up virtual network
        info:    Looking up cloud service
        info:    Getting cloud service properties
        info:    Looking up deployment
        info:    Creating VM
        info:    OK
        info:    vm create command OK
        info:    Executing command vm disk attach-new
        info:    Getting virtual machines
        info:    Adding Data-Disk
        info:    vm disk attach-new command OK
        info:    Executing command vm disk attach-new
        info:    Getting virtual machines
        info:    Adding Data-Disk
        info:    vm disk attach-new command OK
