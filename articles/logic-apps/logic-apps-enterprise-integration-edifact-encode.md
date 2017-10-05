---
title: "Кодирование сообщений EDIFACT в Azure Logic Apps | Документация Майкрософт"
description: "Проверка EDI и создание XML-сообщений с помощью кодировщика сообщений EDIFACT в пакете интеграции Enterprise для Azure Logic Apps"
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
ms.openlocfilehash: b8d577326d23ec45cb4a9ec0e450ebf7afd945f3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="encode-edifact-messages-for-azure-logic-apps-with-the-enterprise-integration-pack"></a><span data-ttu-id="c72dd-103">Кодирование сообщений EDIFACT для Azure Logic Apps с помощью пакета интеграции Enterprise</span><span class="sxs-lookup"><span data-stu-id="c72dd-103">Encode EDIFACT messages for Azure Logic Apps with the Enterprise Integration Pack</span></span>

<span data-ttu-id="c72dd-104">С помощью соединителя для кодирования сообщений EDIFACT вы можете проверить EDI и свойства для конкретного партнера, создать XML-документ для каждого набора транзакций и запросить техническое и (или) функциональное подтверждение.</span><span class="sxs-lookup"><span data-stu-id="c72dd-104">With the Encode EDIFACT message connector, you can validate EDI and partner-specific properties, generate an XML document for each transaction set, and request a Technical Acknowledgement, Functional Acknowledgment, or both.</span></span>
<span data-ttu-id="c72dd-105">Чтобы использовать этот соединитель, добавьте его в существующий триггер в приложении логики.</span><span class="sxs-lookup"><span data-stu-id="c72dd-105">To use this connector, you must add the connector to an existing trigger in your logic app.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="c72dd-106">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="c72dd-106">Before you start</span></span>

<span data-ttu-id="c72dd-107">Вам понадобится следующее:</span><span class="sxs-lookup"><span data-stu-id="c72dd-107">Here's the items you need:</span></span>

