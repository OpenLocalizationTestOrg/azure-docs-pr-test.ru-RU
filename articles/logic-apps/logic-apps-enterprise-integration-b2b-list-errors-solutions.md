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
ms.openlocfilehash: 1865d75f1b4c2aa18d5a3130f639572d19563b3e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="logic-apps-b2b-list-of-errors-and-solutions"></a><span data-ttu-id="5f0ba-103">Список ошибок Logic Apps B2B и их решения</span><span class="sxs-lookup"><span data-stu-id="5f0ba-103">Logic Apps B2B list of errors and solutions</span></span>  
<span data-ttu-id="5f0ba-104">В этой статье содержатся сведения об устранении ошибок в сценариях Logic Apps B2B, а также приведены соответствующие действия по их решению.</span><span class="sxs-lookup"><span data-stu-id="5f0ba-104">This article helps you troubleshoot errors that might happen in Logic Apps B2B scenarios and suggests appropriate actions for correcting those errors.</span></span>


## <a name="agreement-resolution"></a><span data-ttu-id="5f0ba-105">Определение соглашения</span><span class="sxs-lookup"><span data-stu-id="5f0ba-105">Agreement Resolution</span></span>

### <a name="no-agreement-found"></a><span data-ttu-id="5f0ba-106">*Соглашение не найдено</span><span class="sxs-lookup"><span data-stu-id="5f0ba-106">*No agreement found</span></span> 

|   |   |  
|---|---|
| <span data-ttu-id="5f0ba-107">Описание ошибки</span><span class="sxs-lookup"><span data-stu-id="5f0ba-107">Error description</span></span> | <span data-ttu-id="5f0ba-108">Отсутствует соглашение с параметрами определения соглашения.</span><span class="sxs-lookup"><span data-stu-id="5f0ba-108">No agreement found with Agreement Resolution Parameters</span></span>|    
| <span data-ttu-id="5f0ba-109">Рекомендуемые действия</span><span class="sxs-lookup"><span data-stu-id="5f0ba-109">User action</span></span> | <span data-ttu-id="5f0ba-110">Добавьте соглашение в учетную запись интеграции с согласованными бизнес-идентификаторами.</span><span class="sxs-lookup"><span data-stu-id="5f0ba-110">The agreement should be added to the integration account with agreed business identities.</span></span></br> <span data-ttu-id="5f0ba-111">Бизнес-идентификаторы должны совпадать с идентификаторами входящего сообщения.</span><span class="sxs-lookup"><span data-stu-id="5f0ba-111">The business identities should match to the input message ids</span></span>|  
|   |   |

### <a name="-no-agreement-found-with-identities"></a><span data-ttu-id="5f0ba-112">*Соглашение с идентификаторами отсутствует</span><span class="sxs-lookup"><span data-stu-id="5f0ba-112">* No agreement found with identities</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="5f0ba-113">Описание ошибки</span><span class="sxs-lookup"><span data-stu-id="5f0ba-113">Error description</span></span> | <span data-ttu-id="5f0ba-114">Отсутствует соглашение с идентификаторами 'AS2Identity'::'Partner1' и 'AS2Identity'::'Partner3'.</span><span class="sxs-lookup"><span data-stu-id="5f0ba-114">No agreement found with identities: 'AS2Identity'::'Partner1' and'AS2Identity'::'Partner3'</span></span>| 
| <span data-ttu-id="5f0ba-115">Рекомендуемые действия</span><span class="sxs-lookup"><span data-stu-id="5f0ba-115">User action</span></span> | <span data-ttu-id="5f0ba-116">В соглашении определены недопустимые идентификаторы AS2-From (AS2 — от) и AS2-To (AS2 — кому).</span><span class="sxs-lookup"><span data-stu-id="5f0ba-116">Invalid AS2-From or AS2-To configured for agreement.</span></span> </br> <span data-ttu-id="5f0ba-117">Введите правильные идентификаторы AS2-From (AS2 — от) и AS2-To (AS2 — кому) для сопоставления идентификаторов AS2 в заголовках сообщения AS2 с параметрами соглашения.</span><span class="sxs-lookup"><span data-stu-id="5f0ba-117">Correct AS2 message AS2-From or AS2-To headers or agreement to match AS2 ids in AS2 message headers with agreement configurations</span></span> |
|   |   |     

