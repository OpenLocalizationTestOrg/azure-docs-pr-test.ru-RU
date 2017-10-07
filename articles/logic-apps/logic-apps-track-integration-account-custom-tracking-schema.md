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
# <a name="enable-tracking-toomonitor-your-complete-workflow-end-to-end"></a><span data-ttu-id="40a5b-103">Включить отслеживание toomonitor завершении рабочего процесса, конца в конец</span><span class="sxs-lookup"><span data-stu-id="40a5b-103">Enable tracking toomonitor your complete workflow, end-to-end</span></span>
<span data-ttu-id="40a5b-104">Доступна встроенная функция отслеживания, которую можно включить для различных частей рабочего процесса B2B, например для отслеживания сообщений AS2 или X12.</span><span class="sxs-lookup"><span data-stu-id="40a5b-104">There is built-in tracking that you can enable for different parts of your business-to-business workflow, such as tracking AS2 or X12 messages.</span></span> <span data-ttu-id="40a5b-105">При создании рабочих процессов, включая приложения логики, BizTalk Server, SQL Server или любой другой слой, можно включить настраиваемое отслеживание, регистрирует события из hello начало toohello конец рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="40a5b-105">When you create workflows that includes a logic app, BizTalk Server, SQL Server, or any other layer, then you can enable custom tracking that logs events from hello beginning toohello end of your workflow.</span></span> 

<span data-ttu-id="40a5b-106">Этот раздел содержит пользовательский код, который можно использовать в слоях hello за пределами логику приложения.</span><span class="sxs-lookup"><span data-stu-id="40a5b-106">This topic provides custom code that you can use in hello layers outside of your logic app.</span></span> 

## <a name="custom-tracking-schema"></a><span data-ttu-id="40a5b-107">Настраиваемая схема отслеживания</span><span class="sxs-lookup"><span data-stu-id="40a5b-107">Custom tracking schema</span></span>
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

