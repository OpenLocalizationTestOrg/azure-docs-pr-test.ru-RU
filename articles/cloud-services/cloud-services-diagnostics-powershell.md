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
# <a name="enable-diagnostics-in-azure-cloud-services-using-powershell"></a>Включение диагностики в облачных службах Azure с помощью PowerShell 
Можно собирать диагностические данные, такие как журналы приложений, счетчики производительности и т.д., из облачной службы с помощью hello расширения службы диагностики Azure. В этой статье описывается, как tooenable hello расширения системы диагностики Azure для облачной службы с помощью PowerShell.  В разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview) для hello предварительных требований для этой статьи.

## <a name="enable-diagnostics-extension-as-part-of-deploying-a-cloud-service"></a>Включение расширения диагностики как части развертывания облачной службы
Этот подход является тип интеграции применимо toocontinuous сценариев, где расширение можно включить как часть развертывания диагностики hello hello облачной службы. При развертывании новой облачной службы можно включить расширение диагностики hello, передавая hello *ExtensionConfiguration* toohello параметр [New-AzureDeployment](/powershell/module/azure/new-azuredeployment?view=azuresmps-3.7.0) командлета. Hello *ExtensionConfiguration* принимает массив конфигурации диагностики, которые могут быть созданы с помощью hello [New AzureServiceDiagnosticsExtensionConfig](/powershell/module/azure/new-azureservicediagnosticsextensionconfig?view=azuresmps-3.7.0) командлета.

Hello пример включения диагностики для облачной службы с WebRole и WorkerRole, каждый из которых конфигурации различных диагностики.

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

Если файл конфигурации диагностики hello указывает `StorageAccount` элемент с именем учетной записи хранилища, затем hello `New-AzureServiceDiagnosticsExtensionConfig` командлет автоматически будет использовать эту учетную запись хранилища. Для этого toowork учетной записи хранилища hello должен toobe в hello той же подписке, как Здравствуйте, развертываемое в облачной службе.

Из файлов конфигурации расширения пусть hello, созданных hello MSBuild публикации пакета Azure SDK 2.6 целевой результат будет включать имя учетной записи хранения hello, на основе строки конфигурации диагностики hello, указанную в файле конфигурации службы hello (.cscfg). Приведенный ниже сценарий Hello показано, как файлы конфигурации расширения tooparse hello из hello публикации вывод целевого объекта и настроить расширения диагностики для каждой роли, при развертывании облачной службы hello.

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

Visual Studio Online подобный подход используется для автоматического развертывания облачных служб с расширением диагностики hello. Полный пример см. в файле [Publish-AzureCloudDeployment.ps1](https://github.com/Microsoft/vso-agent-tasks/blob/master/Tasks/AzureCloudPowerShellDeployment/Publish-AzureCloudDeployment.ps1).

Если не `StorageAccount` был указан в конфигурации диагностики hello, то вы должны toopass в hello *StorageAccountName* параметра toohello командлета. Если hello *StorageAccountName* параметр указан, то hello командлет будет всегда использовать учетную запись хранения hello, указанный в параметре hello и не hello, указанный в файле конфигурации диагностики hello.

Если учетная запись хранения — в другой подписке из hello облачной службы, потребуется tooexplicitly диагностики hello проходит hello *StorageAccountName* и *StorageAccountKey* параметров командлет toohello. Hello *StorageAccountKey* параметр не требуется, если учетной записи хранения диагностики hello hello одной подписке, как командлет hello автоматически можно запрашивать и устанавливать значение ключа hello, при включении расширения диагностики hello. Однако если hello учетная запись хранения диагностики — в другой подписке, а затем hello командлет может быть ключ hello tooget может автоматически и требуется tooexplicitly укажите ключ hello через hello *StorageAccountKey* параметр.

```powershell
$webrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WebRole" -DiagnosticsConfigurationPath $webrole_diagconfigpath -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key
$workerrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WorkerRole" -DiagnosticsConfigurationPath $workerrole_diagconfigpath -StorageAccountName $diagnosticsstorage_name -StorageAccountKey $diagnosticsstorage_key
```

## <a name="enable-diagnostics-extension-on-an-existing-cloud-service"></a>Включение расширения диагностики в существующей облачной службе
Можно использовать hello [AzureServiceDiagnosticsExtension набор](/powershell/module/azure/set-azureservicediagnosticsextension?view=azuresmps-3.7.0) командлет tooenable или обновления конфигурации диагностики в облачной службе, на котором уже выполняется.

[!INCLUDE [cloud-services-wad-warning](../../includes/cloud-services-wad-warning.md)]

```powershell
$service_name = "MyService"
$webrole_diagconfigpath = "MyService.WebRole.PubConfig.xml"
$workerrole_diagconfigpath = "MyService.WorkerRole.PubConfig.xml"

$webrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WebRole" -DiagnosticsConfigurationPath $webrole_diagconfigpath
$workerrole_diagconfig = New-AzureServiceDiagnosticsExtensionConfig -Role "WorkerRole" -DiagnosticsConfigurationPath $workerrole_diagconfigpath

Set-AzureServiceDiagnosticsExtension -DiagnosticsConfiguration @($webrole_diagconfig,$workerrole_diagconfig) -ServiceName $service_name
```

## <a name="get-current-diagnostics-extension-configuration"></a>Получение текущей конфигурации расширения диагностики
Используйте hello [Get AzureServiceDiagnosticsExtension](/powershell/module/azure/get-azureservicediagnosticsextension?view=azuresmps-3.7.0) командлет tooget hello текущую конфигурацию диагностики для облачной службы.

```powershell
Get-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

## <a name="remove-diagnostics-extension"></a>Удаление расширения диагностики
tooturn из системы диагностики в облачной службы вы можно использовать hello [AzureServiceDiagnosticsExtension удаление](/powershell/module/azure/remove-azureservicediagnosticsextension?view=azuresmps-3.7.0) командлета.

```powershell
Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

Если включен с помощью расширения диагностики hello *набор AzureServiceDiagnosticsExtension* или hello *New AzureServiceDiagnosticsExtensionConfig* без hello *роли* параметр, то можно удалить с помощью расширения hello *удаление AzureServiceDiagnosticsExtension* без hello *роли* параметра. Если hello *роли* параметр была использована при включении расширения hello, то оно также должно использоваться при удалении расширения hello.

Модуль диагностики hello tooremove из каждого отдельного роли:

```powershell
Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService" -Role "WebRole"
```

## <a name="next-steps"></a>Дальнейшие действия
* Дополнительные рекомендации по использованию службы диагностики Azure и других проблем tootroubleshoot методы. в разделе [включение диагностики в облачных службах Azure и виртуальные машины](cloud-services-dotnet-diagnostics.md).
* Hello [схема конфигурации службы диагностики](https://msdn.microsoft.com/library/azure/dn782207.aspx) объясняет различные конфигурации xml параметры для расширения диагностики hello hello.
* расширения диагностики hello tooenable для виртуальных машин. в статье toolearn [создать Windows виртуальной машины с помощью мониторинга и диагностики с помощью шаблона Azure Resource Manager](../virtual-machines/windows/extensions-diagnostics-template.md)
