---
title: "Автоматическое включение параметров диагностики с помощью шаблона Resource Manager | Документация Майкрософт"
description: "Узнайте, как использовать шаблон Resource Manager для создания параметров диагностики, которые позволят передавать журналы диагностики в концентраторы событий или сохранять их в учетной записи хранения."
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
ms.openlocfilehash: dde2435e976bbd14ca35cccc714ea21dcc5817b7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="automatically-enable-diagnostic-settings-at-resource-creation-using-a-resource-manager-template"></a><span data-ttu-id="03280-103">Автоматическое включение параметров диагностики при создании ресурса из шаблона Resource Manager</span><span class="sxs-lookup"><span data-stu-id="03280-103">Automatically enable Diagnostic Settings at resource creation using a Resource Manager template</span></span>
<span data-ttu-id="03280-104">В этой статье мы покажем, как применить [шаблон Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) для настройки параметров диагностики при создании ресурса.</span><span class="sxs-lookup"><span data-stu-id="03280-104">In this article we show how you can use an [Azure Resource Manager template](../azure-resource-manager/resource-group-authoring-templates.md) to configure Diagnostic Settings on a resource when it is created.</span></span> <span data-ttu-id="03280-105">Это позволит автоматически запускать потоковую передачу журналов диагностики и метрик в концентраторы событий, архивировать их в учетной записи хранения ли отправлять в Log Analytics при создании ресурса.</span><span class="sxs-lookup"><span data-stu-id="03280-105">This enables you to automatically start streaming your Diagnostic Logs and metrics to Event Hubs, archiving them in a Storage Account, or sending them to Log Analytics when a resource is created.</span></span>

<span data-ttu-id="03280-106">Для разных типов ресурсов журналы диагностики включаются с помощью шаблона Resource Manager по-разному.</span><span class="sxs-lookup"><span data-stu-id="03280-106">The method for enabling Diagnostic Logs using a Resource Manager template depends on the resource type.</span></span>

* <span data-ttu-id="03280-107">**Невычислительные** ресурсы (например, группы безопасности сети, Logic Apps или служба автоматизации) используют [параметры диагностики, описанные в этой статье](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings).</span><span class="sxs-lookup"><span data-stu-id="03280-107">**Non-Compute** resources (for example, Network Security Groups, Logic Apps, Automation) use [Diagnostic Settings described in this article](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings).</span></span>
* <span data-ttu-id="03280-108">**Вычислительные** ресурсы (на основе WAD/LAD) используют [файл конфигурации WAD/LAD, описанный в этой статье](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md).</span><span class="sxs-lookup"><span data-stu-id="03280-108">**Compute** (WAD/LAD-based) resources use the [WAD/LAD configuration file described in this article](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md).</span></span>

<span data-ttu-id="03280-109">В этой статьей объясняется, как настроить диагностику с помощью каждого из этих методов.</span><span class="sxs-lookup"><span data-stu-id="03280-109">In this article we describe how to configure diagnostics using either method.</span></span>

<span data-ttu-id="03280-110">Основные этапы:</span><span class="sxs-lookup"><span data-stu-id="03280-110">The basic steps are as follows:</span></span>

