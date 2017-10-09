---
title: "схемы aaaX12 отслеживания для наблюдения за B2B - приложения логики Azure | Документы Microsoft"
description: "Используйте отслеживание сообщений toomonitor B2B схемы из транзакций в вашей учетной записи Azure Integration X12."
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: a5413f80-eaad-4bcf-b371-2ad0ef629c3d
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ed1b338730214dcae12c367ebff025d7122328fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="start-or-enable-tracking-of-x12-messages-toomonitor-success-errors-and-message-properties"></a>Запуск или включение отслеживание X12 сообщения toomonitor успех, ошибок и свойства сообщения
Можно использовать эти X12 отслеживания схемы в вашей toohelp учетная запись Azure integration отслеживать операции бизнес бизнес (B2B):

* Схема отслеживания набора транзакций X12
* схема отслеживания подтверждения набора транзакций X12;
* схема отслеживания обмена X12;
* схема отслеживания подтверждения обмена X12;
* схема отслеживания функциональной группы X12;
* схема отслеживания подтверждения для функциональной группы X12.

## <a name="x12-transaction-set-tracking-schema"></a>Схема отслеживания набора транзакций X12
````java

    {
            "agreementProperties": {
                "senderPartnerName": "",
                "receiverPartnerName": "",
                "senderQualifier": "",
                "senderIdentifier": "",
                "receiverQualifier": "",
                "receiverIdentifier": "",
                "agreementName": ""
            },
            "messageProperties": {
                "direction": "",
                "interchangeControlNumber": "",
                "functionalGroupControlNumber": "",
                "transactionSetControlNumber": "",
                "CorrelationMessageId": "",
                "messageType": "",
                "isMessageFailed": "",
                "isTechnicalAcknowledgmentExpected": "",
                "isFunctionalAcknowledgmentExpected": "",
                "needAk2LoopForValidMessages":  "",
                "segmentsCount": ""
            }
    }
````

| Свойство | Тип | Описание |
| --- | --- | --- |
| senderPartnerName | Строка | Имя партнера отправителя сообщения X12. (необязательный параметр) |
| receiverPartnerName | Строка | Имя партнера получателя сообщения X12. (необязательный параметр) |
| senderQualifier | string | Отправка квалификатора партнера. (обязательный параметр) |
| senderIdentifier | Строка | Отправка идентификатора партнера. (обязательный параметр) |
| receiverQualifier | string | Получение квалификатора партнера. (обязательный параметр) |
| receiverIdentifier | Строка | Получение идентификатора партнера. (обязательный параметр) |
| agreementName | Строка | Имя X12 соглашение toowhich hello сообщений hello разрешаются. (необязательный параметр) |
| direction | Перечисление. | Направление потока сообщений hello, получения или отправки. (обязательный параметр) |
| interchangeControlNumber | Строка | Контрольный номер обмена. (необязательный параметр) |
| functionalGroupControlNumber | Строка | Функциональный контрольный номер. (необязательный параметр) |
| transactionSetControlNumber | Строка | Контрольный номер набора транзакций. (необязательный параметр) |
| CorrelationMessageId | Строка | Идентификатор сообщения корреляции. Сочетание свойств {AgreementName}{*GroupControlNumber*}{TransactionSetControlNumber}. (необязательный параметр) |
| messageType | string | Набор транзакций или тип документа. (необязательный параметр) |
| isMessageFailed | Логический | Является ли сообщение hello X12 сбой. (обязательный параметр) |
| isTechnicalAcknowledgmentExpected | Логический | Настроена ли Техническое подтверждение hello hello X12 соглашения. (обязательный параметр) |
| isFunctionalAcknowledgmentExpected | Логический | Настроена ли функциональное подтверждение hello hello X12 соглашения. (обязательный параметр) |
| needAk2LoopForValidMessages | Логический | Является ли цикл hello AK2 требуется допустимое сообщение. (обязательный параметр) |
| segmentsCount | Целое число  | Количество сегментов в наборе hello X12 транзакции. (необязательный параметр) |

