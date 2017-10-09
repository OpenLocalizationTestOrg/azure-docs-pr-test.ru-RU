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
# <a name="using-powershell-tooset-up-application-insights-for-an-azure-web-app"></a><span data-ttu-id="119d6-103">С помощью PowerShell tooset копирование Application Insights для веб-приложение Azure</span><span class="sxs-lookup"><span data-stu-id="119d6-103">Using PowerShell tooset up Application Insights for an Azure web app</span></span>
<span data-ttu-id="119d6-104">[Microsoft Azure](https://azure.com) может быть [настроили систему диагностики Azure toosend](app-insights-azure-diagnostics.md) слишком[Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="119d6-104">[Microsoft Azure](https://azure.com) can be [configured toosend Azure Diagnostics](app-insights-azure-diagnostics.md) too[Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="119d6-105">Диагностика Hello связаны tooAzure облачных служб и виртуальных машинах Azure.</span><span class="sxs-lookup"><span data-stu-id="119d6-105">hello diagnostics relate tooAzure Cloud Services and Azure VMs.</span></span> <span data-ttu-id="119d6-106">Они дополняют hello данные телеметрии, отправляемого из приложения hello, с помощью пакета SDK Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="119d6-106">They complement hello telemetry that you send from within hello app using hello Application Insights SDK.</span></span> <span data-ttu-id="119d6-107">В рамках автоматизации hello процесс создания новых ресурсов в Azure, можно настроить диагностику с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="119d6-107">As part of automating hello process of creating new resources in Azure, you can configure diagnostics using PowerShell.</span></span>

## <a name="azure-template"></a><span data-ttu-id="119d6-108">Шаблон Azure</span><span class="sxs-lookup"><span data-stu-id="119d6-108">Azure template</span></span>
<span data-ttu-id="119d6-109">Если hello веб-приложения в Azure и создать ресурсы с помощью шаблона Azure Resource Manager, можно настроить путем добавления этого узла toohello ресурсы Application Insights:</span><span class="sxs-lookup"><span data-stu-id="119d6-109">If hello web app is in Azure and you create your resources using an Azure Resource Manager template, you can configure Application Insights by adding this toohello resources node:</span></span>

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

* <span data-ttu-id="119d6-110">`nameOfAIAppResource`-Имя ресурса Application Insights hello</span><span class="sxs-lookup"><span data-stu-id="119d6-110">`nameOfAIAppResource` - a name for hello Application Insights resource</span></span>
* <span data-ttu-id="119d6-111">`myWebAppName`— Идентификатор hello hello веб-приложения</span><span class="sxs-lookup"><span data-stu-id="119d6-111">`myWebAppName` - hello id of hello web app</span></span>

## <a name="enable-diagnostics-extension-as-part-of-deploying-a-cloud-service"></a><span data-ttu-id="119d6-112">Включение расширения диагностики как части развертывания облачной службы</span><span class="sxs-lookup"><span data-stu-id="119d6-112">Enable diagnostics extension as part of deploying a Cloud Service</span></span>
<span data-ttu-id="119d6-113">Hello `New-AzureDeployment` содержит параметр `ExtensionConfiguration`, который принимает массив конфигурации диагностики.</span><span class="sxs-lookup"><span data-stu-id="119d6-113">hello `New-AzureDeployment` cmdlet has a parameter `ExtensionConfiguration`, which takes an array of diagnostics configurations.</span></span> <span data-ttu-id="119d6-114">Эти компоненты можно создать с помощью hello `New-AzureServiceDiagnosticsExtensionConfig` командлета.</span><span class="sxs-lookup"><span data-stu-id="119d6-114">These can be created using hello `New-AzureServiceDiagnosticsExtensionConfig` cmdlet.</span></span> <span data-ttu-id="119d6-115">Например:</span><span class="sxs-lookup"><span data-stu-id="119d6-115">For example:</span></span>

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

## <a name="enable-diagnostics-extension-on-an-existing-cloud-service"></a><span data-ttu-id="119d6-116">Включение расширения диагностики в существующей облачной службе</span><span class="sxs-lookup"><span data-stu-id="119d6-116">Enable diagnostics extension on an existing Cloud Service</span></span>
<span data-ttu-id="119d6-117">Для уже существующей службы используйте командлет `Set-AzureServiceDiagnosticsExtension`.</span><span class="sxs-lookup"><span data-stu-id="119d6-117">On an existing service, use `Set-AzureServiceDiagnosticsExtension`.</span></span>

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

## <a name="get-current-diagnostics-extension-configuration"></a><span data-ttu-id="119d6-118">Получение текущей конфигурации расширения диагностики</span><span class="sxs-lookup"><span data-stu-id="119d6-118">Get current diagnostics extension configuration</span></span>
```ps

    Get-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```


## <a name="remove-diagnostics-extension"></a><span data-ttu-id="119d6-119">Удаление расширения диагностики</span><span class="sxs-lookup"><span data-stu-id="119d6-119">Remove diagnostics extension</span></span>
```ps

    Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

<span data-ttu-id="119d6-120">Если включен с помощью расширения диагностики hello `Set-AzureServiceDiagnosticsExtension` или `New-AzureServiceDiagnosticsExtensionConfig` без параметра роли hello, затем можно удалить с помощью расширения hello `Remove-AzureServiceDiagnosticsExtension` без параметра роли hello.</span><span class="sxs-lookup"><span data-stu-id="119d6-120">If you enabled hello diagnostics extension using either `Set-AzureServiceDiagnosticsExtension` or `New-AzureServiceDiagnosticsExtensionConfig` without hello Role parameter, then you can remove hello extension using `Remove-AzureServiceDiagnosticsExtension` without hello Role parameter.</span></span> <span data-ttu-id="119d6-121">Если параметр hello роль была использована при включении расширения hello затем он должен также использоваться при удалении расширения hello.</span><span class="sxs-lookup"><span data-stu-id="119d6-121">If hello Role parameter was used when enabling hello extension then it must also be used when removing hello extension.</span></span>

<span data-ttu-id="119d6-122">Модуль диагностики hello tooremove из каждого отдельного роли:</span><span class="sxs-lookup"><span data-stu-id="119d6-122">tooremove hello diagnostics extension from each individual role:</span></span>

```ps

    Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService" -Role "WebRole"
```


## <a name="see-also"></a><span data-ttu-id="119d6-123">См. также</span><span class="sxs-lookup"><span data-stu-id="119d6-123">See also</span></span>
* [<span data-ttu-id="119d6-124">Мониторинг приложений облачных служб Azure с помощью Application Insights</span><span class="sxs-lookup"><span data-stu-id="119d6-124">Monitor Azure Cloud Services apps with Application Insights</span></span>](app-insights-cloudservices.md)
* [<span data-ttu-id="119d6-125">Отправить аналитики tooApplication диагностики Azure</span><span class="sxs-lookup"><span data-stu-id="119d6-125">Send Azure Diagnostics tooApplication Insights</span></span>](app-insights-azure-diagnostics.md)
* [<span data-ttu-id="119d6-126">Use PowerShell to set alerts in Application Insights</span><span class="sxs-lookup"><span data-stu-id="119d6-126">Automate configuring alerts</span></span>](app-insights-powershell-alerts.md)

