---
title: "aaaAutomate аналитики приложения Azure с помощью PowerShell | Документы Microsoft"
description: "Автоматизация создания ресурсов, оповещений и тестов доступности в PowerShell с помощью шаблона Azure Resource Manager."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 9f73b87f-be63-4847-88c8-368543acad8b
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/02/2017
ms.author: bwren
ms.openlocfilehash: ebd336eafba58a690a0e8ffbd1c74f7e93dbb682
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
#  <a name="create-application-insights-resources-using-powershell"></a><span data-ttu-id="134eb-103">Создание ресурсов Application Insights с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="134eb-103">Create Application Insights resources using PowerShell</span></span>
<span data-ttu-id="134eb-104">В этой статье показано, как tooautomate hello, создание и обновление [Application Insights](app-insights-overview.md) ресурсы автоматически с помощью управления ресурсами Azure.</span><span class="sxs-lookup"><span data-stu-id="134eb-104">This article shows you how tooautomate hello creation and update of [Application Insights](app-insights-overview.md) resources automatically by using Azure Resource Management.</span></span> <span data-ttu-id="134eb-105">Эту функцию можно использовать, например, в процессе сборки.</span><span class="sxs-lookup"><span data-stu-id="134eb-105">You might, for example, do so as part of a build process.</span></span> <span data-ttu-id="134eb-106">Вместе с hello основные ресурс Application Insights, можно создать [доступности веб-тесты](app-insights-monitor-web-app-availability.md)настройте [оповещения](app-insights-alerts.md), задайте hello [цены схему](app-insights-pricing.md)и создать другой Azure ресурсы.</span><span class="sxs-lookup"><span data-stu-id="134eb-106">Along with hello basic Application Insights resource, you can create [availability web tests](app-insights-monitor-web-app-availability.md), set up [alerts](app-insights-alerts.md), set hello [pricing scheme](app-insights-pricing.md), and create other Azure resources.</span></span>

