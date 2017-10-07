---
title: "aaaAutomatically Включение параметров диагностики с помощью шаблона диспетчера ресурсов | Документы Microsoft"
description: "Узнайте, как toouse диспетчера ресурсов шаблона toocreate параметров диагностики, позволяющие toostream вашей диагностики журналы tooEvent концентраторов и сохранять их в учетной записи хранилища."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: a8a88a8c-4a48-4df6-8f7e-d90634d39c57
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 2/14/2017
ms.author: johnkem
ms.openlocfilehash: 8f38731107029928029c6d940da7bd076fea5d49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="automatically-enable-diagnostic-settings-at-resource-creation-using-a-resource-manager-template"></a><span data-ttu-id="3171c-103">Автоматическое включение параметров диагностики при создании ресурса из шаблона Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3171c-103">Automatically enable Diagnostic Settings at resource creation using a Resource Manager template</span></span>
<span data-ttu-id="3171c-104">В этой статье показано, как можно использовать [шаблона Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) tooconfigure параметров диагностики для ресурса при его создании.</span><span class="sxs-lookup"><span data-stu-id="3171c-104">In this article we show how you can use an [Azure Resource Manager template](../azure-resource-manager/resource-group-authoring-templates.md) tooconfigure Diagnostic Settings on a resource when it is created.</span></span> <span data-ttu-id="3171c-105">Это позволяет tooautomatically начала потоковой передачи в журналы диагностики и метрики tooEvent концентраторов архивации их в учетной записи хранения или отправке tooLog Analytics, при создании ресурса.</span><span class="sxs-lookup"><span data-stu-id="3171c-105">This enables you tooautomatically start streaming your Diagnostic Logs and metrics tooEvent Hubs, archiving them in a Storage Account, or sending them tooLog Analytics when a resource is created.</span></span>

<span data-ttu-id="3171c-106">метод Hello для включения журналов диагностики с помощью шаблона диспетчера ресурсов, зависит от типа ресурса hello.</span><span class="sxs-lookup"><span data-stu-id="3171c-106">hello method for enabling Diagnostic Logs using a Resource Manager template depends on hello resource type.</span></span>

* <span data-ttu-id="3171c-107">**Невычислительные** ресурсы (например, группы безопасности сети, Logic Apps или служба автоматизации) используют [параметры диагностики, описанные в этой статье](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings).</span><span class="sxs-lookup"><span data-stu-id="3171c-107">**Non-Compute** resources (for example, Network Security Groups, Logic Apps, Automation) use [Diagnostic Settings described in this article](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings).</span></span>
* <span data-ttu-id="3171c-108">**Вычислений** (WAD/LAD на основе) ресурсы используют hello [WAD/LAD файл конфигурации, описанной в этой статье](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md).</span><span class="sxs-lookup"><span data-stu-id="3171c-108">**Compute** (WAD/LAD-based) resources use hello [WAD/LAD configuration file described in this article](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md).</span></span>

<span data-ttu-id="3171c-109">В этой статье описывается как tooconfigure диагностики с помощью любого метода.</span><span class="sxs-lookup"><span data-stu-id="3171c-109">In this article we describe how tooconfigure diagnostics using either method.</span></span>

<span data-ttu-id="3171c-110">Ниже приведены основные шаги Hello.</span><span class="sxs-lookup"><span data-stu-id="3171c-110">hello basic steps are as follows:</span></span>

