---
title: "решения aaaCreate B2B - приложения логики Azure | Документы Microsoft"
description: "Получение данных в приложениях для логики с помощью функций hello B2B в hello пакет интеграции Enterprise"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: 20fc3722-6f8b-402f-b391-b84e9df6fcff
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 8f01318a0415d81c37b216f9b991c060edec2053
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="receive-data-in-logic-apps-with-hello-b2b-features-in-hello-enterprise-integration-pack"></a><span data-ttu-id="3bb30-103">Получение данных в приложениях для логики с функциями B2B hello в hello пакет интеграции Enterprise</span><span class="sxs-lookup"><span data-stu-id="3bb30-103">Receive data in logic apps with hello B2B features in hello Enterprise Integration Pack</span></span>

<span data-ttu-id="3bb30-104">После создания учетной записи интеграции с партнерами и соглашениями, будут готовы toocreate toobusiness (B2B) рабочий процесс для логики приложения с hello [пакет интеграции Enterprise](logic-apps-enterprise-integration-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3bb30-104">After you create an integration account that has partners and agreements, you are ready toocreate a business toobusiness (B2B) workflow for your logic app with hello [Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3bb30-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="3bb30-105">Prerequisites</span></span>

<span data-ttu-id="3bb30-106">toouse Здравствуйте, AS2 и X12 действия, необходимо иметь учетную запись интеграции Enterprise.</span><span class="sxs-lookup"><span data-stu-id="3bb30-106">toouse hello AS2 and X12 actions, you must have an Enterprise Integration Account.</span></span> <span data-ttu-id="3bb30-107">Дополнительные сведения [toocreate интеграцию учетной записи](../logic-apps/logic-apps-enterprise-integration-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="3bb30-107">Learn [how toocreate an Enterprise Integration Account](../logic-apps/logic-apps-enterprise-integration-accounts.md).</span></span>

## <a name="create-a-logic-app-with-b2b-connectors"></a><span data-ttu-id="3bb30-108">Создание приложения логики с помощью соединителей B2B</span><span class="sxs-lookup"><span data-stu-id="3bb30-108">Create a logic app with B2B connectors</span></span>

<span data-ttu-id="3bb30-109">Выполните эти шаги toocreate B2B приложения логики, использующий hello AS2 и X12 действия tooreceive данных от торгового партнера:</span><span class="sxs-lookup"><span data-stu-id="3bb30-109">Follow these steps toocreate a B2B logic app that uses hello AS2 and X12 actions tooreceive data from a trading partner:</span></span>

1. <span data-ttu-id="3bb30-110">Создание приложения логики, затем [связать свою учетную запись интеграции приложения tooyour](../logic-apps/logic-apps-enterprise-integration-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="3bb30-110">Create a logic app, then [link your app tooyour integration account](../logic-apps/logic-apps-enterprise-integration-accounts.md).</span></span>

2. <span data-ttu-id="3bb30-111">Добавить **запрос — при HTTP-запрос получен** триггер tooyour логику приложения.</span><span class="sxs-lookup"><span data-stu-id="3bb30-111">Add a **Request - When an HTTP request is received** trigger tooyour logic app.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/flatfile-1.png)

3. <span data-ttu-id="3bb30-112">tooadd hello **декодировать AS2** действия, выберите **добавить действие**.</span><span class="sxs-lookup"><span data-stu-id="3bb30-112">tooadd hello **Decode AS2** action, select **Add an action**.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/transform-2.png)

4. <span data-ttu-id="3bb30-113">toofilter все toohello действия, который вы хотите ввести слово hello **as2** в поле поиска hello.</span><span class="sxs-lookup"><span data-stu-id="3bb30-113">toofilter all actions toohello one that you want, enter hello word **as2** in hello search box.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-5.png)

5. <span data-ttu-id="3bb30-114">Выберите hello **AS2 - сообщения AS2 декодировать** действие.</span><span class="sxs-lookup"><span data-stu-id="3bb30-114">Select hello **AS2 - Decode AS2 message** action.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-6.png)

