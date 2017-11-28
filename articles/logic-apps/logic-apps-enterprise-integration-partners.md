---
title: "партнеры aaaCreate для сообщения о бизнес бизнес (B2B) — приложения логики Azure | Документы Microsoft"
description: "Узнайте, как учетной записи tooadd партнеров tooyour интеграции с приложениями логики и hello пакет интеграции Enterprise"
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
ms.openlocfilehash: 8dc70a8f441fcf228ed178029dcdbac940d794b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-or-update-partners-in-business-to-business-agreements-in-your-workflow"></a><span data-ttu-id="74bf3-103">Добавление или обновление партнеров в соглашениях B2B в рабочем процессе</span><span class="sxs-lookup"><span data-stu-id="74bf3-103">Add or update partners in business-to-business agreements in your workflow</span></span>

<span data-ttu-id="74bf3-104">Партнеры — это сущности, которые участвуют в обмене сообщениями и транзакциях "бизнес — бизнес" (B2B).</span><span class="sxs-lookup"><span data-stu-id="74bf3-104">Partners are entities that participate in business-to-business (B2B) transactions and exchange messages between each other.</span></span> <span data-ttu-id="74bf3-105">Прежде чем создавать партнеров, которые представляют вас и другую организацию в подобных транзакциях, обе стороны должны обменяться информацией, которая идентифицирует и проверяет сообщения, отправляемые друг другу.</span><span class="sxs-lookup"><span data-stu-id="74bf3-105">Before you can create partners that represent you and another organization in these transactions, you must both share information that identifies and validates messages sent by each other.</span></span> <span data-ttu-id="74bf3-106">После обсуждать эти сведения и будут готовы toostart вашей бизнес-отношения, можно создать партнеров в вашей toorepresent учетной записи интеграции как.</span><span class="sxs-lookup"><span data-stu-id="74bf3-106">After you discuss these details and are ready toostart your business relationship, you can create partners in your integration account toorepresent you both.</span></span>

## <a name="what-roles-do-partners-have-in-your-integration-account"></a><span data-ttu-id="74bf3-107">Какие роли нужно определить партнерам в учетной записи интеграции?</span><span class="sxs-lookup"><span data-stu-id="74bf3-107">What roles do partners have in your integration account?</span></span>

<span data-ttu-id="74bf3-108">toodefine сведения о hello сообщений, передаваемых между партнерами, создание соглашений между этими партнерами.</span><span class="sxs-lookup"><span data-stu-id="74bf3-108">toodefine details about hello messages exchanged between partners, you create agreements between those partners.</span></span> <span data-ttu-id="74bf3-109">Тем не менее прежде чем вы сможете создать соглашение, необходимо добавить учетной записи интеграции tooyour по крайней мере двух участников.</span><span class="sxs-lookup"><span data-stu-id="74bf3-109">However, before you can create an agreement, you must have added at least two partners tooyour integration account.</span></span> <span data-ttu-id="74bf3-110">Вашей организации должен быть частью соглашения hello hello **размещаемый партнер**.</span><span class="sxs-lookup"><span data-stu-id="74bf3-110">Your organization must be part of hello agreement as hello **host partner**.</span></span> <span data-ttu-id="74bf3-111">Здравствуйте, другого участника или **гостевой партнер** представляет hello организации, которая обменивается сообщениями с вашей организацией.</span><span class="sxs-lookup"><span data-stu-id="74bf3-111">hello other partner, or **guest partner** represents hello organization that exchanges messages with your organization.</span></span> <span data-ttu-id="74bf3-112">Hello гостевой партнер может быть другой организации или даже отдел в вашей организации.</span><span class="sxs-lookup"><span data-stu-id="74bf3-112">hello guest partner can be another company, or even a department in your own organization.</span></span>

<span data-ttu-id="74bf3-113">Добавив этих партнеров, можно приступать к созданию соглашения.</span><span class="sxs-lookup"><span data-stu-id="74bf3-113">After you add these partners, you can create an agreement.</span></span>

<span data-ttu-id="74bf3-114">Получать и отправлять параметры, которые направлены с точки зрения hello объекта hello размещаемого партнера.</span><span class="sxs-lookup"><span data-stu-id="74bf3-114">Receive and Send settings are oriented from hello point of view of hello Hosted Partner.</span></span> <span data-ttu-id="74bf3-115">Например, hello параметры получения в соглашении определяют, как размещенные hello партнер получает сообщения, отправленные от гостевого партнера.</span><span class="sxs-lookup"><span data-stu-id="74bf3-115">For example, hello receive settings in an agreement determine how hello hosted partner receives messages sent from a guest partner.</span></span> <span data-ttu-id="74bf3-116">Аналогичным образом параметры отправки hello в соглашении о hello указывают, как размещенные hello партнер отправляет сообщения toohello гостевого партнера.</span><span class="sxs-lookup"><span data-stu-id="74bf3-116">Likewise, hello send settings on hello agreement indicate how hello hosted partner sends messages toohello guest partner.</span></span>

## <a name="how-toocreate-a-partner"></a><span data-ttu-id="74bf3-117">Как toocreate партнером?</span><span class="sxs-lookup"><span data-stu-id="74bf3-117">How toocreate a partner?</span></span>