## <a name="x12-transaction-set-acknowledgement-tracking-schema"></a>Схема отслеживания подтверждения набора транзакций X12
````java

    {
            "agreementProperties": {
                "senderPartnerName": "",
                "receiverPartnerName": "",
                "senderQualifier": "",
                "senderIdentifier": "",
                "receiverQualifier": "",
                "receiverIdentifier": "",
                "agreementName": ""
            },
            "messageProperties": {
                "direction": "",
                "interchangeControlNumber": "",
                "functionalGroupControlNumber": "",
                "isaSegment": "",
                "gsSegment": "",
                "respondingfunctionalGroupControlNumber": "",
                "respondingFunctionalGroupId": "",
                "respondingtransactionSetControlNumber": "",
                "respondingTransactionSetId": "",
                "statusCode": "",
                "processingStatus": "",
                "CorrelationMessageId": ""
                "isMessageFailed": "",
                "ak2Segment": "",
                "ak3Segment": "",
                "ak5Segment": ""
            }
    }
````

| Свойство | Тип | Описание |
| --- | --- | --- |
| senderPartnerName | Строка | Имя партнера отправителя сообщения X12. (необязательный параметр) |
| receiverPartnerName | Строка | Имя партнера получателя сообщения X12. (необязательный параметр) |
| senderQualifier | string | Отправка квалификатора партнера. (обязательный параметр) |
| senderIdentifier | Строка | Отправка идентификатора партнера. (обязательный параметр) |
| receiverQualifier | string | Получение квалификатора партнера. (обязательный параметр) |
| receiverIdentifier | Строка | Получение идентификатора партнера. (обязательный параметр) |
| agreementName | Строка | Имя X12 соглашение toowhich hello сообщений hello разрешаются. (необязательный параметр) |
| direction | Перечисление. | Направление потока сообщений hello, получения или отправки. (обязательный параметр) |
| interchangeControlNumber | Строка | Номер управления из функциональное подтверждение hello обменом. Значение заполняется только для hello отправляющая сторона, где функционального подтверждения для сообщений, отправляемых toopartner hello. (необязательный параметр) |
| functionalGroupControlNumber | Строка | Номер управления функциональной группы hello функциональное подтверждение. Значение заполняется только для hello отправляющая сторона, где функционального подтверждения для сообщений, отправляемых toopartner hello. (необязательный параметр) |
| isaSegment | Строка | Сегмент ISA приветственное сообщение. Значение заполняется только для hello отправляющая сторона, где функционального подтверждения для сообщений, отправляемых toopartner hello. (необязательный параметр) |
| gsSegment | Строка | Сегмент GS приветственное сообщение. Значение заполняется только для hello отправляющая сторона, где функционального подтверждения для сообщений, отправляемых toopartner hello. (необязательный параметр) |
| respondingfunctionalGroupControlNumber | Строка | Контрольный номер обмена в ответе. (необязательный параметр) |
| respondingFunctionalGroupId | Строка | Отвечать на запросы идентификатор функциональной группы, который сопоставляет tooAK101 hello подтверждения. (необязательный параметр) |
| respondingtransactionSetControlNumber | string | Контрольный номер набора транзакций в ответе. (необязательный параметр) |
| respondingTransactionSetId | Строка | Идентификатор, который сопоставляет tooAK201 подтверждение hello набора отвечает транзакций. (необязательный параметр) |
| statusCode | Логический | Код состояния подтверждения для набора транзакций. (обязательный параметр) |
| segmentsCount | Перечисление. | Код состояния подтверждения. Допустимые значения: **Accepted**, **Rejected** и **AcceptedWithErrros**. (обязательный параметр) |
| processingStatus | Перечисление. | Состояние обработки подтверждения hello. Допустимые значения: **Received**, **Generated** и **Sent**. (обязательный параметр) |
| CorrelationMessageId | Строка | Идентификатор сообщения корреляции. Сочетание свойств {AgreementName}{*GroupControlNumber*}{TransactionSetControlNumber}. (необязательный параметр) |
| isMessageFailed | Логический | Является ли сообщение hello X12 сбой. (обязательный параметр) |
| ak2Segment | Строка | Подтверждения для набора транзакций в hello получил функциональной группы. (необязательный параметр) |
| ak3Segment | Строка | Сообщает об ошибках в сегменте данных. (необязательный параметр) |
| ak5Segment | Строка | Сообщает набор идентифицированных в сегменте hello AK2 транзакций hello приняты или отклонены и почему. (необязательный параметр) |

