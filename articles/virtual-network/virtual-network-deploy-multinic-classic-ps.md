---
title: "aaaCreate виртуальной Машины (классические) с несколькими сетевыми адаптерами - Azure PowerShell | Документы Microsoft"
description: "Узнайте, как toocreate виртуальной Машины (классические) с несколькими сетевыми адаптерами, с помощью PowerShell."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 6e50f39a-2497-4845-a5d4-7332dbc203c5
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 90c967929bb418042c3fb7079e0f69246faac53c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-classic-with-multiple-nics-using-powershell"></a><span data-ttu-id="0ecf3-103">Создание виртуальных машин (классическая модель) с несколькими сетевыми интерфейсами с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="0ecf3-103">Create a VM (Classic) with multiple NICs using PowerShell</span></span>

[!INCLUDE [virtual-network-deploy-multinic-classic-selectors-include.md](../../includes/virtual-network-deploy-multinic-classic-selectors-include.md)]

<span data-ttu-id="0ecf3-104">Можно создавать виртуальные машины (ВМ) в Azure и присоединить несколько tooeach сетевых интерфейсов (NIC) виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="0ecf3-104">You can create virtual machines (VMs) in Azure and attach multiple network interfaces (NICs) tooeach of your VMs.</span></span> <span data-ttu-id="0ecf3-105">Применение нескольких сетевых карт дает возможность разделять типы трафика между сетевыми картами.</span><span class="sxs-lookup"><span data-stu-id="0ecf3-105">Multiple NICs enable separation of traffic types across NICs.</span></span> <span data-ttu-id="0ecf3-106">Например один сетевой Адаптер может обмениваться данными с hello Интернета, пока другой взаимодействует только с внутренним ресурсам, не подключен toohello Интернета.</span><span class="sxs-lookup"><span data-stu-id="0ecf3-106">For example, one NIC might communicate with hello Internet, while another communicates only with internal resources not connected toohello Internet.</span></span> <span data-ttu-id="0ecf3-107">для многих виртуальных сетевых устройств, таких как предоставление приложений и решений ГЛОБАЛЬНОЙ оптимизации требуется Hello возможность tooseparate сетевой трафик по нескольким сетевым картам.</span><span class="sxs-lookup"><span data-stu-id="0ecf3-107">hello ability tooseparate network traffic across multiple NICs is required for many network virtual appliances, such as application delivery and WAN optimization solutions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0ecf3-108">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Resource Manager и классическая модель](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="0ecf3-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="0ecf3-109">В этой статье описан с помощью hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="0ecf3-109">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="0ecf3-110">Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="0ecf3-110">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="0ecf3-111">Узнайте, как tooperform следующие действия с помощью hello [модели развертывания диспетчера ресурсов](virtual-network-deploy-multinic-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="0ecf3-111">Learn how tooperform these steps using hello [Resource Manager deployment model](virtual-network-deploy-multinic-arm-ps.md).</span></span>

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="0ecf3-112">Hello Далее используется группа ресурсов с именем *IaaSStory* hello веб-серверов и группу ресурсов с именем *IaaSStory серверной* hello DB серверов.</span><span class="sxs-lookup"><span data-stu-id="0ecf3-112">hello following steps use a resource group named *IaaSStory* for hello WEB servers and a resource group named *IaaSStory-BackEnd* for hello DB servers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0ecf3-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="0ecf3-113">Prerequisites</span></span>

<span data-ttu-id="0ecf3-114">Перед созданием hello DB серверы, необходимо toocreate hello *IaaSStory* группы ресурсов со всеми ресурсами hello необходимые для этого сценария.</span><span class="sxs-lookup"><span data-stu-id="0ecf3-114">Before you can create hello DB servers, you need toocreate hello *IaaSStory* resource group with all hello necessary resources for this scenario.</span></span> <span data-ttu-id="0ecf3-115">toocreate эти ресурсы, полный Здравствуйте, описанных ниже.</span><span class="sxs-lookup"><span data-stu-id="0ecf3-115">toocreate these resources, complete hello steps that follow.</span></span> <span data-ttu-id="0ecf3-116">Создание виртуальной сети с помощью инструкции hello в hello [создать виртуальную сеть](virtual-networks-create-vnet-classic-netcfg-ps.md) статьи.</span><span class="sxs-lookup"><span data-stu-id="0ecf3-116">Create a virtual network by following hello steps in hello [Create a virtual network](virtual-networks-create-vnet-classic-netcfg-ps.md) article.</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-hello-back-end-vms"></a><span data-ttu-id="0ecf3-117">Создать hello внутренней виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="0ecf3-117">Create hello back-end VMs</span></span>
<span data-ttu-id="0ecf3-118">Hello ВМ внутренней зависят от создания hello hello следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="0ecf3-118">hello back-end VMs depend on hello creation of hello following resources:</span></span>

* <span data-ttu-id="0ecf3-119">**Внутренняя подсеть**.</span><span class="sxs-lookup"><span data-stu-id="0ecf3-119">**Backend subnet**.</span></span> <span data-ttu-id="0ecf3-120">серверы баз данных Hello будет частью отдельной подсети toosegregate трафика.</span><span class="sxs-lookup"><span data-stu-id="0ecf3-120">hello database servers will be part of a separate subnet, toosegregate traffic.</span></span> <span data-ttu-id="0ecf3-121">Приведенный ниже сценарий Hello ожидает tooexist этой подсети в виртуальной сети с именем *WTestVnet*.</span><span class="sxs-lookup"><span data-stu-id="0ecf3-121">hello script below expects this subnet tooexist in a vnet named *WTestVnet*.</span></span>
* <span data-ttu-id="0ecf3-122">**Учетная запись хранения для дисков данных**.</span><span class="sxs-lookup"><span data-stu-id="0ecf3-122">**Storage account for data disks**.</span></span> <span data-ttu-id="0ecf3-123">Для повышения производительности hello диски с данными на серверах баз данных hello будет использовать технологию твердотельный накопитель (SSD), которая требуется учетная запись хранения premium.</span><span class="sxs-lookup"><span data-stu-id="0ecf3-123">For better performance, hello data disks on hello database servers will use solid state drive (SSD) technology, which requires a premium storage account.</span></span> <span data-ttu-id="0ecf3-124">Убедитесь, что hello расположение Azure, развертывание toosupport хранилище premium.</span><span class="sxs-lookup"><span data-stu-id="0ecf3-124">Make sure hello Azure location you deploy toosupport premium storage.</span></span>
* <span data-ttu-id="0ecf3-125">**Группа доступности**.</span><span class="sxs-lookup"><span data-stu-id="0ecf3-125">**Availability set**.</span></span> <span data-ttu-id="0ecf3-126">Все серверы баз данных будет добавлен tooa одну группу доступности, хотя бы один из виртуальных машин hello tooensure работает и запущена во время обслуживания.</span><span class="sxs-lookup"><span data-stu-id="0ecf3-126">All database servers will be added tooa single availability set, tooensure at least one of hello VMs is up and running during maintenance.</span></span>

### <a name="step-1---start-your-script"></a><span data-ttu-id="0ecf3-127">Шаг 1. Запуск сценария</span><span class="sxs-lookup"><span data-stu-id="0ecf3-127">Step 1 - Start your script</span></span>
<span data-ttu-id="0ecf3-128">Вы можете загрузить hello использовать полный скрипт PowerShell [здесь](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-ps.ps1).</span><span class="sxs-lookup"><span data-stu-id="0ecf3-128">You can download hello full PowerShell script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-ps.ps1).</span></span> <span data-ttu-id="0ecf3-129">Выполните действия hello ниже toowork сценария toochange hello в вашей среде.</span><span class="sxs-lookup"><span data-stu-id="0ecf3-129">Follow hello steps below toochange hello script toowork in your environment.</span></span>

