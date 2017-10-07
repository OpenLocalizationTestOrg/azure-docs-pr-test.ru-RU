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
# <a name="powershell-script-toocreate-an-application-insights-resource"></a><span data-ttu-id="06bc7-103">Сценарий PowerShell toocreate ресурс Application Insights</span><span class="sxs-lookup"><span data-stu-id="06bc7-103">PowerShell script toocreate an Application Insights resource</span></span>


<span data-ttu-id="06bc7-104">При необходимости toomonitor новое приложение - или новая версия приложения - с [Azure Application Insights](https://azure.microsoft.com/services/application-insights/), Настройка нового ресурса в Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="06bc7-104">When you want toomonitor a new application - or a new version of an application - with [Azure Application Insights](https://azure.microsoft.com/services/application-insights/), you set up a new resource in Microsoft Azure.</span></span> <span data-ttu-id="06bc7-105">Этот ресурс находится где анализируются и отображаются hello данные телеметрии из приложения.</span><span class="sxs-lookup"><span data-stu-id="06bc7-105">This resource is where hello telemetry data from your app is analyzed and displayed.</span></span> 

<span data-ttu-id="06bc7-106">Создание нового ресурса hello можно автоматизировать с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="06bc7-106">You can automate hello creation of a new resource by using PowerShell.</span></span>

<span data-ttu-id="06bc7-107">Например, если вы разрабатываете приложение для мобильных устройств, вполне вероятно, что в одно и то же время клиенты будут использовать несколько опубликованных версий вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="06bc7-107">For example, if you are developing a mobile device app, it's likely that, at any time, there will be several published versions of your app in use by your customers.</span></span> <span data-ttu-id="06bc7-108">Вы не хотите tooget hello телеметрии результаты из различных версий смешивать.</span><span class="sxs-lookup"><span data-stu-id="06bc7-108">You don't want tooget hello telemetry results from different versions mixed up.</span></span> <span data-ttu-id="06bc7-109">Таким образом вы получаете вашей toocreate процесс построения нового ресурса для каждой сборки.</span><span class="sxs-lookup"><span data-stu-id="06bc7-109">So you get your build process toocreate a new resource for each build.</span></span>

> [!NOTE]
> <span data-ttu-id="06bc7-110">Если требуется набор ресурсов в toocreate hello же времени, рассмотрите возможность [Создание hello ресурсов с помощью шаблона Azure](app-insights-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="06bc7-110">If you want toocreate a set of resources all at hello same time, consider [creating hello resources using an Azure template](app-insights-powershell.md).</span></span>
> 
> 

## <a name="script-toocreate-an-application-insights-resource"></a><span data-ttu-id="06bc7-111">Сценарий toocreate ресурс Application Insights</span><span class="sxs-lookup"><span data-stu-id="06bc7-111">Script toocreate an Application Insights resource</span></span>
<span data-ttu-id="06bc7-112">См. в спецификации hello соответствующий командлет:</span><span class="sxs-lookup"><span data-stu-id="06bc7-112">See hello relevant cmdlet specs:</span></span>

* [<span data-ttu-id="06bc7-113">New-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="06bc7-113">New-AzureRmResource</span></span>](https://msdn.microsoft.com/library/mt652510.aspx)
* [<span data-ttu-id="06bc7-114">New-AzureRmRoleAssignment</span><span class="sxs-lookup"><span data-stu-id="06bc7-114">New-AzureRmRoleAssignment</span></span>](https://msdn.microsoft.com/library/mt678995.aspx)

<span data-ttu-id="06bc7-115">*Сценарий PowerShell*</span><span class="sxs-lookup"><span data-stu-id="06bc7-115">*PowerShell Script*</span></span>  

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

## <a name="what-toodo-with-hello-ikey"></a><span data-ttu-id="06bc7-116">Какие toodo с hello iKey</span><span class="sxs-lookup"><span data-stu-id="06bc7-116">What toodo with hello iKey</span></span>
<span data-ttu-id="06bc7-117">Каждый ресурс определяется по ключу инструментирования (iKey).</span><span class="sxs-lookup"><span data-stu-id="06bc7-117">Each resource is identified by its instrumentation key (iKey).</span></span> <span data-ttu-id="06bc7-118">Hello iKey выводится hello скрипт создания ресурса.</span><span class="sxs-lookup"><span data-stu-id="06bc7-118">hello iKey is an output of hello resource creation script.</span></span> <span data-ttu-id="06bc7-119">Скрипт сборки должен предоставить toohello iKey hello, пакет SDK Application Insights внедренных в приложение.</span><span class="sxs-lookup"><span data-stu-id="06bc7-119">Your build script should provide hello iKey toohello Application Insights SDK embedded in your app.</span></span>

<span data-ttu-id="06bc7-120">Существует два способа toomake hello iKey доступных toohello SDK:</span><span class="sxs-lookup"><span data-stu-id="06bc7-120">There are two ways toomake hello iKey available toohello SDK:</span></span>

* <span data-ttu-id="06bc7-121">В файле [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span><span class="sxs-lookup"><span data-stu-id="06bc7-121">In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span></span> 
  * <span data-ttu-id="06bc7-122">`<instrumentationkey>`*ikey*`</instrumentationkey>`</span><span class="sxs-lookup"><span data-stu-id="06bc7-122">`<instrumentationkey>`*ikey*`</instrumentationkey>`</span></span>
* <span data-ttu-id="06bc7-123">Или в [коде инициализации](app-insights-api-custom-events-metrics.md):</span><span class="sxs-lookup"><span data-stu-id="06bc7-123">Or in [initialization code](app-insights-api-custom-events-metrics.md):</span></span> 
  * <span data-ttu-id="06bc7-124">`Microsoft.ApplicationInsights.Extensibility.
    TelemetryConfiguration.Active.InstrumentationKey = "`*iKey*`";`</span><span class="sxs-lookup"><span data-stu-id="06bc7-124">`Microsoft.ApplicationInsights.Extensibility.
TelemetryConfiguration.Active.InstrumentationKey = "`*iKey*`";`</span></span>

## <a name="see-also"></a><span data-ttu-id="06bc7-125">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="06bc7-125">See also</span></span>
* [<span data-ttu-id="06bc7-126">Создание ресурсов Application Insights и веб-тестов на основе шаблонов</span><span class="sxs-lookup"><span data-stu-id="06bc7-126">Create Application Insights and web test resources from templates</span></span>](app-insights-powershell.md)
* [<span data-ttu-id="06bc7-127">Настройка мониторинга диагностики Azure с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="06bc7-127">Set up monitoring of Azure diagnostics with PowerShell</span></span>](app-insights-powershell-azure-diagnostics.md) 
* [<span data-ttu-id="06bc7-128">Настройка оповещений с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="06bc7-128">Set alerts by using PowerShell</span></span>](app-insights-powershell-alerts.md)

