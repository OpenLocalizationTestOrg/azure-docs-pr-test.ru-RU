---
title: "виртуальные машины в наборе масштабирования виртуальных машин aaaManage | Документы Microsoft"
description: "Узнайте, как управлять виртуальными машинами в наборе масштабирования виртуальных машин с помощью Azure PowerShell."
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d35fa77a-de96-4ccd-a332-eb181d1f4273
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/27/2016
ms.author: adegeo
ms.openlocfilehash: 7d848729c0fc708bd596b61feb528cf4bf4bafd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-virtual-machines-in-a-virtual-machine-scale-set"></a><span data-ttu-id="47e21-103">Управление виртуальными машинами в масштабируемом наборе виртуальных машин</span><span class="sxs-lookup"><span data-stu-id="47e21-103">Manage virtual machines in a virtual machine scale set</span></span>
<span data-ttu-id="47e21-104">Использование задач hello в этой статье toomanage виртуальных машин в ваш набор масштабирования виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="47e21-104">Use hello tasks in this article toomanage virtual machines in your virtual machine scale set.</span></span>

<span data-ttu-id="47e21-105">Большинство задач hello, которые включают управление виртуальной машины в наборе масштабирования требуют знания hello идентификатор экземпляра, которые должны toomanage машины hello.</span><span class="sxs-lookup"><span data-stu-id="47e21-105">Most of hello tasks that involve managing a virtual machine in a scale set require that you know hello instance ID of hello machine that you want toomanage.</span></span> <span data-ttu-id="47e21-106">Можно использовать [обозревателя ресурсов Azure](https://resources.azure.com) toofind hello идентификатор экземпляра виртуальной машины в наборе масштабирования.</span><span class="sxs-lookup"><span data-stu-id="47e21-106">You can use [Azure Resource Explorer](https://resources.azure.com) toofind hello instance ID of a virtual machine in a scale set.</span></span> <span data-ttu-id="47e21-107">Вы также использовать обозреватель ресурсов tooverify hello состояние завершения задач hello.</span><span class="sxs-lookup"><span data-stu-id="47e21-107">You also use Resource Explorer tooverify hello status of hello tasks that you finish.</span></span>

<span data-ttu-id="47e21-108">В разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview) сведения об установке hello последнюю версию Azure PowerShell, выбрав подписку и вход в учетную запись tooyour.</span><span class="sxs-lookup"><span data-stu-id="47e21-108">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for information about installing hello latest version of Azure PowerShell, selecting your subscription, and signing in tooyour account.</span></span>

## <a name="display-information-about-a-scale-set"></a><span data-ttu-id="47e21-109">Отображение информации о масштабируемом наборе</span><span class="sxs-lookup"><span data-stu-id="47e21-109">Display information about a scale set</span></span>
<span data-ttu-id="47e21-110">Можно получить общие сведения о наборе масштабирования, который также является tooas, который ссылается представление экземпляра hello.</span><span class="sxs-lookup"><span data-stu-id="47e21-110">You can get general information about a scale set, which is also referred tooas hello instance view.</span></span> <span data-ttu-id="47e21-111">Также можно получить более подробные сведения, такие как сведения о ресурсах hello в наборе масштабирования hello.</span><span class="sxs-lookup"><span data-stu-id="47e21-111">Or, you can get more specific information, such as information about hello resources in hello scale set.</span></span>

<span data-ttu-id="47e21-112">Замените значения с именем hello или группа ресурсов и масштабирования, установите и запустите команду hello hello:</span><span class="sxs-lookup"><span data-stu-id="47e21-112">Replace hello quoted values with hello name or your resource group and scale set and then run hello command:</span></span>

    Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name"

