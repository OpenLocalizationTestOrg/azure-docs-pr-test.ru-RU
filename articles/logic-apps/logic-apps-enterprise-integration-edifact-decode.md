---
title: "сообщения EDIFACT aaaDecode - приложения логики Azure | Документы Microsoft"
description: "Проверка EDI и создания подтверждений с декодером сообщение hello EDIFACT в hello пакет интеграции Enterprise для логики приложений Azure"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 0e61501d-21a2-4419-8c6c-88724d346e81
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 94faebdec4e4ffc8ad76ad1609495ddf9f002250
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="decode-edifact-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a><span data-ttu-id="9c346-103">Декодирование сообщения EDIFACT для приложения логики Azure с hello пакет интеграции Enterprise</span><span class="sxs-lookup"><span data-stu-id="9c346-103">Decode EDIFACT messages for Azure Logic Apps with hello Enterprise Integration Pack</span></span>

<span data-ttu-id="9c346-104">Соединитель сообщения EDIFACT декодировать hello можно проверки EDI и свойств, разделить операции обмена на наборы транзакций или сохранения всей операции обмена и создание подтверждений для обработанных транзакций.</span><span class="sxs-lookup"><span data-stu-id="9c346-104">With hello Decode EDIFACT message connector, you can validate EDI and partner-specific properties, split interchanges into transactions sets or preserve entire interchanges, and generate acknowledgments for processed transactions.</span></span> <span data-ttu-id="9c346-105">toouse этот соединитель, необходимо добавить существующий триггер в приложении логику tooan соединитель hello.</span><span class="sxs-lookup"><span data-stu-id="9c346-105">toouse this connector, you must add hello connector tooan existing trigger in your logic app.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="9c346-106">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="9c346-106">Before you start</span></span>

<span data-ttu-id="9c346-107">Вот hello необходимых элементов.</span><span class="sxs-lookup"><span data-stu-id="9c346-107">Here's hello items you need:</span></span>

