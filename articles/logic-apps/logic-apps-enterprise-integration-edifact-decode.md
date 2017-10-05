---
title: "Декодирование сообщений EDIFACT в Azure Logic Apps | Документация Майкрософт"
description: "Проверка EDI и создание подтверждений с помощью декодера сообщений EDIFACT в пакете интеграции Enterprise для Azure Logic Apps"
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
ms.openlocfilehash: e3787b48037360bf6066ddce2bacba6842213b2d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="decode-edifact-messages-for-azure-logic-apps-with-the-enterprise-integration-pack"></a><span data-ttu-id="9f310-103">Декодирование сообщений EDIFACT для Azure Logic Apps с помощью пакета интеграции Enterprise</span><span class="sxs-lookup"><span data-stu-id="9f310-103">Decode EDIFACT messages for Azure Logic Apps with the Enterprise Integration Pack</span></span>

<span data-ttu-id="9f310-104">С помощью соединителя для декодирования сообщений EDIFACT вы можете проверить свойства партнера и EDI, а также разделить обмен на наборы транзакций или сохранить целые обмены и создавать подтверждения для обработанных транзакций.</span><span class="sxs-lookup"><span data-stu-id="9f310-104">With the Decode EDIFACT message connector, you can validate EDI and partner-specific properties, split interchanges into transactions sets or preserve entire interchanges, and generate acknowledgments for processed transactions.</span></span> <span data-ttu-id="9f310-105">Чтобы использовать этот соединитель, добавьте его в существующий триггер в приложении логики.</span><span class="sxs-lookup"><span data-stu-id="9f310-105">To use this connector, you must add the connector to an existing trigger in your logic app.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="9f310-106">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="9f310-106">Before you start</span></span>

<span data-ttu-id="9f310-107">Вам понадобится следующее:</span><span class="sxs-lookup"><span data-stu-id="9f310-107">Here's the items you need:</span></span>

