---
title: "aaaCreate, ссылку, удалить или переместить учетную запись интеграции приложения логики Azure | Документы Microsoft"
description: "Как toocreate интеграцию учетной записи и связать его tooyour логику приложения"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: d3ad9e99-a9ee-477b-81bf-0881e11e632f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/23/2017
ms.author: LADocs; mandia
ms.openlocfilehash: fda6c91723b3e3624ee176df112ba8b6c9800273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-an-integration-account"></a><span data-ttu-id="68ab1-103">Что такое учетная запись интеграции?</span><span class="sxs-lookup"><span data-stu-id="68ab1-103">What is an integration account?</span></span>

<span data-ttu-id="68ab1-104">Учетная запись интеграции позволяет интеграции корпоративных приложений toomanage артефакты, включая схемы, карты, сертификаты, партнеров и соглашения.</span><span class="sxs-lookup"><span data-stu-id="68ab1-104">An integration account allows enterprise integration apps toomanage artifacts, including schemas, maps, certificates, partners and agreements.</span></span> <span data-ttu-id="68ab1-105">Любое приложение интеграции, создаваемые вами использует tooaccess учетной записи интеграции эти схемы, карты, сертификаты и т. д.</span><span class="sxs-lookup"><span data-stu-id="68ab1-105">Any integration app you create uses an integration account tooaccess these schemas, maps, certificates, and so on.</span></span>

## <a name="create-an-integration-account"></a><span data-ttu-id="68ab1-106">Создание учетной записи интеграции</span><span class="sxs-lookup"><span data-stu-id="68ab1-106">Create an integration account</span></span>

