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
# <a name="use-powershell-tooenable-azure-diagnostics-in-a-virtual-machine-running-windows"></a>Использовать диагностику Azure tooenable PowerShell на виртуальной машине под управлением Windows
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Система диагностики Azure — возможность hello в Azure, которая включает hello сбор диагностических данных с развернутым приложением. Можно использовать hello диагностики расширения toocollect диагностических данных как журналы приложения или счетчики производительности из виртуальной машины Azure (ВМ) под управлением Windows. В этой статье описывается, как Windows PowerShell tooenable toouse hello расширения диагностики для виртуальной Машины. В разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview) для hello предварительных требований для этой статьи.

## <a name="enable-hello-diagnostics-extension-if-you-use-hello-resource-manager-deployment-model"></a>Включить расширение диагностики hello при использовании модели развертывания диспетчера ресурсов hello
При создании ВМ Windows с помощью модели развертывания диспетчера ресурсов Azure hello путем добавления шаблона диспетчера ресурсов toohello конфигурации расширения hello можно включить расширение диагностики hello. В разделе [Создание виртуальной машины Windows с помощью мониторинга и диагностики с помощью шаблона Azure Resource Manager hello](extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

расширение диагностики tooenable hello в существующей виртуальной Машины, которая была создана с помощью модели развертывания диспетчера ресурсов hello, можно использовать hello [AzureRMVMDiagnosticsExtension набор](/powershell/module/azurerm.compute/set-azurermvmdiagnosticsextension) командлета PowerShell, как показано ниже.

    $vm_resourcegroup = "myvmresourcegroup"
    $vm_name = "myvm"
    $diagnosticsconfig_path = "DiagnosticsPubConfig.xml"

    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name -DiagnosticsConfigurationPath $diagnosticsconfig_path


*$diagnosticsconfig_path* — hello путь toohello файл, содержащий конфигурацию диагностики hello в формате XML, как описано в hello [пример](#sample-diagnostics-configuration) ниже.  

Если файл конфигурации диагностики hello указывает **StorageAccount** элемент с именем учетной записи хранилища, затем hello *AzureRMVMDiagnosticsExtension набор* hello будет автоматически задан сценарий расширение toosend диагностических данных toothat учетная запись хранения диагностики. Для этого toowork учетной записи хранилища hello должен toobe в hello той же подписке, как hello виртуальной Машины.

Если не **StorageAccount** был указан в конфигурации диагностики hello, то вы должны toopass в hello *StorageAccountName* параметра toohello командлета. Если hello *StorageAccountName* параметр указан, то hello командлет будет всегда использовать учетную запись хранения hello, указанный в параметре hello и не hello, указанный в файле конфигурации диагностики hello.

Если учетная запись хранения — в другой подписке из hello виртуальной Машины, потребуется tooexplicitly диагностики hello проходит hello *StorageAccountName* и *StorageAccountKey* toohello командлет параметры. Hello *StorageAccountKey* параметр не требуется, если учетной записи хранения диагностики hello hello одной подписке, как командлет hello автоматически можно запрашивать и устанавливать значение ключа hello, при включении расширения диагностики hello. Однако если hello учетная запись хранения диагностики — в другой подписке, а затем hello командлет может быть ключ hello tooget может автоматически и требуется tooexplicitly укажите ключ hello через hello *StorageAccountKey* параметр.  

    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name -DiagnosticsConfigurationPath $diagnosticsconfig_path -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key

После включения расширения диагностики hello на виртуальной Машине hello текущие настройки можно получить с помощью hello [Get AzureRMVmDiagnosticsExtension](/powershell/module/azurerm.compute/get-azurermvmdiagnosticsextension) командлета.

    Get-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name

Hello командлет возвращает *PublicSettings*, который содержит конфигурацию диагностики hello. Поддерживаются два типа конфигурации: WadCfg и xmlCfg. WadCfg — это конфигурации JSON, а xmlCfg — это конфигурация XML в кодировке Base64. tooread Здравствуйте XML, необходимо toodecode его.

    $publicsettings = (Get-AzureRmVMDiagnosticsExtension -ResourceGroupName $vm_resourcegroup -VMName $vm_name).PublicSettings
    $encodedconfig = (ConvertFrom-Json -InputObject $publicsettings).xmlCfg
    $xmlconfig = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($encodedconfig))
    Write-Host $xmlconfig

Hello [AzureRMVmDiagnosticsExtension удаление](/powershell/module/azurerm.compute/remove-azurermvmdiagnosticsextension) командлет может быть расширения диагностики используется tooremove hello из hello виртуальной Машины.  

## <a name="enable-hello-diagnostics-extension-if-you-use-hello-classic-deployment-model"></a>Включить расширение диагностики hello при использовании hello классической модели развертывания
Можно использовать hello [AzureVMDiagnosticsExtension набор](/powershell/module/azure/set-azurevmdiagnosticsextension) tooenable командлет расширения диагностики в ВМ, созданный с помощью hello классической модели развертывания. Hello следующем примере показано, как toocreate новой виртуальной Машины через hello классической модели развертывания с расширением диагностики hello включена.

    $VM = New-AzureVMConfig -Name $VM -InstanceSize Small -ImageName $VMImage
    $VM = Add-AzureProvisioningConfig -VM $VM -AdminUsername $Username -Password $Password -Windows
    $VM = Set-AzureVMDiagnosticsExtension -DiagnosticsConfigurationPath $Config_Path -VM $VM -StorageContext $Storage_Context
    New-AzureVM -Location $Location -ServiceName $Service_Name -VM $VM

расширение диагностики tooenable hello в существующей виртуальной Машины, который был создан при помощи hello классической модели развертывания, hello первого использования [Get-AzureVM](/powershell/module/azure/get-azurevm) конфигурацию виртуальной Машины hello tooget командлета. Обновите модуль диагностики hello tooinclude configuration hello виртуальной Машины с помощью hello [AzureVMDiagnosticsExtension набор](/powershell/module/azure/set-azurevmdiagnosticsextension) командлета. Наконец, примените toohello hello обновить конфигурацию виртуальной Машины с помощью [Update-AzureVM](/powershell/module/azure/update-azurevm).

    $VM = Get-AzureVM -ServiceName $Service_Name -Name $VM_Name
    $VM_Update = Set-AzureVMDiagnosticsExtension -DiagnosticsConfigurationPath $Config_Path -VM $VM -StorageContext $Storage_Context
    Update-AzureVM -ServiceName $Service_Name -Name $VM_Name -VM $VM_Update.VM

## <a name="sample-diagnostics-configuration"></a>Пример конфигурации диагностики
Здравствуйте, следующий XML-код можно использовать для настройки общих hello диагностики с hello выше сценариев. Этот пример конфигурации будут перенесены из системы диагностики hello различных производительности счетчики toohello учетная запись хранения диагностики, вместе с ошибок приложения hello, безопасности и система каналов в журналы событий Windows hello и любые ошибки журналы инфраструктуры.

Hello конфигурации необходимы следующие hello обновленные tooinclude toobe:

* Hello *resourceID* атрибут hello **метрики** элемент должен toobe обновляется hello ресурс с Идентификатором hello виртуальной Машины.
  
  * Здравствуйте, используя следующий шаблон hello можно сконструировать идентификатор ресурса: «/ subscriptions / {*идентификатор подписки для подписки hello с hello ВМ*} /resourceGroups/ {*имя hello группа ресурсов для виртуальной Машиныhello*} / providers/Microsoft.Compute/virtualMachines/ {*hello имя виртуальной Машины*}».
  * Например, если hello идентификатор подписки для подписки hello, где hello ВМ работает — **11111111-1111-1111-1111-111111111111**, hello имя группы ресурсов для группы ресурсов hello **MyResourceGroup**, а hello имя виртуальной Машины — **MyWindowsVM**, затем hello значение *resourceID* будет:
    
      ```
      <Metrics resourceId="/subscriptions/11111111-1111-1111-1111-111111111111/resourceGroups/MyResourceGroup/providers/Microsoft.Compute/virtualMachines/MyWindowsVM" >
      ```
  * Дополнительные сведения о том, как показатели, созданный на основе hello счетчики производительности и показатели конфигурации см. в разделе [таблице показателей диагностики Azure в хранилище](extensions-diagnostics-template.md#wadmetrics-tables-in-storage).
* Hello **StorageAccount** элемент должен toobe обновляется hello имя учетной записи хранения диагностики hello.
  
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

## <a name="next-steps"></a>Дальнейшие действия
* Дополнительные рекомендации по использованию возможностей диагностики Azure hello и других проблем tootroubleshoot методы. в разделе [включение диагностики в облачных службах Azure и виртуальные машины](../../cloud-services/cloud-services-dotnet-diagnostics.md).
* [Схема конфигурации диагностики](https://msdn.microsoft.com/library/azure/mt634524.aspx) объясняет различные конфигурации XML параметры для расширения диагностики hello hello.

