---
title: "aaaCreate виртуальной Машины (классические) с несколькими сетевыми адаптерами - Azure CLI 1.0 | Документы Microsoft"
description: "Узнайте, как toocreate виртуальной Машины (классические) с несколькими сетевыми картами с помощью hello Azure командной строки (CLI) 1.0."
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
ms.openlocfilehash: 181bfb28027caff33410ca94744e79206a2a0d0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-classic-with-multiple-nics-using-hello-azure-cli-10"></a><span data-ttu-id="820d0-103">Создание виртуальной Машины (классические) с несколькими сетевыми адаптерами, используя hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="820d0-103">Create a VM (Classic) with multiple NICs using hello Azure CLI 1.0</span></span>

[!INCLUDE [virtual-network-deploy-multinic-classic-selectors-include.md](../../includes/virtual-network-deploy-multinic-classic-selectors-include.md)]

<span data-ttu-id="820d0-104">Можно создавать виртуальные машины (ВМ) в Azure и присоединить несколько tooeach сетевых интерфейсов (NIC) виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="820d0-104">You can create virtual machines (VMs) in Azure and attach multiple network interfaces (NICs) tooeach of your VMs.</span></span> <span data-ttu-id="820d0-105">Применение нескольких сетевых карт дает возможность разделять типы трафика между сетевыми картами.</span><span class="sxs-lookup"><span data-stu-id="820d0-105">Multiple NICs enable separation of traffic types across NICs.</span></span> <span data-ttu-id="820d0-106">Например один сетевой Адаптер может обмениваться данными с hello Интернета, пока другой взаимодействует только с внутренним ресурсам, не подключен toohello Интернета.</span><span class="sxs-lookup"><span data-stu-id="820d0-106">For example, one NIC might communicate with hello Internet, while another communicates only with internal resources not connected toohello Internet.</span></span> <span data-ttu-id="820d0-107">для многих виртуальных сетевых устройств, таких как предоставление приложений и решений ГЛОБАЛЬНОЙ оптимизации требуется Hello возможность tooseparate сетевой трафик по нескольким сетевым картам.</span><span class="sxs-lookup"><span data-stu-id="820d0-107">hello ability tooseparate network traffic across multiple NICs is required for many network virtual appliances, such as application delivery and WAN optimization solutions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="820d0-108">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Resource Manager и классическая модель](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="820d0-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="820d0-109">В этой статье описан с помощью hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="820d0-109">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="820d0-110">Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="820d0-110">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="820d0-111">Узнайте, как tooperform следующие действия с помощью hello [модели развертывания диспетчера ресурсов](virtual-network-deploy-multinic-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="820d0-111">Learn how tooperform these steps using hello [Resource Manager deployment model](virtual-network-deploy-multinic-arm-cli.md).</span></span>

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="820d0-112">Hello Далее используется группа ресурсов с именем *IaaSStory* hello веб-серверов и группу ресурсов с именем *IaaSStory серверной* hello DB серверов.</span><span class="sxs-lookup"><span data-stu-id="820d0-112">hello following steps use a resource group named *IaaSStory* for hello WEB servers and a resource group named *IaaSStory-BackEnd* for hello DB servers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="820d0-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="820d0-113">Prerequisites</span></span>
<span data-ttu-id="820d0-114">Перед созданием hello DB серверы, необходимо toocreate hello *IaaSStory* группы ресурсов со всеми ресурсами hello необходимые для этого сценария.</span><span class="sxs-lookup"><span data-stu-id="820d0-114">Before you can create hello DB servers, you need toocreate hello *IaaSStory* resource group with all hello necessary resources for this scenario.</span></span> <span data-ttu-id="820d0-115">toocreate эти ресурсы, полный Здравствуйте, описанных ниже.</span><span class="sxs-lookup"><span data-stu-id="820d0-115">toocreate these resources, complete hello steps that follow.</span></span> <span data-ttu-id="820d0-116">Создание виртуальной сети с помощью инструкции hello в hello [создать виртуальную сеть](virtual-networks-create-vnet-classic-cli.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="820d0-116">Create a virtual network by following hello steps in hello [Create a virtual network](virtual-networks-create-vnet-classic-cli.md) article.</span></span>

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="deploy-hello-back-end-vms"></a><span data-ttu-id="820d0-117">Развертывание внутренней hello виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="820d0-117">Deploy hello back-end VMs</span></span>
<span data-ttu-id="820d0-118">Hello ВМ внутренней зависят от создания hello hello следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="820d0-118">hello back-end VMs depend on hello creation of hello following resources:</span></span>

* <span data-ttu-id="820d0-119">**Учетная запись хранения для дисков данных**.</span><span class="sxs-lookup"><span data-stu-id="820d0-119">**Storage account for data disks**.</span></span> <span data-ttu-id="820d0-120">Для повышения производительности hello диски с данными на серверах баз данных hello будет использовать технологию твердотельный накопитель (SSD), которая требуется учетная запись хранения premium.</span><span class="sxs-lookup"><span data-stu-id="820d0-120">For better performance, hello data disks on hello database servers will use solid state drive (SSD) technology, which requires a premium storage account.</span></span> <span data-ttu-id="820d0-121">Убедитесь, что hello расположение Azure, развертывание toosupport хранилище premium.</span><span class="sxs-lookup"><span data-stu-id="820d0-121">Make sure hello Azure location you deploy toosupport premium storage.</span></span>
* <span data-ttu-id="820d0-122">**Сетевые карты**.</span><span class="sxs-lookup"><span data-stu-id="820d0-122">**NICs**.</span></span> <span data-ttu-id="820d0-123">У каждой виртуальной машины будет две сетевые карты: одна для доступа к базе данных, другая — для управления.</span><span class="sxs-lookup"><span data-stu-id="820d0-123">Each VM will have two NICs, one for database access, and one for management.</span></span>
* <span data-ttu-id="820d0-124">**Группа доступности**.</span><span class="sxs-lookup"><span data-stu-id="820d0-124">**Availability set**.</span></span> <span data-ttu-id="820d0-125">Все серверы баз данных будет добавлен tooa одну группу доступности, хотя бы один из виртуальных машин hello tooensure работает и запущена во время обслуживания.</span><span class="sxs-lookup"><span data-stu-id="820d0-125">All database servers will be added tooa single availability set, tooensure at least one of hello VMs is up and running during maintenance.</span></span>

### <a name="step-1---start-your-script"></a><span data-ttu-id="820d0-126">Шаг 1. Запуск сценария</span><span class="sxs-lookup"><span data-stu-id="820d0-126">Step 1 - Start your script</span></span>
<span data-ttu-id="820d0-127">Вы можете загрузить hello bash полный сценарий [здесь](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-cli.sh).</span><span class="sxs-lookup"><span data-stu-id="820d0-127">You can download hello full bash script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-cli.sh).</span></span> <span data-ttu-id="820d0-128">Выполните следующие toowork действия toochange hello скрипта в среде hello.</span><span class="sxs-lookup"><span data-stu-id="820d0-128">Complete hello following steps toochange hello script toowork in your environment:</span></span>

1. <span data-ttu-id="820d0-129">Изменить значения hello hello переменных ниже в зависимости от вашего развертывания выше в существующую группу ресурсов [необходимых компонентов](#Prerequisites).</span><span class="sxs-lookup"><span data-stu-id="820d0-129">Change hello values of hello variables below based on your existing resource group deployed above in [Prerequisites](#Prerequisites).</span></span>

    ```azurecli
    location="useast2"
    vnetName="WTestVNet"
    backendSubnetName="BackEnd"
    ```
2. <span data-ttu-id="820d0-130">Изменить значения hello hello следующих переменных на основе значений hello нужно toouse для развертывания базы данных.</span><span class="sxs-lookup"><span data-stu-id="820d0-130">Change hello values of hello variables below based on hello values you want toouse for your backend deployment.</span></span>

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

### <a name="step-2---create-necessary-resources-for-your-vms"></a><span data-ttu-id="820d0-131">Шаг 2. Создание необходимых ресурсов для виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="820d0-131">Step 2 - Create necessary resources for your VMs</span></span>
1. <span data-ttu-id="820d0-132">Создайте облачную службу для всех внутренних виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="820d0-132">Create a new cloud service for all backend VMs.</span></span> <span data-ttu-id="820d0-133">Использование уведомления hello hello `$backendCSName` переменных для имени группы ресурсов hello, и `$location` для hello регион Azure.</span><span class="sxs-lookup"><span data-stu-id="820d0-133">Notice hello use of hello `$backendCSName` variable for hello resource group name, and `$location` for hello Azure region.</span></span>

    ```azurecli
    azure service create --serviceName $backendCSName \
        --location $location
    ```

2. <span data-ttu-id="820d0-134">Создайте учетную запись хранения premium для hello ОС и toobe дисков данных, используемые вашим виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="820d0-134">Create a premium storage account for hello OS and data disks toobe used by yours VMs.</span></span>

    ```azurecli
    azure storage account create $prmStorageAccountName \
        --location $location \
        --type PLRS
    ```

### <a name="step-3---create-vms-with-multiple-nics"></a><span data-ttu-id="820d0-135">Шаг 3. Создание виртуальных машин с несколькими сетевыми картами</span><span class="sxs-lookup"><span data-stu-id="820d0-135">Step 3 - Create VMs with multiple NICs</span></span>
1. <span data-ttu-id="820d0-136">Запуск нескольких виртуальных машин, в зависимости от hello toocreate цикла `numberOfVMs` переменных.</span><span class="sxs-lookup"><span data-stu-id="820d0-136">Start a loop toocreate multiple VMs, based on hello `numberOfVMs` variables.</span></span>

    ```azurecli
    for ((suffixNumber=1;suffixNumber<=numberOfVMs;suffixNumber++));
    do
    ```

2. <span data-ttu-id="820d0-137">Для каждой виртуальной Машины укажите имя hello и IP-адрес каждого hello двух сетевых адаптеров.</span><span class="sxs-lookup"><span data-stu-id="820d0-137">For each VM, specify hello name and IP address of each of hello two NICs.</span></span>

    ```azurecli
    nic1Name=$vmNamePrefix$suffixNumber-DA
    x=$((suffixNumber+3))
    ipAddress1=$ipAddressPrefix$x

    nic2Name=$vmNamePrefix$suffixNumber-RA
    x=$((suffixNumber+53))
    ipAddress2=$ipAddressPrefix$x
    ```

3. <span data-ttu-id="820d0-138">Создайте hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="820d0-138">Create hello VM.</span></span> <span data-ttu-id="820d0-139">Обратите внимание, использование hello hello `--nic-config` параметр, содержащий список всех сетевых адаптеров с именем, подсети и IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="820d0-139">Notice hello usage of hello `--nic-config` parameter, containing a list of all NICs with name, subnet, and IP address.</span></span>

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

4. <span data-ttu-id="820d0-140">Создайте по два диска данных для каждой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="820d0-140">For each VM, create two data disks.</span></span>

    ```azurecli
    azure vm disk attach-new $vmNamePrefix$suffixNumber \
        $diskSize \
        vhds/$dataDiskPrefix$suffixNumber$dataDiskName-1.vhd

    azure vm disk attach-new $vmNamePrefix$suffixNumber \
        $diskSize \
        vhds/$dataDiskPrefix$suffixNumber$dataDiskName-2.vhd
    done
    ```

### <a name="step-4---run-hello-script"></a><span data-ttu-id="820d0-141">Шаг 4. выполнение сценариев hello</span><span class="sxs-lookup"><span data-stu-id="820d0-141">Step 4 - Run hello script</span></span>
<span data-ttu-id="820d0-142">Теперь, когда вы загрузили и изменить скрипт hello с учетом ваших потребностей, выполнение архивации hello сценария toocreate hello последний ВМ базы данных с несколькими сетевыми адаптерами.</span><span class="sxs-lookup"><span data-stu-id="820d0-142">Now that you downloaded and changed hello script based on your needs, run hello script toocreate hello back end database VMs with multiple NICs.</span></span>

1. <span data-ttu-id="820d0-143">Сохраните сценарий и запустите его в терминале **Bash** .</span><span class="sxs-lookup"><span data-stu-id="820d0-143">Save your script and run it from your **Bash** terminal.</span></span> <span data-ttu-id="820d0-144">Вы увидите выходные данные начальной hello, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="820d0-144">You will see hello initial output, as shown below.</span></span>

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

2. <span data-ttu-id="820d0-145">Через несколько минут hello выполнение будет завершено, и вы увидите rest hello hello выходных данных, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="820d0-145">After a few minutes, hello execution will end and you will see hello rest of hello output as shown below.</span></span>

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
