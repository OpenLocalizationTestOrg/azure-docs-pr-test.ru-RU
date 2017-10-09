---
title: "группы действий aaaCreate с помощью шаблонов диспетчера ресурсов | Документы Microsoft"
description: "Узнайте, как toocreate действия группы с помощью шаблона диспетчера ресурсов Azure."
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
ms.openlocfilehash: 9902b33cad99bd99b3deda0cf6f4ff12278c89c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-action-group-with-a-resource-manager-template"></a><span data-ttu-id="7b423-103">Создание группы действий с помощью шаблона Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7b423-103">Create an action group with a Resource Manager template</span></span>
<span data-ttu-id="7b423-104">В этой статье показано, как toouse [шаблона Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authoring-templates) tooconfigure группы действий.</span><span class="sxs-lookup"><span data-stu-id="7b423-104">This article shows you how toouse an [Azure Resource Manager template](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authoring-templates) tooconfigure action groups.</span></span> <span data-ttu-id="7b423-105">С помощью шаблонов можно автоматически настроить группы действий, которые можно использовать повторно в определенных типах оповещений.</span><span class="sxs-lookup"><span data-stu-id="7b423-105">By using templates, you can automatically set up action groups that can be reused in certain types of alerts.</span></span> <span data-ttu-id="7b423-106">Эти группы действий убедитесь, что все hello правильных сторонам получать уведомления при активации оповещения.</span><span class="sxs-lookup"><span data-stu-id="7b423-106">These action groups ensure that all hello correct parties are notified when an alert is triggered.</span></span>

<span data-ttu-id="7b423-107">Основные этапы Hello</span><span class="sxs-lookup"><span data-stu-id="7b423-107">hello basic steps are:</span></span>

1. <span data-ttu-id="7b423-108">Создание шаблона в формате JSON, описывающий, как toocreate hello группы действий.</span><span class="sxs-lookup"><span data-stu-id="7b423-108">Create a template as a JSON file that describes how toocreate hello action group.</span></span>

2. <span data-ttu-id="7b423-109">Развертывание с помощью шаблона hello [любой метод развертывания](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).</span><span class="sxs-lookup"><span data-stu-id="7b423-109">Deploy hello template by using [any deployment method](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).</span></span>

<span data-ttu-id="7b423-110">Во-первых, мы опишем как toocreate шаблона диспетчера ресурсов для действия группы, где определения действие hello жестко запрограммированы в шаблоне hello.</span><span class="sxs-lookup"><span data-stu-id="7b423-110">First, we describe how toocreate a Resource Manager template for an action group where hello action definitions are hard-coded in hello template.</span></span> <span data-ttu-id="7b423-111">Во-вторых чтобы описать как toocreate шаблон, который принимает данные конфигурации веб-перехватчика hello как входные параметры при развертывании шаблона hello.</span><span class="sxs-lookup"><span data-stu-id="7b423-111">Second, we describe how toocreate a template that takes hello webhook configuration information as input parameters when hello template is deployed.</span></span>

## <a name="resource-manager-templates-for-an-action-group"></a><span data-ttu-id="7b423-112">Шаблоны Resource Manager для группы действий</span><span class="sxs-lookup"><span data-stu-id="7b423-112">Resource Manager templates for an action group</span></span>

<span data-ttu-id="7b423-113">toocreate группу действий с помощью шаблона диспетчера ресурсов, создать ресурс типа hello `Microsoft.Insights/actionGroups`.</span><span class="sxs-lookup"><span data-stu-id="7b423-113">toocreate an action group by using a Resource Manager template, you create a resource of hello type `Microsoft.Insights/actionGroups`.</span></span> <span data-ttu-id="7b423-114">Затем следует заполнить все связанные свойства.</span><span class="sxs-lookup"><span data-stu-id="7b423-114">Then you fill in all related properties.</span></span> <span data-ttu-id="7b423-115">Ниже представлено два примера шаблонов для создания группы действий.</span><span class="sxs-lookup"><span data-stu-id="7b423-115">Here are two sample templates that create an action group.</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "actionGroupName": {
      "type": "string",
      "metadata": {
        "description": "Unique name (within hello Resource Group) for hello Action group."
      }
    },
    "actionGroupShortName": {
      "type": "string",
      "metadata": {
        "description": "Short name (maximum 12 characters) for hello Action group."
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
        "description": "Unique name (within hello Resource Group) for hello Action group."
      }
    },
    "actionGroupShortName": {
      "type": "string",
      "metadata": {
        "description": "Short name (maximum 12 characters) for hello Action group."
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


## <a name="next-steps"></a><span data-ttu-id="7b423-116">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7b423-116">Next steps</span></span>
* <span data-ttu-id="7b423-117">Дополнительные сведения о группах действий см. в статье [Создание групп действий и управление ими на портале Azure](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="7b423-117">Learn more about [action groups](monitoring-action-groups.md).</span></span>
* <span data-ttu-id="7b423-118">Узнайте больше об [оповещениях](monitoring-overview-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="7b423-118">Learn more about [alerts](monitoring-overview-alerts.md).</span></span>
* <span data-ttu-id="7b423-119">Узнайте, как tooadd [оповещений с помощью шаблона диспетчера ресурсов](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="7b423-119">Learn how tooadd [alerts by using a Resource Manager template](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span></span>
