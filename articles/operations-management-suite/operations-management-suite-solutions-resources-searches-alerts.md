---
title: "aaaSaved поиск и предупреждений в решениях OMS | Документы Microsoft"
description: "Как правило, решения в OMS включает сохраненные поисковые запросы в службе анализа журналов tooanalyze данные, собранные решением hello.  Они могут также определить предупреждения toonotify hello пользователем или автоматически выполнять определенные операции в ответ tooa критическую ошибку.  В этой статье описывается процедура toodefine анализа журналов сохранения оповещения и поиск в шаблон ARM, они могут быть включены в решения для управления."
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
ms.openlocfilehash: 93d7c5bbf061473833ca6c0a8e4d8e10d923f3ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="adding-log-analytics-saved-searches-and-alerts-toooms-management-solution-preview"></a>Добавление службы анализа журналов сохранены tooOMS оповещения и поиск решения для управления (Предварительная версия)

> [!NOTE]
> Это предварительная документация для создания решений для управления в консоли OMS, которая доступна в данный момент в режиме предварительной версии. Ни одной схеме, описанной ниже — toochange субъекта.   


[Решения для управления в OMS](operations-management-suite-solutions.md) как правило, включает [сохраненные поисковые запросы](../log-analytics/log-analytics-log-searches.md) в службе анализа журналов tooanalyze данные, собранные решением hello.  Они также могут определять [оповещения](../log-analytics/log-analytics-alerts.md) toonotify hello пользователем или автоматически выполнять определенные операции в ответ tooa критическую ошибку.  В этой статье описывается процедура сохранения toodefine анализа журналов, поиска и оповещений в [управление ресурсами шаблона](../resource-manager-template-walkthrough.md) , они могут быть включены в [решения для управления](operations-management-suite-solutions-creating.md).

> [!NOTE]
> Hello примеры в этой статье с помощью параметров и переменные, которые либо обязательными или общие toomanagement решений и описано в [создание решений для управления в Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)  

## <a name="prerequisites"></a>Предварительные требования
В этой статье предполагается, что вы уже знакомы с работой слишком[создать решение управления](operations-management-suite-solutions-creating.md) и структуру hello [шаблон ARM](../resource-group-authoring-templates.md) и файл решения.


