---
title: "Сохраненные поиски и оповещения в решениях OMS | Документация Майкрософт"
description: "Как правило, решения в OMS включают в себя возможность сохранения поисков в Log Analytics для анализа данных, собранных решением.  Они могут также определить оповещения для уведомления пользователя или автоматического выполнения действия в ответ на критическую ошибку.  В этой статье описывается, как определить сохраненные поиски и оповещения Log Analytics в шаблоне ARM, чтобы их можно было добавлять в решения для управления."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 21c42a747a08c5386c65d10190baf0054a7adef8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="adding-log-analytics-saved-searches-and-alerts-to-oms-management-solution-preview"></a>Добавление сохраненных поисковых запросов и оповещений Log Analytics в решении по управлению OMS (предварительная версия)

> [!NOTE]
> Это предварительная документация для создания решений для управления в консоли OMS, которая доступна в данный момент в режиме предварительной версии. Любые схемы, приведенные ниже, могут измениться.   


Как правило, [решения для управления в OMS](operations-management-suite-solutions.md) включают в себя возможность [сохранения поисков](../log-analytics/log-analytics-log-searches.md) в Log Analytics для анализа данных, собранных решением.  Они могут также определять [оповещения](../log-analytics/log-analytics-alerts.md) для уведомления пользователя или автоматического выполнения действия в ответ на критическую ошибку.  В этой статье описывается, как определить сохраненные поиски и оповещения Log Analytics в [шаблоне Resource Manager](../resource-manager-template-walkthrough.md), чтобы их можно было добавлять в [решения для управления](operations-management-suite-solutions-creating.md).

> [!NOTE]
> В примерах здесь используются обязательные или общие параметры и переменные для решений по управлению, описанные в статье [Создание решений для управления в Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md).  

## <a name="prerequisites"></a>Предварительные требования
В этой статье предполагается, что вы уже знаете, как [создать решение для управления](operations-management-suite-solutions-creating.md), структуру [шаблона ARM](../resource-group-authoring-templates.md) и файл решения.


## <a name="log-analytics-workspace"></a>Рабочая область Log Analytics
Все ресурсы в Log Analytics размещаются в [рабочей области](../log-analytics/log-analytics-manage-access.md).  Как описано в разделе [Рабочая область OMS и учетная запись службы автоматизации](operations-management-suite-solutions.md#oms-workspace-and-automation-account), рабочая область не включена в решение для управления и должна быть создана до его установки.  Если она недоступна, произойдет сбой установки решения.

Имя рабочей области указывается в имени каждого ресурса Log Analytics.  Для этого в решении используется параметр **workspace**, как показано в следующем примере ресурса savedsearch.

    "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearchId'))]"


## <a name="saved-searches"></a>Сохраненные поиски
Добавьте в решение функцию [сохраненных поисков](../log-analytics/log-analytics-log-searches.md), чтобы пользователи могли запрашивать данные, собранные решением.  Сохраненные поиски будут отображены в разделе **Избранное** на портале OMS и в разделе **Сохраненные условия поиска** на портале Azure.  Сохраненный поиск также является обязательным для каждого оповещения.   

Ресурсы [сохраненных поисков Log Analytics](../log-analytics/log-analytics-log-searches.md) имеют тип `Microsoft.OperationalInsights/workspaces/savedSearches`. Их структура приведена ниже.  Далее представлены общие переменные и параметры, чтобы этот фрагмент кода можно было скопировать и вставить в файл решения и изменить имена параметров. 

    {
        "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name)]",
        "type": "Microsoft.OperationalInsights/workspaces/savedSearches",
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "dependsOn": [
        ],
        "tags": { },
        "properties": {
            "etag": "*",
            "query": "[variables('SavedSearch').Query]",
            "displayName": "[variables('SavedSearch').DisplayName]",
            "category": "[variables('SavedSearch').Category]"
        }
    }



Каждое из свойств сохраненного поиска описано в следующей таблице. 

| Свойство | Описание |
|:--- |:--- |
| category | Категория для сохраненного поиска.  Сохраненные поиски в одном решении часто будут принадлежать одной категории, поэтому они группируются в консоли. |
| displayname | Имя, отображаемое для сохраненного поиска на портале. |
| запрос | Запрос для выполнения. |

> [!NOTE]
> В запросе необходимо использовать escape-символы, если он содержит знаки, которые можно интерпретировать как JSON.  Например, запрос **Type:AzureActivity OperationName:"Microsoft.Compute/virtualMachines/write"** в файл решения должен быть записан как **Type:AzureActivity OperationName:\"Microsoft.Compute/virtualMachines/write\"**.

## <a name="alerts"></a>Оповещения
[Оповещения Log Analytics](../log-analytics/log-analytics-alerts.md) создаются правилами генерации оповещений, которые выполняют сохраненный через равные промежутки времени.  Если результаты запроса соответствуют указанным условиям, то создается запись оповещения и выполняются одно или несколько действий.  

Правила генерации оповещений в решении для управления состоят из трех различных ресурсов.

- **Сохраненный поиск.**  Определяет выполняемый поиск в журнале.  Один сохраненный поиск может использоваться несколькими правилами генерации оповещений.
- **Расписание.**  Определяет, как часто будет выполняться поиск в журнале.  У каждого правила генерации оповещений будет только одно расписание.
- **Действие оповещения.**  У каждого правила генерации оповещений будет один ресурс действия типа **Alert**, определяющий данные оповещения, такие как условия создания записи оповещения и серьезность оповещения.  Ресурс действия может также определять электронную почту и Runbook для ответа.
- **Действие webhook (необязательно).**  Если правило генерации оповещений будет вызывать webhook, то ему требуется дополнительный ресурс действия типа **Webhook**.    

Ресурсы сохраненных поисков описаны выше.  Другие ресурсы описываются ниже.


### <a name="schedule-resource"></a>Ресурс расписания

У сохраненного поиска может быть одно или несколько расписаний, представляющих отдельное правило генерации оповещений. Расписание определяет, как часто выполняется поиск, а также интервал времени для извлечения данных.  Ресурсы расписания имеют тип `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/`. Их структура приведена ниже. Далее представлены общие переменные и параметры, чтобы этот фрагмент кода можно было скопировать и вставить в файл решения и изменить имена параметров. 


    {
        "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name, '/', variables('Schedule').Name)]",
        "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/",
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('SavedSearch').Name)]"
        ],
        "properties": {
            "etag": "*",
            "interval": "[variables('Schedule').Interval]",
            "queryTimeSpan": "[variables('Schedule').TimeSpan]",
            "enabled": "[variables('Schedule').Enabled]"
        }
    }



