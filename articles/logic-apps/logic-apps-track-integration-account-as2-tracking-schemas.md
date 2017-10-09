---
title: "схемы aaaAS2 отслеживания для наблюдения за B2B - приложения логики Azure | Документы Microsoft"
description: "Использовать AS2 отслеживание сообщений toomonitor B2B схемы из транзакций в вашей учетной записи интеграции Azure."
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: f169c411-1bd7-4554-80c1-84351247bf94
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: fe3c5845e2e80160d6857d8c308d836e88af7331
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="start-or-enable-tracking-of-as2-messages-and-mdns-toomonitor-success-errors-and-message-properties"></a>Запуск или включение отслеживание сообщения AS2, успех toomonitor MDN, ошибок и свойства сообщения
Эти схемы отслеживания AS2 можно использовать в вашей toohelp учетная запись Azure integration отслеживать операции бизнес бизнес (B2B):

* Схема отслеживания сообщений AS2
* Схема отслеживания уведомлений о состоянии сообщений AS2

## <a name="as2-message-tracking-schema"></a>Схема отслеживания сообщений AS2
````java

    {
       "agreementProperties": {  
            "senderPartnerName": "",  
            "receiverPartnerName": "",  
            "as2To": "",  
            "as2From": "",  
            "agreementName": ""  
        },  
        "messageProperties": {
            "direction": "",
            "messageId": "",
            "dispositionType": "",
            "fileName": "",
            "isMessageFailed": "",
            "isMessageSigned": "",
            "isMessageEncrypted": "",
            "isMessageCompressed": "",
            "correlationMessageId": "",
            "incomingHeaders": {
            },
            "outgoingHeaders": {
            },
        "isNrrEnabled": "",
        "isMdnExpected": "",
        "mdnType": ""
        }
    }
````

| Свойство | Тип | Описание |
| --- | --- | --- |
| senderPartnerName | Строка | Имя партнера отправителя сообщения AS2. (необязательный параметр) |
| receiverPartnerName | string | Имя партнера получателя сообщения AS2. (необязательный параметр) |
| as2To | Строка | Имя получателя сообщения AS2 из hello заголовки сообщения hello AS2. (обязательный параметр) |
| as2From | Строка | Имя отправителя сообщения AS2 из hello заголовки сообщения hello AS2. (обязательный параметр) |
| agreementName | Строка | Имя сообщения hello toowhich соглашение AS2 hello разрешаются. (необязательный параметр) |
| direction | Строка | Направление потока сообщений hello, получения или отправки. (обязательный параметр) |
| messageId | Строка | Код сообщения AS2, из hello заголовки сообщения hello AS2 (необязательно) |
| dispositionType |Строка | Значение типа метода обработки уведомлений о состоянии сообщения (MDN). (необязательный параметр) |
| fileName | Строка | Имя файла из заголовка hello сообщения hello AS2. (необязательный параметр) |
| isMessageFailed |Логический | Является ли сбой приветственное сообщение AS2. (обязательный параметр) |
| isMessageSigned | Логический | Указывает, подписан ли сообщение hello AS2. (обязательный параметр) |
| isMessageEncrypted | Логический | Зашифровано ли сообщение hello AS2. (обязательный параметр) |
| isMessageCompressed |Логический | Является ли сообщение hello AS2 была сжата. (обязательный параметр) |
| correlationMessageId | Строка | Идентификатор сообщения AS2, toocorrelate сообщения с MDN. (необязательный параметр) |
| incomingHeaders |Словарь JToken | Сведения о заголовке входящего сообщения AS2. (необязательный параметр) |
| outgoingHeaders |Словарь JToken | Сведения о заголовке исходящего сообщения AS2. (необязательный параметр) |
| isNrrEnabled | Логический | Используйте значение по умолчанию, если не известно значение hello. (обязательный параметр) |
| isMdnExpected | Логический | Используйте значение по умолчанию, если не известно значение hello. (обязательный параметр) |
| mdnType | Перечисление. | Допустимые значения: **NotConfigured**, **Sync** и **Async**. (обязательный параметр) |

## <a name="as2-mdn-tracking-schema"></a>Схема отслеживания уведомлений о состоянии сообщений AS2
````java

    {
        "agreementProperties": {
                "senderPartnerName": "",
                "receiverPartnerName": "",
                "as2To": "",
                "as2From": "",
                "agreementName": "g"
            },
            "messageProperties": {
                "direction": "",
                "messageId": "",
                "originalMessageId": "",
                "dispositionType": "",
                "isMessageFailed": "",
                "isMessageSigned": "",
                "isNrrEnabled": "",
                "statusCode": "",
                "micVerificationStatus": "",
                "correlationMessageId": "",
                "incomingHeaders": {
                },
                "outgoingHeaders": {
                }
            }
    }
````

| Свойство | Тип | Описание |
| --- | --- | --- |
| senderPartnerName | Строка | Имя партнера отправителя сообщения AS2. (необязательный параметр) |
| receiverPartnerName | string | Имя партнера получателя сообщения AS2. (необязательный параметр) |
| as2To | Строка | Имя участника, который получает сообщение hello AS2. (обязательный параметр) |
| as2From | Строка | Имя участника, который отправляет сообщение hello AS2. (обязательный параметр) |
| agreementName | Строка | Имя сообщения hello toowhich соглашение AS2 hello разрешаются. (необязательный параметр) |
| direction |Строка | Направление потока сообщений hello, получения или отправки. (обязательный параметр) |
| messageId | string | Идентификатор сообщения AS2. (необязательный параметр) |
| originalMessageId |string | Исходный идентификатор сообщения AS2. (необязательный параметр) |
| dispositionType | Строка | Значение типа метода обработки уведомлений о состоянии сообщения. (необязательный параметр) |
| isMessageFailed |Логический | Является ли сбой приветственное сообщение AS2. (обязательный параметр) |
| isMessageSigned |Логический | Указывает, подписан ли сообщение hello AS2. (обязательный параметр) |
| isNrrEnabled | Логический | Используйте значение по умолчанию, если не известно значение hello. (обязательный параметр) |
| statusCode | Перечисление. | Допустимые значения: **Accepted**, **Rejected** и **AcceptedWithErrros**. (обязательный параметр) |
| micVerificationStatus | Перечисление. | Допустимые значения: **NotApplicable**, **Succeeded** и **Failed**. (обязательный параметр) |
| correlationMessageId | string | Идентификатор корреляции. Hello исходного сообщения регистрируются ID (идентификатор сообщения hello, в котором настроено MDN hello). (необязательный параметр) |
| incomingHeaders | Словарь JToken | Указывает сведения о заголовке входящего сообщения. (необязательный параметр) |
| outgoingHeaders |Словарь JToken | Указывает сведения о заголовке исходящего сообщения. (необязательный параметр) |

## <a name="next-steps"></a>Дальнейшие действия
* Дополнительные сведения о hello [пакет интеграции Enterprise](../logic-apps/logic-apps-enterprise-integration-overview.md).    
* Дополнительные сведения о [мониторинге сообщений B2B](logic-apps-monitor-b2b-message.md).   
* Дополнительные сведения о [настраиваемых схемах отслеживания B2B](logic-apps-track-integration-account-custom-tracking-schema.md).   
* Дополнительные сведения о [схемах отслеживания X12](logic-apps-track-integration-account-x12-tracking-schema.md).   
* Дополнительные сведения о [отслеживание сообщений B2B на портале Operations Management Suite hello](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).
