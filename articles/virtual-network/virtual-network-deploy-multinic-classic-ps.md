---
title: "Создание виртуальных машин (классическая модель) с несколькими сетевыми картами с помощью Azure PowerShell | Документация Майкрософт"
description: "Узнайте, как создать виртуальные машины (классическая модель) с несколькими сетевыми картами с помощью PowerShell."
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
ms.openlocfilehash: 923d4817d96399fc423b0a89cbf88f8d397f1af0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-vm-classic-with-multiple-nics-using-powershell"></a><span data-ttu-id="38a25-103">Создание виртуальных машин (классическая модель) с несколькими сетевыми интерфейсами с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="38a25-103">Create a VM (Classic) with multiple NICs using PowerShell</span></span>

[!INCLUDE [virtual-network-deploy-multinic-classic-selectors-include.md](../../includes/virtual-network-deploy-multinic-classic-selectors-include.md)]

<span data-ttu-id="38a25-104">Можно создать виртуальные машины в Azure и подключить к каждой из них несколько сетевых карт.</span><span class="sxs-lookup"><span data-stu-id="38a25-104">You can create virtual machines (VMs) in Azure and attach multiple network interfaces (NICs) to each of your VMs.</span></span> <span data-ttu-id="38a25-105">Применение нескольких сетевых карт дает возможность разделять типы трафика между сетевыми картами.</span><span class="sxs-lookup"><span data-stu-id="38a25-105">Multiple NICs enable separation of traffic types across NICs.</span></span> <span data-ttu-id="38a25-106">Например, одна сетевая карта может обмениваться данными с Интернетом, а другая — только с внутренними ресурсами, не подключенными к Интернету.</span><span class="sxs-lookup"><span data-stu-id="38a25-106">For example, one NIC might communicate with the Internet, while another communicates only with internal resources not connected to the Internet.</span></span> <span data-ttu-id="38a25-107">Возможность разделения сетевого трафика между несколькими сетевыми картами требуется для работы многих виртуальных сетевых устройств, таких как решения для доставки приложений и оптимизации глобальной сети.</span><span class="sxs-lookup"><span data-stu-id="38a25-107">The ability to separate network traffic across multiple NICs is required for many network virtual appliances, such as application delivery and WAN optimization solutions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="38a25-108">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Resource Manager и классическая модель](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="38a25-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="38a25-109">В этой статье рассматривается использование классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="38a25-109">This article covers using the classic deployment model.</span></span> <span data-ttu-id="38a25-110">Для большинства новых развертываний Майкрософт рекомендует использовать модель диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="38a25-110">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="38a25-111">Действия для модели развертывания с помощью Resource Manager см. в [этой статье](virtual-network-deploy-multinic-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="38a25-111">Learn how to perform these steps using the [Resource Manager deployment model](virtual-network-deploy-multinic-arm-ps.md).</span></span>

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="38a25-112">В приведенных ниже действиях используются следующие группы ресурсов: *IaaSStory* для веб-серверов и *IaaSStory-BackEnd* для серверов базы данных.</span><span class="sxs-lookup"><span data-stu-id="38a25-112">The following steps use a resource group named *IaaSStory* for the WEB servers and a resource group named *IaaSStory-BackEnd* for the DB servers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="38a25-113">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="38a25-113">Prerequisites</span></span>

<span data-ttu-id="38a25-114">Перед созданием серверов базы данных необходимо создать группу ресурсов *IaaSStory* со всеми ресурсами, необходимыми для этого сценария.</span><span class="sxs-lookup"><span data-stu-id="38a25-114">Before you can create the DB servers, you need to create the *IaaSStory* resource group with all the necessary resources for this scenario.</span></span> <span data-ttu-id="38a25-115">Чтобы создать эти ресурсы, выполните приведенные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="38a25-115">To create these resources, complete the steps that follow.</span></span> <span data-ttu-id="38a25-116">Создайте виртуальную сеть, следуя инструкциям в [этой статье](virtual-networks-create-vnet-classic-netcfg-ps.md).</span><span class="sxs-lookup"><span data-stu-id="38a25-116">Create a virtual network by following the steps in the [Create a virtual network](virtual-networks-create-vnet-classic-netcfg-ps.md) article.</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-the-back-end-vms"></a><span data-ttu-id="38a25-117">Создание внутренних виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="38a25-117">Create the back-end VMs</span></span>
<span data-ttu-id="38a25-118">Внутренние виртуальные машины зависят от создания следующих ресурсов:</span><span class="sxs-lookup"><span data-stu-id="38a25-118">The back-end VMs depend on the creation of the following resources:</span></span>

* <span data-ttu-id="38a25-119">**Внутренняя подсеть**.</span><span class="sxs-lookup"><span data-stu-id="38a25-119">**Backend subnet**.</span></span> <span data-ttu-id="38a25-120">Чтобы разделить трафик, серверы базы данных будут входить в отдельную подсеть.</span><span class="sxs-lookup"><span data-stu-id="38a25-120">The database servers will be part of a separate subnet, to segregate traffic.</span></span> <span data-ttu-id="38a25-121">Приведенный ниже сценарий предполагает наличие этой подсети в виртуальной сети с именем *WTestVnet*.</span><span class="sxs-lookup"><span data-stu-id="38a25-121">The script below expects this subnet to exist in a vnet named *WTestVnet*.</span></span>
* <span data-ttu-id="38a25-122">**Учетная запись хранения для дисков данных**.</span><span class="sxs-lookup"><span data-stu-id="38a25-122">**Storage account for data disks**.</span></span> <span data-ttu-id="38a25-123">Для повышения производительности для дисков данных на серверах баз данных будет использоваться технология твердотельного накопителя (SSD), которая требует наличия учетной записи хранения класса Premium.</span><span class="sxs-lookup"><span data-stu-id="38a25-123">For better performance, the data disks on the database servers will use solid state drive (SSD) technology, which requires a premium storage account.</span></span> <span data-ttu-id="38a25-124">Расположение Azure, в которое выполняется развертывание, должно поддерживать хранилище класса Premium.</span><span class="sxs-lookup"><span data-stu-id="38a25-124">Make sure the Azure location you deploy to support premium storage.</span></span>
* <span data-ttu-id="38a25-125">**Группа доступности**.</span><span class="sxs-lookup"><span data-stu-id="38a25-125">**Availability set**.</span></span> <span data-ttu-id="38a25-126">Все серверы баз данных будут добавлены в одну группу доступности, чтобы гарантировать, что как минимум одна из виртуальных машин будет запущена и доступна во время обслуживания.</span><span class="sxs-lookup"><span data-stu-id="38a25-126">All database servers will be added to a single availability set, to ensure at least one of the VMs is up and running during maintenance.</span></span>

### <a name="step-1---start-your-script"></a><span data-ttu-id="38a25-127">Шаг 1. Запуск сценария</span><span class="sxs-lookup"><span data-stu-id="38a25-127">Step 1 - Start your script</span></span>
<span data-ttu-id="38a25-128">Полный сценарий PowerShell можно скачать [здесь](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-ps.ps1).</span><span class="sxs-lookup"><span data-stu-id="38a25-128">You can download the full PowerShell script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-ps.ps1).</span></span> <span data-ttu-id="38a25-129">Чтобы изменить сценарий для работы в вашей среде, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="38a25-129">Follow the steps below to change the script to work in your environment.</span></span>