## <a name="log-analytics-workspace"></a>Рабочая область Log Analytics
Все ресурсы в Log Analytics размещаются в [рабочей области](../log-analytics/log-analytics-manage-access.md).  Как описано в [OMS рабочей области и учетной записи автоматизации](operations-management-suite-solutions.md#oms-workspace-and-automation-account) hello рабочей области не включен в решение по управлению hello, но должна существовать до установки решения hello.  Если эти сведения недоступны, то произойдет сбой установки решения hello.

Имя Hello hello рабочей области находится в hello имя каждого ресурса анализа журналов.  Для этого в решении hello с hello **рабочей** параметра как следующий пример сохраненным результатом поиска ресурса hello.

    "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearchId'))]"


## <a name="saved-searches"></a>Сохраненные поиски
Включить [сохраненные поисковые запросы](../log-analytics/log-analytics-log-searches.md) в решение tooallow пользователей tooquery данные, собранные в решении.  Сохраненные условия поиска будут отображаться в узле **Избранное** на портале OMS hello и **сохраненные поиски** в hello портал Azure.  Сохраненный поиск также является обязательным для каждого оповещения.   

[Служба аналитики журналов сохраненного поиска](../log-analytics/log-analytics-log-searches.md) ресурсы имеют тип `Microsoft.OperationalInsights/workspaces/savedSearches` и имеют следующие структуры hello.  Сюда входят общие переменные и параметры, чтобы скопировать и вставить этот фрагмент кода в файл решения и измените имена параметров hello. 

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



Каждое из свойств hello сохраненного поиска описаны в следующей таблице hello. 

| Свойство | Описание |
|:--- |:--- |
| category | Категория Hello hello сохраненные условия поиска.  Все сохраненные поисковые запросы в hello того же решения часто общей папки одной категории, они группируются в консоли hello. |
| displayname | Имя toodisplay для hello сохраненного поиска в портале hello. |
| query | Toorun запроса. |

> [!NOTE]
> Toouse escape-символы в запросе hello может понадобиться, если он содержит символы, которые можно интерпретировать как JSON.  Например, если запрос был **OperationName:"Microsoft.Compute/virtualMachines/write типа: AzureActivity»**, должен быть записан в файл решения hello как **Имя_операции типа: AzureActivity:\" Microsoft.Compute/virtualMachines/write\"**.

## <a name="alerts"></a>Оповещения
[Оповещения Log Analytics](../log-analytics/log-analytics-alerts.md) создаются правилами генерации оповещений, которые выполняют сохраненный через равные промежутки времени.  Если hello результаты запроса hello соответствующих указанным критериям, создается запись предупреждений и выполняются одно или несколько действий.  

Правила оповещений в решении для управления состоят из следующих трех разных ресурсов hello.

- **Сохраненный поиск.**  Определяет hello поиска журналов, которые будут запущены.  Один сохраненный поиск может использоваться несколькими правилами генерации оповещений.
- **Расписание.**  Определяет, как часто hello поиска журналов будет выполняться.  У каждого правила генерации оповещений будет только одно расписание.
- **Действие оповещения.**  Каждое правило оповещения будут иметь один ресурс действие с типом **предупреждение** , определяющий hello подробные сведения о предупреждении hello, например hello критерий будет создана запись предупреждений и hello серьезность предупреждения.  ресурс действие Hello будет определять ответ почты и runbook.
- **Действие webhook (необязательно).**  Если правило оповещения hello будет вызывать веб-перехватчика, то требуется дополнительное действие ресурс с типом **веб-перехватчика**.    

Ресурсы сохраненных поисков описаны выше.  Hello другие ресурсы, описаны ниже.


### <a name="schedule-resource"></a>Ресурс расписания

У сохраненного поиска может быть одно или несколько расписаний, представляющих отдельное правило генерации оповещений. Hello расписание определяет частоту hello поиска выполняется и hello интервал времени, через какие hello извлекаются данные.  Планирование ресурсов имеют тип `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/` и имеют следующие структуры hello. Сюда входят общие переменные и параметры, чтобы скопировать и вставить этот фрагмент кода в файл решения и измените имена параметров hello. 


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



в hello в следующей таблице описаны свойства Hello планирование ресурсов.

| Имя элемента | Обязательно | Описание |
|:--|:--|:--|
| Включено       | Да | Указывает, включено ли предупреждение hello при его создании. |
| interval      | Да | Как часто hello запрос выполняется в минутах. |
| queryTimeSpan | Да | Продолжительность времени в минутах, по которому tooevaluate результаты. |

Планирование ресурсов Hello должны зависеть от сохраненного поиска, чтобы он создан, прежде чем расписание hello hello.


### <a name="actions"></a>Действия
Существует два типа действия ресурса, указанного в hello **тип** свойства.  Расписание требуется один **предупреждение** действия, который определяет сведения hello правило генерации оповещений hello и действия, предпринимаемые при создании оповещения.  Он также может включать **веб-перехватчика** действие, если веб-перехватчика должна вызываться из hello предупреждения.  

Ресурсы действия имеют тип `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions`.  

#### <a name="alert-actions"></a>Действия оповещений

У каждого расписания будет одно действие **Alert**.  Определяет сведения hello hello предупреждение, и при необходимости действия уведомления и исправления.  Уведомление отправляется по электронной почте tooone или несколько адресов.  Исправление запуск модуля runbook в автоматизации Azure tooattempt tooremediate hello обнаружена проблема.

Оповещения имеют следующие структуры hello.  Сюда входят общие переменные и параметры, чтобы скопировать и вставить этот фрагмент кода в файл решения и измените имена параметров hello. 



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

свойства Hello ресурсов действие предупреждения описаны в следующей таблице hello.

| Имя элемента | Обязательно | Описание |
|:--|:--|:--|
| Тип | Да | Тип действия hello.  Для действий оповещения это будет **Alert**. |
| Имя | Да | Отображаемое имя для hello предупреждения.  Это имя hello, которое отображается в консоли hello для правила оповещения hello. |
| Описание | Нет | Необязательное описание предупреждения hello. |
| Severity | Да | Серьезность предупреждения записи hello из hello следующие значения:<br><br> **Critical**<br>**Предупреждение;**<br>**Informational** |


##### <a name="threshold"></a>Threshold (Пороговое значение)
Это обязательный раздел.  Он определяет свойства hello hello порога оповещения.

| Имя элемента | Обязательно | Описание |
|:--|:--|:--|
| Оператор | Да | Оператор для сравнения hello из hello следующие значения:<br><br>**gt — больше;<br>lt — меньше.** |
| Значение | Да | результаты hello toocompare значение Hello. |


##### <a name="metricstrigger"></a>MetricsTrigger
Это необязательный раздел.  Он добавляется для оповещения об измерении метрики.

> [!NOTE]
> Оповещения об измерении метрики в настоящее время находятся на этапе общедоступной предварительной версии. 

| Имя элемента | Обязательно | Описание |
|:--|:--|:--|
| TriggerCondition | Да | Указывает, является ли hello пороговое значение для общее число нарушений или последовательных нарушения безопасности hello следующие значения:<br><br>**Total;<br>Consecutive.** |
| Оператор | Да | Оператор для сравнения hello из hello следующие значения:<br><br>**gt — больше;<br>lt — меньше.** |
| Значение | Да | Число hello время hello условия должно быть выполнены tootrigger hello предупреждение. |

##### <a name="throttling"></a>Регулирование
Это необязательный раздел.  Включите в этом разделе, если требуется, чтобы предупреждения toosuppress от hello же правило минимальное количество времени, после создания предупреждения.

| Имя элемента | Обязательно | Описание |
|:--|:--|:--|
| DurationInMinutes | Значение Yes, если добавлен элемент Throttling. | Число минут toosuppress оповещений после одного из hello созданных же правило оповещения. |

##### <a name="emailnotification"></a>EmailNotification
 Этот раздел является необязательным включить его, если вы хотите hello предупреждения toosend mail tooone или нескольких получателей.

| Имя элемента | Обязательно | Описание |
|:--|:--|:--|
| Recipients | Да | Список с разделителями-запятыми по электронной почте адресов toosend уведомление при создании оповещения как в следующий пример hello.<br><br>**[ "recipient1@contoso.com", "recipient2@contoso.com" ]** |
| Субъект | Да | Тема сообщений hello. |
| Вложение | Нет | Вложения в настоящее время не поддерживаются.  Если этот элемент добавлен, он должен иметь значение **None**. |


##### <a name="remediation"></a>Исправление
Этот раздел является необязательным включите его, если требуется, чтобы toostart runbook в предупреждении toohello ответа. |

| Имя элемента | Обязательно | Описание |
|:--|:--|:--|
| RunbookName | Да | Имя hello runbook toostart. |
| WebhookUri | Да | URI веб-перехватчика hello для hello runbook. |
| Expiry | Нет | Дата и время hello исправления истечения срока действия. |

#### <a name="webhook-actions"></a>Действия webhook

Действия веб-перехватчика запустить процесс путем вызова URL-адрес и Дополнительно может предоставлять полезные данные toobe отправлено. Они являются подобные действия tooRemediation, за исключением того, они предназначены для веб-перехватчиков, который может вызывать процессами, отличными от Runbook автоматизации Azure. Они также предоставляют hello дополнительную возможность предоставления удаленных процессов toohello toobe доставляется полезных данных.

Если оповещение будет вызывать веб-перехватчика, то он должен быть ресурс действие с типом **веб-перехватчика** в дополнение toohello **предупреждение** действия ресурса.  

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

Hello свойств ресурсов веб-перехватчика действия описаны в hello в следующей таблице.

| Имя элемента | Обязательно | Description (Описание) |
|:--|:--|:--|
| type | Да | Тип действия hello.  Для действий webhook это будет **Webhook**. |
| name | Да | Отображаемое имя для действия hello.  Не отображается в консоли hello. |
| wehookUri | Да | URI для веб-перехватчика hello. |
| CustomPayload | Нет | Настраиваемые полезные данные отправлены toobe toohello веб-перехватчика. Формат Hello будет зависеть от ожидается какой веб-перехватчика hello. |




## <a name="sample"></a>Образец

Ниже приведен образец, включают решение, включающее hello следующие ресурсы:

- Сохраненный поиск
- Расписание
- Действие оповещения
- Действия webhook

Здравствуйте, образец использует [параметры стандартное решение](operations-management-suite-solutions-solution-file.md#parameters) переменные, которые часто используются в решении, что отличие от значений toohardcoding в hello определения ресурсов.

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
              "Description": "List of recipients for hello email alert separated by semicolon"
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


Следующий файл параметров Hello предоставляет значения, образцы для этого решения.

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
* [Добавление представления](operations-management-suite-solutions-resources-views.md) tooyour решение для управления.
* [Добавить Runbook автоматизации и другим ресурсам](operations-management-suite-solutions-resources-automation.md) tooyour решение для управления.

