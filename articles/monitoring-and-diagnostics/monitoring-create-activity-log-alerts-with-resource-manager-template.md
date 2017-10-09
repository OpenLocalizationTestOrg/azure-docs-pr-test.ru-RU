---
title: "оповещение журнала активности с помощью шаблона диспетчера ресурсов aaaCreate | Документы Microsoft"
description: "Получение уведомлений при создании ресурсов в Azure."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: ancav
ms.openlocfilehash: 0fb8aa037b9dce54ce35498622770955f2341bc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-activity-log-alert-with-a-resource-manager-template"></a><span data-ttu-id="6a8c4-103">Создание оповещения журнала действий с помощью шаблона Resource Manager</span><span class="sxs-lookup"><span data-stu-id="6a8c4-103">Create an activity log alert with a Resource Manager template</span></span>
<span data-ttu-id="6a8c4-104">В этой статье показано, как toouse [шаблона Azure Resource Manager](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authoring-templates) tooconfigure предупреждения журнала действий.</span><span class="sxs-lookup"><span data-stu-id="6a8c4-104">This article shows you how toouse an [Azure Resource Manager template](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authoring-templates) tooconfigure activity log alerts.</span></span> <span data-ttu-id="6a8c4-105">С помощью шаблонов можно легко настроить большое количество предупреждений, которые активируются по определенным условиям события журнала действий в рамках автоматического развертывания.</span><span class="sxs-lookup"><span data-stu-id="6a8c4-105">By using templates, you can easily set up many alerts that activate based on specific activity log event conditions as part of your automated deployment process.</span></span>

<span data-ttu-id="6a8c4-106">Основные этапы Hello</span><span class="sxs-lookup"><span data-stu-id="6a8c4-106">hello basic steps are:</span></span>

1. <span data-ttu-id="6a8c4-107">Создание шаблона в формате JSON, описывающий, как действие hello toocreate входа предупреждение.</span><span class="sxs-lookup"><span data-stu-id="6a8c4-107">Create a template as a JSON file that describes how toocreate hello activity log alert.</span></span>

2. <span data-ttu-id="6a8c4-108">Развертывание с помощью шаблона hello [любой метод развертывания](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).</span><span class="sxs-lookup"><span data-stu-id="6a8c4-108">Deploy hello template by using [any deployment method](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).</span></span>

## <a name="resource-manager-template-for-an-activity-log-alert"></a><span data-ttu-id="6a8c4-109">Шаблон Resource Manager для оповещения журнала действий</span><span class="sxs-lookup"><span data-stu-id="6a8c4-109">Resource Manager template for an activity log alert</span></span>
<span data-ttu-id="6a8c4-110">toocreate оповещение журнал действий с помощью шаблона диспетчера ресурсов, создать ресурс типа hello `microsoft.insights/activityLogAlerts`.</span><span class="sxs-lookup"><span data-stu-id="6a8c4-110">toocreate an activity log alert by using a Resource Manager template, you create a resource of hello type `microsoft.insights/activityLogAlerts`.</span></span> <span data-ttu-id="6a8c4-111">Затем следует заполнить все связанные свойства.</span><span class="sxs-lookup"><span data-stu-id="6a8c4-111">Then you fill in all related properties.</span></span> <span data-ttu-id="6a8c4-112">Вот шаблон, создающий оповещение журнала действий.</span><span class="sxs-lookup"><span data-stu-id="6a8c4-112">Here's a template that creates an activity log alert.</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "activityLogAlertName": {
      "type": "string",
      "metadata": {
        "description": "Unique name (within hello Resource Group) for hello Activity log alert."
      }
    },
    "activityLogAlertEnabled": {
      "type": "bool",
      "defaultValue": true,
      "metadata": {
        "description": "Indicates whether or not hello alert is enabled."
      }
    },
    "actionGroupResourceId": {
      "type": "string",
      "metadata": {
        "description": "Resource Id for hello Action group."
      }
    }
  },
  "resources": [   
    {
      "type": "Microsoft.Insights/activityLogAlerts",
      "apiVersion": "2017-04-01",
      "name": "[parameters('activityLogAlertName')]",      
      "location": "Global",
      "properties": {
        "enabled": "[parameters('activityLogAlertEnabled')]",
        "scopes": [
            "[subscription().id]"
        ],        
        "condition": {
          "allOf": [
            {
              "field": "category",
              "equals": "Administrative"
            },
            {
              "field": "operationName",
              "equals": "Microsoft.Resources/deployments/write"
            },
            {
              "field": "resourceType",
              "equals": "Microsoft.Resources/deployments"
            }
          ] 
        },
        "actions": {
          "actionGroups": 
          [
            {
              "actionGroupId": "[parameters('actionGroupResourceId')]"
            }
          ]
        }
      }
    }
  ]
}
```

<span data-ttu-id="6a8c4-113">Примеры шаблонов для оповещений журнала действий см. в [коллекции шаблонов для быстрого начала работы с Azure](https://azure.microsoft.com/resources/templates/?resourceType=Microsoft.Insights).</span><span class="sxs-lookup"><span data-stu-id="6a8c4-113">Visit our [Azure Quickstart gallery](https://azure.microsoft.com/resources/templates/?resourceType=Microsoft.Insights) for some examples of activity log alert templates.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6a8c4-114">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="6a8c4-114">Next steps</span></span>
- <span data-ttu-id="6a8c4-115">Узнайте больше об [оповещениях](monitoring-overview-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="6a8c4-115">Learn more about [alerts](monitoring-overview-alerts.md).</span></span>
- <span data-ttu-id="6a8c4-116">Узнайте, как tooadd [группы действий с помощью шаблона диспетчера ресурсов](monitoring-create-action-group-with-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="6a8c4-116">Learn how tooadd [action groups by using a Resource Manager template](monitoring-create-action-group-with-resource-manager-template.md).</span></span>
- <span data-ttu-id="6a8c4-117">Узнайте, каким образом слишком[создания предупреждения toomonitor журнала действий всех операций автомасштабирования обработчика по подписке](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert).</span><span class="sxs-lookup"><span data-stu-id="6a8c4-117">Learn how too[create an activity log alert toomonitor all autoscale engine operations on your subscription](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert).</span></span>
- <span data-ttu-id="6a8c4-118">Узнайте, каким образом слишком[создания предупреждения toomonitor журнала действий все операции масштабирования в/scale out Сбой автоматического масштабирования для одной подписки](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).</span><span class="sxs-lookup"><span data-stu-id="6a8c4-118">Learn how too[create an activity log alert toomonitor all failed autoscale scale-in/scale-out operations on your subscription](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).</span></span>