## <a name="as2"></a><span data-ttu-id="5f0ba-118">AS2</span><span class="sxs-lookup"><span data-stu-id="5f0ba-118">AS2</span></span>

### <a name="-missing-as2-message-headers"></a><span data-ttu-id="5f0ba-119">*Отсутствуют заголовки сообщения AS2</span><span class="sxs-lookup"><span data-stu-id="5f0ba-119">* Missing AS2 message headers</span></span>  

|   |   |  
|---|---|
| <span data-ttu-id="5f0ba-120">Описание ошибки</span><span class="sxs-lookup"><span data-stu-id="5f0ba-120">Error description</span></span>| <span data-ttu-id="5f0ba-121">Недопустимые заголовки AS2.</span><span class="sxs-lookup"><span data-stu-id="5f0ba-121">Invalid AS2 headers.</span></span> <span data-ttu-id="5f0ba-122">Идентификатор AS2-From (AS2 — от) или 2-To (AS2 — кому) пустой.</span><span class="sxs-lookup"><span data-stu-id="5f0ba-122">One of 'AS2-To' or 'AS2-From' headers are empty</span></span>| 
| <span data-ttu-id="5f0ba-123">Рекомендуемые действия</span><span class="sxs-lookup"><span data-stu-id="5f0ba-123">User action</span></span> | <span data-ttu-id="5f0ba-124">Получено сообщение AS2, не содержащее заголовки AS2-From (AS2 — от) или 2-To (AS2 — кому) (один из них или оба).</span><span class="sxs-lookup"><span data-stu-id="5f0ba-124">An AS2 message was received that did not contain the AS2-From or AS2-To or both headers.</span></span> </br> <span data-ttu-id="5f0ba-125">Проверьте эти заголовки и исправьте их в соответствии с конфигурацией соглашения.</span><span class="sxs-lookup"><span data-stu-id="5f0ba-125">Check AS2 message AS2-From and AS2-To headers and correct them based on agreement configuration</span></span> |
|  |  | 


### <a name="-missing-as2-message-body-and-headers"></a><span data-ttu-id="5f0ba-126">*Отсутствуют заголовки или текст сообщения AS2</span><span class="sxs-lookup"><span data-stu-id="5f0ba-126">* Missing AS2 message body and headers</span></span>    

|   |   |  
|---|---|
| <span data-ttu-id="5f0ba-127">Описание ошибки</span><span class="sxs-lookup"><span data-stu-id="5f0ba-127">Error description</span></span>| <span data-ttu-id="5f0ba-128">Содержимое запроса пустое или имеет значение Null.</span><span class="sxs-lookup"><span data-stu-id="5f0ba-128">The request content is null or empty</span></span> | 
| <span data-ttu-id="5f0ba-129">Рекомендуемые действия</span><span class="sxs-lookup"><span data-stu-id="5f0ba-129">User action</span></span> | <span data-ttu-id="5f0ba-130">Получено пустое сообщение AS2 (без текста).</span><span class="sxs-lookup"><span data-stu-id="5f0ba-130">An AS2 message was received that did not contain the message body</span></span> |
|  |  | 

### <a name="-as2-message-decryption-failure"></a><span data-ttu-id="5f0ba-131">*Ошибка расшифровки сообщения AS2</span><span class="sxs-lookup"><span data-stu-id="5f0ba-131">* AS2 message decryption failure</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="5f0ba-132">Описание ошибки</span><span class="sxs-lookup"><span data-stu-id="5f0ba-132">Error description</span></span> |  <span data-ttu-id="5f0ba-133">[processed/Error: decryption-failed]</span><span class="sxs-lookup"><span data-stu-id="5f0ba-133">[processed/Error: decryption-failed]</span></span> | 
| <span data-ttu-id="5f0ba-134">Рекомендуемые действия</span><span class="sxs-lookup"><span data-stu-id="5f0ba-134">User action</span></span> | <span data-ttu-id="5f0ba-135">Добавьте в сообщение AS2 параметр @base64ToBinary перед отправкой партнеру.</span><span class="sxs-lookup"><span data-stu-id="5f0ba-135">Add @base64ToBinary to AS2Message before sending to partner</span></span> 
```java
            "HTTP": {
                "inputs": {
                    "body": "@base64ToBinary(body('Encode_to_AS2_message')?['AS2Message']?['Content'])",
                    "headers": "@body('Encode_to_AS2_message')?['AS2Message']?['OutboundHeaders']",
                    "method": "POST",
                    "uri": "xxxxx.xxx"
                },
                
``` 