В следующей таблице описаны свойства ресурсов расписания.

| Имя элемента | Обязательно | Описание |
|:--|:--|:--|
| Включено       | Да | Указывает, включено ли оповещение при его создании. |
| interval      | Да | Как часто выполняется запрос (в минутах). |
| queryTimeSpan | Да | Интервал времени в минутах, на котором следует оценивать результаты. |

Ресурс расписания будет зависеть от сохраненного поиска, поэтому он должен быть создан перед расписанием.


### <a name="actions"></a>Действия
Существуют два типа ресурса действия, которые задает свойство **Type**.  Для расписания требуется одно действие **Alert**, которое определяет сведения о правиле генерации оповещений и действия, предпринимаемые при создании оповещения.  Оно может также включать в себя действие **Webhook**, если оповещение должно вызывать webhook.  

Ресурсы действия имеют тип `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions`.  

#### <a name="alert-actions"></a>Действия оповещений

У каждого расписания будет одно действие **Alert**.  Оно определяет данные оповещения и, при необходимости, уведомление и действия для исправления  Уведомление позволяет отправить электронное сообщение на один или несколько адресов.  Исправление позволяет запустить Runbook в службе автоматизации Azure, чтобы попытаться устранить обнаруженную проблему.

Структура действий оповещений приведена ниже.  Далее представлены общие переменные и параметры, чтобы этот фрагмент кода можно было скопировать и вставить в файл решения и изменить имена параметров. 



    {
        "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name, '/', variables('Schedule').Name, '/', variables('Alert').Name)]",
        "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions",
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('SavedSearch').Name, '/schedules/', variables('Schedule').Name)]"
        ],
        "properties": {
            "etag": "*",
            "type": "Alert",
            "name": "[variables('Alert').Name]",
            "description": "[variables('Alert').Description]",
            "severity": "[variables('Alert').Severity]",
            "threshold": {
                "operator": "[variables('Alert').Threshold.Operator]",
                "value": "[variables('Alert').Threshold.Value]",
                "metricsTrigger": {
                    "triggerCondition": "[variables('Alert').Threshold.Trigger.Condition]",
                    "operator": "[variables('Alert').Trigger.Operator]",
                    "value": "[variables('Alert').Trigger.Value]"
                },
            },
            "emailNotification": {
                "recipients": [
                    "[variables('Alert').Recipients]"
                ],
                "subject": "[variables('Alert').Subject]"
            },
            "remediation": {
                "runbookName": "[variables('Alert').Remedition.RunbookName]",
                "webhookUri": "[variables('Alert').Remedition.WebhookUri]"
            }
        }
    }

