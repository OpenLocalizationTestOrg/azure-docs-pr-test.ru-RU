---
title: "Высокая плотность размещения в службе приложений Azure | Документация Майкрософт"
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
ms.openlocfilehash: 459a310a719695f6366470976d857ec2f9d6f4a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="high-density-hosting-on-azure-app-service"></a><span data-ttu-id="04a36-103">Высокая плотность размещения в службе приложений Azure</span><span class="sxs-lookup"><span data-stu-id="04a36-103">High density hosting on Azure App Service</span></span>
<span data-ttu-id="04a36-104">При использовании службы приложений приложение отвязывается от выделяемой для него емкости двумя концепциями:</span><span class="sxs-lookup"><span data-stu-id="04a36-104">When using App Service, your application is decoupled from the capacity allocated to it by two concepts:</span></span>

* <span data-ttu-id="04a36-105">**Приложение**. Представляет приложение и конфигурацию его среды выполнения.</span><span class="sxs-lookup"><span data-stu-id="04a36-105">**The Application:** Represents the app and its runtime configuration.</span></span> <span data-ttu-id="04a36-106">Например, оно включает версию .NET, которую должна загружать среда выполнения, а также параметры приложения.</span><span class="sxs-lookup"><span data-stu-id="04a36-106">For example, it includes the version of .NET that the runtime should load, the app settings.</span></span>
* <span data-ttu-id="04a36-107">**План службы приложений**. Определяет характеристики емкости, доступный набор функций и расположение приложения.</span><span class="sxs-lookup"><span data-stu-id="04a36-107">**The App Service Plan:** Defines the characteristics of the capacity, available feature set, and locality of the application.</span></span> <span data-ttu-id="04a36-108">Это могут быть следующие характеристики: большие (четырехъядерные) компьютеры, четыре экземпляра или функции уровня "Премиум" в восточной части США.</span><span class="sxs-lookup"><span data-stu-id="04a36-108">For example, characteristics might be large (four cores) machine, four instances, Premium features in East US.</span></span>

<span data-ttu-id="04a36-109">Приложение всегда связано с одним планом службы приложений, но план службы приложений может предоставлять емкость для одного или нескольких приложений.</span><span class="sxs-lookup"><span data-stu-id="04a36-109">An app is always linked to an App Service plan, but an App Service plan can provide capacity to one or more apps.</span></span>

<span data-ttu-id="04a36-110">В результате платформа позволяет не только изолировать одно приложение, но и настроить несколько приложений так, чтобы они использовали один и тот же план службы приложений и одни и те же ресурсы.</span><span class="sxs-lookup"><span data-stu-id="04a36-110">As a result, the platform provides the flexibility to isolate a single app or have multiple apps share resources by sharing an App Service plan.</span></span>

<span data-ttu-id="04a36-111">Однако если несколько приложений совместно используют план службы приложений, один экземпляр этого приложения будет выполняться на каждом экземпляре данного плана службы приложений.</span><span class="sxs-lookup"><span data-stu-id="04a36-111">However, when multiple apps share an App Service plan, an instance of that app runs on every instance of that App Service plan.</span></span>

## <a name="per-app-scaling"></a><span data-ttu-id="04a36-112">Независимое масштабирование приложений</span><span class="sxs-lookup"><span data-stu-id="04a36-112">Per app scaling</span></span>
<span data-ttu-id="04a36-113">*Независимое масштабирование приложений* — это функция, которую можно включить на уровне плана службы приложений и затем использовать для каждого приложения.</span><span class="sxs-lookup"><span data-stu-id="04a36-113">*Per app scaling* is a feature that can be enabled at the App Service plan level and then used per application.</span></span>

<span data-ttu-id="04a36-114">Она позволяет масштабировать приложение независимо от плана службы приложений, в котором оно размещено.</span><span class="sxs-lookup"><span data-stu-id="04a36-114">Per app scaling scales an app independently from the App Service plan that hosts it.</span></span> <span data-ttu-id="04a36-115">Таким образом, план службы приложений можно увеличить до 10 экземпляров, но приложение максимально может использовать только пять.</span><span class="sxs-lookup"><span data-stu-id="04a36-115">This way, an App Service plan can be scaled to 10 instances, but an app can be set to use only five.</span></span>

   >[!NOTE]
   ><span data-ttu-id="04a36-116">Независимое масштабирование приложений доступно только для планов службы приложений с номером SKU уровня **Премиум**.</span><span class="sxs-lookup"><span data-stu-id="04a36-116">Per app scaling is available only for **Premium** SKU App Service plans</span></span>
   >

### <a name="per-app-scaling-using-powershell"></a><span data-ttu-id="04a36-117">Независимое масштабирование приложений с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="04a36-117">Per app scaling using PowerShell</span></span>