* <span data-ttu-id="9c346-108">Учетная запись Azure. Вы можете создать [бесплатную учетную запись](https://azure.microsoft.com/free).</span><span class="sxs-lookup"><span data-stu-id="9c346-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="9c346-109">[Учетная запись интеграции](logic-apps-enterprise-integration-create-integration-account.md), уже определенная и связанная с подпиской Azure.</span><span class="sxs-lookup"><span data-stu-id="9c346-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="9c346-110">Необходимо иметь соединителя интеграции декодировать EDIFACT hello учетной записи toouse сообщения.</span><span class="sxs-lookup"><span data-stu-id="9c346-110">You must have an integration account toouse hello Decode EDIFACT message connector.</span></span> 
* <span data-ttu-id="9c346-111">В учетной записи интеграции должны быть определены по крайней мере два [партнера](logic-apps-enterprise-integration-partners.md).</span><span class="sxs-lookup"><span data-stu-id="9c346-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="9c346-112">В учетной записи интеграции должно быть определено [соглашение EDIFACT](logic-apps-enterprise-integration-edifact.md).</span><span class="sxs-lookup"><span data-stu-id="9c346-112">An [EDIFACT agreement](logic-apps-enterprise-integration-edifact.md) that's already defined in your integration account</span></span>

## <a name="decode-edifact-messages"></a><span data-ttu-id="9c346-113">Декодирование сообщений EDIFACT</span><span class="sxs-lookup"><span data-stu-id="9c346-113">Decode EDIFACT messages</span></span>

1. <span data-ttu-id="9c346-114">[Создание приложения логики](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="9c346-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="9c346-115">Соединитель сообщения EDIFACT декодировать Hello не имеет триггеры, поэтому ее нужно добавить триггер для запуска приложения логики, как триггер запроса.</span><span class="sxs-lookup"><span data-stu-id="9c346-115">hello Decode EDIFACT message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="9c346-116">В hello конструктор логики приложения добавить триггер и добавьте действие tooyour логику приложения.</span><span class="sxs-lookup"><span data-stu-id="9c346-116">In hello Logic App Designer, add a trigger, and then add an action tooyour logic app.</span></span>

3. <span data-ttu-id="9c346-117">В поле поиска hello введите «EDIFACT» фильтра.</span><span class="sxs-lookup"><span data-stu-id="9c346-117">In hello search box, enter "EDIFACT" as your filter.</span></span> <span data-ttu-id="9c346-118">Выберите**Decode EDIFACT Message** (Декодировать сообщение EDIFACT).</span><span class="sxs-lookup"><span data-stu-id="9c346-118">Select **Decode EDIFACT Message**.</span></span>
   
    ![поиск EDIFACT](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage1.png)

3. <span data-ttu-id="9c346-120">Если вы еще не создана ранее все подключения учетной записи интеграции tooyour, появится предложение toocreate теперь это подключение.</span><span class="sxs-lookup"><span data-stu-id="9c346-120">If you didn't previously create any connections tooyour integration account, you're prompted toocreate that connection now.</span></span> <span data-ttu-id="9c346-121">Имя подключения и установите hello интеграции учетной записью, которую tooconnect.</span><span class="sxs-lookup"><span data-stu-id="9c346-121">Name your connection, and select hello integration account that you want tooconnect.</span></span>
   
    ![Создание учетной записи интеграции](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage2.png)

    <span data-ttu-id="9c346-123">Свойства со звездочкой обязательные.</span><span class="sxs-lookup"><span data-stu-id="9c346-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="9c346-124">Свойство</span><span class="sxs-lookup"><span data-stu-id="9c346-124">Property</span></span> | <span data-ttu-id="9c346-125">Сведения</span><span class="sxs-lookup"><span data-stu-id="9c346-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="9c346-126">Имя подключения*</span><span class="sxs-lookup"><span data-stu-id="9c346-126">Connection Name *</span></span> |<span data-ttu-id="9c346-127">Введите имя подключения</span><span class="sxs-lookup"><span data-stu-id="9c346-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="9c346-128">Учетная запись интеграции*</span><span class="sxs-lookup"><span data-stu-id="9c346-128">Integration Account *</span></span> |<span data-ttu-id="9c346-129">Выберите имя для учетной записи интеграции.</span><span class="sxs-lookup"><span data-stu-id="9c346-129">Enter a name for your integration account.</span></span> <span data-ttu-id="9c346-130">Обеспечить наличие учетной записи и логика приложения интеграции в hello Azure местоположения.</span><span class="sxs-lookup"><span data-stu-id="9c346-130">Make sure that your integration account and logic app are in hello same Azure location.</span></span> |

4. <span data-ttu-id="9c346-131">После завершения toofinish при создании подключения, выберите **создать**.</span><span class="sxs-lookup"><span data-stu-id="9c346-131">When you're done toofinish creating your connection, choose **Create**.</span></span> <span data-ttu-id="9c346-132">Сведения о соединении с вашей должен выглядеть аналогичный пример toothis:</span><span class="sxs-lookup"><span data-stu-id="9c346-132">Your connection details should look similar toothis example:</span></span>

    ![Данные учетной записи интеграции](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage3.png)  

5. <span data-ttu-id="9c346-134">После создания подключения, как показано в следующем примере, выберите toodecode сообщение неструктурированного файла EDIFACT hello.</span><span class="sxs-lookup"><span data-stu-id="9c346-134">After your connection is created, as shown in this example, select hello EDIFACT flat file message toodecode.</span></span>

    ![создано подключение к учетной записи интеграции](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage4.png)  

    <span data-ttu-id="9c346-136">Например:</span><span class="sxs-lookup"><span data-stu-id="9c346-136">For example:</span></span>

    ![Выбор неструктурированного файла сообщения EDIFACT для декодирования](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage5.png)  

## <a name="edifact-decoder-details"></a><span data-ttu-id="9c346-138">Сведения о декодере EDIFACT</span><span class="sxs-lookup"><span data-stu-id="9c346-138">EDIFACT decoder details</span></span>

<span data-ttu-id="9c346-139">Соединитель декодировать EDIFACT Hello выполняет следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="9c346-139">hello Decode EDIFACT connector performs these tasks:</span></span> 

* <span data-ttu-id="9c346-140">Проверяет конверт hello от соглашение торговых партнеров.</span><span class="sxs-lookup"><span data-stu-id="9c346-140">Validates hello envelope against trading partner agreement.</span></span>
* <span data-ttu-id="9c346-141">Разрешает hello соглашения, сопоставляя квалификатор отправителя hello и идентификатор и квалификатор получателя и идентификатор.</span><span class="sxs-lookup"><span data-stu-id="9c346-141">Resolves hello agreement by matching hello sender qualifier & identifier and receiver qualifier & identifier.</span></span>
* <span data-ttu-id="9c346-142">Разделяет сообщении в нескольких транзакциях, когда обмена hello имеет более чем одной транзакцией, на основе соглашения hello получения параметров конфигурации.</span><span class="sxs-lookup"><span data-stu-id="9c346-142">Splits an interchange into multiple transactions when hello interchange has more than one transaction based on hello agreement's receive settings configuration.</span></span>
* <span data-ttu-id="9c346-143">Дизассемблирует сообщение hello.</span><span class="sxs-lookup"><span data-stu-id="9c346-143">Disassembles hello interchange.</span></span>
* <span data-ttu-id="9c346-144">Проверяет EDI и свойства партнера, включая следующие проверки:</span><span class="sxs-lookup"><span data-stu-id="9c346-144">Validates EDI and partner-specific properties including:</span></span>
  * <span data-ttu-id="9c346-145">Проверка структуры конверта сообщения hello</span><span class="sxs-lookup"><span data-stu-id="9c346-145">Validation of hello interchange envelope structure</span></span>
  * <span data-ttu-id="9c346-146">Проверка схемы конверта hello по схеме управления hello</span><span class="sxs-lookup"><span data-stu-id="9c346-146">Schema validation of hello envelope against hello control schema</span></span>
  * <span data-ttu-id="9c346-147">Проверка схемы элементов данных набора транзакций hello по схеме сообщение hello</span><span class="sxs-lookup"><span data-stu-id="9c346-147">Schema validation of hello transaction-set data elements against hello message schema</span></span>
  * <span data-ttu-id="9c346-148">Проверяет EDI для элементов данных в наборе транзакций.</span><span class="sxs-lookup"><span data-stu-id="9c346-148">EDI validation performed on transaction-set data elements</span></span>
* <span data-ttu-id="9c346-149">Проверяет то, что hello обмена, группы и транзакции номеров управления набором повторяющиеся значения (если настроено)</span><span class="sxs-lookup"><span data-stu-id="9c346-149">Verifies that hello interchange, group, and transaction set control numbers are not duplicates (if configured)</span></span> 
  * <span data-ttu-id="9c346-150">Проверяет hello контрольного числа сообщения от полученных ранее сообщений.</span><span class="sxs-lookup"><span data-stu-id="9c346-150">Checks hello interchange control number against previously received interchanges.</span></span> 
  * <span data-ttu-id="9c346-151">Проверяет hello контрольного числа группы от других контрольными числами групп в сообщении hello.</span><span class="sxs-lookup"><span data-stu-id="9c346-151">Checks hello group control number against other group control numbers in hello interchange.</span></span> 
  * <span data-ttu-id="9c346-152">Проверяет, что номер управления набором транзакций hello от других номеров управления набором транзакций в этой группе.</span><span class="sxs-lookup"><span data-stu-id="9c346-152">Checks hello transaction set control number against other transaction set control numbers in that group.</span></span>
* <span data-ttu-id="9c346-153">Разделяет hello обмена на наборы транзакций или сохраняет всего сообщения hello:</span><span class="sxs-lookup"><span data-stu-id="9c346-153">Splits hello interchange into transaction sets, or preserves hello entire interchange:</span></span>
  * <span data-ttu-id="9c346-154">Разделение обмена на наборы транзакций — блокировка наборов транзакций при ошибке: разделяет обмен на наборы транзакций и анализирует каждый из них.</span><span class="sxs-lookup"><span data-stu-id="9c346-154">Split Interchange as transaction sets - suspend transaction sets on error: Splits interchange into transaction sets and parses each transaction set.</span></span> 
  <span data-ttu-id="9c346-155">Действие Hello X12 декодирования выводит только этих наборов, не прошедшие проверку слишком`badMessages`и выводит hello оставшиеся транзакции задает слишком`goodMessages`.</span><span class="sxs-lookup"><span data-stu-id="9c346-155">hello X12 Decode action outputs only those transaction sets that fail validation too`badMessages`, and outputs hello remaining transactions sets too`goodMessages`.</span></span>
  * <span data-ttu-id="9c346-156">Разделение обмена на наборы транзакций — блокировка обмена при ошибке: разделяет обмен на наборы транзакций и анализирует каждый из них.</span><span class="sxs-lookup"><span data-stu-id="9c346-156">Split Interchange as transaction sets - suspend interchange on error: Splits interchange into transaction sets and parses each transaction set.</span></span> 
  <span data-ttu-id="9c346-157">Если один или несколько наборов транзакций hello обмена сбой проверки, действие hello X12 декодирования выводит все транзакции hello задает в этом сообщении слишком`badMessages`.</span><span class="sxs-lookup"><span data-stu-id="9c346-157">If one or more transaction sets in hello interchange fail validation, hello X12 Decode action outputs all hello transaction sets in that interchange too`badMessages`.</span></span>
  * <span data-ttu-id="9c346-158">Сохранить обмен — приостанавливать обработку наборов транзакций при ошибке: сообщение hello Preserve и процесс hello всего пакетного сообщения.</span><span class="sxs-lookup"><span data-stu-id="9c346-158">Preserve Interchange - suspend transaction sets on error: Preserve hello interchange and process hello entire batched interchange.</span></span> 
  <span data-ttu-id="9c346-159">Действие Hello X12 декодирования выводит только этих наборов, не прошедшие проверку слишком`badMessages`и выводит hello оставшиеся транзакции задает слишком`goodMessages`.</span><span class="sxs-lookup"><span data-stu-id="9c346-159">hello X12 Decode action outputs only those transaction sets that fail validation too`badMessages`, and outputs hello remaining transactions sets too`goodMessages`.</span></span>
  * <span data-ttu-id="9c346-160">Сохранить обмен — приостанавливать обработку сообщения об ошибке: сообщение hello Preserve и процесс hello всего пакетного сообщения.</span><span class="sxs-lookup"><span data-stu-id="9c346-160">Preserve Interchange - suspend interchange on error: Preserve hello interchange and process hello entire batched interchange.</span></span> 
  <span data-ttu-id="9c346-161">Если один или несколько наборов транзакций hello обмена сбой проверки, действие hello X12 декодирования выводит все транзакции hello задает в этом сообщении слишком`badMessages`.</span><span class="sxs-lookup"><span data-stu-id="9c346-161">If one or more transaction sets in hello interchange fail validation, hello X12 Decode action outputs all hello transaction sets in that interchange too`badMessages`.</span></span>
* <span data-ttu-id="9c346-162">Создает техническое (управляющее) и функциональное подтверждение (если настроено).</span><span class="sxs-lookup"><span data-stu-id="9c346-162">Generates a Technical (control) and/or Functional acknowledgment (if configured).</span></span>
  * <span data-ttu-id="9c346-163">Техническое подтверждение или hello CONTRL ACK сообщает результаты hello синтаксической проверки hello завершения получения обмена.</span><span class="sxs-lookup"><span data-stu-id="9c346-163">A Technical Acknowledgment or hello CONTRL ACK reports hello results of a syntactical check of hello complete received interchange.</span></span>
  * <span data-ttu-id="9c346-164">Функциональное подтверждение сообщает о принятии или отклонении полученного обмена или отдельной группы.</span><span class="sxs-lookup"><span data-stu-id="9c346-164">A functional acknowledgment acknowledges accept or reject a received interchange or a group</span></span>

## <a name="view-swagger-file"></a><span data-ttu-id="9c346-165">Просмотр файла Swagger</span><span class="sxs-lookup"><span data-stu-id="9c346-165">View Swagger file</span></span>
<span data-ttu-id="9c346-166">tooview hello Swagger сведения для соединителя EDIFACT hello, см. [EDIFACT](/connectors/edifact/).</span><span class="sxs-lookup"><span data-stu-id="9c346-166">tooview hello Swagger details for hello EDIFACT connector, see [EDIFACT](/connectors/edifact/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9c346-167">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9c346-167">Next steps</span></span>
[<span data-ttu-id="9c346-168">Дополнительные сведения о hello пакет интеграции Enterprise</span><span class="sxs-lookup"><span data-stu-id="9c346-168">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "Дополнительные сведения о пакет интеграции Enterprise") 

