---
title: "сообщения об изменении aaaEncode X12 - приложения логики Azure | Документы Microsoft"
description: "Проверка EDI и преобразования XML-кодировке сообщения с X12 сообщений кодировщика в hello пакет интеграции Enterprise для логики приложений Azure"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: a01e9ca9-816b-479e-ab11-4a984f10f62d
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 785dbd2c7c82463154732921e07e3586d2307840
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="encode-x12-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a><span data-ttu-id="3086a-103">Кодирование X12 сообщений для приложения логики Azure с hello пакет интеграции Enterprise</span><span class="sxs-lookup"><span data-stu-id="3086a-103">Encode X12 messages for Azure Logic Apps with hello Enterprise Integration Pack</span></span>

<span data-ttu-id="3086a-104">С соединителем сообщение hello Encode X12 проверка EDI и свойств, преобразовать XML-кодировке сообщения в EDI наборов транзакций в сообщении hello и запросить Техническое подтверждение и функциональное подтверждение.</span><span class="sxs-lookup"><span data-stu-id="3086a-104">With hello Encode X12 message connector, you can validate EDI and partner-specific properties, convert XML-encoded messages into EDI transaction sets in hello interchange, and request a Technical Acknowledgement, Functional Acknowledgment, or both.</span></span>
<span data-ttu-id="3086a-105">toouse этот соединитель, необходимо добавить существующий триггер в приложении логику tooan соединитель hello.</span><span class="sxs-lookup"><span data-stu-id="3086a-105">toouse this connector, you must add hello connector tooan existing trigger in your logic app.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="3086a-106">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="3086a-106">Before you start</span></span>

<span data-ttu-id="3086a-107">Вот hello необходимых элементов.</span><span class="sxs-lookup"><span data-stu-id="3086a-107">Here's hello items you need:</span></span>

