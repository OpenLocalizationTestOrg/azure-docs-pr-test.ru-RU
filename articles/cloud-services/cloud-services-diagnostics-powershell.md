---
title: "Включение диагностики в облачных службах Azure с использованием PowerShell | Документация Майкрософт"
description: "Узнайте, как включить диагностику для облачных служб с помощью PowerShell."
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
ms.openlocfilehash: 8dd9724981860c9cd4ccc443cc2bfdc465811e7c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="enable-diagnostics-in-azure-cloud-services-using-powershell"></a><span data-ttu-id="ec37e-103">Включение диагностики в облачных службах Azure с помощью PowerShell </span><span class="sxs-lookup"><span data-stu-id="ec37e-103">Enable diagnostics in Azure Cloud Services using PowerShell</span></span>
<span data-ttu-id="ec37e-104">Для сбора диагностических данных, таких как журналы приложений, счетчики производительности и т. д., из облачной службы можно использовать расширение системы диагностики Azure.</span><span class="sxs-lookup"><span data-stu-id="ec37e-104">You can collect diagnostic data like application logs, performance counters etc. from a Cloud Service using the Azure Diagnostics extension.</span></span> <span data-ttu-id="ec37e-105">В этой статье описывается включение расширения диагностики Azure для облачной службы с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ec37e-105">This article describes how to enable the Azure Diagnostics extension for a Cloud Service using PowerShell.</span></span>  <span data-ttu-id="ec37e-106">Сведения о компонентах, которые потребуются для выполнения инструкций в этой статье, см. в статье [Установка и настройка Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ec37e-106">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for the prerequisites needed for this article.</span></span>

## <a name="enable-diagnostics-extension-as-part-of-deploying-a-cloud-service"></a><span data-ttu-id="ec37e-107">Включение расширения диагностики как части развертывания облачной службы</span><span class="sxs-lookup"><span data-stu-id="ec37e-107">Enable diagnostics extension as part of deploying a Cloud Service</span></span>
<span data-ttu-id="ec37e-108">Этот подход подходит для сценариев непрерывной интеграции, в которых в ходе развертывания облачной службы можно включить расширение системы диагностики.</span><span class="sxs-lookup"><span data-stu-id="ec37e-108">This approach is applicable to continuous integration type of scenarios, where the diagnostics extension can be enabled as part of deploying the cloud service.</span></span> <span data-ttu-id="ec37e-109">При развертывании новой облачной службы можно включить расширение системы диагностики, передав параметр *ExtensionConfiguration* командлету [New-AzureDeployment](/powershell/module/azure/new-azuredeployment?view=azuresmps-3.7.0) .</span><span class="sxs-lookup"><span data-stu-id="ec37e-109">When creating a new Cloud Service deployment you can enable the diagnostics extension by passing in the *ExtensionConfiguration* parameter to the [New-AzureDeployment](/powershell/module/azure/new-azuredeployment?view=azuresmps-3.7.0) cmdlet.</span></span> <span data-ttu-id="ec37e-110">Параметр *ExtensionConfiguration* принимает массив конфигураций диагностики, которые могут быть созданы с помощью командлета [New-AzureServiceDiagnosticsExtensionConfig](/powershell/module/azure/new-azureservicediagnosticsextensionconfig?view=azuresmps-3.7.0) .</span><span class="sxs-lookup"><span data-stu-id="ec37e-110">The *ExtensionConfiguration* parameter takes an array of diagnostics configurations that can be created using the [New-AzureServiceDiagnosticsExtensionConfig](/powershell/module/azure/new-azureservicediagnosticsextensionconfig?view=azuresmps-3.7.0) cmdlet.</span></span>

<span data-ttu-id="ec37e-111">В следующем примере показано включение диагностики для облачной службы с веб-ролью и рабочей ролью, каждая из которых имеет свою конфигурацию диагностики.</span><span class="sxs-lookup"><span data-stu-id="ec37e-111">The following example shows how you can enable diagnostics for a cloud service with a WebRole and WorkerRole, each having a different diagnostics configuration.</span></span>

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