<span data-ttu-id="134eb-107">Здравствуйте ключа toocreating эти ресурсы — шаблоны JSON для [диспетчера ресурсов Azure](../azure-resource-manager/powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="134eb-107">hello key toocreating these resources is JSON templates for [Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md).</span></span> <span data-ttu-id="134eb-108">По сути, является процедуры hello: загрузить определения JSON hello имеющихся ресурсов; параметризация определенные значения, например имена; затем снова запустите шаблона hello всякий раз, когда требуется toocreate новый ресурс.</span><span class="sxs-lookup"><span data-stu-id="134eb-108">In a nutshell, hello procedure is: download hello JSON definitions of existing resources; parameterize certain values such as names; and then run hello template whenever you want toocreate a new resource.</span></span> <span data-ttu-id="134eb-109">Вы можете компоновать несколько ресурсы вместе, toocreate их все в одном откройте - например, монитор приложения с тестов доступности, оповещения и хранилище для непрерывного экспорта.</span><span class="sxs-lookup"><span data-stu-id="134eb-109">You can package several resources together, toocreate them all in one go - for example, an app monitor with availability tests, alerts, and storage for continuous export.</span></span> <span data-ttu-id="134eb-110">Существуют некоторые toosome тонкостей для параметризации hello, которые будут описаны ниже.</span><span class="sxs-lookup"><span data-stu-id="134eb-110">There are some subtleties toosome of hello parameterizations, which we'll explain here.</span></span>

## <a name="one-time-setup"></a><span data-ttu-id="134eb-111">Однократная настройка</span><span class="sxs-lookup"><span data-stu-id="134eb-111">One-time setup</span></span>
<span data-ttu-id="134eb-112">Если вы ранее не использовали PowerShell для подписки Azure:</span><span class="sxs-lookup"><span data-stu-id="134eb-112">If you haven't used PowerShell with your Azure subscription before:</span></span>

<span data-ttu-id="134eb-113">Установка модуля Azure Powershell hello на hello компьютер, где toorun hello сценариев:</span><span class="sxs-lookup"><span data-stu-id="134eb-113">Install hello Azure Powershell module on hello machine where you want toorun hello scripts:</span></span>

1. <span data-ttu-id="134eb-114">Установите [установщик веб-платформы Майкрософт (версии 5 или более поздней)](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="134eb-114">Install [Microsoft Web Platform Installer (v5 or higher)](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
2. <span data-ttu-id="134eb-115">Используйте tooinstall Microsoft Azure Powershell.</span><span class="sxs-lookup"><span data-stu-id="134eb-115">Use it tooinstall Microsoft Azure Powershell.</span></span>

## <a name="create-an-azure-resource-manager-template"></a><span data-ttu-id="134eb-116">Создание шаблона Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="134eb-116">Create an Azure Resource Manager template</span></span>
<span data-ttu-id="134eb-117">Создайте новый файл JSON — в данном примере назовем его `template1.json` .</span><span class="sxs-lookup"><span data-stu-id="134eb-117">Create a new .json file - let's call it `template1.json` in this example.</span></span> <span data-ttu-id="134eb-118">Скопируйте в него следующее содержимое:</span><span class="sxs-lookup"><span data-stu-id="134eb-118">Copy this content into it:</span></span>

```JSON
    {
        "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "appName": {
                "type": "string",
                "metadata": {
                    "description": "Enter hello application name."
                }
            },
            "appType": {
                "type": "string",
                "defaultValue": "web",
                "allowedValues": [
                    "web",
                    "java",
                    "HockeyAppBridge",
                    "other"
                ],
                "metadata": {
                    "description": "Enter hello application type."
                }
            },
            "appLocation": {
                "type": "string",
                "defaultValue": "East US",
                "allowedValues": [
                    "South Central US",
                    "West Europe",
                    "East US",
                    "North Europe"
                ],
                "metadata": {
                    "description": "Enter hello application location."
                }
            },
            "priceCode": {
                "type": "int",
                "defaultValue": 1,
                "allowedValues": [
                    1,
                    2
                ],
                "metadata": {
                    "description": "1 = Basic, 2 = Enterprise"
                }
            },
            "dailyQuota": {
                "type": "int",
                "defaultValue": 100,
                "minValue": 1,
                "metadata": {
                    "description": "Enter daily quota in GB."
                }
            },
            "dailyQuotaResetTime": {
                "type": "int",
                "defaultValue": 24,
                "metadata": {
                    "description": "Enter daily quota reset hour in UTC (0 too23). Values outside hello range will get a random reset hour."
                }
            },
            "warningThreshold": {
                "type": "int",
                "defaultValue": 90,
                "minValue": 1,
                "maxValue": 100,
                "metadata": {
                    "description": "Enter hello % value of daily quota after which warning mail toobe sent. "
                }
            }
        },
        "variables": {
            "priceArray": [
                "Basic",
                "Application Insights Enterprise"
            ],
            "pricePlan": "[take(variables('priceArray'),parameters('priceCode'))]",
            "billingplan": "[concat(parameters('appName'),'/', variables('pricePlan')[0])]"
        },
        "resources": [
            {
                "type": "microsoft.insights/components",
                "kind": "[parameters('appType')]",
                "name": "[parameters('appName')]",
                "apiVersion": "2014-04-01",
                "location": "[parameters('appLocation')]",
                "tags": {},
                "properties": {
                    "ApplicationId": "[parameters('appName')]"
                },
                "dependsOn": []
            },
            {
                "name": "[variables('billingplan')]",
                "type": "microsoft.insights/components/CurrentBillingFeatures",
                "location": "[parameters('appLocation')]",
                "apiVersion": "2015-05-01",
                "dependsOn": [
                    "[resourceId('microsoft.insights/components', parameters('appName'))]"
                ],
                "properties": {
                    "CurrentBillingFeatures": "[variables('pricePlan')]",
                    "DataVolumeCap": {
                        "Cap": "[parameters('dailyQuota')]",
                        "WarningThreshold": "[parameters('warningThreshold')]",
                        "ResetTime": "[parameters('dailyQuotaResetTime')]"
                    }
                }
            }
        ]
    }
```



## <a name="create-application-insights-resources"></a><span data-ttu-id="134eb-119">Создание ресурсов Application Insights</span><span class="sxs-lookup"><span data-stu-id="134eb-119">Create Application Insights resources</span></span>
1. <span data-ttu-id="134eb-120">В PowerShell войдите в tooAzure:</span><span class="sxs-lookup"><span data-stu-id="134eb-120">In PowerShell, sign in tooAzure:</span></span>
   
    `Login-AzureRmAccount`
2. <span data-ttu-id="134eb-121">Выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="134eb-121">Run a command like this:</span></span>
   
    ```PS
   
        New-AzureRmResourceGroupDeployment -ResourceGroupName Fabrikam `
               -TemplateFile .\template1.json `
               -appName myNewApp

    ``` 
   
   * <span data-ttu-id="134eb-122">`-ResourceGroupName`— hello группы, которую toocreate hello новые ресурсы.</span><span class="sxs-lookup"><span data-stu-id="134eb-122">`-ResourceGroupName` is hello group where you want toocreate hello new resources.</span></span>
   * <span data-ttu-id="134eb-123">`-TemplateFile`должна предшествовать hello настраиваемых параметров.</span><span class="sxs-lookup"><span data-stu-id="134eb-123">`-TemplateFile` must occur before hello custom parameters.</span></span>
   * <span data-ttu-id="134eb-124">`-appName`Имя ресурса toocreate hello Hello.</span><span class="sxs-lookup"><span data-stu-id="134eb-124">`-appName` hello name of hello resource toocreate.</span></span>

<span data-ttu-id="134eb-125">Можно добавить другие параметры - вы найдете в разделе параметров hello шаблона hello их описания.</span><span class="sxs-lookup"><span data-stu-id="134eb-125">You can add other parameters - you'll find their descriptions in hello parameters section of hello template.</span></span>

## <a name="tooget-hello-instrumentation-key"></a><span data-ttu-id="134eb-126">ключ инструментирования tooget hello</span><span class="sxs-lookup"><span data-stu-id="134eb-126">tooget hello instrumentation key</span></span>
<span data-ttu-id="134eb-127">После создания ресурса приложения, потребуется ключ инструментирования hello:</span><span class="sxs-lookup"><span data-stu-id="134eb-127">After creating an application resource, you'll want hello instrumentation key:</span></span> 

```PS
    $resource = Find-AzureRmResource -ResourceNameEquals "<YOUR APP NAME>" -ResourceType "Microsoft.Insights/components"
    $details = Get-AzureRmResource -ResourceId $resource.ResourceId
    $ikey = $details.Properties.InstrumentationKey
```


<a id="price"></a>
## <a name="set-hello-price-plan"></a><span data-ttu-id="134eb-128">Набор hello цена плана</span><span class="sxs-lookup"><span data-stu-id="134eb-128">Set hello price plan</span></span>

<span data-ttu-id="134eb-129">Можно задать hello [цена плана](app-insights-pricing.md).</span><span class="sxs-lookup"><span data-stu-id="134eb-129">You can set hello [price plan](app-insights-pricing.md).</span></span>

<span data-ttu-id="134eb-130">toocreate ресурс приложения с планом цены Enterprise hello, с помощью шаблона hello выше:</span><span class="sxs-lookup"><span data-stu-id="134eb-130">toocreate an app resource with hello Enterprise price plan, using hello template above:</span></span>

```PS
        New-AzureRmResourceGroupDeployment -ResourceGroupName Fabrikam `
               -TemplateFile .\template1.json `
               -priceCode 2 `
               -appName myNewApp
```

|<span data-ttu-id="134eb-131">priceCode</span><span class="sxs-lookup"><span data-stu-id="134eb-131">priceCode</span></span>|<span data-ttu-id="134eb-132">План</span><span class="sxs-lookup"><span data-stu-id="134eb-132">plan</span></span>|
|---|---|
|<span data-ttu-id="134eb-133">1</span><span class="sxs-lookup"><span data-stu-id="134eb-133">1</span></span>|<span data-ttu-id="134eb-134">базовая;</span><span class="sxs-lookup"><span data-stu-id="134eb-134">Basic</span></span>|
|<span data-ttu-id="134eb-135">2</span><span class="sxs-lookup"><span data-stu-id="134eb-135">2</span></span>|<span data-ttu-id="134eb-136">Enterprise</span><span class="sxs-lookup"><span data-stu-id="134eb-136">Enterprise</span></span>|

* <span data-ttu-id="134eb-137">Требуется только план базовой цены по умолчанию hello toouse можно опустить hello CurrentBillingFeatures ресурсов на основе шаблона hello.</span><span class="sxs-lookup"><span data-stu-id="134eb-137">If you only want toouse hello default Basic price plan, you can omit hello CurrentBillingFeatures resource from hello template.</span></span>
* <span data-ttu-id="134eb-138">Если требуется toochange hello цена плана после создания ресурса компонента hello, можно использовать шаблон, который опускает hello ресурсов «Microsoft.Insights/Components.».</span><span class="sxs-lookup"><span data-stu-id="134eb-138">If you want toochange hello price plan after hello component resource has been created, you can use a template that omits hello "microsoft.insights/components" resource.</span></span> <span data-ttu-id="134eb-139">Кроме того, пропустите hello `dependsOn` узел из hello выставления счетов ресурсов.</span><span class="sxs-lookup"><span data-stu-id="134eb-139">Also, omit hello `dependsOn` node from hello billing resource.</span></span> 

<span data-ttu-id="134eb-140">tooverify Здравствуйте плана обновленная цена, просмотрите колонку hello «Компоненты + цены» в браузере hello.</span><span class="sxs-lookup"><span data-stu-id="134eb-140">tooverify hello updated price plan, look at hello "Features+pricing" blade in hello browser.</span></span> <span data-ttu-id="134eb-141">**Обновите представление браузера hello** toomake убедиться, что вы видите hello последнее состояние.</span><span class="sxs-lookup"><span data-stu-id="134eb-141">**Refresh hello browser view** toomake sure you see hello latest state.</span></span>



## <a name="add-a-metric-alert"></a><span data-ttu-id="134eb-142">Добавление оповещения метрики</span><span class="sxs-lookup"><span data-stu-id="134eb-142">Add a metric alert</span></span>

<span data-ttu-id="134eb-143">tooset копирование метрики предупреждение в hello одновременную как ресурс приложения, слияния следующий код в файл шаблона hello:</span><span class="sxs-lookup"><span data-stu-id="134eb-143">tooset up a metric alert at hello same time as your app resource, merge code like this into hello template file:</span></span>

```JSON
{
    parameters: { ... // existing parameters ...
            "responseTime": {
              "type": "int",
              "defaultValue": 3,
              "minValue": 1,
              "metadata": {
                "description": "Enter response time threshold in seconds."
              }
    },
    variables: { ... // existing variables ...
      // Alert names must be unique within resource group.
      "responseAlertName": "[concat('ResponseTime-', toLower(parameters('appName')))]"
    }, 
    resources: { ... // existing resources ...
     {
      //
      // Metric alert on response time
      //
      "name": "[variables('responseAlertName')]",
      "type": "Microsoft.Insights/alertrules",
      "apiVersion": "2014-04-01",
      "location": "[parameters('appLocation')]",
      // Ensure this resource is created after hello app resource:
      "dependsOn": [
        "[resourceId('Microsoft.Insights/components', parameters('appName'))]"
      ],
      "tags": {
        "[concat('hidden-link:', resourceId('Microsoft.Insights/components', parameters('appName')))]": "Resource"
      },
      "properties": {
        "name": "[variables('responseAlertName')]",
        "description": "response time alert",
        "isEnabled": true,
        "condition": {
          "$type": "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.ThresholdRuleCondition, Microsoft.WindowsAzure.Management.Mon.Client",
          "odata.type": "Microsoft.Azure.Management.Insights.Models.ThresholdRuleCondition",
          "dataSource": {
            "$type": "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleMetricDataSource, Microsoft.WindowsAzure.Management.Mon.Client",
            "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleMetricDataSource",
            "resourceUri": "[resourceId('microsoft.insights/components', parameters('appName'))]",
            "metricName": "request.duration"
          },
          "threshold": "[parameters('responseTime')]", //seconds
          "windowSize": "PT15M" // Take action if changed state for 15 minutes
        },
        "actions": [
          {
            "$type": "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleEmailAction, Microsoft.WindowsAzure.Management.Mon.Client",
            "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
            "sendToServiceOwners": true,
            "customEmails": []
          }
        ]
      }
    }
}
```

<span data-ttu-id="134eb-144">При вызове шаблона hello, при необходимости можно добавить следующий параметр:</span><span class="sxs-lookup"><span data-stu-id="134eb-144">When you invoke hello template, you can optionally add this parameter:</span></span>

    `-responseTime 2`

<span data-ttu-id="134eb-145">Вы можете также выполнить параметризацию других полей.</span><span class="sxs-lookup"><span data-stu-id="134eb-145">You can of course parameterize other fields.</span></span> 

<span data-ttu-id="134eb-146">toofind имена типов hello и сведения о конфигурации других правил оповещения вручную создать правило, а затем проверьте его на [диспетчера ресурсов Azure](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="134eb-146">toofind out hello type names and configuration details of other alert rules, create a rule manually and then inspect it in [Azure Resource Manager](https://resources.azure.com/).</span></span> 


## <a name="add-an-availability-test"></a><span data-ttu-id="134eb-147">Добавление теста доступности</span><span class="sxs-lookup"><span data-stu-id="134eb-147">Add an availability test</span></span>

<span data-ttu-id="134eb-148">Этот пример предназначен для проверки связи (tootest отдельную страницу).</span><span class="sxs-lookup"><span data-stu-id="134eb-148">This example is for a ping test (tootest a single page).</span></span>  

<span data-ttu-id="134eb-149">**Состоит из двух частей** в тест доступности: hello тест и hello оповещения, уведомляющее о сбоев.</span><span class="sxs-lookup"><span data-stu-id="134eb-149">**There are two parts** in an availability test: hello test itself, and hello alert that notifies you of failures.</span></span>

<span data-ttu-id="134eb-150">Слияние hello, следующий код в файл шаблона hello, которое создает приложение hello.</span><span class="sxs-lookup"><span data-stu-id="134eb-150">Merge hello following code into hello template file that creates hello app.</span></span>

```JSON
{
    parameters: { ... // existing parameters here ...
      "pingURL": { "type": "string" },
      "pingText": { "type": "string" , defaultValue: ""}
    },
    variables: { ... // existing variables here ...
      "pingTestName":"[concat('PingTest-', toLower(parameters('appName')))]",
      "pingAlertRuleName": "[concat('PingAlert-', toLower(parameters('appName')), '-', subscription().subscriptionId)]"
    },
    resources: { ... // existing resources here ...
    { //
      // Availability test: part 1 configures hello test
      //
      "name": "[variables('pingTestName')]",
      "type": "Microsoft.Insights/webtests",
      "apiVersion": "2014-04-01",
      "location": "[parameters('appLocation')]",
      // Ensure this is created after hello app resource:
      "dependsOn": [
        "[resourceId('Microsoft.Insights/components', parameters('appName'))]"
      ],
      "tags": {
        "[concat('hidden-link:', resourceId('Microsoft.Insights/components', parameters('appName')))]": "Resource"
      },
      "properties": {
        "Name": "[variables('pingTestName')]",
        "Description": "Basic ping test",
        "Enabled": true,
        "Frequency": 900, // 15 minutes
        "Timeout": 120, // 2 minutes
        "Kind": "ping", // single URL test
        "RetryEnabled": true,
        "Locations": [
          {
            "Id": "us-va-ash-azr"
          },
          {
            "Id": "emea-nl-ams-azr"
          },
          {
            "Id": "apac-jp-kaw-edge"
          }
        ],
        "Configuration": {
          "WebTest": "[concat('<WebTest   Name=\"', variables('pingTestName'), '\"   Enabled=\"True\"         CssProjectStructure=\"\"    CssIteration=\"\"  Timeout=\"120\"  WorkItemIds=\"\"         xmlns=\"http://microsoft.com/schemas/VisualStudio/TeamTest/2010\"         Description=\"\"  CredentialUserName=\"\"  CredentialPassword=\"\"         PreAuthenticate=\"True\"  Proxy=\"default\"  StopOnError=\"False\"         RecordedResultFile=\"\"  ResultsLocale=\"\">  <Items>  <Request Method=\"GET\"    Version=\"1.1\"  Url=\"', parameters('Url'),   '\" ThinkTime=\"0\"  Timeout=\"300\" ParseDependentRequests=\"True\"         FollowRedirects=\"True\" RecordResult=\"True\" Cache=\"False\"         ResponseTimeGoal=\"0\"  Encoding=\"utf-8\"  ExpectedHttpStatusCode=\"200\"         ExpectedResponseUrl=\"\" ReportingName=\"\" IgnoreHttpStatusCode=\"False\" />        </Items>  <ValidationRules> <ValidationRule  Classname=\"Microsoft.VisualStudio.TestTools.WebTesting.Rules.ValidationRuleFindText, Microsoft.VisualStudio.QualityTools.WebTestFramework, Version=10.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a\" DisplayName=\"Find Text\"         Description=\"Verifies hello existence of hello specified text in hello response.\"         Level=\"High\"  ExectuionOrder=\"BeforeDependents\">  <RuleParameters>        <RuleParameter Name=\"FindText\" Value=\"',   parameters('pingText'), '\" />  <RuleParameter Name=\"IgnoreCase\" Value=\"False\" />  <RuleParameter Name=\"UseRegularExpression\" Value=\"False\" />  <RuleParameter Name=\"PassIfTextFound\" Value=\"True\" />  </RuleParameters> </ValidationRule>  </ValidationRules>  </WebTest>')]"
        },
        "SyntheticMonitorId": "[variables('pingTestName')]"
      }
    },

    {
      //
      // Availability test: part 2, hello alert rule
      //
      "name": "[variables('pingAlertRuleName')]",
      "type": "Microsoft.Insights/alertrules",
      "apiVersion": "2014-04-01",
      "location": "[parameters('appLocation')]", 
      "dependsOn": [
        "[resourceId('Microsoft.Insights/webtests', variables('pingTestName'))]"
      ],
      "tags": {
        "[concat('hidden-link:', resourceId('Microsoft.Insights/components', parameters('appName')))]": "Resource",
        "[concat('hidden-link:', resourceId('Microsoft.Insights/webtests', variables('pingTestName')))]": "Resource"
      },
      "properties": {
        "name": "[variables('pingAlertRuleName')]",
        "description": "alert for web test",
        "isEnabled": true,
        "condition": {
          "$type": "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.LocationThresholdRuleCondition, Microsoft.WindowsAzure.Management.Mon.Client",
          "odata.type": "Microsoft.Azure.Management.Insights.Models.LocationThresholdRuleCondition",
          "dataSource": {
            "$type": "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleMetricDataSource, Microsoft.WindowsAzure.Management.Mon.Client",
            "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleMetricDataSource",
            "resourceUri": "[resourceId('microsoft.insights/webtests', variables('pingTestName'))]",
            "metricName": "GSMT_AvRaW"
          },
          "windowSize": "PT15M", // Take action if changed state for 15 minutes
          "failedLocationCount": 2
        },
        "actions": [
          {
            "$type": "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.RuleEmailAction, Microsoft.WindowsAzure.Management.Mon.Client",
            "odata.type": "Microsoft.Azure.Management.Insights.Models.RuleEmailAction",
            "sendToServiceOwners": true,
            "customEmails": []
          }
        ]
      }
    }
}
```

<span data-ttu-id="134eb-151">коды hello toodiscover для других расположений теста или tooautomate hello создания более сложных веб-тестов, необходимо вручную создать пример и затем параметризовать кода hello из [диспетчера ресурсов Azure](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="134eb-151">toodiscover hello codes for other test locations, or tooautomate hello creation of more complex web tests, create an example manually and then parameterize hello code from [Azure Resource Manager](https://resources.azure.com/).</span></span>

## <a name="add-more-resources"></a><span data-ttu-id="134eb-152">Добавление дополнительных ресурсов</span><span class="sxs-lookup"><span data-stu-id="134eb-152">Add more resources</span></span>

<span data-ttu-id="134eb-153">создания hello tooautomate любого рода, любой другой ресурс вручную, создать пример, затем скопируйте и параметризовать свой код из [диспетчера ресурсов Azure](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="134eb-153">tooautomate hello creation of any other resource of any kind, create an example manually, and then copy and parameterize its code from [Azure Resource Manager](https://resources.azure.com/).</span></span> 

1. <span data-ttu-id="134eb-154">Откройте [диспетчер ресурсов Azure](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="134eb-154">Open [Azure Resource Manager](https://resources.azure.com/).</span></span> <span data-ttu-id="134eb-155">Перейдите вниз до `subscriptions/resourceGroups/<your resource group>/providers/Microsoft.Insights/components`, tooyour ресурса приложения.</span><span class="sxs-lookup"><span data-stu-id="134eb-155">Navigate down through `subscriptions/resourceGroups/<your resource group>/providers/Microsoft.Insights/components`, tooyour application resource.</span></span> 
   
    ![Навигация в обозревателе ресурсов Azure](./media/app-insights-powershell/01.png)
   
    <span data-ttu-id="134eb-157">*Компоненты* являются hello основные ресурсы Application Insights для отображения приложений.</span><span class="sxs-lookup"><span data-stu-id="134eb-157">*Components* are hello basic Application Insights resources for displaying applications.</span></span> <span data-ttu-id="134eb-158">Существуют отдельные ресурсы для hello связанные правила оповещения и доступности веб-тестов.</span><span class="sxs-lookup"><span data-stu-id="134eb-158">There are separate resources for hello associated alert rules and availability web tests.</span></span>
2. <span data-ttu-id="134eb-159">Копировать hello JSON компонента hello в соответствующее место hello в `template1.json`.</span><span class="sxs-lookup"><span data-stu-id="134eb-159">Copy hello JSON of hello component into hello appropriate place in `template1.json`.</span></span>
3. <span data-ttu-id="134eb-160">Удалите следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="134eb-160">Delete these properties:</span></span>
   
   * `id`
   * `InstrumentationKey`
   * `CreationDate`
   * `TenantId`
4. <span data-ttu-id="134eb-161">Откройте разделы webtests и alertrules hello и скопируйте hello JSON для отдельных элементов в шаблон.</span><span class="sxs-lookup"><span data-stu-id="134eb-161">Open hello webtests and alertrules sections and copy hello JSON for individual items into your template.</span></span> <span data-ttu-id="134eb-162">(Не копировать с hello webtests или alertrules узлов: перейдите в элементы hello, находящихся на них.)</span><span class="sxs-lookup"><span data-stu-id="134eb-162">(Don't copy from hello webtests or alertrules nodes: go into hello items under them.)</span></span>
   
    <span data-ttu-id="134eb-163">Каждой веб-теста имеет соответствующее правило генерации оповещений, поэтому у вас есть toocopy оба из них.</span><span class="sxs-lookup"><span data-stu-id="134eb-163">Each web test has an associated alert rule, so you have toocopy both of them.</span></span>
   
    <span data-ttu-id="134eb-164">Можно также добавить оповещения для метрик.</span><span class="sxs-lookup"><span data-stu-id="134eb-164">You can also include alerts on metrics.</span></span> <span data-ttu-id="134eb-165">[Имена метрик](app-insights-powershell-alerts.md#metric-names).</span><span class="sxs-lookup"><span data-stu-id="134eb-165">[Metric names](app-insights-powershell-alerts.md#metric-names).</span></span>
5. <span data-ttu-id="134eb-166">Вставьте в каждый ресурс следующую строку.</span><span class="sxs-lookup"><span data-stu-id="134eb-166">Insert this line in each resource:</span></span>
   
    `"apiVersion": "2015-05-01",`

### <a name="parameterize-hello-template"></a><span data-ttu-id="134eb-167">Параметризация hello шаблона</span><span class="sxs-lookup"><span data-stu-id="134eb-167">Parameterize hello template</span></span>
<span data-ttu-id="134eb-168">Теперь у вас tooreplace hello конкретных имен параметров.</span><span class="sxs-lookup"><span data-stu-id="134eb-168">Now you have tooreplace hello specific names with parameters.</span></span> <span data-ttu-id="134eb-169">слишком[параметризовать шаблона](../azure-resource-manager/resource-group-authoring-templates.md), запись выражениях, использующих [набор вспомогательных функций](../azure-resource-manager/resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="134eb-169">too[parameterize a template](../azure-resource-manager/resource-group-authoring-templates.md), you write expressions using a [set of helper functions](../azure-resource-manager/resource-group-template-functions.md).</span></span> 

<span data-ttu-id="134eb-170">Не удается параметризировать только часть строки, поэтому следует использовать `concat()` toobuild строки.</span><span class="sxs-lookup"><span data-stu-id="134eb-170">You can't parameterize just part of a string, so use `concat()` toobuild strings.</span></span>

<span data-ttu-id="134eb-171">Ниже приведены примеры подстановок hello нужно toomake.</span><span class="sxs-lookup"><span data-stu-id="134eb-171">Here are examples of hello substitutions you'll want toomake.</span></span> <span data-ttu-id="134eb-172">Каждая замена используется несколько раз.</span><span class="sxs-lookup"><span data-stu-id="134eb-172">There are several occurrences of each substitution.</span></span> <span data-ttu-id="134eb-173">В вашем шаблоне могут потребоваться другие замены.</span><span class="sxs-lookup"><span data-stu-id="134eb-173">You might need others in your template.</span></span> <span data-ttu-id="134eb-174">Эти примеры используйте hello параметров и переменных, который мы определили вверху hello hello шаблона.</span><span class="sxs-lookup"><span data-stu-id="134eb-174">These examples use hello parameters and variables we defined at hello top of hello template.</span></span>

| <span data-ttu-id="134eb-175">поиск</span><span class="sxs-lookup"><span data-stu-id="134eb-175">find</span></span> | <span data-ttu-id="134eb-176">заменить на</span><span class="sxs-lookup"><span data-stu-id="134eb-176">replace with</span></span> |
| --- | --- |
| `"hidden-link:/subscriptions/.../components/MyAppName"` |`"[concat('hidden-link:',`<br/>` resourceId('microsoft.insights/components',` <br/> ` parameters('appName')))]"` |
| `"/subscriptions/.../alertrules/myAlertName-myAppName-subsId",` |`"[resourceId('Microsoft.Insights/alertrules', variables('alertRuleName'))]",` |
| `"/subscriptions/.../webtests/myTestName-myAppName",` |`"[resourceId('Microsoft.Insights/webtests', parameters('webTestName'))]",` |
| `"myWebTest-myAppName"` |`"[variables(testName)]"'` |
| `"myTestName-myAppName-subsId"` |`"[variables('alertRuleName')]"` |
| `"myAppName"` |`"[parameters('appName')]"` |
| <span data-ttu-id="134eb-177">`"myappname"` (строчная)</span><span class="sxs-lookup"><span data-stu-id="134eb-177">`"myappname"` (lower case)</span></span> |`"[toLower(parameters('appName'))]"` |
| `"<WebTest Name=\"myWebTest\" ...`<br/>` Url=\"http://fabrikam.com/home\" ...>"` |`[concat('<WebTest Name=\"',` <br/> `parameters('webTestName'),` <br/> `'\" ... Url=\"', parameters('Url'),` <br/> `'\"...>')]"`<br/><span data-ttu-id="134eb-178">Удалите GUID и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="134eb-178">Delete Guid and Id.</span></span> |

### <a name="set-dependencies-between-hello-resources"></a><span data-ttu-id="134eb-179">Набор зависимостей между ресурсами hello</span><span class="sxs-lookup"><span data-stu-id="134eb-179">Set dependencies between hello resources</span></span>
<span data-ttu-id="134eb-180">Azure следует настроить ресурсы hello в строгом порядке.</span><span class="sxs-lookup"><span data-stu-id="134eb-180">Azure should set up hello resources in strict order.</span></span> <span data-ttu-id="134eb-181">том, что был задан завершения перед выполнением hello рядом toomake добавьте строки зависимостей:</span><span class="sxs-lookup"><span data-stu-id="134eb-181">toomake sure one setup completes before hello next begins, add dependency lines:</span></span>

* <span data-ttu-id="134eb-182">В доступности hello проверку ресурсов:</span><span class="sxs-lookup"><span data-stu-id="134eb-182">In hello availability test resource:</span></span>
  
    `"dependsOn": ["[resourceId('Microsoft.Insights/components', parameters('appName'))]"],`
* <span data-ttu-id="134eb-183">В ресурсе предупреждения hello для тест доступности:</span><span class="sxs-lookup"><span data-stu-id="134eb-183">In hello alert resource for an availability test:</span></span>
  
    `"dependsOn": ["[resourceId('Microsoft.Insights/webtests', variables('testName'))]"],`



## <a name="next-steps"></a><span data-ttu-id="134eb-184">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="134eb-184">Next steps</span></span>
<span data-ttu-id="134eb-185">Другие статьи об автоматизации:</span><span class="sxs-lookup"><span data-stu-id="134eb-185">Other automation articles:</span></span>

* <span data-ttu-id="134eb-186">[Создание ресурса Application Insights](app-insights-powershell-script-create-resource.md) — быстрый метод без использования шаблона.</span><span class="sxs-lookup"><span data-stu-id="134eb-186">[Create an Application Insights resource](app-insights-powershell-script-create-resource.md) - quick method without using a template.</span></span>
* [<span data-ttu-id="134eb-187">Настройка оповещений</span><span class="sxs-lookup"><span data-stu-id="134eb-187">Set up Alerts</span></span>](app-insights-powershell-alerts.md)
* [<span data-ttu-id="134eb-188">Creating an Application Insights Web Test and Alert Programmatically</span><span class="sxs-lookup"><span data-stu-id="134eb-188">Create web tests</span></span>](https://azure.microsoft.com/blog/creating-a-web-test-alert-programmatically-with-application-insights/)
* [<span data-ttu-id="134eb-189">Отправить аналитики tooApplication диагностики Azure</span><span class="sxs-lookup"><span data-stu-id="134eb-189">Send Azure Diagnostics tooApplication Insights</span></span>](app-insights-powershell-azure-diagnostics.md)
* [<span data-ttu-id="134eb-190">Развертывание tooAzure из GitHub</span><span class="sxs-lookup"><span data-stu-id="134eb-190">Deploy tooAzure from GitHub</span></span>](http://blogs.msdn.com/b/webdev/archive/2015/09/16/deploy-to-azure-from-github-with-application-insights.aspx)
* [<span data-ttu-id="134eb-191">Создание заметок выпуска</span><span class="sxs-lookup"><span data-stu-id="134eb-191">Create release annotations</span></span>](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/API/CreateReleaseAnnotation.ps1)