1. <span data-ttu-id="0ecf3-130">Изменить значения hello hello переменных ниже в зависимости от вашего развертывания выше в существующую группу ресурсов [необходимых компонентов](#Prerequisites).</span><span class="sxs-lookup"><span data-stu-id="0ecf3-130">Change hello values of hello variables below based on your existing resource group deployed above in [Prerequisites](#Prerequisites).</span></span>

    ```powershell
    $location              = "West US"
    $vnetName              = "WTestVNet"
    $backendSubnetName     = "BackEnd"
    ```

2. <span data-ttu-id="0ecf3-131">Изменить значения hello hello следующих переменных на основе значений hello нужно toouse для развертывания базы данных.</span><span class="sxs-lookup"><span data-stu-id="0ecf3-131">Change hello values of hello variables below based on hello values you want toouse for your backend deployment.</span></span>

    ```powershell
    $backendCSName         = "IaaSStory-Backend"
    $prmStorageAccountName = "iaasstoryprmstorage"
    $avSetName             = "ASDB"
    $vmSize                = "Standard_DS3"
    $diskSize              = 127
    $vmNamePrefix          = "DB"
    $dataDiskSuffix        = "datadisk"
    $ipAddressPrefix       = "192.168.2."
    $numberOfVMs           = 2
    ```

### <a name="step-2---create-necessary-resources-for-your-vms"></a><span data-ttu-id="0ecf3-132">Шаг 2. Создание необходимых ресурсов для виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="0ecf3-132">Step 2 - Create necessary resources for your VMs</span></span>
<span data-ttu-id="0ecf3-133">Необходимо toocreate новой облачной службы и хранилища учетной записи для hello дисков данных для всех виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="0ecf3-133">You need toocreate a new cloud service and a storage account for hello data disks for all VMs.</span></span> <span data-ttu-id="0ecf3-134">Необходимо также toospecify изображения, а учетная запись локального администратора для hello виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="0ecf3-134">You also need toospecify an image, and a local administrator account for hello VMs.</span></span> <span data-ttu-id="0ecf3-135">завершить эти ресурсы toocreate hello следующие действия:</span><span class="sxs-lookup"><span data-stu-id="0ecf3-135">toocreate these resources, complete hello following steps:</span></span>

1. <span data-ttu-id="0ecf3-136">Создайте облачную службу.</span><span class="sxs-lookup"><span data-stu-id="0ecf3-136">Create a new cloud service.</span></span>

    ```powershell
    New-AzureService -ServiceName $backendCSName -Location $location
    ```

2. <span data-ttu-id="0ecf3-137">Создайте учетную запись хранения класса Premium.</span><span class="sxs-lookup"><span data-stu-id="0ecf3-137">Create a new premium storage account.</span></span>

    ```powershell
    New-AzureStorageAccount -StorageAccountName $prmStorageAccountName `
    -Location $location -Type Premium_LRS
    ```
3. <span data-ttu-id="0ecf3-138">Набор hello учетной записи хранения создана выше как hello текущей учетной записи хранения для вашей подписки.</span><span class="sxs-lookup"><span data-stu-id="0ecf3-138">Set hello storage account created above as hello current storage account for your subscription.</span></span>

    ```powershell
    $subscription = Get-AzureSubscription | where {$_.IsCurrent -eq $true}  
    Set-AzureSubscription -SubscriptionName $subscription.SubscriptionName `
    -CurrentStorageAccountName $prmStorageAccountName
    ```

4. <span data-ttu-id="0ecf3-139">Выберите изображение для hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="0ecf3-139">Select an image for hello VM.</span></span>

    ```powershell
    $image = Get-AzureVMImage `
    | where{$_.ImageFamily -eq "SQL Server 2014 RTM Web on Windows Server 2012 R2"} `
    | sort PublishedDate -Descending `
    | select -ExpandProperty ImageName -First 1
    ```

5. <span data-ttu-id="0ecf3-140">Задайте учетные данные учетной записи локального администратора hello.</span><span class="sxs-lookup"><span data-stu-id="0ecf3-140">Set hello local administrator account credentials.</span></span>

    ```powershell
    $cred = Get-Credential -Message "Enter username and password for local admin account"
    ```

### <a name="step-3---create-vms"></a><span data-ttu-id="0ecf3-141">Шаг 3. Создание виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="0ecf3-141">Step 3 - Create VMs</span></span>
<span data-ttu-id="0ecf3-142">Необходимо toouse toocreate цикла, как много виртуальных машин, а создать hello необходимые сетевые адаптеры и виртуальные машины в цикле hello.</span><span class="sxs-lookup"><span data-stu-id="0ecf3-142">You need toouse a loop toocreate as many VMs as you want, and create hello necessary NICs and VMs within hello loop.</span></span> <span data-ttu-id="0ecf3-143">hello toocreate сетевых адаптеров и виртуальных машин, выполните hello следующие шаги.</span><span class="sxs-lookup"><span data-stu-id="0ecf3-143">toocreate hello NICs and VMs, execute hello following steps.</span></span>

1. <span data-ttu-id="0ecf3-144">Запуск `for` hello toorepeat цикла команды toocreate виртуальной Машины, а также две сетевые платы как столько раз, сколько необходимо, на основе hello значения hello `$numberOfVMs` переменной.</span><span class="sxs-lookup"><span data-stu-id="0ecf3-144">Start a `for` loop toorepeat hello commands toocreate a VM and two NICs as many times as necessary, based on hello value of hello `$numberOfVMs` variable.</span></span>

    ```powershell
    for ($suffixNumber = 1; $suffixNumber -le $numberOfVMs; $suffixNumber++){
    ```

2. <span data-ttu-id="0ecf3-145">Создание `VMConfig` объект, указывающий hello изображение, размер и доступности для hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="0ecf3-145">Create a `VMConfig` object specifying hello image, size, and availability set for hello VM.</span></span>

    ```powershell
    $vmName = $vmNamePrefix + $suffixNumber
    $vmConfig = New-AzureVMConfig -Name $vmName `
        -ImageName $image `
        -InstanceSize $vmSize `
        -AvailabilitySetName $avSetName
    ```

3. <span data-ttu-id="0ecf3-146">Здравствуйте, подготовить виртуальную Машину в качестве виртуальной Машины Windows.</span><span class="sxs-lookup"><span data-stu-id="0ecf3-146">Provision hello VM as a Windows VM.</span></span>

    ```powershell
    Add-AzureProvisioningConfig -VM $vmConfig -Windows `
        -AdminUsername $cred.UserName `
        -Password $cred.GetNetworkCredential().Password
    ```

4. <span data-ttu-id="0ecf3-147">Установите сетевой Адаптер по умолчанию hello и назначьте его статический IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="0ecf3-147">Set hello default NIC and assign it a static IP address.</span></span>

    ```powershell
    Set-AzureSubnet         -SubnetNames $backendSubnetName -VM $vmConfig
    Set-AzureStaticVNetIP   -IPAddress ($ipAddressPrefix+$suffixNumber+3) -VM $vmConfig
    ```

5. <span data-ttu-id="0ecf3-148">Добавьте вторую сетевую карту для каждой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="0ecf3-148">Add a second NIC for each VM.</span></span>

    ```powershell
    Add-AzureNetworkInterfaceConfig -Name ("RemoteAccessNIC"+$suffixNumber) `
    -SubnetName $backendSubnetName `
    -StaticVNetIPAddress ($ipAddressPrefix+(53+$suffixNumber)) `
    -VM $vmConfig
    ```

6. <span data-ttu-id="0ecf3-149">Создание дисков toodata для каждой виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="0ecf3-149">Create toodata disks for each VM.</span></span>

    ```powershell
    $dataDisk1Name = $vmName + "-" + $dataDiskSuffix + "-1"    
    Add-AzureDataDisk -CreateNew -VM $vmConfig `
    -DiskSizeInGB $diskSize `
    -DiskLabel $dataDisk1Name `
    -LUN 0

    $dataDisk2Name = $vmName + "-" + $dataDiskSuffix + "-2"   
    Add-AzureDataDisk -CreateNew -VM $vmConfig `
    -DiskSizeInGB $diskSize `
    -DiskLabel $dataDisk2Name `
    -LUN 1
    ```

7. <span data-ttu-id="0ecf3-150">Создайте каждой виртуальной Машины и hello конец цикла.</span><span class="sxs-lookup"><span data-stu-id="0ecf3-150">Create each VM, and end hello loop.</span></span>

    ```powershell
    New-AzureVM -VM $vmConfig `
    -ServiceName $backendCSName `
    -Location $location `
    -VNetName $vnetName
    }
    ```

### <a name="step-4---run-hello-script"></a><span data-ttu-id="0ecf3-151">Шаг 4. выполнение сценариев hello</span><span class="sxs-lookup"><span data-stu-id="0ecf3-151">Step 4 - Run hello script</span></span>
<span data-ttu-id="0ecf3-152">Теперь, когда вы загрузили и изменить скрипт hello зависимости от потребностей, runt он скрипт toocreate hello базой данных виртуальных машин с несколькими сетевыми адаптерами.</span><span class="sxs-lookup"><span data-stu-id="0ecf3-152">Now that you downloaded and changed hello script based on your needs, runt he script toocreate hello back end database VMs with multiple NICs.</span></span>

1. <span data-ttu-id="0ecf3-153">Сохраните сценарий и запустите его из hello **PowerShell** командной строки или **интегрированной среды Сценариев PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="0ecf3-153">Save your script and run it from hello **PowerShell** command prompt, or **PowerShell ISE**.</span></span> <span data-ttu-id="0ecf3-154">Вы увидите выходные данные начальной hello, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="0ecf3-154">You will see hello initial output, as shown below.</span></span>

        OperationDescription    OperationId                          OperationStatus

        New-AzureService        xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        New-AzureStorageAccount xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        
        WARNING: No deployment found in service: 'IaaSStory-Backend'.
2. <span data-ttu-id="0ecf3-155">Заполните hello сведения, необходимые в hello запрос учетных данных и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="0ecf3-155">Fill out hello information needed in hello credentials prompt and click **OK**.</span></span> <span data-ttu-id="0ecf3-156">Вывод Hello ниже возвращается.</span><span class="sxs-lookup"><span data-stu-id="0ecf3-156">hello output below is returned.</span></span>

        New-AzureVM             xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        New-AzureVM             xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