## <a name="x12-interchange-tracking-schema"></a>Схема отслеживания обмена X12
````java

    {
            "agreementProperties": {
                "senderPartnerName": "",
                "receiverPartnerName": "",
                "senderQualifier": "",
                "senderIdentifier": "",
                "receiverQualifier": "",
                "receiverIdentifier": "",
                "agreementName": ""
            },
            "messageProperties": {
                "direction": "",
                "interchangeControlNumber": "",
                "isaSegment": "",
                "isTechnicalAcknowledgmentExpected": "",
                "isMessageFailed": "",
                "isa09": "",
                "isa10": "",
                "isa11": "",
                "isa12": "",
                "isa14": "",
                "isa15": "",
                "isa16": ""
            }
    }
````

| Свойство | Тип | Описание |
| --- | --- | --- |
| senderPartnerName | Строка | Имя партнера отправителя сообщения X12. (необязательный параметр) |
| receiverPartnerName | Строка | Имя партнера получателя сообщения X12. (необязательный параметр) |
| senderQualifier | string | Отправка квалификатора партнера. (обязательный параметр) |
| senderIdentifier | Строка | Отправка идентификатора партнера. (обязательный параметр) |
| receiverQualifier | string | Получение квалификатора партнера. (обязательный параметр) |
| receiverIdentifier | Строка | Получение идентификатора партнера. (обязательный параметр) |
| agreementName | Строка | Имя X12 соглашение toowhich hello сообщений hello разрешаются. (необязательный параметр) |
| direction | Перечисление. | Направление потока сообщений hello, получения или отправки. (обязательный параметр) |
| interchangeControlNumber | Строка | Контрольный номер обмена. (необязательный параметр) |
| isaSegment | Строка | Сегмент ISA сообщения. (необязательный параметр) |
| isTechnicalAcknowledgmentExpected | Логический | Настроена ли Техническое подтверждение hello hello X12 соглашения. (обязательный параметр) |
| isMessageFailed | Логический | Является ли сообщение hello X12 сбой. (обязательный параметр) |
| isa09 | string | Дата обмена документа X12. (необязательный параметр) |
| isa10 | Строка | Время обмена документа X12. (необязательный параметр) |
| isa11 | Строка | Идентификатор стандартов управления обмена X12. (необязательный параметр) |
| isa12 | string | Контрольный номер версии обмена X12. (необязательный параметр) |
| isa14 | Строка | Запрос подтверждения X12. (необязательный параметр) |
| isa15 | string | Индикатор для тестирования или работы. (необязательный параметр) |
| isa16 | Строка | Разделитель элементов. (необязательный параметр) |

## <a name="x12-interchange-acknowledgement-tracking-schema"></a>Схема отслеживания подтверждения обмена X12
````java
    {
            "agreementProperties": {
                "senderPartnerName": "",
                "receiverPartnerName": "",
                "senderQualifier": "",
                "senderIdentifier": "",
                "receiverQualifier": "",
                "receiverIdentifier": "",
                "agreementName": ""
            },
            "messageProperties": {
                "direction": "",
                "interchangeControlNumber": "",
                "isaSegment": "",
                "respondingInterchangeControlNumber": "",
                "isMessageFailed": "",
                "statusCode": "",
                "processingStatus": "",
                "ta102": "",
                "ta103": "",
                "ta105": ""
            }
    }
````

