---
title: "Создание решений B2B в Azure Logic Apps | Документация Майкрософт"
description: "Получение данных в приложениях логики с использованием функций B2B из пакета интеграции Enterprise"
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
ms.openlocfilehash: 0625787ddcbc0091e70b111f687e25929720ad15
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="receive-data-in-logic-apps-with-the-b2b-features-in-the-enterprise-integration-pack"></a><span data-ttu-id="a94ad-103">Получение данных в приложениях логики с помощью функций B2B из пакета интеграции Enterprise</span><span class="sxs-lookup"><span data-stu-id="a94ad-103">Receive data in logic apps with the B2B features in the Enterprise Integration Pack</span></span>

<span data-ttu-id="a94ad-104">После создания учетной записи интеграции, для которой определены партнеры и соглашения, вы сможете с помощью [пакета интеграции Enterprise](logic-apps-enterprise-integration-overview.md) создать рабочий процесс "бизнес — бизнес" (B2B) для приложения логики.</span><span class="sxs-lookup"><span data-stu-id="a94ad-104">After you create an integration account that has partners and agreements, you are ready to create a business to business (B2B) workflow for your logic app with the [Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a94ad-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a94ad-105">Prerequisites</span></span>

<span data-ttu-id="a94ad-106">Чтобы использовать действия AS2 и X12, потребуется учетная запись интеграции Enterprise.</span><span class="sxs-lookup"><span data-stu-id="a94ad-106">To use the AS2 and X12 actions, you must have an Enterprise Integration Account.</span></span> <span data-ttu-id="a94ad-107">Узнайте, [как создать учетную запись интеграции Enterprise](../logic-apps/logic-apps-enterprise-integration-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="a94ad-107">Learn [how to create an Enterprise Integration Account](../logic-apps/logic-apps-enterprise-integration-accounts.md).</span></span>

## <a name="create-a-logic-app-with-b2b-connectors"></a><span data-ttu-id="a94ad-108">Создание приложения логики с помощью соединителей B2B</span><span class="sxs-lookup"><span data-stu-id="a94ad-108">Create a logic app with B2B connectors</span></span>

<span data-ttu-id="a94ad-109">Выполните следующие действия, чтобы создать приложение логики B2B, которое использует действия AS2 и X12 для получения данных от торгового партнера.</span><span class="sxs-lookup"><span data-stu-id="a94ad-109">Follow these steps to create a B2B logic app that uses the AS2 and X12 actions to receive data from a trading partner:</span></span>

1. <span data-ttu-id="a94ad-110">Создайте приложение логики и [свяжите его с учетной записью интеграции](../logic-apps/logic-apps-enterprise-integration-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="a94ad-110">Create a logic app, then [link your app to your integration account](../logic-apps/logic-apps-enterprise-integration-accounts.md).</span></span>

2. <span data-ttu-id="a94ad-111">Добавьте триггер **Request - When an HTTP request is received** (Запрос: при получении HTTP-запроса) в свое приложение логики.</span><span class="sxs-lookup"><span data-stu-id="a94ad-111">Add a **Request - When an HTTP request is received** trigger to your logic app.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/flatfile-1.png)

3. <span data-ttu-id="a94ad-112">Добавьте действие **Decode AS2** (Декодирование AS2), щелкнув **Добавить действие**.</span><span class="sxs-lookup"><span data-stu-id="a94ad-112">To add the **Decode AS2** action, select **Add an action**.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/transform-2.png)

4. <span data-ttu-id="a94ad-113">Введите слово **as2** в поле поиска, чтобы оставить в списке только нужные действия.</span><span class="sxs-lookup"><span data-stu-id="a94ad-113">To filter all actions to the one that you want, enter the word **as2** in the search box.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-5.png)

5. <span data-ttu-id="a94ad-114">Выберите действие **AS2 - Decode AS2 message** (AS2: декодирование сообщений AS2).</span><span class="sxs-lookup"><span data-stu-id="a94ad-114">Select the **AS2 - Decode AS2 message** action.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-6.png)

