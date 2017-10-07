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
# <a name="automatically-enable-diagnostic-settings-at-resource-creation-using-a-resource-manager-template"></a>Автоматическое включение параметров диагностики при создании ресурса из шаблона Resource Manager
В этой статье показано, как можно использовать [шаблона Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md) tooconfigure параметров диагностики для ресурса при его создании. Это позволяет tooautomatically начала потоковой передачи в журналы диагностики и метрики tooEvent концентраторов архивации их в учетной записи хранения или отправке tooLog Analytics, при создании ресурса.

метод Hello для включения журналов диагностики с помощью шаблона диспетчера ресурсов, зависит от типа ресурса hello.

* **Невычислительные** ресурсы (например, группы безопасности сети, Logic Apps или служба автоматизации) используют [параметры диагностики, описанные в этой статье](monitoring-overview-of-diagnostic-logs.md#resource-diagnostic-settings).
* **Вычислений** (WAD/LAD на основе) ресурсы используют hello [WAD/LAD файл конфигурации, описанной в этой статье](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md).

В этой статье описывается как tooconfigure диагностики с помощью любого метода.

Ниже приведены основные шаги Hello.

1. Создание шаблона в формате JSON, описывающий, как toocreate hello ресурсов и включить диагностику.
2. [Развертывание с помощью любой метод развертывания шаблона hello](../azure-resource-manager/resource-group-template-deploy.md).

Ниже мы предоставляем пример hello шаблона JSON-файла необходимо toogenerate для Невычислительными и вычислительные ресурсы.

## <a name="non-compute-resource-template"></a>Шаблон для невычислительных ресурсов
Для не вычислительных ресурсов вам потребуется toodo две вещи:

1. Добавление BLOB-объект параметров toohello параметры для имени учетной записи хранения hello, ИД правила service bus и/или идентификатор рабочей области аналитики журналов OMS (Включение архивации журналы диагностики в учетную запись хранилища, потоковую передачу журналов tooEvent концентраторы или отправляя tooLog журналы аналитики).
   
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
2. В массиве ресурсы hello hello ресурса, для которого требуется tooenable журналы диагностики, добавьте ресурс типа `[resource namespace]/providers/diagnosticSettings`.
   
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

Hello свойства большого двоичного объекта для hello параметра диагностики следует [hello формата, описанные в этой статье](https://msdn.microsoft.com/library/azure/dn931931.aspx). Добавление hello `metrics` свойство включения tooalso отправки ресурса метрики toothese же выходные данные, при условии, что [метрик мониторинга Azure поддерживает ресурс hello](monitoring-supported-metrics.md).

Ниже приведен полный пример, создает приложение логики и Включение потоковой передачи tooEvent концентраторов и хранилища в учетной записи хранилища.

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

## <a name="compute-resource-template"></a>Шаблон для вычислительных ресурсов
Диагностика tooenable на вычислительных ресурсов, например виртуальной машины или кластера Service Fabric нужно:

1. Добавьте определения ресурсов виртуальной Машины toohello расширения hello диагностики Azure.
2. Укажите в качестве параметра учетную запись хранения и (или) концентратор событий.
3. Добавьте hello содержимое файла WADCfg XML в свойстве XMLCfg hello, правильно экранирование все символы XML.

> [!WARNING]
> Этот последний шаг может быть непростой задачей tooget справа. [См. в статье](../virtual-machines/windows/extensions-diagnostics-template.md#diagnostics-configuration-variables) пример hello, разбиений схема конфигурации системы диагностики в переменные, находящиеся в escape-последовательность и правильный формат.
> 
> 

Hello всего процесса, включая примеры, описанное [в настоящем документе](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="next-steps"></a>Дальнейшие действия
* [Дополнительные сведения о журналах диагностики Azure](monitoring-overview-of-diagnostic-logs.md)
* [Журналы диагностики Azure поток tooEvent концентраторы](monitoring-stream-diagnostic-logs-to-event-hubs.md)