<span data-ttu-id="ec37e-112">Если файл конфигурации диагностики содержит элемент `StorageAccount` с именем учетной записи хранения, то командлет `New-AzureServiceDiagnosticsExtensionConfig` автоматически использует эту учетную запись хранения.</span><span class="sxs-lookup"><span data-stu-id="ec37e-112">If the diagnostics configuration file specifies a `StorageAccount` element with a storage account name, then the `New-AzureServiceDiagnosticsExtensionConfig` cmdlet will automatically use that storage account.</span></span> <span data-ttu-id="ec37e-113">Для этого учетная запись хранения должна входить в ту же подписку, что и развертываемая облачная служба.</span><span class="sxs-lookup"><span data-stu-id="ec37e-113">For this to work, the storage account needs to be in the same subscription as the Cloud Service being deployed.</span></span>

<span data-ttu-id="ec37e-114">В пакете SDK Azure 2.6 и более поздних версий файлы конфигурации расширения, создаваемые выходной целью публикации MSBuild, будут включать имя учетной записи хранения на основе строки конфигурации диагностики, указанной в файле конфигурации службы (.cscfg).</span><span class="sxs-lookup"><span data-stu-id="ec37e-114">From Azure SDK 2.6 onward the extension configuration files generated by the MSBuild publish target output will include the storage account name based on the diagnostics configuration string specified in the service configuration file (.cscfg).</span></span> <span data-ttu-id="ec37e-115">Приведенный ниже сценарий показывает, как анализировать файлы конфигурации расширения из выходной цели публикации и настраивать расширение системы диагностики для каждой роли при развертывании облачной службы.</span><span class="sxs-lookup"><span data-stu-id="ec37e-115">The script below shows you how to parse the Extension configuration files from the publish target output and configure diagnostics extension for each role when deploying the cloud service.</span></span>