1. <span data-ttu-id="3171c-111">Создание шаблона в формате JSON, описывающий, как toocreate hello ресурсов и включить диагностику.</span><span class="sxs-lookup"><span data-stu-id="3171c-111">Create a template as a JSON file that describes how toocreate hello resource and enable diagnostics.</span></span>
2. <span data-ttu-id="3171c-112">[Развертывание с помощью любой метод развертывания шаблона hello](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="3171c-112">[Deploy hello template using any deployment method](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

<span data-ttu-id="3171c-113">Ниже мы предоставляем пример hello шаблона JSON-файла необходимо toogenerate для Невычислительными и вычислительные ресурсы.</span><span class="sxs-lookup"><span data-stu-id="3171c-113">Below we give an example of hello template JSON file you need toogenerate for non-Compute and Compute resources.</span></span>

## <a name="non-compute-resource-template"></a><span data-ttu-id="3171c-114">Шаблон для невычислительных ресурсов</span><span class="sxs-lookup"><span data-stu-id="3171c-114">Non-Compute resource template</span></span>
<span data-ttu-id="3171c-115">Для не вычислительных ресурсов вам потребуется toodo две вещи:</span><span class="sxs-lookup"><span data-stu-id="3171c-115">For non-Compute resources, you will need toodo two things:</span></span>

1. <span data-ttu-id="3171c-116">Добавление BLOB-объект параметров toohello параметры для имени учетной записи хранения hello, ИД правила service bus и/или идентификатор рабочей области аналитики журналов OMS (Включение архивации журналы диагностики в учетную запись хранилища, потоковую передачу журналов tooEvent концентраторы или отправляя tooLog журналы аналитики).</span><span class="sxs-lookup"><span data-stu-id="3171c-116">Add parameters toohello parameters blob for hello storage account name, service bus rule ID, and/or OMS Log Analytics workspace ID (enabling archival of Diagnostic Logs in a storage account, streaming of logs tooEvent Hubs, and/or sending logs tooLog Analytics).</span></span>
   
    ```json
    "storageAccountName": {
      "type": "string",
      "metadata": {
        "description": "Name of hello Storage Account in which Diagnostic Logs should be saved."
      }
    },
    "serviceBusRuleId": {
      "type": "string",
      "metadata": {
        "description": "Service Bus Rule Id for hello Service Bus Namespace in which hello Event Hub should be created or streamed to."
      }
    },
    "workspaceId":{
      "type": "string",
      "metadata": {
        "description": "Log Analytics workspace ID for hello Log Analytics workspace toowhich logs will be sent."
      }
    }
    ```
2. <span data-ttu-id="3171c-117">В массиве ресурсы hello hello ресурса, для которого требуется tooenable журналы диагностики, добавьте ресурс типа `[resource namespace]/providers/diagnosticSettings`.</span><span class="sxs-lookup"><span data-stu-id="3171c-117">In hello resources array of hello resource for which you want tooenable Diagnostic Logs, add a resource of type `[resource namespace]/providers/diagnosticSettings`.</span></span>
   
    ```json
    "resources": [
      {
        "type": "providers/diagnosticSettings",
        "name": "Microsoft.Insights/service",
        "dependsOn": [
          "[/*resource Id for which Diagnostic Logs will be enabled>*/]"
        ],
        "apiVersion": "2015-07-01",
        "properties": {
          "storageAccountId": "[resourceId('Microsoft.Storage/storageAccounts', parameters('storageAccountName'))]",
          "serviceBusRuleId": "[parameters('serviceBusRuleId')]",
          "workspaceId": "[parameters('workspaceId')]",
          "logs": [ 
            {
              "category": "/* log category name */",
              "enabled": true,
              "retentionPolicy": {
                "days": 0,
                "enabled": false
              }
            }
          ],
          "metrics": [
            {
              "timeGrain": "PT1M",
              "enabled": true,
              "retentionPolicy": {
                "enabled": false,
                "days": 0
              }
            }
          ]
        }
      }
    ]
    ```

<span data-ttu-id="3171c-118">Hello свойства большого двоичного объекта для hello параметра диагностики следует [hello формата, описанные в этой статье](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span><span class="sxs-lookup"><span data-stu-id="3171c-118">hello properties blob for hello Diagnostic Setting follows [hello format described in this article](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span></span> <span data-ttu-id="3171c-119">Добавление hello `metrics` свойство включения tooalso отправки ресурса метрики toothese же выходные данные, при условии, что [метрик мониторинга Azure поддерживает ресурс hello](monitoring-supported-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="3171c-119">Adding hello `metrics` property will enable you tooalso send resource metrics toothese same outputs, provided that [hello resource supports Azure Monitor metrics](monitoring-supported-metrics.md).</span></span>

<span data-ttu-id="3171c-120">Ниже приведен полный пример, создает приложение логики и Включение потоковой передачи tooEvent концентраторов и хранилища в учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="3171c-120">Here is a full example that creates a Logic App and turns on streaming tooEvent Hubs and storage in a storage account.</span></span>

```json

{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "logicAppName": {
      "type": "string",
      "metadata": {
        "description": "Name of hello Logic App that will be created."
      }
    },
    "testUri": {
      "type": "string",
      "defaultValue": "http://azure.microsoft.com/en-us/status/feed/"
    },
    "storageAccountName": {
      "type": "string",
      "metadata": {
        "description": "Name of hello Storage Account in which Diagnostic Logs should be saved."
      }
    },
    "serviceBusRuleId": {
      "type": "string",
      "metadata": {
        "description": "Service Bus Rule Id for hello Service Bus Namespace in which hello Event Hub should be created or streamed to."
      }
    },
    "workspaceId": {
      "type": "string",
      "metadata": {
        "description": "Log Analytics workspace ID for hello Log Analytics workspace toowhich logs will be sent."
      }
    }
  },
  "variables": {},
  "resources": [
    {
      "type": "Microsoft.Logic/workflows",
      "name": "[parameters('logicAppName')]",
      "apiVersion": "2016-06-01",
      "location": "[resourceGroup().location]",
      "properties": {
        "definition": {
          "$schema": "http://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
          "contentVersion": "1.0.0.0",
          "parameters": {
            "testURI": {
              "type": "string",
              "defaultValue": "[parameters('testUri')]"
            }
          },
          "triggers": {
            "recurrence": {
              "type": "recurrence",
              "recurrence": {
                "frequency": "Hour",
                "interval": 1
              }
            }
          },
          "actions": {
            "http": {
              "type": "Http",
              "inputs": {
                "method": "GET",
                "uri": "@parameters('testUri')"
              },
              "runAfter": {}
            }
          },
          "outputs": {}
        },
        "parameters": {}
      },
      "resources": [
        {
          "type": "providers/diagnosticSettings",
          "name": "Microsoft.Insights/service",
          "dependsOn": [
            "[resourceId('Microsoft.Logic/workflows', parameters('logicAppName'))]"
          ],
          "apiVersion": "2015-07-01",
          "properties": {
            "storageAccountId": "[resourceId('Microsoft.Storage/storageAccounts', parameters('storageAccountName'))]",
            "serviceBusRuleId": "[parameters('serviceBusRuleId')]",
            "workspaceId": "[parameters('workspaceId')]",
            "logs": [
              {
                "category": "WorkflowRuntime",
                "enabled": true,
                "retentionPolicy": {
                  "days": 0,
                  "enabled": false
                }
              }
            ],
            "metrics": [
              {
                "timeGrain": "PT1M",
                "enabled": true,
                "retentionPolicy": {
                  "enabled": false,
                  "days": 0
                }
              }
            ]
          }
        }
      ],
      "dependsOn": []
    }
  ]
}

```

## <a name="compute-resource-template"></a><span data-ttu-id="3171c-121">Шаблон для вычислительных ресурсов</span><span class="sxs-lookup"><span data-stu-id="3171c-121">Compute resource template</span></span>
<span data-ttu-id="3171c-122">Диагностика tooenable на вычислительных ресурсов, например виртуальной машины или кластера Service Fabric нужно:</span><span class="sxs-lookup"><span data-stu-id="3171c-122">tooenable diagnostics on a Compute resource, for example a Virtual Machine or Service Fabric cluster, you need to:</span></span>

1. <span data-ttu-id="3171c-123">Добавьте определения ресурсов виртуальной Машины toohello расширения hello диагностики Azure.</span><span class="sxs-lookup"><span data-stu-id="3171c-123">Add hello Azure Diagnostics extension toohello VM resource definition.</span></span>
2. <span data-ttu-id="3171c-124">Укажите в качестве параметра учетную запись хранения и (или) концентратор событий.</span><span class="sxs-lookup"><span data-stu-id="3171c-124">Specify a storage account and/or event hub as a parameter.</span></span>
3. <span data-ttu-id="3171c-125">Добавьте hello содержимое файла WADCfg XML в свойстве XMLCfg hello, правильно экранирование все символы XML.</span><span class="sxs-lookup"><span data-stu-id="3171c-125">Add hello contents of your WADCfg XML file into hello XMLCfg property, escaping all XML characters properly.</span></span>

> [!WARNING]
> <span data-ttu-id="3171c-126">Этот последний шаг может быть непростой задачей tooget справа.</span><span class="sxs-lookup"><span data-stu-id="3171c-126">This last step can be tricky tooget right.</span></span> <span data-ttu-id="3171c-127">[См. в статье](../virtual-machines/windows/extensions-diagnostics-template.md#diagnostics-configuration-variables) пример hello, разбиений схема конфигурации системы диагностики в переменные, находящиеся в escape-последовательность и правильный формат.</span><span class="sxs-lookup"><span data-stu-id="3171c-127">[See this article](../virtual-machines/windows/extensions-diagnostics-template.md#diagnostics-configuration-variables) for an example that splits hello Diagnostics Configuration Schema into variables that are escaped and formatted correctly.</span></span>
> 
> 

<span data-ttu-id="3171c-128">Hello всего процесса, включая примеры, описанное [в настоящем документе](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3171c-128">hello entire process, including samples, is described [in this document](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3171c-129">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3171c-129">Next Steps</span></span>
* [<span data-ttu-id="3171c-130">Дополнительные сведения о журналах диагностики Azure</span><span class="sxs-lookup"><span data-stu-id="3171c-130">Read more about Azure Diagnostic Logs</span></span>](monitoring-overview-of-diagnostic-logs.md)
* [<span data-ttu-id="3171c-131">Журналы диагностики Azure поток tooEvent концентраторы</span><span class="sxs-lookup"><span data-stu-id="3171c-131">Stream Azure Diagnostic Logs tooEvent Hubs</span></span>](monitoring-stream-diagnostic-logs-to-event-hubs.md)

