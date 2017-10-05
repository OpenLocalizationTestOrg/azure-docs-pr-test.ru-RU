---
title: "Настраиваемые схемы отслеживания для мониторинга сообщений B2B в Azure Logic Apps | Документация Майкрософт"
description: "Создавайте настраиваемые схемы отслеживания для мониторинга сообщений из транзакций типа \"бизнес — бизнес\" (B2B) в учетной записи интеграции Azure."
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
ms.openlocfilehash: b71a4938dde2a71f1ce29403af7aa9101358d64c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="enable-tracking-to-monitor-your-complete-workflow-end-to-end"></a><span data-ttu-id="43239-103">Включение отслеживания для комплексного мониторинга рабочего процесса</span><span class="sxs-lookup"><span data-stu-id="43239-103">Enable tracking to monitor your complete workflow, end-to-end</span></span>
<span data-ttu-id="43239-104">Доступна встроенная функция отслеживания, которую можно включить для различных частей рабочего процесса B2B, например для отслеживания сообщений AS2 или X12.</span><span class="sxs-lookup"><span data-stu-id="43239-104">There is built-in tracking that you can enable for different parts of your business-to-business workflow, such as tracking AS2 or X12 messages.</span></span> <span data-ttu-id="43239-105">При создании рабочих процессов, содержащих приложение логики, BizTalk Server, SQL Server или любой другой уровень, можно включить настраиваемое отслеживание, которое ведет журнал событий от начала до конца рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="43239-105">When you create workflows that includes a logic app, BizTalk Server, SQL Server, or any other layer, then you can enable custom tracking that logs events from the beginning to the end of your workflow.</span></span> 

<span data-ttu-id="43239-106">В этом разделе приведен настраиваемый код, который можно использовать в уровнях за пределами приложения логики.</span><span class="sxs-lookup"><span data-stu-id="43239-106">This topic provides custom code that you can use in the layers outside of your logic app.</span></span> 

## <a name="custom-tracking-schema"></a><span data-ttu-id="43239-107">Настраиваемая схема отслеживания</span><span class="sxs-lookup"><span data-stu-id="43239-107">Custom tracking schema</span></span>
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

