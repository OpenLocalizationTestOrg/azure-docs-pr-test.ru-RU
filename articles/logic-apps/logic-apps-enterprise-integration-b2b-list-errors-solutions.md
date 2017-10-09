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
# <a name="logic-apps-b2b-list-of-errors-and-solutions"></a><span data-ttu-id="78270-103">Список ошибок Logic Apps B2B и их решения</span><span class="sxs-lookup"><span data-stu-id="78270-103">Logic Apps B2B list of errors and solutions</span></span>  
<span data-ttu-id="78270-104">В этой статье содержатся сведения об устранении ошибок в сценариях Logic Apps B2B, а также приведены соответствующие действия по их решению.</span><span class="sxs-lookup"><span data-stu-id="78270-104">This article helps you troubleshoot errors that might happen in Logic Apps B2B scenarios and suggests appropriate actions for correcting those errors.</span></span>


## <a name="agreement-resolution"></a><span data-ttu-id="78270-105">Определение соглашения</span><span class="sxs-lookup"><span data-stu-id="78270-105">Agreement Resolution</span></span>

### <a name="no-agreement-found"></a><span data-ttu-id="78270-106">*Соглашение не найдено</span><span class="sxs-lookup"><span data-stu-id="78270-106">*No agreement found</span></span> 

|   |   |  
|---|---|
| <span data-ttu-id="78270-107">Описание ошибки</span><span class="sxs-lookup"><span data-stu-id="78270-107">Error description</span></span> | <span data-ttu-id="78270-108">Отсутствует соглашение с параметрами определения соглашения.</span><span class="sxs-lookup"><span data-stu-id="78270-108">No agreement found with Agreement Resolution Parameters</span></span>|    
| <span data-ttu-id="78270-109">Рекомендуемые действия</span><span class="sxs-lookup"><span data-stu-id="78270-109">User action</span></span> | <span data-ttu-id="78270-110">Hello соглашения должны быть добавлены toohello учетной записи интеграции с согласованный бизнес-идентификаторы.</span><span class="sxs-lookup"><span data-stu-id="78270-110">hello agreement should be added toohello integration account with agreed business identities.</span></span></br> <span data-ttu-id="78270-111">бизнес-идентификаторы Hello должен соответствовать toohello входного сообщения с идентификаторами</span><span class="sxs-lookup"><span data-stu-id="78270-111">hello business identities should match toohello input message ids</span></span>|  
|   |   |

### <a name="-no-agreement-found-with-identities"></a><span data-ttu-id="78270-112">*Соглашение с идентификаторами отсутствует</span><span class="sxs-lookup"><span data-stu-id="78270-112">* No agreement found with identities</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="78270-113">Описание ошибки</span><span class="sxs-lookup"><span data-stu-id="78270-113">Error description</span></span> | <span data-ttu-id="78270-114">Отсутствует соглашение с идентификаторами 'AS2Identity'::'Partner1' и 'AS2Identity'::'Partner3'.</span><span class="sxs-lookup"><span data-stu-id="78270-114">No agreement found with identities: 'AS2Identity'::'Partner1' and'AS2Identity'::'Partner3'</span></span>| 
| <span data-ttu-id="78270-115">Рекомендуемые действия</span><span class="sxs-lookup"><span data-stu-id="78270-115">User action</span></span> | <span data-ttu-id="78270-116">Недопустимый AS2-от или AS2-tooconfigured для соглашения.</span><span class="sxs-lookup"><span data-stu-id="78270-116">Invalid AS2-From or AS2-tooconfigured for agreement.</span></span> </br> <span data-ttu-id="78270-117">Правильное сообщение AS2 AS2-от или AS2 tooheaders или соглашение toomatch AS2 идентификаторы в AS2 заголовки сообщения с конфигурации соглашения</span><span class="sxs-lookup"><span data-stu-id="78270-117">Correct AS2 message AS2-From or AS2-tooheaders or agreement toomatch AS2 ids in AS2 message headers with agreement configurations</span></span> |
|   |   |     

