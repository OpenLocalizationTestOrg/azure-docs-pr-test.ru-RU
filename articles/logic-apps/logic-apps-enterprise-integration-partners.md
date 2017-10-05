---
title: "Создание партнеров для сообщений B2B с помощью Azure Logic Apps | Документация Майкрософт"
description: "Узнайте, как добавить партнеры в учетную запись интеграции с помощью Пакета интеграции Enterprise и Logic Apps."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: b179325c-a511-4c1b-9796-f7484b4f6873
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 950cb449b53f400f0f0f860caf5415bbb5212269
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="add-or-update-partners-in-business-to-business-agreements-in-your-workflow"></a><span data-ttu-id="7b191-103">Добавление или обновление партнеров в соглашениях B2B в рабочем процессе</span><span class="sxs-lookup"><span data-stu-id="7b191-103">Add or update partners in business-to-business agreements in your workflow</span></span>

<span data-ttu-id="7b191-104">Партнеры — это сущности, которые участвуют в обмене сообщениями и транзакциях "бизнес — бизнес" (B2B).</span><span class="sxs-lookup"><span data-stu-id="7b191-104">Partners are entities that participate in business-to-business (B2B) transactions and exchange messages between each other.</span></span> <span data-ttu-id="7b191-105">Прежде чем создавать партнеров, которые представляют вас и другую организацию в подобных транзакциях, обе стороны должны обменяться информацией, которая идентифицирует и проверяет сообщения, отправляемые друг другу.</span><span class="sxs-lookup"><span data-stu-id="7b191-105">Before you can create partners that represent you and another organization in these transactions, you must both share information that identifies and validates messages sent by each other.</span></span> <span data-ttu-id="7b191-106">Обсудив все необходимое, можно приступать к реализации взаимодействия "бизнес — бизнес". Для этого вы можете создать в своей учетной записи интеграции партнеров, которые будут представлять обе стороны.</span><span class="sxs-lookup"><span data-stu-id="7b191-106">After you discuss these details and are ready to start your business relationship, you can create partners in your integration account to represent you both.</span></span>

## <a name="what-roles-do-partners-have-in-your-integration-account"></a><span data-ttu-id="7b191-107">Какие роли нужно определить партнерам в учетной записи интеграции?</span><span class="sxs-lookup"><span data-stu-id="7b191-107">What roles do partners have in your integration account?</span></span>

<span data-ttu-id="7b191-108">Для определения сведений о сообщениях, обмен которыми осуществляется между партнерами, создайте соглашения между этими партнерами.</span><span class="sxs-lookup"><span data-stu-id="7b191-108">To define details about the messages exchanged between partners, you create agreements between those partners.</span></span> <span data-ttu-id="7b191-109">Перед созданием соглашения необходимо добавить в свою учетную запись интеграции по крайней мере двух партнеров.</span><span class="sxs-lookup"><span data-stu-id="7b191-109">However, before you can create an agreement, you must have added at least two partners to your integration account.</span></span> <span data-ttu-id="7b191-110">Ваша организация должна быть включена в соглашение как **главный партнер**.</span><span class="sxs-lookup"><span data-stu-id="7b191-110">Your organization must be part of the agreement as the **host partner**.</span></span> <span data-ttu-id="7b191-111">Другой участник (**гостевой партнер**) представляет организацию, которая обменивается сообщениями с вашей организацией.</span><span class="sxs-lookup"><span data-stu-id="7b191-111">The other partner, or **guest partner** represents the organization that exchanges messages with your organization.</span></span> <span data-ttu-id="7b191-112">Гостевым партнером может быть другая компания или даже подразделение вашей организации.</span><span class="sxs-lookup"><span data-stu-id="7b191-112">The guest partner can be another company, or even a department in your own organization.</span></span>

<span data-ttu-id="7b191-113">Добавив этих партнеров, можно приступать к созданию соглашения.</span><span class="sxs-lookup"><span data-stu-id="7b191-113">After you add these partners, you can create an agreement.</span></span>

<span data-ttu-id="7b191-114">Параметры получения и отправки задаются для главного партнера.</span><span class="sxs-lookup"><span data-stu-id="7b191-114">Receive and Send settings are oriented from the point of view of the Hosted Partner.</span></span> <span data-ttu-id="7b191-115">Например, параметры получения в соглашении определяют, как главный партнер получает сообщения от партнера-гостя.</span><span class="sxs-lookup"><span data-stu-id="7b191-115">For example, the receive settings in an agreement determine how the hosted partner receives messages sent from a guest partner.</span></span> <span data-ttu-id="7b191-116">Аналогично параметры отправки в соглашении указывают, как главный партнер отправляет сообщения партнеру-гостю.</span><span class="sxs-lookup"><span data-stu-id="7b191-116">Likewise, the send settings on the agreement indicate how the hosted partner sends messages to the guest partner.</span></span>

## <a name="how-to-create-a-partner"></a><span data-ttu-id="7b191-117">Как создать партнер?</span><span class="sxs-lookup"><span data-stu-id="7b191-117">How to create a partner?</span></span>