6. <span data-ttu-id="a94ad-115">Добавьте **текст**, который будет использоваться в качестве входных данных.</span><span class="sxs-lookup"><span data-stu-id="a94ad-115">Add the **Body** that you want to use as input.</span></span> <span data-ttu-id="a94ad-116">Для этого примера выберите текст HTTP-запроса, который активирует приложение логики.</span><span class="sxs-lookup"><span data-stu-id="a94ad-116">In this example, select the body of the HTTP request that triggers the logic app.</span></span> <span data-ttu-id="a94ad-117">Или введите выражение, которое передает заголовки для поля **HEADERS** (Заголовки):</span><span class="sxs-lookup"><span data-stu-id="a94ad-117">Or enter an expression that inputs the headers in the **HEADERS** field:</span></span>

    <span data-ttu-id="a94ad-118">@triggerOutputs()['headers']</span><span class="sxs-lookup"><span data-stu-id="a94ad-118">@triggerOutputs()['headers']</span></span>

7. <span data-ttu-id="a94ad-119">Добавьте необходимые **заголовки** для AS2, которые содержатся в заголовках HTTP-запроса.</span><span class="sxs-lookup"><span data-stu-id="a94ad-119">Add the required **Headers** for AS2, which you can find in the HTTP request headers.</span></span> <span data-ttu-id="a94ad-120">Для этого примера выберите заголовки HTTP-запроса, который активирует приложение логики.</span><span class="sxs-lookup"><span data-stu-id="a94ad-120">In this example, select the headers of the HTTP request that trigger the logic app.</span></span>

8. <span data-ttu-id="a94ad-121">Теперь добавьте действие для декодирования сообщений X12 (Decode X12 message).</span><span class="sxs-lookup"><span data-stu-id="a94ad-121">Now add the Decode X12 message action.</span></span> <span data-ttu-id="a94ad-122">Выберите **Добавить действие**.</span><span class="sxs-lookup"><span data-stu-id="a94ad-122">Select **Add an action**.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-9.png)

9. <span data-ttu-id="a94ad-123">Введите слово **x12** в поле поиска, чтобы оставить в списке только нужные действия.</span><span class="sxs-lookup"><span data-stu-id="a94ad-123">To filter all actions to the one that you want, enter the word **x12** in the search box.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-10.png)

10. <span data-ttu-id="a94ad-124">Выберите действие **X12 - Decode X12 message** (X12: декодирование сообщений X12).</span><span class="sxs-lookup"><span data-stu-id="a94ad-124">Select the **X12 - Decode X12 message** action.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-as2message.png)

11. <span data-ttu-id="a94ad-125">Теперь нужно указать входные данные для этого действия.</span><span class="sxs-lookup"><span data-stu-id="a94ad-125">Now you must specify the input to this action.</span></span> <span data-ttu-id="a94ad-126">Здесь это будут выходные данные предыдущего действия AS2.</span><span class="sxs-lookup"><span data-stu-id="a94ad-126">This input is the output from the previous AS2 action.</span></span>

    <span data-ttu-id="a94ad-127">Содержимое сообщения по сути представляет собой объект JSON в кодировке base64, поэтому в качестве входных данных нужно указать выражение.</span><span class="sxs-lookup"><span data-stu-id="a94ad-127">The actual message content is in a JSON object and is base64 encoded, so you must specify an expression as the input.</span></span> 
    <span data-ttu-id="a94ad-128">В поле ввода **X12 FLAT FILE MESSAGE TO DECODE** (Сообщение для декодирования в формате неструктурированного файла X12) введите следующее выражение:</span><span class="sxs-lookup"><span data-stu-id="a94ad-128">Enter the following expression in the **X12 FLAT FILE MESSAGE TO DECODE** input field:</span></span>
    
    <span data-ttu-id="a94ad-129">@base64ToString(body('Decode_AS2_message')?['AS2Message']?['Content'])</span><span class="sxs-lookup"><span data-stu-id="a94ad-129">@base64ToString(body('Decode_AS2_message')?['AS2Message']?['Content'])</span></span>

    <span data-ttu-id="a94ad-130">Теперь добавьте шаги для декодирования данных X12, полученных от торгового партнера, и вывода элементов в формате объекта JSON.</span><span class="sxs-lookup"><span data-stu-id="a94ad-130">Now add steps to decode the X12 data received from the trading partner and output items in a JSON object.</span></span> 
    <span data-ttu-id="a94ad-131">Чтобы известить партнера о получении данных, можно отправлять ему ответ, содержащий уведомление о состоянии сообщения AS2 (MDN), в действии ответа HTTP.</span><span class="sxs-lookup"><span data-stu-id="a94ad-131">To notify the partner that the data was received, you can send back a response containing the AS2 Message Disposition Notification (MDN) in an HTTP Response Action.</span></span>

