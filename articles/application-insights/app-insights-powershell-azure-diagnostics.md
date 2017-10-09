---
title: "toosetup aaaUsing PowerShell Application Insights в Azure | Документы Microsoft"
description: "Автоматизируйте настройку диагностики Azure toopipe tooApplication аналитики."
services: application-insights
documentationcenter: .net
author: sbtron
manager: carmonm
ms.assetid: 4ac803a8-f424-4c0c-b18f-4b9c189a64a5
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/17/2015
ms.author: bwren
ms.openlocfilehash: c48a5d8eb23df162522860935af876063aaa6976
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-powershell-tooset-up-application-insights-for-an-azure-web-app"></a>С помощью PowerShell tooset копирование Application Insights для веб-приложение Azure
[Microsoft Azure](https://azure.com) может быть [настроили систему диагностики Azure toosend](app-insights-azure-diagnostics.md) слишком[Azure Application Insights](app-insights-overview.md). Диагностика Hello связаны tooAzure облачных служб и виртуальных машинах Azure. Они дополняют hello данные телеметрии, отправляемого из приложения hello, с помощью пакета SDK Application Insights hello. В рамках автоматизации hello процесс создания новых ресурсов в Azure, можно настроить диагностику с помощью PowerShell.

## <a name="azure-template"></a>Шаблон Azure
Если hello веб-приложения в Azure и создать ресурсы с помощью шаблона Azure Resource Manager, можно настроить путем добавления этого узла toohello ресурсы Application Insights:

    {
      resources: [
        /* Create Application Insights resource */
        {
          "apiVersion": "2015-05-01",
          "type": "microsoft.insights/components",
          "name": "nameOfAIAppResource",
          "location": "centralus",
          "kind": "web",
          "properties": { "ApplicationId": "nameOfAIAppResource" },
          "dependsOn": [
            "[concat('Microsoft.Web/sites/', myWebAppName)]"
          ]
        }
       ]
     } 

* `nameOfAIAppResource`-Имя ресурса Application Insights hello
* `myWebAppName`— Идентификатор hello hello веб-приложения

## <a name="enable-diagnostics-extension-as-part-of-deploying-a-cloud-service"></a>Включение расширения диагностики как части развертывания облачной службы
Hello `New-AzureDeployment` содержит параметр `ExtensionConfiguration`, который принимает массив конфигурации диагностики. Эти компоненты можно создать с помощью hello `New-AzureServiceDiagnosticsExtensionConfig` командлета. Например:

```ps

    $service_package = "CloudService.cspkg"
    $service_config = "ServiceConfiguration.Cloud.cscfg"
    $diagnostics_storagename = "myservicediagnostics"
    $webrole_diagconfigpath = "MyService.WebRole.PubConfig.xml" 
    $workerrole_diagconfigpath = "MyService.WorkerRole.PubConfig.xml"

    $primary_storagekey = (Get-AzureStorageKey `
     -StorageAccountName "$diagnostics_storagename").Primary
    $storage_context = New-AzureStorageContext `
       -StorageAccountName $diagnostics_storagename `
       -StorageAccountKey $primary_storagekey

    $webrole_diagconfig = `
     New-AzureServiceDiagnosticsExtensionConfig `
      -Role "WebRole" -Storage_context $storageContext `
      -DiagnosticsConfigurationPath $webrole_diagconfigpath
    $workerrole_diagconfig = `
     New-AzureServiceDiagnosticsExtensionConfig `
      -Role "WorkerRole" `
      -StorageContext $storage_context `
      -DiagnosticsConfigurationPath $workerrole_diagconfigpath

    New-AzureDeployment `
      -ServiceName $service_name `
      -Slot Production `
      -Package $service_package `
      -Configuration $service_config `
      -ExtensionConfiguration @($webrole_diagconfig,$workerrole_diagconfig)

``` 

## <a name="enable-diagnostics-extension-on-an-existing-cloud-service"></a>Включение расширения диагностики в существующей облачной службе
Для уже существующей службы используйте командлет `Set-AzureServiceDiagnosticsExtension`.

```ps

    $service_name = "MyService"
    $diagnostics_storagename = "myservicediagnostics"
    $webrole_diagconfigpath = "MyService.WebRole.PubConfig.xml" 
    $workerrole_diagconfigpath = "MyService.WorkerRole.PubConfig.xml"
    $primary_storagekey = (Get-AzureStorageKey `
         -StorageAccountName "$diagnostics_storagename").Primary
    $storage_context = New-AzureStorageContext `
        -StorageAccountName $diagnostics_storagename `
        -StorageAccountKey $primary_storagekey

    Set-AzureServiceDiagnosticsExtension `
        -StorageContext $storage_context `
        -DiagnosticsConfigurationPath $webrole_diagconfigpath `
        -ServiceName $service_name `
        -Slot Production `
        -Role "WebRole" 
    Set-AzureServiceDiagnosticsExtension `
        -StorageContext $storage_context `
        -DiagnosticsConfigurationPath $workerrole_diagconfigpath `
        -ServiceName $service_name `
        -Slot Production `
        -Role "WorkerRole"
```

## <a name="get-current-diagnostics-extension-configuration"></a>Получение текущей конфигурации расширения диагностики
```ps

    Get-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```


## <a name="remove-diagnostics-extension"></a>Удаление расширения диагностики
```ps

    Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

Если включен с помощью расширения диагностики hello `Set-AzureServiceDiagnosticsExtension` или `New-AzureServiceDiagnosticsExtensionConfig` без параметра роли hello, затем можно удалить с помощью расширения hello `Remove-AzureServiceDiagnosticsExtension` без параметра роли hello. Если параметр hello роль была использована при включении расширения hello затем он должен также использоваться при удалении расширения hello.

Модуль диагностики hello tooremove из каждого отдельного роли:

```ps

    Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService" -Role "WebRole"
```


## <a name="see-also"></a>См. также
* [Мониторинг приложений облачных служб Azure с помощью Application Insights](app-insights-cloudservices.md)
* [Отправить аналитики tooApplication диагностики Azure](app-insights-azure-diagnostics.md)
* [Use PowerShell to set alerts in Application Insights](app-insights-powershell-alerts.md)

