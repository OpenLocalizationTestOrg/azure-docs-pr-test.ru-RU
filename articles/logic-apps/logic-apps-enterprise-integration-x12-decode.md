---
title: "сообщения об изменении aaaDecode X12 - приложения логики Azure | Документы Microsoft"
description: "Проверка EDI и создания подтверждений с декодером сообщение hello X12 в hello пакет интеграции Enterprise для логики приложений Azure"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 4fd48d2d-2008-4080-b6a1-8ae183b48131
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 1ffececca1ff835b319b64c85f86c421395833c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="decode-x12-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a><span data-ttu-id="2edcd-103">Декодирование X12 сообщений для приложения логики Azure с hello пакет интеграции Enterprise</span><span class="sxs-lookup"><span data-stu-id="2edcd-103">Decode X12 messages for Azure Logic Apps with hello Enterprise Integration Pack</span></span>

<span data-ttu-id="2edcd-104">С соединителем сообщение декодирования X12 hello можно проверить конверт hello от соглашения с торговым партнером, проверки EDI и свойств, разделить операции обмена на наборы транзакций или сохранения всей операции обмена и создать подтверждения для транзакций, проведенных.</span><span class="sxs-lookup"><span data-stu-id="2edcd-104">With hello Decode X12 message connector, you can validate hello envelope against a trading partner agreement, validate EDI and partner-specific properties, split interchanges into transactions sets or preserve entire interchanges, and generate acknowledgments for processed transactions.</span></span> <span data-ttu-id="2edcd-105">toouse этот соединитель, необходимо добавить существующий триггер в приложении логику tooan соединитель hello.</span><span class="sxs-lookup"><span data-stu-id="2edcd-105">toouse this connector, you must add hello connector tooan existing trigger in your logic app.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="2edcd-106">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="2edcd-106">Before you start</span></span>

<span data-ttu-id="2edcd-107">Вот hello необходимых элементов.</span><span class="sxs-lookup"><span data-stu-id="2edcd-107">Here's hello items you need:</span></span>

