---
title: "Использование Azure PowerShell для включения диагностики на виртуальной машине Windows | Документация Майкрософт"
services: virtual-machines-windows
documentationcenter: 
description: "Описание процедуры включения системы диагностики Azure на виртуальной машине под управлением Windows с помощью PowerShell."
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
ms.openlocfilehash: d0be4a712657edfc516c5f32e66519f5d9486728
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-enable-azure-diagnostics-in-a-virtual-machine-running-windows"></a><span data-ttu-id="d74f6-103">Включение системы диагностики Azure на виртуальной машине под управлением Windows с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="d74f6-103">Use PowerShell to enable Azure Diagnostics in a virtual machine running Windows</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="d74f6-104">Система диагностики Azure позволяет выполнять сбор диагностических данных в развернутом приложении.</span><span class="sxs-lookup"><span data-stu-id="d74f6-104">Azure Diagnostics is the capability within Azure that enables the collection of diagnostic data on a deployed application.</span></span> <span data-ttu-id="d74f6-105">Для сбора диагностических данных, таких как журналы приложений или счетчики производительности, на виртуальной машине Azure под управлением Windows можно использовать расширение диагностики.</span><span class="sxs-lookup"><span data-stu-id="d74f6-105">You can use the diagnostics extension to collect diagnostic data like application logs or performance counters from an Azure virtual machine (VM) that is running Windows.</span></span> <span data-ttu-id="d74f6-106">В этой статье описано, как включить расширения диагностики для виртуальной машины с помощью Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d74f6-106">This article describes how to use Windows PowerShell to enable the diagnostics extension for a VM.</span></span> <span data-ttu-id="d74f6-107">Сведения о компонентах, которые потребуются для выполнения инструкций в этой статье, см. в статье [Установка и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d74f6-107">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for the prerequisites needed for this article.</span></span>

## <a name="enable-the-diagnostics-extension-if-you-use-the-resource-manager-deployment-model"></a><span data-ttu-id="d74f6-108">Включения расширения диагностики при использовании модели развертывания диспетчера ресурсов</span><span class="sxs-lookup"><span data-stu-id="d74f6-108">Enable the diagnostics extension if you use the Resource Manager deployment model</span></span>
<span data-ttu-id="d74f6-109">Вы можете включить расширение диагностики при создании виртуальной машины Windows, используя модель развертывания диспетчера ресурсов Azure. Для этого в шаблон диспетчера ресурсов нужно добавить конфигурацию расширения.</span><span class="sxs-lookup"><span data-stu-id="d74f6-109">You can enable the diagnostics extension while you create a Windows VM through the Azure Resource Manager deployment model by adding the extension configuration to the Resource Manager template.</span></span> <span data-ttu-id="d74f6-110">Дополнительные сведения см. в статье [Создание виртуальной машины Windows с мониторингом и диагностикой с использованием шаблона диспетчера ресурсов Azure](extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d74f6-110">See [Create a Windows virtual machine with monitoring and diagnostics by using the Azure Resource Manager template](extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="d74f6-111">Чтобы включить расширение диагностики на уже существующей виртуальной машине, созданной с помощью модели развертывания диспетчера ресурсов, можно использовать командлет PowerShell [Set-AzureRMVMDiagnosticsExtension](/powershell/module/azurerm.compute/set-azurermvmdiagnosticsextension) , как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="d74f6-111">To enable the diagnostics extension on an existing VM that was created through the Resource Manager deployment model, you can use the [Set-AzureRMVMDiagnosticsExtension](/powershell/module/azurerm.compute/set-azurermvmdiagnosticsextension) PowerShell cmdlet as shown below.</span></span>

    $vm_resourcegroup = "myvmresourcegroup"
    $vm_name = "myvm"
    $diagnosticsconfig_path = "DiagnosticsPubConfig.xml"

    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name -DiagnosticsConfigurationPath $diagnosticsconfig_path


<span data-ttu-id="d74f6-112">*$diagnosticsconfig_path* — это путь к файлу с конфигурацией диагностики в формате XML, как показано в [примере](#sample-diagnostics-configuration) ниже.</span><span class="sxs-lookup"><span data-stu-id="d74f6-112">*$diagnosticsconfig_path* is the path to the file that contains the diagnostics configuration in XML, as described in the [sample](#sample-diagnostics-configuration) below.</span></span>  

<span data-ttu-id="d74f6-113">Если файл конфигурации диагностики содержит элемент **StorageAccount** с именем учетной записи хранения, сценарий *Set-AzureRMVMDiagnosticsExtension* автоматически настраивает для расширения диагностики отправку диагностических данных в эту учетную запись.</span><span class="sxs-lookup"><span data-stu-id="d74f6-113">If the diagnostics configuration file specifies a **StorageAccount** element with a storage account name, then the *Set-AzureRMVMDiagnosticsExtension* script will automatically set the diagnostics extension to send diagnostic data to that storage account.</span></span> <span data-ttu-id="d74f6-114">Для этого учетная запись хранения должна входить в ту же подписку, что и виртуальная машина.</span><span class="sxs-lookup"><span data-stu-id="d74f6-114">For this to work, the storage account needs to be in the same subscription as the VM.</span></span>

<span data-ttu-id="d74f6-115">Если в конфигурации диагностики нет элемента **StorageAccount** , в командлет необходимо передать параметр *StorageAccountName* .</span><span class="sxs-lookup"><span data-stu-id="d74f6-115">If no **StorageAccount** was specified in the diagnostics configuration, then you need to pass in the *StorageAccountName* parameter to the cmdlet.</span></span> <span data-ttu-id="d74f6-116">Если параметр *StorageAccountName* указан, командлет использует учетную запись хранения, указанную в этом параметре, а не в файле конфигурации диагностики.</span><span class="sxs-lookup"><span data-stu-id="d74f6-116">If the *StorageAccountName* parameter is specified, then the cmdlet will always use the storage account that is specified in the parameter and not the one that is specified in the diagnostics configuration file.</span></span>

<span data-ttu-id="d74f6-117">Если учетная запись хранения диагностики и виртуальная машина относятся к разным подпискам, то в командлет необходимо явно передать параметры *StorageAccountName* и *StorageAccountKey*.</span><span class="sxs-lookup"><span data-stu-id="d74f6-117">If the diagnostics storage account is in a different subscription from the VM, then you need to explicitly pass in the *StorageAccountName* and *StorageAccountKey* parameters to the cmdlet.</span></span> <span data-ttu-id="d74f6-118">Параметр *StorageAccountKey* не требуется, если учетная запись хранения диагностики входит в ту же подписку, так как при включении расширения диагностики командлет автоматически запрашивает и устанавливает значение ключа.</span><span class="sxs-lookup"><span data-stu-id="d74f6-118">The *StorageAccountKey* parameter is not needed when the diagnostics storage account is in the same subscription, as the cmdlet can automatically query and set the key value when enabling the diagnostics extension.</span></span> <span data-ttu-id="d74f6-119">Если же учетная запись хранения диагностики входит в другую подписку, командлет не сможет получить ключ автоматически, а значит, его необходимо явно указать с помощью параметра *StorageAccountKey* .</span><span class="sxs-lookup"><span data-stu-id="d74f6-119">However, if the diagnostics storage account is in a different subscription, then the cmdlet might not be able to get the key automatically and you need to explicitly specify the key through the *StorageAccountKey* parameter.</span></span>  

    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name -DiagnosticsConfigurationPath $diagnosticsconfig_path -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key

<span data-ttu-id="d74f6-120">После включения расширения диагностики на виртуальной машине получить текущие параметры можно с помощью командлета [Get-AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/get-azurermvmdiagnosticsextension) .</span><span class="sxs-lookup"><span data-stu-id="d74f6-120">Once the diagnostics extension is enabled on a VM, you can get the current settings by using the [Get-AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/get-azurermvmdiagnosticsextension) cmdlet.</span></span>

    Get-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name

<span data-ttu-id="d74f6-121">Командлет возвращает значение *PublicSettings*, содержащее конфигурацию диагностики.</span><span class="sxs-lookup"><span data-stu-id="d74f6-121">The cmdlet returns *PublicSettings*, which contains the diagnostics configuration.</span></span> <span data-ttu-id="d74f6-122">Поддерживаются два типа конфигурации: WadCfg и xmlCfg.</span><span class="sxs-lookup"><span data-stu-id="d74f6-122">There are two kinds of configuration supported, WadCfg and xmlCfg.</span></span> <span data-ttu-id="d74f6-123">WadCfg — это конфигурации JSON, а xmlCfg — это конфигурация XML в кодировке Base64.</span><span class="sxs-lookup"><span data-stu-id="d74f6-123">WadCfg is JSON configuration, and xmlCfg is XML configuration in a Base64-encoded format.</span></span> <span data-ttu-id="d74f6-124">Чтобы прочитать XML-файл, его необходимо декодировать.</span><span class="sxs-lookup"><span data-stu-id="d74f6-124">To read the XML, you need to decode it.</span></span>

    $publicsettings = (Get-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name).PublicSettings
    $encodedconfig = (ConvertFrom-Json -InputObject $publicsettings).xmlCfg
    $xmlconfig = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($encodedconfig))
    Write-Host $xmlconfig

<span data-ttu-id="d74f6-125">Для удаления расширения диагностики с виртуальной машины вы можете использовать командлет [Remove-AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/remove-azurermvmdiagnosticsextension) .</span><span class="sxs-lookup"><span data-stu-id="d74f6-125">The [Remove-AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/remove-azurermvmdiagnosticsextension) cmdlet can be used to remove the diagnostics extension from the VM.</span></span>  

## <a name="enable-the-diagnostics-extension-if-you-use-the-classic-deployment-model"></a><span data-ttu-id="d74f6-126">Включения расширения диагностики при использовании классической модели развертывания</span><span class="sxs-lookup"><span data-stu-id="d74f6-126">Enable the diagnostics extension if you use the classic deployment model</span></span>
<span data-ttu-id="d74f6-127">Включить расширение диагностики на виртуальной машине, созданной на основе классической модели развертывания, можно с помощью командлета [Set-AzureVMDiagnosticsExtension](/powershell/module/azure/set-azurevmdiagnosticsextension) .</span><span class="sxs-lookup"><span data-stu-id="d74f6-127">You can use the [Set-AzureVMDiagnosticsExtension](/powershell/module/azure/set-azurevmdiagnosticsextension) cmdlet to enable a diagnostics extension on a VM that you create through the classic deployment model.</span></span> <span data-ttu-id="d74f6-128">В следующем примере показано, как создать новую виртуальную машину, используя классическую модель развертывания при включенном расширении диагностики.</span><span class="sxs-lookup"><span data-stu-id="d74f6-128">The following example shows how to create a new VM through the classic deployment model with the diagnostics extension enabled.</span></span>

    $VM = New-AzureVMConfig -Name $VM -InstanceSize Small -ImageName $VMImage
    $VM = Add-AzureProvisioningConfig -VM $VM -AdminUsername $Username -Password $Password -Windows
    $VM = Set-AzureVMDiagnosticsExtension -DiagnosticsConfigurationPath $Config_Path -VM $VM -StorageContext $Storage_Context
    New-AzureVM -Location $Location -ServiceName $Service_Name -VM $VM

<span data-ttu-id="d74f6-129">Чтобы включить расширение диагностики на существующей виртуальной машине, созданной с помощью классической модели развертывания, сначала используйте командлет [Get-AzureVM](/powershell/module/azure/get-azurevm) , который позволит получить конфигурацию виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="d74f6-129">To enable the diagnostics extension on an existing VM that was created through the classic deployment model, first use the [Get-AzureVM](/powershell/module/azure/get-azurevm) cmdlet to get the VM configuration.</span></span> <span data-ttu-id="d74f6-130">Затем обновите конфигурацию виртуальной машины, чтобы активировать расширение диагностики, с помощью командлета [Set-AzureVMDiagnosticsExtension](/powershell/module/azure/set-azurevmdiagnosticsextension) .</span><span class="sxs-lookup"><span data-stu-id="d74f6-130">Then update the VM configuration to include the diagnostics extension by using the [Set-AzureVMDiagnosticsExtension](/powershell/module/azure/set-azurevmdiagnosticsextension) cmdlet.</span></span> <span data-ttu-id="d74f6-131">И, наконец, примените обновленную конфигурацию к виртуальной машине с помощью командлета [Update-AzureVM](/powershell/module/azure/update-azurevm).</span><span class="sxs-lookup"><span data-stu-id="d74f6-131">Finally, apply the updated configuration to the VM by using [Update-AzureVM](/powershell/module/azure/update-azurevm).</span></span>

    $VM = Get-AzureVM -ServiceName $Service_Name -Name $VM_Name
    $VM_Update = Set-AzureVMDiagnosticsExtension -DiagnosticsConfigurationPath $Config_Path -VM $VM -StorageContext $Storage_Context
    Update-AzureVM -ServiceName $Service_Name -Name $VM_Name -VM $VM_Update.VM

## <a name="sample-diagnostics-configuration"></a><span data-ttu-id="d74f6-132">Пример конфигурации диагностики</span><span class="sxs-lookup"><span data-stu-id="d74f6-132">Sample diagnostics configuration</span></span>
<span data-ttu-id="d74f6-133">Представленный ниже XML-код можно использовать для открытой конфигурации диагностики с применением описанных выше сценариев.</span><span class="sxs-lookup"><span data-stu-id="d74f6-133">The following XML can be used for the diagnostics public configuration with the above scripts.</span></span> <span data-ttu-id="d74f6-134">Конфигурация в данном примере передает в учетную запись хранения диагностических данных различные счетчики производительности вместе с ошибками из журналов приложений, событий безопасности и системных каналов в Windows, а также из журналов инфраструктуры диагностики.</span><span class="sxs-lookup"><span data-stu-id="d74f6-134">This sample configuration will transfer various performance counters to the diagnostics storage account, along with errors from the application, security, and system channels in the Windows event logs and any errors from the diagnostics infrastructure logs.</span></span>

<span data-ttu-id="d74f6-135">Конфигурацию необходимо обновить, чтобы включить в нее следующее:</span><span class="sxs-lookup"><span data-stu-id="d74f6-135">The configuration needs to be updated to include the following:</span></span>

* <span data-ttu-id="d74f6-136">Атрибут *resourceID* элемента **Metrics** необходимо обновить, указав идентификатор ресурса для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="d74f6-136">The *resourceID* attribute of the **Metrics** element needs to be updated with the resource ID for the VM.</span></span>
  
  * <span data-ttu-id="d74f6-137">Идентификатор ресурса может иметь следующий формат: "/subscriptions/{*идентификатор подписки, в которую входит виртуальная машина*}/resourceGroups/{*имя группы ресурсов виртуальной машины*}/providers/Microsoft.Compute/virtualMachines/{*имя виртуальной машины*}".</span><span class="sxs-lookup"><span data-stu-id="d74f6-137">The resource ID can be constructed by using the following pattern: "/subscriptions/{*subscription ID for the subscription with the VM*}/resourceGroups/{*The resourcegroup name for the VM*}/providers/Microsoft.Compute/virtualMachines/{*The VM Name*}".</span></span>
  * <span data-ttu-id="d74f6-138">Например, если подписка, в которую входит виртуальная машина, имеет идентификатор **11111111-1111-1111-1111-111111111111**, группа ресурсов называется **MyResourceGroup**, а виртуальная машина — **MyWindowsVM**, то атрибут *resourceID* будет выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="d74f6-138">For example, if the subscription ID for the subscription where the VM is running is **11111111-1111-1111-1111-111111111111**, the resource group name for the resource group is **MyResourceGroup**, and the VM Name is **MyWindowsVM**, then the value for *resourceID* would be:</span></span>
    
      ```
      <Metrics resourceId="/subscriptions/11111111-1111-1111-1111-111111111111/resourceGroups/MyResourceGroup/providers/Microsoft.Compute/virtualMachines/MyWindowsVM" >
      ```
  * <span data-ttu-id="d74f6-139">Дополнительные сведения о генерировании метрик на основе счетчиков производительности и конфигурации метрик см. в статье, посвященной [таблице метрик диагностики Azure в хранилище](extensions-diagnostics-template.md#wadmetrics-tables-in-storage).</span><span class="sxs-lookup"><span data-stu-id="d74f6-139">For more information on how metrics are generated based on the performance counters and metrics configuration, see [Azure Diagnostics metrics table in storage](extensions-diagnostics-template.md#wadmetrics-tables-in-storage).</span></span>
* <span data-ttu-id="d74f6-140">Элемент **StorageAccount** необходимо обновить, указав диагностическое имя учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="d74f6-140">The **StorageAccount** element needs to be updated with the name of the diagnostics storage account.</span></span>
  
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
        <Metrics resourceId="(Update with resource ID for the VM)" >
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

## <a name="next-steps"></a><span data-ttu-id="d74f6-141">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d74f6-141">Next steps</span></span>
* <span data-ttu-id="d74f6-142">Дополнительные рекомендации по использованию системы диагностики Azure и других методов для устранения неполадок см. в статье [Включение системы диагностики Azure в облачных службах Azure](../../cloud-services/cloud-services-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="d74f6-142">For additional guidance on using the Azure Diagnostics capability and other techniques to troubleshoot problems, see [Enabling Diagnostics in Azure Cloud Services and Virtual Machines](../../cloud-services/cloud-services-dotnet-diagnostics.md).</span></span>
* <span data-ttu-id="d74f6-143">Пояснение различных параметров XML-конфигураций для расширения диагностики см. в статье, посвященной [схеме конфигураций диагностики](https://msdn.microsoft.com/library/azure/mt634524.aspx).</span><span class="sxs-lookup"><span data-stu-id="d74f6-143">[Diagnostics configurations schema](https://msdn.microsoft.com/library/azure/mt634524.aspx) explains the various XML configurations options for the diagnostics extension.</span></span>