6. <span data-ttu-id="3bb30-115">Добавить hello **текст** , которые должны toouse в качестве входных данных.</span><span class="sxs-lookup"><span data-stu-id="3bb30-115">Add hello **Body** that you want toouse as input.</span></span> <span data-ttu-id="3bb30-116">В этом примере выберите текст hello hello HTTP-запроса, что триггеры hello приложения логики.</span><span class="sxs-lookup"><span data-stu-id="3bb30-116">In this example, select hello body of hello HTTP request that triggers hello logic app.</span></span> <span data-ttu-id="3bb30-117">Или введите выражение, которое получает на входе заголовки hello в hello **ЗАГОЛОВКИ** поля:</span><span class="sxs-lookup"><span data-stu-id="3bb30-117">Or enter an expression that inputs hello headers in hello **HEADERS** field:</span></span>

    <span data-ttu-id="3bb30-118">@triggerOutputs()['headers']</span><span class="sxs-lookup"><span data-stu-id="3bb30-118">@triggerOutputs()['headers']</span></span>

7. <span data-ttu-id="3bb30-119">Добавьте необходимые hello **заголовки** для AS2, который можно найти в заголовках hello HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="3bb30-119">Add hello required **Headers** for AS2, which you can find in hello HTTP request headers.</span></span> <span data-ttu-id="3bb30-120">В этом примере выберите hello заголовки HTTP-запроса hello этого триггера hello логику приложения.</span><span class="sxs-lookup"><span data-stu-id="3bb30-120">In this example, select hello headers of hello HTTP request that trigger hello logic app.</span></span>

8. <span data-ttu-id="3bb30-121">Теперь добавьте действие сообщения hello декодирования X12.</span><span class="sxs-lookup"><span data-stu-id="3bb30-121">Now add hello Decode X12 message action.</span></span> <span data-ttu-id="3bb30-122">Выберите **Добавить действие**.</span><span class="sxs-lookup"><span data-stu-id="3bb30-122">Select **Add an action**.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-9.png)

9. <span data-ttu-id="3bb30-123">toofilter все toohello действия, который вы хотите ввести слово hello **x12** в поле поиска hello.</span><span class="sxs-lookup"><span data-stu-id="3bb30-123">toofilter all actions toohello one that you want, enter hello word **x12** in hello search box.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-10.png)

10. <span data-ttu-id="3bb30-124">Выберите hello **X12-декодирование X12 сообщение** действие.</span><span class="sxs-lookup"><span data-stu-id="3bb30-124">Select hello **X12 - Decode X12 message** action.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-as2message.png)

11. <span data-ttu-id="3bb30-125">Теперь необходимо указать входной toothis действие hello.</span><span class="sxs-lookup"><span data-stu-id="3bb30-125">Now you must specify hello input toothis action.</span></span> <span data-ttu-id="3bb30-126">Входные данные — hello выходные данные предыдущего действия AS2 hello.</span><span class="sxs-lookup"><span data-stu-id="3bb30-126">This input is hello output from hello previous AS2 action.</span></span>

    <span data-ttu-id="3bb30-127">содержимое фактическое сообщение Hello объекта JSON и имеет кодировку base64, поэтому необходимо указать выражение в качестве входного hello.</span><span class="sxs-lookup"><span data-stu-id="3bb30-127">hello actual message content is in a JSON object and is base64 encoded, so you must specify an expression as hello input.</span></span> 
    <span data-ttu-id="3bb30-128">Введите следующее выражение в hello hello **X12 НЕСТРУКТУРИРОВАННОГО файла сообщения tooDECODE** поля ввода:</span><span class="sxs-lookup"><span data-stu-id="3bb30-128">Enter hello following expression in hello **X12 FLAT FILE MESSAGE tooDECODE** input field:</span></span>
    
    <span data-ttu-id="3bb30-129">@base64ToString(body('Decode_AS2_message')?['AS2Message']?['Content'])</span><span class="sxs-lookup"><span data-stu-id="3bb30-129">@base64ToString(body('Decode_AS2_message')?['AS2Message']?['Content'])</span></span>

    <span data-ttu-id="3bb30-130">Теперь добавьте шаги toodecode hello X12 данных получено от торгового партнера hello и выходных элементов в объекте JSON.</span><span class="sxs-lookup"><span data-stu-id="3bb30-130">Now add steps toodecode hello X12 data received from hello trading partner and output items in a JSON object.</span></span> 
    <span data-ttu-id="3bb30-131">Получено toonotify hello партнера, который hello данных, можно отправить обратно ответ, содержащий hello AS2 сообщения метода обработки уведомления (MDN) в действие ответа HTTP.</span><span class="sxs-lookup"><span data-stu-id="3bb30-131">toonotify hello partner that hello data was received, you can send back a response containing hello AS2 Message Disposition Notification (MDN) in an HTTP Response Action.</span></span>

