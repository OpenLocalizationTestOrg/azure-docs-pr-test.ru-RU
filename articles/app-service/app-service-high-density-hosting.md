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
# <a name="high-density-hosting-on-azure-app-service"></a>Высокая плотность размещения в службе приложений Azure
При использовании службы приложений, приложение отсоединяется от емкости hello, занимаемый tooit двух основных понятиях:

* **Приложение Hello:** представляет приложение hello и конфигурации среды выполнения. Например, он включает hello версию .NET, hello среды выполнения необходимо загрузить, параметры приложения hello.
* **Привет, план служб приложений:** определяет характеристики hello емкости hello, набор доступных функций и расположение приложения hello. Это могут быть следующие характеристики: большие (четырехъядерные) компьютеры, четыре экземпляра или функции уровня "Премиум" в восточной части США.

Приложения всегда связанного tooan план служб приложений, однако план службы приложений можно предоставить tooone емкости или другие приложения.

В результате платформы hello обеспечивает гибкость tooisolate hello одного приложения или у нескольких приложений, общий доступ к ресурсам, предоставив план служб приложений.

Однако если несколько приложений совместно используют план службы приложений, один экземпляр этого приложения будет выполняться на каждом экземпляре данного плана службы приложений.

## <a name="per-app-scaling"></a>Независимое масштабирование приложений
*Независимое масштабирование приложений* — это функция, которую можно включить на уровне плана службы приложений и затем использовать для каждого приложения.

Она позволяет масштабировать приложение независимо от плана службы приложений, в котором оно размещено. Таким образом, план может иметь службу приложений масштабировать too10 экземпляров, но приложение может устанавливаться только пять toouse.

   >[!NOTE]
   >Независимое масштабирование приложений доступно только для планов службы приложений с номером SKU уровня **Премиум**.
   >

### <a name="per-app-scaling-using-powershell"></a>Независимое масштабирование приложений с помощью PowerShell

Можно создать план настроен в качестве *на масштабирование приложения* плана, передавая hello ```-perSiteScaling $true``` атрибута toohello ```New-AzureRmAppServicePlan``` командлетов для

```
New-AzureRmAppServicePlan -ResourceGroupName $ResourceGroup -Name $AppServicePlan `
                            -Location $Location `
                            -Tier Premium -WorkerSize Small `
                            -NumberofWorkers 5 -PerSiteScaling $true
```

Если требуется tooupdate существующей службы приложений спланировать toouse эту функцию. 

- получить hello целевого плана```Get-AzureRmAppServicePlan```
- Изменение свойства hello локально```$newASP.PerSiteScaling = $true```
- Учет к задней tooazure изменения```Set-AzureRmAppServicePlan``` 

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

На уровне приложения hello нам нужна tooconfigure hello количество экземпляров, которое можно использовать приложение hello в плане обслуживания приложения hello.

В приведенном ниже примере hello приложение hello является ограниченной tootwo экземпляров независимо от того, сколько экземпляров hello базового приложения службы плана масштабирование out для.

```
# Get hello app we want tooconfigure toouse "PerSiteScaling"
$newapp = Get-AzureRmWebApp -ResourceGroupName $ResourceGroup -Name $webapp
    
# Modify hello NumberOfWorkers setting toohello desired value.
$newapp.SiteConfig.NumberOfWorkers = 2
    
# Post updated app back tooazure
Set-AzureRmWebApp $newapp
```

> [!IMPORTANT]
> $newapp.SiteConfig.NumberOfWorkers — это другая форма свойства $newapp.MaxNumberOfWorkers. На каждое приложение масштабирование использует $newapp. SiteConfig.NumberOfWorkers toodetermine hello шкалы характеристики приложение hello.

### <a name="per-app-scaling-using-azure-resource-manager"></a>Независимое масштабирование приложений с помощью Azure Resource Manager

следующие Hello *шаблона Azure Resource Manager* создает:

- План служб приложений с масштабированием too10 экземпляров
- приложение, которое настроил tooscale tooa максимум пять экземпляров.

Hello план служб приложений является установка hello **PerSiteScaling** tootrue свойства ```"perSiteScaling": true```. устанавливает приложение Hello hello **количество работников** toouse too5 ```"properties": { "numberOfWorkers": "5" }```.

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

## <a name="recommended-configuration-for-high-density-hosting"></a>Рекомендуемая конфигурация для высокой плотности размещения
Независимое масштабирование приложений — это функция, которая включается как в глобальных регионах Azure, так и в средах службы приложений. Тем не менее hello рекомендуемая стратегия заключается в использовании среды службы приложения tootake преимущества дополнительных возможностей и hello большего пулы емкости.  

Выполните эти шаги tooconfigure высокая плотность размещения для приложения.

1. Настройте hello среды службы приложений и выберите пул работника, высокая плотность выделенный toohello вариант размещения.
1. Создать отдельный план службы приложений и масштабировать его toouse все hello доступной емкости в hello рабочего пула.
1. Установите флаг tootrue hello PerSiteScaling hello план служб приложений.
1. Новые приложения создаются и назначенный toothat план служб приложений с **numberOfWorkers** значение свойства слишком**1**. С помощью данной конфигурации дает hello максимальной плотностью возможных для этого пула работника.
1. Hello число рабочих процессов, можно настроить независимо друг от друга на дополнительные ресурсы toogrant приложения при необходимости. Например:
    - Можно установить приложение интенсивно используемых **numberOfWorkers** слишком**3** toohave дополнительные обработки емкости для этого приложения. 
    - Установить приложения малоиспользуемых **numberOfWorkers** слишком**1**.

## <a name="next-steps"></a>Дальнейшие действия

- [Подробный обзор планов службы приложений Azure](azure-web-sites-web-hosting-plans-in-depth-overview.md)
- [Введение tooApp среды службы](../app-service-web/app-service-app-service-environment-intro.md)
