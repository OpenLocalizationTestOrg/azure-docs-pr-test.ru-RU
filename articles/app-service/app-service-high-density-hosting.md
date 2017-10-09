---
title: "aaaHigh плотность размещения в службе приложений Azure | Документы Microsoft"
description: "Высокая плотность размещения в службе приложений Azure"
author: btardif
manager: erikre
editor: 
services: app-service\web
documentationcenter: 
ms.assetid: a903cb78-4927-47b0-8427-56412c4e3e64
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 06/12/2017
ms.author: byvinyal
ms.openlocfilehash: a10cb81ace13ba6992b572a44361061ecf72b266
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="high-density-hosting-on-azure-app-service"></a><span data-ttu-id="b377d-103">Высокая плотность размещения в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="b377d-103">High density hosting on Azure App Service</span></span>
<span data-ttu-id="b377d-104">При использовании службы приложений, приложение отсоединяется от емкости hello, занимаемый tooit двух основных понятиях:</span><span class="sxs-lookup"><span data-stu-id="b377d-104">When using App Service, your application is decoupled from hello capacity allocated tooit by two concepts:</span></span>

* <span data-ttu-id="b377d-105">**Приложение Hello:** представляет приложение hello и конфигурации среды выполнения.</span><span class="sxs-lookup"><span data-stu-id="b377d-105">**hello Application:** Represents hello app and its runtime configuration.</span></span> <span data-ttu-id="b377d-106">Например, он включает hello версию .NET, hello среды выполнения необходимо загрузить, параметры приложения hello.</span><span class="sxs-lookup"><span data-stu-id="b377d-106">For example, it includes hello version of .NET that hello runtime should load, hello app settings.</span></span>
* <span data-ttu-id="b377d-107">**Привет, план служб приложений:** определяет характеристики hello емкости hello, набор доступных функций и расположение приложения hello.</span><span class="sxs-lookup"><span data-stu-id="b377d-107">**hello App Service Plan:** Defines hello characteristics of hello capacity, available feature set, and locality of hello application.</span></span> <span data-ttu-id="b377d-108">Это могут быть следующие характеристики: большие (четырехъядерные) компьютеры, четыре экземпляра или функции уровня "Премиум" в восточной части США.</span><span class="sxs-lookup"><span data-stu-id="b377d-108">For example, characteristics might be large (four cores) machine, four instances, Premium features in East US.</span></span>

<span data-ttu-id="b377d-109">Приложения всегда связанного tooan план служб приложений, однако план службы приложений можно предоставить tooone емкости или другие приложения.</span><span class="sxs-lookup"><span data-stu-id="b377d-109">An app is always linked tooan App Service plan, but an App Service plan can provide capacity tooone or more apps.</span></span>

<span data-ttu-id="b377d-110">В результате платформы hello обеспечивает гибкость tooisolate hello одного приложения или у нескольких приложений, общий доступ к ресурсам, предоставив план служб приложений.</span><span class="sxs-lookup"><span data-stu-id="b377d-110">As a result, hello platform provides hello flexibility tooisolate a single app or have multiple apps share resources by sharing an App Service plan.</span></span>

<span data-ttu-id="b377d-111">Однако если несколько приложений совместно используют план службы приложений, один экземпляр этого приложения будет выполняться на каждом экземпляре данного плана службы приложений.</span><span class="sxs-lookup"><span data-stu-id="b377d-111">However, when multiple apps share an App Service plan, an instance of that app runs on every instance of that App Service plan.</span></span>

## <a name="per-app-scaling"></a><span data-ttu-id="b377d-112">Независимое масштабирование приложений</span><span class="sxs-lookup"><span data-stu-id="b377d-112">Per app scaling</span></span>
<span data-ttu-id="b377d-113">*Независимое масштабирование приложений* — это функция, которую можно включить на уровне плана службы приложений и затем использовать для каждого приложения.</span><span class="sxs-lookup"><span data-stu-id="b377d-113">*Per app scaling* is a feature that can be enabled at the App Service plan level and then used per application.</span></span>