<span data-ttu-id="47e21-113">Результат буде выглядеть примерно так:</span><span class="sxs-lookup"><span data-stu-id="47e21-113">It returns something like this:</span></span>

    Id                                          : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Compute/virtualMachineScaleSets/myvmss1
    Name                                        : myvmss1
    Type                                        : Microsoft.Compute/virtualMachineScaleSets
    Location                                    : centralus
    Sku                                         :
      Name                                      : Standard_A0
      Tier                                      : Standard
      Capacity                                  : 3
    UpgradePolicy                               :
      Mode                                      : Manual
    VirtualMachineProfile                       :
      OsProfile                                 :
        ComputerNamePrefix                      : vmss1
        AdminUsername                           : admin1
        WindowsConfiguration                    :
          ProvisionVMAgent                      : True
          EnableAutomaticUpdates                : True
    StorageProfile                              :
      ImageReference                            :
        Publisher                               : MicrosoftWindowsServer
        Offer                                   : WindowsServer
        Sku                                     : 2012-R2-Datacenter
        Version                                 : latest
      OsDisk                                    :
        Name                                    : vmssosdisk
        Caching                                 : ReadOnly
        CreateOption                            : FromImage
        VhdContainers[0]                        : https://astore.blob.core.windows.net/vmss
        VhdContainers[1]                        : https://gstore.blob.core.windows.net/vmss
        VhdContainers[2]                        : https://mstore.blob.core.windows.net/vmss
        VhdContainers[3]                        : https://sstore.blob.core.windows.net/vmss
        VhdContainers[4]                        : https://ystore.blob.core.windows.net/vmss
    NetworkProfile                              :
      NetworkInterfaceConfigurations[0]         :
        Name                                    : mync1
        Primary                                 : True
        IpConfigurations[0]                     :
          Name                                  : ip1
          Subnet                                :
            Id                                  : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Network/virtualNetworks/myvn1/subnets/mysn1
          LoadBalancerBackendAddressPools[0]    :
            Id                                  : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Network/loadBalancers/mylb1/backendAddressPools/bepool1
        LoadBalancerInboundNatPools[0]          :
            Id                                  : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Network/loadBalancers/mylb1/inboundNatPools/natpool1
    ExtensionProfile                            :
      Extensions[0]                             :
        Name                                    : Microsoft.Insights.VMDiagnosticsSettings
        Publisher                               : Microsoft.Azure.Diagnostics
        Type                                    : IaaSDiagnostics
        TypeHandlerVersion                      : 1.5
        AutoUpgradeMinorVersion                 : True
        Settings                                : {"xmlCfg":"...","storageAccount":"astore"}
    ProvisioningState                           : Succeeded

<span data-ttu-id="47e21-114">Замените значения с именем hello набора ресурсов группы и масштаб hello.</span><span class="sxs-lookup"><span data-stu-id="47e21-114">Replace hello quoted values with hello name of your resource group and scale set.</span></span> <span data-ttu-id="47e21-115">Замените  *#*  с идентификатором hello экземпляр виртуальной машины hello интересующий tooget и запустите его:</span><span class="sxs-lookup"><span data-stu-id="47e21-115">Replace *#* with hello instance identifier of hello virtual machine that you want tooget information about and then run it:</span></span>

    Get-AzureRmVmssVM -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

<span data-ttu-id="47e21-116">Результат будет выглядеть примерно так:</span><span class="sxs-lookup"><span data-stu-id="47e21-116">It returns something like this example:</span></span>

    Id                            : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Compute/
                                    virtualMachineScaleSets/myvmss1/virtualMachines/0
    Name                          : myvmss1_0
    Type                          : Microsoft.Compute/virtualMachineScaleSets/virtualMachines
    Location                      : centralus
    InstanceId                    : 0
    Sku                           :
      Name                        : Standard_A0
      Tier                        : Standard
    LatestModelApplied            : True
    StorageProfile                :
      ImageReference              :
        Publisher                 : MicrosoftWindowsServer
        Offer                     : WindowsServer
        Sku                       : 2012-R2-Datacenter
        Version                   : 4.0.20160617
      OsDisk                      :
        OsType                    : Windows
        Name                      : vmssosdisk-os-0-e11cad52959b4b76a8d9f26c5190c4f8
        Vhd                       :
          Uri                     : https://astore.blob.core.windows.net/vmss/vmssosdisk-os-0-e11cad52959b4b76a8d9f26c5190c4f8.vhd
        Caching                   : ReadOnly
        CreateOption              : FromImage
    OsProfile                     :
      ComputerName                : myvmss1-0
      AdminUsername               : admin1
      WindowsConfiguration        :
        ProvisionVMAgent          : True
        EnableAutomaticUpdates    : True
    NetworkProfile                :
      NetworkInterfaces[0]        :
        Id                        : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Compute/virtualMachineScaleSets/
                                    myvmss1/virtualMachines/0/networkInterfaces/mync1
    ProvisioningState             : Succeeded
    Resources[0]                  :
      Id                          : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Compute/virtualMachines/
                                    myvmss1_0/extensions/Microsoft.Insights.VMDiagnosticsSettings
      Name                        : Microsoft.Insights.VMDiagnosticsSettings
      Type                        : Microsoft.Compute/virtualMachines/extensions
      Location                    : centralus
      Publisher                   : Microsoft.Azure.Diagnostics
      VirtualMachineExtensionType : IaaSDiagnostics
      TypeHandlerVersion          : 1.5
      AutoUpgradeMinorVersion     : True
      Settings                    : {"xmlCfg":"...","storageAccount":"astore"}
      ProvisioningState           : Succeeded