В следующей таблице описаны свойства ресурсов действия оповещения.

| Имя элемента | Обязательно | Описание |
|:--|:--|:--|
| Тип | Да | Тип действия.  Для действий оповещения это будет **Alert**. |
| Имя | Да | Отображаемое имя оповещения.  Это имя, которое отображается в консоли для правила генерации оповещений. |
| Описание | Нет | Необязательное описание оповещения. |
| Severity | Да | Серьезность записи оповещения состоит из следующих значений.<br><br> **Critical**<br>**Предупреждение;**<br>**Informational** |


##### <a name="threshold"></a>Threshold (Пороговое значение)
Это обязательный раздел.  Он определяет свойства порога оповещения.

| Имя элемента | Обязательно | Описание |
|:--|:--|:--|
| Оператор | Да | Оператор сравнения может содержать следующие значения:<br><br>**gt — больше;<br>lt — меньше.** |
| Значение | Да | Значение для сравнения с результатами. |


##### <a name="metricstrigger"></a>MetricsTrigger
Это необязательный раздел.  Он добавляется для оповещения об измерении метрики.

> [!NOTE]
> Оповещения об измерении метрики в настоящее время находятся на этапе общедоступной предварительной версии. 

| Имя элемента | Обязательно | Описание |
|:--|:--|:--|
| TriggerCondition | Да | Указывает, задает ли порог общее число нарушений или число последовательных нарушений посредством следующих значений:<br><br>**Total;<br>Consecutive.** |
| Оператор | Да | Оператор сравнения может содержать следующие значения:<br><br>**gt — больше;<br>lt — меньше.** |
| Значение | Да | Определяет, сколько раз должны быть соблюдены условия для активации оповещения. |

##### <a name="throttling"></a>Регулирование
Это необязательный раздел.  Добавьте этот раздел, если некоторое время после создания оповещения тем же правилом его не нужно отображать.

| Имя элемента | Обязательно | Описание |
|:--|:--|:--|
| DurationInMinutes | Значение Yes, если добавлен элемент Throttling. | Количество минут, в течение которых оповещение не отображается после его создания тем же правилом генерации оповещений. |

##### <a name="emailnotification"></a>EmailNotification
 Этот раздел является необязательным. Добавьте его, если требуется, чтобы оповещение отправляло электронное сообщение одному или нескольким получателям.

| Имя элемента | Обязательно | Описание |
|:--|:--|:--|
| Recipients | Да | Разделенный запятыми список электронных адресов для отправки уведомления при создании оповещения, как показано в следующем примере.<br><br>**[ "recipient1@contoso.com", "recipient2@contoso.com" ]** |
| Субъект | Да | Строка темы электронного сообщения. |
| Вложение | Нет | Вложения в настоящее время не поддерживаются.  Если этот элемент добавлен, он должен иметь значение **None**. |


##### <a name="remediation"></a>Исправление
Этот раздел является необязательным. Добавьте его, если требуется, чтобы в ответ на оповещение запускался Runbook. |

| Имя элемента | Обязательно | Описание |
|:--|:--|:--|
| RunbookName | Да | Имя запускаемого модуля Runbook. |
| WebhookUri | Да | Универсальный код ресурса (URI) webhook для Runbook. |
| Expiry | Нет | Дата и время истечения срока действия исправления. |

#### <a name="webhook-actions"></a>Действия webhook

Действия webhook запускают процесс путем вызова URL-адреса и, при необходимости, предоставления полезных данных для отправки. Они похожи на действия исправления, но предназначены для объектов webhook, которые могут вызывать процессы, отличные от модулей Runbook службы автоматизации Azure. Они также включают дополнительную возможность предоставления полезных данных, доставляемых в удаленный процесс.