### <a name="-mdn-decryption-failure"></a><span data-ttu-id="5f0ba-136">*Ошибка расшифровки MDN</span><span class="sxs-lookup"><span data-stu-id="5f0ba-136">* MDN decryption failure</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="5f0ba-137">Описание ошибки</span><span class="sxs-lookup"><span data-stu-id="5f0ba-137">Error description</span></span> |  <span data-ttu-id="5f0ba-138">[processed/Error: decryption-failed]</span><span class="sxs-lookup"><span data-stu-id="5f0ba-138">[processed/Error: decryption-failed]</span></span> | 
| <span data-ttu-id="5f0ba-139">Рекомендуемые действия</span><span class="sxs-lookup"><span data-stu-id="5f0ba-139">User action</span></span> | <span data-ttu-id="5f0ba-140">Добавьте в сообщение MDN параметр @base64ToBinary перед отправкой партнеру.</span><span class="sxs-lookup"><span data-stu-id="5f0ba-140">Add @base64ToBinary to MDN before sending to partner</span></span> 
```java
            "Response": {
                "inputs": {
                    "body": "@base64ToBinary(body('Decode_AS2_message')?['OutgoingMDN']?['Content'])",
                    "headers": "@body('Decode_AS2_message')?['OutgoingMDN']?['OutboundHeaders']",
                    "statusCode": 200
                },
                
``` 

### <a name="-missing-signing-certificate"></a><span data-ttu-id="5f0ba-141">*Отсутствует сертификат для подписи</span><span class="sxs-lookup"><span data-stu-id="5f0ba-141">* Missing signing certificate</span></span>

|   |   |  
|---|---|
| <span data-ttu-id="5f0ba-142">Описание ошибки</span><span class="sxs-lookup"><span data-stu-id="5f0ba-142">Error description</span></span>| <span data-ttu-id="5f0ba-143">Сертификат для подписи не настроен для стороны AS2</span><span class="sxs-lookup"><span data-stu-id="5f0ba-143">The Signing Certificate has not been configured for AS2 party.</span></span> </br> <span data-ttu-id="5f0ba-144">(AS2-From: partner1 AS2-To: partner2)</span><span class="sxs-lookup"><span data-stu-id="5f0ba-144">AS2-From: partner1 AS2-To: partner2</span></span> | 
| <span data-ttu-id="5f0ba-145">Рекомендуемые действия</span><span class="sxs-lookup"><span data-stu-id="5f0ba-145">User action</span></span> | <span data-ttu-id="5f0ba-146">Настройте параметры соглашения AS2 с помощью правильного сертификата для подписи.</span><span class="sxs-lookup"><span data-stu-id="5f0ba-146">Configure AS2 agreement settings with correct certificate for signature</span></span> |
|  |  | 

## <a name="x12-and-edifact"></a><span data-ttu-id="5f0ba-147">X12 и EDIFACT</span><span class="sxs-lookup"><span data-stu-id="5f0ba-147">X12 and EDIFACT</span></span>

### <a name="-leading-or-trailing-space-found"></a><span data-ttu-id="5f0ba-148">*Лишний начальный или конечный пробел</span><span class="sxs-lookup"><span data-stu-id="5f0ba-148">* Leading or trailing space found</span></span>    
    
