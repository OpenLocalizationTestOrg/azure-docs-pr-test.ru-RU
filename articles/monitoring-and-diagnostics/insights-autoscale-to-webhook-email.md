---
title: "aaaUse автомасштабирования действия toosend электронной почты и веб-перехватчика уведомлений о предупреждениях. | Документация Майкрософт"
description: "См. как toocall действий автомасштабирования toouse веб-URL-адреса или отправлять уведомления по электронной почте в мониторе Azure. "
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: eb9a4c98-0894-488c-8ee8-5df0065d094f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/03/2017
ms.author: ancav
ms.openlocfilehash: f611a18f5a808412fbdd0c89e3addb36437064c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-autoscale-actions-toosend-email-and-webhook-alert-notifications-in-azure-monitor"></a>Используйте автомасштабирования действия toosend электронной почты и веб-перехватчика уведомлений о предупреждениях в мониторе Azure
В этой статье показано, как настраиваются триггеры, позволяющие вам обращаться к определенным URL-адресам или отправлять сообщения электронной почты на основе действий автоматического масштабирования в Azure.  

## <a name="webhooks"></a>Объекты Webhook
Веб-Перехватчики позволяют tooroute hello Azure уведомления о предупреждениях tooother системы, после обработки или пользовательские уведомления. Например маршрутизации tooservices предупреждения hello, которые могут обрабатывать входящие web запроса toosend SMS, журнал ошибок, уведомлять команды с помощью чата или служб обмена сообщениями, веб-перехватчика hello и т.д. URI должен быть действительной конечной точке HTTP или HTTPS.

## <a name="email"></a>Email
Tooany допустимый адрес электронной почты могут отправляться по электронной почте. Администраторы и соадминистраторы подписки hello, где запущено правило hello также получать уведомления.

## <a name="cloud-services-and-web-apps"></a>Облачные службы и веб-приложения
Можно включить в из hello портал Azure для облачных служб и ферм серверов (веб-приложений).

* Выберите hello **масштабирования по** метрику.

![scale by (масштабировать по)](./media/insights-autoscale-to-webhook-email/insights-autoscale-notify.png)

## <a name="virtual-machine-scale-sets"></a>Наборы для масштабирования виртуальных машин
Для новых виртуальных машин, созданных с помощью Resource Manager, наборы для масштабирования можно настроить с помощью REST API, шаблонов Resource Manager, PowerShell и интерфейса командной строки. Интерфейс портала еще недоступен.
При использовании hello API-интерфейса REST или шаблона диспетчера ресурсов, включите элемент уведомления hello hello следующие параметры.

```
"notifications": [
      {
        "operation": "Scale",
        "email": {
          "sendToSubscriptionAdministrator": false,
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
| Поле | Обязательное? | Описание |
| --- | --- | --- |
| операция |Да |Значение должно быть Scale. |
| sendToSubscriptionAdministrator |Да |Значение должно быть true или false. |
| sendToSubscriptionCoAdministrators |Да |Значение должно быть true или false. |
| customEmails |Да |Значение может быть null или массивом строк с адресами электронной почты. |
| Объекты Webhook |Да |Значение может быть null или допустимым универсальным кодом ресурса (URI). |
| serviceUri |Да |Допустимый универсальный код ресурса (URI) HTTPS. |
| properties |Да |Значение должно быть пустым {} или может содержать пары "ключ — значение". |

## <a name="authentication-in-webhooks"></a>Проверка подлинности в веб-перехватчиках
веб-перехватчика Hello могут проходить проверку подлинности с помощью проверки подлинности на основе токенов, где сохранить веб-перехватчика hello URI с маркера идентификатор как параметр запроса. Например, https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue

## <a name="autoscale-notification-webhook-payload-schema"></a>Схема полезных данных веб-перехватчика уведомлений автомасштабирования
При создании уведомлений автомасштабирования hello hello следующие метаданные входит в полезные данные веб-перехватчика hello:

```
{
        "version": "1.0",
        "status": "Activated",
        "operation": "Scale In",
        "context": {
                "timestamp": "2016-03-11T07:31:04.5834118Z",
                "id": "/subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/autoscalesettings/myautoscaleSetting",
                "name": "myautoscaleSetting",
                "details": "Autoscale successfully started scale operation for resource 'MyCSRole' from capacity '3' toocapacity '2'",
                "subscriptionId": "s1",
                "resourceGroupName": "rg1",
                "resourceName": "MyCSRole",
                "resourceType": "microsoft.classiccompute/domainnames/slots/roles",
                "resourceId": "/subscriptions/s1/resourceGroups/rg1/providers/microsoft.classicCompute/domainNames/myCloudService/slots/Production/roles/MyCSRole",
                "portalLink": "https://portal.azure.com/#resource/subscriptions/s1/resourceGroups/rg1/providers/microsoft.classicCompute/domainNames/myCloudService",
                "oldCapacity": "3",
                "newCapacity": "2"
        },
        "properties": {
                "key1": "value1",
                "key2": "value2"
        }
}
```


| Поле | Обязательное? | Описание |
| --- | --- | --- |
| status |Да |состояние Hello, которое указывает, что действие автоматического масштабирования была создана |
| операция |Да |Для увеличения экземпляров это будет "Развернуть", а для уменьшения экземпляров — "Свернуть" |
| context |Да |контекст действия автомасштабирования Hello |
| Timestamp |Да |Метка времени, когда было запущено действие hello автоматического масштабирования |
| id |Да |Идентификатор диспетчера ресурсов параметра автомасштабирования hello |
| name |Да |Имя настройки автомасштабирования hello Hello |
| сведения |Да |Описание действия hello, заняла службы автомасштабирования hello и hello изменение количества экземпляров hello |
| subscriptionId |Да |Идентификатор подписки целевой ресурс hello, масштаб изменяется |
| имя_группы_ресурсов |Да |Имя группы ресурсов целевой ресурс hello, масштаб изменяется |
| resourceName |Да |Имя ресурса целевой hello, масштаб изменяется |
| тип_ресурса |Да |Здравствуйте, три поддерживаемые значения: «microsoft.classiccompute/domainnames/slots/roles» - ролей облачной службы «microsoft.compute/virtualmachinescalesets» - наборы масштабирования виртуальной машины и «Microsoft.Web/serverfarms» — веб-приложения |
| resourceId |Да |Идентификатор целевого ресурса hello, масштабируется диспетчера ресурсов |
| portalLink |Да |Ссылка на портал Azure toohello hello целевого ресурса "Сводка" |
| oldCapacity |Да |Hello текущего (старая) число экземпляров когда Автомасштабирование были действие масштабирования |
| newCapacity |Да |число экземпляров новый Hello, автомасштабирования слишком масштабировать hello ресурсов|
| Свойства |Нет |необязательный параметр. Набор пар <ключ, значение> (например, Dictionary <String, String>). поле свойств Hello является необязательным. Настраиваемый пользовательский интерфейс или логики приложения на основе рабочего процесса можно ввести ключи и значения, которые могут быть переданы в полезных данных hello. Пользовательские свойства toopass резервное toohello исходящий вызов веб-перехватчика альтернативный способ — веб-перехватчика hello toouse URI себя (как параметры запроса) |
