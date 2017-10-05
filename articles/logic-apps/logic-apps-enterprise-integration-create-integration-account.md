---
title: "Создание, привязка, удаление или перемещение учетной записи интеграции в Azure Logic Apps | Документация Майкрософт"
description: "Узнайте, как создать учетную запись интеграции и связать ее с приложениями логики."
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
ms.openlocfilehash: 716e7b5bab8725dea0fd2b760d0e46e8e892c5b4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="what-is-an-integration-account"></a><span data-ttu-id="d44ad-103">Что такое учетная запись интеграции?</span><span class="sxs-lookup"><span data-stu-id="d44ad-103">What is an integration account?</span></span>

<span data-ttu-id="d44ad-104">Учетная запись интеграции позволяет приложениям интеграции Enterprise управлять артефактами, включая схемы, карты, сертификаты, партнеры и соглашения.</span><span class="sxs-lookup"><span data-stu-id="d44ad-104">An integration account allows enterprise integration apps to manage artifacts, including schemas, maps, certificates, partners and agreements.</span></span> <span data-ttu-id="d44ad-105">Любое создаваемое приложение интеграции использует учетную запись интеграции для доступа к схемам, картам, сертификатам и т. д.</span><span class="sxs-lookup"><span data-stu-id="d44ad-105">Any integration app you create uses an integration account to access these schemas, maps, certificates, and so on.</span></span>

## <a name="create-an-integration-account"></a><span data-ttu-id="d44ad-106">Создание учетной записи интеграции</span><span class="sxs-lookup"><span data-stu-id="d44ad-106">Create an integration account</span></span>

