---
title: "Создание групп действий с помощью шаблонов Resource Manager | Документация Майкрософт"
description: "Узнайте, как создать группу действий с помощью шаблона Azure Resource Manager."
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
ms.date: 03/31/2017
ms.author: ancav
ms.openlocfilehash: 76bf353cac13f1c2169380f8dd3c1e163d4f3f41
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="create-an-action-group-with-a-resource-manager-template"></a><span data-ttu-id="d3311-103">Создание группы действий с помощью шаблона Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d3311-103">Create an action group with a Resource Manager template</span></span>
<span data-ttu-id="d3311-104">В этой статье показано, как можно использовать [шаблон Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authoring-templates) для настройки групп действий.</span><span class="sxs-lookup"><span data-stu-id="d3311-104">This article shows you how to use an [Azure Resource Manager template](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authoring-templates) to configure action groups.</span></span> <span data-ttu-id="d3311-105">С помощью шаблонов можно автоматически настроить группы действий, которые можно использовать повторно в определенных типах оповещений.</span><span class="sxs-lookup"><span data-stu-id="d3311-105">By using templates, you can automatically set up action groups that can be reused in certain types of alerts.</span></span> <span data-ttu-id="d3311-106">С помощью этих групп действий обеспечивается уведомление соответствующих участников при активации оповещения.</span><span class="sxs-lookup"><span data-stu-id="d3311-106">These action groups ensure that all the correct parties are notified when an alert is triggered.</span></span>

<span data-ttu-id="d3311-107">Основными шагами являются:</span><span class="sxs-lookup"><span data-stu-id="d3311-107">The basic steps are:</span></span>

1. <span data-ttu-id="d3311-108">Создайте шаблон в виде JSON-файла, который описывает создание группы действий.</span><span class="sxs-lookup"><span data-stu-id="d3311-108">Create a template as a JSON file that describes how to create the action group.</span></span>

2. <span data-ttu-id="d3311-109">Разверните шаблон, используя [любой метод развертывания](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).</span><span class="sxs-lookup"><span data-stu-id="d3311-109">Deploy the template by using [any deployment method](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).</span></span>

<span data-ttu-id="d3311-110">Ниже описано, как создать шаблон Resource Manager для группы действий, в котором определения действий жестко запрограммированы,</span><span class="sxs-lookup"><span data-stu-id="d3311-110">First, we describe how to create a Resource Manager template for an action group where the action definitions are hard-coded in the template.</span></span> <span data-ttu-id="d3311-111">а также представлены способы создания шаблона, принимающего данные конфигурации веб-перехватчика в качестве входных параметров при развертывании шаблона.</span><span class="sxs-lookup"><span data-stu-id="d3311-111">Second, we describe how to create a template that takes the webhook configuration information as input parameters when the template is deployed.</span></span>

## <a name="resource-manager-templates-for-an-action-group"></a><span data-ttu-id="d3311-112">Шаблоны Resource Manager для группы действий</span><span class="sxs-lookup"><span data-stu-id="d3311-112">Resource Manager templates for an action group</span></span>

<span data-ttu-id="d3311-113">Чтобы создать группу действий с помощью шаблона Resource Manager, создайте ресурс типа `Microsoft.Insights/actionGroups`.</span><span class="sxs-lookup"><span data-stu-id="d3311-113">To create an action group by using a Resource Manager template, you create a resource of the type `Microsoft.Insights/actionGroups`.</span></span> <span data-ttu-id="d3311-114">Затем следует заполнить все связанные свойства.</span><span class="sxs-lookup"><span data-stu-id="d3311-114">Then you fill in all related properties.</span></span> <span data-ttu-id="d3311-115">Ниже представлено два примера шаблонов для создания группы действий.</span><span class="sxs-lookup"><span data-stu-id="d3311-115">Here are two sample templates that create an action group.</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "actionGroupName": {
      "type": "string",
      "metadata": {
        "description": "Unique name (within the Resource Group) for the Action group."
      }
    },
    "actionGroupShortName": {
      "type": "string",
      "metadata": {
        "description": "Short name (maximum 12 characters) for the Action group."
      }
    }
  },
  "resources": [
    {
      "type": "Microsoft.Insights/actionGroups",
      "apiVersion": "2017-04-01",
      "name": "[parameters('actionGroupName')]",
      "location": "Global",
      "properties": {
        "groupShortName": "[parameters('actionGroupShortName')]",
        "enabled": true,
        "smsReceivers": [
          {
            "name": "contosoSMS",
            "countryCode": "1",
            "phoneNumber": "5555551212"
          },
          {
            "name": "contosoSMS2",
            "countryCode": "1",
            "phoneNumber": "5555552121"
          }
        ],
        "emailReceivers": [
          {
            "name": "contosoEmail",
            "emailAddress": "devops@contoso.com"
          },
          {
            "name": "contosoEmail2",
            "emailAddress": "devops2@contoso.com"
          }
        ],
        "webhookReceivers": [
          {
            "name": "contosoHook",
            "serviceUri": "http://requestb.in/1bq62iu1"
          },
          {
            "name": "contosoHook2",
            "serviceUri": "http://requestb.in/1bq62iu2"
          }
        ]
      }
    }
  ],
  "outputs":{
      "actionGroupId":{
          "type":"string",
          "value":"[resourceId('Microsoft.Insights/actionGroups',parameters('actionGroupName'))]"
      }
  }
}
```

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "actionGroupName": {
      "type": "string",
      "metadata": {
        "description": "Unique name (within the Resource Group) for the Action group."
      }
    },
    "actionGroupShortName": {
      "type": "string",
      "metadata": {
        "description": "Short name (maximum 12 characters) for the Action group."
      }
    },
    "webhookReceiverName": {
      "type": "string",
      "metadata": {
        "description": "Webhook receiver service URI."
      }
    },    
    "webhookServiceUri": {
      "type": "string",
      "metadata": {
        "description": "Webhook receiver service URI."
      }
    }    
  },
  "resources": [
    {
      "type": "Microsoft.Insights/actionGroups",
      "apiVersion": "2017-04-01",
      "name": "[parameters('actionGroupName')]",
      "location": "Global",
      "properties": {
        "groupShortName": "[parameters('actionGroupShortName')]",
        "enabled": true,
        "smsReceivers": [
        ],
        "emailReceivers": [
        ],
        "webhookReceivers": [
          {
            "name": "[parameters('webhookReceiverName')]",
            "serviceUri": "[parameters('webhookServiceUri')]"
          }
        ]
      }
    }
  ],
  "outputs":{
      "actionGroupResourceId":{
          "type":"string",
          "value":"[resourceId('Microsoft.Insights/actionGroups',parameters('actionGroupName'))]"
      }
  }
}
```


## <a name="next-steps"></a><span data-ttu-id="d3311-116">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d3311-116">Next steps</span></span>
* <span data-ttu-id="d3311-117">Дополнительные сведения о группах действий см. в статье [Создание групп действий и управление ими на портале Azure](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="d3311-117">Learn more about [action groups](monitoring-action-groups.md).</span></span>
* <span data-ttu-id="d3311-118">Узнайте больше об [оповещениях](monitoring-overview-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="d3311-118">Learn more about [alerts](monitoring-overview-alerts.md).</span></span>
* <span data-ttu-id="d3311-119">Узнайте, как добавить [оповещения с помощью шаблона Resource Manager](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="d3311-119">Learn how to add [alerts by using a Resource Manager template](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span></span>