<span data-ttu-id="b377d-114">Она позволяет масштабировать приложение независимо от плана службы приложений, в котором оно размещено.</span><span class="sxs-lookup"><span data-stu-id="b377d-114">Per app scaling scales an app independently from the App Service plan that hosts it.</span></span> <span data-ttu-id="b377d-115">Таким образом, план может иметь службу приложений масштабировать too10 экземпляров, но приложение может устанавливаться только пять toouse.</span><span class="sxs-lookup"><span data-stu-id="b377d-115">This way, an App Service plan can be scaled too10 instances, but an app can be set toouse only five.</span></span>

   >[!NOTE]
   ><span data-ttu-id="b377d-116">Независимое масштабирование приложений доступно только для планов службы приложений с номером SKU уровня **Премиум**.</span><span class="sxs-lookup"><span data-stu-id="b377d-116">Per app scaling is available only for **Premium** SKU App Service plans</span></span>
   >

### <a name="per-app-scaling-using-powershell"></a><span data-ttu-id="b377d-117">Независимое масштабирование приложений с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="b377d-117">Per app scaling using PowerShell</span></span>

<span data-ttu-id="b377d-118">Можно создать план настроен в качестве *на масштабирование приложения* плана, передавая hello ```-perSiteScaling $true``` атрибута toohello ```New-AzureRmAppServicePlan``` командлетов для</span><span class="sxs-lookup"><span data-stu-id="b377d-118">You can create a plan configured as a *Per app scaling* plan by passing in hello ```-perSiteScaling $true``` attribute toohello ```New-AzureRmAppServicePlan``` commandlet</span></span>

```
New-AzureRmAppServicePlan -ResourceGroupName $ResourceGroup -Name $AppServicePlan `
                            -Location $Location `
                            -Tier Premium -WorkerSize Small `
                            -NumberofWorkers 5 -PerSiteScaling $true
```

<span data-ttu-id="b377d-119">Если требуется tooupdate существующей службы приложений спланировать toouse эту функцию.</span><span class="sxs-lookup"><span data-stu-id="b377d-119">If you want tooupdate an existing App Service plan toouse this feature:</span></span> 

- <span data-ttu-id="b377d-120">получить hello целевого плана```Get-AzureRmAppServicePlan```</span><span class="sxs-lookup"><span data-stu-id="b377d-120">get hello target plan ```Get-AzureRmAppServicePlan```</span></span>
- <span data-ttu-id="b377d-121">Изменение свойства hello локально```$newASP.PerSiteScaling = $true```</span><span class="sxs-lookup"><span data-stu-id="b377d-121">modifying hello property locally ```$newASP.PerSiteScaling = $true```</span></span>
- <span data-ttu-id="b377d-122">Учет к задней tooazure изменения```Set-AzureRmAppServicePlan```</span><span class="sxs-lookup"><span data-stu-id="b377d-122">posting your changes back tooazure ```Set-AzureRmAppServicePlan```</span></span> 

```
# Get hello new App Service Plan and modify hello "PerSiteScaling" property.
$newASP = Get-AzureRmAppServicePlan -ResourceGroupName $ResourceGroup -Name $AppServicePlan
$newASP

#Modify hello local copy toouse "PerSiteScaling" property.
$newASP.PerSiteScaling = $true
$newASP
    
#Post updated app service plan back tooazure
Set-AzureRmAppServicePlan $newASP
```

<span data-ttu-id="b377d-123">На уровне приложения hello нам нужна tooconfigure hello количество экземпляров, которое можно использовать приложение hello в плане обслуживания приложения hello.</span><span class="sxs-lookup"><span data-stu-id="b377d-123">At hello app level, we need tooconfigure hello number of instances hello app can use in hello app service plan.</span></span>

<span data-ttu-id="b377d-124">В приведенном ниже примере hello приложение hello является ограниченной tootwo экземпляров независимо от того, сколько экземпляров hello базового приложения службы плана масштабирование out для.</span><span class="sxs-lookup"><span data-stu-id="b377d-124">In hello example below, hello app is limited tootwo instances regardless of how many instances hello underlying app service plan scales out to.</span></span>

```
# Get hello app we want tooconfigure toouse "PerSiteScaling"
$newapp = Get-AzureRmWebApp -ResourceGroupName $ResourceGroup -Name $webapp
    
