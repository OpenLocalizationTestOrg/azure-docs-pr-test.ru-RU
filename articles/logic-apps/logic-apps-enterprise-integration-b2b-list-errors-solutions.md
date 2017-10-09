---
title: "Список ошибок Logic Apps B2B и их решения. Служба приложений Azure | Документация Майкрософт"
description: "Список ошибок Logic Apps B2B и их решения"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: cf44af18-1fe5-41d5-9e06-cc57a968207c
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 0340e2979f1972ba631354e206c93969e55946e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="logic-apps-b2b-list-of-errors-and-solutions"></a>Список ошибок Logic Apps B2B и их решения  
В этой статье содержатся сведения об устранении ошибок в сценариях Logic Apps B2B, а также приведены соответствующие действия по их решению.


## <a name="agreement-resolution"></a>Определение соглашения

### <a name="no-agreement-found"></a>*Соглашение не найдено 

|   |   |  
|---|---|
| Описание ошибки | Отсутствует соглашение с параметрами определения соглашения.|    
| Рекомендуемые действия | Hello соглашения должны быть добавлены toohello учетной записи интеграции с согласованный бизнес-идентификаторы.</br> бизнес-идентификаторы Hello должен соответствовать toohello входного сообщения с идентификаторами|  
|   |   |

### <a name="-no-agreement-found-with-identities"></a>*Соглашение с идентификаторами отсутствует

|   |   | 
|---|---|
| Описание ошибки | Отсутствует соглашение с идентификаторами 'AS2Identity'::'Partner1' и 'AS2Identity'::'Partner3'.| 
| Рекомендуемые действия | Недопустимый AS2-от или AS2-tooconfigured для соглашения. </br> Правильное сообщение AS2 AS2-от или AS2 tooheaders или соглашение toomatch AS2 идентификаторы в AS2 заголовки сообщения с конфигурации соглашения |
|   |   |     

## <a name="as2"></a>AS2

### <a name="-missing-as2-message-headers"></a>*Отсутствуют заголовки сообщения AS2  

|   |   |  
|---|---|
| Описание ошибки| Недопустимые заголовки AS2. Идентификатор AS2-From (AS2 — от) или 2-To (AS2 — кому) пустой.| 
| Рекомендуемые действия | Получено сообщение AS2, не содержащий hello AS2-от или AS2 tooor оба заголовка. </br> Проверьте сообщение AS2 AS2-от и AS2-tooheaders и исправьте их, основываясь на конфигурации соглашения |
|  |  | 


### <a name="-missing-as2-message-body-and-headers"></a>*Отсутствуют заголовки или текст сообщения AS2    

|   |   |  
|---|---|
| Описание ошибки| содержимое запроса Hello пуст или равен null | 
| Рекомендуемые действия | Получено сообщение AS2, не содержащий тело сообщения hello |
|  |  | 

### <a name="-as2-message-decryption-failure"></a>*Ошибка расшифровки сообщения AS2

|   |   | 
|---|---|
| Описание ошибки |  [processed/Error: decryption-failed] | 
| Рекомендуемые действия | Добавить @base64ToBinary tooAS2Message перед отправкой toopartner 
```java
            "HTTP": {
                "inputs": {
                    "body": "@base64ToBinary(body('Encode_to_AS2_message')?['AS2Message']?['Content'])",
                    "headers": "@body('Encode_to_AS2_message')?['AS2Message']?['OutboundHeaders']",
                    "method": "POST",
                    "uri": "xxxxx.xxx"
                },
                
``` 

### <a name="-mdn-decryption-failure"></a>*Ошибка расшифровки MDN

|   |   | 
|---|---|
| Описание ошибки |  [processed/Error: decryption-failed] | 
| Рекомендуемые действия | Добавить @base64ToBinary tooMDN перед отправкой toopartner 
```java
            "Response": {
                "inputs": {
                    "body": "@base64ToBinary(body('Decode_AS2_message')?['OutgoingMDN']?['Content'])",
                    "headers": "@body('Decode_AS2_message')?['OutgoingMDN']?['OutboundHeaders']",
                    "statusCode": 200
                },
                
``` 

### <a name="-missing-signing-certificate"></a>*Отсутствует сертификат для подписи

|   |   |  
|---|---|
| Описание ошибки| Hello сертификат подписи не был настроен для стороны AS2. </br> (AS2-From: partner1 AS2-To: partner2) | 
| Рекомендуемые действия | Настройте параметры соглашения AS2 с помощью правильного сертификата для подписи. |
|  |  | 

## <a name="x12-and-edifact"></a>X12 и EDIFACT

### <a name="-leading-or-trailing-space-found"></a>*Лишний начальный или конечный пробел    
    
|   |   | 
|---|---|
| Описание ошибки | Ошибка, обнаруженная во время синтаксического анализа. Здравствуйте, набор с идентификатором "123456"содержащиеся в сообщении (без группа) с идентификатором "987654" Edifact транзакций, идентификатор отправителя «Partner1», идентификатор получателя «Partner2» приостановке за следующих ошибок: начальные конечные разделители найден |
| Рекомендуемые действия | Параметры toobe Hello соглашение настроено tooallow начальный и конечный пробелы. </br> Изменение соглашения параметры tooallow начальный и конечный пробелы |
|   |   |

![Разрешение пробелов](./media/logic-apps-enterprise-integration-b2b-list-errors-solutions/leadingandtrailing.png)

### <a name="-duplicate-check-has-enabled-in-hello-agreement"></a>* Проверка включил в соглашении hello

|   |   | 
|---|---| 
| Описание ошибки | Повторяющиеся контрольные номера. |
| Рекомендуемые действия | Эта ошибка указывает, что сообщение получено hello имеет повторяющихся контрольных чисел. </br> Исправьте контрольное число hello и повторно отправить сообщение hello |
|   |   |

### <a name="-missing-schema-in-hello-agreement"></a>* Отсутствует схема в соглашении hello

|   |   | 
|---|---| 
| Описание ошибки | Ошибка, обнаруженная во время синтаксического анализа. набор транзакций Hello X12 с идентификатором "564220001' содержащиеся в функциональной группы с идентификатором '56422', в сообщении с идентификатором"000056422"с идентификатором отправителя 12345678"», идентификатор получателя "87654321" приостановке следующих ошибок «hello сообщение имеет неизвестный документ ty PE и не помогли разрешить tooany hello существующих схем, настроенные в соглашении hello» |
| Рекомендуемые действия | Настройка схемы в параметры соглашения hello  |
|   |   |

### <a name="-incorrect-schema-in-hello-agreement"></a>* Неправильную схему в соглашении hello

|   |   | 
|---|---| 
| Описание ошибки | приветственное сообщение имеет неизвестный тип документа и не помогли разрешить tooany hello существующих схем, настроенные в соглашении hello. |
| Рекомендуемые действия | Настроить правильную схему в параметры соглашения hello  |
|   |   |

## <a name="flat-file"></a>Неструктурированный файл

### <a name="-input-message-with-no-body"></a>*Входящее сообщение без текста

|   |   | 
|---|---|
| Описание ошибки | Недопустимый шаблон. Не удается tooprocess выражения языка шаблона в входными параметрами действий «Flat_File_Decoding» в строке "1" и столбце "1902": "требуется свойство «content» ожидает значение но было получено значение null. Путь ''.'. |
| Рекомендуемые действия | Эта ошибка указывает, что входящее сообщение hello не содержит текста |
|   |   | 

## <a name="learn-more"></a>Подробнее
[Дополнительные сведения о hello пакет интеграции Enterprise](logic-apps-enterprise-integration-overview.md)