1. <span data-ttu-id="74bf3-118">В hello портал Azure, выберите **Обзор**.</span><span class="sxs-lookup"><span data-stu-id="74bf3-118">In hello Azure portal, select **Browse**.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-1.png)

2. <span data-ttu-id="74bf3-119">Введите в поле поиска фильтра hello, **интеграции**, а затем выберите **учетные записи службы интеграции** в списке результатов hello.</span><span class="sxs-lookup"><span data-stu-id="74bf3-119">In hello filter search box, enter **integration**, then select **Integration Accounts** in hello results list.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-2.png)

3. <span data-ttu-id="74bf3-120">Выберите место tooadd партнеров учетной записи интеграции hello.</span><span class="sxs-lookup"><span data-stu-id="74bf3-120">Select hello integration account where you want tooadd your partners.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-3.png)

4. <span data-ttu-id="74bf3-121">Выберите hello **партнеров** плитки.</span><span class="sxs-lookup"><span data-stu-id="74bf3-121">Select hello **Partners** tile.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-1.png)

5. <span data-ttu-id="74bf3-122">В колонке hello партнеров выберите **добавить**.</span><span class="sxs-lookup"><span data-stu-id="74bf3-122">In hello Partners blade, choose **Add**.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-2.png)

6. <span data-ttu-id="74bf3-123">Укажите имя партнера и выберите **Квалификатор**.</span><span class="sxs-lookup"><span data-stu-id="74bf3-123">Enter a name for your partner, then select a **Qualifier**.</span></span> <span data-ttu-id="74bf3-124">Наконец, введите **значение** toohelp идентификации документами, полученными от приложений.</span><span class="sxs-lookup"><span data-stu-id="74bf3-124">Finally, enter a **Value** toohelp identify documents that come into your apps.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-3.png)

7. <span data-ttu-id="74bf3-125">Ход выполнения hello toosee для процесса создания партнера, выберите hello *bell* значок уведомления.</span><span class="sxs-lookup"><span data-stu-id="74bf3-125">toosee hello progress for your partner creation process, select hello *bell* notification icon.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-4.png)

8. <span data-ttu-id="74bf3-126">tooconfirm, новый партнеров были успешно добавлен, выберите hello **партнеров** плитки.</span><span class="sxs-lookup"><span data-stu-id="74bf3-126">tooconfirm that your new partners were successfully added, select hello **Partners** tile.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-5.png)

    <span data-ttu-id="74bf3-127">После выбора плитки приветствия партнеров, вы также увидите вновь добавленный партнеров в колонке партнеров hello.</span><span class="sxs-lookup"><span data-stu-id="74bf3-127">After you select hello Partners tile, you'll also see  newly added partners in hello Partners blade.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-6.png)

## <a name="how-tooedit-existing-partners-in-your-integration-account"></a><span data-ttu-id="74bf3-128">Как существующие tooedit партнерам в вашей учетной записи интеграции</span><span class="sxs-lookup"><span data-stu-id="74bf3-128">How tooedit existing partners in your integration account</span></span>

1. <span data-ttu-id="74bf3-129">Выберите hello **партнеров** плитки.</span><span class="sxs-lookup"><span data-stu-id="74bf3-129">Select hello **Partners** tile.</span></span>
2. <span data-ttu-id="74bf3-130">После открытия колонке hello партнеров, выберите требуется tooedit партнера hello.</span><span class="sxs-lookup"><span data-stu-id="74bf3-130">After hello Partners blade opens, select hello partner you want tooedit.</span></span>
3. <span data-ttu-id="74bf3-131">На hello **обновление партнера** плитки, внесите изменения.</span><span class="sxs-lookup"><span data-stu-id="74bf3-131">On hello **Update Partner** tile, make your changes.</span></span>
4. <span data-ttu-id="74bf3-132">После завершения нажмите **Сохранить**, или выберите изменения, toocancel **отменить**.</span><span class="sxs-lookup"><span data-stu-id="74bf3-132">After you're done, choose **Save**, or toocancel your changes, select **Discard**.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/edit-1.png)

## <a name="how-toodelete-a-partner"></a><span data-ttu-id="74bf3-133">Как toodelete партнера</span><span class="sxs-lookup"><span data-stu-id="74bf3-133">How toodelete a partner</span></span>

1. <span data-ttu-id="74bf3-134">Выберите hello **партнеров** плитки.</span><span class="sxs-lookup"><span data-stu-id="74bf3-134">Select hello **Partners** tile.</span></span>
2. <span data-ttu-id="74bf3-135">После открытия колонке партнера hello, выберите нужных toodelete партнера hello.</span><span class="sxs-lookup"><span data-stu-id="74bf3-135">After hello Partner blade opens, select hello partner that you want toodelete.</span></span>
3. <span data-ttu-id="74bf3-136">Щелкните **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="74bf3-136">Choose **Delete**.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/delete-1.png)

## <a name="next-steps"></a><span data-ttu-id="74bf3-137">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="74bf3-137">Next steps</span></span>
* [<span data-ttu-id="74bf3-138">Узнайте о соглашениях и Пакете интеграции Enterprise</span><span class="sxs-lookup"><span data-stu-id="74bf3-138">Learn more about agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "Узнайте о соглашениях и Пакете интеграции Enterprise")  

