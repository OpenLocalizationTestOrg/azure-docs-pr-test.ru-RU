---
title: "Настройка Application Insights в Azure с помощью PowerShell | Документация Майкрософт"
description: "Автоматизируйте настройку системы диагностики Azure для передачи данных в Application Insights."
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
ms.openlocfilehash: 3b6da89cc33cda713b483a2af3cbb493a03d6bec
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="using-powershell-to-set-up-application-insights-for-an-azure-web-app"></a><span data-ttu-id="bc759-103">Настройка Application Insights для веб-приложения Azure с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="bc759-103">Using PowerShell to set up Application Insights for an Azure web app</span></span>
<span data-ttu-id="bc759-104">[Microsoft Azure](https://azure.com) можно [настроить для отправки данных системы диагностики Azure](app-insights-azure-diagnostics.md) в [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bc759-104">[Microsoft Azure](https://azure.com) can be [configured to send Azure Diagnostics](app-insights-azure-diagnostics.md) to [Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="bc759-105">Данные диагностики связаны с облачными службами Azure и виртуальными машинами Azure.</span><span class="sxs-lookup"><span data-stu-id="bc759-105">The diagnostics relate to Azure Cloud Services and Azure VMs.</span></span> <span data-ttu-id="bc759-106">Они дополняют данные телеметрии, отправляемые из приложения с помощью пакета SDK Application Insights.</span><span class="sxs-lookup"><span data-stu-id="bc759-106">They complement the telemetry that you send from within the app using the Application Insights SDK.</span></span> <span data-ttu-id="bc759-107">В рамках автоматизации создания новых ресурсов в Azure вы можете настроить диагностику с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bc759-107">As part of automating the process of creating new resources in Azure, you can configure diagnostics using PowerShell.</span></span>

## <a name="azure-template"></a><span data-ttu-id="bc759-108">Шаблон Azure</span><span class="sxs-lookup"><span data-stu-id="bc759-108">Azure template</span></span>
<span data-ttu-id="bc759-109">Если веб-приложение работает в Azure и вы создаете ресурсы с помощью шаблона Azure Resource Manager, можно настроить Application Insights, добавив следующий код в узел ресурсов:</span><span class="sxs-lookup"><span data-stu-id="bc759-109">If the web app is in Azure and you create your resources using an Azure Resource Manager template, you can configure Application Insights by adding this to the resources node:</span></span>

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

* <span data-ttu-id="bc759-110">`nameOfAIAppResource` — имя ресурса Application Insights.</span><span class="sxs-lookup"><span data-stu-id="bc759-110">`nameOfAIAppResource` - a name for the Application Insights resource</span></span>
* <span data-ttu-id="bc759-111">`myWebAppName` — идентификатор веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="bc759-111">`myWebAppName` - the id of the web app</span></span>

## <a name="enable-diagnostics-extension-as-part-of-deploying-a-cloud-service"></a><span data-ttu-id="bc759-112">Включение расширения диагностики как части развертывания облачной службы</span><span class="sxs-lookup"><span data-stu-id="bc759-112">Enable diagnostics extension as part of deploying a Cloud Service</span></span>
<span data-ttu-id="bc759-113">Параметр `ExtensionConfiguration` командлета `New-AzureDeployment` принимает массив значений для конфигурации диагностики.</span><span class="sxs-lookup"><span data-stu-id="bc759-113">The `New-AzureDeployment` cmdlet has a parameter `ExtensionConfiguration`, which takes an array of diagnostics configurations.</span></span> <span data-ttu-id="bc759-114">Их можно создать с помощью командлета `New-AzureServiceDiagnosticsExtensionConfig` .</span><span class="sxs-lookup"><span data-stu-id="bc759-114">These can be created using the `New-AzureServiceDiagnosticsExtensionConfig` cmdlet.</span></span> <span data-ttu-id="bc759-115">Например:</span><span class="sxs-lookup"><span data-stu-id="bc759-115">For example:</span></span>

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

## <a name="enable-diagnostics-extension-on-an-existing-cloud-service"></a><span data-ttu-id="bc759-116">Включение расширения диагностики в существующей облачной службе</span><span class="sxs-lookup"><span data-stu-id="bc759-116">Enable diagnostics extension on an existing Cloud Service</span></span>
<span data-ttu-id="bc759-117">Для уже существующей службы используйте командлет `Set-AzureServiceDiagnosticsExtension`.</span><span class="sxs-lookup"><span data-stu-id="bc759-117">On an existing service, use `Set-AzureServiceDiagnosticsExtension`.</span></span>

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

## <a name="get-current-diagnostics-extension-configuration"></a><span data-ttu-id="bc759-118">Получение текущей конфигурации расширения диагностики</span><span class="sxs-lookup"><span data-stu-id="bc759-118">Get current diagnostics extension configuration</span></span>
```ps

    Get-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```


## <a name="remove-diagnostics-extension"></a><span data-ttu-id="bc759-119">Удаление расширения диагностики</span><span class="sxs-lookup"><span data-stu-id="bc759-119">Remove diagnostics extension</span></span>
```ps

    Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

<span data-ttu-id="bc759-120">Если расширение диагностики было включено с помощью командлета `Set-AzureServiceDiagnosticsExtension` или `New-AzureServiceDiagnosticsExtensionConfig` без параметра Role, вы можете удалить расширение с помощью командлета `Remove-AzureServiceDiagnosticsExtension` без параметра Role.</span><span class="sxs-lookup"><span data-stu-id="bc759-120">If you enabled the diagnostics extension using either `Set-AzureServiceDiagnosticsExtension` or `New-AzureServiceDiagnosticsExtensionConfig` without the Role parameter, then you can remove the extension using `Remove-AzureServiceDiagnosticsExtension` without the Role parameter.</span></span> <span data-ttu-id="bc759-121">Если параметр Role использовался при включении расширения, он также должен применяться и при его удалении.</span><span class="sxs-lookup"><span data-stu-id="bc759-121">If the Role parameter was used when enabling the extension then it must also be used when removing the extension.</span></span>

<span data-ttu-id="bc759-122">Удаление расширения диагностики из каждой отдельной роли</span><span class="sxs-lookup"><span data-stu-id="bc759-122">To remove the diagnostics extension from each individual role:</span></span>

```ps

    Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService" -Role "WebRole"
```


## <a name="see-also"></a><span data-ttu-id="bc759-123">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="bc759-123">See also</span></span>
* [<span data-ttu-id="bc759-124">Мониторинг приложений облачных служб Azure с помощью Application Insights</span><span class="sxs-lookup"><span data-stu-id="bc759-124">Monitor Azure Cloud Services apps with Application Insights</span></span>](app-insights-cloudservices.md)
* [<span data-ttu-id="bc759-125">Отправка данных системы диагностики Azure в Application Insights</span><span class="sxs-lookup"><span data-stu-id="bc759-125">Send Azure Diagnostics to Application Insights</span></span>](app-insights-azure-diagnostics.md)
* [<span data-ttu-id="bc759-126">Use PowerShell to set alerts in Application Insights</span><span class="sxs-lookup"><span data-stu-id="bc759-126">Automate configuring alerts</span></span>](app-insights-powershell-alerts.md)

