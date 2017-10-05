---
title: "Декодирование сообщений X12 в Azure Logic Apps | Документация Майкрософт"
description: "Проверка EDI и создание подтверждений с помощью декодера сообщений X12 в пакете интеграции Enterprise для Azure Logic Apps"
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
ms.openlocfilehash: 18719a8f49c74973947517161f7306c233a9323f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="decode-x12-messages-for-azure-logic-apps-with-the-enterprise-integration-pack"></a><span data-ttu-id="06df6-103">Декодирование сообщений X12 для Azure Logic Apps с помощью пакета интеграции Enterprise</span><span class="sxs-lookup"><span data-stu-id="06df6-103">Decode X12 messages for Azure Logic Apps with the Enterprise Integration Pack</span></span>

<span data-ttu-id="06df6-104">С помощью соединителя для декодирования сообщений X12 вы можете проверить конверт на соответствие соглашению с торговым партнером, проверить свойства партнера и EDI, а также разделить обмен на наборы транзакций или сохранить целые обмены и создавать подтверждения для обработанных транзакций.</span><span class="sxs-lookup"><span data-stu-id="06df6-104">With the Decode X12 message connector, you can validate the envelope against a trading partner agreement, validate EDI and partner-specific properties, split interchanges into transactions sets or preserve entire interchanges, and generate acknowledgments for processed transactions.</span></span> <span data-ttu-id="06df6-105">Чтобы использовать этот соединитель, добавьте его в существующий триггер в приложении логики.</span><span class="sxs-lookup"><span data-stu-id="06df6-105">To use this connector, you must add the connector to an existing trigger in your logic app.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="06df6-106">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="06df6-106">Before you start</span></span>

<span data-ttu-id="06df6-107">Вам понадобится следующее:</span><span class="sxs-lookup"><span data-stu-id="06df6-107">Here's the items you need:</span></span>

