---
title: "сценарий aaaPowerShell toocreate ресурс Application Insights | Документы Microsoft"
description: "Автоматизация создания ресурсов Application Insights."
services: application-insights
documentationcenter: windows
author: CFreemanwa
manager: carmonm
ms.assetid: f0082c9b-43ad-4576-a417-4ea8e0daf3d9
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/19/2016
ms.author: bwren
ms.openlocfilehash: 2ac00376d38026d64c2c5deabfaca60588924510
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="powershell-script-toocreate-an-application-insights-resource"></a>Сценарий PowerShell toocreate ресурс Application Insights


При необходимости toomonitor новое приложение - или новая версия приложения - с [Azure Application Insights](https://azure.microsoft.com/services/application-insights/), Настройка нового ресурса в Microsoft Azure. Этот ресурс находится где анализируются и отображаются hello данные телеметрии из приложения. 

Создание нового ресурса hello можно автоматизировать с помощью PowerShell.

Например, если вы разрабатываете приложение для мобильных устройств, вполне вероятно, что в одно и то же время клиенты будут использовать несколько опубликованных версий вашего приложения. Вы не хотите tooget hello телеметрии результаты из различных версий смешивать. Таким образом вы получаете вашей toocreate процесс построения нового ресурса для каждой сборки.

> [!NOTE]
> Если требуется набор ресурсов в toocreate hello же времени, рассмотрите возможность [Создание hello ресурсов с помощью шаблона Azure](app-insights-powershell.md).
> 
> 

## <a name="script-toocreate-an-application-insights-resource"></a>Сценарий toocreate ресурс Application Insights
См. в спецификации hello соответствующий командлет:

* [New-AzureRmResource](https://msdn.microsoft.com/library/mt652510.aspx)
* [New-AzureRmRoleAssignment](https://msdn.microsoft.com/library/mt678995.aspx)

*Сценарий PowerShell*  

```PowerShell


###########################################
# Set Values
###########################################

# If running manually, uncomment before hello first 
# execution toologin toohello Azure Portal:

# Add-AzureRmAccount / Login-AzureRmAccount

# Set hello name of hello Application Insights Resource

$appInsightsName = "TestApp"

# Set hello application name used for hello value of hello Tag "AppInsightsApp" 

$applicationTagName = "MyApp"

# Set hello name of hello Resource Group toouse.  
# Default is hello application name.
$resourceGroupName = "MyAppResourceGroup"

###################################################
# Create hello Resource and Output hello name and iKey
###################################################

# Select hello azure subscription
Select-AzureSubscription -SubscriptionName "MySubscription"

# Create hello App Insights Resource


$resource = New-AzureRmResource `
  -ResourceName $appInsightsName `
  -ResourceGroupName $resourceGroupName `
  -Tag @{ applicationType = "web"; applicationName = $applicationTagName} `
  -ResourceType "Microsoft.Insights/components" `
  -Location "East US" `  # or North Europe, West Europe, South Central US
  -PropertyObject @{"Application_Type"="web"} `
  -Force

# Give owner access toohello team

New-AzureRmRoleAssignment `
  -SignInName "myteam@fabrikam.com" `
  -RoleDefinitionName Owner `
  -Scope $resource.ResourceId 


# Display iKey
Write-Host "App Insights Name = " $resource.Name
Write-Host "IKey = " $resource.Properties.InstrumentationKey

```

## <a name="what-toodo-with-hello-ikey"></a>Какие toodo с hello iKey
Каждый ресурс определяется по ключу инструментирования (iKey). Hello iKey выводится hello скрипт создания ресурса. Скрипт сборки должен предоставить toohello iKey hello, пакет SDK Application Insights внедренных в приложение.

Существует два способа toomake hello iKey доступных toohello SDK:

* В файле [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md): 
  * `<instrumentationkey>`*ikey*`</instrumentationkey>`
* Или в [коде инициализации](app-insights-api-custom-events-metrics.md): 
  * `Microsoft.ApplicationInsights.Extensibility.
    TelemetryConfiguration.Active.InstrumentationKey = "`*iKey*`";`

## <a name="see-also"></a>Дополнительные материалы
* [Создание ресурсов Application Insights и веб-тестов на основе шаблонов](app-insights-powershell.md)
* [Настройка мониторинга диагностики Azure с помощью PowerShell](app-insights-powershell-azure-diagnostics.md) 
* [Настройка оповещений с помощью PowerShell](app-insights-powershell-alerts.md)