* <span data-ttu-id="c72dd-108">Учетная запись Azure. Вы можете создать [бесплатную учетную запись](https://azure.microsoft.com/free).</span><span class="sxs-lookup"><span data-stu-id="c72dd-108">An Azure account; you can create a [free account](https://azure.microsoft.com/free)</span></span>
* <span data-ttu-id="c72dd-109">[Учетная запись интеграции](logic-apps-enterprise-integration-create-integration-account.md), уже определенная и связанная с подпиской Azure.</span><span class="sxs-lookup"><span data-stu-id="c72dd-109">An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription.</span></span> <span data-ttu-id="c72dd-110">Для работы с соединителем для кодирования сообщений EDIFACT потребуется учетная запись интеграции.</span><span class="sxs-lookup"><span data-stu-id="c72dd-110">You must have an integration account to use the Encode EDIFACT message connector.</span></span> 
* <span data-ttu-id="c72dd-111">В учетной записи интеграции должны быть определены по крайней мере два [партнера](logic-apps-enterprise-integration-partners.md).</span><span class="sxs-lookup"><span data-stu-id="c72dd-111">At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account</span></span>
* <span data-ttu-id="c72dd-112">В учетной записи интеграции должно быть определено [соглашение EDIFACT](logic-apps-enterprise-integration-edifact.md).</span><span class="sxs-lookup"><span data-stu-id="c72dd-112">An [EDIFACT agreement](logic-apps-enterprise-integration-edifact.md) that's already defined in your integration account</span></span>

## <a name="encode-edifact-messages"></a><span data-ttu-id="c72dd-113">Кодирование сообщений EDIFACT</span><span class="sxs-lookup"><span data-stu-id="c72dd-113">Encode EDIFACT messages</span></span>

1. <span data-ttu-id="c72dd-114">[Создание приложения логики](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="c72dd-114">[Create a logic app](logic-apps-create-a-logic-app.md).</span></span>

2. <span data-ttu-id="c72dd-115">В соединителе для кодирования сообщений EDIFACT нет триггеров, поэтому вам придется добавить триггер, чтобы запустить приложение логики (например, триггер запроса).</span><span class="sxs-lookup"><span data-stu-id="c72dd-115">The Encode EDIFACT message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger.</span></span> <span data-ttu-id="c72dd-116">В конструкторе приложений логики добавьте триггер, а затем добавьте действие в приложение логики.</span><span class="sxs-lookup"><span data-stu-id="c72dd-116">In the Logic App Designer, add a trigger, and then add an action to your logic app.</span></span>

3.  <span data-ttu-id="c72dd-117">В поле поиска введите "EDIFACT" в качестве фильтра.</span><span class="sxs-lookup"><span data-stu-id="c72dd-117">In the search box, enter "EDIFACT" as your filter.</span></span> <span data-ttu-id="c72dd-118">Выберите пункт **Encode EDIFACT Message by agreement name** (Кодирование сообщения EDIFACT по имени соглашения) или **Encode to EDIFACT message by identities** (Кодирование сообщения EDIFACT по идентификаторам).</span><span class="sxs-lookup"><span data-stu-id="c72dd-118">Select either **Encode EDIFACT Message by agreement name** or **Encode to EDIFACT message by identities**.</span></span>
   
    ![поиск EDIFACT](media/logic-apps-enterprise-integration-edifact-encode/edifactdecodeimage1.png)  

3. <span data-ttu-id="c72dd-120">Если ранее вы не создавали подключения к учетной записи интеграции, вам будет предложено сделать это сейчас.</span><span class="sxs-lookup"><span data-stu-id="c72dd-120">If you didn't previously create any connections to your integration account, you're prompted to create that connection now.</span></span> <span data-ttu-id="c72dd-121">Присвойте подключению имя и выберите учетную запись интеграции, которую следует подключить.</span><span class="sxs-lookup"><span data-stu-id="c72dd-121">Name your connection, and select the integration account that you want to connect.</span></span>

    ![создание подключения к учетной записи интеграции](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage1.png)  

    <span data-ttu-id="c72dd-123">Свойства со звездочкой обязательные.</span><span class="sxs-lookup"><span data-stu-id="c72dd-123">Properties with an asterisk are required.</span></span>

    | <span data-ttu-id="c72dd-124">Свойство</span><span class="sxs-lookup"><span data-stu-id="c72dd-124">Property</span></span> | <span data-ttu-id="c72dd-125">Сведения</span><span class="sxs-lookup"><span data-stu-id="c72dd-125">Details</span></span> |
    | --- | --- |
    | <span data-ttu-id="c72dd-126">Имя подключения*</span><span class="sxs-lookup"><span data-stu-id="c72dd-126">Connection Name *</span></span> |<span data-ttu-id="c72dd-127">Введите имя подключения</span><span class="sxs-lookup"><span data-stu-id="c72dd-127">Enter any name for your connection.</span></span> |
    | <span data-ttu-id="c72dd-128">Учетная запись интеграции*</span><span class="sxs-lookup"><span data-stu-id="c72dd-128">Integration Account *</span></span> |<span data-ttu-id="c72dd-129">Выберите имя для учетной записи интеграции.</span><span class="sxs-lookup"><span data-stu-id="c72dd-129">Enter a name for your integration account.</span></span> <span data-ttu-id="c72dd-130">Убедитесь, что учетная запись интеграции и приложение логики находятся в одном регионе Azure.</span><span class="sxs-lookup"><span data-stu-id="c72dd-130">Make sure that your integration account and logic app are in the same Azure location.</span></span> |

5.  <span data-ttu-id="c72dd-131">Когда все будет готово, данные для подключения должны выглядеть примерно так, как показано в примере.</span><span class="sxs-lookup"><span data-stu-id="c72dd-131">When you're done, your connection details should look similar to this example.</span></span> <span data-ttu-id="c72dd-132">Чтобы завершить создание подключения, нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="c72dd-132">To finish creating your connection, choose **Create**.</span></span>

    ![сведения о подключении к учетной записи интеграции](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage2.png)

    <span data-ttu-id="c72dd-134">Подключение создано.</span><span class="sxs-lookup"><span data-stu-id="c72dd-134">Your connection is now created.</span></span>

    ![создано подключение к учетной записи интеграции](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage4.png)

#### <a name="encode-edifact-message-by-agreement-name"></a><span data-ttu-id="c72dd-136">Кодирование сообщений EDIFACT по названию соглашения</span><span class="sxs-lookup"><span data-stu-id="c72dd-136">Encode EDIFACT Message by agreement name</span></span>

<span data-ttu-id="c72dd-137">Если вы решили закодировать сообщения EDIFACT по имени соглашения, откройте список **имен соглашений EDIFACT** и введите или выберите свое имя соглашения EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="c72dd-137">If you chose to encode EDIFACT messages by agreement name, open the **Name of EDIFACT agreement** list, enter or select your EDIFACT agreement name.</span></span> <span data-ttu-id="c72dd-138">Введите XML-сообщение для кодирования.</span><span class="sxs-lookup"><span data-stu-id="c72dd-138">Enter the XML message to encode.</span></span>

![Введите имя соглашения EDIFACT и XML-сообщение для кодирования.](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage6.png)

#### <a name="encode-edifact-message-by-identities"></a><span data-ttu-id="c72dd-140">Кодирование сообщения EDIFACT по идентификаторам</span><span class="sxs-lookup"><span data-stu-id="c72dd-140">Encode EDIFACT Message by identities</span></span>

<span data-ttu-id="c72dd-141">Если вы выбрали кодирование сообщения EDIFACT по идентификатору, введите идентификатор отправителя, квалификатор отправителя, идентификатор получателя и квалификатор получателя, как указано в соглашении EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="c72dd-141">If you choose to encode EDIFACT messages by identities, enter the sender identifier, sender qualifier, receiver identifier, and receiver qualifier as configured in your EDIFACT agreement.</span></span> <span data-ttu-id="c72dd-142">Выберите XML-сообщение для кодирования.</span><span class="sxs-lookup"><span data-stu-id="c72dd-142">Select the XML message to encode.</span></span>

![Указание идентификаторов отправителя и получателя, выбор XML-сообщения для кодирования](media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage7.png)

## <a name="edifact-encode-details"></a><span data-ttu-id="c72dd-144">Сведения о кодировании EDIFACT</span><span class="sxs-lookup"><span data-stu-id="c72dd-144">EDIFACT Encode details</span></span>

<span data-ttu-id="c72dd-145">Соединитель для кодирования EDIFACT выполняет следующие задачи.</span><span class="sxs-lookup"><span data-stu-id="c72dd-145">The Encode EDIFACT connector performs these tasks:</span></span> 

* <span data-ttu-id="c72dd-146">Определяет соглашение, сопоставляя квалификатор и идентификатор отправителя с квалификатором и идентификатором получателя.</span><span class="sxs-lookup"><span data-stu-id="c72dd-146">Resolve the agreement by matching the sender qualifier & identifier and receiver qualifier and identifier</span></span>
* <span data-ttu-id="c72dd-147">Сериализует обмен EDI путем преобразования сообщения в кодировке XML в набор транзакций EDI.</span><span class="sxs-lookup"><span data-stu-id="c72dd-147">Serializes the EDI interchange, converting XML-encoded messages into EDI transaction sets in the interchange.</span></span>
* <span data-ttu-id="c72dd-148">Генерирует сегменты заголовков и окончаний для наборов транзакций.</span><span class="sxs-lookup"><span data-stu-id="c72dd-148">Applies transaction set header and trailer segments</span></span>
* <span data-ttu-id="c72dd-149">Создает контрольное число обмена, контрольное число группы и контрольное число набора транзакций для каждого исходящего обмена.</span><span class="sxs-lookup"><span data-stu-id="c72dd-149">Generates an interchange control number, a group control number, and a transaction set control number for each outgoing interchange</span></span>
* <span data-ttu-id="c72dd-150">Заменяет разделители в полезных данных.</span><span class="sxs-lookup"><span data-stu-id="c72dd-150">Replaces separators in the payload data</span></span>
* <span data-ttu-id="c72dd-151">Проверяет EDI и свойства для конкретного партнера.</span><span class="sxs-lookup"><span data-stu-id="c72dd-151">Validates EDI and partner-specific properties</span></span>
  * <span data-ttu-id="c72dd-152">Проверяет схемы элементов данных в наборе транзакций на соответствие схеме сообщения.</span><span class="sxs-lookup"><span data-stu-id="c72dd-152">Schema validation of the transaction-set data elements against the message schema.</span></span>
  * <span data-ttu-id="c72dd-153">Выполняет проверку EDI для элементов данных в наборе транзакций.</span><span class="sxs-lookup"><span data-stu-id="c72dd-153">EDI validation performed on transaction-set data elements.</span></span>
  * <span data-ttu-id="c72dd-154">Выполняет расширенную проверку для элементов данных в наборе транзакций.</span><span class="sxs-lookup"><span data-stu-id="c72dd-154">Extended validation performed on transaction-set data elements</span></span>
* <span data-ttu-id="c72dd-155">Создает XML-документ для каждого набора транзакций.</span><span class="sxs-lookup"><span data-stu-id="c72dd-155">Generates an XML document for each transaction set.</span></span>
* <span data-ttu-id="c72dd-156">Запрашивает техническое и (или) функциональное подтверждение (если настроено).</span><span class="sxs-lookup"><span data-stu-id="c72dd-156">Requests a Technical and/or Functional acknowledgment (if configured).</span></span>
  * <span data-ttu-id="c72dd-157">Техническим подтверждением является сообщение CONTRL, сообщающее о получении обмена.</span><span class="sxs-lookup"><span data-stu-id="c72dd-157">As a technical acknowledgment, the CONTRL message indicates receipt of an interchange.</span></span>
  * <span data-ttu-id="c72dd-158">Функциональным подтверждением является сообщение CONTRL, информирующее о принятии или отклонении полученного обмена, отдельной группы или сообщения, и содержащее список ошибок или неподдерживаемых функциональных возможностей.</span><span class="sxs-lookup"><span data-stu-id="c72dd-158">As a functional acknowledgment, the CONTRL message indicates acceptance or rejection of the received interchange, group, or message, with a list of errors or unsupported functionality</span></span>

## <a name="view-swagger-file"></a><span data-ttu-id="c72dd-159">Просмотр файла Swagger</span><span class="sxs-lookup"><span data-stu-id="c72dd-159">View Swagger file</span></span>
<span data-ttu-id="c72dd-160">Дополнительные сведения о Swagger для соединителя EDIFACT см.в [этой статье](/connectors/edifact/).</span><span class="sxs-lookup"><span data-stu-id="c72dd-160">To view the Swagger details for the EDIFACT connector, see [EDIFACT](/connectors/edifact/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c72dd-161">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c72dd-161">Next steps</span></span>
[<span data-ttu-id="c72dd-162">Обзор пакета интеграции Enterprise</span><span class="sxs-lookup"><span data-stu-id="c72dd-162">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "Обзор пакета интеграции Enterprise") 