Если оповещение будет вызывать webhook, то помимо ресурса действия **Alert** ему требуется ресурс действия типа **Webhook**.  

    {
      "name": "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name, '/', variables('Schedule').Name, '/', variables('Webhook').Name)]",
      "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions/",
      "apiVersion": "[variables('LogAnalyticsApiVersion')]",
      "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('SavedSearch').Name, '/schedules/', variables('Schedule').Name)]"
      ],
      "properties": {
        "etag": "*",
        "type": "[variables('Alert').Webhook.Type]",
        "name": "[variables('Alert').Webhook.Name]",
        "webhookUri": "[variables('Alert').Webhook.webhookUri]",
        "customPayload": "[variables('Alert').Webhook.CustomPayLoad]"
      }
    }

В следующей таблице описаны свойства ресурсов действия webhook.

| Имя элемента | Обязательно | Description (Описание) |
|:--|:--|:--|
| type | Да | Тип действия.  Для действий webhook это будет **Webhook**. |
| name | Да | Отображаемое имя действия.  Оно не отображается в консоли. |
| wehookUri | Да | Универсальный код ресурса (URI) webhook. |
| CustomPayload | Нет | Пользовательские полезные данные, отправляемые в объект webhook. Формат зависит от данных, ожидаемых объектом webhook. |




## <a name="sample"></a>Образец

Ниже приведен пример решения со приведенными ниже ресурсами.

- Сохраненный поиск
- Расписание
- Действие оповещения
- Действия webhook