| <span data-ttu-id="43239-108">Свойство</span><span class="sxs-lookup"><span data-stu-id="43239-108">Property</span></span> | <span data-ttu-id="43239-109">Тип</span><span class="sxs-lookup"><span data-stu-id="43239-109">Type</span></span> | <span data-ttu-id="43239-110">Описание</span><span class="sxs-lookup"><span data-stu-id="43239-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="43239-111">sourceType</span><span class="sxs-lookup"><span data-stu-id="43239-111">sourceType</span></span> |   | <span data-ttu-id="43239-112">Тип источника выполнения.</span><span class="sxs-lookup"><span data-stu-id="43239-112">Type of the run source.</span></span> <span data-ttu-id="43239-113">Допустимые значения — **Microsoft.Logic/workflows** или **custom**.</span><span class="sxs-lookup"><span data-stu-id="43239-113">Allowed values are **Microsoft.Logic/workflows** and **custom**.</span></span> <span data-ttu-id="43239-114">(обязательный параметр)</span><span class="sxs-lookup"><span data-stu-id="43239-114">(Mandatory)</span></span> |
| <span data-ttu-id="43239-115">Источник</span><span class="sxs-lookup"><span data-stu-id="43239-115">Source</span></span> |   | <span data-ttu-id="43239-116">Если тип источника — **Microsoft.Logic/workflows**, то сведения источника должны следовать этой схеме.</span><span class="sxs-lookup"><span data-stu-id="43239-116">If the source type is **Microsoft.Logic/workflows**, the source information needs to follow this schema.</span></span> <span data-ttu-id="43239-117">Если тип источника — **custom**, то используется схема JToken.</span><span class="sxs-lookup"><span data-stu-id="43239-117">If the source type is **custom**, the schema is a JToken.</span></span> <span data-ttu-id="43239-118">(обязательный параметр)</span><span class="sxs-lookup"><span data-stu-id="43239-118">(Mandatory)</span></span> |
| <span data-ttu-id="43239-119">systemId</span><span class="sxs-lookup"><span data-stu-id="43239-119">systemId</span></span> | <span data-ttu-id="43239-120">Строка</span><span class="sxs-lookup"><span data-stu-id="43239-120">String</span></span> | <span data-ttu-id="43239-121">Системный идентификатор приложения логики.</span><span class="sxs-lookup"><span data-stu-id="43239-121">Logic app system ID.</span></span> <span data-ttu-id="43239-122">(обязательный параметр)</span><span class="sxs-lookup"><span data-stu-id="43239-122">(Mandatory)</span></span> |
| <span data-ttu-id="43239-123">runId</span><span class="sxs-lookup"><span data-stu-id="43239-123">runId</span></span> | <span data-ttu-id="43239-124">Строка</span><span class="sxs-lookup"><span data-stu-id="43239-124">String</span></span> | <span data-ttu-id="43239-125">Идентификатор выполнения приложения логики.</span><span class="sxs-lookup"><span data-stu-id="43239-125">Logic app run ID.</span></span> <span data-ttu-id="43239-126">(обязательный параметр)</span><span class="sxs-lookup"><span data-stu-id="43239-126">(Mandatory)</span></span> |
| <span data-ttu-id="43239-127">operationName</span><span class="sxs-lookup"><span data-stu-id="43239-127">operationName</span></span> | <span data-ttu-id="43239-128">Строка</span><span class="sxs-lookup"><span data-stu-id="43239-128">String</span></span> | <span data-ttu-id="43239-129">Имя операции (например, действие или триггер).</span><span class="sxs-lookup"><span data-stu-id="43239-129">Name of the operation (for example, action or trigger).</span></span> <span data-ttu-id="43239-130">(обязательный параметр)</span><span class="sxs-lookup"><span data-stu-id="43239-130">(Mandatory)</span></span> |
| <span data-ttu-id="43239-131">repeatItemScopeName</span><span class="sxs-lookup"><span data-stu-id="43239-131">repeatItemScopeName</span></span> | <span data-ttu-id="43239-132">string</span><span class="sxs-lookup"><span data-stu-id="43239-132">String</span></span> | <span data-ttu-id="43239-133">Повторяет имя элемента, если действие находится внутри цикла `foreach`/ или `until`.</span><span class="sxs-lookup"><span data-stu-id="43239-133">Repeat item name if the action is inside a `foreach`/`until` loop.</span></span> <span data-ttu-id="43239-134">(обязательный параметр)</span><span class="sxs-lookup"><span data-stu-id="43239-134">(Mandatory)</span></span> |
| <span data-ttu-id="43239-135">repeatItemIndex</span><span class="sxs-lookup"><span data-stu-id="43239-135">repeatItemIndex</span></span> | <span data-ttu-id="43239-136">Целое число </span><span class="sxs-lookup"><span data-stu-id="43239-136">Integer</span></span> | <span data-ttu-id="43239-137">Определяет, находится ли действие внутри цикла `foreach`/ или `until`.</span><span class="sxs-lookup"><span data-stu-id="43239-137">Whether the action is inside a `foreach`/`until` loop.</span></span> <span data-ttu-id="43239-138">Указывает индекс повторяющегося элемента.</span><span class="sxs-lookup"><span data-stu-id="43239-138">Indicates the repeated item index.</span></span> <span data-ttu-id="43239-139">(обязательный параметр)</span><span class="sxs-lookup"><span data-stu-id="43239-139">(Mandatory)</span></span> |
| <span data-ttu-id="43239-140">trackingId</span><span class="sxs-lookup"><span data-stu-id="43239-140">trackingId</span></span> | <span data-ttu-id="43239-141">Строка</span><span class="sxs-lookup"><span data-stu-id="43239-141">String</span></span> | <span data-ttu-id="43239-142">Идентификатор отслеживания для корреляции сообщений.</span><span class="sxs-lookup"><span data-stu-id="43239-142">Tracking ID, to correlate the messages.</span></span> <span data-ttu-id="43239-143">(необязательный параметр)</span><span class="sxs-lookup"><span data-stu-id="43239-143">(Optional)</span></span> |
| <span data-ttu-id="43239-144">correlationId</span><span class="sxs-lookup"><span data-stu-id="43239-144">correlationId</span></span> | <span data-ttu-id="43239-145">string</span><span class="sxs-lookup"><span data-stu-id="43239-145">String</span></span> | <span data-ttu-id="43239-146">Идентификатор корреляции для корреляции сообщений.</span><span class="sxs-lookup"><span data-stu-id="43239-146">Correlation ID, to correlate the messages.</span></span> <span data-ttu-id="43239-147">(необязательный параметр)</span><span class="sxs-lookup"><span data-stu-id="43239-147">(Optional)</span></span> |
| <span data-ttu-id="43239-148">clientRequestId</span><span class="sxs-lookup"><span data-stu-id="43239-148">clientRequestId</span></span> | <span data-ttu-id="43239-149">Строка</span><span class="sxs-lookup"><span data-stu-id="43239-149">String</span></span> | <span data-ttu-id="43239-150">Клиент может включить его для корреляции сообщений.</span><span class="sxs-lookup"><span data-stu-id="43239-150">Client can populate it to correlate messages.</span></span> <span data-ttu-id="43239-151">(необязательный параметр)</span><span class="sxs-lookup"><span data-stu-id="43239-151">(Optional)</span></span> |
| <span data-ttu-id="43239-152">eventLevel</span><span class="sxs-lookup"><span data-stu-id="43239-152">eventLevel</span></span> |   | <span data-ttu-id="43239-153">Уровень события.</span><span class="sxs-lookup"><span data-stu-id="43239-153">Level of the event.</span></span> <span data-ttu-id="43239-154">(обязательный параметр)</span><span class="sxs-lookup"><span data-stu-id="43239-154">(Mandatory)</span></span> |
| <span data-ttu-id="43239-155">eventTime</span><span class="sxs-lookup"><span data-stu-id="43239-155">eventTime</span></span> |   | <span data-ttu-id="43239-156">Время события в формате UTC (ГГГГ-ММ-ДДTЧЧ:ММ:СС.00000Z).</span><span class="sxs-lookup"><span data-stu-id="43239-156">Time of the event, in UTC format YYYY-MM-DDTHH:MM:SS.00000Z.</span></span> <span data-ttu-id="43239-157">(обязательный параметр)</span><span class="sxs-lookup"><span data-stu-id="43239-157">(Mandatory)</span></span> |
| <span data-ttu-id="43239-158">recordType</span><span class="sxs-lookup"><span data-stu-id="43239-158">recordType</span></span> |   | <span data-ttu-id="43239-159">Тип записи отслеживания.</span><span class="sxs-lookup"><span data-stu-id="43239-159">Type of the track record.</span></span> <span data-ttu-id="43239-160">Допустимое значение — **custom**.</span><span class="sxs-lookup"><span data-stu-id="43239-160">Allowed value is **custom**.</span></span> <span data-ttu-id="43239-161">(обязательный параметр)</span><span class="sxs-lookup"><span data-stu-id="43239-161">(Mandatory)</span></span> |
| <span data-ttu-id="43239-162">record</span><span class="sxs-lookup"><span data-stu-id="43239-162">record</span></span> |   | <span data-ttu-id="43239-163">Настраиваемый тип записи.</span><span class="sxs-lookup"><span data-stu-id="43239-163">Custom record type.</span></span> <span data-ttu-id="43239-164">Разрешен формат JToken.</span><span class="sxs-lookup"><span data-stu-id="43239-164">Allowed format is JToken.</span></span> <span data-ttu-id="43239-165">(обязательный параметр)</span><span class="sxs-lookup"><span data-stu-id="43239-165">(Mandatory)</span></span> |

