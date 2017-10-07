---
title: "aaaCreate виртуальной Машины с несколькими сетевыми картами - Azure PowerShell | Документы Microsoft"
description: "Узнайте, как toocreate виртуальной Машины с несколькими сетевыми картами с помощью PowerShell."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 88880483-8f9e-4eeb-b783-64b8613407d9
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 507a413510da3ee69aefed324977ee40e442268b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-multiple-nics-using-powershell"></a><span data-ttu-id="f927e-103">Создание виртуальной машины с несколькими сетевыми интерфейсами с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="f927e-103">Create a VM with multiple NICs using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f927e-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f927e-104">PowerShell</span></span>](virtual-network-deploy-multinic-arm-ps.md)
> * [<span data-ttu-id="f927e-105">Интерфейс командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="f927e-105">Azure CLI</span></span>](virtual-network-deploy-multinic-arm-cli.md)
> * [<span data-ttu-id="f927e-106">Шаблон</span><span class="sxs-lookup"><span data-stu-id="f927e-106">Template</span></span>](virtual-network-deploy-multinic-arm-template.md)
> * [<span data-ttu-id="f927e-107">PowerShell (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="f927e-107">PowerShell (Classic)</span></span>](virtual-network-deploy-multinic-classic-ps.md)
> * [<span data-ttu-id="f927e-108">Интерфейс командной строки Azure (классическая модель)</span><span class="sxs-lookup"><span data-stu-id="f927e-108">Azure CLI (Classic)</span></span>](virtual-network-deploy-multinic-classic-cli.md)

[!INCLUDE [virtual-network-deploy-multinic-intro-include.md](../../includes/virtual-network-deploy-multinic-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="f927e-109">В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Resource Manager и классическая модель](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="f927e-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="f927e-110">В этой статье описывается использование модели развертывания диспетчера ресурсов hello, который рекомендуется в большинстве случаев новый вместо hello [классической модели развертывания](virtual-network-deploy-multinic-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="f927e-110">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](virtual-network-deploy-multinic-classic-ps.md).</span></span>
>

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="f927e-111">Hello Далее используется группа ресурсов с именем *IaaSStory* hello веб-серверов и группу ресурсов с именем *IaaSStory серверной* hello DB серверов.</span><span class="sxs-lookup"><span data-stu-id="f927e-111">hello following steps use a resource group named *IaaSStory* for hello WEB servers and a resource group named *IaaSStory-BackEnd* for hello DB servers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f927e-112">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="f927e-112">Prerequisites</span></span>
<span data-ttu-id="f927e-113">Перед созданием hello DB серверы, необходимо toocreate hello *IaaSStory* группы ресурсов со всеми ресурсами hello необходимые для этого сценария.</span><span class="sxs-lookup"><span data-stu-id="f927e-113">Before you can create hello DB servers, you need toocreate hello *IaaSStory* resource group with all hello necessary resources for this scenario.</span></span> <span data-ttu-id="f927e-114">завершить эти ресурсы toocreate hello следующие действия:</span><span class="sxs-lookup"><span data-stu-id="f927e-114">toocreate these resources, complete hello following steps:</span></span>

1. <span data-ttu-id="f927e-115">Перейдите в слишком[страницы шаблона hello](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span><span class="sxs-lookup"><span data-stu-id="f927e-115">Navigate too[hello template page](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span></span>
2. <span data-ttu-id="f927e-116">На странице шаблона hello, toohello справа от **родительской группы ресурсов**, нажмите кнопку **развертывание tooAzure**.</span><span class="sxs-lookup"><span data-stu-id="f927e-116">In hello template page, toohello right of **Parent resource group**, click **Deploy tooAzure**.</span></span>
3. <span data-ttu-id="f927e-117">При необходимости измените значения параметров hello, а затем выполните действия hello в группе ресурсов hello toodeploy портала предварительной версии Azure hello.</span><span class="sxs-lookup"><span data-stu-id="f927e-117">If needed, change hello parameter values, then follow hello steps in hello Azure preview portal toodeploy hello resource group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f927e-118">Имена учетных записей хранения должны быть уникальными.</span><span class="sxs-lookup"><span data-stu-id="f927e-118">Make sure your storage account names are unique.</span></span> <span data-ttu-id="f927e-119">Они не могут повторяться в Azure.</span><span class="sxs-lookup"><span data-stu-id="f927e-119">You cannot have duplicate storage account names in Azure.</span></span>
> 

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-hello-back-end-vms"></a><span data-ttu-id="f927e-120">Создать hello внутренней виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="f927e-120">Create hello back-end VMs</span></span>
<span data-ttu-id="f927e-121">Hello ВМ внутренней зависят от создания hello hello следующие ресурсы:</span><span class="sxs-lookup"><span data-stu-id="f927e-121">hello back-end VMs depend on hello creation of hello following resources:</span></span>

* <span data-ttu-id="f927e-122">**Учетная запись хранения для дисков данных**.</span><span class="sxs-lookup"><span data-stu-id="f927e-122">**Storage account for data disks**.</span></span> <span data-ttu-id="f927e-123">Для повышения производительности hello диски с данными на серверах баз данных hello будет использовать технологию твердотельный накопитель (SSD), которая требуется учетная запись хранения premium.</span><span class="sxs-lookup"><span data-stu-id="f927e-123">For better performance, hello data disks on hello database servers will use solid state drive (SSD) technology, which requires a premium storage account.</span></span> <span data-ttu-id="f927e-124">Убедитесь, что hello расположение Azure, развертывание toosupport хранилище premium.</span><span class="sxs-lookup"><span data-stu-id="f927e-124">Make sure hello Azure location you deploy toosupport premium storage.</span></span>
* <span data-ttu-id="f927e-125">**Сетевые карты**.</span><span class="sxs-lookup"><span data-stu-id="f927e-125">**NICs**.</span></span> <span data-ttu-id="f927e-126">У каждой виртуальной машины будет две сетевые карты: одна для доступа к базе данных, другая — для управления.</span><span class="sxs-lookup"><span data-stu-id="f927e-126">Each VM will have two NICs, one for database access, and one for management.</span></span>
* <span data-ttu-id="f927e-127">**Группа доступности**.</span><span class="sxs-lookup"><span data-stu-id="f927e-127">**Availability set**.</span></span> <span data-ttu-id="f927e-128">Все серверы баз данных будет добавлен tooa одну группу доступности, хотя бы один из виртуальных машин hello tooensure работает и запущена во время обслуживания.</span><span class="sxs-lookup"><span data-stu-id="f927e-128">All database servers will be added tooa single availability set, tooensure at least one of hello VMs is up and running during maintenance.</span></span>  

### <a name="step-1---start-your-script"></a><span data-ttu-id="f927e-129">Шаг 1. Запуск сценария</span><span class="sxs-lookup"><span data-stu-id="f927e-129">Step 1 - Start your script</span></span>
<span data-ttu-id="f927e-130">Вы можете загрузить hello использовать полный скрипт PowerShell [здесь](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/arm/virtual-network-deploy-multinic-arm-ps.ps1).</span><span class="sxs-lookup"><span data-stu-id="f927e-130">You can download hello full PowerShell script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/arm/virtual-network-deploy-multinic-arm-ps.ps1).</span></span> <span data-ttu-id="f927e-131">Выполните действия hello ниже toowork сценария toochange hello в вашей среде.</span><span class="sxs-lookup"><span data-stu-id="f927e-131">Follow hello steps below toochange hello script toowork in your environment.</span></span>

1. <span data-ttu-id="f927e-132">Изменить значения hello hello переменных ниже в зависимости от вашего развертывания выше в существующую группу ресурсов [необходимых компонентов](#Prerequisites).</span><span class="sxs-lookup"><span data-stu-id="f927e-132">Change hello values of hello variables below based on your existing resource group deployed above in [Prerequisites](#Prerequisites).</span></span>

    ```powershell
    $existingRGName        = "IaaSStory"
    $location              = "West US"
    $vnetName              = "WTestVNet"
    $backendSubnetName     = "BackEnd"
    $remoteAccessNSGName   = "NSG-RemoteAccess"
    $stdStorageAccountName = "wtestvnetstoragestd"
    ```

2. <span data-ttu-id="f927e-133">Изменить значения hello hello следующих переменных на основе значений hello нужно toouse для развертывания базы данных.</span><span class="sxs-lookup"><span data-stu-id="f927e-133">Change hello values of hello variables below based on hello values you want toouse for your backend deployment.</span></span>

    ```powershell
    $backendRGName         = "IaaSStory-Backend"
    $prmStorageAccountName = "wtestvnetstorageprm"
    $avSetName             = "ASDB"
    $vmSize                = "Standard_DS3"
    $publisher             = "MicrosoftSQLServer"
    $offer                 = "SQL2014SP1-WS2012R2"
    $sku                   = "Standard"
    $version               = "latest"
    $vmNamePrefix          = "DB"
    $osDiskPrefix          = "osdiskdb"
    $dataDiskPrefix        = "datadisk"
    $diskSize               = "120"    
    $nicNamePrefix         = "NICDB"
    $ipAddressPrefix       = "192.168.2."
    $numberOfVMs           = 2
    ```
3. <span data-ttu-id="f927e-134">Получить hello существующих ресурсов, необходимых для развертывания.</span><span class="sxs-lookup"><span data-stu-id="f927e-134">Retrieve hello existing resources needed for your deployment.</span></span>

    ```powershell
    $vnet                  = Get-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $existingRGName
    $backendSubnet         = $vnet.Subnets|?{$_.Name -eq $backendSubnetName}
    $remoteAccessNSG       = Get-AzureRmNetworkSecurityGroup -Name $remoteAccessNSGName -ResourceGroupName $existingRGName
    $stdStorageAccount     = Get-AzureRmStorageAccount -Name $stdStorageAccountName -ResourceGroupName $existingRGName
    ```

### <a name="step-2---create-necessary-resources-for-your-vms"></a><span data-ttu-id="f927e-135">Шаг 2. Создание необходимых ресурсов для виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="f927e-135">Step 2 - Create necessary resources for your VMs</span></span>
<span data-ttu-id="f927e-136">Потребуется toocreate новую группу ресурсов учетной записи хранения для дисков с данными hello и набор доступности для всех виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="f927e-136">You need toocreate a new resource group, a storage account for hello data disks, and an availability set for all VMs.</span></span> <span data-ttu-id="f927e-137">Alos необходимо hello учетные данные учетной записи локального администратора для каждой виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="f927e-137">You alos need hello local administrator account credentials for each VM.</span></span> <span data-ttu-id="f927e-138">выполнение этих ресурсов toocreate hello следующие действия.</span><span class="sxs-lookup"><span data-stu-id="f927e-138">toocreate these resources, execute hello following steps.</span></span>

1. <span data-ttu-id="f927e-139">Создайте новую группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="f927e-139">Create a new resource group.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name $backendRGName -Location $location
    ```
2. <span data-ttu-id="f927e-140">Создайте новую учетную запись хранения premium в группе ресурсов hello, созданной ранее.</span><span class="sxs-lookup"><span data-stu-id="f927e-140">Create a new premium storage account in hello resource group created above.</span></span>

    ```powershell
    $prmStorageAccount = New-AzureRmStorageAccount -Name $prmStorageAccountName `
    -ResourceGroupName $backendRGName -Type Premium_LRS -Location $location
    ```
3. <span data-ttu-id="f927e-141">Создайте группу доступности.</span><span class="sxs-lookup"><span data-stu-id="f927e-141">Create a new availability set.</span></span>

    ```powershell
    $avSet = New-AzureRmAvailabilitySet -Name $avSetName -ResourceGroupName $backendRGName -Location $location
    ```
4. <span data-ttu-id="f927e-142">Получение локального администратора hello toobe учетные данные учетной записи, используемый для каждой виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="f927e-142">Get hello local administrator account credentials toobe used for each VM.</span></span>

    ```powershell
    $cred = Get-Credential -Message "Type hello name and password for hello local administrator account."
    ```

### <a name="step-3---create-hello-nics-and-back-end-vms"></a><span data-ttu-id="f927e-143">Шаг 3 — Создание hello сетевых адаптеров и виртуальных машин серверной части</span><span class="sxs-lookup"><span data-stu-id="f927e-143">Step 3 - Create hello NICs and back-end VMs</span></span>
<span data-ttu-id="f927e-144">Необходимо toouse toocreate цикла, как много виртуальных машин, а создать hello необходимые сетевые адаптеры и виртуальные машины в цикле hello.</span><span class="sxs-lookup"><span data-stu-id="f927e-144">You need toouse a loop toocreate as many VMs as you want, and create hello necessary NICs and VMs within hello loop.</span></span> <span data-ttu-id="f927e-145">hello toocreate сетевых адаптеров и виртуальных машин, выполните hello следующие шаги.</span><span class="sxs-lookup"><span data-stu-id="f927e-145">toocreate hello NICs and VMs, execute hello following steps.</span></span>

1. <span data-ttu-id="f927e-146">Запуск `for` hello toorepeat цикла команды toocreate виртуальной Машины, а также две сетевые платы как столько раз, сколько необходимо, на основе hello значения hello `$numberOfVMs` переменной.</span><span class="sxs-lookup"><span data-stu-id="f927e-146">Start a `for` loop toorepeat hello commands toocreate a VM and two NICs as many times as necessary, based on hello value of hello `$numberOfVMs` variable.</span></span>
   
    ```powershell
    for ($suffixNumber = 1; $suffixNumber -le $numberOfVMs; $suffixNumber++){
    ```

2. <span data-ttu-id="f927e-147">Создайте hello сетевых Адаптеров используются для доступа к базе данных.</span><span class="sxs-lookup"><span data-stu-id="f927e-147">Create hello NIC used for database access.</span></span>

    ```powershell
    $nic1Name = $nicNamePrefix + $suffixNumber + "-DA"
    $ipAddress1 = $ipAddressPrefix + ($suffixNumber + 3)
    $nic1 = New-AzureRmNetworkInterface -Name $nic1Name -ResourceGroupName $backendRGName `
    -Location $location -SubnetId $backendSubnet.Id -PrivateIpAddress $ipAddress1
    ```

3. <span data-ttu-id="f927e-148">Создайте hello сетевых Адаптеров используются для удаленного доступа.</span><span class="sxs-lookup"><span data-stu-id="f927e-148">Create hello NIC used for remote access.</span></span> <span data-ttu-id="f927e-149">Обратите внимание на то, как этот сетевой Адаптер имеет связанный NSG tooit.</span><span class="sxs-lookup"><span data-stu-id="f927e-149">Notice how this NIC has an NSG associated tooit.</span></span>

    ```powershell
    $nic2Name = $nicNamePrefix + $suffixNumber + "-RA"
    $ipAddress2 = $ipAddressPrefix + (53 + $suffixNumber)
    $nic2 = New-AzureRmNetworkInterface -Name $nic2Name -ResourceGroupName $backendRGName `
    -Location $location -SubnetId $backendSubnet.Id -PrivateIpAddress $ipAddress2 `
    -NetworkSecurityGroupId $remoteAccessNSG.Id
    ```

4. <span data-ttu-id="f927e-150">Создайте объект `vmConfig`.</span><span class="sxs-lookup"><span data-stu-id="f927e-150">Create `vmConfig` object.</span></span>

    ```powershell
    $vmName = $vmNamePrefix + $suffixNumber
    $vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize -AvailabilitySetId $avSet.Id
    ```

5. <span data-ttu-id="f927e-151">Создайте по два диска данных на виртуальную машину.</span><span class="sxs-lookup"><span data-stu-id="f927e-151">Create two data disks per VM.</span></span> <span data-ttu-id="f927e-152">Обратите внимание, что диски с данными hello в учетной записи хранения premium hello созданного ранее.</span><span class="sxs-lookup"><span data-stu-id="f927e-152">Notice that hello data disks are in hello premium storage account created earlier.</span></span>

    ```powershell
    $dataDisk1Name = $vmName + "-" + $osDiskPrefix + "-1"
    $data1VhdUri = $prmStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $dataDisk1Name + ".vhd"
    Add-AzureRmVMDataDisk -VM $vmConfig -Name $dataDisk1Name -DiskSizeInGB $diskSize `
    -VhdUri $data1VhdUri -CreateOption empty -Lun 0

    $dataDisk2Name = $vmName + "-" + $dataDiskPrefix + "-2"
    $data2VhdUri = $prmStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $dataDisk2Name + ".vhd"
    Add-AzureRmVMDataDisk -VM $vmConfig -Name $dataDisk2Name -DiskSizeInGB $diskSize `
    -VhdUri $data2VhdUri -CreateOption empty -Lun 1
    ```

6. <span data-ttu-id="f927e-153">Настройте hello операционной системы и toobe изображения для hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="f927e-153">Configure hello operating system, and image toobe used for hello VM.</span></span>

    ```powershell
    $vmConfig = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $vmName -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig -PublisherName $publisher -Offer $offer -Skus $sku -Version $version
    ```

7. <span data-ttu-id="f927e-154">Добавить hello двух сетевых адаптеров, созданной ранее toohello `vmConfig` объекта.</span><span class="sxs-lookup"><span data-stu-id="f927e-154">Add hello two NICs created above toohello `vmConfig` object.</span></span>

    ```powershell
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic1.Id -Primary
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic2.Id
    ```

8. <span data-ttu-id="f927e-155">Создайте диск ОС hello и hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="f927e-155">Create hello OS disk and create hello VM.</span></span> <span data-ttu-id="f927e-156">Обратите внимание hello `}` конца hello `for` цикла.</span><span class="sxs-lookup"><span data-stu-id="f927e-156">Notice hello `}` ending hello `for` loop.</span></span>

    ```powershell
    $osDiskName = $vmName + "-" + $osDiskSuffix
    $osVhdUri = $stdStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $osDiskName + ".vhd"
    $vmConfig = Set-AzureRmVMOSDisk -VM $vmConfig -Name $osDiskName -VhdUri $osVhdUri -CreateOption fromImage
    New-AzureRmVM -VM $vmConfig -ResourceGroupName $backendRGName -Location $location
    }
    ```

### <a name="step-4---run-hello-script"></a><span data-ttu-id="f927e-157">Шаг 4. выполнение сценариев hello</span><span class="sxs-lookup"><span data-stu-id="f927e-157">Step 4 - Run hello script</span></span>
<span data-ttu-id="f927e-158">Теперь, когда вы загрузили и изменить скрипт hello зависимости от потребностей, runt он скрипт toocreate hello базой данных виртуальных машин с несколькими сетевыми адаптерами.</span><span class="sxs-lookup"><span data-stu-id="f927e-158">Now that you downloaded and changed hello script based on your needs, runt he script toocreate hello back end database VMs with multiple NICs.</span></span>

1. <span data-ttu-id="f927e-159">Сохраните сценарий и запустите его из hello **PowerShell** командной строки или **интегрированной среды Сценариев PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="f927e-159">Save your script and run it from hello **PowerShell** command prompt, or **PowerShell ISE**.</span></span> <span data-ttu-id="f927e-160">Вы увидите выходные данные начальной hello, следующим образом:</span><span class="sxs-lookup"><span data-stu-id="f927e-160">You will see hello initial output, as follows:</span></span>

        ResourceGroupName : IaaSStory-Backend
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
            Actions  NotActions
            =======  ==========
                *                  

        ResourceId        : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory-Backend

2. <span data-ttu-id="f927e-161">Через несколько минут, заполните hello запрос учетных данных и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="f927e-161">After a few minutes, fill out hello credentials prompt and click **OK**.</span></span> <span data-ttu-id="f927e-162">ниже вывода Hello представляет одной виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="f927e-162">hello output below represents a single VM.</span></span> <span data-ttu-id="f927e-163">Обратите внимание hello весь процесс занял toocomplete 8 минут.</span><span class="sxs-lookup"><span data-stu-id="f927e-163">Notice hello entire process took 8 minutes toocomplete.</span></span>

        ResourceGroupName            :
        Id                           :
        Name                         : DB2
        Type                         :
        Location                     :
        Tags                         :
        TagsText                     : null
        AvailabilitySetReference     : Microsoft.Azure.Management.Compute.Models.AvailabilitySetReference
        AvailabilitySetReferenceText :  {
                                    "ReferenceUri": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/IaaSStory-Backend/providers/Microsoft.Compute/availabilitySets/ASDB"
                                    }
        Extensions                   :
        ExtensionsText               : null
        HardwareProfile              : Microsoft.Azure.Management.Compute.Models.HardwareProfile
        HardwareProfileText          : {
                                        "VirtualMachineSize": "Standard_DS3"
                                       }
        InstanceView                 :
        InstanceViewText             : null
        NetworkProfile               :
        NetworkProfileText           : null
        OSProfile                    :
        OSProfileText                : null
        Plan                         :
        PlanText                     : null
        ProvisioningState            :
        StorageProfile               : Microsoft.Azure.Management.Compute.Models.StorageProfile
        StorageProfileText           : {
                                         "DataDisks": [
                                           {
                                             "Lun": 0,
                                             "Caching": null,
                                             "CreateOption": "empty",
                                             "DiskSizeGB": 127,
                                             "Name": "DB2-datadisk-1",
                                             "SourceImage": null,
                                             "VirtualHardDisk": {
                                               "Uri": "https://wtestvnetstorageprm.blob.core.windows.net/vhds/DB2-datadisk-1.vhd"
                                             }
                                           }
                                         ],
                                         "ImageReference": null,
                                         "OSDisk": null
                                       }
        DataDiskNames                : {DB2-datadisk-1}
        NetworkInterfaceIDs          :
        RequestId                    :
        StatusCode                   : 0

        ResourceGroupName            :
        Id                           :
        Name                         : DB2
        Type                         :
        Location                     :
        Tags                         :
        TagsText                     : null
        AvailabilitySetReference     : Microsoft.Azure.Management.Compute.Models.AvailabilitySetReference
        AvailabilitySetReferenceText : {
                                         "ReferenceUri": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/IaaSStory-Backend/providers/
                                       Microsoft.Compute/availabilitySets/ASDB"
                                       }
        Extensions                   :
        ExtensionsText               : null
        HardwareProfile              : Microsoft.Azure.Management.Compute.Models.HardwareProfile
        HardwareProfileText          : {
                                         "VirtualMachineSize": "Standard_DS3"
                                       }
        InstanceView                 :
        InstanceViewText             : null
        NetworkProfile               :
        NetworkProfileText           : null
        OSProfile                    :
        OSProfileText                : null
        Plan                         :
        PlanText                     : null
        ProvisioningState            :
        StorageProfile               : Microsoft.Azure.Management.Compute.Models.StorageProfile
        StorageProfileText           : {
                                         "DataDisks": [
                                           {
                                             "Lun": 0,
                                             "Caching": null,
                                             "CreateOption": "empty",
                                             "DiskSizeGB": 127,
                                             "Name": "DB2-datadisk-1",
                                             "SourceImage": null,
                                             "VirtualHardDisk": {
                                               "Uri": "https://wtestvnetstorageprm.blob.core.windows.net/vhds/DB2-datadisk-1.vhd"
                                             }
                                           },
                                           {
                                             "Lun": 1,
                                             "Caching": null,
                                             "CreateOption": "empty",
                                             "DiskSizeGB": 127,
                                             "Name": "DB2-datadisk-2",
                                             "SourceImage": null,
                                             "VirtualHardDisk": {
                                               "Uri": "https://wtestvnetstorageprm.blob.core.windows.net/vhds/DB2-datadisk-2.vhd"
                                             }
                                           }
                                         ],
                                         "ImageReference": null,
                                         "OSDisk": null
                                       }
        DataDiskNames                : {DB2-datadisk-1, DB2-datadisk-2}
        NetworkInterfaceIDs          :
        RequestId                    :
        StatusCode                   : 0
        EndTime             : [Date] [Time]
        Error               :
        Output              :
        StartTime           : [Date] [Time]
        Status              : Succeeded
        TrackingOperationId : xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
        RequestId           : xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
        StatusCode          : OK
