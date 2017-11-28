---
title: "aaaEnable диагностики в облачных службах Azure с помощью PowerShell | Документы Microsoft"
description: "Узнайте, как tooenable диагностики для облачной службы с помощью PowerShell"
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 66e08754-8639-4022-ae18-4237749ba17d
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 09/06/2016
ms.author: adegeo
ms.openlocfilehash: 7c7444df13edc8d7f5663e20ec7558d36aac45d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enable-diagnostics-in-azure-cloud-services-using-powershell"></a><span data-ttu-id="54f0c-103">Включение диагностики в облачных службах Azure с помощью PowerShell </span><span class="sxs-lookup"><span data-stu-id="54f0c-103">Enable diagnostics in Azure Cloud Services using PowerShell</span></span>
<span data-ttu-id="54f0c-104">Можно собирать диагностические данные, такие как журналы приложений, счетчики производительности и т.д., из облачной службы с помощью hello расширения службы диагностики Azure.</span><span class="sxs-lookup"><span data-stu-id="54f0c-104">You can collect diagnostic data like application logs, performance counters etc. from a Cloud Service using hello Azure Diagnostics extension.</span></span> <span data-ttu-id="54f0c-105">В этой статье описывается, как tooenable hello расширения системы диагностики Azure для облачной службы с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="54f0c-105">This article describes how tooenable hello Azure Diagnostics extension for a Cloud Service using PowerShell.</span></span>  <span data-ttu-id="54f0c-106">В разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview) для hello предварительных требований для этой статьи.</span><span class="sxs-lookup"><span data-stu-id="54f0c-106">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for hello prerequisites needed for this article.</span></span>

## <a name="enable-diagnostics-extension-as-part-of-deploying-a-cloud-service"></a><span data-ttu-id="54f0c-107">Включение расширения диагностики как части развертывания облачной службы</span><span class="sxs-lookup"><span data-stu-id="54f0c-107">Enable diagnostics extension as part of deploying a Cloud Service</span></span>
<span data-ttu-id="54f0c-108">Этот подход является тип интеграции применимо toocontinuous сценариев, где расширение можно включить как часть развертывания диагностики hello hello облачной службы.</span><span class="sxs-lookup"><span data-stu-id="54f0c-108">This approach is applicable toocontinuous integration type of scenarios, where hello diagnostics extension can be enabled as part of deploying hello cloud service.</span></span> <span data-ttu-id="54f0c-109">При развертывании новой облачной службы можно включить расширение диагностики hello, передавая hello *ExtensionConfiguration* toohello параметр [New-AzureDeployment](/powershell/module/azure/new-azuredeployment?view=azuresmps-3.7.0) командлета.</span><span class="sxs-lookup"><span data-stu-id="54f0c-109">When creating a new Cloud Service deployment you can enable hello diagnostics extension by passing in hello *ExtensionConfiguration* parameter toohello [New-AzureDeployment](/powershell/module/azure/new-azuredeployment?view=azuresmps-3.7.0) cmdlet.</span></span> <span data-ttu-id="54f0c-110">Hello *ExtensionConfiguration* принимает массив конфигурации диагностики, которые могут быть созданы с помощью hello [New AzureServiceDiagnosticsExtensionConfig](/powershell/module/azure/new-azureservicediagnosticsextensionconfig?view=azuresmps-3.7.0) командлета.</span><span class="sxs-lookup"><span data-stu-id="54f0c-110">hello *ExtensionConfiguration* parameter takes an array of diagnostics configurations that can be created using hello [New-AzureServiceDiagnosticsExtensionConfig](/powershell/module/azure/new-azureservicediagnosticsextensionconfig?view=azuresmps-3.7.0) cmdlet.</span></span>

<span data-ttu-id="54f0c-111">Hello пример включения диагностики для облачной службы с WebRole и WorkerRole, каждый из которых конфигурации различных диагностики.</span><span class="sxs-lookup"><span data-stu-id="54f0c-111">hello following example shows how you can enable diagnostics for a cloud service with a WebRole and WorkerRole, each having a different diagnostics configuration.</span></span>

```powershell
$service_name = "MyService"
$service_package = "CloudService.cspkg"
$service_config = "ServiceConfiguration.Cloud.cscfg"
$webrole_diagconfigpath = "MyService.WebRole.PubConfig.xml"
$workerrole_diagconfigpath = "MyService.WorkerRole.PubConfig.xml"

$webrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WebRole" -DiagnosticsConfigurationPath $webrole_diagconfigpath
$workerrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WorkerRole" -DiagnosticsConfigurationPath $workerrole_diagconfigpath

New-AzureDeployment -ServiceName $service_name -Slot Production -Package $service_package -Configuration $service_config -ExtensionConfiguration @($webrole_diagconfig,$workerrole_diagconfig)
```

