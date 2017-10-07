---
title: "сообщения EDIFACT aaaEncode - приложения логики Azure | Документы Microsoft"
description: "Проверка EDI и формирования XML с помощью кодировщика сообщений EDIFACT в hello пакет интеграции Enterprise для логики приложений Azure"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: 974ac339-d97a-4715-bc92-62d02281e900
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: b3799dbd2492adef597022d017cf28f5ceb1085c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="encode-edifact-messages-for-azure-logic-apps-with-hello-enterprise-integration-pack"></a><span data-ttu-id="9a465-103">Кодирование сообщений EDIFACT для приложения логики Azure с помощью hello пакет интеграции Enterprise</span><span class="sxs-lookup"><span data-stu-id="9a465-103">Encode EDIFACT messages for Azure Logic Apps with hello Enterprise Integration Pack</span></span>

<span data-ttu-id="9a465-104">С соединителем сообщение hello кодирования EDIFACT проверки EDI и свойств, создание XML-документа для каждого набора транзакций и запросить Техническое подтверждение и функциональное подтверждение.</span><span class="sxs-lookup"><span data-stu-id="9a465-104">With hello Encode EDIFACT message connector, you can validate EDI and partner-specific properties, generate an XML document for each transaction set, and request a Technical Acknowledgement, Functional Acknowledgment, or both.</span></span>
<span data-ttu-id="9a465-105">toouse этот соединитель, необходимо добавить существующий триггер в приложении логику tooan соединитель hello.</span><span class="sxs-lookup"><span data-stu-id="9a465-105">toouse this connector, you must add hello connector tooan existing trigger in your logic app.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="9a465-106">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="9a465-106">Before you start</span></span>

<span data-ttu-id="9a465-107">Вот hello необходимых элементов.</span><span class="sxs-lookup"><span data-stu-id="9a465-107">Here's hello items you need:</span></span>