12. <span data-ttu-id="a94ad-132">Чтобы добавить действие **Ответ**, щелкните **Добавить действие**.</span><span class="sxs-lookup"><span data-stu-id="a94ad-132">To add the **Response** action, choose **Add an action**.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-14.png)

13. <span data-ttu-id="a94ad-133">Введите слово **response** (ответ) в поле поиска, чтобы оставить в списке только нужные действия.</span><span class="sxs-lookup"><span data-stu-id="a94ad-133">To filter all actions to the one that you want, enter the word **response** in the search box.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-15.png)

14. <span data-ttu-id="a94ad-134">Выберите действие **Response** (Ответ).</span><span class="sxs-lookup"><span data-stu-id="a94ad-134">Select the **Response** action.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-16.png)

15. <span data-ttu-id="a94ad-135">Чтобы использовать MDN из выходных данных действия **Decode X12 message** (Декодирование сообщения X12), в качестве значения для поля **BODY** (Текст) укажите следующее выражение:</span><span class="sxs-lookup"><span data-stu-id="a94ad-135">To access the MDN from the output of the **Decode X12 message** action, set the response **BODY** field with this expression:</span></span>

    <span data-ttu-id="a94ad-136">@base64ToString(body('Decode_AS2_message')?['OutgoingMdn']?['Content'])</span><span class="sxs-lookup"><span data-stu-id="a94ad-136">@base64ToString(body('Decode_AS2_message')?['OutgoingMdn']?['Content'])</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-17.png)  

16. <span data-ttu-id="a94ad-137">Сохраните результаты своих действий.</span><span class="sxs-lookup"><span data-stu-id="a94ad-137">Save your work.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/transform-5.png)  

<span data-ttu-id="a94ad-138">Настройка приложения логики B2B завершена.</span><span class="sxs-lookup"><span data-stu-id="a94ad-138">You are now done setting up your B2B logic app.</span></span> <span data-ttu-id="a94ad-139">В настоящем приложении вам нужно будет сохранить декодированные данные X12 в бизнес-приложении или в хранилище данных.</span><span class="sxs-lookup"><span data-stu-id="a94ad-139">In a real world application, you might want to store the decoded X12 data in a line-of-business (LOB) app or data store.</span></span> <span data-ttu-id="a94ad-140">Для подключения к своим бизнес-приложениям и использования этих API-интерфейсов в приложении логики вы можете добавить дополнительные действия или создать пользовательские API.</span><span class="sxs-lookup"><span data-stu-id="a94ad-140">To connect your own LOB apps and use these APIs in your logic app, you can add further actions or write custom APIs.</span></span>

## <a name="features-and-use-cases"></a><span data-ttu-id="a94ad-141">Функции и варианты использования</span><span class="sxs-lookup"><span data-stu-id="a94ad-141">Features and use cases</span></span>

* <span data-ttu-id="a94ad-142">Действия кодирования и декодирования AS2 и X12 позволяют передавать данные между торговыми партнерами в приложениях логики с использованием стандартных протоколов.</span><span class="sxs-lookup"><span data-stu-id="a94ad-142">The AS2 and X12 decode and encode actions let you exchange data between trading partners by using industry standard protocols in logic apps.</span></span>
* <span data-ttu-id="a94ad-143">AS2 и X12 можно использовать вместе или по отдельности для обмена данными с торговыми партнерами.</span><span class="sxs-lookup"><span data-stu-id="a94ad-143">To exchange data with trading partners, you can use AS2 and X12 with or without each other.</span></span>
* <span data-ttu-id="a94ad-144">Действия B2B упрощают создание партнеров и соглашений в учетной записи интеграции и их использование в приложениях логики.</span><span class="sxs-lookup"><span data-stu-id="a94ad-144">The B2B actions help you create partners and agreements easily in your integration account and consume them in a logic app.</span></span>
* <span data-ttu-id="a94ad-145">Вы можете дополнительно расширить возможности приложения логики, настроив обмен данными с другими приложениями и службами, например Salesforce.</span><span class="sxs-lookup"><span data-stu-id="a94ad-145">When you extend your logic app with other actions, you can send and receive data between other apps and services like SalesForce.</span></span>

## <a name="learn-more"></a><span data-ttu-id="a94ad-146">Подробнее</span><span class="sxs-lookup"><span data-stu-id="a94ad-146">Learn more</span></span>
[<span data-ttu-id="a94ad-147">Обзор Пакета интеграции Enterprise</span><span class="sxs-lookup"><span data-stu-id="a94ad-147">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md)