* <span data-ttu-id="2edcd-108">Учетная запись Azure. Вы можете создать [бесплатную учетную запись](https://azure.microsoft.com/free).</span><span class="sxs-lookup"><span data-stu-id="2edcd-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="2edcd-109">[Учетная запись интеграции](logic-apps-enterprise-integration-create-integration-account.md), уже определенная и связанная с подпиской Azure.</span><span class="sxs-lookup"><span data-stu-id="2edcd-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="2edcd-110">Необходимо иметь соединителя интеграции декодирования X12 hello учетной записи toouse сообщения.</span><span class="sxs-lookup"><span data-stu-id="2edcd-110">You must have an integration account toouse hello Decode X12 message connector.</span></span>
* <span data-ttu-id="2edcd-111">В учетной записи интеграции должны быть определены по крайней мере два [партнера](logic-apps-enterprise-integration-partners.md).</span><span class="sxs-lookup"><span data-stu-id="2edcd-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="2edcd-112">В учетной записи интеграции должно быть определено [соглашение X12](logic-apps-enterprise-integration-x12.md).</span><span class="sxs-lookup"><span data-stu-id="2edcd-112">An [X12 agreement](logic-apps-enterprise-integration-x12.md) that's already defined in your integration account</span></span>

## <a name="decode-x12-messages"></a><span data-ttu-id="2edcd-113">Декодирование сообщений X12</span><span class="sxs-lookup"><span data-stu-id="2edcd-113">Decode X12 messages</span></span>

1. <span data-ttu-id="2edcd-114">[Создание приложения логики](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="2edcd-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="2edcd-115">Соединитель сообщения Hello декодирования X12 нет триггеры, поэтому необходимо добавить триггер для запуска приложения логики, как триггер запроса.</span><span class="sxs-lookup"><span data-stu-id="2edcd-115">hello Decode X12 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="2edcd-116">В hello конструктор логики приложения добавить триггер и добавьте действие tooyour логику приложения.</span><span class="sxs-lookup"><span data-stu-id="2edcd-116">In hello Logic App Designer, add a trigger, and then add an action tooyour logic app.</span></span>

3.  <span data-ttu-id="2edcd-117">В поле поиска hello введите «x12» для фильтра.</span><span class="sxs-lookup"><span data-stu-id="2edcd-117">In hello search box, enter "x12" for your filter.</span></span> <span data-ttu-id="2edcd-118">Выберите **X12 - Decode X12 message** (X12 — декодировать сообщение X12).</span><span class="sxs-lookup"><span data-stu-id="2edcd-118">Select **X12 - Decode X12 message**.</span></span>
   
    ![Поиск по запросу "x12"](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage1.png)  

3. <span data-ttu-id="2edcd-120">Если вы еще не создана ранее все подключения учетной записи интеграции tooyour, появится предложение toocreate теперь это подключение.</span><span class="sxs-lookup"><span data-stu-id="2edcd-120">If you didn't previously create any connections tooyour integration account, you're prompted toocreate that connection now.</span></span> <span data-ttu-id="2edcd-121">Имя подключения и установите hello интеграции учетной записью, которую tooconnect.</span><span class="sxs-lookup"><span data-stu-id="2edcd-121">Name your connection, and select hello integration account that you want tooconnect.</span></span> 

    ![Указание сведений о подключении к учетной записи интеграции](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage4.png)

    <span data-ttu-id="2edcd-123">Свойства со звездочкой обязательные.</span><span class="sxs-lookup"><span data-stu-id="2edcd-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="2edcd-124">Свойство</span><span class="sxs-lookup"><span data-stu-id="2edcd-124">Property</span></span> | <span data-ttu-id="2edcd-125">Сведения</span><span class="sxs-lookup"><span data-stu-id="2edcd-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="2edcd-126">Имя подключения*</span><span class="sxs-lookup"><span data-stu-id="2edcd-126">Connection Name *</span></span> |<span data-ttu-id="2edcd-127">Введите имя подключения</span><span class="sxs-lookup"><span data-stu-id="2edcd-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="2edcd-128">Учетная запись интеграции*</span><span class="sxs-lookup"><span data-stu-id="2edcd-128">Integration Account *</span></span> |<span data-ttu-id="2edcd-129">Выберите имя для учетной записи интеграции.</span><span class="sxs-lookup"><span data-stu-id="2edcd-129">Enter a name for your integration account.</span></span> <span data-ttu-id="2edcd-130">Обеспечить наличие учетной записи и логика приложения интеграции в hello Azure местоположения.</span><span class="sxs-lookup"><span data-stu-id="2edcd-130">Make sure that your integration account and logic app are in hello same Azure location.</span></span> |

5.  <span data-ttu-id="2edcd-131">После завершения, сведения о соединении с вашей должен выглядеть аналогичный пример toothis.</span><span class="sxs-lookup"><span data-stu-id="2edcd-131">When you're done, your connection details should look similar toothis example.</span></span> <span data-ttu-id="2edcd-132">toofinish при создании подключения, выберите **создать**.</span><span class="sxs-lookup"><span data-stu-id="2edcd-132">toofinish creating your connection, choose **Create**.</span></span>
   
    ![сведения о подключении к учетной записи интеграции](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage5.png) 

6. <span data-ttu-id="2edcd-134">После создания подключения, как показано в следующем примере, выберите toodecode сообщение hello X12 неструктурированного файла.</span><span class="sxs-lookup"><span data-stu-id="2edcd-134">After your connection is created, as shown in this example, select hello X12 flat file message toodecode.</span></span>

    ![создано подключение к учетной записи интеграции](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage6.png) 

    <span data-ttu-id="2edcd-136">Например:</span><span class="sxs-lookup"><span data-stu-id="2edcd-136">For example:</span></span>

    ![Выбор неструктурированного файла сообщения X12 для декодирования](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage7.png) 

## <a name="x12-decode-details"></a><span data-ttu-id="2edcd-138">Сведения о декодировании X12</span><span class="sxs-lookup"><span data-stu-id="2edcd-138">X12 Decode details</span></span>

<span data-ttu-id="2edcd-139">Соединитель декодирования Hello X12 выполняет следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="2edcd-139">hello X12 Decode connector performs these tasks:</span></span>

* <span data-ttu-id="2edcd-140">Проверяет конверт hello от соглашение торговых партнеров</span><span class="sxs-lookup"><span data-stu-id="2edcd-140">Validates hello envelope against trading partner agreement</span></span>
* <span data-ttu-id="2edcd-141">Проверяет EDI и свойства для конкретного партнера.</span><span class="sxs-lookup"><span data-stu-id="2edcd-141">Validates EDI and partner-specific properties</span></span>
  * <span data-ttu-id="2edcd-142">Проводит структурную проверку EDI и расширенную проверку схемы.</span><span class="sxs-lookup"><span data-stu-id="2edcd-142">EDI structural validation, and extended schema validation</span></span>
  * <span data-ttu-id="2edcd-143">Проверка структуры hello конверта сообщения hello.</span><span class="sxs-lookup"><span data-stu-id="2edcd-143">Validation of hello structure of hello interchange envelope.</span></span>
  * <span data-ttu-id="2edcd-144">Проверка схемы конверта hello по схеме управления hello.</span><span class="sxs-lookup"><span data-stu-id="2edcd-144">Schema validation of hello envelope against hello control schema.</span></span>
  * <span data-ttu-id="2edcd-145">Проверка схемы элементов данных набора транзакций hello по схеме сообщение hello.</span><span class="sxs-lookup"><span data-stu-id="2edcd-145">Schema validation of hello transaction-set data elements against hello message schema.</span></span>
  * <span data-ttu-id="2edcd-146">Проверяет EDI для элементов данных в наборе транзакций.</span><span class="sxs-lookup"><span data-stu-id="2edcd-146">EDI validation performed on transaction-set data elements</span></span> 
* <span data-ttu-id="2edcd-147">Проверяет, что hello обмена, группы и транзакции номеров управления набором не являются дубликатами</span><span class="sxs-lookup"><span data-stu-id="2edcd-147">Verifies that hello interchange, group, and transaction set control numbers are not duplicates</span></span>
  * <span data-ttu-id="2edcd-148">Проверяет hello контрольного числа сообщения от полученных ранее сообщений.</span><span class="sxs-lookup"><span data-stu-id="2edcd-148">Checks hello interchange control number against previously received interchanges.</span></span>
  * <span data-ttu-id="2edcd-149">Проверяет hello контрольного числа группы от других контрольными числами групп в сообщении hello.</span><span class="sxs-lookup"><span data-stu-id="2edcd-149">Checks hello group control number against other group control numbers in hello interchange.</span></span>
  * <span data-ttu-id="2edcd-150">Проверяет, что номер управления набором транзакций hello от других номеров управления набором транзакций в этой группе.</span><span class="sxs-lookup"><span data-stu-id="2edcd-150">Checks hello transaction set control number against other transaction set control numbers in that group.</span></span>
* <span data-ttu-id="2edcd-151">Разделяет hello обмена на наборы транзакций или сохраняет всего сообщения hello:</span><span class="sxs-lookup"><span data-stu-id="2edcd-151">Splits hello interchange into transaction sets, or preserves hello entire interchange:</span></span>
  * <span data-ttu-id="2edcd-152">Разделение обмена на наборы транзакций — блокировка наборов транзакций при ошибке: разделяет обмен на наборы транзакций и анализирует каждый из них.</span><span class="sxs-lookup"><span data-stu-id="2edcd-152">Split Interchange as transaction sets - suspend transaction sets on error: Splits interchange into transaction sets and parses each transaction set.</span></span> 
  <span data-ttu-id="2edcd-153">Действие Hello X12 декодирования выводит только этих наборов, не прошедшие проверку слишком`badMessages`и выводит hello оставшиеся транзакции задает слишком`goodMessages`.</span><span class="sxs-lookup"><span data-stu-id="2edcd-153">hello X12 Decode action outputs only those transaction sets that fail validation too`badMessages`, and outputs hello remaining transactions sets too`goodMessages`.</span></span>
  * <span data-ttu-id="2edcd-154">Разделение обмена на наборы транзакций — блокировка обмена при ошибке: разделяет обмен на наборы транзакций и анализирует каждый из них.</span><span class="sxs-lookup"><span data-stu-id="2edcd-154">Split Interchange as transaction sets - suspend interchange on error: Splits interchange into transaction sets and parses each transaction set.</span></span> 
  <span data-ttu-id="2edcd-155">Если один или несколько наборов транзакций hello обмена сбой проверки, действие hello X12 декодирования выводит все транзакции hello задает в этом сообщении слишком`badMessages`.</span><span class="sxs-lookup"><span data-stu-id="2edcd-155">If one or more transaction sets in hello interchange fail validation, hello X12 Decode action outputs all hello transaction sets in that interchange too`badMessages`.</span></span>
  * <span data-ttu-id="2edcd-156">Сохранить обмен — приостанавливать обработку наборов транзакций при ошибке: сообщение hello Preserve и процесс hello всего пакетного сообщения.</span><span class="sxs-lookup"><span data-stu-id="2edcd-156">Preserve Interchange - suspend transaction sets on error: Preserve hello interchange and process hello entire batched interchange.</span></span> 
  <span data-ttu-id="2edcd-157">Действие Hello X12 декодирования выводит только этих наборов, не прошедшие проверку слишком`badMessages`и выводит hello оставшиеся транзакции задает слишком`goodMessages`.</span><span class="sxs-lookup"><span data-stu-id="2edcd-157">hello X12 Decode action outputs only those transaction sets that fail validation too`badMessages`, and outputs hello remaining transactions sets too`goodMessages`.</span></span>
  * <span data-ttu-id="2edcd-158">Сохранить обмен — приостанавливать обработку сообщения об ошибке: сообщение hello Preserve и процесс hello всего пакетного сообщения.</span><span class="sxs-lookup"><span data-stu-id="2edcd-158">Preserve Interchange - suspend interchange on error: Preserve hello interchange and process hello entire batched interchange.</span></span> 
  <span data-ttu-id="2edcd-159">Если один или несколько наборов транзакций hello обмена сбой проверки, действие hello X12 декодирования выводит все транзакции hello задает в этом сообщении слишком`badMessages`.</span><span class="sxs-lookup"><span data-stu-id="2edcd-159">If one or more transaction sets in hello interchange fail validation, hello X12 Decode action outputs all hello transaction sets in that interchange too`badMessages`.</span></span> 
* <span data-ttu-id="2edcd-160">Генерирует техническое и (или) функциональное подтверждение (если настроено).</span><span class="sxs-lookup"><span data-stu-id="2edcd-160">Generates a Technical and/or Functional acknowledgment (if configured).</span></span>
  * <span data-ttu-id="2edcd-161">Техническое подтверждение создается по результатам проверки заголовков.</span><span class="sxs-lookup"><span data-stu-id="2edcd-161">A Technical Acknowledgment generates as a result of header validation.</span></span> <span data-ttu-id="2edcd-162">Техническое подтверждение Hello сообщает состояние hello hello обработки заголовка обмена и трейлер получатель адрес hello.</span><span class="sxs-lookup"><span data-stu-id="2edcd-162">hello technical acknowledgment reports hello status of hello processing of an interchange header and trailer by hello address receiver.</span></span>
  * <span data-ttu-id="2edcd-163">Функциональное подтверждение создается по результатам проверки тела сообщения.</span><span class="sxs-lookup"><span data-stu-id="2edcd-163">A Functional Acknowledgment generates as a result of body validation.</span></span> <span data-ttu-id="2edcd-164">Hello функциональное подтверждение сообщает каждая ошибка возникла при обработке hello получил документ</span><span class="sxs-lookup"><span data-stu-id="2edcd-164">hello functional acknowledgment reports each error encountered while processing hello received document</span></span>

## <a name="view-hello-swagger"></a><span data-ttu-id="2edcd-165">Представление hello swagger</span><span class="sxs-lookup"><span data-stu-id="2edcd-165">View hello swagger</span></span>
<span data-ttu-id="2edcd-166">В разделе hello [swagger сведения](/connectors/x12/).</span><span class="sxs-lookup"><span data-stu-id="2edcd-166">See hello [swagger details](/connectors/x12/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="2edcd-167">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2edcd-167">Next steps</span></span>
[<span data-ttu-id="2edcd-168">Дополнительные сведения о hello пакет интеграции Enterprise</span><span class="sxs-lookup"><span data-stu-id="2edcd-168">Learn more about hello Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "Дополнительные сведения о пакет интеграции Enterprise") 

