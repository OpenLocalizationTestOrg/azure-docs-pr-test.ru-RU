---
title: "Автоматизация Azure Application Insights с помощью PowerShell | Документация Майкрософт"
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
ms.openlocfilehash: 88dbb9515300f847789bc889911cdeff5f5bdb53
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
#  <a name="create-application-insights-resources-using-powershell"></a><span data-ttu-id="fa53d-103">Создание ресурсов Application Insights с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="fa53d-103">Create Application Insights resources using PowerShell</span></span>
<span data-ttu-id="fa53d-104">В этой статье показано, как автоматизировать создание и обновление ресурсов [Application Insights](app-insights-overview.md) с помощью управления ресурсами Azure.</span><span class="sxs-lookup"><span data-stu-id="fa53d-104">This article shows you how to automate the creation and update of [Application Insights](app-insights-overview.md) resources automatically by using Azure Resource Management.</span></span> <span data-ttu-id="fa53d-105">Эту функцию можно использовать, например, в процессе сборки.</span><span class="sxs-lookup"><span data-stu-id="fa53d-105">You might, for example, do so as part of a build process.</span></span> <span data-ttu-id="fa53d-106">Наряду с базовым ресурсом Application Insights можно создавать [веб-тесты доступности](app-insights-monitor-web-app-availability.md) и другие ресурсы Azure, а также настраивать [оповещения](app-insights-alerts.md) и [схему цен](app-insights-pricing.md).</span><span class="sxs-lookup"><span data-stu-id="fa53d-106">Along with the basic Application Insights resource, you can create [availability web tests](app-insights-monitor-web-app-availability.md), set up [alerts](app-insights-alerts.md), set the [pricing scheme](app-insights-pricing.md), and create other Azure resources.</span></span>