<span data-ttu-id="04a36-118">Вы можете создать план, настроенный в качестве плана с *независимым масштабированием приложений*, передав атрибут ```-perSiteScaling $true``` в командлет ```New-AzureRmAppServicePlan```.</span><span class="sxs-lookup"><span data-stu-id="04a36-118">You can create a plan configured as a *Per app scaling* plan by passing in the ```-perSiteScaling $true``` attribute to the ```New-AzureRmAppServicePlan``` commandlet</span></span>

```
New-AzureRmAppServicePlan -ResourceGroupName $ResourceGroup -Name $AppServicePlan `
                            -Location $Location `
                            -Tier Premium -WorkerSize Small `
                            -NumberofWorkers 5 -PerSiteScaling $true
```

<span data-ttu-id="04a36-119">Если вы хотите обновить существующий план службы приложений для использования этой функции:</span><span class="sxs-lookup"><span data-stu-id="04a36-119">If you want to update an existing App Service plan to use this feature:</span></span> 

- <span data-ttu-id="04a36-120">получите целевой план (```Get-AzureRmAppServicePlan```);</span><span class="sxs-lookup"><span data-stu-id="04a36-120">get the target plan ```Get-AzureRmAppServicePlan```</span></span>
- <span data-ttu-id="04a36-121">измените свойство локально (```$newASP.PerSiteScaling = $true```);</span><span class="sxs-lookup"><span data-stu-id="04a36-121">modifying the property locally ```$newASP.PerSiteScaling = $true```</span></span>
- <span data-ttu-id="04a36-122">опубликуйте изменения в Azure (```Set-AzureRmAppServicePlan```).</span><span class="sxs-lookup"><span data-stu-id="04a36-122">posting your changes back to azure ```Set-AzureRmAppServicePlan```</span></span> 

```
# Get the new App Service Plan and modify the "PerSiteScaling" property.
$newASP = Get-AzureRmAppServicePlan -ResourceGroupName $ResourceGroup -Name $AppServicePlan
$newASP

#Modify the local copy to use "PerSiteScaling" property.
$newASP.PerSiteScaling = $true
$newASP
    
#Post updated app service plan back to azure
Set-AzureRmAppServicePlan $newASP
```

<span data-ttu-id="04a36-123">На уровне приложения необходимо настроить несколько экземпляров, которые приложение сможет использовать в плане службы приложений.</span><span class="sxs-lookup"><span data-stu-id="04a36-123">At the app level, we need to configure the number of instances the app can use in the app service plan.</span></span>

<span data-ttu-id="04a36-124">В следующем примере для приложения установлено ограничение на два экземпляра независимо от того, сколько экземпляров можно развернуть в пределах базового плана службы приложений.</span><span class="sxs-lookup"><span data-stu-id="04a36-124">In the example below, the app is limited to two instances regardless of how many instances the underlying app service plan scales out to.</span></span>

```
# Get the app we want to configure to use "PerSiteScaling"
$newapp = Get-AzureRmWebApp -ResourceGroupName $ResourceGroup -Name $webapp
    
# Modify the NumberOfWorkers setting to the desired value.
$newapp.SiteConfig.NumberOfWorkers = 2
    