* <span data-ttu-id="9a465-108">Учетная запись Azure. Вы можете создать [бесплатную учетную запись](https://azure.microsoft.com/free).</span><span class="sxs-lookup"><span data-stu-id="9a465-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="9a465-109">[Учетная запись интеграции](logic-apps-enterprise-integration-create-integration-account.md), уже определенная и связанная с подпиской Azure.</span><span class="sxs-lookup"><span data-stu-id="9a465-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="9a465-110">Необходимо иметь соединителя интеграции кодирования EDIFACT hello учетной записи toouse сообщения.</span><span class="sxs-lookup"><span data-stu-id="9a465-110">You must have an integration account toouse hello Encode EDIFACT message connector.</span></span> 
* <span data-ttu-id="9a465-111">В учетной записи интеграции должны быть определены по крайней мере два [партнера](logic-apps-enterprise-integration-partners.md).</span><span class="sxs-lookup"><span data-stu-id="9a465-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="9a465-112">В учетной записи интеграции должно быть определено [соглашение EDIFACT](logic-apps-enterprise-integration-edifact.md).</span><span class="sxs-lookup"><span data-stu-id="9a465-112">An [EDIFACT agreement](logic-apps-enterprise-integration-edifact.md) that's already defined in your integration account</span></span>

## <a name="encode-edifact-messages"></a><span data-ttu-id="9a465-113">Кодирование сообщений EDIFACT</span><span class="sxs-lookup"><span data-stu-id="9a465-113">Encode EDIFACT messages</span></span>

1. <span data-ttu-id="9a465-114">[Создание приложения логики](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="9a465-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="9a465-115">Соединитель сообщения EDIFACT кодирования Hello не имеет триггеры, поэтому ее нужно добавить триггер для запуска приложения логики, как триггер запроса.</span><span class="sxs-lookup"><span data-stu-id="9a465-115">hello Encode EDIFACT message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="9a465-116">В hello конструктор логики приложения добавить триггер и добавьте действие tooyour логику приложения.</span><span class="sxs-lookup"><span data-stu-id="9a465-116">In hello Logic App Designer, add a trigger, and then add an action tooyour logic app.</span></span>

3.  <span data-ttu-id="9a465-117">В поле поиска hello введите «EDIFACT» фильтра.</span><span class="sxs-lookup"><span data-stu-id="9a465-117">In hello search box, enter "EDIFACT" as your filter.</span></span> <span data-ttu-id="9a465-118">Выберите либо **кодирования сообщения EDIFACT, название соглашения** или **Encode tooEDIFACT сообщение с удостоверениями**.</span><span class="sxs-lookup"><span data-stu-id="9a465-118">Select either **Encode EDIFACT Message by agreement name** or **Encode tooEDIFACT message by identities**.</span></span>
   
    ![поиск EDIFACT](media/logic-apps-enterprise-integration-edifact-encode/edifactdecodeimage1.png)  

3. <span data-ttu-id="9a465-120">Если вы еще не создана ранее все подключения учетной записи интеграции tooyour, появится предложение toocreate теперь это подключение.</span><span class="sxs-lookup"><span data-stu-id="9a465-120">If you didn't previously create any connections tooyour integration account, you're prompted toocreate that connection now.</span></span> <span data-ttu-id="9a465-121">Имя подключения и установите hello интеграции учетной записью, которую tooconnect.</span><span class="sxs-lookup"><span data-stu-id="9a465-121">Name your connection, and select hello integration account that you want tooconnect.</span></span>

    ![создание подключения к учетной записи интеграции](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage1.png)  

    <span data-ttu-id="9a465-123">Свойства со звездочкой обязательные.</span><span class="sxs-lookup"><span data-stu-id="9a465-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="9a465-124">Свойство</span><span class="sxs-lookup"><span data-stu-id="9a465-124">Property</span></span> | <span data-ttu-id="9a465-125">Сведения</span><span class="sxs-lookup"><span data-stu-id="9a465-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="9a465-126">Имя подключения*</span><span class="sxs-lookup"><span data-stu-id="9a465-126">Connection Name *</span></span> |<span data-ttu-id="9a465-127">Введите имя подключения</span><span class="sxs-lookup"><span data-stu-id="9a465-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="9a465-128">Учетная запись интеграции*</span><span class="sxs-lookup"><span data-stu-id="9a465-128">Integration Account *</span></span> |<span data-ttu-id="9a465-129">Выберите имя для учетной записи интеграции.</span><span class="sxs-lookup"><span data-stu-id="9a465-129">Enter a name for your integration account.</span></span> <span data-ttu-id="9a465-130">Обеспечить наличие учетной записи и логика приложения интеграции в hello Azure местоположения.</span><span class="sxs-lookup"><span data-stu-id="9a465-130">Make sure that your integration account and logic app are in hello same Azure location.</span></span> |

5.  <span data-ttu-id="9a465-131">После завершения, сведения о соединении с вашей должен выглядеть аналогичный пример toothis.</span><span class="sxs-lookup"><span data-stu-id="9a465-131">When you're done, your connection details should look similar toothis example.</span></span> <span data-ttu-id="9a465-132">toofinish при создании подключения, выберите **создать**.</span><span class="sxs-lookup"><span data-stu-id="9a465-132">toofinish creating your connection, choose **Create**.</span></span>

    ![сведения о подключении к учетной записи интеграции](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage2.png)

    <span data-ttu-id="9a465-134">Подключение создано.</span><span class="sxs-lookup"><span data-stu-id="9a465-134">Your connection is now created.</span></span>

    ![создано подключение к учетной записи интеграции](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage4.png)

#### <a name="encode-edifact-message-by-agreement-name"></a><span data-ttu-id="9a465-136">Кодирование сообщений EDIFACT по названию соглашения</span><span class="sxs-lookup"><span data-stu-id="9a465-136">Encode EDIFACT Message by agreement name</span></span>

<span data-ttu-id="9a465-137">Если вы настроили tooencode сообщения EDIFACT, название соглашения, открыть hello **соглашения имя EDIFACT** введите или выберите имя соглашения EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="9a465-137">If you chose tooencode EDIFACT messages by agreement name, open hello **Name of EDIFACT agreement** list, enter or select your EDIFACT agreement name.</span></span> <span data-ttu-id="9a465-138">Введите tooencode сообщение hello XML.</span><span class="sxs-lookup"><span data-stu-id="9a465-138">Enter hello XML message tooencode.</span></span>

![Введите название соглашения EDIFACT и tooencode сообщения XML](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage6.png)

#### <a name="encode-edifact-message-by-identities"></a><span data-ttu-id="9a465-140">Кодирование сообщения EDIFACT по идентификаторам</span><span class="sxs-lookup"><span data-stu-id="9a465-140">Encode EDIFACT Message by identities</span></span>

<span data-ttu-id="9a465-141">Если выбранное tooencode сообщений EDIFACT удостоверений, введите идентификатор отправителя hello, квалификатор отправителя, идентификатор получателя и квалификатор получателя согласно настройкам в соглашении EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="9a465-141">If you choose tooencode EDIFACT messages by identities, enter hello sender identifier, sender qualifier, receiver identifier, and receiver qualifier as configured in your EDIFACT agreement.</span></span> <span data-ttu-id="9a465-142">Выберите tooencode сообщение hello XML.</span><span class="sxs-lookup"><span data-stu-id="9a465-142">Select hello XML message tooencode.</span></span>

![Введите идентификаторы для отправителя и получателя, выберите tooencode сообщения XML](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage7.png)

## <a name="edifact-encode-details"></a><span data-ttu-id="9a465-144">Сведения о кодировании EDIFACT</span><span class="sxs-lookup"><span data-stu-id="9a465-144">EDIFACT Encode details</span></span>

<span data-ttu-id="9a465-145">Соединитель кодирования EDIFACT Hello выполняет следующие задачи:</span><span class="sxs-lookup"><span data-stu-id="9a465-145">hello Encode EDIFACT connector performs these tasks:</span></span> 

* <span data-ttu-id="9a465-146">Разрешить hello соглашения, сопоставляя квалификатор отправителя hello & идентификатор квалификатор получателя, а и идентификатор</span><span class="sxs-lookup"><span data-stu-id="9a465-146">Resolve hello agreement by matching hello sender qualifier & identifier and receiver qualifier and identifier</span></span>
* <span data-ttu-id="9a465-147">Сериализует hello обмен EDI, преобразование сообщений XML-кодировке в EDI наборов транзакций в сообщении hello.</span><span class="sxs-lookup"><span data-stu-id="9a465-147">Serializes hello EDI interchange, converting XML-encoded messages into EDI transaction sets in hello interchange.</span></span>
* <span data-ttu-id="9a465-148">Генерирует сегменты заголовков и окончаний для наборов транзакций.</span><span class="sxs-lookup"><span data-stu-id="9a465-148">Applies transaction set header and trailer segments</span></span>
* <span data-ttu-id="9a465-149">Создает контрольное число обмена, контрольное число группы и контрольное число набора транзакций для каждого исходящего обмена.</span><span class="sxs-lookup"><span data-stu-id="9a465-149">Generates an interchange control number, a group control number, and a transaction set control number for each outgoing interchange</span></span>
* <span data-ttu-id="9a465-150">Заменяет разделителей в полезных данных hello</span><span class="sxs-lookup"><span data-stu-id="9a465-150">Replaces separators in hello payload data</span></span>
* <span data-ttu-id="9a465-151">Проверяет EDI и свойства для конкретного партнера.</span><span class="sxs-lookup"><span data-stu-id="9a465-151">Validates EDI and partner-specific properties</span></span>
  * <span data-ttu-id="9a465-152">Проверка схемы элементов данных набора транзакций hello по схеме сообщение hello.</span><span class="sxs-lookup"><span data-stu-id="9a465-152">Schema validation of hello transaction-set data elements against hello message schema.</span></span>
  * <span data-ttu-id="9a465-153">Выполняет проверку EDI для элементов данных в наборе транзакций.</span><span class="sxs-lookup"><span data-stu-id="9a465-153">EDI validation performed on transaction-set data elements.</span></span>
  * <span data-ttu-id="9a465-154">Выполняет расширенную проверку для элементов данных в наборе транзакций.</span><span class="sxs-lookup"><span data-stu-id="9a465-154">Extended validation performed on transaction-set data elements</span></span>
* <span data-ttu-id="9a465-155">Создает XML-документ для каждого набора транзакций.</span><span class="sxs-lookup"><span data-stu-id="9a465-155">Generates an XML document for each transaction set.</span></span>
* <span data-ttu-id="9a465-156">Запрашивает техническое и (или) функциональное подтверждение (если настроено).</span><span class="sxs-lookup"><span data-stu-id="9a465-156">Requests a Technical and/or Functional acknowledgment (if configured).</span></span>
  * <span data-ttu-id="9a465-157">Как Техническое подтверждение CONTRL сообщение hello указывает поступления обмена.</span><span class="sxs-lookup"><span data-stu-id="9a465-157">As a technical acknowledgment, hello CONTRL message indicates receipt of an interchange.</span></span>
  * <span data-ttu-id="9a465-158">Как функциональное подтверждение CONTRL сообщение hello указывает принятия или отклонения hello получил сообщение, группы или сообщения, и список ошибок или неподдерживаемых функций</span><span class="sxs-lookup"><span data-stu-id="9a465-158">As a functional acknowledgment, hello CONTRL message indicates acceptance or rejection of hello received interchange, group, or message, with a list of errors or unsupported functionality</span></span>

## <a name="view-swagger-file"></a><span data-ttu-id="9a465-159">Просмотр файла Swagger</span><span class="sxs-lookup"><span data-stu-id="9a465-159">View Swagger file</span></span>
<span data-ttu-id="9a465-160">tooview hello Swagger сведения для соединителя EDIFACT hello, см. [EDIFACT](/connectors/edifact/).</span><span class="sxs-lookup"><span data-stu-id="9a465-160">tooview hello Swagger details for hello EDIFACT connector, see [EDIFACT](/connectors/edifact/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9a465-161">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9a465-161">Next steps</span></span>
[<span data-ttu-id="9a465-162">Дополнительные сведения о hello пакет интеграции Enterprise</span><span class="sxs-lookup"><span data-stu-id="9a465-162">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "Дополнительные сведения о пакет интеграции Enterprise") 

