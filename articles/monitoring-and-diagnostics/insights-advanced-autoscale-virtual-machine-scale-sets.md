---
title: "aaaAdvanced автоматического масштабирования с использованием виртуальных машин Azure | Документы Microsoft"
description: "Использование Resource Manager и Масштабируемых наборов ВМ с несколькими правилами и профилями, которые отправляют сообщения электронной почты и вызывают URL-адреса объектов webhook с действиями масштабирования."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 7e3576e2-4a2b-4736-b5ae-98c4689cdd2b
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2016
ms.author: ancav
ms.openlocfilehash: ecb01e3094f715837b75ef07a7dbecdf0f2e78f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-autoscale-configuration-using-resource-manager-templates-for-vm-scale-sets"></a>Расширенная настройка автомасштабирования с помощью шаблонов Resource Manager для набора масштабирования виртуальных машин
Масштабируемые наборы виртуальных машин можно свертывать и развертывать на основе пороговых значений метрик производительности по расписанию или на определенную дату. Можно также настроить уведомления с помощью электронной почты и webhook для действий масштабирования. В этом пошаговом руководстве показан пример настройки всех этих объектов для масштабируемого набора виртуальных машин с помощью шаблона Resource Manager.

> [!NOTE]
> Хотя в этом пошаговом руководстве описаны шаги hello для набора масштабирования виртуальных Машин, hello же информация относится tooautoscaling [облачные службы](https://azure.microsoft.com/services/cloud-services/), и [службы приложений — веб-приложений](https://azure.microsoft.com/services/app-service/web/).
> Простой шкале in/out параметр в наборе масштабирования виртуальных Машин на основании метрики производительности простой как ЦП, описаны в toohello [Linux](../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md) и [Windows](../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md) документов
>
>

## <a name="walkthrough"></a>Пошаговое руководство
В этом пошаговом руководстве мы используем [обозревателя ресурсов Azure](https://resources.azure.com/) tooconfigure и обновления параметров автоматического масштабирования hello для набора масштабирования. Azure обозреватель ресурсов — простой способ toomanage ресурсы Azure через шаблоны диспетчера ресурсов. Новое средство обозревателя ресурсов tooAzure, прочитайте [вводном разделе](https://azure.microsoft.com/blog/azure-resource-explorer-a-new-tool-to-discover-the-azure-api/).

1. Разверните новый набор масштабирования с базовой конфигурацией автомасштабирования. В этой статье используется hello один из коллекции Azure краткое руководство, имеющая Windows hello в наборе с помощью шаблона основные автомасштабирования. Масштаб Linux задает hello рабочих таким же образом.
2. После создания набора масштабирования hello перейдите toohello шкалы набор ресурсов из обозревателя ресурсов Azure. Вы увидите следующее hello в узле с помощью Microsoft.Insights.

    ![Azure Explorer](./media/insights-advanced-autoscale-vmss/azure_explorer_navigate.png)

    выполнения шаблона Hello создал автомасштабирования по умолчанию с именем hello **«autoscalewad»**. На правой стороне hello можно просмотреть hello полное определение этого параметра автоматического масштабирования. В этом случае по умолчанию автомасштабирования hello поставляется с правила масштабирования и масштабирования в основе % ЦП.  

3. Теперь можно добавить дополнительные профили и правила на основе расписания hello или конкретных требований. Мы создадим конфигурацию автомасштабирования с тремя профилями. профили toounderstand и правила в автоматического масштабирования, просмотрите [автомасштабирования рекомендации](insights-autoscale-best-practices.md).  

    | Профили и правила | Description (Описание) |
    |--- | --- |
    | **Профиль** |**На основе производительности или метрики** |
    | правило; |Количество сообщений в очереди служебной шины > x |
    | правило; |Количество сообщений в очереди служебной шины < y |
    | правило; |% загрузки ЦП > n |
    | правило; |% загрузки ЦП < p |
    | **Профиль** |**Утренние часы в рабочие дни (без правил)** |
    | **Профиль** |**День запуска продукта (без правил)** |

4. Ниже приведен гипотетический сценарий масштабирования, который используется в данном пошаговом руководстве.

    * **На основе нагрузки** -как tooscale out или в зависимости от нагрузки hello в тестируемом приложении, размещенных на мой set.* шкалы
    * **Размер очереди сообщения** -использовать очередь служебной шины для hello входящих сообщений toomy приложения. Я использую количество сообщений в очереди hello и % ЦП и настройка tootrigger профиля по умолчанию действие масштабирования, если число сообщений или ЦП попаданий hello threshold.*
    * **Время недели и дня** -требуется еженедельного повторения «время дня hello» на основе профиля называется «Часов утра рабочего дня». На основе исторических данных, я знаю, что это лучше toohave уверенности, что количество виртуальных Машин экземпляров toohandle нагрузки моего приложения во время этого time.*
    * **Особые даты** — добавлен профиль "День запуска продукта". Я заранее определенных дат что мое приложение готово toohandle hello нагрузки из-за объявления маркетинга и когда мы поместили новый продукт hello application.*
    * *Hello двух последних профили могут также иметь другие метрики на основе правила производительности в них. В этом случае я решил не toohave один, и вместо этого правила на основе toorely на метрики производительности по умолчанию hello. Правила являются необязательными для hello повторяющейся основе даты и профили.*

    Приоритетов автомасштабирования engine профилей hello и правила также фиксируется при hello [автоматическое масштабирование рекомендации](insights-autoscale-best-practices.md) статьи.
    Список стандартных метрик для автомасштабирования см. в статье [Общие метрики автомасштабирования Azure Insights](insights-autoscale-common-metrics.md).

5. Убедитесь, что вы используете hello **чтения и записи** режим в обозревателе ресурсов

    ![Autoscalewad, конфигурация автомасштабирования по умолчанию](./media/insights-advanced-autoscale-vmss/autoscalewad.png)

6. Нажмите кнопку «Изменить». **Замените** элемент hello «профили» в заданной настройке автомасштабирования с hello следующая конфигурация:

    ![профили](./media/insights-advanced-autoscale-vmss/profiles.png)

    ```
    {
            "name": "Perf_Based_Scale",
            "capacity": {
              "minimum": "2",
              "maximum": "12",
              "default": "2"
            },
            "rules": [
              {
                "metricTrigger": {
                  "metricName": "MessageCount",
                  "metricNamespace": "",
                  "metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ServiceBus/namespaces/mySB/queues/myqueue",
                  "timeGrain": "PT5M",
                  "statistic": "Average",
                  "timeWindow": "PT5M",
                  "timeAggregation": "Average",
                  "operator": "GreaterThan",
                  "threshold": 10
                },
                "scaleAction": {
                  "direction": "Increase",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              },
              {
                "metricTrigger": {
                  "metricName": "MessageCount",
                  "metricNamespace": "",
                  "metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ServiceBus/namespaces/mySB/queues/myqueue",
                  "timeGrain": "PT5M",
                  "statistic": "Average",
                  "timeWindow": "PT5M",
                  "timeAggregation": "Average",
                  "operator": "LessThan",
                  "threshold": 3
                },
                "scaleAction": {
                  "direction": "Decrease",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              },
              {
                "metricTrigger": {
                  "metricName": "Percentage CPU",
                  "metricNamespace": "",
                  "metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.Compute/virtualMachineScaleSets/<this_vmss_name>",
                  "timeGrain": "PT5M",
                  "statistic": "Average",
                  "timeWindow": "PT30M",
                  "timeAggregation": "Average",
                  "operator": "GreaterThan",
                  "threshold": 85
                },
                "scaleAction": {
                  "direction": "Increase",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              },
              {
                "metricTrigger": {
                  "metricName": "Percentage CPU",
                  "metricNamespace": "",
                  "metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.Compute/virtualMachineScaleSets/<this_vmss_name>",
                  "timeGrain": "PT5M",
                  "statistic": "Average",
                  "timeWindow": "PT30M",
                  "timeAggregation": "Average",
                  "operator": "LessThan",
                  "threshold": 60
                },
                "scaleAction": {
                  "direction": "Decrease",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              }
            ]
          },
          {
            "name": "Weekday_Morning_Hours_Scale",
            "capacity": {
              "minimum": "4",
              "maximum": "12",
              "default": "4"
            },
            "rules": [],
            "recurrence": {
              "frequency": "Week",
              "schedule": {
                "timeZone": "Pacific Standard Time",
                "days": [
                  "Monday",
                  "Tuesday",
                  "Wednesday",
                  "Thursday",
                  "Friday"
                ],
                "hours": [
                  6
                ],
                "minutes": [
                  0
                ]
              }
            }
          },
          {
            "name": "Product_Launch_Day",
            "capacity": {
              "minimum": "6",
              "maximum": "20",
              "default": "6"
            },
            "rules": [],
            "fixedDate": {
              "timeZone": "Pacific Standard Time",
              "start": "2016-06-20T00:06:00Z",
              "end": "2016-06-21T23:59:00Z"
            }
          }
    ```
    Описание поддерживаемых полей и их значений см. в [документации по REST API автомасштабирования](https://msdn.microsoft.com/en-us/library/azure/dn931928.aspx). Теперь параметры автомасштабирования содержит три профиля hello описан ранее.

7. Наконец, просмотрите hello автомасштабирования **уведомления** раздела. Автомасштабирование уведомлений позволяют toodo три действия, когда к масштабному развертыванию или в действие успешно запущено.
   - Уведомлять об Здравствуйте, администратор и соадминистраторы подписки
   - от править электронное сообщение набору пользователей;
   - активировать вызов webhook. При создании этого веб-перехватчика отправляет метаданные об условии автоматическое масштабирование hello и задать масштаб hello ресурсов. toolearn Дополнительные сведения о полезных данных hello автомасштабирования веб-перехватчика, в разделе [настроить веб-перехватчика & уведомления по электронной почте для автомасштабирования](insights-autoscale-to-webhook-email.md).

   Добавить после замены параметра автомасштабирования toohello hello вашей **уведомления** элемент, значение которого равно null

   ```
   "notifications": [
      {
        "operation": "Scale",
        "email": {
          "sendToSubscriptionAdministrator": true,
          "sendToSubscriptionCoAdministrators": false,
          "customEmails": [
              "user1@mycompany.com",
              "user2@mycompany.com"
              ]
        },
        "webhooks": [
          {
            "serviceUri": "https://foo.webhook.example.com?token=abcd1234",
            "properties": {
              "optional_key1": "optional_value1",
              "optional_key2": "optional_value2"
            }
          }
        ]
      }
    ]

   ```

   Попаданий **поместить** кнопку в настройке автомасштабирования hello tooupdate обозреватель ресурсов.

Обновили параметр на tooinclude набор масштабирования виртуальных Машин нескольких профилей масштабирования автомасштабирования и масштабировать уведомления.

## <a name="next-steps"></a>Дальнейшие действия
Используйте эти ссылки toolearn Дополнительные сведения об автоматическом масштабировании.

[Устранение неполадок при автомасштабировании масштабируемых наборов виртуальных машин](../virtual-machine-scale-sets/virtual-machine-scale-sets-troubleshoot.md)

[Общие метрики автомасштабирования Azure Insights](insights-autoscale-common-metrics.md)

[Рекомендации по автомасштабированию Azure Insights](insights-autoscale-best-practices.md)

[Создание параметров автомасштабирования и управление ими](insights-powershell-samples.md#create-and-manage-autoscale-settings)

[Автомасштабирование](insights-cli-samples.md#autoscale)

[Использование действий автомасштабирования для отправки электронной почты и уведомлений об оповещениях веб-перехватчика в Azure Insights](insights-autoscale-to-webhook-email.md)
