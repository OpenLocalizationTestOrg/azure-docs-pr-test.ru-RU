---
title: "Кодирование сообщений X12 в Azure Logic Apps | Документация Майкрософт"
description: "Проверка EDI и преобразование XML-сообщений с помощью кодировщика сообщений X12 в пакете интеграции Enterprise для Azure Logic Apps"
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
ms.openlocfilehash: 29d19364b9a98e351c95f13e68a2e63b9f6439f8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="encode-x12-messages-for-azure-logic-apps-with-the-enterprise-integration-pack"></a><span data-ttu-id="9fa38-103">Кодирование сообщений X12 для Azure Logic Apps с помощью пакета интеграции Enterprise</span><span class="sxs-lookup"><span data-stu-id="9fa38-103">Encode X12 messages for Azure Logic Apps with the Enterprise Integration Pack</span></span>

<span data-ttu-id="9fa38-104">С помощью соединителя для кодирования сообщений X12 вы можете проверить EDI и свойства для конкретного партнера, преобразовать XML-кодированные сообщения в наборы транзакций EDI в обмене и запросить техническое и (или) функциональное подтверждение.</span><span class="sxs-lookup"><span data-stu-id="9fa38-104">With the Encode X12 message connector, you can validate EDI and partner-specific properties, convert XML-encoded messages into EDI transaction sets in the interchange, and request a Technical Acknowledgement, Functional Acknowledgment, or both.</span></span>
<span data-ttu-id="9fa38-105">Чтобы использовать этот соединитель, добавьте его в существующий триггер в приложении логики.</span><span class="sxs-lookup"><span data-stu-id="9fa38-105">To use this connector, you must add the connector to an existing trigger in your logic app.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="9fa38-106">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="9fa38-106">Before you start</span></span>

<span data-ttu-id="9fa38-107">Вам понадобится следующее:</span><span class="sxs-lookup"><span data-stu-id="9fa38-107">Here's the items you need:</span></span>