1. <span data-ttu-id="38a25-130">Измените значения следующих переменных в зависимости от существующей группы ресурсов, развернутой в соответствии с инструкциями в разделе [Предварительные требования](#Prerequisites)выше.</span><span class="sxs-lookup"><span data-stu-id="38a25-130">Change the values of the variables below based on your existing resource group deployed above in [Prerequisites](#Prerequisites).</span></span>

    ```powershell
    $location              = "West US"
    $vnetName              = "WTestVNet"
    $backendSubnetName     = "BackEnd"
    ```

2. <span data-ttu-id="38a25-131">Измените значения следующих переменных на основе значений, которые нужно использовать для внутреннего развертывания.</span><span class="sxs-lookup"><span data-stu-id="38a25-131">Change the values of the variables below based on the values you want to use for your backend deployment.</span></span>

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

### <a name="step-2---create-necessary-resources-for-your-vms"></a><span data-ttu-id="38a25-132">Шаг 2. Создание необходимых ресурсов для виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="38a25-132">Step 2 - Create necessary resources for your VMs</span></span>
<span data-ttu-id="38a25-133">Необходимо создать облачную службу и учетную запись хранения для дисков данных для всех виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="38a25-133">You need to create a new cloud service and a storage account for the data disks for all VMs.</span></span> <span data-ttu-id="38a25-134">Кроме того, для виртуальных машин необходимо указать образ и учетную запись локального администратора.</span><span class="sxs-lookup"><span data-stu-id="38a25-134">You also need to specify an image, and a local administrator account for the VMs.</span></span> <span data-ttu-id="38a25-135">Чтобы создать эти ресурсы, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="38a25-135">To create these resources, complete the following steps:</span></span>

1. <span data-ttu-id="38a25-136">Создайте облачную службу.</span><span class="sxs-lookup"><span data-stu-id="38a25-136">Create a new cloud service.</span></span>

    ```powershell
    New-AzureService -ServiceName $backendCSName -Location $location
    ```

2. <span data-ttu-id="38a25-137">Создайте учетную запись хранения класса Premium.</span><span class="sxs-lookup"><span data-stu-id="38a25-137">Create a new premium storage account.</span></span>

    ```powershell
    New-AzureStorageAccount -StorageAccountName $prmStorageAccountName `
    -Location $location -Type Premium_LRS
    ```
3. <span data-ttu-id="38a25-138">Задайте созданную ранее учетную запись хранения в качестве текущей учетной записи хранения для подписки.</span><span class="sxs-lookup"><span data-stu-id="38a25-138">Set the storage account created above as the current storage account for your subscription.</span></span>

    ```powershell
    $subscription = Get-AzureSubscription | where {$_.IsCurrent -eq $true}  
    Set-AzureSubscription -SubscriptionName $subscription.SubscriptionName `
    -CurrentStorageAccountName $prmStorageAccountName
    ```

4. <span data-ttu-id="38a25-139">Выберите образ виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="38a25-139">Select an image for the VM.</span></span>

    ```powershell
    $image = Get-AzureVMImage `
    | where{$_.ImageFamily -eq "SQL Server 2014 RTM Web on Windows Server 2012 R2"} `
    | sort PublishedDate -Descending `
    | select -ExpandProperty ImageName -First 1
    ```

5. <span data-ttu-id="38a25-140">Задайте учетные данные пароля учетной записи локального администратора.</span><span class="sxs-lookup"><span data-stu-id="38a25-140">Set the local administrator account credentials.</span></span>

    ```powershell
    $cred = Get-Credential -Message "Enter username and password for local admin account"
    ```

### <a name="step-3---create-vms"></a><span data-ttu-id="38a25-141">Шаг 3. Создание виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="38a25-141">Step 3 - Create VMs</span></span>
<span data-ttu-id="38a25-142">Необходимо использовать цикл, чтобы создать необходимое количество виртуальных машин, и создать в нем необходимые сетевые карты и виртуальные машины.</span><span class="sxs-lookup"><span data-stu-id="38a25-142">You need to use a loop to create as many VMs as you want, and create the necessary NICs and VMs within the loop.</span></span> <span data-ttu-id="38a25-143">Чтобы создать сетевые карты и виртуальные машины, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="38a25-143">To create the NICs and VMs, execute the following steps.</span></span>

1. <span data-ttu-id="38a25-144">Запустите цикл `for` для повтора команды, которая позволяет создать виртуальную машину и две сетевые карты необходимое количество раз на основе значения переменной `$numberOfVMs`.</span><span class="sxs-lookup"><span data-stu-id="38a25-144">Start a `for` loop to repeat the commands to create a VM and two NICs as many times as necessary, based on the value of the `$numberOfVMs` variable.</span></span>

    ```powershell
    for ($suffixNumber = 1; $suffixNumber -le $numberOfVMs; $suffixNumber++){
    ```

2. <span data-ttu-id="38a25-145">Создайте объект `VMConfig`, указывающий образ, размер и группу доступности для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="38a25-145">Create a `VMConfig` object specifying the image, size, and availability set for the VM.</span></span>

    ```powershell
    $vmName = $vmNamePrefix + $suffixNumber
    $vmConfig = New-AzureVMConfig -Name $vmName `
        -ImageName $image `
        -InstanceSize $vmSize `
        -AvailabilitySetName $avSetName
    ```

3. <span data-ttu-id="38a25-146">Подготовьте виртуальную машину в качестве виртуальной машины Windows.</span><span class="sxs-lookup"><span data-stu-id="38a25-146">Provision the VM as a Windows VM.</span></span>

    ```powershell
    Add-AzureProvisioningConfig -VM $vmConfig -Windows `
        -AdminUsername $cred.UserName `
        -Password $cred.GetNetworkCredential().Password
    ```

4. <span data-ttu-id="38a25-147">Задайте сетевую карту по умолчанию и назначьте ей статический IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="38a25-147">Set the default NIC and assign it a static IP address.</span></span>

    ```powershell
    Set-AzureSubnet         -SubnetNames $backendSubnetName -VM $vmConfig
    Set-AzureStaticVNetIP   -IPAddress ($ipAddressPrefix+$suffixNumber+3) -VM $vmConfig
    ```

5. <span data-ttu-id="38a25-148">Добавьте вторую сетевую карту для каждой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="38a25-148">Add a second NIC for each VM.</span></span>

    ```powershell
    Add-AzureNetworkInterfaceConfig -Name ("RemoteAccessNIC"+$suffixNumber) `
    -SubnetName $backendSubnetName `
    -StaticVNetIPAddress ($ipAddressPrefix+(53+$suffixNumber)) `
    -VM $vmConfig
    ```

6. <span data-ttu-id="38a25-149">Создайте по два диска данных для каждой виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="38a25-149">Create to data disks for each VM.</span></span>

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

7. <span data-ttu-id="38a25-150">Создайте каждую виртуальную машину и завершите цикл.</span><span class="sxs-lookup"><span data-stu-id="38a25-150">Create each VM, and end the loop.</span></span>

    ```powershell
    New-AzureVM -VM $vmConfig `
    -ServiceName $backendCSName `
    -Location $location `
    -VNetName $vnetName
    }
    ```

### <a name="step-4---run-the-script"></a><span data-ttu-id="38a25-151">Шаг 4. Запуск сценария</span><span class="sxs-lookup"><span data-stu-id="38a25-151">Step 4 - Run the script</span></span>
<span data-ttu-id="38a25-152">Теперь, когда вы скачали и изменили сценарий в соответствии со своими потребностями, запустите сценарий для создания виртуальных машин внутренней базы данных с несколькими сетевыми картами.</span><span class="sxs-lookup"><span data-stu-id="38a25-152">Now that you downloaded and changed the script based on your needs, runt he script to create the back end database VMs with multiple NICs.</span></span>

1. <span data-ttu-id="38a25-153">Сохраните сценарий и запустите его из командной строки **PowerShell** или **интегрированной среды сценариев PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="38a25-153">Save your script and run it from the **PowerShell** command prompt, or **PowerShell ISE**.</span></span> <span data-ttu-id="38a25-154">Вы увидите начальный вывод сценария, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="38a25-154">You will see the initial output, as shown below.</span></span>

        OperationDescription    OperationId                          OperationStatus

        New-AzureService        xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        New-AzureStorageAccount xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        
        WARNING: No deployment found in service: 'IaaSStory-Backend'.
2. <span data-ttu-id="38a25-155">Укажите учетные данные и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="38a25-155">Fill out the information needed in the credentials prompt and click **OK**.</span></span> <span data-ttu-id="38a25-156">Отобразится результат, показанный ниже.</span><span class="sxs-lookup"><span data-stu-id="38a25-156">The output below is returned.</span></span>

        New-AzureVM             xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        New-AzureVM             xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