1.  <span data-ttu-id="68ab1-107">Войдите в toohello [портал Azure](http://portal.azure.com "портал Azure").</span><span class="sxs-lookup"><span data-stu-id="68ab1-107">Sign in toohello [Azure portal](http://portal.azure.com "Azure portal").</span></span> <span data-ttu-id="68ab1-108">Hello в левом меню, выберите **дополнительные службы**.</span><span class="sxs-lookup"><span data-stu-id="68ab1-108">From hello left menu, select **More services**.</span></span>

    ![Выбор "Больше служб"](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. <span data-ttu-id="68ab1-110">В поле поиска hello введите «интеграция» для фильтра.</span><span class="sxs-lookup"><span data-stu-id="68ab1-110">In hello search box, type "integration" for your filter.</span></span> <span data-ttu-id="68ab1-111">В списке результатов hello выберите **учетные записи службы интеграции**.</span><span class="sxs-lookup"><span data-stu-id="68ab1-111">In hello results list, select **Integration Accounts**.</span></span>

    ![Фильтрация по интеграции, выбор "Учетные записи интеграции"](./media/logic-apps-enterprise-integration-accounts/account-2.png)  

3. <span data-ttu-id="68ab1-113">В начале hello страницы приветствия, выберите **добавить**.</span><span class="sxs-lookup"><span data-stu-id="68ab1-113">At hello top of hello page, choose **Add**.</span></span>

    ![Кнопка "Добавить"](./media/logic-apps-enterprise-integration-accounts/account-3.png)

4. <span data-ttu-id="68ab1-115">Имя вашей учетной записи интеграции и выберите hello подписки Azure, которые должны toouse.</span><span class="sxs-lookup"><span data-stu-id="68ab1-115">Name your integration account and select hello Azure subscription that you want toouse.</span></span> <span data-ttu-id="68ab1-116">Вы можете создать **группу ресурсов** или выбрать имеющуюся.</span><span class="sxs-lookup"><span data-stu-id="68ab1-116">You can either create a new **Resource group** or select an existing resource group.</span></span> <span data-ttu-id="68ab1-117">Выберите **Расположение** для размещения учетной записи интеграции и **ценовую категорию**.</span><span class="sxs-lookup"><span data-stu-id="68ab1-117">Then select a **Location** for hosting your integration account and a **Pricing Tier**.</span></span> 

    <span data-ttu-id="68ab1-118">Когда вы будете готовы, нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="68ab1-118">When you're ready, choose **Create**.</span></span>

    ![Ввод сведений для учетной записи интеграции](./media/logic-apps-enterprise-integration-accounts/account-4.png)

    <span data-ttu-id="68ab1-120">Azure подготавливает учетную запись интеграции в hello выбрать расположение, которое следует выполнить в пределах 1 минуты.</span><span class="sxs-lookup"><span data-stu-id="68ab1-120">Azure provisions your integration account  in hello selected location, which should complete within 1 minute.</span></span>

5. <span data-ttu-id="68ab1-121">Обновите страницу приветствия.</span><span class="sxs-lookup"><span data-stu-id="68ab1-121">Refresh hello page.</span></span> <span data-ttu-id="68ab1-122">Вы увидите новую учетную запись интеграции в списке.</span><span class="sxs-lookup"><span data-stu-id="68ab1-122">You see your new integration account listed.</span></span>

    ![Отображение новой учетной записи интеграции](./media/logic-apps-enterprise-integration-accounts/account-5.png) 

<span data-ttu-id="68ab1-124">Затем подключитесь учетной записи интеграции hello, то созданный tooyour приложения логики.</span><span class="sxs-lookup"><span data-stu-id="68ab1-124">Next, link hello integration account that you created tooyour logic app.</span></span> 

## <a name="link-an-integration-account-tooa-logic-app"></a><span data-ttu-id="68ab1-125">Связать приложение логики интеграции tooa учетной записи</span><span class="sxs-lookup"><span data-stu-id="68ab1-125">Link an integration account tooa logic app</span></span>

<span data-ttu-id="68ab1-126">toogive свои приложения логики доступа к toomaps, схемы, соглашения и другие артефакты в учетной записи интеграции tooyour ссылку hello интеграции учетной записи приложения логики.</span><span class="sxs-lookup"><span data-stu-id="68ab1-126">toogive your logic apps access toomaps, schemas, agreements, and other artifacts in your integration account, link hello integration account tooyour logic app.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="68ab1-127">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="68ab1-127">Prerequisites</span></span>

* <span data-ttu-id="68ab1-128">Учетная запись интеграции.</span><span class="sxs-lookup"><span data-stu-id="68ab1-128">An integration account</span></span>
* <span data-ttu-id="68ab1-129">Приложение логики</span><span class="sxs-lookup"><span data-stu-id="68ab1-129">A logic app</span></span>

> [!NOTE] 
> <span data-ttu-id="68ab1-130">Убедитесь, что приложения учетной записи и логики интеграции в hello *же расположению Azure* перед началом.</span><span class="sxs-lookup"><span data-stu-id="68ab1-130">Make sure your integration account and logic app are in hello *same Azure location* before you begin.</span></span>


1. <span data-ttu-id="68ab1-131">В hello портал Azure выберите логику приложения и проверить расположение приложения логики.</span><span class="sxs-lookup"><span data-stu-id="68ab1-131">In hello Azure portal, select your logic app, and check your logic app's location.</span></span>

    ![Выбор приложения логики, проверка расположения](./media/logic-apps-enterprise-integration-accounts/linkaccount-1.png)

2. <span data-ttu-id="68ab1-133">В разделе **Параметры** выберите **Учетная запись интеграции**.</span><span class="sxs-lookup"><span data-stu-id="68ab1-133">Under **Settings**, select **Integration Account**.</span></span>

    ![Выбор "Учетная запись интеграции"](./media/logic-apps-enterprise-integration-accounts/linkaccount-2.png)

3. <span data-ttu-id="68ab1-135">Из hello **выберите учетную запись интеграции** список, выберите hello интеграции счета, toolink tooyour логику приложения.</span><span class="sxs-lookup"><span data-stu-id="68ab1-135">From hello **Select an Integration account** list, select hello integration account you want toolink tooyour logic app.</span></span> <span data-ttu-id="68ab1-136">Выберите toofinish связывания, **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="68ab1-136">toofinish linking, choose **Save**.</span></span>

    ![Выбор учетной записи интеграции](./media/logic-apps-enterprise-integration-accounts/linkaccount-3.png)

    <span data-ttu-id="68ab1-138">Вы получаете уведомление, которое показывает интеграцию учетной записи связанного tooyour логику приложения, и все артефакты в вашей учетной записи интеграции, теперь доступны tooyour логику приложения.</span><span class="sxs-lookup"><span data-stu-id="68ab1-138">You get a notification that shows your integration account is linked tooyour logic app,  and that all artifacts in your integration account are now available tooyour logic app.</span></span>

    ![Логика приложения связана учетная запись tooyour интеграции](./media/logic-apps-enterprise-integration-accounts/linkaccount-5.png)

<span data-ttu-id="68ab1-140">Теперь, когда ваша учетная запись интеграции связанного tooyour логику приложения, можно использовать в приложениях для логики соединители hello B2B.</span><span class="sxs-lookup"><span data-stu-id="68ab1-140">Now that your integration account is linked tooyour logic app, you can use hello B2B connectors in your logic apps.</span></span> <span data-ttu-id="68ab1-141">Некоторые распространенные соединители B2B включают в себя проверку XML, кодирование и декодирование неструктурированных файлов.</span><span class="sxs-lookup"><span data-stu-id="68ab1-141">Some common B2B connectors include XML validation and flat file encode/decode.</span></span>  

## <a name="delete-your-integration-account"></a><span data-ttu-id="68ab1-142">Удаление учетной записи интеграции</span><span class="sxs-lookup"><span data-stu-id="68ab1-142">Delete your integration account</span></span>

1. <span data-ttu-id="68ab1-143">Выберите **Больше служб**.</span><span class="sxs-lookup"><span data-stu-id="68ab1-143">Select **More services**.</span></span>

    ![Выбор "Больше служб"](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. <span data-ttu-id="68ab1-145">В поле поиска hello введите «интеграция» для фильтра.</span><span class="sxs-lookup"><span data-stu-id="68ab1-145">In hello search box, type "integration" for your filter.</span></span> <span data-ttu-id="68ab1-146">В списке результатов hello выберите **учетные записи службы интеграции**.</span><span class="sxs-lookup"><span data-stu-id="68ab1-146">In hello results list, select **Integration Accounts**.</span></span>

    ![Фильтрация по интеграции, выбор "Учетные записи интеграции"](./media/logic-apps-enterprise-integration-accounts/account-2.png)  

3. <span data-ttu-id="68ab1-148">Выберите hello интеграции учетной записью, которую toodelete.</span><span class="sxs-lookup"><span data-stu-id="68ab1-148">Select hello integration account that you want toodelete.</span></span>

    ![Выбор учетной записи toodelete интеграции](./media/logic-apps-enterprise-integration-accounts/account-5.png)

4. <span data-ttu-id="68ab1-150">Выберите пункт меню hello **удалить**.</span><span class="sxs-lookup"><span data-stu-id="68ab1-150">On hello menu, choose **Delete**.</span></span>

    ![Выбор команды "Удалить"](./media/logic-apps-enterprise-integration-accounts/delete.png)

5. <span data-ttu-id="68ab1-152">Подтверждение учетной записи интеграции choice toodelete hello.</span><span class="sxs-lookup"><span data-stu-id="68ab1-152">Confirm your choice toodelete hello integration account.</span></span>

## <a name="move-your-integration-account"></a><span data-ttu-id="68ab1-153">Перемещение учетной записи интеграции</span><span class="sxs-lookup"><span data-stu-id="68ab1-153">Move your integration account</span></span>

<span data-ttu-id="68ab1-154">toomove tooanother учетной записи интеграции Azure подписка или группа ресурсов, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="68ab1-154">toomove an integration account tooanother Azure subscription or resource group, follow these steps.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="68ab1-155">После перемещения интеграции учетную запись, необходимо обновить все сценарии toouse hello новые идентификаторы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="68ab1-155">You must update all scripts toouse hello new resource IDs after you move an integration account.</span></span>

1. <span data-ttu-id="68ab1-156">Выберите **Больше служб**.</span><span class="sxs-lookup"><span data-stu-id="68ab1-156">Select **More services**.</span></span>

    ![Выбор "Больше служб"](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. <span data-ttu-id="68ab1-158">В поле поиска hello введите «интеграция» для фильтра.</span><span class="sxs-lookup"><span data-stu-id="68ab1-158">In hello search box, type "integration" for your filter.</span></span> <span data-ttu-id="68ab1-159">В списке результатов hello выберите **учетные записи службы интеграции**.</span><span class="sxs-lookup"><span data-stu-id="68ab1-159">In hello results list, select **Integration Accounts**.</span></span>

    ![Фильтрация по интеграции, выбор "Учетные записи интеграции"](./media/logic-apps-enterprise-integration-accounts/account-2.png)

3. <span data-ttu-id="68ab1-161">Выберите hello интеграции учетной записью, которую toomove.</span><span class="sxs-lookup"><span data-stu-id="68ab1-161">Select hello integration account that you want toomove.</span></span> <span data-ttu-id="68ab1-162">В разделе **Параметры** выберите **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="68ab1-162">Under **Settings**, choose **Properties**.</span></span>

    ![Выберите toomove учетной записи интеграции.](./media/logic-apps-enterprise-integration-accounts/move.png)

5. <span data-ttu-id="68ab1-165">Изменение hello группы ресурсов или подписку Azure, связанной с вашей учетной записи интеграции.</span><span class="sxs-lookup"><span data-stu-id="68ab1-165">Change hello resource group or Azure subscription that's associated with your integration account.</span></span>

    ![Выбор "Изменить группу ресурсов" или "Изменить подписку"](./media/logic-apps-enterprise-integration-accounts/move-2.png)

## <a name="next-steps"></a><span data-ttu-id="68ab1-167">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="68ab1-167">Next Steps</span></span>
* [<span data-ttu-id="68ab1-168">Узнайте о соглашениях и Пакете интеграции Enterprise</span><span class="sxs-lookup"><span data-stu-id="68ab1-168">Learn more about agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "Узнайте о соглашениях и Пакете интеграции Enterprise")  