## <a name="start-a-virtual-machine-in-a-scale-set"></a><span data-ttu-id="47e21-117">Запуск виртуальной машины в наборе масштабирования</span><span class="sxs-lookup"><span data-stu-id="47e21-117">Start a virtual machine in a scale set</span></span>
<span data-ttu-id="47e21-118">Замените значения с именем hello набора ресурсов группы и масштаб hello.</span><span class="sxs-lookup"><span data-stu-id="47e21-118">Replace hello quoted values with hello name of your resource group and scale set.</span></span> <span data-ttu-id="47e21-119">Замените  *#*  с идентификатором hello hello виртуальной машины требуется toostart и запустите его:</span><span class="sxs-lookup"><span data-stu-id="47e21-119">Replace *#* with hello identifier of hello virtual machine that you want toostart and then run it:</span></span>

    Start-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

<span data-ttu-id="47e21-120">В обозревателе ресурсов, мы видим, что находится в состоянии hello hello экземпляра **под управлением**:</span><span class="sxs-lookup"><span data-stu-id="47e21-120">In Resource Explorer, we can see that hello status of hello instance is **running**:</span></span>

    "statuses": [
      {
        "code": "ProvisioningState/succeeded",
        "level": "Info",
        "displayStatus": "Provisioning succeeded",
        "time": "2016-03-15T02:10:08.0730839+00:00"
      },
      {
        "code": "PowerState/running",
        "level": "Info",
        "displayStatus": "VM running"
      }
    ]

<span data-ttu-id="47e21-121">Можно запустить все виртуальные машины hello в наборе с помощью параметра - InstanceId hello не масштабирования hello.</span><span class="sxs-lookup"><span data-stu-id="47e21-121">You can start all hello virtual machines in hello scale set by not using hello -InstanceId parameter.</span></span>

## <a name="stop-a-virtual-machine-in-a-scale-set"></a><span data-ttu-id="47e21-122">Остановка виртуальной машины в наборе масштабирования</span><span class="sxs-lookup"><span data-stu-id="47e21-122">Stop a virtual machine in a scale set</span></span>
<span data-ttu-id="47e21-123">Замените значения с именем hello набора ресурсов группы и масштаб hello.</span><span class="sxs-lookup"><span data-stu-id="47e21-123">Replace hello quoted values with hello name of your resource group and scale set.</span></span> <span data-ttu-id="47e21-124">Замените  *#*  с идентификатором hello hello виртуальной машины требуется toostop и запустите его:</span><span class="sxs-lookup"><span data-stu-id="47e21-124">Replace *#* with hello identifier of hello virtual machine that you want toostop and then run it:</span></span>

    Stop-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

<span data-ttu-id="47e21-125">В обозревателе ресурсов, мы видим, что находится в состоянии hello hello экземпляра **освобождена**:</span><span class="sxs-lookup"><span data-stu-id="47e21-125">In Resource Explorer, we can see that hello status of hello instance is **deallocated**:</span></span>

    "statuses": [
      {
        "code": "ProvisioningState/succeeded",
        "level": "Info",
        "displayStatus": "Provisioning succeeded",
        "time": "2016-03-15T01:25:17.8792929+00:00"
      },
      {
        "code": "PowerState/deallocated",
        "level": "Info",
        "displayStatus": "VM deallocated"
      }
    ]

<span data-ttu-id="47e21-126">toostop виртуальной машины и не освободить его, используйте параметр - StayProvisioned hello.</span><span class="sxs-lookup"><span data-stu-id="47e21-126">toostop a virtual machine and not deallocate it, use hello -StayProvisioned parameter.</span></span> <span data-ttu-id="47e21-127">Вы можете остановить все виртуальные машины hello в устанавливается с помощью параметра - InstanceId hello не hello.</span><span class="sxs-lookup"><span data-stu-id="47e21-127">You can stop all hello virtual machines in hello set by not using hello -InstanceId parameter.</span></span>