| Свойство | Тип | Описание |
| --- | --- | --- |
| senderPartnerName | Строка | Имя партнера отправителя сообщения X12. (необязательный параметр) |
| receiverPartnerName | Строка | Имя партнера получателя сообщения X12. (необязательный параметр) |
| senderQualifier | string | Отправка квалификатора партнера. (обязательный параметр) |
| senderIdentifier | Строка | Отправка идентификатора партнера. (обязательный параметр) |
| receiverQualifier | string | Получение квалификатора партнера. (обязательный параметр) |
| receiverIdentifier | Строка | Получение идентификатора партнера. (обязательный параметр) |
| agreementName | Строка | Имя X12 соглашение toowhich hello сообщений hello разрешаются. (необязательный параметр) |
| direction | Перечисление. | Направление потока сообщений hello, получения или отправки. (обязательный параметр) |
| interchangeControlNumber | Строка | Номер управления hello технических уведомлений, полученных от партнеров обменом. (необязательный параметр) |
| isaSegment | Строка | Сегмент ISA для hello Техническое подтверждение, полученные от партнеров. (необязательный параметр) |
| respondingInterchangeControlNumber |Строка | Номер управления для hello Техническое подтверждение, полученные от партнеров обменом. (необязательный параметр) |
| isMessageFailed | Логический | Является ли сообщение hello X12 сбой. (обязательный параметр) |
| statusCode | Перечисление. | Код состояния подтверждения обмена. Допустимые значения: **Accepted**, **Rejected** и **AcceptedWithErrros**. (обязательный параметр) |
| processingStatus | Перечисление. | Состояние подтверждения. Допустимые значения: **Received**, **Generated** и **Sent**. (обязательный параметр) |
| ta102 | string | Дата обмена. (необязательный параметр) |
| ta103 | string | Время обмена. (необязательный параметр) |
| ta105 | Строка | Код примечания обмена. (необязательный параметр) |

## <a name="x12-functional-group-tracking-schema"></a>Схема отслеживания функциональной группы X12
````java

    {
            "agreementProperties": {
                "senderPartnerName": "",
                "receiverPartnerName": "",
                "senderQualifier": "",
                "senderIdentifier": "",
                "receiverQualifier": "",
                "receiverIdentifier": "",
                "agreementName": ""
            },
            "messageProperties": {
                "direction": "",
                "interchangeControlNumber": "",
                "functionalGroupControlNumber": "",
                "gsSegment": "",
                "isTechnicalAcknowledgmentExpected": "",
                "isFunctionalAcknowledgmentExpected": "",
                "isMessageFailed": "",
                "gs01": "",
                "gs02": "",
                "gs03": "",
                "gs04": "",
                "gs05": "",
                "gs07": "",
                "gs08": ""
            }
    }
````

| Свойство | Тип | Описание |
| --- | --- | --- |
| senderPartnerName | Строка | Имя партнера отправителя сообщения X12. (необязательный параметр) |
| receiverPartnerName | Строка | Имя партнера получателя сообщения X12. (необязательный параметр) |
| senderQualifier | string | Отправка квалификатора партнера. (обязательный параметр) |
| senderIdentifier | Строка | Отправка идентификатора партнера. (обязательный параметр) |
| receiverQualifier | string | Получение квалификатора партнера. (обязательный параметр) |
| receiverIdentifier | Строка | Получение идентификатора партнера. (обязательный параметр) |
| agreementName | Строка | Имя X12 соглашение toowhich hello сообщений hello разрешаются. (необязательный параметр) |
| direction | Перечисление. | Направление потока сообщений hello, получения или отправки. (обязательный параметр) |
| interchangeControlNumber | Строка | Контрольный номер обмена. (необязательный параметр) |
| functionalGroupControlNumber | Строка | Функциональный контрольный номер. (необязательный параметр) |
| gsSegment | Строка | Сегмент GS сообщения. (необязательный параметр) |
| isTechnicalAcknowledgmentExpected | Логический | Настроена ли Техническое подтверждение hello hello X12 соглашения. (обязательный параметр) |
| isFunctionalAcknowledgmentExpected | Логический | Настроена ли функциональное подтверждение hello hello X12 соглашения. (обязательный параметр) |
| isMessageFailed | Логический | Является ли сообщение hello X12 сбой. (обязательный параметр)|
| gs01 | Строка | Код функционального идентификатора. (необязательный параметр) |
| gs02 | Строка | Код отправителя приложения. (необязательный параметр) |
| gs03 | Строка | Код получателя приложения. (необязательный параметр) |
| gs04 | Строка | Дата функциональной группы. (необязательный параметр) |
| gs05 | Строка | Время функциональной группы. (необязательный параметр) |
| gs07 | Строка | Код ответственного агентства. (необязательный параметр) |
| gs08 | Строка | Код версии, выпуска и промышленного идентификатора. (необязательный параметр) |