1. <span data-ttu-id="03280-111">Создайте шаблон в виде файла JSON, который описывает, как создать ресурс и включить диагностику.</span><span class="sxs-lookup"><span data-stu-id="03280-111">Create a template as a JSON file that describes how to create the resource and enable diagnostics.</span></span>
2. <span data-ttu-id="03280-112">[Разверните шаблон с помощью любого метода развертывания](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="03280-112">[Deploy the template using any deployment method](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

<span data-ttu-id="03280-113">Ниже приведены примеры файла JSON шаблона для создания вычислительных и невычислительных ресурсов.</span><span class="sxs-lookup"><span data-stu-id="03280-113">Below we give an example of the template JSON file you need to generate for non-Compute and Compute resources.</span></span>

## <a name="non-compute-resource-template"></a><span data-ttu-id="03280-114">Шаблон для невычислительных ресурсов</span><span class="sxs-lookup"><span data-stu-id="03280-114">Non-Compute resource template</span></span>
<span data-ttu-id="03280-115">Для невычислительных ресурсов выполните два действия.</span><span class="sxs-lookup"><span data-stu-id="03280-115">For non-Compute resources, you will need to do two things:</span></span>

1. <span data-ttu-id="03280-116">Добавьте в большой двоичный объект параметров параметры имени учетной записи хранения, идентификатора правила служебной шины и (или) идентификатор рабочей области OMS Log Analytics. Это позволит архивировать журналы диагностики в учетную запись хранения, передавать поток журналов в концентраторы событий и (или) отправлять журналы в Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="03280-116">Add parameters to the parameters blob for the storage account name, service bus rule ID, and/or OMS Log Analytics workspace ID (enabling archival of Diagnostic Logs in a storage account, streaming of logs to Event Hubs, and/or sending logs to Log Analytics).</span></span>
   
    ```json
    "storageAccountName": {
      "type": "string",
      "metadata": {
        "description": "Name of the Storage Account in which Diagnostic Logs should be saved."
      }
    },
    "serviceBusRuleId": {
      "type": "string",
      "metadata": {
        "description": "Service Bus Rule Id for the Service Bus Namespace in which the Event Hub should be created or streamed to."
      }
    },
    "workspaceId":{
      "type": "string",
      "metadata": {
        "description": "Log Analytics workspace ID for the Log Analytics workspace to which logs will be sent."
      }
    }
    ```
2. <span data-ttu-id="03280-117">Добавьте ресурс с типом `[resource namespace]/providers/diagnosticSettings`в массив ресурсов того ресурса, для которого нужно включить журналы диагностики.</span><span class="sxs-lookup"><span data-stu-id="03280-117">In the resources array of the resource for which you want to enable Diagnostic Logs, add a resource of type `[resource namespace]/providers/diagnosticSettings`.</span></span>
   
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

<span data-ttu-id="03280-118">Свойства большого двоичного объекта для параметров диагностики соответствуют [формату, который описан в этой статье](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span><span class="sxs-lookup"><span data-stu-id="03280-118">The properties blob for the Diagnostic Setting follows [the format described in this article](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span></span> <span data-ttu-id="03280-119">Добавление свойства `metrics` позволит также передавать метрики ресурса в эти же выходные данные, если [этот ресурс поддерживает метрики Azure Monitor](monitoring-supported-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="03280-119">Adding the `metrics` property will enable you to also send resource metrics to these same outputs, provided that [the resource supports Azure Monitor metrics](monitoring-supported-metrics.md).</span></span>

<span data-ttu-id="03280-120">Ниже приведен полный пример, в котором создается приложение логики, а также включается потоковая передача в концентраторы событий и хранение в учетной записи хранения.</span><span class="sxs-lookup"><span data-stu-id="03280-120">Here is a full example that creates a Logic App and turns on streaming to Event Hubs and storage in a storage account.</span></span>

```json

{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "logicAppName": {
      "type": "string",
      "metadata": {
        "description": "Name of the Logic App that will be created."
      }
    },
    "testUri": {
      "type": "string",
      "defaultValue": "http://azure.microsoft.com/en-us/status/feed/"
    },
    "storageAccountName": {
      "type": "string",
      "metadata": {
        "description": "Name of the Storage Account in which Diagnostic Logs should be saved."
      }
    },
    "serviceBusRuleId": {
      "type": "string",
      "metadata": {
        "description": "Service Bus Rule Id for the Service Bus Namespace in which the Event Hub should be created or streamed to."
      }
    },
    "workspaceId": {
      "type": "string",
      "metadata": {
        "description": "Log Analytics workspace ID for the Log Analytics workspace to which logs will be sent."
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

## <a name="compute-resource-template"></a><span data-ttu-id="03280-121">Шаблон для вычислительных ресурсов</span><span class="sxs-lookup"><span data-stu-id="03280-121">Compute resource template</span></span>
<span data-ttu-id="03280-122">Чтобы включить диагностику для вычислительных ресурсов, например виртуальной машины или Service Fabric, выполните эти действия.</span><span class="sxs-lookup"><span data-stu-id="03280-122">To enable diagnostics on a Compute resource, for example a Virtual Machine or Service Fabric cluster, you need to:</span></span>

1. <span data-ttu-id="03280-123">Добавьте расширение системы диагностики Azure в определение ресурсов для виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="03280-123">Add the Azure Diagnostics extension to the VM resource definition.</span></span>
2. <span data-ttu-id="03280-124">Укажите в качестве параметра учетную запись хранения и (или) концентратор событий.</span><span class="sxs-lookup"><span data-stu-id="03280-124">Specify a storage account and/or event hub as a parameter.</span></span>
3. <span data-ttu-id="03280-125">Добавьте содержимое XML-файла WADCfg в свойство XMLCfg, правильно экранируя все XML-символы.</span><span class="sxs-lookup"><span data-stu-id="03280-125">Add the contents of your WADCfg XML file into the XMLCfg property, escaping all XML characters properly.</span></span>

> [!WARNING]
> <span data-ttu-id="03280-126">Этот этап может оказаться непростой задачей.</span><span class="sxs-lookup"><span data-stu-id="03280-126">This last step can be tricky to get right.</span></span> <span data-ttu-id="03280-127">[В этой статье](../virtual-machines/windows/extensions-diagnostics-template.md#diagnostics-configuration-variables) приводится пример разбиения схемы конфигурации диагностики на переменные, которые правильно экранируются и форматируются.</span><span class="sxs-lookup"><span data-stu-id="03280-127">[See this article](../virtual-machines/windows/extensions-diagnostics-template.md#diagnostics-configuration-variables) for an example that splits the Diagnostics Configuration Schema into variables that are escaped and formatted correctly.</span></span>
> 
> 

<span data-ttu-id="03280-128">Весь процесса описан [в этом документе](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)с примерами.</span><span class="sxs-lookup"><span data-stu-id="03280-128">The entire process, including samples, is described [in this document](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="03280-129">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="03280-129">Next Steps</span></span>
* [<span data-ttu-id="03280-130">Дополнительные сведения о журналах диагностики Azure</span><span class="sxs-lookup"><span data-stu-id="03280-130">Read more about Azure Diagnostic Logs</span></span>](monitoring-overview-of-diagnostic-logs.md)
* [<span data-ttu-id="03280-131">Потоковая передача журналов диагностики Azure в концентраторы событий</span><span class="sxs-lookup"><span data-stu-id="03280-131">Stream Azure Diagnostic Logs to Event Hubs</span></span>](monitoring-stream-diagnostic-logs-to-event-hubs.md)