<span data-ttu-id="fa53d-107">Ключ к созданию этих ресурсов — шаблоны JSON для [диспетчера ресурсов Azure](../azure-resource-manager/powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="fa53d-107">The key to creating these resources is JSON templates for [Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md).</span></span> <span data-ttu-id="fa53d-108">Порядок действий выглядит следующим образом: загрузить JSON-определения существующих ресурсов, параметризовать определенные значения как имена и выполнить шаблон, когда возникнет необходимость в создании нового ресурса.</span><span class="sxs-lookup"><span data-stu-id="fa53d-108">In a nutshell, the procedure is: download the JSON definitions of existing resources; parameterize certain values such as names; and then run the template whenever you want to create a new resource.</span></span> <span data-ttu-id="fa53d-109">Несколько ресурсов можно объединить, чтобы создавать их одновременно, например, объединить монитор приложений с тестами доступности, оповещениями и хранилищем для непрерывного экспорта.</span><span class="sxs-lookup"><span data-stu-id="fa53d-109">You can package several resources together, to create them all in one go - for example, an app monitor with availability tests, alerts, and storage for continuous export.</span></span> <span data-ttu-id="fa53d-110">С параметризацией некоторых значений связаны определенные тонкости, которые мы рассмотрим позднее.</span><span class="sxs-lookup"><span data-stu-id="fa53d-110">There are some subtleties to some of the parameterizations, which we'll explain here.</span></span>

## <a name="one-time-setup"></a><span data-ttu-id="fa53d-111">Однократная настройка</span><span class="sxs-lookup"><span data-stu-id="fa53d-111">One-time setup</span></span>
<span data-ttu-id="fa53d-112">Если вы ранее не использовали PowerShell для подписки Azure:</span><span class="sxs-lookup"><span data-stu-id="fa53d-112">If you haven't used PowerShell with your Azure subscription before:</span></span>

<span data-ttu-id="fa53d-113">Установите модуль Azure Powershell на компьютере, где требуется выполнять сценарии.</span><span class="sxs-lookup"><span data-stu-id="fa53d-113">Install the Azure Powershell module on the machine where you want to run the scripts:</span></span>

1. <span data-ttu-id="fa53d-114">Установите [установщик веб-платформы Майкрософт (версии 5 или более поздней)](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="fa53d-114">Install [Microsoft Web Platform Installer (v5 or higher)](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
2. <span data-ttu-id="fa53d-115">Используйте его для установки Microsoft Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fa53d-115">Use it to install Microsoft Azure Powershell.</span></span>

## <a name="create-an-azure-resource-manager-template"></a><span data-ttu-id="fa53d-116">Создание шаблона Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="fa53d-116">Create an Azure Resource Manager template</span></span>
<span data-ttu-id="fa53d-117">Создайте новый файл JSON — в данном примере назовем его `template1.json` .</span><span class="sxs-lookup"><span data-stu-id="fa53d-117">Create a new .json file - let's call it `template1.json` in this example.</span></span> <span data-ttu-id="fa53d-118">Скопируйте в него следующее содержимое:</span><span class="sxs-lookup"><span data-stu-id="fa53d-118">Copy this content into it:</span></span>

```JSON
    {
        "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "appName": {
                "type": "string",
                "metadata": {
                    "description": "Enter the application name."
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
                    "description": "Enter the application type."
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
                    "description": "Enter the application location."
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
                    "description": "Enter daily quota reset hour in UTC (0 to 23). Values outside the range will get a random reset hour."
                }
            },
            "warningThreshold": {
                "type": "int",
                "defaultValue": 90,
                "minValue": 1,
                "maxValue": 100,
                "metadata": {
                    "description": "Enter the % value of daily quota after which warning mail to be sent. "
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



## <a name="create-application-insights-resources"></a><span data-ttu-id="fa53d-119">Создание ресурсов Application Insights</span><span class="sxs-lookup"><span data-stu-id="fa53d-119">Create Application Insights resources</span></span>
1. <span data-ttu-id="fa53d-120">В PowerShell войдите в Azure:</span><span class="sxs-lookup"><span data-stu-id="fa53d-120">In PowerShell, sign in to Azure:</span></span>
   
    `Login-AzureRmAccount`
2. <span data-ttu-id="fa53d-121">Выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="fa53d-121">Run a command like this:</span></span>
   
    ```PS
   
        New-AzureRmResourceGroupDeployment -ResourceGroupName Fabrikam `
               -TemplateFile .\template1.json `
               -appName myNewApp

    ``` 
   
   * <span data-ttu-id="fa53d-122">`-ResourceGroupName` — группа, в которой необходимо создать ресурсы.</span><span class="sxs-lookup"><span data-stu-id="fa53d-122">`-ResourceGroupName` is the group where you want to create the new resources.</span></span>
   * <span data-ttu-id="fa53d-123">Параметр `-TemplateFile` должен предшествовать пользовательским параметрам.</span><span class="sxs-lookup"><span data-stu-id="fa53d-123">`-TemplateFile` must occur before the custom parameters.</span></span>
   * <span data-ttu-id="fa53d-124">`-appName` — имя создаваемого ресурса.</span><span class="sxs-lookup"><span data-stu-id="fa53d-124">`-appName` The name of the resource to create.</span></span>

<span data-ttu-id="fa53d-125">Можно добавить другие параметры. Их описание доступно в разделе параметров шаблона.</span><span class="sxs-lookup"><span data-stu-id="fa53d-125">You can add other parameters - you'll find their descriptions in the parameters section of the template.</span></span>

## <a name="to-get-the-instrumentation-key"></a><span data-ttu-id="fa53d-126">Получение ключа инструментирования</span><span class="sxs-lookup"><span data-stu-id="fa53d-126">To get the instrumentation key</span></span>
<span data-ttu-id="fa53d-127">После создания ресурса приложения вам понадобится ключ инструментирования.</span><span class="sxs-lookup"><span data-stu-id="fa53d-127">After creating an application resource, you'll want the instrumentation key:</span></span> 

```PS
    $resource = Find-AzureRmResource -ResourceNameEquals "<YOUR APP NAME>" -ResourceType "Microsoft.Insights/components"
    $details = Get-AzureRmResource -ResourceId $resource.ResourceId
    $ikey = $details.Properties.InstrumentationKey
```


<a id="price"></a>
## <a name="set-the-price-plan"></a><span data-ttu-id="fa53d-128">Настройка тарифного плана</span><span class="sxs-lookup"><span data-stu-id="fa53d-128">Set the price plan</span></span>

<span data-ttu-id="fa53d-129">Вы можете настроить [тарифный план](app-insights-pricing.md).</span><span class="sxs-lookup"><span data-stu-id="fa53d-129">You can set the [price plan](app-insights-pricing.md).</span></span>

<span data-ttu-id="fa53d-130">Для создания ресурса приложения с тарифным планом "Корпоративный" с помощью приведенного выше шаблона, выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="fa53d-130">To create an app resource with the Enterprise price plan, using the template above:</span></span>

```PS
        New-AzureRmResourceGroupDeployment -ResourceGroupName Fabrikam `
               -TemplateFile .\template1.json `
               -priceCode 2 `
               -appName myNewApp
```

|<span data-ttu-id="fa53d-131">priceCode</span><span class="sxs-lookup"><span data-stu-id="fa53d-131">priceCode</span></span>|<span data-ttu-id="fa53d-132">План</span><span class="sxs-lookup"><span data-stu-id="fa53d-132">plan</span></span>|
|---|---|
|<span data-ttu-id="fa53d-133">1</span><span class="sxs-lookup"><span data-stu-id="fa53d-133">1</span></span>|<span data-ttu-id="fa53d-134">базовая;</span><span class="sxs-lookup"><span data-stu-id="fa53d-134">Basic</span></span>|
|<span data-ttu-id="fa53d-135">2</span><span class="sxs-lookup"><span data-stu-id="fa53d-135">2</span></span>|<span data-ttu-id="fa53d-136">Enterprise</span><span class="sxs-lookup"><span data-stu-id="fa53d-136">Enterprise</span></span>|

* <span data-ttu-id="fa53d-137">Если вы хотите использовать только тарифный план по умолчанию "Базовый", то можете не указывать в шаблоне ресурс CurrentBillingFeatures.</span><span class="sxs-lookup"><span data-stu-id="fa53d-137">If you only want to use the default Basic price plan, you can omit the CurrentBillingFeatures resource from the template.</span></span>
* <span data-ttu-id="fa53d-138">Если вы хотите изменить ценовой план после создания ресурса компонента, можно использовать шаблон, пропускающий ресурс microsoft.insights/components.</span><span class="sxs-lookup"><span data-stu-id="fa53d-138">If you want to change the price plan after the component resource has been created, you can use a template that omits the "microsoft.insights/components" resource.</span></span> <span data-ttu-id="fa53d-139">Кроме того, опустите узел `dependsOn` из ресурса выставления счетов.</span><span class="sxs-lookup"><span data-stu-id="fa53d-139">Also, omit the `dependsOn` node from the billing resource.</span></span> 

<span data-ttu-id="fa53d-140">Чтобы проверить обновленный ценовой план, просмотрите колонку Features+pricing (Компоненты и цены) в браузере.</span><span class="sxs-lookup"><span data-stu-id="fa53d-140">To verify the updated price plan, look at the "Features+pricing" blade in the browser.</span></span> <span data-ttu-id="fa53d-141">**Обновите окно браузера**, чтобы убедиться, что отображается последнее состояние.</span><span class="sxs-lookup"><span data-stu-id="fa53d-141">**Refresh the browser view** to make sure you see the latest state.</span></span>



## <a name="add-a-metric-alert"></a><span data-ttu-id="fa53d-142">Добавление оповещения метрики</span><span class="sxs-lookup"><span data-stu-id="fa53d-142">Add a metric alert</span></span>

<span data-ttu-id="fa53d-143">Чтобы настроить оповещение метрики одновременно с ресурсом приложения, добавьте следующий код в файл шаблона:</span><span class="sxs-lookup"><span data-stu-id="fa53d-143">To set up a metric alert at the same time as your app resource, merge code like this into the template file:</span></span>

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
      // Ensure this resource is created after the app resource:
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

<span data-ttu-id="fa53d-144">При вызове шаблона можно также добавить этот параметр (при необходимости):</span><span class="sxs-lookup"><span data-stu-id="fa53d-144">When you invoke the template, you can optionally add this parameter:</span></span>

    `-responseTime 2`

<span data-ttu-id="fa53d-145">Вы можете также выполнить параметризацию других полей.</span><span class="sxs-lookup"><span data-stu-id="fa53d-145">You can of course parameterize other fields.</span></span> 

<span data-ttu-id="fa53d-146">Чтобы узнать имена типов и сведения о настройке других правил оповещения, создайте правило вручную и проверьте его в [Azure Resource Manager](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="fa53d-146">To find out the type names and configuration details of other alert rules, create a rule manually and then inspect it in [Azure Resource Manager](https://resources.azure.com/).</span></span> 


## <a name="add-an-availability-test"></a><span data-ttu-id="fa53d-147">Добавление теста доступности</span><span class="sxs-lookup"><span data-stu-id="fa53d-147">Add an availability test</span></span>

<span data-ttu-id="fa53d-148">Этот пример предназначен для проверки связи (проверки одной страницы).</span><span class="sxs-lookup"><span data-stu-id="fa53d-148">This example is for a ping test (to test a single page).</span></span>  

<span data-ttu-id="fa53d-149">Тест доступности **состоит из двух частей**: самого теста и оповещения, сообщающего об ошибках.</span><span class="sxs-lookup"><span data-stu-id="fa53d-149">**There are two parts** in an availability test: the test itself, and the alert that notifies you of failures.</span></span>

<span data-ttu-id="fa53d-150">Добавьте следующий код в файл шаблона, из которого создается приложение:</span><span class="sxs-lookup"><span data-stu-id="fa53d-150">Merge the following code into the template file that creates the app.</span></span>

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
      // Availability test: part 1 configures the test
      //
      "name": "[variables('pingTestName')]",
      "type": "Microsoft.Insights/webtests",
      "apiVersion": "2014-04-01",
      "location": "[parameters('appLocation')]",
      // Ensure this is created after the app resource:
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
          "WebTest": "[concat('<WebTest   Name=\"', variables('pingTestName'), '\"   Enabled=\"True\"         CssProjectStructure=\"\"    CssIteration=\"\"  Timeout=\"120\"  WorkItemIds=\"\"         xmlns=\"http://microsoft.com/schemas/VisualStudio/TeamTest/2010\"         Description=\"\"  CredentialUserName=\"\"  CredentialPassword=\"\"         PreAuthenticate=\"True\"  Proxy=\"default\"  StopOnError=\"False\"         RecordedResultFile=\"\"  ResultsLocale=\"\">  <Items>  <Request Method=\"GET\"    Version=\"1.1\"  Url=\"', parameters('Url'),   '\" ThinkTime=\"0\"  Timeout=\"300\" ParseDependentRequests=\"True\"         FollowRedirects=\"True\" RecordResult=\"True\" Cache=\"False\"         ResponseTimeGoal=\"0\"  Encoding=\"utf-8\"  ExpectedHttpStatusCode=\"200\"         ExpectedResponseUrl=\"\" ReportingName=\"\" IgnoreHttpStatusCode=\"False\" />        </Items>  <ValidationRules> <ValidationRule  Classname=\"Microsoft.VisualStudio.TestTools.WebTesting.Rules.ValidationRuleFindText, Microsoft.VisualStudio.QualityTools.WebTestFramework, Version=10.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a\" DisplayName=\"Find Text\"         Description=\"Verifies the existence of the specified text in the response.\"         Level=\"High\"  ExectuionOrder=\"BeforeDependents\">  <RuleParameters>        <RuleParameter Name=\"FindText\" Value=\"',   parameters('pingText'), '\" />  <RuleParameter Name=\"IgnoreCase\" Value=\"False\" />  <RuleParameter Name=\"UseRegularExpression\" Value=\"False\" />  <RuleParameter Name=\"PassIfTextFound\" Value=\"True\" />  </RuleParameters> </ValidationRule>  </ValidationRules>  </WebTest>')]"
        },
        "SyntheticMonitorId": "[variables('pingTestName')]"
      }
    },

    {
      //
      // Availability test: part 2, the alert rule
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

<span data-ttu-id="fa53d-151">Чтобы получить коды для других расположений тестирования или автоматизировать создание более сложных веб-тестов, создайте пример вручную, а затем выполните параметризацию кода из [Azure Resource Manager](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="fa53d-151">To discover the codes for other test locations, or to automate the creation of more complex web tests, create an example manually and then parameterize the code from [Azure Resource Manager](https://resources.azure.com/).</span></span>

## <a name="add-more-resources"></a><span data-ttu-id="fa53d-152">Добавление дополнительных ресурсов</span><span class="sxs-lookup"><span data-stu-id="fa53d-152">Add more resources</span></span>

<span data-ttu-id="fa53d-153">Чтобы автоматизировать создание любого другого ресурса любого типа, создайте пример вручную, а затем скопируйте его код и выполните его параметризацию из [Azure Resource Manager](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="fa53d-153">To automate the creation of any other resource of any kind, create an example manually, and then copy and parameterize its code from [Azure Resource Manager](https://resources.azure.com/).</span></span> 

1. <span data-ttu-id="fa53d-154">Откройте [диспетчер ресурсов Azure](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="fa53d-154">Open [Azure Resource Manager](https://resources.azure.com/).</span></span> <span data-ttu-id="fa53d-155">Перейдите в `subscriptions/resourceGroups/<your resource group>/providers/Microsoft.Insights/components` к своему ресурсу приложения.</span><span class="sxs-lookup"><span data-stu-id="fa53d-155">Navigate down through `subscriptions/resourceGroups/<your resource group>/providers/Microsoft.Insights/components`, to your application resource.</span></span> 
   
    ![Навигация в обозревателе ресурсов Azure](./media/app-insights-powershell/01.png)
   
    <span data-ttu-id="fa53d-157">*Компоненты* — это основные ресурсы Application Insights для отображения приложений.</span><span class="sxs-lookup"><span data-stu-id="fa53d-157">*Components* are the basic Application Insights resources for displaying applications.</span></span> <span data-ttu-id="fa53d-158">Для соответствующих правил оповещения и веб-тестов доступности имеются отдельные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="fa53d-158">There are separate resources for the associated alert rules and availability web tests.</span></span>
2. <span data-ttu-id="fa53d-159">Скопируйте JSON компонента в соответствующее место в файле `template1.json`.</span><span class="sxs-lookup"><span data-stu-id="fa53d-159">Copy the JSON of the component into the appropriate place in `template1.json`.</span></span>
3. <span data-ttu-id="fa53d-160">Удалите следующие свойства:</span><span class="sxs-lookup"><span data-stu-id="fa53d-160">Delete these properties:</span></span>
   
   * `id`
   * `InstrumentationKey`
   * `CreationDate`
   * `TenantId`
4. <span data-ttu-id="fa53d-161">Откройте разделы webtests и alertrules и скопируйте JSON для отдельных элементов в шаблон.</span><span class="sxs-lookup"><span data-stu-id="fa53d-161">Open the webtests and alertrules sections and copy the JSON for individual items into your template.</span></span> <span data-ttu-id="fa53d-162">(Не копируйте содержимое узлов webtests или alertrules, перейдите в элементы под ними.)</span><span class="sxs-lookup"><span data-stu-id="fa53d-162">(Don't copy from the webtests or alertrules nodes: go into the items under them.)</span></span>
   
    <span data-ttu-id="fa53d-163">С каждым веб-тестом связано правило оповещения, поэтому скопировать необходимо оба элемента.</span><span class="sxs-lookup"><span data-stu-id="fa53d-163">Each web test has an associated alert rule, so you have to copy both of them.</span></span>
   
    <span data-ttu-id="fa53d-164">Можно также добавить оповещения для метрик.</span><span class="sxs-lookup"><span data-stu-id="fa53d-164">You can also include alerts on metrics.</span></span> <span data-ttu-id="fa53d-165">[Имена метрик](app-insights-powershell-alerts.md#metric-names).</span><span class="sxs-lookup"><span data-stu-id="fa53d-165">[Metric names](app-insights-powershell-alerts.md#metric-names).</span></span>
5. <span data-ttu-id="fa53d-166">Вставьте в каждый ресурс следующую строку.</span><span class="sxs-lookup"><span data-stu-id="fa53d-166">Insert this line in each resource:</span></span>
   
    `"apiVersion": "2015-05-01",`

### <a name="parameterize-the-template"></a><span data-ttu-id="fa53d-167">Параметризация шаблона</span><span class="sxs-lookup"><span data-stu-id="fa53d-167">Parameterize the template</span></span>
<span data-ttu-id="fa53d-168">Теперь отдельные имена необходимо заменить параметрами.</span><span class="sxs-lookup"><span data-stu-id="fa53d-168">Now you have to replace the specific names with parameters.</span></span> <span data-ttu-id="fa53d-169">Для [параметризации шаблона](../azure-resource-manager/resource-group-authoring-templates.md) необходимо записать выражения, используя [набор вспомогательных функций](../azure-resource-manager/resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="fa53d-169">To [parameterize a template](../azure-resource-manager/resource-group-authoring-templates.md), you write expressions using a [set of helper functions](../azure-resource-manager/resource-group-template-functions.md).</span></span> 

<span data-ttu-id="fa53d-170">Параметризовать только часть строки нельзя, поэтому для формирования строки используйте `concat()` .</span><span class="sxs-lookup"><span data-stu-id="fa53d-170">You can't parameterize just part of a string, so use `concat()` to build strings.</span></span>

<span data-ttu-id="fa53d-171">Вот примеры возможных замен:</span><span class="sxs-lookup"><span data-stu-id="fa53d-171">Here are examples of the substitutions you'll want to make.</span></span> <span data-ttu-id="fa53d-172">Каждая замена используется несколько раз.</span><span class="sxs-lookup"><span data-stu-id="fa53d-172">There are several occurrences of each substitution.</span></span> <span data-ttu-id="fa53d-173">В вашем шаблоне могут потребоваться другие замены.</span><span class="sxs-lookup"><span data-stu-id="fa53d-173">You might need others in your template.</span></span> <span data-ttu-id="fa53d-174">В данных примерах используются параметры и переменные, определенные в верхней части шаблона.</span><span class="sxs-lookup"><span data-stu-id="fa53d-174">These examples use the parameters and variables we defined at the top of the template.</span></span>

| <span data-ttu-id="fa53d-175">поиск</span><span class="sxs-lookup"><span data-stu-id="fa53d-175">find</span></span> | <span data-ttu-id="fa53d-176">заменить на</span><span class="sxs-lookup"><span data-stu-id="fa53d-176">replace with</span></span> |
| --- | --- |
| `"hidden-link:/subscriptions/.../components/MyAppName"` |`"[concat('hidden-link:',`<br/>` resourceId('microsoft.insights/components',` <br/> ` parameters('appName')))]"` |
| `"/subscriptions/.../alertrules/myAlertName-myAppName-subsId",` |`"[resourceId('Microsoft.Insights/alertrules', variables('alertRuleName'))]",` |
| `"/subscriptions/.../webtests/myTestName-myAppName",` |`"[resourceId('Microsoft.Insights/webtests', parameters('webTestName'))]",` |
| `"myWebTest-myAppName"` |`"[variables(testName)]"'` |
| `"myTestName-myAppName-subsId"` |`"[variables('alertRuleName')]"` |
| `"myAppName"` |`"[parameters('appName')]"` |
| <span data-ttu-id="fa53d-177">`"myappname"` (строчная)</span><span class="sxs-lookup"><span data-stu-id="fa53d-177">`"myappname"` (lower case)</span></span> |`"[toLower(parameters('appName'))]"` |
| `"<WebTest Name=\"myWebTest\" ...`<br/>` Url=\"http://fabrikam.com/home\" ...>"` |`[concat('<WebTest Name=\"',` <br/> `parameters('webTestName'),` <br/> `'\" ... Url=\"', parameters('Url'),` <br/> `'\"...>')]"`<br/><span data-ttu-id="fa53d-178">Удалите GUID и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="fa53d-178">Delete Guid and Id.</span></span> |

### <a name="set-dependencies-between-the-resources"></a><span data-ttu-id="fa53d-179">Установка зависимостей между ресурсами</span><span class="sxs-lookup"><span data-stu-id="fa53d-179">Set dependencies between the resources</span></span>
<span data-ttu-id="fa53d-180">Служба Azure должна настраивать ресурсы в строгом порядке.</span><span class="sxs-lookup"><span data-stu-id="fa53d-180">Azure should set up the resources in strict order.</span></span> <span data-ttu-id="fa53d-181">Чтобы одна процедура настройки не начиналась прежде, чем завершится предыдущая, добавьте строки зависимости:</span><span class="sxs-lookup"><span data-stu-id="fa53d-181">To make sure one setup completes before the next begins, add dependency lines:</span></span>

* <span data-ttu-id="fa53d-182">В ресурсе теста доступности:</span><span class="sxs-lookup"><span data-stu-id="fa53d-182">In the availability test resource:</span></span>
  
    `"dependsOn": ["[resourceId('Microsoft.Insights/components', parameters('appName'))]"],`
* <span data-ttu-id="fa53d-183">В ресурсе оповещения для теста доступности:</span><span class="sxs-lookup"><span data-stu-id="fa53d-183">In the alert resource for an availability test:</span></span>
  
    `"dependsOn": ["[resourceId('Microsoft.Insights/webtests', variables('testName'))]"],`



## <a name="next-steps"></a><span data-ttu-id="fa53d-184">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fa53d-184">Next steps</span></span>
<span data-ttu-id="fa53d-185">Другие статьи об автоматизации:</span><span class="sxs-lookup"><span data-stu-id="fa53d-185">Other automation articles:</span></span>

* <span data-ttu-id="fa53d-186">[Создание ресурса Application Insights](app-insights-powershell-script-create-resource.md) — быстрый метод без использования шаблона.</span><span class="sxs-lookup"><span data-stu-id="fa53d-186">[Create an Application Insights resource](app-insights-powershell-script-create-resource.md) - quick method without using a template.</span></span>
* [<span data-ttu-id="fa53d-187">Настройка оповещений</span><span class="sxs-lookup"><span data-stu-id="fa53d-187">Set up Alerts</span></span>](app-insights-powershell-alerts.md)
* [<span data-ttu-id="fa53d-188">Creating an Application Insights Web Test and Alert Programmatically</span><span class="sxs-lookup"><span data-stu-id="fa53d-188">Create web tests</span></span>](https://azure.microsoft.com/blog/creating-a-web-test-alert-programmatically-with-application-insights/)
* [<span data-ttu-id="fa53d-189">Отправка данных системы диагностики Azure в Application Insights</span><span class="sxs-lookup"><span data-stu-id="fa53d-189">Send Azure Diagnostics to Application Insights</span></span>](app-insights-powershell-azure-diagnostics.md)
* [<span data-ttu-id="fa53d-190">Развертывание в Azure из GitHub</span><span class="sxs-lookup"><span data-stu-id="fa53d-190">Deploy to Azure from GitHub</span></span>](http://blogs.msdn.com/b/webdev/archive/2015/09/16/deploy-to-azure-from-github-with-application-insights.aspx)
* [<span data-ttu-id="fa53d-191">Создание заметок выпуска</span><span class="sxs-lookup"><span data-stu-id="fa53d-191">Create release annotations</span></span>](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/API/CreateReleaseAnnotation.ps1)