|   |   | 
|---|---|
| <span data-ttu-id="5f0ba-149">Описание ошибки</span><span class="sxs-lookup"><span data-stu-id="5f0ba-149">Error description</span></span> | <span data-ttu-id="5f0ba-150">Ошибка, обнаруженная во время синтаксического анализа.</span><span class="sxs-lookup"><span data-stu-id="5f0ba-150">Error encountered during parsing.</span></span> <span data-ttu-id="5f0ba-151">В наборе транзакций Edifact с идентификатором 123456, хранящимся в заголовке обмена (без группы) с идентификатором 987654, а также в идентификаторе отправителя Partner1 и получателя Partner2 обнаружена следующая ошибка: Leading Trailing separator found (Обнаружен начальный и конечный разделитель).</span><span class="sxs-lookup"><span data-stu-id="5f0ba-151">The Edifact transaction set with id '123456' contained in interchange (without group) with id '987654', with sender id 'Partner1', receiver id 'Partner2' is being suspended with following errors: Leading Trailing separator found</span></span> |
| <span data-ttu-id="5f0ba-152">Рекомендуемые действия</span><span class="sxs-lookup"><span data-stu-id="5f0ba-152">User action</span></span> | <span data-ttu-id="5f0ba-153">Разрешите начальный и конечный пробелы</span><span class="sxs-lookup"><span data-stu-id="5f0ba-153">The agreement settings to be configured to allow leading and trailing space.</span></span> </br> <span data-ttu-id="5f0ba-154">в параметрах соглашения.</span><span class="sxs-lookup"><span data-stu-id="5f0ba-154">Edit agreement settings to allow leading and trailing space</span></span> |
|   |   |

![Разрешение пробелов](./media/logic-apps-enterprise-integration-b2b-list-errors-solutions/leadingandtrailing.png)

### <a name="-duplicate-check-has-enabled-in-the-agreement"></a><span data-ttu-id="5f0ba-156">*В соглашении включены повторяющиеся параметры проверки</span><span class="sxs-lookup"><span data-stu-id="5f0ba-156">* Duplicate check has enabled in the agreement</span></span>

|   |   | 
|---|---| 
| <span data-ttu-id="5f0ba-157">Описание ошибки</span><span class="sxs-lookup"><span data-stu-id="5f0ba-157">Error description</span></span> | <span data-ttu-id="5f0ba-158">Повторяющиеся контрольные номера.</span><span class="sxs-lookup"><span data-stu-id="5f0ba-158">Duplicate Control Number</span></span> |
| <span data-ttu-id="5f0ba-159">Рекомендуемые действия</span><span class="sxs-lookup"><span data-stu-id="5f0ba-159">User action</span></span> | <span data-ttu-id="5f0ba-160">Эта ошибка означает, что полученное сообщение содержит повторяющиеся контрольные номера.</span><span class="sxs-lookup"><span data-stu-id="5f0ba-160">This error indicates the received message has duplicate control numbers.</span></span> </br> <span data-ttu-id="5f0ba-161">Исправьте контрольные номера и повторно отправьте сообщение.</span><span class="sxs-lookup"><span data-stu-id="5f0ba-161">Correct the control number and resend the message</span></span> |
|   |   |

### <a name="-missing-schema-in-the-agreement"></a><span data-ttu-id="5f0ba-162">*В соглашении отсутствует схема</span><span class="sxs-lookup"><span data-stu-id="5f0ba-162">* Missing schema in the agreement</span></span>

|   |   | 
|---|---| 
| <span data-ttu-id="5f0ba-163">Описание ошибки</span><span class="sxs-lookup"><span data-stu-id="5f0ba-163">Error description</span></span> | <span data-ttu-id="5f0ba-164">Ошибка, обнаруженная во время синтаксического анализа.</span><span class="sxs-lookup"><span data-stu-id="5f0ba-164">Error encountered during parsing.</span></span> <span data-ttu-id="5f0ba-165">В наборе транзакций X12 с идентификатором 564220001, хранящимся в функциональной группе с идентификатором 56422 в заголовке обмена с идентификатором 000056422, а также в идентификаторе отправителя 12345678 и идентификаторе получателя 87654321 обнаружена следующая ошибка: The message has an unknown document type and did not resolve to any of the existing schemas configured in the agreement (Неизвестный тип документов в сообщении, который не сопоставляется с имеющимися схемами в соглашении).</span><span class="sxs-lookup"><span data-stu-id="5f0ba-165">The X12 transaction set with id '564220001' contained in functional group with id '56422', in interchange with id '000056422', with sender id '12345678       ', receiver id '87654321       ' is being suspended with following errors "The message has an unknown document type and did not resolve to any of the existing schemas configured in the agreement"</span></span> |
| <span data-ttu-id="5f0ba-166">Рекомендуемые действия</span><span class="sxs-lookup"><span data-stu-id="5f0ba-166">User action</span></span> | <span data-ttu-id="5f0ba-167">Настройте схему в параметрах соглашения.</span><span class="sxs-lookup"><span data-stu-id="5f0ba-167">Configure schema in the agreement settings</span></span>  |
|   |   |