# Post updated app back to azure
Set-AzureRmWebApp $newapp
```

> [!IMPORTANT]
> <span data-ttu-id="04a36-125">$newapp.SiteConfig.NumberOfWorkers — это другая форма свойства $newapp.MaxNumberOfWorkers.</span><span class="sxs-lookup"><span data-stu-id="04a36-125">$newapp.SiteConfig.NumberOfWorkers is different form $newapp.MaxNumberOfWorkers.</span></span> <span data-ttu-id="04a36-126">Функция "Независимое масштабирование приложений" определяет с помощью свойства $newapp.SiteConfig.NumberOfWorkers параметры масштабирования приложения.</span><span class="sxs-lookup"><span data-stu-id="04a36-126">Per app scaling uses $newapp.SiteConfig.NumberOfWorkers to determine the scale characteristics of the app.</span></span>

### <a name="per-app-scaling-using-azure-resource-manager"></a><span data-ttu-id="04a36-127">Независимое масштабирование приложений с помощью Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="04a36-127">Per app scaling using Azure Resource Manager</span></span>

<span data-ttu-id="04a36-128">Следующий *шаблон Azure Resource Manager* создает:</span><span class="sxs-lookup"><span data-stu-id="04a36-128">The following *Azure Resource Manager template* creates:</span></span>

- <span data-ttu-id="04a36-129">план службы приложений, в пределах которого можно развернуть до 10 экземпляров;</span><span class="sxs-lookup"><span data-stu-id="04a36-129">An App Service plan that's scaled out to 10 instances</span></span>
- <span data-ttu-id="04a36-130">приложение, для которого настроено масштабирование до пяти экземпляров максимум.</span><span class="sxs-lookup"><span data-stu-id="04a36-130">an app that's configured to scale to a max of five instances.</span></span>

<span data-ttu-id="04a36-131">План службы приложений задает для свойства **PerSiteScaling** значение true (```"perSiteScaling": true```).</span><span class="sxs-lookup"><span data-stu-id="04a36-131">The App Service plan is setting the **PerSiteScaling** property to true ```"perSiteScaling": true```.</span></span> <span data-ttu-id="04a36-132">Приложение задает **количество рабочих ролей**, равное 5 (```"properties": { "numberOfWorkers": "5" }```).</span><span class="sxs-lookup"><span data-stu-id="04a36-132">The app is setting the **number of workers** to use to 5 ```"properties": { "numberOfWorkers": "5" }```.</span></span>

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

## <a name="recommended-configuration-for-high-density-hosting"></a><span data-ttu-id="04a36-133">Рекомендуемая конфигурация для высокой плотности размещения</span><span class="sxs-lookup"><span data-stu-id="04a36-133">Recommended configuration for high density hosting</span></span>
<span data-ttu-id="04a36-134">Независимое масштабирование приложений — это функция, которая включается как в глобальных регионах Azure, так и в средах службы приложений.</span><span class="sxs-lookup"><span data-stu-id="04a36-134">Per app scaling is a feature that is enabled in both global Azure regions and App Service Environments.</span></span> <span data-ttu-id="04a36-135">Однако рекомендуется использовать среды службы приложений, так как они предоставляют дополнительные возможности и пулы большей емкости.</span><span class="sxs-lookup"><span data-stu-id="04a36-135">However, the recommended strategy is to use App Service Environments to take advantage of their advanced features and the larger pools of capacity.</span></span>  

<span data-ttu-id="04a36-136">Чтобы настроить высокую плотность размещения приложений, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="04a36-136">Follow these steps to configure high density hosting for your apps:</span></span>

1. <span data-ttu-id="04a36-137">Настройте среду службы приложений и выберите рабочий пул, выделенный для сценария высокой плотности размещения.</span><span class="sxs-lookup"><span data-stu-id="04a36-137">Configure the App Service Environment and choose a worker pool that is dedicated to the high density hosting scenario.</span></span>
1. <span data-ttu-id="04a36-138">Создайте один план службы приложений и настройте его для использования всей доступной емкости в рабочем пуле.</span><span class="sxs-lookup"><span data-stu-id="04a36-138">Create a single App Service plan, and scale it to use all the available capacity on the worker pool.</span></span>
1. <span data-ttu-id="04a36-139">Задайте для флага PerSiteScaling плана службы приложений значение true.</span><span class="sxs-lookup"><span data-stu-id="04a36-139">Set the PerSiteScaling flag to true on the App Service plan.</span></span>
1. <span data-ttu-id="04a36-140">Новые приложения будут созданы и назначены этому плану службы приложений, при этом для свойства **numberOfWorkers** будет задано значение **1**.</span><span class="sxs-lookup"><span data-stu-id="04a36-140">New apps are created and assigned to that App Service plan with the **numberOfWorkers** property set to **1**.</span></span> <span data-ttu-id="04a36-141">Такая конфигурация позволит достичь максимальной плотности в этом рабочем пуле.</span><span class="sxs-lookup"><span data-stu-id="04a36-141">Using this configuration yields the highest density possible on this worker pool.</span></span>
1. <span data-ttu-id="04a36-142">Число рабочих ролей можно настроить отдельно для каждого приложения, чтобы предоставить дополнительные ресурсы согласно требованиям.</span><span class="sxs-lookup"><span data-stu-id="04a36-142">The number of workers can be configured independently per app to grant additional resources as needed.</span></span> <span data-ttu-id="04a36-143">Например:</span><span class="sxs-lookup"><span data-stu-id="04a36-143">For example:</span></span>
    - <span data-ttu-id="04a36-144">Для приложения с высоким уровнем использования свойству **numberOfWorkers** можно присвоить значение **3**, чтобы обеспечить большую вычислительную мощность для этого приложения.</span><span class="sxs-lookup"><span data-stu-id="04a36-144">A high-use app can set **numberOfWorkers** to **3** to have more processing capacity for that app.</span></span> 
    - <span data-ttu-id="04a36-145">Для приложений с низким уровнем использования свойству **numberOfWorkers** можно присвоить значение **1**.</span><span class="sxs-lookup"><span data-stu-id="04a36-145">Low-use apps would set **numberOfWorkers** to **1**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="04a36-146">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="04a36-146">Next Steps</span></span>

- [<span data-ttu-id="04a36-147">Подробный обзор планов службы приложений Azure</span><span class="sxs-lookup"><span data-stu-id="04a36-147">Azure App Service plans in-depth overview</span></span>](azure-web-sites-web-hosting-plans-in-depth-overview.md)
- [<span data-ttu-id="04a36-148">Введение в среду службы приложения</span><span class="sxs-lookup"><span data-stu-id="04a36-148">Introduction to App Service Environment</span></span>](../app-service-web/app-service-app-service-environment-intro.md)