* <span data-ttu-id="3086a-108">Учетная запись Azure. Вы можете создать [бесплатную учетную запись](https://azure.microsoft.com/free).</span><span class="sxs-lookup"><span data-stu-id="3086a-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="3086a-109">[Учетная запись интеграции](logic-apps-enterprise-integration-create-integration-account.md), уже определенная и связанная с подпиской Azure.</span><span class="sxs-lookup"><span data-stu-id="3086a-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="3086a-110">Необходимо иметь соединителя интеграции Encode X12 hello учетной записи toouse сообщения.</span><span class="sxs-lookup"><span data-stu-id="3086a-110">You must have an integration account toouse hello Encode X12 message connector.</span></span>
* <span data-ttu-id="3086a-111">В учетной записи интеграции должны быть определены по крайней мере два [партнера](logic-apps-enterprise-integration-partners.md).</span><span class="sxs-lookup"><span data-stu-id="3086a-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="3086a-112">В учетной записи интеграции должно быть определено [соглашение X12](logic-apps-enterprise-integration-x12.md).</span><span class="sxs-lookup"><span data-stu-id="3086a-112">An [X12 agreement](logic-apps-enterprise-integration-x12.md) that's already defined in your integration account</span></span>

## <a name="encode-x12-messages"></a><span data-ttu-id="3086a-113">Кодирование сообщений X12</span><span class="sxs-lookup"><span data-stu-id="3086a-113">Encode X12 messages</span></span>

1. <span data-ttu-id="3086a-114">[Создание приложения логики](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="3086a-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="3086a-115">Соединитель сообщения Hello Encode X12 не имеет триггеры, поэтому ее нужно добавить триггер для запуска приложения логики, как триггер запроса.</span><span class="sxs-lookup"><span data-stu-id="3086a-115">hello Encode X12 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="3086a-116">В hello конструктор логики приложения добавить триггер и добавьте действие tooyour логику приложения.</span><span class="sxs-lookup"><span data-stu-id="3086a-116">In hello Logic App Designer, add a trigger, and then add an action tooyour logic app.</span></span>

3.  <span data-ttu-id="3086a-117">В поле поиска hello введите «x12» для фильтра.</span><span class="sxs-lookup"><span data-stu-id="3086a-117">In hello search box, enter "x12" for your filter.</span></span> <span data-ttu-id="3086a-118">Выберите либо **X12-кодирования сообщений tooX12 по имени соглашения** или **X12-кодирования сообщений tooX12 с удостоверениями**.</span><span class="sxs-lookup"><span data-stu-id="3086a-118">Select either **X12 - Encode tooX12 message by agreement name** or **X12 - Encode tooX12 message by identities**.</span></span>
   
    ![Поиск по запросу "x12"](./media/logic-apps-enterprise-integration-x12-encode/x12decodeimage1.png) 

3. <span data-ttu-id="3086a-120">Если вы еще не создана ранее все подключения учетной записи интеграции tooyour, появится предложение toocreate теперь это подключение.</span><span class="sxs-lookup"><span data-stu-id="3086a-120">If you didn't previously create any connections tooyour integration account, you're prompted toocreate that connection now.</span></span> <span data-ttu-id="3086a-121">Имя подключения и установите hello интеграции учетной записью, которую tooconnect.</span><span class="sxs-lookup"><span data-stu-id="3086a-121">Name your connection, and select hello integration account that you want tooconnect.</span></span> 
   
    ![подключение к учетной записи интеграции](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage1.png)

    <span data-ttu-id="3086a-123">Свойства со звездочкой обязательные.</span><span class="sxs-lookup"><span data-stu-id="3086a-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="3086a-124">Свойство</span><span class="sxs-lookup"><span data-stu-id="3086a-124">Property</span></span> | <span data-ttu-id="3086a-125">Сведения</span><span class="sxs-lookup"><span data-stu-id="3086a-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="3086a-126">Имя подключения*</span><span class="sxs-lookup"><span data-stu-id="3086a-126">Connection Name *</span></span> |<span data-ttu-id="3086a-127">Введите имя подключения</span><span class="sxs-lookup"><span data-stu-id="3086a-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="3086a-128">Учетная запись интеграции*</span><span class="sxs-lookup"><span data-stu-id="3086a-128">Integration Account *</span></span> |<span data-ttu-id="3086a-129">Выберите имя для учетной записи интеграции.</span><span class="sxs-lookup"><span data-stu-id="3086a-129">Enter a name for your integration account.</span></span> <span data-ttu-id="3086a-130">Обеспечить наличие учетной записи и логика приложения интеграции в hello Azure местоположения.</span><span class="sxs-lookup"><span data-stu-id="3086a-130">Make sure that your integration account and logic app are in hello same Azure location.</span></span> |

5.  <span data-ttu-id="3086a-131">После завершения, сведения о соединении с вашей должен выглядеть аналогичный пример toothis.</span><span class="sxs-lookup"><span data-stu-id="3086a-131">When you're done, your connection details should look similar toothis example.</span></span> <span data-ttu-id="3086a-132">toofinish при создании подключения, выберите **создать**.</span><span class="sxs-lookup"><span data-stu-id="3086a-132">toofinish creating your connection, choose **Create**.</span></span>

    ![создано подключение к учетной записи интеграции](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage2.png)

    <span data-ttu-id="3086a-134">Подключение создано.</span><span class="sxs-lookup"><span data-stu-id="3086a-134">Your connection is now created.</span></span>

    ![сведения о подключении к учетной записи интеграции](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage3.png) 

#### <a name="encode-x12-messages-by-agreement-name"></a><span data-ttu-id="3086a-136">Кодирование сообщений X12 по имени соглашения</span><span class="sxs-lookup"><span data-stu-id="3086a-136">Encode X12 messages by agreement name</span></span>

<span data-ttu-id="3086a-137">При выборе tooencode X12 сообщения по имени соглашения открывается hello **имя X12 соглашение** введите или выберите вашей существующей X12 соглашения.</span><span class="sxs-lookup"><span data-stu-id="3086a-137">If you chose tooencode X12 messages by agreement name, open hello **Name of X12 agreement** list, enter or select your existing X12 agreement.</span></span> <span data-ttu-id="3086a-138">Введите tooencode сообщение hello XML.</span><span class="sxs-lookup"><span data-stu-id="3086a-138">Enter hello XML message tooencode.</span></span>

![Введите X12 соглашения, имя и XML-сообщений tooencode](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage4.png)

#### <a name="encode-x12-messages-by-identities"></a><span data-ttu-id="3086a-140">Кодирование сообщений X12 по идентификаторам</span><span class="sxs-lookup"><span data-stu-id="3086a-140">Encode X12 messages by identities</span></span>

<span data-ttu-id="3086a-141">При выборе tooencode X12 сообщения с удостоверениями ввести идентификатор отправителя hello, квалификатор отправителя, идентификатор получателя и квалификатор получателя, настроенным в вашей X12 соглашения.</span><span class="sxs-lookup"><span data-stu-id="3086a-141">If you choose tooencode X12 messages by identities, enter hello sender identifier, sender qualifier, receiver identifier, and receiver qualifier as configured in your X12 agreement.</span></span> <span data-ttu-id="3086a-142">Выберите tooencode сообщение hello XML.</span><span class="sxs-lookup"><span data-stu-id="3086a-142">Select hello XML message tooencode.</span></span>
   
![Введите идентификаторы для отправителя и получателя, выберите tooencode сообщения XML](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage5.png) 

## <a name="x12-encode-details"></a><span data-ttu-id="3086a-144">Сведения о кодировании X12</span><span class="sxs-lookup"><span data-stu-id="3086a-144">X12 Encode details</span></span>

<span data-ttu-id="3086a-145">Соединитель Encode Hello X12 выполняет следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="3086a-145">hello X12 Encode connector performs these tasks:</span></span>

* <span data-ttu-id="3086a-146">Определяет соглашение путем сопоставления свойств контекста отправителя и получателя.</span><span class="sxs-lookup"><span data-stu-id="3086a-146">Agreement resolution by matching sender and receiver context properties.</span></span>
* <span data-ttu-id="3086a-147">Сериализует hello обмен EDI, преобразование сообщений XML-кодировке в EDI наборов транзакций в сообщении hello.</span><span class="sxs-lookup"><span data-stu-id="3086a-147">Serializes hello EDI interchange, converting XML-encoded messages into EDI transaction sets in hello interchange.</span></span>
* <span data-ttu-id="3086a-148">Генерирует сегменты заголовков и окончаний для наборов транзакций.</span><span class="sxs-lookup"><span data-stu-id="3086a-148">Applies transaction set header and trailer segments</span></span>
* <span data-ttu-id="3086a-149">Создает контрольное число обмена, контрольное число группы и контрольное число набора транзакций для каждого исходящего обмена.</span><span class="sxs-lookup"><span data-stu-id="3086a-149">Generates an interchange control number, a group control number, and a transaction set control number for each outgoing interchange</span></span>
* <span data-ttu-id="3086a-150">Заменяет разделителей в полезных данных hello</span><span class="sxs-lookup"><span data-stu-id="3086a-150">Replaces separators in hello payload data</span></span>
* <span data-ttu-id="3086a-151">Проверяет EDI и свойства для конкретного партнера.</span><span class="sxs-lookup"><span data-stu-id="3086a-151">Validates EDI and partner-specific properties</span></span>
  * <span data-ttu-id="3086a-152">Проверка схемы hello элементов данных набора транзакций от приветственное сообщение схемы</span><span class="sxs-lookup"><span data-stu-id="3086a-152">Schema validation of hello transaction-set data elements against hello message Schema</span></span>
  * <span data-ttu-id="3086a-153">Выполняет проверку EDI для элементов данных в наборе транзакций.</span><span class="sxs-lookup"><span data-stu-id="3086a-153">EDI validation performed on transaction-set data elements.</span></span>
  * <span data-ttu-id="3086a-154">Выполняет расширенную проверку для элементов данных в наборе транзакций.</span><span class="sxs-lookup"><span data-stu-id="3086a-154">Extended validation performed on transaction-set data elements</span></span>
* <span data-ttu-id="3086a-155">Запрашивает техническое и (или) функциональное подтверждение (если настроено).</span><span class="sxs-lookup"><span data-stu-id="3086a-155">Requests a Technical and/or Functional acknowledgment (if configured).</span></span>
  * <span data-ttu-id="3086a-156">Техническое подтверждение создается по результатам проверки заголовков.</span><span class="sxs-lookup"><span data-stu-id="3086a-156">A Technical Acknowledgment generates as a result of header validation.</span></span> <span data-ttu-id="3086a-157">Техническое подтверждение Hello сообщает о состоянии hello hello обработки заголовка обмена и трейлер получатель адрес hello</span><span class="sxs-lookup"><span data-stu-id="3086a-157">hello technical acknowledgment reports hello status of hello processing of an interchange header and trailer by hello address receiver</span></span>
  * <span data-ttu-id="3086a-158">Функциональное подтверждение создается по результатам проверки тела сообщения.</span><span class="sxs-lookup"><span data-stu-id="3086a-158">A Functional Acknowledgment generates as a result of body validation.</span></span> <span data-ttu-id="3086a-159">Hello функциональное подтверждение сообщает каждая ошибка возникла при обработке hello получил документ</span><span class="sxs-lookup"><span data-stu-id="3086a-159">hello functional acknowledgment reports each error encountered while processing hello received document</span></span>

## <a name="view-hello-swagger"></a><span data-ttu-id="3086a-160">Представление hello swagger</span><span class="sxs-lookup"><span data-stu-id="3086a-160">View hello swagger</span></span>
<span data-ttu-id="3086a-161">В разделе hello [swagger сведения](/connectors/x12/).</span><span class="sxs-lookup"><span data-stu-id="3086a-161">See hello [swagger details](/connectors/x12/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="3086a-162">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3086a-162">Next steps</span></span>
[<span data-ttu-id="3086a-163">Дополнительные сведения о hello пакет интеграции Enterprise</span><span class="sxs-lookup"><span data-stu-id="3086a-163">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "Дополнительные сведения о пакет интеграции Enterprise") 

