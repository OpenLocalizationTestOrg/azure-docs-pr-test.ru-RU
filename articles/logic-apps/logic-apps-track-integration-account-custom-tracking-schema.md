---
title: "Отслеживание схемы B2B aaaCustom мониторинг - приложения логики Azure | Документы Microsoft"
description: "Создайте настраиваемое отслеживание схемы toomonitor B2B сообщения из транзакций в вашей учетной записи интеграции Azure."
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 433ae852-a833-44d3-a3c3-14cca33403a2
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8cf26a43d89f0414a2a8c5ef59d804235afeb5d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enable-tracking-toomonitor-your-complete-workflow-end-to-end"></a>Включить отслеживание toomonitor завершении рабочего процесса, конца в конец
Доступна встроенная функция отслеживания, которую можно включить для различных частей рабочего процесса B2B, например для отслеживания сообщений AS2 или X12. При создании рабочих процессов, включая приложения логики, BizTalk Server, SQL Server или любой другой слой, можно включить настраиваемое отслеживание, регистрирует события из hello начало toohello конец рабочего процесса. 

Этот раздел содержит пользовательский код, который можно использовать в слоях hello за пределами логику приложения. 

## <a name="custom-tracking-schema"></a>Настраиваемая схема отслеживания
````java

        {
            "sourceType": "",
            "source": {

            "workflow": {
                "systemId": ""
            },
            "runInstance": {
                "runId": ""
            },
            "operation": {
                "operationName": "",
                "repeatItemScopeName": "",
                "repeatItemIndex": "",
                "trackingId": "",
                "correlationId": "",
                "clientRequestId": ""
                }
            },
            "events": [
            {
                "eventLevel": "",
                "eventTime": "",
                "recordType": "",
                "record": {                
                }
            }
         ]
      }

````

| Свойство | Тип | Описание |
| --- | --- | --- |
| sourceType |   | Тип запуска hello источника. Допустимые значения — **Microsoft.Logic/workflows** или **custom**. (обязательный параметр) |
| Источник |   | Если тип источника hello **Microsoft.Logic/workflows**, сведения об источнике hello эта схема нужна toofollow. Если тип источника hello **пользовательские**, схема hello — JToken. (обязательный параметр) |
| systemId | Строка | Системный идентификатор приложения логики. (обязательный параметр) |
| runId | Строка | Идентификатор выполнения приложения логики. (обязательный параметр) |
| operationName | Строка | Имя операции hello (например, действий или триггер). (обязательный параметр) |
| repeatItemScopeName | Строка | Повторите имя элемента, если действие hello находится внутри `foreach` / `until` цикла. (обязательный параметр) |
| repeatItemIndex | Целое число  | Является ли действие hello внутри `foreach` / `until` цикла. Указывает индекс hello повторяющихся элементов. (обязательный параметр) |
| trackingId | Строка | Идентификатор отслеживания сообщений hello toocorrelate. (необязательный параметр) |
| correlationId | Строка | Идентификатор корреляции сообщений hello toocorrelate. (необязательный параметр) |
| clientRequestId | Строка | Клиент может заполнить его toocorrelate сообщения. (необязательный параметр) |
| eventLevel |   | Уровень события hello. (обязательный параметр) |
| eventTime |   | Время события hello в формате UTC, гггг-мм-DDTHH:MM:SS.00000Z. (обязательный параметр) |
| recordType |   | Тип записи отслеживания hello. Допустимое значение — **custom**. (обязательный параметр) |
| record |   | Настраиваемый тип записи. Разрешен формат JToken. (обязательный параметр) |

## <a name="b2b-protocol-tracking-schemas"></a>Схемы отслеживания для протоколов B2B
Сведения о схемах отслеживания для протоколов B2B см. в следующих статьях:
* [Схемы отслеживания AS2](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)   
* [Схемы отслеживания X12](logic-apps-track-integration-account-x12-tracking-schema.md)

## <a name="next-steps"></a>Дальнейшие действия
* Дополнительные сведения о [мониторинге сообщений B2B](logic-apps-monitor-b2b-message.md).   
* Дополнительные сведения о [отслеживание сообщений B2B на портале Operations Management Suite hello](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).
* Дополнительные сведения о hello [пакет интеграции Enterprise](../logic-apps/logic-apps-enterprise-integration-overview.md).