<span data-ttu-id="54f0c-112">Если файл конфигурации диагностики hello указывает `StorageAccount` элемент с именем учетной записи хранилища, затем hello `New-AzureServiceDiagnosticsExtensionConfig` командлет автоматически будет использовать эту учетную запись хранилища.</span><span class="sxs-lookup"><span data-stu-id="54f0c-112">If hello diagnostics configuration file specifies a `StorageAccount` element with a storage account name, then hello `New-AzureServiceDiagnosticsExtensionConfig` cmdlet will automatically use that storage account.</span></span> <span data-ttu-id="54f0c-113">Для этого toowork учетной записи хранилища hello должен toobe в hello той же подписке, как Здравствуйте, развертываемое в облачной службе.</span><span class="sxs-lookup"><span data-stu-id="54f0c-113">For this toowork, hello storage account needs toobe in hello same subscription as hello Cloud Service being deployed.</span></span>

<span data-ttu-id="54f0c-114">Из файлов конфигурации расширения пусть hello, созданных hello MSBuild публикации пакета Azure SDK 2.6 целевой результат будет включать имя учетной записи хранения hello, на основе строки конфигурации диагностики hello, указанную в файле конфигурации службы hello (.cscfg).</span><span class="sxs-lookup"><span data-stu-id="54f0c-114">From Azure SDK 2.6 onward hello extension configuration files generated by hello MSBuild publish target output will include hello storage account name based on hello diagnostics configuration string specified in hello service configuration file (.cscfg).</span></span> <span data-ttu-id="54f0c-115">Приведенный ниже сценарий Hello показано, как файлы конфигурации расширения tooparse hello из hello публикации вывод целевого объекта и настроить расширения диагностики для каждой роли, при развертывании облачной службы hello.</span><span class="sxs-lookup"><span data-stu-id="54f0c-115">hello script below shows you how tooparse hello Extension configuration files from hello publish target output and configure diagnostics extension for each role when deploying hello cloud service.</span></span>

```powershell
$service_name = "MyService"
$service_package = "C:\build\output\CloudService.cspkg"
$service_config = "C:\build\output\ServiceConfiguration.Cloud.cscfg"

#Find hello Extensions path based on service configuration file
$extensionsSearchPath = Join-Path -Path (Split-Path -Parent $service_config) -ChildPath "Extensions"

$diagnosticsExtensions = Get-ChildItem -Path $extensionsSearchPath -Filter "PaaSDiagnostics.*.PubConfig.xml"
$diagnosticsConfigurations = @()
foreach ($extPath in $diagnosticsExtensions)
{
    #Find hello RoleName based on file naming convention PaaSDiagnostics.<RoleName>.PubConfig.xml
    $roleName = ""
    $roles = $extPath -split ".",0,"simplematch"
    if ($roles -is [system.array] -and $roles.Length -gt 1)
    {
        $roleName = $roles[1]
        $x = 2
        while ($x -le $roles.Length)
            {
               if ($roles[$x] -ne "PubConfig")
                {
                    $roleName = $roleName + "." + $roles[$x]
                }
                else
                {
                    break
                }
                $x++
            }
        $fullExtPath = Join-Path -path $extensionsSearchPath -ChildPath $extPath
        $diagnosticsconfig = New-AzureServiceDiagnosticsExtensionConfig -Role $roleName -DiagnosticsConfigurationPath $fullExtPath
        $diagnosticsConfigurations += $diagnosticsconfig
    }
}
New-AzureDeployment -ServiceName $service_name -Slot Production -Package $service_package -Configuration $service_config -ExtensionConfiguration $diagnosticsConfigurations
```