## <a name="b2b-protocol-tracking-schemas"></a><span data-ttu-id="43239-166">Схемы отслеживания для протоколов B2B</span><span class="sxs-lookup"><span data-stu-id="43239-166">B2B protocol tracking schemas</span></span>
<span data-ttu-id="43239-167">Сведения о схемах отслеживания для протоколов B2B см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="43239-167">For information about B2B protocol tracking schemas, see:</span></span>
* [<span data-ttu-id="43239-168">Схемы отслеживания AS2</span><span class="sxs-lookup"><span data-stu-id="43239-168">AS2 tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)   
* [<span data-ttu-id="43239-169">Схемы отслеживания X12</span><span class="sxs-lookup"><span data-stu-id="43239-169">X12 tracking schemas</span></span>](logic-apps-track-integration-account-x12-tracking-schema.md)

## <a name="next-steps"></a><span data-ttu-id="43239-170">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="43239-170">Next steps</span></span>
* <span data-ttu-id="43239-171">Дополнительные сведения о [мониторинге сообщений B2B](logic-apps-monitor-b2b-message.md).</span><span class="sxs-lookup"><span data-stu-id="43239-171">Learn more about [monitoring B2B messages](logic-apps-monitor-b2b-message.md).</span></span>   
* <span data-ttu-id="43239-172">Дополнительные сведения об [отслеживании сообщений B2B на портале Operations Management Suite](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span><span class="sxs-lookup"><span data-stu-id="43239-172">Learn about [tracking B2B messages in the Operations Management Suite portal](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span></span>
* <span data-ttu-id="43239-173">Дополнительные сведения о [Пакете интеграции Enterprise](../logic-apps/logic-apps-enterprise-integration-overview.md).</span><span class="sxs-lookup"><span data-stu-id="43239-173">Learn more about the [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).</span></span>