### <a name="-incorrect-schema-in-the-agreement"></a><span data-ttu-id="5f0ba-168">*Неправильная схема соглашения</span><span class="sxs-lookup"><span data-stu-id="5f0ba-168">* Incorrect schema in the agreement</span></span>

|   |   | 
|---|---| 
| <span data-ttu-id="5f0ba-169">Описание ошибки</span><span class="sxs-lookup"><span data-stu-id="5f0ba-169">Error description</span></span> | <span data-ttu-id="5f0ba-170">Неизвестный тип документов в сообщении, который не сопоставляется со всеми имеющимися схемами в соглашении.</span><span class="sxs-lookup"><span data-stu-id="5f0ba-170">The message has an unknown document type and did not resolve to any of the existing schemas configured in the agreement.</span></span> |
| <span data-ttu-id="5f0ba-171">Рекомендуемые действия</span><span class="sxs-lookup"><span data-stu-id="5f0ba-171">User action</span></span> | <span data-ttu-id="5f0ba-172">Настройте схему в параметрах соглашения.</span><span class="sxs-lookup"><span data-stu-id="5f0ba-172">Configure correct schema in the agreement settings</span></span>  |
|   |   |

## <a name="flat-file"></a><span data-ttu-id="5f0ba-173">Неструктурированный файл</span><span class="sxs-lookup"><span data-stu-id="5f0ba-173">Flat file</span></span>

### <a name="-input-message-with-no-body"></a><span data-ttu-id="5f0ba-174">*Входящее сообщение без текста</span><span class="sxs-lookup"><span data-stu-id="5f0ba-174">* Input message with no body</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="5f0ba-175">Описание ошибки</span><span class="sxs-lookup"><span data-stu-id="5f0ba-175">Error description</span></span> | <span data-ttu-id="5f0ba-176">Недопустимый шаблон.</span><span class="sxs-lookup"><span data-stu-id="5f0ba-176">InvalidTemplate.</span></span> <span data-ttu-id="5f0ba-177">Невозможно обработать выражения языка шаблона во входных данных действия Flat_File_Decoding в строке 1 и столбце 1902: обязательное свойство content ожидает значение, но возвращается Null.</span><span class="sxs-lookup"><span data-stu-id="5f0ba-177">Unable to process template language expressions in action 'Flat_File_Decoding' inputs at line '1' and column '1902': 'Required property 'content' expects a value but got null.</span></span> <span data-ttu-id="5f0ba-178">Путь ''.'.</span><span class="sxs-lookup"><span data-stu-id="5f0ba-178">Path ''.'.</span></span> |
| <span data-ttu-id="5f0ba-179">Рекомендуемые действия</span><span class="sxs-lookup"><span data-stu-id="5f0ba-179">User action</span></span> | <span data-ttu-id="5f0ba-180">Эта ошибка означает, что входящее сообщение не содержит текста.</span><span class="sxs-lookup"><span data-stu-id="5f0ba-180">This error indicates the input message does not contain a body</span></span> |
|   |   | 

## <a name="learn-more"></a><span data-ttu-id="5f0ba-181">Подробнее</span><span class="sxs-lookup"><span data-stu-id="5f0ba-181">Learn more</span></span>
[<span data-ttu-id="5f0ba-182">Обзор Пакета интеграции Enterprise</span><span class="sxs-lookup"><span data-stu-id="5f0ba-182">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md)