1.  <span data-ttu-id="d44ad-107">Войдите на [портал Azure](http://portal.azure.com "Портал Azure").</span><span class="sxs-lookup"><span data-stu-id="d44ad-107">Sign in to the [Azure portal](http://portal.azure.com "Azure portal").</span></span> <span data-ttu-id="d44ad-108">В меню слева выберите **Больше служб**.</span><span class="sxs-lookup"><span data-stu-id="d44ad-108">From the left menu, select **More services**.</span></span>

    ![Выбор "Больше служб"](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. <span data-ttu-id="d44ad-110">Введите "интеграция" в поле поиска для фильтрации.</span><span class="sxs-lookup"><span data-stu-id="d44ad-110">In the search box, type "integration" for your filter.</span></span> <span data-ttu-id="d44ad-111">В списке результатов выберите **Учетные записи интеграции**.</span><span class="sxs-lookup"><span data-stu-id="d44ad-111">In the results list, select **Integration Accounts**.</span></span>

    ![Фильтрация по интеграции, выбор "Учетные записи интеграции"](./media/logic-apps-enterprise-integration-accounts/account-2.png)  

3. <span data-ttu-id="d44ad-113">В верхней части страницы нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="d44ad-113">At the top of the page, choose **Add**.</span></span>

    ![Кнопка "Добавить"](./media/logic-apps-enterprise-integration-accounts/account-3.png)

4. <span data-ttu-id="d44ad-115">Введите имя для учетной записи интеграции и выберите подписку Azure, которую вы хотите использовать.</span><span class="sxs-lookup"><span data-stu-id="d44ad-115">Name your integration account and select the Azure subscription that you want to use.</span></span> <span data-ttu-id="d44ad-116">Вы можете создать **группу ресурсов** или выбрать имеющуюся.</span><span class="sxs-lookup"><span data-stu-id="d44ad-116">You can either create a new **Resource group** or select an existing resource group.</span></span> <span data-ttu-id="d44ad-117">Выберите **Расположение** для размещения учетной записи интеграции и **ценовую категорию**.</span><span class="sxs-lookup"><span data-stu-id="d44ad-117">Then select a **Location** for hosting your integration account and a **Pricing Tier**.</span></span> 

    <span data-ttu-id="d44ad-118">Когда вы будете готовы, нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="d44ad-118">When you're ready, choose **Create**.</span></span>

    ![Ввод сведений для учетной записи интеграции](./media/logic-apps-enterprise-integration-accounts/account-4.png)

    <span data-ttu-id="d44ad-120">Azure создает учетную запись интеграции в выбранном расположении. На это потребуется не больше 1 минуты.</span><span class="sxs-lookup"><span data-stu-id="d44ad-120">Azure provisions your integration account  in the selected location, which should complete within 1 minute.</span></span>

5. <span data-ttu-id="d44ad-121">Обновите страницу.</span><span class="sxs-lookup"><span data-stu-id="d44ad-121">Refresh the page.</span></span> <span data-ttu-id="d44ad-122">Вы увидите новую учетную запись интеграции в списке.</span><span class="sxs-lookup"><span data-stu-id="d44ad-122">You see your new integration account listed.</span></span>

    ![Отображение новой учетной записи интеграции](./media/logic-apps-enterprise-integration-accounts/account-5.png) 

<span data-ttu-id="d44ad-124">Теперь свяжите созданную учетную запись интеграции с приложением логики.</span><span class="sxs-lookup"><span data-stu-id="d44ad-124">Next, link the integration account that you created to your logic app.</span></span> 

## <a name="link-an-integration-account-to-a-logic-app"></a><span data-ttu-id="d44ad-125">Привязка учетной записи интеграции к приложению логики</span><span class="sxs-lookup"><span data-stu-id="d44ad-125">Link an integration account to a logic app</span></span>

<span data-ttu-id="d44ad-126">Чтобы предоставить приложению логики доступ к картам, схемам, соглашениям и другим артефактам в учетной записи интеграции, свяжите ее с приложением логики.</span><span class="sxs-lookup"><span data-stu-id="d44ad-126">To give your logic apps access to maps, schemas, agreements, and other artifacts in your integration account, link the integration account to your logic app.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="d44ad-127">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d44ad-127">Prerequisites</span></span>

* <span data-ttu-id="d44ad-128">Учетная запись интеграции.</span><span class="sxs-lookup"><span data-stu-id="d44ad-128">An integration account</span></span>
* <span data-ttu-id="d44ad-129">Приложение логики</span><span class="sxs-lookup"><span data-stu-id="d44ad-129">A logic app</span></span>

> [!NOTE] 
> <span data-ttu-id="d44ad-130">Прежде чем начать, убедитесь, что учетная запись интеграции и приложение логики находятся в *одном расположении Azure*.</span><span class="sxs-lookup"><span data-stu-id="d44ad-130">Make sure your integration account and logic app are in the *same Azure location* before you begin.</span></span>


1. <span data-ttu-id="d44ad-131">На портале Azure выберите приложение логики и проверьте его расположение.</span><span class="sxs-lookup"><span data-stu-id="d44ad-131">In the Azure portal, select your logic app, and check your logic app's location.</span></span>

    ![Выбор приложения логики, проверка расположения](./media/logic-apps-enterprise-integration-accounts/linkaccount-1.png)

2. <span data-ttu-id="d44ad-133">В разделе **Параметры** выберите **Учетная запись интеграции**.</span><span class="sxs-lookup"><span data-stu-id="d44ad-133">Under **Settings**, select **Integration Account**.</span></span>

    ![Выбор "Учетная запись интеграции"](./media/logic-apps-enterprise-integration-accounts/linkaccount-2.png)

3. <span data-ttu-id="d44ad-135">Выберите учетную запись интеграции, которую необходимо связать с приложением логики, из списка **Выберите учетную запись интеграции**.</span><span class="sxs-lookup"><span data-stu-id="d44ad-135">From the **Select an Integration account** list, select the integration account you want to link to your logic app.</span></span> <span data-ttu-id="d44ad-136">Чтобы завершить связывание, нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="d44ad-136">To finish linking, choose **Save**.</span></span>

    ![Выбор учетной записи интеграции](./media/logic-apps-enterprise-integration-accounts/linkaccount-3.png)

    <span data-ttu-id="d44ad-138">Вы увидите уведомление о том, что учетная запись интеграции связана с вашим приложением логики, а все артефакты в вашей учетной записи интеграции доступны для этого приложения логики.</span><span class="sxs-lookup"><span data-stu-id="d44ad-138">You get a notification that shows your integration account is linked to your logic app,  and that all artifacts in your integration account are now available to your logic app.</span></span>

    ![Приложение логики связано с учетной записью интеграции](./media/logic-apps-enterprise-integration-accounts/linkaccount-5.png)

<span data-ttu-id="d44ad-140">Теперь, когда ваша учетная запись интеграции связана с приложением логики, вы можете использовать соединители "бизнес — бизнес" (B2B), доступные в приложениях логики.</span><span class="sxs-lookup"><span data-stu-id="d44ad-140">Now that your integration account is linked to your logic app, you can use the B2B connectors in your logic apps.</span></span> <span data-ttu-id="d44ad-141">Некоторые распространенные соединители B2B включают в себя проверку XML, кодирование и декодирование неструктурированных файлов.</span><span class="sxs-lookup"><span data-stu-id="d44ad-141">Some common B2B connectors include XML validation and flat file encode/decode.</span></span>  

## <a name="delete-your-integration-account"></a><span data-ttu-id="d44ad-142">Удаление учетной записи интеграции</span><span class="sxs-lookup"><span data-stu-id="d44ad-142">Delete your integration account</span></span>

1. <span data-ttu-id="d44ad-143">Выберите **Больше служб**.</span><span class="sxs-lookup"><span data-stu-id="d44ad-143">Select **More services**.</span></span>

    ![Выбор "Больше служб"](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. <span data-ttu-id="d44ad-145">Введите "интеграция" в поле поиска для фильтрации.</span><span class="sxs-lookup"><span data-stu-id="d44ad-145">In the search box, type "integration" for your filter.</span></span> <span data-ttu-id="d44ad-146">В списке результатов выберите **Учетные записи интеграции**.</span><span class="sxs-lookup"><span data-stu-id="d44ad-146">In the results list, select **Integration Accounts**.</span></span>

    ![Фильтрация по интеграции, выбор "Учетные записи интеграции"](./media/logic-apps-enterprise-integration-accounts/account-2.png)  

3. <span data-ttu-id="d44ad-148">Выберите учетную запись интеграции, которую нужно удалить.</span><span class="sxs-lookup"><span data-stu-id="d44ad-148">Select the integration account that you want to delete.</span></span>

    ![Выбор учетной записи интеграции для удаления](./media/logic-apps-enterprise-integration-accounts/account-5.png)

4. <span data-ttu-id="d44ad-150">В меню выберите **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="d44ad-150">On the menu, choose **Delete**.</span></span>

    ![Выбор команды "Удалить"](./media/logic-apps-enterprise-integration-accounts/delete.png)

5. <span data-ttu-id="d44ad-152">Подтвердите свой выбор, чтобы удалить учетную запись интеграции.</span><span class="sxs-lookup"><span data-stu-id="d44ad-152">Confirm your choice to delete the integration account.</span></span>

## <a name="move-your-integration-account"></a><span data-ttu-id="d44ad-153">Перемещение учетной записи интеграции</span><span class="sxs-lookup"><span data-stu-id="d44ad-153">Move your integration account</span></span>

<span data-ttu-id="d44ad-154">Чтобы переместить учетную запись интеграции в другую подписку Azure или группу ресурсов, выполните описанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="d44ad-154">To move an integration account to another Azure subscription or resource group, follow these steps.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d44ad-155">После перемещения учетной записи интеграции необходимо обновить все скрипты, чтобы в них использовались новые идентификаторы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="d44ad-155">You must update all scripts to use the new resource IDs after you move an integration account.</span></span>

1. <span data-ttu-id="d44ad-156">Выберите **Больше служб**.</span><span class="sxs-lookup"><span data-stu-id="d44ad-156">Select **More services**.</span></span>

    ![Выбор "Больше служб"](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. <span data-ttu-id="d44ad-158">Введите "интеграция" в поле поиска для фильтрации.</span><span class="sxs-lookup"><span data-stu-id="d44ad-158">In the search box, type "integration" for your filter.</span></span> <span data-ttu-id="d44ad-159">В списке результатов выберите **Учетные записи интеграции**.</span><span class="sxs-lookup"><span data-stu-id="d44ad-159">In the results list, select **Integration Accounts**.</span></span>

    ![Фильтрация по интеграции, выбор "Учетные записи интеграции"](./media/logic-apps-enterprise-integration-accounts/account-2.png)

3. <span data-ttu-id="d44ad-161">Выберите учетную запись интеграции, которую нужно переместить.</span><span class="sxs-lookup"><span data-stu-id="d44ad-161">Select the integration account that you want to move.</span></span> <span data-ttu-id="d44ad-162">В разделе **Параметры** выберите **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="d44ad-162">Under **Settings**, choose **Properties**.</span></span>

    ![Выбор учетной записи интеграции для перемещения](./media/logic-apps-enterprise-integration-accounts/move.png)

5. <span data-ttu-id="d44ad-165">Измените группу ресурсов или подписку Azure, связанную с вашей учетной записью интеграции.</span><span class="sxs-lookup"><span data-stu-id="d44ad-165">Change the resource group or Azure subscription that's associated with your integration account.</span></span>

    ![Выбор "Изменить группу ресурсов" или "Изменить подписку"](./media/logic-apps-enterprise-integration-accounts/move-2.png)

## <a name="next-steps"></a><span data-ttu-id="d44ad-167">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d44ad-167">Next Steps</span></span>
* [<span data-ttu-id="d44ad-168">Узнайте о соглашениях и Пакете интеграции Enterprise</span><span class="sxs-lookup"><span data-stu-id="d44ad-168">Learn more about agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "Узнайте о соглашениях и Пакете интеграции Enterprise")  