* <span data-ttu-id="9f310-108">Учетная запись Azure. Вы можете создать [бесплатную учетную запись](https://azure.microsoft.com/free).</span><span class="sxs-lookup"><span data-stu-id="9f310-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="9f310-109">[Учетная запись интеграции](logic-apps-enterprise-integration-create-integration-account.md), уже определенная и связанная с подпиской Azure.</span><span class="sxs-lookup"><span data-stu-id="9f310-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="9f310-110">Для работы с соединителем для декодирования сообщений EDIFACT потребуется учетная запись интеграции.</span><span class="sxs-lookup"><span data-stu-id="9f310-110">You must have an integration account to use the Decode EDIFACT message connector.</span></span> 
* <span data-ttu-id="9f310-111">В учетной записи интеграции должны быть определены по крайней мере два [партнера](logic-apps-enterprise-integration-partners.md).</span><span class="sxs-lookup"><span data-stu-id="9f310-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="9f310-112">В учетной записи интеграции должно быть определено [соглашение EDIFACT](logic-apps-enterprise-integration-edifact.md).</span><span class="sxs-lookup"><span data-stu-id="9f310-112">An [EDIFACT agreement](logic-apps-enterprise-integration-edifact.md) that's already defined in your integration account</span></span>

## <a name="decode-edifact-messages"></a><span data-ttu-id="9f310-113">Декодирование сообщений EDIFACT</span><span class="sxs-lookup"><span data-stu-id="9f310-113">Decode EDIFACT messages</span></span>

1. <span data-ttu-id="9f310-114">[Создание приложения логики](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="9f310-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="9f310-115">В соединителе для декодирования сообщений EDIFACT нет триггеров, поэтому вам придется добавить триггер, чтобы запустить приложение логики (например, триггер запроса).</span><span class="sxs-lookup"><span data-stu-id="9f310-115">The Decode EDIFACT message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="9f310-116">В конструкторе приложений логики добавьте триггер, а затем добавьте действие в приложение логики.</span><span class="sxs-lookup"><span data-stu-id="9f310-116">In the Logic App Designer, add a trigger, and then add an action to your logic app.</span></span>

3. <span data-ttu-id="9f310-117">В поле поиска введите "EDIFACT" в качестве фильтра.</span><span class="sxs-lookup"><span data-stu-id="9f310-117">In the search box, enter "EDIFACT" as your filter.</span></span> <span data-ttu-id="9f310-118">Выберите**Decode EDIFACT Message** (Декодировать сообщение EDIFACT).</span><span class="sxs-lookup"><span data-stu-id="9f310-118">Select **Decode EDIFACT Message**.</span></span>
   
    ![поиск EDIFACT](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage1.png)

3. <span data-ttu-id="9f310-120">Если ранее вы не создавали подключения к учетной записи интеграции, вам будет предложено сделать это сейчас.</span><span class="sxs-lookup"><span data-stu-id="9f310-120">If you didn't previously create any connections to your integration account, you're prompted to create that connection now.</span></span> <span data-ttu-id="9f310-121">Присвойте подключению имя и выберите учетную запись интеграции, которую следует подключить.</span><span class="sxs-lookup"><span data-stu-id="9f310-121">Name your connection, and select the integration account that you want to connect.</span></span>
   
    ![Создание учетной записи интеграции](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage2.png)

    <span data-ttu-id="9f310-123">Свойства со звездочкой обязательные.</span><span class="sxs-lookup"><span data-stu-id="9f310-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="9f310-124">Свойство</span><span class="sxs-lookup"><span data-stu-id="9f310-124">Property</span></span> | <span data-ttu-id="9f310-125">Сведения</span><span class="sxs-lookup"><span data-stu-id="9f310-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="9f310-126">Имя подключения*</span><span class="sxs-lookup"><span data-stu-id="9f310-126">Connection Name *</span></span> |<span data-ttu-id="9f310-127">Введите имя подключения</span><span class="sxs-lookup"><span data-stu-id="9f310-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="9f310-128">Учетная запись интеграции*</span><span class="sxs-lookup"><span data-stu-id="9f310-128">Integration Account *</span></span> |<span data-ttu-id="9f310-129">Выберите имя для учетной записи интеграции.</span><span class="sxs-lookup"><span data-stu-id="9f310-129">Enter a name for your integration account.</span></span> <span data-ttu-id="9f310-130">Убедитесь, что учетная запись интеграции и приложение логики находятся в одном регионе Azure.</span><span class="sxs-lookup"><span data-stu-id="9f310-130">Make sure that your integration account and logic app are in the same Azure location.</span></span> |

4. <span data-ttu-id="9f310-131">Чтобы завершить создание подключения, нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="9f310-131">When you're done to finish creating your connection, choose **Create**.</span></span> <span data-ttu-id="9f310-132">Данные для подключения должны выглядеть примерно так, как показано в примере.</span><span class="sxs-lookup"><span data-stu-id="9f310-132">Your connection details should look similar to this example:</span></span>

    ![Данные учетной записи интеграции](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage3.png)  

5. <span data-ttu-id="9f310-134">После того как подключение будет создано, как показано в этом примере, выберите неструктурированный файл сообщения EDIFACT для декодирования.</span><span class="sxs-lookup"><span data-stu-id="9f310-134">After your connection is created, as shown in this example, select the EDIFACT flat file message to decode.</span></span>

    ![создано подключение к учетной записи интеграции](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage4.png)  

    <span data-ttu-id="9f310-136">Например:</span><span class="sxs-lookup"><span data-stu-id="9f310-136">For example:</span></span>

    ![Выбор неструктурированного файла сообщения EDIFACT для декодирования](./media/logic-apps-enterprise-integration-edifact-decode/edifactdecodeimage5.png)  

## <a name="edifact-decoder-details"></a><span data-ttu-id="9f310-138">Сведения о декодере EDIFACT</span><span class="sxs-lookup"><span data-stu-id="9f310-138">EDIFACT decoder details</span></span>

<span data-ttu-id="9f310-139">Соединитель для декодирования EDIFACT выполняет следующие задачи.</span><span class="sxs-lookup"><span data-stu-id="9f310-139">The Decode EDIFACT connector performs these tasks:</span></span> 

* <span data-ttu-id="9f310-140">Проверяет конверт на соответствие соглашению с торговым партнером.</span><span class="sxs-lookup"><span data-stu-id="9f310-140">Validates the envelope against trading partner agreement.</span></span>
* <span data-ttu-id="9f310-141">Определяет соглашение, сопоставляя квалификатор и идентификатор отправителя с квалификатором и идентификатором получателя.</span><span class="sxs-lookup"><span data-stu-id="9f310-141">Resolves the agreement by matching the sender qualifier & identifier and receiver qualifier & identifier.</span></span>
* <span data-ttu-id="9f310-142">Разделяет обмен на несколько транзакций (если в нем есть несколько транзакций) на основе настройки параметров получения соглашения.</span><span class="sxs-lookup"><span data-stu-id="9f310-142">Splits an interchange into multiple transactions when the interchange has more than one transaction based on the agreement's receive settings configuration.</span></span>
* <span data-ttu-id="9f310-143">Дизассемблирует обмен.</span><span class="sxs-lookup"><span data-stu-id="9f310-143">Disassembles the interchange.</span></span>
* <span data-ttu-id="9f310-144">Проверяет EDI и свойства партнера, включая следующие проверки:</span><span class="sxs-lookup"><span data-stu-id="9f310-144">Validates EDI and partner-specific properties including:</span></span>
  * <span data-ttu-id="9f310-145">Проверка структуры конверта обмена.</span><span class="sxs-lookup"><span data-stu-id="9f310-145">Validation of the interchange envelope structure</span></span>
  * <span data-ttu-id="9f310-146">Проверка схемы конверта на соответствие схеме управления.</span><span class="sxs-lookup"><span data-stu-id="9f310-146">Schema validation of the envelope against the control schema</span></span>
  * <span data-ttu-id="9f310-147">Проверка схемы элементов данных в наборе транзакций на соответствие схеме сообщения.</span><span class="sxs-lookup"><span data-stu-id="9f310-147">Schema validation of the transaction-set data elements against the message schema</span></span>
  * <span data-ttu-id="9f310-148">Проверяет EDI для элементов данных в наборе транзакций.</span><span class="sxs-lookup"><span data-stu-id="9f310-148">EDI validation performed on transaction-set data elements</span></span>
* <span data-ttu-id="9f310-149">Проверяет отсутствие дубликатов контрольных номеров для обмена, группы и транзакции (если настроено).</span><span class="sxs-lookup"><span data-stu-id="9f310-149">Verifies that the interchange, group, and transaction set control numbers are not duplicates (if configured)</span></span> 
  * <span data-ttu-id="9f310-150">Проверяет контрольный номер на соответствие предыдущим обменам.</span><span class="sxs-lookup"><span data-stu-id="9f310-150">Checks the interchange control number against previously received interchanges.</span></span> 
  * <span data-ttu-id="9f310-151">Проверяет контрольный номер группы на соответствие контрольным номерам групп в других обменах.</span><span class="sxs-lookup"><span data-stu-id="9f310-151">Checks the group control number against other group control numbers in the interchange.</span></span> 
  * <span data-ttu-id="9f310-152">Проверяет контрольный номер набора транзакций на соответствие контрольным номерам других наборов транзакций в той же группе.</span><span class="sxs-lookup"><span data-stu-id="9f310-152">Checks the transaction set control number against other transaction set control numbers in that group.</span></span>
* <span data-ttu-id="9f310-153">Разделяет обмен на наборы транзакций или сохраняет весь обмен:</span><span class="sxs-lookup"><span data-stu-id="9f310-153">Splits the interchange into transaction sets, or preserves the entire interchange:</span></span>
  * <span data-ttu-id="9f310-154">Разделение обмена на наборы транзакций — блокировка наборов транзакций при ошибке: разделяет обмен на наборы транзакций и анализирует каждый из них.</span><span class="sxs-lookup"><span data-stu-id="9f310-154">Split Interchange as transaction sets - suspend transaction sets on error: Splits interchange into transaction sets and parses each transaction set.</span></span> 
  <span data-ttu-id="9f310-155">Действие декодирования X12 выводит только те наборы транзакций, которые не прошли проверку в `badMessages`, и выводит оставшиеся наборы транзакций в `goodMessages`.</span><span class="sxs-lookup"><span data-stu-id="9f310-155">The X12 Decode action outputs only those transaction sets that fail validation to `badMessages`, and outputs the remaining transactions sets to `goodMessages`.</span></span>
  * <span data-ttu-id="9f310-156">Разделение обмена на наборы транзакций — блокировка обмена при ошибке: разделяет обмен на наборы транзакций и анализирует каждый из них.</span><span class="sxs-lookup"><span data-stu-id="9f310-156">Split Interchange as transaction sets - suspend interchange on error: Splits interchange into transaction sets and parses each transaction set.</span></span> 
  <span data-ttu-id="9f310-157">Если один или несколько наборов транзакций, входящих в обмен, не проходят проверку, декодирование X12 выводит все наборы транзакций этого обмена в `badMessages`.</span><span class="sxs-lookup"><span data-stu-id="9f310-157">If one or more transaction sets in the interchange fail validation, the X12 Decode action outputs all the transaction sets in that interchange to `badMessages`.</span></span>
  * <span data-ttu-id="9f310-158">Сохранение обмена — блокировка наборов транзакций при ошибке: сохраняет обмен и обрабатывает весь пакетный обмен.</span><span class="sxs-lookup"><span data-stu-id="9f310-158">Preserve Interchange - suspend transaction sets on error: Preserve the interchange and process the entire batched interchange.</span></span> 
  <span data-ttu-id="9f310-159">Действие декодирования X12 выводит только те наборы транзакций, которые не прошли проверку в `badMessages`, и выводит оставшиеся наборы транзакций в `goodMessages`.</span><span class="sxs-lookup"><span data-stu-id="9f310-159">The X12 Decode action outputs only those transaction sets that fail validation to `badMessages`, and outputs the remaining transactions sets to `goodMessages`.</span></span>
  * <span data-ttu-id="9f310-160">Сохранение обмена — блокировка обмена при ошибке: сохраняет обмен и обрабатывает весь пакетный обмен.</span><span class="sxs-lookup"><span data-stu-id="9f310-160">Preserve Interchange - suspend interchange on error: Preserve the interchange and process the entire batched interchange.</span></span> 
  <span data-ttu-id="9f310-161">Если один или несколько наборов транзакций, входящих в обмен, не проходят проверку, декодирование X12 выводит все наборы транзакций этого обмена в `badMessages`.</span><span class="sxs-lookup"><span data-stu-id="9f310-161">If one or more transaction sets in the interchange fail validation, the X12 Decode action outputs all the transaction sets in that interchange to `badMessages`.</span></span>
* <span data-ttu-id="9f310-162">Создает техническое (управляющее) и функциональное подтверждение (если настроено).</span><span class="sxs-lookup"><span data-stu-id="9f310-162">Generates a Technical (control) and/or Functional acknowledgment (if configured).</span></span>
  * <span data-ttu-id="9f310-163">Техническое подтверждение (CONTRL ACK) выводит результаты синтаксической проверки для всего полученного обмена.</span><span class="sxs-lookup"><span data-stu-id="9f310-163">A Technical Acknowledgment or the CONTRL ACK reports the results of a syntactical check of the complete received interchange.</span></span>
  * <span data-ttu-id="9f310-164">Функциональное подтверждение сообщает о принятии или отклонении полученного обмена или отдельной группы.</span><span class="sxs-lookup"><span data-stu-id="9f310-164">A functional acknowledgment acknowledges accept or reject a received interchange or a group</span></span>

## <a name="view-swagger-file"></a><span data-ttu-id="9f310-165">Просмотр файла Swagger</span><span class="sxs-lookup"><span data-stu-id="9f310-165">View Swagger file</span></span>
<span data-ttu-id="9f310-166">Дополнительные сведения о Swagger для соединителя EDIFACT см.в [этой статье](/connectors/edifact/).</span><span class="sxs-lookup"><span data-stu-id="9f310-166">To view the Swagger details for the EDIFACT connector, see [EDIFACT](/connectors/edifact/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9f310-167">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9f310-167">Next steps</span></span>
[<span data-ttu-id="9f310-168">Обзор пакета интеграции Enterprise</span><span class="sxs-lookup"><span data-stu-id="9f310-168">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "Обзор пакета интеграции Enterprise") 