* <span data-ttu-id="06df6-108">Учетная запись Azure. Вы можете создать [бесплатную учетную запись](https://azure.microsoft.com/free).</span><span class="sxs-lookup"><span data-stu-id="06df6-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="06df6-109">[Учетная запись интеграции](logic-apps-enterprise-integration-create-integration-account.md), уже определенная и связанная с подпиской Azure.</span><span class="sxs-lookup"><span data-stu-id="06df6-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="06df6-110">Для работы с соединителем для декодирования сообщений X12 потребуется учетная запись интеграции.</span><span class="sxs-lookup"><span data-stu-id="06df6-110">You must have an integration account to use the Decode X12 message connector.</span></span>
* <span data-ttu-id="06df6-111">В учетной записи интеграции должны быть определены по крайней мере два [партнера](logic-apps-enterprise-integration-partners.md).</span><span class="sxs-lookup"><span data-stu-id="06df6-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="06df6-112">В учетной записи интеграции должно быть определено [соглашение X12](logic-apps-enterprise-integration-x12.md).</span><span class="sxs-lookup"><span data-stu-id="06df6-112">An [X12 agreement](logic-apps-enterprise-integration-x12.md) that's already defined in your integration account</span></span>

## <a name="decode-x12-messages"></a><span data-ttu-id="06df6-113">Декодирование сообщений X12</span><span class="sxs-lookup"><span data-stu-id="06df6-113">Decode X12 messages</span></span>

1. <span data-ttu-id="06df6-114">[Создание приложения логики](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="06df6-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="06df6-115">В соединителе для декодирования сообщений X12 нет триггеров, поэтому вам придется добавить триггер, чтобы запустить приложение логики (например, триггер запроса).</span><span class="sxs-lookup"><span data-stu-id="06df6-115">The Decode X12 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="06df6-116">В конструкторе приложений логики добавьте триггер, а затем добавьте действие в приложение логики.</span><span class="sxs-lookup"><span data-stu-id="06df6-116">In the Logic App Designer, add a trigger, and then add an action to your logic app.</span></span>

3.  <span data-ttu-id="06df6-117">В поле поиска введите "x12" в качестве фильтра.</span><span class="sxs-lookup"><span data-stu-id="06df6-117">In the search box, enter "x12" for your filter.</span></span> <span data-ttu-id="06df6-118">Выберите **X12 - Decode X12 message** (X12 — декодировать сообщение X12).</span><span class="sxs-lookup"><span data-stu-id="06df6-118">Select **X12 - Decode X12 message**.</span></span>
   
    ![Поиск по запросу "x12"](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage1.png)  

3. <span data-ttu-id="06df6-120">Если ранее вы не создавали подключения к учетной записи интеграции, вам будет предложено сделать это сейчас.</span><span class="sxs-lookup"><span data-stu-id="06df6-120">If you didn't previously create any connections to your integration account, you're prompted to create that connection now.</span></span> <span data-ttu-id="06df6-121">Присвойте подключению имя и выберите учетную запись интеграции, которую следует подключить.</span><span class="sxs-lookup"><span data-stu-id="06df6-121">Name your connection, and select the integration account that you want to connect.</span></span> 

    ![Указание сведений о подключении к учетной записи интеграции](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage4.png)

    <span data-ttu-id="06df6-123">Свойства со звездочкой обязательные.</span><span class="sxs-lookup"><span data-stu-id="06df6-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="06df6-124">Свойство</span><span class="sxs-lookup"><span data-stu-id="06df6-124">Property</span></span> | <span data-ttu-id="06df6-125">Сведения</span><span class="sxs-lookup"><span data-stu-id="06df6-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="06df6-126">Имя подключения*</span><span class="sxs-lookup"><span data-stu-id="06df6-126">Connection Name *</span></span> |<span data-ttu-id="06df6-127">Введите имя подключения</span><span class="sxs-lookup"><span data-stu-id="06df6-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="06df6-128">Учетная запись интеграции*</span><span class="sxs-lookup"><span data-stu-id="06df6-128">Integration Account *</span></span> |<span data-ttu-id="06df6-129">Выберите имя для учетной записи интеграции.</span><span class="sxs-lookup"><span data-stu-id="06df6-129">Enter a name for your integration account.</span></span> <span data-ttu-id="06df6-130">Убедитесь, что учетная запись интеграции и приложение логики находятся в одном регионе Azure.</span><span class="sxs-lookup"><span data-stu-id="06df6-130">Make sure that your integration account and logic app are in the same Azure location.</span></span> |

5.  <span data-ttu-id="06df6-131">Когда все будет готово, данные для подключения должны выглядеть примерно так, как показано в примере.</span><span class="sxs-lookup"><span data-stu-id="06df6-131">When you're done, your connection details should look similar to this example.</span></span> <span data-ttu-id="06df6-132">Чтобы завершить создание подключения, нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="06df6-132">To finish creating your connection, choose **Create**.</span></span>
   
    ![сведения о подключении к учетной записи интеграции](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage5.png) 

6. <span data-ttu-id="06df6-134">Когда подключение будет создано, как показано в этом примере, выберите неструктурированный файл сообщения X12 для декодирования.</span><span class="sxs-lookup"><span data-stu-id="06df6-134">After your connection is created, as shown in this example, select the X12 flat file message to decode.</span></span>

    ![создано подключение к учетной записи интеграции](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage6.png) 

    <span data-ttu-id="06df6-136">Например:</span><span class="sxs-lookup"><span data-stu-id="06df6-136">For example:</span></span>

    ![Выбор неструктурированного файла сообщения X12 для декодирования](media/logic-apps-enterprise-integration-x12-decode/x12decodeimage7.png) 

## <a name="x12-decode-details"></a><span data-ttu-id="06df6-138">Сведения о декодировании X12</span><span class="sxs-lookup"><span data-stu-id="06df6-138">X12 Decode details</span></span>

<span data-ttu-id="06df6-139">Соединитель для декодирования X12 выполняет следующие задачи.</span><span class="sxs-lookup"><span data-stu-id="06df6-139">The X12 Decode connector performs these tasks:</span></span>

* <span data-ttu-id="06df6-140">Проверяет конверт на соответствие соглашению с торговым партнером.</span><span class="sxs-lookup"><span data-stu-id="06df6-140">Validates the envelope against trading partner agreement</span></span>
* <span data-ttu-id="06df6-141">Проверяет EDI и свойства для конкретного партнера.</span><span class="sxs-lookup"><span data-stu-id="06df6-141">Validates EDI and partner-specific properties</span></span>
  * <span data-ttu-id="06df6-142">Проводит структурную проверку EDI и расширенную проверку схемы.</span><span class="sxs-lookup"><span data-stu-id="06df6-142">EDI structural validation, and extended schema validation</span></span>
  * <span data-ttu-id="06df6-143">Проверяет структуру конверта обмена.</span><span class="sxs-lookup"><span data-stu-id="06df6-143">Validation of the structure of the interchange envelope.</span></span>
  * <span data-ttu-id="06df6-144">Проверяет схему конверта на соответствие схеме управления.</span><span class="sxs-lookup"><span data-stu-id="06df6-144">Schema validation of the envelope against the control schema.</span></span>
  * <span data-ttu-id="06df6-145">Проверяет схемы элементов данных в наборе транзакций на соответствие схеме сообщения.</span><span class="sxs-lookup"><span data-stu-id="06df6-145">Schema validation of the transaction-set data elements against the message schema.</span></span>
  * <span data-ttu-id="06df6-146">Проверяет EDI для элементов данных в наборе транзакций.</span><span class="sxs-lookup"><span data-stu-id="06df6-146">EDI validation performed on transaction-set data elements</span></span> 
* <span data-ttu-id="06df6-147">Проверяет отсутствие дубликатов контрольных номеров для обмена, группы и транзакции.</span><span class="sxs-lookup"><span data-stu-id="06df6-147">Verifies that the interchange, group, and transaction set control numbers are not duplicates</span></span>
  * <span data-ttu-id="06df6-148">Проверяет контрольный номер на соответствие предыдущим обменам.</span><span class="sxs-lookup"><span data-stu-id="06df6-148">Checks the interchange control number against previously received interchanges.</span></span>
  * <span data-ttu-id="06df6-149">Проверяет контрольный номер группы на соответствие контрольным номерам групп в других обменах.</span><span class="sxs-lookup"><span data-stu-id="06df6-149">Checks the group control number against other group control numbers in the interchange.</span></span>
  * <span data-ttu-id="06df6-150">Проверяет контрольный номер набора транзакций на соответствие контрольным номерам других наборов транзакций в той же группе.</span><span class="sxs-lookup"><span data-stu-id="06df6-150">Checks the transaction set control number against other transaction set control numbers in that group.</span></span>
* <span data-ttu-id="06df6-151">Разделяет обмен на наборы транзакций или сохраняет весь обмен:</span><span class="sxs-lookup"><span data-stu-id="06df6-151">Splits the interchange into transaction sets, or preserves the entire interchange:</span></span>
  * <span data-ttu-id="06df6-152">Разделение обмена на наборы транзакций — блокировка наборов транзакций при ошибке: разделяет обмен на наборы транзакций и анализирует каждый из них.</span><span class="sxs-lookup"><span data-stu-id="06df6-152">Split Interchange as transaction sets - suspend transaction sets on error: Splits interchange into transaction sets and parses each transaction set.</span></span> 
  <span data-ttu-id="06df6-153">Действие декодирования X12 выводит только те наборы транзакций, которые не прошли проверку в `badMessages`, и выводит оставшиеся наборы транзакций в `goodMessages`.</span><span class="sxs-lookup"><span data-stu-id="06df6-153">The X12 Decode action outputs only those transaction sets that fail validation to `badMessages`, and outputs the remaining transactions sets to `goodMessages`.</span></span>
  * <span data-ttu-id="06df6-154">Разделение обмена на наборы транзакций — блокировка обмена при ошибке: разделяет обмен на наборы транзакций и анализирует каждый из них.</span><span class="sxs-lookup"><span data-stu-id="06df6-154">Split Interchange as transaction sets - suspend interchange on error: Splits interchange into transaction sets and parses each transaction set.</span></span> 
  <span data-ttu-id="06df6-155">Если один или несколько наборов транзакций, входящих в обмен, не проходят проверку, декодирование X12 выводит все наборы транзакций этого обмена в `badMessages`.</span><span class="sxs-lookup"><span data-stu-id="06df6-155">If one or more transaction sets in the interchange fail validation, the X12 Decode action outputs all the transaction sets in that interchange to `badMessages`.</span></span>
  * <span data-ttu-id="06df6-156">Сохранение обмена — блокировка наборов транзакций при ошибке: сохраняет обмен и обрабатывает весь пакетный обмен.</span><span class="sxs-lookup"><span data-stu-id="06df6-156">Preserve Interchange - suspend transaction sets on error: Preserve the interchange and process the entire batched interchange.</span></span> 
  <span data-ttu-id="06df6-157">Действие декодирования X12 выводит только те наборы транзакций, которые не прошли проверку в `badMessages`, и выводит оставшиеся наборы транзакций в `goodMessages`.</span><span class="sxs-lookup"><span data-stu-id="06df6-157">The X12 Decode action outputs only those transaction sets that fail validation to `badMessages`, and outputs the remaining transactions sets to `goodMessages`.</span></span>
  * <span data-ttu-id="06df6-158">Сохранение обмена — блокировка обмена при ошибке: сохраняет обмен и обрабатывает весь пакетный обмен.</span><span class="sxs-lookup"><span data-stu-id="06df6-158">Preserve Interchange - suspend interchange on error: Preserve the interchange and process the entire batched interchange.</span></span> 
  <span data-ttu-id="06df6-159">Если один или несколько наборов транзакций, входящих в обмен, не проходят проверку, декодирование X12 выводит все наборы транзакций этого обмена в `badMessages`.</span><span class="sxs-lookup"><span data-stu-id="06df6-159">If one or more transaction sets in the interchange fail validation, the X12 Decode action outputs all the transaction sets in that interchange to `badMessages`.</span></span> 
* <span data-ttu-id="06df6-160">Генерирует техническое и (или) функциональное подтверждение (если настроено).</span><span class="sxs-lookup"><span data-stu-id="06df6-160">Generates a Technical and/or Functional acknowledgment (if configured).</span></span>
  * <span data-ttu-id="06df6-161">Техническое подтверждение создается по результатам проверки заголовков.</span><span class="sxs-lookup"><span data-stu-id="06df6-161">A Technical Acknowledgment generates as a result of header validation.</span></span> <span data-ttu-id="06df6-162">Техническое подтверждение сообщает о состоянии обработки заголовка и окончания обмена получателем.</span><span class="sxs-lookup"><span data-stu-id="06df6-162">The technical acknowledgment reports the status of the processing of an interchange header and trailer by the address receiver.</span></span>
  * <span data-ttu-id="06df6-163">Функциональное подтверждение создается по результатам проверки тела сообщения.</span><span class="sxs-lookup"><span data-stu-id="06df6-163">A Functional Acknowledgment generates as a result of body validation.</span></span> <span data-ttu-id="06df6-164">Функциональное подтверждение сообщает обо всех ошибках, зарегистрированных при обработке полученного документа.</span><span class="sxs-lookup"><span data-stu-id="06df6-164">The functional acknowledgment reports each error encountered while processing the received document</span></span>

## <a name="view-the-swagger"></a><span data-ttu-id="06df6-165">Просмотр Swagger</span><span class="sxs-lookup"><span data-stu-id="06df6-165">View the swagger</span></span>
<span data-ttu-id="06df6-166">Ознакомьтесь с [дополнительными сведениями о Swagger](/connectors/x12/).</span><span class="sxs-lookup"><span data-stu-id="06df6-166">See the [swagger details](/connectors/x12/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="06df6-167">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="06df6-167">Next steps</span></span>
[<span data-ttu-id="06df6-168">Обзор пакета интеграции Enterprise</span><span class="sxs-lookup"><span data-stu-id="06df6-168">Learn more about the Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "Обзор пакета интеграции Enterprise") 