| <span data-ttu-id="40a5b-108">Свойство</span><span class="sxs-lookup"><span data-stu-id="40a5b-108">Property</span></span> | <span data-ttu-id="40a5b-109">Тип</span><span class="sxs-lookup"><span data-stu-id="40a5b-109">Type</span></span> | <span data-ttu-id="40a5b-110">Описание</span><span class="sxs-lookup"><span data-stu-id="40a5b-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40a5b-111">sourceType</span><span class="sxs-lookup"><span data-stu-id="40a5b-111">sourceType</span></span> |   | <span data-ttu-id="40a5b-112">Тип запуска hello источника.</span><span class="sxs-lookup"><span data-stu-id="40a5b-112">Type of hello run source.</span></span> <span data-ttu-id="40a5b-113">Допустимые значения — **Microsoft.Logic/workflows** или **custom**.</span><span class="sxs-lookup"><span data-stu-id="40a5b-113">Allowed values are **Microsoft.Logic/workflows** and **custom**.</span></span> <span data-ttu-id="40a5b-114">(обязательный параметр)</span><span class="sxs-lookup"><span data-stu-id="40a5b-114">(Mandatory)</span></span> |
| <span data-ttu-id="40a5b-115">Источник</span><span class="sxs-lookup"><span data-stu-id="40a5b-115">Source</span></span> |   | <span data-ttu-id="40a5b-116">Если тип источника hello **Microsoft.Logic/workflows**, сведения об источнике hello эта схема нужна toofollow.</span><span class="sxs-lookup"><span data-stu-id="40a5b-116">If hello source type is **Microsoft.Logic/workflows**, hello source information needs toofollow this schema.</span></span> <span data-ttu-id="40a5b-117">Если тип источника hello **пользовательские**, схема hello — JToken.</span><span class="sxs-lookup"><span data-stu-id="40a5b-117">If hello source type is **custom**, hello schema is a JToken.</span></span> <span data-ttu-id="40a5b-118">(обязательный параметр)</span><span class="sxs-lookup"><span data-stu-id="40a5b-118">(Mandatory)</span></span> |
| <span data-ttu-id="40a5b-119">systemId</span><span class="sxs-lookup"><span data-stu-id="40a5b-119">systemId</span></span> | <span data-ttu-id="40a5b-120">Строка</span><span class="sxs-lookup"><span data-stu-id="40a5b-120">String</span></span> | <span data-ttu-id="40a5b-121">Системный идентификатор приложения логики.</span><span class="sxs-lookup"><span data-stu-id="40a5b-121">Logic app system ID.</span></span> <span data-ttu-id="40a5b-122">(обязательный параметр)</span><span class="sxs-lookup"><span data-stu-id="40a5b-122">(Mandatory)</span></span> |
| <span data-ttu-id="40a5b-123">runId</span><span class="sxs-lookup"><span data-stu-id="40a5b-123">runId</span></span> | <span data-ttu-id="40a5b-124">Строка</span><span class="sxs-lookup"><span data-stu-id="40a5b-124">String</span></span> | <span data-ttu-id="40a5b-125">Идентификатор выполнения приложения логики.</span><span class="sxs-lookup"><span data-stu-id="40a5b-125">Logic app run ID.</span></span> <span data-ttu-id="40a5b-126">(обязательный параметр)</span><span class="sxs-lookup"><span data-stu-id="40a5b-126">(Mandatory)</span></span> |
| <span data-ttu-id="40a5b-127">operationName</span><span class="sxs-lookup"><span data-stu-id="40a5b-127">operationName</span></span> | <span data-ttu-id="40a5b-128">Строка</span><span class="sxs-lookup"><span data-stu-id="40a5b-128">String</span></span> | <span data-ttu-id="40a5b-129">Имя операции hello (например, действий или триггер).</span><span class="sxs-lookup"><span data-stu-id="40a5b-129">Name of hello operation (for example, action or trigger).</span></span> <span data-ttu-id="40a5b-130">(обязательный параметр)</span><span class="sxs-lookup"><span data-stu-id="40a5b-130">(Mandatory)</span></span> |
| <span data-ttu-id="40a5b-131">repeatItemScopeName</span><span class="sxs-lookup"><span data-stu-id="40a5b-131">repeatItemScopeName</span></span> | <span data-ttu-id="40a5b-132">Строка</span><span class="sxs-lookup"><span data-stu-id="40a5b-132">String</span></span> | <span data-ttu-id="40a5b-133">Повторите имя элемента, если действие hello находится внутри `foreach` / `until` цикла.</span><span class="sxs-lookup"><span data-stu-id="40a5b-133">Repeat item name if hello action is inside a `foreach`/`until` loop.</span></span> <span data-ttu-id="40a5b-134">(обязательный параметр)</span><span class="sxs-lookup"><span data-stu-id="40a5b-134">(Mandatory)</span></span> |
| <span data-ttu-id="40a5b-135">repeatItemIndex</span><span class="sxs-lookup"><span data-stu-id="40a5b-135">repeatItemIndex</span></span> | <span data-ttu-id="40a5b-136">Целое число </span><span class="sxs-lookup"><span data-stu-id="40a5b-136">Integer</span></span> | <span data-ttu-id="40a5b-137">Является ли действие hello внутри `foreach` / `until` цикла.</span><span class="sxs-lookup"><span data-stu-id="40a5b-137">Whether hello action is inside a `foreach`/`until` loop.</span></span> <span data-ttu-id="40a5b-138">Указывает индекс hello повторяющихся элементов.</span><span class="sxs-lookup"><span data-stu-id="40a5b-138">Indicates hello repeated item index.</span></span> <span data-ttu-id="40a5b-139">(обязательный параметр)</span><span class="sxs-lookup"><span data-stu-id="40a5b-139">(Mandatory)</span></span> |
| <span data-ttu-id="40a5b-140">trackingId</span><span class="sxs-lookup"><span data-stu-id="40a5b-140">trackingId</span></span> | <span data-ttu-id="40a5b-141">Строка</span><span class="sxs-lookup"><span data-stu-id="40a5b-141">String</span></span> | <span data-ttu-id="40a5b-142">Идентификатор отслеживания сообщений hello toocorrelate.</span><span class="sxs-lookup"><span data-stu-id="40a5b-142">Tracking ID, toocorrelate hello messages.</span></span> <span data-ttu-id="40a5b-143">(необязательный параметр)</span><span class="sxs-lookup"><span data-stu-id="40a5b-143">(Optional)</span></span> |
| <span data-ttu-id="40a5b-144">correlationId</span><span class="sxs-lookup"><span data-stu-id="40a5b-144">correlationId</span></span> | <span data-ttu-id="40a5b-145">Строка</span><span class="sxs-lookup"><span data-stu-id="40a5b-145">String</span></span> | <span data-ttu-id="40a5b-146">Идентификатор корреляции сообщений hello toocorrelate.</span><span class="sxs-lookup"><span data-stu-id="40a5b-146">Correlation ID, toocorrelate hello messages.</span></span> <span data-ttu-id="40a5b-147">(необязательный параметр)</span><span class="sxs-lookup"><span data-stu-id="40a5b-147">(Optional)</span></span> |
| <span data-ttu-id="40a5b-148">clientRequestId</span><span class="sxs-lookup"><span data-stu-id="40a5b-148">clientRequestId</span></span> | <span data-ttu-id="40a5b-149">Строка</span><span class="sxs-lookup"><span data-stu-id="40a5b-149">String</span></span> | <span data-ttu-id="40a5b-150">Клиент может заполнить его toocorrelate сообщения.</span><span class="sxs-lookup"><span data-stu-id="40a5b-150">Client can populate it toocorrelate messages.</span></span> <span data-ttu-id="40a5b-151">(необязательный параметр)</span><span class="sxs-lookup"><span data-stu-id="40a5b-151">(Optional)</span></span> |
| <span data-ttu-id="40a5b-152">eventLevel</span><span class="sxs-lookup"><span data-stu-id="40a5b-152">eventLevel</span></span> |   | <span data-ttu-id="40a5b-153">Уровень события hello.</span><span class="sxs-lookup"><span data-stu-id="40a5b-153">Level of hello event.</span></span> <span data-ttu-id="40a5b-154">(обязательный параметр)</span><span class="sxs-lookup"><span data-stu-id="40a5b-154">(Mandatory)</span></span> |
| <span data-ttu-id="40a5b-155">eventTime</span><span class="sxs-lookup"><span data-stu-id="40a5b-155">eventTime</span></span> |   | <span data-ttu-id="40a5b-156">Время события hello в формате UTC, гггг-мм-DDTHH:MM:SS.00000Z.</span><span class="sxs-lookup"><span data-stu-id="40a5b-156">Time of hello event, in UTC format YYYY-MM-DDTHH:MM:SS.00000Z.</span></span> <span data-ttu-id="40a5b-157">(обязательный параметр)</span><span class="sxs-lookup"><span data-stu-id="40a5b-157">(Mandatory)</span></span> |
| <span data-ttu-id="40a5b-158">recordType</span><span class="sxs-lookup"><span data-stu-id="40a5b-158">recordType</span></span> |   | <span data-ttu-id="40a5b-159">Тип записи отслеживания hello.</span><span class="sxs-lookup"><span data-stu-id="40a5b-159">Type of hello track record.</span></span> <span data-ttu-id="40a5b-160">Допустимое значение — **custom**.</span><span class="sxs-lookup"><span data-stu-id="40a5b-160">Allowed value is **custom**.</span></span> <span data-ttu-id="40a5b-161">(обязательный параметр)</span><span class="sxs-lookup"><span data-stu-id="40a5b-161">(Mandatory)</span></span> |
| <span data-ttu-id="40a5b-162">record</span><span class="sxs-lookup"><span data-stu-id="40a5b-162">record</span></span> |   | <span data-ttu-id="40a5b-163">Настраиваемый тип записи.</span><span class="sxs-lookup"><span data-stu-id="40a5b-163">Custom record type.</span></span> <span data-ttu-id="40a5b-164">Разрешен формат JToken.</span><span class="sxs-lookup"><span data-stu-id="40a5b-164">Allowed format is JToken.</span></span> <span data-ttu-id="40a5b-165">(обязательный параметр)</span><span class="sxs-lookup"><span data-stu-id="40a5b-165">(Mandatory)</span></span> |

