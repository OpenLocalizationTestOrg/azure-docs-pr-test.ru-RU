---
title: "aaaUse диагностики tooenable Azure PowerShell на виртуальной Машине Windows | Документы Microsoft"
services: virtual-machines-windows
documentationcenter: 
description: "Узнайте, как tooenable PowerShell toouse диагностики Azure в виртуальной машине под управлением Windows"
author: sbtron
manager: timlt
editor: 
ms.assetid: 2e6d88f2-1980-4a24-827e-a81616a0d247
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 12/15/2015
ms.author: saurabh
ms.openlocfilehash: e945f0de154b5ba600f845f0d577b48e2254573b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooenable-azure-diagnostics-in-a-virtual-machine-running-windows"></a><span data-ttu-id="a89bf-103">Использовать диагностику Azure tooenable PowerShell на виртуальной машине под управлением Windows</span><span class="sxs-lookup"><span data-stu-id="a89bf-103">Use PowerShell tooenable Azure Diagnostics in a virtual machine running Windows</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="a89bf-104">Система диагностики Azure — возможность hello в Azure, которая включает hello сбор диагностических данных с развернутым приложением.</span><span class="sxs-lookup"><span data-stu-id="a89bf-104">Azure Diagnostics is hello capability within Azure that enables hello collection of diagnostic data on a deployed application.</span></span> <span data-ttu-id="a89bf-105">Можно использовать hello диагностики расширения toocollect диагностических данных как журналы приложения или счетчики производительности из виртуальной машины Azure (ВМ) под управлением Windows.</span><span class="sxs-lookup"><span data-stu-id="a89bf-105">You can use hello diagnostics extension toocollect diagnostic data like application logs or performance counters from an Azure virtual machine (VM) that is running Windows.</span></span> <span data-ttu-id="a89bf-106">В этой статье описывается, как Windows PowerShell tooenable toouse hello расширения диагностики для виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="a89bf-106">This article describes how toouse Windows PowerShell tooenable hello diagnostics extension for a VM.</span></span> <span data-ttu-id="a89bf-107">В разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview) для hello предварительных требований для этой статьи.</span><span class="sxs-lookup"><span data-stu-id="a89bf-107">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for hello prerequisites needed for this article.</span></span>

