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
ms.date: 8/30/2017
ms.author: johnkem
ms.openlocfilehash: 2f764bc14e882f71957299b833d5bc1a6765622a
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/11/2017
---
# <a name="automatically-enable-diagnostic-settings-at-resource-creation-using-a-resource-manager-template"></a>Автоматическое включение параметров диагностики при создании ресурса из шаблона Resource Manager
В этой статье мы покажем, как применить [шаблон Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) для настройки параметров диагностики при создании ресурса. Это позволит автоматически запускать потоковую передачу журналов диагностики и метрик в концентраторы событий, архивировать их в учетной записи хранения ли отправлять в Log Analytics при создании ресурса.

Для разных типов ресурсов журналы диагностики включаются с помощью шаблона Resource Manager по-разному.

* **Невычислительные** ресурсы (например, группы безопасности сети, Logic Apps или служба автоматизации) используют [параметры диагностики, описанные в этой статье](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings).
* **Вычислительные** ресурсы (на основе WAD/LAD) используют [файл конфигурации WAD/LAD, описанный в этой статье](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md).

В этой статьей объясняется, как настроить диагностику с помощью каждого из этих методов.

Основные этапы:

1. Создайте шаблон в виде файла JSON, который описывает, как создать ресурс и включить диагностику.
2. [Разверните шаблон с помощью любого метода развертывания](../azure-resource-manager/resource-group-template-deploy.md).

Ниже приведены примеры файла JSON шаблона для создания вычислительных и невычислительных ресурсов.

## <a name="non-compute-resource-template"></a>Шаблон для невычислительных ресурсов
Для невычислительных ресурсов выполните два действия.

1. Добавьте в большой двоичный объект параметров параметры имени учетной записи хранения, идентификатора правила служебной шины и (или) идентификатор рабочей области OMS Log Analytics. Это позволит архивировать журналы диагностики в учетную запись хранения, передавать поток журналов в концентраторы событий и (или) отправлять журналы в Log Analytics.
   
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
        "description": "Resource ID of the Service Bus Rule for the Service Bus Namespace in which the Event Hub should be created or streamed to."
      }
    },
    "workspaceId":{
      "type": "string",
      "metadata": {
        "description": "Azure Resource ID of the Log Analytics workspace for the Log Analytics workspace to which logs will be sent."
      }
    }
    ```
2. Добавьте ресурс с типом `[resource namespace]/providers/diagnosticSettings`в массив ресурсов того ресурса, для которого нужно включить журналы диагностики.
   
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

Свойства большого двоичного объекта для параметров диагностики соответствуют [формату, который описан в этой статье](https://msdn.microsoft.com/library/azure/dn931931.aspx). Добавление свойства `metrics` позволит также передавать метрики ресурса в эти же выходные данные, если [этот ресурс поддерживает метрики Azure Monitor](monitoring-supported-metrics.md).

Ниже приведен полный пример, в котором создается приложение логики, а также включается потоковая передача в концентраторы событий и хранение в учетной записи хранения.

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

## <a name="compute-resource-template"></a>Шаблон для вычислительных ресурсов
Чтобы включить диагностику для вычислительных ресурсов, например виртуальной машины или Service Fabric, выполните эти действия.

1. Добавьте расширение системы диагностики Azure в определение ресурсов для виртуальной машины.
2. Укажите в качестве параметра учетную запись хранения и (или) концентратор событий.
3. Добавьте содержимое XML-файла WADCfg в свойство XMLCfg, правильно экранируя все XML-символы.

> [!WARNING]
> Этот этап может оказаться непростой задачей. [В этой статье](../virtual-machines/windows/extensions-diagnostics-template.md#diagnostics-configuration-variables) приводится пример разбиения схемы конфигурации диагностики на переменные, которые правильно экранируются и форматируются.
> 
> 

Весь процесса описан [в этом документе](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)с примерами.

## <a name="next-steps"></a>Дальнейшие действия
* [Дополнительные сведения о журналах диагностики Azure](monitoring-overview-of-diagnostic-logs.md)
* [Потоковая передача журналов диагностики Azure в концентраторы событий](monitoring-stream-diagnostic-logs-to-event-hubs.md)