## <a name="b2b-protocol-tracking-schemas"></a><span data-ttu-id="40a5b-166">Схемы отслеживания для протоколов B2B</span><span class="sxs-lookup"><span data-stu-id="40a5b-166">B2B protocol tracking schemas</span></span>
<span data-ttu-id="40a5b-167">Сведения о схемах отслеживания для протоколов B2B см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="40a5b-167">For information about B2B protocol tracking schemas, see:</span></span>
* [<span data-ttu-id="40a5b-168">Схемы отслеживания AS2</span><span class="sxs-lookup"><span data-stu-id="40a5b-168">AS2 tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)   
* [<span data-ttu-id="40a5b-169">Схемы отслеживания X12</span><span class="sxs-lookup"><span data-stu-id="40a5b-169">X12 tracking schemas</span></span>](logic-apps-track-integration-account-x12-tracking-schema.md)

## <a name="next-steps"></a><span data-ttu-id="40a5b-170">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="40a5b-170">Next steps</span></span>
* <span data-ttu-id="40a5b-171">Дополнительные сведения о [мониторинге сообщений B2B](logic-apps-monitor-b2b-message.md).</span><span class="sxs-lookup"><span data-stu-id="40a5b-171">Learn more about [monitoring B2B messages](logic-apps-monitor-b2b-message.md).</span></span>   
* <span data-ttu-id="40a5b-172">Дополнительные сведения о [отслеживание сообщений B2B на портале Operations Management Suite hello](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span><span class="sxs-lookup"><span data-stu-id="40a5b-172">Learn about [tracking B2B messages in hello Operations Management Suite portal](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span></span>
* <span data-ttu-id="40a5b-173">Дополнительные сведения о hello [пакет интеграции Enterprise](../logic-apps/logic-apps-enterprise-integration-overview.md).</span><span class="sxs-lookup"><span data-stu-id="40a5b-173">Learn more about hello [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).</span></span>