## <a name="enable-hello-diagnostics-extension-if-you-use-hello-resource-manager-deployment-model"></a><span data-ttu-id="a89bf-108">Включить расширение диагностики hello при использовании модели развертывания диспетчера ресурсов hello</span><span class="sxs-lookup"><span data-stu-id="a89bf-108">Enable hello diagnostics extension if you use hello Resource Manager deployment model</span></span>
<span data-ttu-id="a89bf-109">При создании ВМ Windows с помощью модели развертывания диспетчера ресурсов Azure hello путем добавления шаблона диспетчера ресурсов toohello конфигурации расширения hello можно включить расширение диагностики hello.</span><span class="sxs-lookup"><span data-stu-id="a89bf-109">You can enable hello diagnostics extension while you create a Windows VM through hello Azure Resource Manager deployment model by adding hello extension configuration toohello Resource Manager template.</span></span> <span data-ttu-id="a89bf-110">В разделе [Создание виртуальной машины Windows с помощью мониторинга и диагностики с помощью шаблона Azure Resource Manager hello](extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a89bf-110">See [Create a Windows virtual machine with monitoring and diagnostics by using hello Azure Resource Manager template](extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="a89bf-111">расширение диагностики tooenable hello в существующей виртуальной Машины, которая была создана с помощью модели развертывания диспетчера ресурсов hello, можно использовать hello [AzureRMVMDiagnosticsExtension набор](/powershell/module/azurerm.compute/set-azurermvmdiagnosticsextension) командлета PowerShell, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="a89bf-111">tooenable hello diagnostics extension on an existing VM that was created through hello Resource Manager deployment model, you can use hello [Set-AzureRMVMDiagnosticsExtension](/powershell/module/azurerm.compute/set-azurermvmdiagnosticsextension) PowerShell cmdlet as shown below.</span></span>

    $vm_resourcegroup = "myvmresourcegroup"
    $vm_name = "myvm"
    $diagnosticsconfig_path = "DiagnosticsPubConfig.xml"

    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name -DiagnosticsConfigurationPath $diagnosticsconfig_path


<span data-ttu-id="a89bf-112">*$diagnosticsconfig_path* — hello путь toohello файл, содержащий конфигурацию диагностики hello в формате XML, как описано в hello [пример](#sample-diagnostics-configuration) ниже.</span><span class="sxs-lookup"><span data-stu-id="a89bf-112">*$diagnosticsconfig_path* is hello path toohello file that contains hello diagnostics configuration in XML, as described in hello [sample](#sample-diagnostics-configuration) below.</span></span>  

<span data-ttu-id="a89bf-113">Если файл конфигурации диагностики hello указывает **StorageAccount** элемент с именем учетной записи хранилища, затем hello *AzureRMVMDiagnosticsExtension набор* hello будет автоматически задан сценарий расширение toosend диагностических данных toothat учетная запись хранения диагностики.</span><span class="sxs-lookup"><span data-stu-id="a89bf-113">If hello diagnostics configuration file specifies a **StorageAccount** element with a storage account name, then hello *Set-AzureRMVMDiagnosticsExtension* script will automatically set hello diagnostics extension toosend diagnostic data toothat storage account.</span></span> <span data-ttu-id="a89bf-114">Для этого toowork учетной записи хранилища hello должен toobe в hello той же подписке, как hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="a89bf-114">For this toowork, hello storage account needs toobe in hello same subscription as hello VM.</span></span>

<span data-ttu-id="a89bf-115">Если не **StorageAccount** был указан в конфигурации диагностики hello, то вы должны toopass в hello *StorageAccountName* параметра toohello командлета.</span><span class="sxs-lookup"><span data-stu-id="a89bf-115">If no **StorageAccount** was specified in hello diagnostics configuration, then you need toopass in hello *StorageAccountName* parameter toohello cmdlet.</span></span> <span data-ttu-id="a89bf-116">Если hello *StorageAccountName* параметр указан, то hello командлет будет всегда использовать учетную запись хранения hello, указанный в параметре hello и не hello, указанный в файле конфигурации диагностики hello.</span><span class="sxs-lookup"><span data-stu-id="a89bf-116">If hello *StorageAccountName* parameter is specified, then hello cmdlet will always use hello storage account that is specified in hello parameter and not hello one that is specified in hello diagnostics configuration file.</span></span>

<span data-ttu-id="a89bf-117">Если учетная запись хранения — в другой подписке из hello виртуальной Машины, потребуется tooexplicitly диагностики hello проходит hello *StorageAccountName* и *StorageAccountKey* toohello командлет параметры.</span><span class="sxs-lookup"><span data-stu-id="a89bf-117">If hello diagnostics storage account is in a different subscription from hello VM, then you need tooexplicitly pass in hello *StorageAccountName* and *StorageAccountKey* parameters toohello cmdlet.</span></span> <span data-ttu-id="a89bf-118">Hello *StorageAccountKey* параметр не требуется, если учетной записи хранения диагностики hello hello одной подписке, как командлет hello автоматически можно запрашивать и устанавливать значение ключа hello, при включении расширения диагностики hello.</span><span class="sxs-lookup"><span data-stu-id="a89bf-118">hello *StorageAccountKey* parameter is not needed when hello diagnostics storage account is in hello same subscription, as hello cmdlet can automatically query and set hello key value when enabling hello diagnostics extension.</span></span> <span data-ttu-id="a89bf-119">Однако если hello учетная запись хранения диагностики — в другой подписке, а затем hello командлет может быть ключ hello tooget может автоматически и требуется tooexplicitly укажите ключ hello через hello *StorageAccountKey* параметр.</span><span class="sxs-lookup"><span data-stu-id="a89bf-119">However, if hello diagnostics storage account is in a different subscription, then hello cmdlet might not be able tooget hello key automatically and you need tooexplicitly specify hello key through hello *StorageAccountKey* parameter.</span></span>  

    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name -DiagnosticsConfigurationPath $diagnosticsconfig_path -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key

<span data-ttu-id="a89bf-120">После включения расширения диагностики hello на виртуальной Машине hello текущие настройки можно получить с помощью hello [Get AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/get-azurermvmdiagnosticsextension) командлета.</span><span class="sxs-lookup"><span data-stu-id="a89bf-120">Once hello diagnostics extension is enabled on a VM, you can get hello current settings by using hello [Get-AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/get-azurermvmdiagnosticsextension) cmdlet.</span></span>

    Get-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name

<span data-ttu-id="a89bf-121">Hello командлет возвращает *PublicSettings*, который содержит конфигурацию диагностики hello.</span><span class="sxs-lookup"><span data-stu-id="a89bf-121">hello cmdlet returns *PublicSettings*, which contains hello diagnostics configuration.</span></span> <span data-ttu-id="a89bf-122">Поддерживаются два типа конфигурации: WadCfg и xmlCfg.</span><span class="sxs-lookup"><span data-stu-id="a89bf-122">There are two kinds of configuration supported, WadCfg and xmlCfg.</span></span> <span data-ttu-id="a89bf-123">WadCfg — это конфигурации JSON, а xmlCfg — это конфигурация XML в кодировке Base64.</span><span class="sxs-lookup"><span data-stu-id="a89bf-123">WadCfg is JSON configuration, and xmlCfg is XML configuration in a Base64-encoded format.</span></span> <span data-ttu-id="a89bf-124">tooread Здравствуйте XML, необходимо toodecode его.</span><span class="sxs-lookup"><span data-stu-id="a89bf-124">tooread hello XML, you need toodecode it.</span></span>

    $publicsettings = (Get-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name).PublicSettings
    $encodedconfig = (ConvertFrom-Json -InputObject $publicsettings).xmlCfg
    $xmlconfig = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($encodedconfig))
    Write-Host $xmlconfig

<span data-ttu-id="a89bf-125">Hello [AzureRMVmDiagnosticsExtension удаление](/powershell/module/azurerm.compute/remove-azurermvmdiagnosticsextension) командлет может быть расширения диагностики используется tooremove hello из hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="a89bf-125">hello [Remove-AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/remove-azurermvmdiagnosticsextension) cmdlet can be used tooremove hello diagnostics extension from hello VM.</span></span>  

## <a name="enable-hello-diagnostics-extension-if-you-use-hello-classic-deployment-model"></a><span data-ttu-id="a89bf-126">Включить расширение диагностики hello при использовании hello классической модели развертывания</span><span class="sxs-lookup"><span data-stu-id="a89bf-126">Enable hello diagnostics extension if you use hello classic deployment model</span></span>
<span data-ttu-id="a89bf-127">Можно использовать hello [AzureVMDiagnosticsExtension набор](/powershell/module/azure/set-azurevmdiagnosticsextension) tooenable командлет расширения диагностики в ВМ, созданный с помощью hello классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="a89bf-127">You can use hello [Set-AzureVMDiagnosticsExtension](/powershell/module/azure/set-azurevmdiagnosticsextension) cmdlet tooenable a diagnostics extension on a VM that you create through hello classic deployment model.</span></span> <span data-ttu-id="a89bf-128">Hello следующем примере показано, как toocreate новой виртуальной Машины через hello классической модели развертывания с расширением диагностики hello включена.</span><span class="sxs-lookup"><span data-stu-id="a89bf-128">hello following example shows how toocreate a new VM through hello classic deployment model with hello diagnostics extension enabled.</span></span>

    $VM = New-AzureVMConfig -Name $VM -InstanceSize Small -ImageName $VMImage
    $VM = Add-AzureProvisioningConfig -VM $VM -AdminUsername $Username -Password $Password -Windows
    $VM = Set-AzureVMDiagnosticsExtension -DiagnosticsConfigurationPath $Config_Path -VM $VM -StorageContext $Storage_Context
    New-AzureVM -Location $Location -ServiceName $Service_Name -VM $VM

<span data-ttu-id="a89bf-129">расширение диагностики tooenable hello в существующей виртуальной Машины, который был создан при помощи hello классической модели развертывания, hello первого использования [Get-AzureVM](/powershell/module/azure/get-azurevm) конфигурацию виртуальной Машины hello tooget командлета.</span><span class="sxs-lookup"><span data-stu-id="a89bf-129">tooenable hello diagnostics extension on an existing VM that was created through hello classic deployment model, first use hello [Get-AzureVM](/powershell/module/azure/get-azurevm) cmdlet tooget hello VM configuration.</span></span> <span data-ttu-id="a89bf-130">Обновите модуль диагностики hello tooinclude configuration hello виртуальной Машины с помощью hello [AzureVMDiagnosticsExtension набор](/powershell/module/azure/set-azurevmdiagnosticsextension) командлета.</span><span class="sxs-lookup"><span data-stu-id="a89bf-130">Then update hello VM configuration tooinclude hello diagnostics extension by using hello [Set-AzureVMDiagnosticsExtension](/powershell/module/azure/set-azurevmdiagnosticsextension) cmdlet.</span></span> <span data-ttu-id="a89bf-131">Наконец, примените toohello hello обновить конфигурацию виртуальной Машины с помощью [Update-AzureVM](/powershell/module/azure/update-azurevm).</span><span class="sxs-lookup"><span data-stu-id="a89bf-131">Finally, apply hello updated configuration toohello VM by using [Update-AzureVM](/powershell/module/azure/update-azurevm).</span></span>

    $VM = Get-AzureVM -ServiceName $Service_Name -Name $VM_Name
    $VM_Update = Set-AzureVMDiagnosticsExtension -DiagnosticsConfigurationPath $Config_Path -VM $VM -StorageContext $Storage_Context
    Update-AzureVM -ServiceName $Service_Name -Name $VM_Name -VM $VM_Update.VM

## <a name="sample-diagnostics-configuration"></a><span data-ttu-id="a89bf-132">Пример конфигурации диагностики</span><span class="sxs-lookup"><span data-stu-id="a89bf-132">Sample diagnostics configuration</span></span>
<span data-ttu-id="a89bf-133">Здравствуйте, следующий XML-код можно использовать для настройки общих hello диагностики с hello выше сценариев.</span><span class="sxs-lookup"><span data-stu-id="a89bf-133">hello following XML can be used for hello diagnostics public configuration with hello above scripts.</span></span> <span data-ttu-id="a89bf-134">Этот пример конфигурации будут перенесены из системы диагностики hello различных производительности счетчики toohello учетная запись хранения диагностики, вместе с ошибок приложения hello, безопасности и система каналов в журналы событий Windows hello и любые ошибки журналы инфраструктуры.</span><span class="sxs-lookup"><span data-stu-id="a89bf-134">This sample configuration will transfer various performance counters toohello diagnostics storage account, along with errors from hello application, security, and system channels in hello Windows event logs and any errors from hello diagnostics infrastructure logs.</span></span>

<span data-ttu-id="a89bf-135">Hello конфигурации необходимы следующие hello обновленные tooinclude toobe:</span><span class="sxs-lookup"><span data-stu-id="a89bf-135">hello configuration needs toobe updated tooinclude hello following:</span></span>

* <span data-ttu-id="a89bf-136">Hello *resourceID* атрибут hello **метрики** элемент должен toobe обновляется hello ресурс с Идентификатором hello виртуальной Машины.</span><span class="sxs-lookup"><span data-stu-id="a89bf-136">hello *resourceID* attribute of hello **Metrics** element needs toobe updated with hello resource ID for hello VM.</span></span>
  
  * <span data-ttu-id="a89bf-137">Здравствуйте, используя следующий шаблон hello можно сконструировать идентификатор ресурса: «/ subscriptions / {*идентификатор подписки для подписки hello с hello ВМ*} /resourceGroups/ {*имя hello группа ресурсов для виртуальной Машиныhello*} / providers/Microsoft.Compute/virtualMachines/ {*hello имя виртуальной Машины*}».</span><span class="sxs-lookup"><span data-stu-id="a89bf-137">hello resource ID can be constructed by using hello following pattern: "/subscriptions/{*subscription ID for hello subscription with hello VM*}/resourceGroups/{*hello resourcegroup name for hello VM*}/providers/Microsoft.Compute/virtualMachines/{*hello VM Name*}".</span></span>
  * <span data-ttu-id="a89bf-138">Например, если hello идентификатор подписки для подписки hello, где hello ВМ работает — **11111111-1111-1111-1111-111111111111**, hello имя группы ресурсов для группы ресурсов hello **MyResourceGroup**, а hello имя виртуальной Машины — **MyWindowsVM**, затем hello значение *resourceID* будет:</span><span class="sxs-lookup"><span data-stu-id="a89bf-138">For example, if hello subscription ID for hello subscription where hello VM is running is **11111111-1111-1111-1111-111111111111**, hello resource group name for hello resource group is **MyResourceGroup**, and hello VM Name is **MyWindowsVM**, then hello value for *resourceID* would be:</span></span>
    
      ```
      <Metrics resourceId="/subscriptions/11111111-1111-1111-1111-111111111111/resourceGroups/MyResourceGroup/providers/Microsoft.Compute/virtualMachines/MyWindowsVM" >
      ```
  * <span data-ttu-id="a89bf-139">Дополнительные сведения о том, как показатели, созданный на основе hello счетчики производительности и показатели конфигурации см. в разделе [таблице показателей диагностики Azure в хранилище](extensions-diagnostics-template.md#wadmetrics-tables-in-storage).</span><span class="sxs-lookup"><span data-stu-id="a89bf-139">For more information on how metrics are generated based on hello performance counters and metrics configuration, see [Azure Diagnostics metrics table in storage](extensions-diagnostics-template.md#wadmetrics-tables-in-storage).</span></span>
* <span data-ttu-id="a89bf-140">Hello **StorageAccount** элемент должен toobe обновляется hello имя учетной записи хранения диагностики hello.</span><span class="sxs-lookup"><span data-stu-id="a89bf-140">hello **StorageAccount** element needs toobe updated with hello name of hello diagnostics storage account.</span></span>
  
    ```
    <?xml version="1.0" encoding="utf-8"?>
    <PublicConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
        <WadCfg>
          <DiagnosticMonitorConfiguration overallQuotaInMB="4096">
            <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter="Error"/>
            <PerformanceCounters scheduledTransferPeriod="PT1M">
          <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="CPU utilization" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Privileged Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="CPU privileged time" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% User Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="CPU user time" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Processor Information(_Total)\Processor Frequency" sampleRate="PT15S" unit="Count">
            <annotation displayName="CPU frequency" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\System\Processes" sampleRate="PT15S" unit="Count">
            <annotation displayName="Processes" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Process(_Total)\Thread Count" sampleRate="PT15S" unit="Count">
            <annotation displayName="Threads" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Process(_Total)\Handle Count" sampleRate="PT15S" unit="Count">
            <annotation displayName="Handles" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\% Committed Bytes In Use" sampleRate="PT15S" unit="Percent">
            <annotation displayName="Memory usage" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Available Bytes" sampleRate="PT15S" unit="Bytes">
            <annotation displayName="Memory available" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Committed Bytes" sampleRate="PT15S" unit="Bytes">
            <annotation displayName="Memory committed" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Commit Limit" sampleRate="PT15S" unit="Bytes">
            <annotation displayName="Memory commit limit" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Pool Paged Bytes" sampleRate="PT15S" unit="Bytes">
            <annotation displayName="Memory paged pool" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Pool Nonpaged Bytes" sampleRate="PT15S" unit="Bytes">
            <annotation displayName="Memory non-paged pool" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\% Disk Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="Disk active time" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\% Disk Read Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="Disk active read time" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\% Disk Write Time" sampleRate="PT15S" unit="Percent">
            <annotation displayName="Disk active write time" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Transfers/sec" sampleRate="PT15S" unit="CountPerSecond">
            <annotation displayName="Disk operations" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Reads/sec" sampleRate="PT15S" unit="CountPerSecond">
            <annotation displayName="Disk read operations" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Writes/sec" sampleRate="PT15S" unit="CountPerSecond">
            <annotation displayName="Disk write operations" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Bytes/sec" sampleRate="PT15S" unit="BytesPerSecond">
            <annotation displayName="Disk speed" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Read Bytes/sec" sampleRate="PT15S" unit="BytesPerSecond">
            <annotation displayName="Disk read speed" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Disk Write Bytes/sec" sampleRate="PT15S" unit="BytesPerSecond">
            <annotation displayName="Disk write speed" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Avg. Disk Queue Length" sampleRate="PT15S" unit="Count">
            <annotation displayName="Disk average queue length" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Avg. Disk Read Queue Length" sampleRate="PT15S" unit="Count">
            <annotation displayName="Disk average read queue length" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\PhysicalDisk(_Total)\Avg. Disk Write Queue Length" sampleRate="PT15S" unit="Count">
            <annotation displayName="Disk average write queue length" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\LogicalDisk(_Total)\% Free Space" sampleRate="PT15S" unit="Percent">
            <annotation displayName="Disk free space (percentage)" locale="en-us"/>
          </PerformanceCounterConfiguration>
          <PerformanceCounterConfiguration counterSpecifier="\LogicalDisk(_Total)\Free Megabytes" sampleRate="PT15S" unit="Count">
            <annotation displayName="Disk free space (MB)" locale="en-us"/>
          </PerformanceCounterConfiguration>
        </PerformanceCounters>
        <Metrics resourceId="(Update with resource ID for hello VM)" >
            <MetricAggregation scheduledTransferPeriod="PT1H"/>
            <MetricAggregation scheduledTransferPeriod="PT1M"/>
        </Metrics>
        <WindowsEventLog scheduledTransferPeriod="PT1M">
          <DataSource name="Application!*[System[(Level = 1 or Level = 2)]]"/>
          <DataSource name="Security!*[System[(Level = 1 or Level = 2)]"/>
          <DataSource name="System!*[System[(Level = 1 or Level = 2)]]"/>
        </WindowsEventLog>
          </DiagnosticMonitorConfiguration>
        </WadCfg>
        <StorageAccount>(Update with diagnostics storage account name)</StorageAccount>
    </PublicConfig>
    ```

## <a name="next-steps"></a><span data-ttu-id="a89bf-141">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a89bf-141">Next steps</span></span>
* <span data-ttu-id="a89bf-142">Дополнительные рекомендации по использованию возможностей диагностики Azure hello и других проблем tootroubleshoot методы. в разделе [включение диагностики в облачных службах Azure и виртуальные машины](../../cloud-services/cloud-services-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="a89bf-142">For additional guidance on using hello Azure Diagnostics capability and other techniques tootroubleshoot problems, see [Enabling Diagnostics in Azure Cloud Services and Virtual Machines](../../cloud-services/cloud-services-dotnet-diagnostics.md).</span></span>
* <span data-ttu-id="a89bf-143">[Схема конфигурации диагностики](https://msdn.microsoft.com/library/azure/mt634524.aspx) объясняет различные конфигурации XML параметры для расширения диагностики hello hello.</span><span class="sxs-lookup"><span data-stu-id="a89bf-143">[Diagnostics configurations schema](https://msdn.microsoft.com/library/azure/mt634524.aspx) explains hello various XML configurations options for hello diagnostics extension.</span></span>

