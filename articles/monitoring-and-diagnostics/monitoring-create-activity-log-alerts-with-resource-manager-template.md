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
# <a name="create-an-activity-log-alert-with-a-resource-manager-template"></a>Создание оповещения журнала действий с помощью шаблона Resource Manager
В этой статье показано, как toouse [шаблона Azure Resource Manager](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authoring-templates) tooconfigure предупреждения журнала действий. С помощью шаблонов можно легко настроить большое количество предупреждений, которые активируются по определенным условиям события журнала действий в рамках автоматического развертывания.

Основные этапы Hello

1. Создание шаблона в формате JSON, описывающий, как действие hello toocreate входа предупреждение.

2. Развертывание с помощью шаблона hello [любой метод развертывания](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).

## <a name="resource-manager-template-for-an-activity-log-alert"></a>Шаблон Resource Manager для оповещения журнала действий
toocreate оповещение журнал действий с помощью шаблона диспетчера ресурсов, создать ресурс типа hello `microsoft.insights/activityLogAlerts`. Затем следует заполнить все связанные свойства. Вот шаблон, создающий оповещение журнала действий.

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

Примеры шаблонов для оповещений журнала действий см. в [коллекции шаблонов для быстрого начала работы с Azure](https://azure.microsoft.com/resources/templates/?resourceType=Microsoft.Insights).

## <a name="next-steps"></a>Дальнейшие действия
- Узнайте больше об [оповещениях](monitoring-overview-alerts.md).
- Узнайте, как tooadd [группы действий с помощью шаблона диспетчера ресурсов](monitoring-create-action-group-with-resource-manager-template.md).
- Узнайте, каким образом слишком[создания предупреждения toomonitor журнала действий всех операций автомасштабирования обработчика по подписке](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert).
- Узнайте, каким образом слишком[создания предупреждения toomonitor журнала действий все операции масштабирования в/scale out Сбой автоматического масштабирования для одной подписки](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).