* <span data-ttu-id="9fa38-108">Учетная запись Azure. Вы можете создать [бесплатную учетную запись](https://azure.microsoft.com/free).</span><span class="sxs-lookup"><span data-stu-id="9fa38-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="9fa38-109">[Учетная запись интеграции](logic-apps-enterprise-integration-create-integration-account.md), уже определенная и связанная с подпиской Azure.</span><span class="sxs-lookup"><span data-stu-id="9fa38-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="9fa38-110">Для работы с соединителем для кодирования сообщений X12 потребуется учетная запись интеграции.</span><span class="sxs-lookup"><span data-stu-id="9fa38-110">You must have an integration account to use the Encode X12 message connector.</span></span>
* <span data-ttu-id="9fa38-111">В учетной записи интеграции должны быть определены по крайней мере два [партнера](logic-apps-enterprise-integration-partners.md).</span><span class="sxs-lookup"><span data-stu-id="9fa38-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="9fa38-112">В учетной записи интеграции должно быть определено [соглашение X12](logic-apps-enterprise-integration-x12.md).</span><span class="sxs-lookup"><span data-stu-id="9fa38-112">An [X12 agreement](logic-apps-enterprise-integration-x12.md) that's already defined in your integration account</span></span>

## <a name="encode-x12-messages"></a><span data-ttu-id="9fa38-113">Кодирование сообщений X12</span><span class="sxs-lookup"><span data-stu-id="9fa38-113">Encode X12 messages</span></span>

1. <span data-ttu-id="9fa38-114">[Создание приложения логики](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="9fa38-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="9fa38-115">В соединителе для кодирования сообщений X12 нет триггеров, поэтому вам придется добавить триггер, чтобы запустить приложение логики (например, триггер запроса).</span><span class="sxs-lookup"><span data-stu-id="9fa38-115">The Encode X12 message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="9fa38-116">В конструкторе приложений логики добавьте триггер, а затем добавьте действие в приложение логики.</span><span class="sxs-lookup"><span data-stu-id="9fa38-116">In the Logic App Designer, add a trigger, and then add an action to your logic app.</span></span>

3.  <span data-ttu-id="9fa38-117">В поле поиска введите "x12" в качестве фильтра.</span><span class="sxs-lookup"><span data-stu-id="9fa38-117">In the search box, enter "x12" for your filter.</span></span> <span data-ttu-id="9fa38-118">Выберите пункт **X12 - Encode to X12 message by agreement name** (X12 — Кодирование в сообщение X12 по имени соглашения) или **X12 - Encode to X12 message by identities** (X12 — Кодирование в сообщение X12 по идентификаторам).</span><span class="sxs-lookup"><span data-stu-id="9fa38-118">Select either **X12 - Encode to X12 message by agreement name** or **X12 - Encode to X12 message by identities**.</span></span>
   
    ![Поиск по запросу "x12"](./media/logic-apps-enterprise-integration-x12-encode/x12decodeimage1.png) 

3. <span data-ttu-id="9fa38-120">Если ранее вы не создавали подключения к учетной записи интеграции, вам будет предложено сделать это сейчас.</span><span class="sxs-lookup"><span data-stu-id="9fa38-120">If you didn't previously create any connections to your integration account, you're prompted to create that connection now.</span></span> <span data-ttu-id="9fa38-121">Присвойте подключению имя и выберите учетную запись интеграции, которую следует подключить.</span><span class="sxs-lookup"><span data-stu-id="9fa38-121">Name your connection, and select the integration account that you want to connect.</span></span> 
   
    ![подключение к учетной записи интеграции](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage1.png)

    <span data-ttu-id="9fa38-123">Свойства со звездочкой обязательные.</span><span class="sxs-lookup"><span data-stu-id="9fa38-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="9fa38-124">Свойство</span><span class="sxs-lookup"><span data-stu-id="9fa38-124">Property</span></span> | <span data-ttu-id="9fa38-125">Сведения</span><span class="sxs-lookup"><span data-stu-id="9fa38-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="9fa38-126">Имя подключения*</span><span class="sxs-lookup"><span data-stu-id="9fa38-126">Connection Name *</span></span> |<span data-ttu-id="9fa38-127">Введите имя подключения</span><span class="sxs-lookup"><span data-stu-id="9fa38-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="9fa38-128">Учетная запись интеграции*</span><span class="sxs-lookup"><span data-stu-id="9fa38-128">Integration Account *</span></span> |<span data-ttu-id="9fa38-129">Выберите имя для учетной записи интеграции.</span><span class="sxs-lookup"><span data-stu-id="9fa38-129">Enter a name for your integration account.</span></span> <span data-ttu-id="9fa38-130">Убедитесь, что учетная запись интеграции и приложение логики находятся в одном регионе Azure.</span><span class="sxs-lookup"><span data-stu-id="9fa38-130">Make sure that your integration account and logic app are in the same Azure location.</span></span> |

5.  <span data-ttu-id="9fa38-131">Когда все будет готово, данные для подключения должны выглядеть примерно так, как показано в примере.</span><span class="sxs-lookup"><span data-stu-id="9fa38-131">When you're done, your connection details should look similar to this example.</span></span> <span data-ttu-id="9fa38-132">Чтобы завершить создание подключения, нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="9fa38-132">To finish creating your connection, choose **Create**.</span></span>

    ![создано подключение к учетной записи интеграции](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage2.png)

    <span data-ttu-id="9fa38-134">Подключение создано.</span><span class="sxs-lookup"><span data-stu-id="9fa38-134">Your connection is now created.</span></span>

    ![сведения о подключении к учетной записи интеграции](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage3.png) 

#### <a name="encode-x12-messages-by-agreement-name"></a><span data-ttu-id="9fa38-136">Кодирование сообщений X12 по имени соглашения</span><span class="sxs-lookup"><span data-stu-id="9fa38-136">Encode X12 messages by agreement name</span></span>

<span data-ttu-id="9fa38-137">Если вы решили закодировать сообщения X12 по имени соглашения, откройте список **Имя соглашения X12**, введите или выберите существующее соглашение X12.</span><span class="sxs-lookup"><span data-stu-id="9fa38-137">If you chose to encode X12 messages by agreement name, open the **Name of X12 agreement** list, enter or select your existing X12 agreement.</span></span> <span data-ttu-id="9fa38-138">Введите XML-сообщение для кодирования.</span><span class="sxs-lookup"><span data-stu-id="9fa38-138">Enter the XML message to encode.</span></span>

![Ввод имени соглашения X12 и XML-сообщения для кодирования](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage4.png)

#### <a name="encode-x12-messages-by-identities"></a><span data-ttu-id="9fa38-140">Кодирование сообщений X12 по идентификаторам</span><span class="sxs-lookup"><span data-stu-id="9fa38-140">Encode X12 messages by identities</span></span>

<span data-ttu-id="9fa38-141">Если вы выбрали кодирование сообщения X12 по идентификатору, введите идентификатор отправителя, квалификатор отправителя, идентификатор получателя и квалификатор получателя, как указано в соглашении X12.</span><span class="sxs-lookup"><span data-stu-id="9fa38-141">If you choose to encode X12 messages by identities, enter the sender identifier, sender qualifier, receiver identifier, and receiver qualifier as configured in your X12 agreement.</span></span> <span data-ttu-id="9fa38-142">Выберите XML-сообщение для кодирования.</span><span class="sxs-lookup"><span data-stu-id="9fa38-142">Select the XML message to encode.</span></span>
   
![Указание идентификаторов отправителя и получателя, выбор XML-сообщения для кодирования](./media/logic-apps-enterprise-integration-x12-encode/x12encodeimage5.png) 

## <a name="x12-encode-details"></a><span data-ttu-id="9fa38-144">Сведения о кодировании X12</span><span class="sxs-lookup"><span data-stu-id="9fa38-144">X12 Encode details</span></span>

<span data-ttu-id="9fa38-145">Соединитель для кодирования X12 выполняет следующие задачи.</span><span class="sxs-lookup"><span data-stu-id="9fa38-145">The X12 Encode connector performs these tasks:</span></span>

* <span data-ttu-id="9fa38-146">Определяет соглашение путем сопоставления свойств контекста отправителя и получателя.</span><span class="sxs-lookup"><span data-stu-id="9fa38-146">Agreement resolution by matching sender and receiver context properties.</span></span>
* <span data-ttu-id="9fa38-147">Сериализует обмен EDI путем преобразования сообщения в кодировке XML в набор транзакций EDI.</span><span class="sxs-lookup"><span data-stu-id="9fa38-147">Serializes the EDI interchange, converting XML-encoded messages into EDI transaction sets in the interchange.</span></span>
* <span data-ttu-id="9fa38-148">Генерирует сегменты заголовков и окончаний для наборов транзакций.</span><span class="sxs-lookup"><span data-stu-id="9fa38-148">Applies transaction set header and trailer segments</span></span>
* <span data-ttu-id="9fa38-149">Создает контрольное число обмена, контрольное число группы и контрольное число набора транзакций для каждого исходящего обмена.</span><span class="sxs-lookup"><span data-stu-id="9fa38-149">Generates an interchange control number, a group control number, and a transaction set control number for each outgoing interchange</span></span>
* <span data-ttu-id="9fa38-150">Заменяет разделители в полезных данных.</span><span class="sxs-lookup"><span data-stu-id="9fa38-150">Replaces separators in the payload data</span></span>
* <span data-ttu-id="9fa38-151">Проверяет EDI и свойства для конкретного партнера.</span><span class="sxs-lookup"><span data-stu-id="9fa38-151">Validates EDI and partner-specific properties</span></span>
  * <span data-ttu-id="9fa38-152">Проверяет схемы элементов данных в наборе транзакций на соответствие схеме сообщения.</span><span class="sxs-lookup"><span data-stu-id="9fa38-152">Schema validation of the transaction-set data elements against the message Schema</span></span>
  * <span data-ttu-id="9fa38-153">Выполняет проверку EDI для элементов данных в наборе транзакций.</span><span class="sxs-lookup"><span data-stu-id="9fa38-153">EDI validation performed on transaction-set data elements.</span></span>
  * <span data-ttu-id="9fa38-154">Выполняет расширенную проверку для элементов данных в наборе транзакций.</span><span class="sxs-lookup"><span data-stu-id="9fa38-154">Extended validation performed on transaction-set data elements</span></span>
* <span data-ttu-id="9fa38-155">Запрашивает техническое и (или) функциональное подтверждение (если настроено).</span><span class="sxs-lookup"><span data-stu-id="9fa38-155">Requests a Technical and/or Functional acknowledgment (if configured).</span></span>
  * <span data-ttu-id="9fa38-156">Техническое подтверждение создается по результатам проверки заголовков.</span><span class="sxs-lookup"><span data-stu-id="9fa38-156">A Technical Acknowledgment generates as a result of header validation.</span></span> <span data-ttu-id="9fa38-157">Техническое подтверждение сообщает о состоянии обработки получателем заголовка и окончания обмена.</span><span class="sxs-lookup"><span data-stu-id="9fa38-157">The technical acknowledgment reports the status of the processing of an interchange header and trailer by the address receiver</span></span>
  * <span data-ttu-id="9fa38-158">Функциональное подтверждение создается по результатам проверки тела сообщения.</span><span class="sxs-lookup"><span data-stu-id="9fa38-158">A Functional Acknowledgment generates as a result of body validation.</span></span> <span data-ttu-id="9fa38-159">Функциональное подтверждение сообщает обо всех ошибках, зарегистрированных при обработке полученного документа.</span><span class="sxs-lookup"><span data-stu-id="9fa38-159">The functional acknowledgment reports each error encountered while processing the received document</span></span>

## <a name="view-the-swagger"></a><span data-ttu-id="9fa38-160">Просмотр Swagger</span><span class="sxs-lookup"><span data-stu-id="9fa38-160">View the swagger</span></span>
<span data-ttu-id="9fa38-161">Ознакомьтесь с [дополнительными сведениями о Swagger](/connectors/x12/).</span><span class="sxs-lookup"><span data-stu-id="9fa38-161">See the [swagger details](/connectors/x12/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="9fa38-162">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9fa38-162">Next steps</span></span>
[<span data-ttu-id="9fa38-163">Обзор пакета интеграции Enterprise</span><span class="sxs-lookup"><span data-stu-id="9fa38-163">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "Обзор пакета интеграции Enterprise") 