В примере используются переменные [стандартных параметров решения](operations-management-suite-solutions-solution-file.md#parameters), что является общепринятой практикой для решений, в отличие от жестко программируемых значений в определениях ресурсов.

    {
        "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0",
        "parameters": {
          "workspaceName": {
            "type": "string",
            "metadata": {
              "Description": "Name of Log Analytics workspace"
            }
          },
          "accountName": {
            "type": "string",
            "metadata": {
              "Description": "Name of Automation account"
            }
          },
          "workspaceregionId": {
            "type": "string",
            "metadata": {
              "Description": "Region of Log Analytics workspace"
            }
          },
          "regionId": {
            "type": "string",
            "metadata": {
              "Description": "Region of Automation account"
            }
          },
          "pricingTier": {
            "type": "string",
            "metadata": {
              "Description": "Pricing tier of both Log Analytics workspace and Azure Automation account"
            }
          },
          "recipients": {
            "type": "string",
            "metadata": {
              "Description": "List of recipients for the email alert separated by semicolon"
            }
          }
        },
        "variables": {
          "SolutionName": "MySolution",
          "SolutionVersion": "1.0",
          "SolutionPublisher": "Contoso",
          "ProductName": "SampleSolution",
    
          "LogAnalyticsApiVersion": "2015-11-01-preview",
    
          "MySearch": {
            "displayName": "Error records by hour",
            "query": "Type=MyRecord_CL | measure avg(Rating_d) by Instance_s interval 60minutes",
            "category": "Samples",
            "name": "Samples-Count of data"
          },
          "MyAlert": {
            "Name": "[toLower(concat('myalert-',uniqueString(resourceGroup().id, deployment().name)))]",
            "DisplayName": "My alert rule",
            "Description": "Sample alert.  Fires when 3 error records found over hour interval.",
            "Severity": "Critical",
            "ThresholdOperator": "gt",
            "ThresholdValue": 3,
            "Schedule": {
              "Name": "[toLower(concat('myschedule-',uniqueString(resourceGroup().id, deployment().name)))]",
              "Interval": 15,
              "TimeSpan": 60
            },
            "MetricsTrigger": {
              "TriggerCondition": "Consecutive",
              "Operator": "gt",
              "Value": 3
            },
            "ThrottleMinutes": 60,
            "Notification": {
              "Recipients": [
                "[parameters('recipients')]"
              ],
              "Subject": "Sample alert"
            },
            "Remediation": {
              "RunbookName": "MyRemediationRunbook",
              "WebhookUri": "https://s1events.azure-automation.net/webhooks?token=TluBFH3GpX4IEAnFoImoAWLTULkjD%2bTS0yscyrr7ogw%3d"
            },
            "Webhook": {
              "Name": "MyWebhook",
              "Uri": "https://MyService.com/webhook",
              "Payload": "{\"field1\":\"value1\",\"field2\":\"value2\"}"
            }
          }
        },
        "resources": [
          {
            "name": "[concat(variables('SolutionName'), '[' ,parameters('workspacename'), ']')]",
            "location": "[parameters('workspaceRegionId')]",
            "tags": { },
            "type": "Microsoft.OperationsManagement/solutions",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches', parameters('workspacename'), variables('MySearch').Name)]",
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name)]",
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Name)]",
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Webhook.Name)]"
            ],
            "properties": {
              "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces', parameters('workspacename'))]",
              "referencedResources": [
              ],
              "containedResources": [
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches', parameters('workspacename'), variables('MySearch').Name)]",
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name)]",
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Name)]",
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Webhook.Name)]"
              ]
            },
            "plan": {
              "name": "[concat(variables('SolutionName'), '[' ,parameters('workspaceName'), ']')]",
              "Version": "[variables('SolutionVersion')]",
              "product": "[variables('ProductName')]",
              "publisher": "[variables('SolutionPublisher')]",
              "promotionCode": ""
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [ ],
            "tags": { },
            "properties": {
              "etag": "*",
              "query": "[variables('MySearch').query]",
              "displayName": "[variables('MySearch').displayName]",
              "category": "[variables('MySearch').category]"
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name, '/', variables('MyAlert').Schedule.Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('MySearch').Name)]"
            ],
            "properties": {
              "etag": "*",
              "interval": "[variables('MyAlert').Schedule.Interval]",
              "queryTimeSpan": "[variables('MyAlert').Schedule.TimeSpan]",
              "enabled": true
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name, '/',  variables('MyAlert').Schedule.Name, '/',  variables('MyAlert').Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/',  variables('MySearch').Name, '/schedules/', variables('MyAlert').Schedule.Name)]"
            ],
            "properties": {
              "etag": "*",
              "Type": "Alert",
              "Name": "[variables('MyAlert').DisplayName]",
              "Description": "[variables('MyAlert').Description]",
              "Severity": "[variables('MyAlert').Severity]",
              "Threshold": {
                "Operator": "[variables('MyAlert').ThresholdOperator]",
                "Value": "[variables('MyAlert').ThresholdValue]",
                "MetricsTrigger": {
                  "TriggerCondition": "[variables('MyAlert').MetricsTrigger.TriggerCondition]",
                  "Operator": "[variables('MyAlert').MetricsTrigger.Operator]",
                  "Value": "[variables('MyAlert').MetricsTrigger.Value]"
                }
              },
              "Throttling": {
                "DurationInMinutes": "[variables('MyAlert').ThrottleMinutes]"
              },
              "EmailNotification": {
                "Recipients": "[variables('MyAlert').Notification.Recipients]",
                "Subject": "[variables('MyAlert').Notification.Subject]",
                "Attachment": "None"
              },
              "Remediation": {
                "RunbookName": "[variables('MyAlert').Remediation.RunbookName]",
                "WebhookUri": "[variables('MyAlert').Remediation.WebhookUri]"
              }
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name, '/', variables('MyAlert').Schedule.Name, '/', variables('MyAlert').Webhook.Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('MySearch').Name, '/schedules/', variables('MyAlert').Schedule.Name)]",
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('MySearch').Name, '/schedules/', variables('MyAlert').Schedule.Name, '/actions/',variables('MyAlert').Name)]"
            ],
            "properties": {
              "etag": "*",
              "Type": "Webhook",
              "Name": "[variables('MyAlert').Webhook.Name]",
              "WebhookUri": "[variables('MyAlert').Webhook.Uri]",
              "CustomPayload": "[variables('MyAlert').Webhook.Payload]"
            }
          }
        ]
    }


Следующий файл параметров содержит примеры значений для такого решения.

    {
        "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "workspacename": {
                "value": "myWorkspace"
            },
            "accountName": {
                "value": "myAccount"
            },
            "workspaceregionId": {
                "value": "East US"
            },
            "regionId": {
                "value": "East US 2"
            },
            "pricingTier": {
                "value": "Free"
            },
            "recipients": {
                "value": "recipient1@contoso.com;recipient2@contoso.com"
            }
        }
    }


## <a name="next-steps"></a>Дальнейшие действия
* [Добавьте представления](operations-management-suite-solutions-resources-views.md) в решение для управления.
* [Добавьте модули Runbook и другие ресурсы службы автоматизации](operations-management-suite-solutions-resources-automation.md) в решение для управления.