<span data-ttu-id="54f0c-116">Visual Studio Online подобный подход используется для автоматического развертывания облачных служб с расширением диагностики hello.</span><span class="sxs-lookup"><span data-stu-id="54f0c-116">Visual Studio Online uses a similar approach for automated deployments of Cloud Services with hello diagnostics extension.</span></span> <span data-ttu-id="54f0c-117">Полный пример см. в файле [Publish-AzureCloudDeployment.ps1](https://github.com/Microsoft/vso-agent-tasks/blob/master/Tasks/AzureCloudPowerShellDeployment/Publish-AzureCloudDeployment.ps1).</span><span class="sxs-lookup"><span data-stu-id="54f0c-117">See [Publish-AzureCloudDeployment.ps1](https://github.com/Microsoft/vso-agent-tasks/blob/master/Tasks/AzureCloudPowerShellDeployment/Publish-AzureCloudDeployment.ps1) for a complete example.</span></span>

<span data-ttu-id="54f0c-118">Если не `StorageAccount` был указан в конфигурации диагностики hello, то вы должны toopass в hello *StorageAccountName* параметра toohello командлета.</span><span class="sxs-lookup"><span data-stu-id="54f0c-118">If no `StorageAccount` was specified in hello diagnostics configuration, then you need toopass in hello *StorageAccountName* parameter toohello cmdlet.</span></span> <span data-ttu-id="54f0c-119">Если hello *StorageAccountName* параметр указан, то hello командлет будет всегда использовать учетную запись хранения hello, указанный в параметре hello и не hello, указанный в файле конфигурации диагностики hello.</span><span class="sxs-lookup"><span data-stu-id="54f0c-119">If hello *StorageAccountName* parameter is specified, then hello cmdlet will always use hello storage account that is specified in hello parameter and not hello one that is specified in hello diagnostics configuration file.</span></span>

<span data-ttu-id="54f0c-120">Если учетная запись хранения — в другой подписке из hello облачной службы, потребуется tooexplicitly диагностики hello проходит hello *StorageAccountName* и *StorageAccountKey* параметров командлет toohello.</span><span class="sxs-lookup"><span data-stu-id="54f0c-120">If hello diagnostics storage account is in a different subscription from hello Cloud Service, then you need tooexplicitly pass in hello *StorageAccountName* and *StorageAccountKey* parameters toohello cmdlet.</span></span> <span data-ttu-id="54f0c-121">Hello *StorageAccountKey* параметр не требуется, если учетной записи хранения диагностики hello hello одной подписке, как командлет hello автоматически можно запрашивать и устанавливать значение ключа hello, при включении расширения диагностики hello.</span><span class="sxs-lookup"><span data-stu-id="54f0c-121">hello *StorageAccountKey* parameter is not needed when hello diagnostics storage account is in hello same subscription, as hello cmdlet can automatically query and set hello key value when enabling hello diagnostics extension.</span></span> <span data-ttu-id="54f0c-122">Однако если hello учетная запись хранения диагностики — в другой подписке, а затем hello командлет может быть ключ hello tooget может автоматически и требуется tooexplicitly укажите ключ hello через hello *StorageAccountKey* параметр.</span><span class="sxs-lookup"><span data-stu-id="54f0c-122">However, if hello diagnostics storage account is in a different subscription, then hello cmdlet might not be able tooget hello key automatically and you need tooexplicitly specify hello key through hello *StorageAccountKey* parameter.</span></span>

```powershell
$webrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WebRole" -DiagnosticsConfigurationPath $webrole_diagconfigpath -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key
$workerrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WorkerRole" -DiagnosticsConfigurationPath $workerrole_diagconfigpath -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key
```

## <a name="enable-diagnostics-extension-on-an-existing-cloud-service"></a><span data-ttu-id="54f0c-123">Включение расширения диагностики в существующей облачной службе</span><span class="sxs-lookup"><span data-stu-id="54f0c-123">Enable diagnostics extension on an existing Cloud Service</span></span>
<span data-ttu-id="54f0c-124">Можно использовать hello [AzureServiceDiagnosticsExtension набор](/powershell/module/azure/set-azureservicediagnosticsextension?view=azuresmps-3.7.0) командлет tooenable или обновления конфигурации диагностики в облачной службе, на котором уже выполняется.</span><span class="sxs-lookup"><span data-stu-id="54f0c-124">You can use hello [Set-AzureServiceDiagnosticsExtension](/powershell/module/azure/set-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet tooenable or update diagnostics configuration on a Cloud Service that is already running.</span></span>

[!INCLUDE [cloud-services-wad-warning](../../includes/cloud-services-wad-warning.md)]

```powershell
$service_name = "MyService"
$webrole_diagconfigpath = "MyService.WebRole.PubConfig.xml"
$workerrole_diagconfigpath = "MyService.WorkerRole.PubConfig.xml"

$webrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WebRole" -DiagnosticsConfigurationPath $webrole_diagconfigpath
$workerrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WorkerRole" -DiagnosticsConfigurationPath $workerrole_diagconfigpath

Set-AzureServiceDiagnosticsExtension -DiagnosticsConfiguration @($webrole_diagconfig,$workerrole_diagconfig) -ServiceName $service_name
```

## <a name="get-current-diagnostics-extension-configuration"></a><span data-ttu-id="54f0c-125">Получение текущей конфигурации расширения диагностики</span><span class="sxs-lookup"><span data-stu-id="54f0c-125">Get current diagnostics extension configuration</span></span>
<span data-ttu-id="54f0c-126">Используйте hello [Get AzureServiceDiagnosticsExtension](/powershell/module/azure/get-azureservicediagnosticsextension?view=azuresmps-3.7.0) командлет tooget hello текущую конфигурацию диагностики для облачной службы.</span><span class="sxs-lookup"><span data-stu-id="54f0c-126">Use hello [Get-AzureServiceDiagnosticsExtension](/powershell/module/azure/get-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet tooget hello current diagnostics configuration for a cloud service.</span></span>

```powershell
Get-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

## <a name="remove-diagnostics-extension"></a><span data-ttu-id="54f0c-127">Удаление расширения диагностики</span><span class="sxs-lookup"><span data-stu-id="54f0c-127">Remove diagnostics extension</span></span>
<span data-ttu-id="54f0c-128">tooturn из системы диагностики в облачной службы вы можно использовать hello [AzureServiceDiagnosticsExtension удаление](/powershell/module/azure/remove-azureservicediagnosticsextension?view=azuresmps-3.7.0) командлета.</span><span class="sxs-lookup"><span data-stu-id="54f0c-128">tooturn off diagnostics on a cloud service you can use hello [Remove-AzureServiceDiagnosticsExtension](/powershell/module/azure/remove-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet.</span></span>

```powershell
Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

<span data-ttu-id="54f0c-129">Если включен с помощью расширения диагностики hello *набор AzureServiceDiagnosticsExtension* или hello *New AzureServiceDiagnosticsExtensionConfig* без hello *роли* параметр, то можно удалить с помощью расширения hello *удаление AzureServiceDiagnosticsExtension* без hello *роли* параметра.</span><span class="sxs-lookup"><span data-stu-id="54f0c-129">If you enabled hello diagnostics extension using either *Set-AzureServiceDiagnosticsExtension* or hello *New-AzureServiceDiagnosticsExtensionConfig* without hello *Role* parameter then you can remove hello extension using *Remove-AzureServiceDiagnosticsExtension* without hello *Role* parameter.</span></span> <span data-ttu-id="54f0c-130">Если hello *роли* параметр была использована при включении расширения hello, то оно также должно использоваться при удалении расширения hello.</span><span class="sxs-lookup"><span data-stu-id="54f0c-130">If hello *Role* parameter was used when enabling hello extension then it must also be used when removing hello extension.</span></span>

<span data-ttu-id="54f0c-131">Модуль диагностики hello tooremove из каждого отдельного роли:</span><span class="sxs-lookup"><span data-stu-id="54f0c-131">tooremove hello diagnostics extension from each individual role:</span></span>

```powershell
Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService" -Role "WebRole"
```

## <a name="next-steps"></a><span data-ttu-id="54f0c-132">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="54f0c-132">Next Steps</span></span>
* <span data-ttu-id="54f0c-133">Дополнительные рекомендации по использованию службы диагностики Azure и других проблем tootroubleshoot методы. в разделе [включение диагностики в облачных службах Azure и виртуальные машины](cloud-services-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="54f0c-133">For additional guidance on using Azure diagnostics and other techniques tootroubleshoot problems, see [Enabling Diagnostics in Azure Cloud Services and Virtual Machines](cloud-services-dotnet-diagnostics.md).</span></span>
* <span data-ttu-id="54f0c-134">Hello [схема конфигурации службы диагностики](https://msdn.microsoft.com/library/azure/dn782207.aspx) объясняет различные конфигурации xml параметры для расширения диагностики hello hello.</span><span class="sxs-lookup"><span data-stu-id="54f0c-134">hello [Diagnostics Configuration Schema](https://msdn.microsoft.com/library/azure/dn782207.aspx) explains hello various xml configurations options for hello diagnostics extension.</span></span>
* <span data-ttu-id="54f0c-135">расширения диагностики hello tooenable для виртуальных машин. в статье toolearn [создать Windows виртуальной машины с помощью мониторинга и диагностики с помощью шаблона Azure Resource Manager](../virtual-machines/windows/extensions-diagnostics-template.md)</span><span class="sxs-lookup"><span data-stu-id="54f0c-135">toolearn how tooenable hello diagnostics extension for Virtual Machines, see [Create a Windows Virtual machine with monitoring and diagnostics using Azure Resource Manager Template](../virtual-machines/windows/extensions-diagnostics-template.md)</span></span>