# Modify hello NumberOfWorkers setting toohello desired value.
$newapp.SiteConfig.NumberOfWorkers = 2
    
# Post updated app back tooazure
Set-AzureRmWebApp $newapp
```

> [!IMPORTANT]
> <span data-ttu-id="b377d-125">$newapp.SiteConfig.NumberOfWorkers — это другая форма свойства $newapp.MaxNumberOfWorkers.</span><span class="sxs-lookup"><span data-stu-id="b377d-125">$newapp.SiteConfig.NumberOfWorkers is different form $newapp.MaxNumberOfWorkers.</span></span> <span data-ttu-id="b377d-126">На каждое приложение масштабирование использует $newapp. SiteConfig.NumberOfWorkers toodetermine hello шкалы характеристики приложение hello.</span><span class="sxs-lookup"><span data-stu-id="b377d-126">Per app scaling uses $newapp.SiteConfig.NumberOfWorkers toodetermine hello scale characteristics of hello app.</span></span>

### <a name="per-app-scaling-using-azure-resource-manager"></a><span data-ttu-id="b377d-127">Независимое масштабирование приложений с помощью Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b377d-127">Per app scaling using Azure Resource Manager</span></span>

<span data-ttu-id="b377d-128">следующие Hello *шаблона Azure Resource Manager* создает:</span><span class="sxs-lookup"><span data-stu-id="b377d-128">hello following *Azure Resource Manager template* creates:</span></span>

- <span data-ttu-id="b377d-129">План служб приложений с масштабированием too10 экземпляров</span><span class="sxs-lookup"><span data-stu-id="b377d-129">An App Service plan that's scaled out too10 instances</span></span>
- <span data-ttu-id="b377d-130">приложение, которое настроил tooscale tooa максимум пять экземпляров.</span><span class="sxs-lookup"><span data-stu-id="b377d-130">an app that's configured tooscale tooa max of five instances.</span></span>

<span data-ttu-id="b377d-131">Hello план служб приложений является установка hello **PerSiteScaling** tootrue свойства ```"perSiteScaling": true```.</span><span class="sxs-lookup"><span data-stu-id="b377d-131">hello App Service plan is setting hello **PerSiteScaling** property tootrue ```"perSiteScaling": true```.</span></span> <span data-ttu-id="b377d-132">устанавливает приложение Hello hello **количество работников** toouse too5 ```"properties": { "numberOfWorkers": "5" }```.</span><span class="sxs-lookup"><span data-stu-id="b377d-132">hello app is setting hello **number of workers** toouse too5 ```"properties": { "numberOfWorkers": "5" }```.</span></span>

```
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters":{
        "appServicePlanName": { "type": "string" },
        "appName": { "type": "string" }
        },
    "resources": [
    {
        "comments": "App Service Plan with per site perSiteScaling = true",
        "type": "Microsoft.Web/serverFarms",
        "sku": {
            "name": "P1",
            "tier": "Premium",
            "size": "P1",
            "family": "P",
            "capacity": 10
            },
        "name": "[parameters('appServicePlanName')]",
        "apiVersion": "2015-08-01",
        "location": "West US",
        "properties": {
            "name": "[parameters('appServicePlanName')]",
            "perSiteScaling": true
        }
    },
    {
        "type": "Microsoft.Web/sites",
        "name": "[parameters('appName')]",
        "apiVersion": "2015-08-01-preview",
        "location": "West US",
        "dependsOn": [ "[resourceId('Microsoft.Web/serverFarms', parameters('appServicePlanName'))]" ],
        "properties": { "serverFarmId": "[resourceId('Microsoft.Web/serverFarms', parameters('appServicePlanName'))]" },
        "resources": [ {
                "comments": "",
                "type": "config",
                "name": "web",
                "apiVersion": "2015-08-01",
                "location": "West US",
                "dependsOn": [ "[resourceId('Microsoft.Web/Sites', parameters('appName'))]" ],
                "properties": { "numberOfWorkers": "5" }
            } ]
        }]
}
```

## <a name="recommended-configuration-for-high-density-hosting"></a><span data-ttu-id="b377d-133">Рекомендуемая конфигурация для высокой плотности размещения</span><span class="sxs-lookup"><span data-stu-id="b377d-133">Recommended configuration for high density hosting</span></span>
<span data-ttu-id="b377d-134">Независимое масштабирование приложений — это функция, которая включается как в глобальных регионах Azure, так и в средах службы приложений.</span><span class="sxs-lookup"><span data-stu-id="b377d-134">Per app scaling is a feature that is enabled in both global Azure regions and App Service Environments.</span></span> <span data-ttu-id="b377d-135">Тем не менее hello рекомендуемая стратегия заключается в использовании среды службы приложения tootake преимущества дополнительных возможностей и hello большего пулы емкости.</span><span class="sxs-lookup"><span data-stu-id="b377d-135">However, hello recommended strategy is to use App Service Environments tootake advantage of their advanced features and hello larger pools of capacity.</span></span>  

<span data-ttu-id="b377d-136">Выполните эти шаги tooconfigure высокая плотность размещения для приложения.</span><span class="sxs-lookup"><span data-stu-id="b377d-136">Follow these steps tooconfigure high density hosting for your apps:</span></span>

1. <span data-ttu-id="b377d-137">Настройте hello среды службы приложений и выберите пул работника, высокая плотность выделенный toohello вариант размещения.</span><span class="sxs-lookup"><span data-stu-id="b377d-137">Configure hello App Service Environment and choose a worker pool that is dedicated toohello high density hosting scenario.</span></span>
1. <span data-ttu-id="b377d-138">Создать отдельный план службы приложений и масштабировать его toouse все hello доступной емкости в hello рабочего пула.</span><span class="sxs-lookup"><span data-stu-id="b377d-138">Create a single App Service plan, and scale it toouse all hello available capacity on hello worker pool.</span></span>
1. <span data-ttu-id="b377d-139">Установите флаг tootrue hello PerSiteScaling hello план служб приложений.</span><span class="sxs-lookup"><span data-stu-id="b377d-139">Set hello PerSiteScaling flag tootrue on hello App Service plan.</span></span>
1. <span data-ttu-id="b377d-140">Новые приложения создаются и назначенный toothat план служб приложений с **numberOfWorkers** значение свойства слишком**1**.</span><span class="sxs-lookup"><span data-stu-id="b377d-140">New apps are created and assigned toothat App Service plan with the **numberOfWorkers** property set too**1**.</span></span> <span data-ttu-id="b377d-141">С помощью данной конфигурации дает hello максимальной плотностью возможных для этого пула работника.</span><span class="sxs-lookup"><span data-stu-id="b377d-141">Using this configuration yields hello highest density possible on this worker pool.</span></span>
1. <span data-ttu-id="b377d-142">Hello число рабочих процессов, можно настроить независимо друг от друга на дополнительные ресурсы toogrant приложения при необходимости.</span><span class="sxs-lookup"><span data-stu-id="b377d-142">hello number of workers can be configured independently per app toogrant additional resources as needed.</span></span> <span data-ttu-id="b377d-143">Например:</span><span class="sxs-lookup"><span data-stu-id="b377d-143">For example:</span></span>
    - <span data-ttu-id="b377d-144">Можно установить приложение интенсивно используемых **numberOfWorkers** слишком**3** toohave дополнительные обработки емкости для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="b377d-144">A high-use app can set **numberOfWorkers** too**3** toohave more processing capacity for that app.</span></span> 
    - <span data-ttu-id="b377d-145">Установить приложения малоиспользуемых **numberOfWorkers** слишком**1**.</span><span class="sxs-lookup"><span data-stu-id="b377d-145">Low-use apps would set **numberOfWorkers** too**1**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b377d-146">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b377d-146">Next Steps</span></span>

- [<span data-ttu-id="b377d-147">Подробный обзор планов службы приложений Azure</span><span class="sxs-lookup"><span data-stu-id="b377d-147">Azure App Service plans in-depth overview</span></span>](azure-web-sites-web-hosting-plans-in-depth-overview.md)
- [<span data-ttu-id="b377d-148">Введение tooApp среды службы</span><span class="sxs-lookup"><span data-stu-id="b377d-148">Introduction tooApp Service Environment</span></span>](../app-service-web/app-service-app-service-environment-intro.md)