## <a name="as2"></a><span data-ttu-id="78270-118">AS2</span><span class="sxs-lookup"><span data-stu-id="78270-118">AS2</span></span>

### <a name="-missing-as2-message-headers"></a><span data-ttu-id="78270-119">*Отсутствуют заголовки сообщения AS2</span><span class="sxs-lookup"><span data-stu-id="78270-119">* Missing AS2 message headers</span></span>  

|   |   |  
|---|---|
| <span data-ttu-id="78270-120">Описание ошибки</span><span class="sxs-lookup"><span data-stu-id="78270-120">Error description</span></span>| <span data-ttu-id="78270-121">Недопустимые заголовки AS2.</span><span class="sxs-lookup"><span data-stu-id="78270-121">Invalid AS2 headers.</span></span> <span data-ttu-id="78270-122">Идентификатор AS2-From (AS2 — от) или 2-To (AS2 — кому) пустой.</span><span class="sxs-lookup"><span data-stu-id="78270-122">One of 'AS2-To' or 'AS2-From' headers are empty</span></span>| 
| <span data-ttu-id="78270-123">Рекомендуемые действия</span><span class="sxs-lookup"><span data-stu-id="78270-123">User action</span></span> | <span data-ttu-id="78270-124">Получено сообщение AS2, не содержащий hello AS2-от или AS2 tooor оба заголовка.</span><span class="sxs-lookup"><span data-stu-id="78270-124">An AS2 message was received that did not contain hello AS2-From or AS2-tooor both headers.</span></span> </br> <span data-ttu-id="78270-125">Проверьте сообщение AS2 AS2-от и AS2-tooheaders и исправьте их, основываясь на конфигурации соглашения</span><span class="sxs-lookup"><span data-stu-id="78270-125">Check AS2 message AS2-From and AS2-tooheaders and correct them based on agreement configuration</span></span> |
|  |  | 


### <a name="-missing-as2-message-body-and-headers"></a><span data-ttu-id="78270-126">*Отсутствуют заголовки или текст сообщения AS2</span><span class="sxs-lookup"><span data-stu-id="78270-126">* Missing AS2 message body and headers</span></span>    

|   |   |  
|---|---|
| <span data-ttu-id="78270-127">Описание ошибки</span><span class="sxs-lookup"><span data-stu-id="78270-127">Error description</span></span>| <span data-ttu-id="78270-128">содержимое запроса Hello пуст или равен null</span><span class="sxs-lookup"><span data-stu-id="78270-128">hello request content is null or empty</span></span> | 
| <span data-ttu-id="78270-129">Рекомендуемые действия</span><span class="sxs-lookup"><span data-stu-id="78270-129">User action</span></span> | <span data-ttu-id="78270-130">Получено сообщение AS2, не содержащий тело сообщения hello</span><span class="sxs-lookup"><span data-stu-id="78270-130">An AS2 message was received that did not contain hello message body</span></span> |
|  |  | 

### <a name="-as2-message-decryption-failure"></a><span data-ttu-id="78270-131">*Ошибка расшифровки сообщения AS2</span><span class="sxs-lookup"><span data-stu-id="78270-131">* AS2 message decryption failure</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="78270-132">Описание ошибки</span><span class="sxs-lookup"><span data-stu-id="78270-132">Error description</span></span> |  <span data-ttu-id="78270-133">[processed/Error: decryption-failed]</span><span class="sxs-lookup"><span data-stu-id="78270-133">[processed/Error: decryption-failed]</span></span> | 
| <span data-ttu-id="78270-134">Рекомендуемые действия</span><span class="sxs-lookup"><span data-stu-id="78270-134">User action</span></span> | <span data-ttu-id="78270-135">Добавить @base64ToBinary tooAS2Message перед отправкой toopartner</span><span class="sxs-lookup"><span data-stu-id="78270-135">Add @base64ToBinary tooAS2Message before sending toopartner</span></span> 
```java
            "HTTP": {
                "inputs": {
                    "body": "@base64ToBinary(body('Encode_to_AS2_message')?['AS2Message']?['Content'])",
                    "headers": "@body('Encode_to_AS2_message')?['AS2Message']?['OutboundHeaders']",
                    "method": "POST",
                    "uri": "xxxxx.xxx"
                },
                
``` 