## <a name="restart-a-virtual-machine-in-a-scale-set"></a><span data-ttu-id="47e21-128">Перезапуск виртуальной машины в наборе масштабирования</span><span class="sxs-lookup"><span data-stu-id="47e21-128">Restart a virtual machine in a scale set</span></span>
<span data-ttu-id="47e21-129">Замените значения с именем hello набора ресурсов группы и hello шкалы hello.</span><span class="sxs-lookup"><span data-stu-id="47e21-129">Replace hello quoted values with hello name of your resource group and hello scale set.</span></span> <span data-ttu-id="47e21-130">Замените  *#*  с идентификатором hello hello виртуальной машины требуется toorestart и запустите его:</span><span class="sxs-lookup"><span data-stu-id="47e21-130">Replace *#* with hello identifier of hello virtual machine that you want toorestart and then run it:</span></span>

    Restart-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

<span data-ttu-id="47e21-131">Можно перезапустить все виртуальные машины hello в устанавливается с помощью параметра - InstanceId hello не hello.</span><span class="sxs-lookup"><span data-stu-id="47e21-131">You can restart all hello virtual machines in hello set by not using hello -InstanceId parameter.</span></span>

## <a name="remove-a-virtual-machine-from-a-scale-set"></a><span data-ttu-id="47e21-132">Удаление виртуальной машины из набора масштабирования</span><span class="sxs-lookup"><span data-stu-id="47e21-132">Remove a virtual machine from a scale set</span></span>
<span data-ttu-id="47e21-133">Замените значения с именем hello набора ресурсов группы и hello шкалы hello.</span><span class="sxs-lookup"><span data-stu-id="47e21-133">Replace hello quoted values with hello name of your resource group and hello scale set.</span></span> <span data-ttu-id="47e21-134">Замените  *#*  с идентификатором hello hello виртуальной машины требуется tooremove и запустите его:</span><span class="sxs-lookup"><span data-stu-id="47e21-134">Replace *#* with hello identifier of hello virtual machine that you want tooremove and then run it:</span></span>  

    Remove-AzureRmVmss -ResourceGroupName "resource group name" –VMScaleSetName "scale set name" -InstanceId #

<span data-ttu-id="47e21-135">Hello масштабный набор виртуальных машин за один раз можно удалить, не с помощью параметра - InstanceId hello.</span><span class="sxs-lookup"><span data-stu-id="47e21-135">You can remove hello virtual machine scale set all at once by not using hello -InstanceId parameter.</span></span>

## <a name="change-hello-capacity-of-a-scale-set"></a><span data-ttu-id="47e21-136">Изменить hello емкость набора масштабирования</span><span class="sxs-lookup"><span data-stu-id="47e21-136">Change hello capacity of a scale set</span></span>
<span data-ttu-id="47e21-137">Можно добавить или убрать, изменив hello емкость hello набор виртуальных машин.</span><span class="sxs-lookup"><span data-stu-id="47e21-137">You can add or remove virtual machines by changing hello capacity of hello set.</span></span> <span data-ttu-id="47e21-138">Получите необходимый toochange набор hello емкость toowhat нужно toobe, а затем обновить набор масштабирования hello с новой емкости hello набор масштабирования hello.</span><span class="sxs-lookup"><span data-stu-id="47e21-138">Get hello scale set that you want toochange, set hello capacity toowhat you want it toobe, and then update hello scale set with hello new capacity.</span></span> <span data-ttu-id="47e21-139">В этих команд замените значения с именем hello набора ресурсов группы и hello шкалы hello.</span><span class="sxs-lookup"><span data-stu-id="47e21-139">In these commands, replace hello quoted values with hello name of your resource group and hello scale set.</span></span>

    $vmss = Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name"
    $vmss.sku.capacity = 5
    Update-AzureRmVmss -ResourceGroupName "resource group name" -Name "scale set name" -VirtualMachineScaleSet $vmss 

<span data-ttu-id="47e21-140">При удалении из hello масштабный набор виртуальных машин сначала удаляются hello виртуальных машин с высоким идентификаторы hello.</span><span class="sxs-lookup"><span data-stu-id="47e21-140">If you are removing virtual machines from hello scale set, hello virtual machines with hello highest ids are removed first.</span></span>