```powershell
$service_name = "MyService"
$service_package = "C:\build\output\CloudService.cspkg"
$service_config = "C:\build\output\ServiceConfiguration.Cloud.cscfg"

#Find the Extensions path based on service configuration file
$extensionsSearchPath = Join-Path -Path (Split-Path -Parent $service_config) -ChildPath "Extensions"

$diagnosticsExtensions = Get-ChildItem -Path $extensionsSearchPath -Filter "PaaSDiagnostics.*.PubConfig.xml"
$diagnosticsConfigurations = @()
foreach ($extPath in $diagnosticsExtensions)
{
    #Find the RoleName based on file naming convention PaaSDiagnostics.<RoleName>.PubConfig.xml
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

<span data-ttu-id="ec37e-116">Visual Studio Online использует аналогичный подход для автоматических развертываний облачных служб с расширением системы диагностики.</span><span class="sxs-lookup"><span data-stu-id="ec37e-116">Visual Studio Online uses a similar approach for automated deployments of Cloud Services with the diagnostics extension.</span></span> <span data-ttu-id="ec37e-117">Полный пример см. в файле [Publish-AzureCloudDeployment.ps1](https://github.com/Microsoft/vso-agent-tasks/blob/master/Tasks/AzureCloudPowerShellDeployment/Publish-AzureCloudDeployment.ps1).</span><span class="sxs-lookup"><span data-stu-id="ec37e-117">See [Publish-AzureCloudDeployment.ps1](https://github.com/Microsoft/vso-agent-tasks/blob/master/Tasks/AzureCloudPowerShellDeployment/Publish-AzureCloudDeployment.ps1) for a complete example.</span></span>

<span data-ttu-id="ec37e-118">Если в конфигурации диагностики нет элемента `StorageAccount`, то в командлет необходимо передать параметр *StorageAccountName*.</span><span class="sxs-lookup"><span data-stu-id="ec37e-118">If no `StorageAccount` was specified in the diagnostics configuration, then you need to pass in the *StorageAccountName* parameter to the cmdlet.</span></span> <span data-ttu-id="ec37e-119">Если параметр *StorageAccountName* указан, командлет использует учетную запись хранения, указанную в этом параметре, а не в файле конфигурации диагностики.</span><span class="sxs-lookup"><span data-stu-id="ec37e-119">If the *StorageAccountName* parameter is specified, then the cmdlet will always use the storage account that is specified in the parameter and not the one that is specified in the diagnostics configuration file.</span></span>

<span data-ttu-id="ec37e-120">Если учетная запись хранения для диагностики и облачная служба относятся к разным подпискам, то в командлет необходимо явным образом передать параметры *StorageAccountName* и *StorageAccountKey*.</span><span class="sxs-lookup"><span data-stu-id="ec37e-120">If the diagnostics storage account is in a different subscription from the Cloud Service, then you need to explicitly pass in the *StorageAccountName* and *StorageAccountKey* parameters to the cmdlet.</span></span> <span data-ttu-id="ec37e-121">Параметр *StorageAccountKey* не требуется, если учетная запись хранения диагностики входит в ту же подписку, так как при включении расширения диагностики командлет автоматически запрашивает и устанавливает значение ключа.</span><span class="sxs-lookup"><span data-stu-id="ec37e-121">The *StorageAccountKey* parameter is not needed when the diagnostics storage account is in the same subscription, as the cmdlet can automatically query and set the key value when enabling the diagnostics extension.</span></span> <span data-ttu-id="ec37e-122">Если же учетная запись хранения диагностики входит в другую подписку, командлет не сможет получить ключ автоматически, а значит, его необходимо явно указать с помощью параметра *StorageAccountKey* .</span><span class="sxs-lookup"><span data-stu-id="ec37e-122">However, if the diagnostics storage account is in a different subscription, then the cmdlet might not be able to get the key automatically and you need to explicitly specify the key through the *StorageAccountKey* parameter.</span></span>

```powershell
$webrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WebRole" -DiagnosticsConfigurationPath $webrole_diagconfigpath -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key
$workerrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WorkerRole" -DiagnosticsConfigurationPath $workerrole_diagconfigpath -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key
```

## <a name="enable-diagnostics-extension-on-an-existing-cloud-service"></a><span data-ttu-id="ec37e-123">Включение расширения диагностики в существующей облачной службе</span><span class="sxs-lookup"><span data-stu-id="ec37e-123">Enable diagnostics extension on an existing Cloud Service</span></span>
<span data-ttu-id="ec37e-124">Для включения или обновления конфигурации диагностики в уже работающей облачной службе можно использовать командлет [Set-AzureServiceDiagnosticsExtension](/powershell/module/azure/set-azureservicediagnosticsextension?view=azuresmps-3.7.0) .</span><span class="sxs-lookup"><span data-stu-id="ec37e-124">You can use the [Set-AzureServiceDiagnosticsExtension](/powershell/module/azure/set-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet to enable or update diagnostics configuration on a Cloud Service that is already running.</span></span>

[!INCLUDE [cloud-services-wad-warning](../../includes/cloud-services-wad-warning.md)]

```powershell
$service_name = "MyService"
$webrole_diagconfigpath = "MyService.WebRole.PubConfig.xml"
$workerrole_diagconfigpath = "MyService.WorkerRole.PubConfig.xml"

$webrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WebRole" -DiagnosticsConfigurationPath $webrole_diagconfigpath
$workerrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WorkerRole" -DiagnosticsConfigurationPath $workerrole_diagconfigpath

Set-AzureServiceDiagnosticsExtension -DiagnosticsConfiguration @($webrole_diagconfig,$workerrole_diagconfig) -ServiceName $service_name
```

## <a name="get-current-diagnostics-extension-configuration"></a><span data-ttu-id="ec37e-125">Получение текущей конфигурации расширения диагностики</span><span class="sxs-lookup"><span data-stu-id="ec37e-125">Get current diagnostics extension configuration</span></span>
<span data-ttu-id="ec37e-126">Получите текущую конфигурацию диагностики для облачной службы с помощью командлета [Get-AzureServiceDiagnosticsExtension](/powershell/module/azure/get-azureservicediagnosticsextension?view=azuresmps-3.7.0) .</span><span class="sxs-lookup"><span data-stu-id="ec37e-126">Use the [Get-AzureServiceDiagnosticsExtension](/powershell/module/azure/get-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet to get the current diagnostics configuration for a cloud service.</span></span>

```powershell
Get-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