### <a name="-mdn-decryption-failure"></a><span data-ttu-id="78270-136">*Ошибка расшифровки MDN</span><span class="sxs-lookup"><span data-stu-id="78270-136">* MDN decryption failure</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="78270-137">Описание ошибки</span><span class="sxs-lookup"><span data-stu-id="78270-137">Error description</span></span> |  <span data-ttu-id="78270-138">[processed/Error: decryption-failed]</span><span class="sxs-lookup"><span data-stu-id="78270-138">[processed/Error: decryption-failed]</span></span> | 
| <span data-ttu-id="78270-139">Рекомендуемые действия</span><span class="sxs-lookup"><span data-stu-id="78270-139">User action</span></span> | <span data-ttu-id="78270-140">Добавить @base64ToBinary tooMDN перед отправкой toopartner</span><span class="sxs-lookup"><span data-stu-id="78270-140">Add @base64ToBinary tooMDN before sending toopartner</span></span> 
```java
            "Response": {
                "inputs": {
                    "body": "@base64ToBinary(body('Decode_AS2_message')?['OutgoingMDN']?['Content'])",
                    "headers": "@body('Decode_AS2_message')?['OutgoingMDN']?['OutboundHeaders']",
                    "statusCode": 200
                },
                
``` 

### <a name="-missing-signing-certificate"></a><span data-ttu-id="78270-141">*Отсутствует сертификат для подписи</span><span class="sxs-lookup"><span data-stu-id="78270-141">* Missing signing certificate</span></span>

|   |   |  
|---|---|
| <span data-ttu-id="78270-142">Описание ошибки</span><span class="sxs-lookup"><span data-stu-id="78270-142">Error description</span></span>| <span data-ttu-id="78270-143">Hello сертификат подписи не был настроен для стороны AS2.</span><span class="sxs-lookup"><span data-stu-id="78270-143">hello Signing Certificate has not been configured for AS2 party.</span></span> </br> <span data-ttu-id="78270-144">(AS2-From: partner1 AS2-To: partner2)</span><span class="sxs-lookup"><span data-stu-id="78270-144">AS2-From: partner1 AS2-To: partner2</span></span> | 
| <span data-ttu-id="78270-145">Рекомендуемые действия</span><span class="sxs-lookup"><span data-stu-id="78270-145">User action</span></span> | <span data-ttu-id="78270-146">Настройте параметры соглашения AS2 с помощью правильного сертификата для подписи.</span><span class="sxs-lookup"><span data-stu-id="78270-146">Configure AS2 agreement settings with correct certificate for signature</span></span> |
|  |  | 

## <a name="x12-and-edifact"></a><span data-ttu-id="78270-147">X12 и EDIFACT</span><span class="sxs-lookup"><span data-stu-id="78270-147">X12 and EDIFACT</span></span>

### <a name="-leading-or-trailing-space-found"></a><span data-ttu-id="78270-148">*Лишний начальный или конечный пробел</span><span class="sxs-lookup"><span data-stu-id="78270-148">* Leading or trailing space found</span></span>    
    