1. <span data-ttu-id="7b191-118">На портале Azure щелкните **Обзор**.</span><span class="sxs-lookup"><span data-stu-id="7b191-118">In the Azure portal, select **Browse**.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-1.png)

2. <span data-ttu-id="7b191-119">Введите **интеграция** в поле фильтра поиска, а затем в списке результатов выберите **Учетные записи интеграции**.</span><span class="sxs-lookup"><span data-stu-id="7b191-119">In the filter search box, enter **integration**, then select **Integration Accounts** in the results list.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-2.png)

3. <span data-ttu-id="7b191-120">Выберите учетную запись интеграции, в которую нужно добавить партнеров.</span><span class="sxs-lookup"><span data-stu-id="7b191-120">Select the integration account where you want to add your partners.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-3.png)

4. <span data-ttu-id="7b191-121">Выберите элемент **Партнеры** .</span><span class="sxs-lookup"><span data-stu-id="7b191-121">Select the **Partners** tile.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-1.png)

5. <span data-ttu-id="7b191-122">В колонке "Партнеры" щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="7b191-122">In the Partners blade, choose **Add**.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-2.png)

6. <span data-ttu-id="7b191-123">Укажите имя партнера и выберите **Квалификатор**.</span><span class="sxs-lookup"><span data-stu-id="7b191-123">Enter a name for your partner, then select a **Qualifier**.</span></span> <span data-ttu-id="7b191-124">Наконец, укажите **значение**, которое поможет определять документы, поступающие в ваши приложения.</span><span class="sxs-lookup"><span data-stu-id="7b191-124">Finally, enter a **Value** to help identify documents that come into your apps.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-3.png)

7. <span data-ttu-id="7b191-125">Щелкните значок уведомления (*колокольчик*), чтобы отслеживать ход создания партнера.</span><span class="sxs-lookup"><span data-stu-id="7b191-125">To see the progress for your partner creation process, select the *bell* notification icon.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-4.png)

8. <span data-ttu-id="7b191-126">Чтобы проверить добавление новых партнеров, щелкните плитку **Партнеры**.</span><span class="sxs-lookup"><span data-stu-id="7b191-126">To confirm that your new partners were successfully added, select the **Partners** tile.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-5.png)

    <span data-ttu-id="7b191-127">Щелкнув плитку "Партнеры", вы увидите в одноименной колонке добавленных партнеров.</span><span class="sxs-lookup"><span data-stu-id="7b191-127">After you select the Partners tile, you'll also see  newly added partners in the Partners blade.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-6.png)

## <a name="how-to-edit-existing-partners-in-your-integration-account"></a><span data-ttu-id="7b191-128">Как изменить существующих партнеров в учетной записи интеграции</span><span class="sxs-lookup"><span data-stu-id="7b191-128">How to edit existing partners in your integration account</span></span>

1. <span data-ttu-id="7b191-129">Выберите элемент **Партнеры** .</span><span class="sxs-lookup"><span data-stu-id="7b191-129">Select the **Partners** tile.</span></span>
2. <span data-ttu-id="7b191-130">В открывшейся колонке "Партнеры" выберите партнера, которого нужно изменить.</span><span class="sxs-lookup"><span data-stu-id="7b191-130">After the Partners blade opens, select the partner you want to edit.</span></span>
3. <span data-ttu-id="7b191-131">Внесите необходимые изменения на плитке **Обновление партнера**.</span><span class="sxs-lookup"><span data-stu-id="7b191-131">On the **Update Partner** tile, make your changes.</span></span>
4. <span data-ttu-id="7b191-132">После этого щелкните **Сохранить**. Или отмените внесенные изменения, щелкнув **Отменить**.</span><span class="sxs-lookup"><span data-stu-id="7b191-132">After you're done, choose **Save**, or to cancel your changes, select **Discard**.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/edit-1.png)

## <a name="how-to-delete-a-partner"></a><span data-ttu-id="7b191-133">Как удалить партнер</span><span class="sxs-lookup"><span data-stu-id="7b191-133">How to delete a partner</span></span>

1. <span data-ttu-id="7b191-134">Выберите элемент **Партнеры** .</span><span class="sxs-lookup"><span data-stu-id="7b191-134">Select the **Partners** tile.</span></span>
2. <span data-ttu-id="7b191-135">В открывшейся колонке "Партнеры" выберите партнера, которого нужно удалить.</span><span class="sxs-lookup"><span data-stu-id="7b191-135">After the Partner blade opens, select the partner that you want to delete.</span></span>
3. <span data-ttu-id="7b191-136">Щелкните **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="7b191-136">Choose **Delete**.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/delete-1.png)

## <a name="next-steps"></a><span data-ttu-id="7b191-137">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7b191-137">Next steps</span></span>
* [<span data-ttu-id="7b191-138">Узнайте о соглашениях и Пакете интеграции Enterprise</span><span class="sxs-lookup"><span data-stu-id="7b191-138">Learn more about agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "Узнайте о соглашениях и Пакете интеграции Enterprise")  