## <a name="x12-functional-group-acknowledgement-tracking-schema"></a>схема отслеживания подтверждения для функциональной группы X12.
````java
    {
            "agreementProperties": {
                "senderPartnerName": "",
                "receiverPartnerName": "",
                "senderQualifier": "",
                "senderIdentifier": "",
                "receiverQualifier": "",
                "receiverIdentifier": "",
                "agreementName": ""
            },
            "messageProperties": {
                "direction": "",
                "interchangeControlNumber": "",
                "functionalGroupControlNumber": "",
                "isaSegment": "",
                "gsSegment": "",
                "respondingfunctionalGroupControlNumber": "",
                "respondingFunctionalGroupId": "",
                "isMessageFailed": "",
                "statusCode": "",
                "processingStatus": "",
                "ak903": "",
                "ak904": "",
                "ak9Segment": ""
            }
    }
````

| Свойство | Тип | Описание |
| --- | --- | --- |
| senderPartnerName | Строка | Имя партнера отправителя сообщения X12. (необязательный параметр) |
| receiverPartnerName | Строка | Имя партнера получателя сообщения X12. (необязательный параметр) |
| senderQualifier | string | Отправка квалификатора партнера. (обязательный параметр) |
| senderIdentifier | Строка | Отправка идентификатора партнера. (обязательный параметр) |
| receiverQualifier | string | Получение квалификатора партнера. (обязательный параметр) |
| receiverIdentifier | Строка | Получение идентификатора партнера. (обязательный параметр) |
| agreementName | Строка | Имя X12 соглашение toowhich hello сообщений hello разрешаются. (необязательный параметр) |
| direction | Перечисление. | Направление потока сообщений hello, получения или отправки. (обязательный параметр) |
| interchangeControlNumber | Строка | Номера управления обменом, который заполняет для hello передающая сторона при получении Техническое подтверждение от партнеров. (необязательный параметр) |
| functionalGroupControlNumber | Строка | Номер функциональной группы управления Техническое подтверждение hello, который заполняет для hello передающая сторона при получении Техническое подтверждение от партнеров. (необязательный параметр) |
| isaSegment | Строка | Как и контрольный номер обмена, но заполняется только в определенных случаях. (необязательный параметр) |
| gsSegment | string | Как и контрольный номер функциональной группы, но заполняется только в определенных случаях. (необязательный параметр) |
| respondingfunctionalGroupControlNumber | Строка | Число hello исходного функциональной группы управления. (необязательный параметр) |
| respondingFunctionalGroupId | Строка | Сопоставляет tooAK101 в идентификаторе hello подтверждения функциональной группы. (необязательный параметр) |
| isMessageFailed | Логический | Является ли сообщение hello X12 сбой. (обязательный параметр) |
| statusCode | Перечисление. | Код состояния подтверждения. Допустимые значения: **Accepted**, **Rejected** и **AcceptedWithErrros**. (обязательный параметр) |
| processingStatus | Перечисление. | Состояние обработки подтверждения hello. Допустимые значения: **Received**, **Generated** и **Sent**. (обязательный параметр) |
| ak903 | Строка | Число полученных наборов транзакций. (необязательный параметр) |
| ak904 | Строка | Количество наборов транзакций принимается в определенных hello функциональной группы. (необязательный параметр) |
| ak9Segment | Строка | Hello функциональной группы, определенные в сегменте hello AK1 приняты или отклонены и почему. (необязательный параметр) |

## <a name="next-steps"></a>Дальнейшие действия
* Дополнительные сведения о [мониторинге сообщений B2B](logic-apps-monitor-b2b-message.md).
* Дополнительные сведения о [схемах отслеживания AS2](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md).
* Дополнительные сведения о [настраиваемых схемах отслеживания B2B](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md).
* Дополнительные сведения о [отслеживание сообщений B2B на портале Operations Management Suite hello](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).
* Дополнительные сведения о hello [пакет интеграции Enterprise](../logic-apps/logic-apps-enterprise-integration-overview.md).  