|   |   | 
|---|---|
| <span data-ttu-id="78270-149">Описание ошибки</span><span class="sxs-lookup"><span data-stu-id="78270-149">Error description</span></span> | <span data-ttu-id="78270-150">Ошибка, обнаруженная во время синтаксического анализа.</span><span class="sxs-lookup"><span data-stu-id="78270-150">Error encountered during parsing.</span></span> <span data-ttu-id="78270-151">Здравствуйте, набор с идентификатором "123456"содержащиеся в сообщении (без группа) с идентификатором "987654" Edifact транзакций, идентификатор отправителя «Partner1», идентификатор получателя «Partner2» приостановке за следующих ошибок: начальные конечные разделители найден</span><span class="sxs-lookup"><span data-stu-id="78270-151">hello Edifact transaction set with id '123456' contained in interchange (without group) with id '987654', with sender id 'Partner1', receiver id 'Partner2' is being suspended with following errors: Leading Trailing separator found</span></span> |
| <span data-ttu-id="78270-152">Рекомендуемые действия</span><span class="sxs-lookup"><span data-stu-id="78270-152">User action</span></span> | <span data-ttu-id="78270-153">Параметры toobe Hello соглашение настроено tooallow начальный и конечный пробелы.</span><span class="sxs-lookup"><span data-stu-id="78270-153">hello agreement settings toobe configured tooallow leading and trailing space.</span></span> </br> <span data-ttu-id="78270-154">Изменение соглашения параметры tooallow начальный и конечный пробелы</span><span class="sxs-lookup"><span data-stu-id="78270-154">Edit agreement settings tooallow leading and trailing space</span></span> |
|   |   |

![Разрешение пробелов](./media/logic-apps-enterprise-integration-b2b-list-errors-solutions/leadingandtrailing.png)

### <a name="-duplicate-check-has-enabled-in-hello-agreement"></a><span data-ttu-id="78270-156">* Проверка включил в соглашении hello</span><span class="sxs-lookup"><span data-stu-id="78270-156">* Duplicate check has enabled in hello agreement</span></span>

|   |   | 
|---|---| 
| <span data-ttu-id="78270-157">Описание ошибки</span><span class="sxs-lookup"><span data-stu-id="78270-157">Error description</span></span> | <span data-ttu-id="78270-158">Повторяющиеся контрольные номера.</span><span class="sxs-lookup"><span data-stu-id="78270-158">Duplicate Control Number</span></span> |
| <span data-ttu-id="78270-159">Рекомендуемые действия</span><span class="sxs-lookup"><span data-stu-id="78270-159">User action</span></span> | <span data-ttu-id="78270-160">Эта ошибка указывает, что сообщение получено hello имеет повторяющихся контрольных чисел.</span><span class="sxs-lookup"><span data-stu-id="78270-160">This error indicates hello received message has duplicate control numbers.</span></span> </br> <span data-ttu-id="78270-161">Исправьте контрольное число hello и повторно отправить сообщение hello</span><span class="sxs-lookup"><span data-stu-id="78270-161">Correct hello control number and resend hello message</span></span> |
|   |   |

### <a name="-missing-schema-in-hello-agreement"></a><span data-ttu-id="78270-162">* Отсутствует схема в соглашении hello</span><span class="sxs-lookup"><span data-stu-id="78270-162">* Missing schema in hello agreement</span></span>

|   |   | 
|---|---| 
| <span data-ttu-id="78270-163">Описание ошибки</span><span class="sxs-lookup"><span data-stu-id="78270-163">Error description</span></span> | <span data-ttu-id="78270-164">Ошибка, обнаруженная во время синтаксического анализа.</span><span class="sxs-lookup"><span data-stu-id="78270-164">Error encountered during parsing.</span></span> <span data-ttu-id="78270-165">набор транзакций Hello X12 с идентификатором "564220001' содержащиеся в функциональной группы с идентификатором '56422', в сообщении с идентификатором"000056422"с идентификатором отправителя 12345678"», идентификатор получателя "87654321" приостановке следующих ошибок «hello сообщение имеет неизвестный документ ty PE и не помогли разрешить tooany hello существующих схем, настроенные в соглашении hello»</span><span class="sxs-lookup"><span data-stu-id="78270-165">hello X12 transaction set with id '564220001' contained in functional group with id '56422', in interchange with id '000056422', with sender id '12345678       ', receiver id '87654321       ' is being suspended with following errors "hello message has an unknown document type and did not resolve tooany of hello existing schemas configured in hello agreement"</span></span> |
| <span data-ttu-id="78270-166">Рекомендуемые действия</span><span class="sxs-lookup"><span data-stu-id="78270-166">User action</span></span> | <span data-ttu-id="78270-167">Настройка схемы в параметры соглашения hello</span><span class="sxs-lookup"><span data-stu-id="78270-167">Configure schema in hello agreement settings</span></span>  |
|   |   |