12. <span data-ttu-id="3bb30-132">tooadd hello **ответ** действия, выберите **добавить действие**.</span><span class="sxs-lookup"><span data-stu-id="3bb30-132">tooadd hello **Response** action, choose **Add an action**.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-14.png)

13. <span data-ttu-id="3bb30-133">toofilter все toohello действия, который вы хотите ввести слово hello **ответ** в поле поиска hello.</span><span class="sxs-lookup"><span data-stu-id="3bb30-133">toofilter all actions toohello one that you want, enter hello word **response** in hello search box.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-15.png)

14. <span data-ttu-id="3bb30-134">Выберите hello **ответ** действие.</span><span class="sxs-lookup"><span data-stu-id="3bb30-134">Select hello **Response** action.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-16.png)

15. <span data-ttu-id="3bb30-135">tooaccess hello MDN из вывода hello hello **сообщение декодирования X12** действие, hello ответ набора **текст** поля в этом выражении:</span><span class="sxs-lookup"><span data-stu-id="3bb30-135">tooaccess hello MDN from hello output of hello **Decode X12 message** action, set hello response **BODY** field with this expression:</span></span>

    <span data-ttu-id="3bb30-136">@base64ToString(body('Decode_AS2_message')?['OutgoingMdn']?['Content'])</span><span class="sxs-lookup"><span data-stu-id="3bb30-136">@base64ToString(body('Decode_AS2_message')?['OutgoingMdn']?['Content'])</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-17.png)  

16. <span data-ttu-id="3bb30-137">Сохраните результаты своих действий.</span><span class="sxs-lookup"><span data-stu-id="3bb30-137">Save your work.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/transform-5.png)  

<span data-ttu-id="3bb30-138">Настройка приложения логики B2B завершена.</span><span class="sxs-lookup"><span data-stu-id="3bb30-138">You are now done setting up your B2B logic app.</span></span> <span data-ttu-id="3bb30-139">Такого приложения может потребоваться toostore hello декодировать X12 данных в хранилище данных или приложение бизнес-(LOB).</span><span class="sxs-lookup"><span data-stu-id="3bb30-139">In a real world application, you might want toostore hello decoded X12 data in a line-of-business (LOB) app or data store.</span></span> <span data-ttu-id="3bb30-140">tooconnect собственные бизнес-приложений и использовать эти API-интерфейсы в приложение логику, можно добавить дополнительные действия или писать пользовательские API.</span><span class="sxs-lookup"><span data-stu-id="3bb30-140">tooconnect your own LOB apps and use these APIs in your logic app, you can add further actions or write custom APIs.</span></span>

## <a name="features-and-use-cases"></a><span data-ttu-id="3bb30-141">Функции и варианты использования</span><span class="sxs-lookup"><span data-stu-id="3bb30-141">Features and use cases</span></span>

* <span data-ttu-id="3bb30-142">Hello AS2 X12 декодирования и кодирования действия позволяют обмен данными между торговыми партнерами с помощью стандартных отраслевых протоколов в логике приложения.</span><span class="sxs-lookup"><span data-stu-id="3bb30-142">hello AS2 and X12 decode and encode actions let you exchange data between trading partners by using industry standard protocols in logic apps.</span></span>
* <span data-ttu-id="3bb30-143">tooexchange данных с торговыми партнерами, можно использовать AS2 и X12 с или без друг с другом.</span><span class="sxs-lookup"><span data-stu-id="3bb30-143">tooexchange data with trading partners, you can use AS2 and X12 with or without each other.</span></span>
* <span data-ttu-id="3bb30-144">Hello B2B действия позволяют легко создавать партнеров и соглашений в вашей учетной записи интеграции и использовать их в приложение логики.</span><span class="sxs-lookup"><span data-stu-id="3bb30-144">hello B2B actions help you create partners and agreements easily in your integration account and consume them in a logic app.</span></span>
* <span data-ttu-id="3bb30-145">Вы можете дополнительно расширить возможности приложения логики, настроив обмен данными с другими приложениями и службами, например Salesforce.</span><span class="sxs-lookup"><span data-stu-id="3bb30-145">When you extend your logic app with other actions, you can send and receive data between other apps and services like SalesForce.</span></span>

## <a name="learn-more"></a><span data-ttu-id="3bb30-146">Подробнее</span><span class="sxs-lookup"><span data-stu-id="3bb30-146">Learn more</span></span>
[<span data-ttu-id="3bb30-147">Дополнительные сведения о hello пакет интеграции Enterprise</span><span class="sxs-lookup"><span data-stu-id="3bb30-147">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md)