## <a name="remove-diagnostics-extension"></a><span data-ttu-id="ec37e-127">Удаление расширения диагностики</span><span class="sxs-lookup"><span data-stu-id="ec37e-127">Remove diagnostics extension</span></span>
<span data-ttu-id="ec37e-128">Чтобы отключить диагностику в облачной службе, используйте командлет [Remove-AzureServiceDiagnosticsExtension](/powershell/module/azure/remove-azureservicediagnosticsextension?view=azuresmps-3.7.0) .</span><span class="sxs-lookup"><span data-stu-id="ec37e-128">To turn off diagnostics on a cloud service you can use the [Remove-AzureServiceDiagnosticsExtension](/powershell/module/azure/remove-azureservicediagnosticsextension?view=azuresmps-3.7.0) cmdlet.</span></span>

```powershell
Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

<span data-ttu-id="ec37e-129">Если расширение диагностики было включено с использованием командлета *Set-AzureServiceDiagnosticsExtension* или *New-AzureServiceDiagnosticsExtensionConfig* без параметра *Role*, его можно удалить с помощью командлета *Remove-AzureServiceDiagnosticsExtension* без параметра *Role*.</span><span class="sxs-lookup"><span data-stu-id="ec37e-129">If you enabled the diagnostics extension using either *Set-AzureServiceDiagnosticsExtension* or the *New-AzureServiceDiagnosticsExtensionConfig* without the *Role* parameter then you can remove the extension using *Remove-AzureServiceDiagnosticsExtension* without the *Role* parameter.</span></span> <span data-ttu-id="ec37e-130">Если параметр *Role* использовался при включении расширения, он также должен применяться при удалении расширения.</span><span class="sxs-lookup"><span data-stu-id="ec37e-130">If the *Role* parameter was used when enabling the extension then it must also be used when removing the extension.</span></span>

<span data-ttu-id="ec37e-131">Удаление расширения диагностики из каждой отдельной роли</span><span class="sxs-lookup"><span data-stu-id="ec37e-131">To remove the diagnostics extension from each individual role:</span></span>

```powershell
Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService" -Role "WebRole"
```

## <a name="next-steps"></a><span data-ttu-id="ec37e-132">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ec37e-132">Next Steps</span></span>
* <span data-ttu-id="ec37e-133">Дополнительные рекомендации по использованию диагностики Azure и других методов для устранения неполадок см. в статье [Включение диагностики в облачных службах и виртуальных машинах Azure](cloud-services-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="ec37e-133">For additional guidance on using Azure diagnostics and other techniques to troubleshoot problems, see [Enabling Diagnostics in Azure Cloud Services and Virtual Machines](cloud-services-dotnet-diagnostics.md).</span></span>
* <span data-ttu-id="ec37e-134">В статье [Схема конфигурации диагностики](https://msdn.microsoft.com/library/azure/dn782207.aspx) поясняются различные параметры XML-конфигураций для расширения диагностики.</span><span class="sxs-lookup"><span data-stu-id="ec37e-134">The [Diagnostics Configuration Schema](https://msdn.microsoft.com/library/azure/dn782207.aspx) explains the various xml configurations options for the diagnostics extension.</span></span>
* <span data-ttu-id="ec37e-135">Сведения о включении расширения диагностики для виртуальных машин см. в статье [Создание виртуальной машины Windows с мониторингом и диагностикой с использованием шаблона Azure Resource Manager](../virtual-machines/windows/extensions-diagnostics-template.md).</span><span class="sxs-lookup"><span data-stu-id="ec37e-135">To learn how to enable the diagnostics extension for Virtual Machines, see [Create a Windows Virtual machine with monitoring and diagnostics using Azure Resource Manager Template](../virtual-machines/windows/extensions-diagnostics-template.md)</span></span>