### <a name="-incorrect-schema-in-hello-agreement"></a><span data-ttu-id="78270-168">* Неправильную схему в соглашении hello</span><span class="sxs-lookup"><span data-stu-id="78270-168">* Incorrect schema in hello agreement</span></span>

|   |   | 
|---|---| 
| <span data-ttu-id="78270-169">Описание ошибки</span><span class="sxs-lookup"><span data-stu-id="78270-169">Error description</span></span> | <span data-ttu-id="78270-170">приветственное сообщение имеет неизвестный тип документа и не помогли разрешить tooany hello существующих схем, настроенные в соглашении hello.</span><span class="sxs-lookup"><span data-stu-id="78270-170">hello message has an unknown document type and did not resolve tooany of hello existing schemas configured in hello agreement.</span></span> |
| <span data-ttu-id="78270-171">Рекомендуемые действия</span><span class="sxs-lookup"><span data-stu-id="78270-171">User action</span></span> | <span data-ttu-id="78270-172">Настроить правильную схему в параметры соглашения hello</span><span class="sxs-lookup"><span data-stu-id="78270-172">Configure correct schema in hello agreement settings</span></span>  |
|   |   |

## <a name="flat-file"></a><span data-ttu-id="78270-173">Неструктурированный файл</span><span class="sxs-lookup"><span data-stu-id="78270-173">Flat file</span></span>

### <a name="-input-message-with-no-body"></a><span data-ttu-id="78270-174">*Входящее сообщение без текста</span><span class="sxs-lookup"><span data-stu-id="78270-174">* Input message with no body</span></span>

|   |   | 
|---|---|
| <span data-ttu-id="78270-175">Описание ошибки</span><span class="sxs-lookup"><span data-stu-id="78270-175">Error description</span></span> | <span data-ttu-id="78270-176">Недопустимый шаблон.</span><span class="sxs-lookup"><span data-stu-id="78270-176">InvalidTemplate.</span></span> <span data-ttu-id="78270-177">Не удается tooprocess выражения языка шаблона в входными параметрами действий «Flat_File_Decoding» в строке "1" и столбце "1902": "требуется свойство «content» ожидает значение но было получено значение null.</span><span class="sxs-lookup"><span data-stu-id="78270-177">Unable tooprocess template language expressions in action 'Flat_File_Decoding' inputs at line '1' and column '1902': 'Required property 'content' expects a value but got null.</span></span> <span data-ttu-id="78270-178">Путь ''.'.</span><span class="sxs-lookup"><span data-stu-id="78270-178">Path ''.'.</span></span> |
| <span data-ttu-id="78270-179">Рекомендуемые действия</span><span class="sxs-lookup"><span data-stu-id="78270-179">User action</span></span> | <span data-ttu-id="78270-180">Эта ошибка указывает, что входящее сообщение hello не содержит текста</span><span class="sxs-lookup"><span data-stu-id="78270-180">This error indicates hello input message does not contain a body</span></span> |
|   |   | 

## <a name="learn-more"></a><span data-ttu-id="78270-181">Подробнее</span><span class="sxs-lookup"><span data-stu-id="78270-181">Learn more</span></span>
[<span data-ttu-id="78270-182">Дополнительные сведения о hello пакет интеграции Enterprise</span><span class="sxs-lookup"><span data-stu-id="78270-182">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md)
