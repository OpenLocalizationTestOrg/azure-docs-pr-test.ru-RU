---
title: "Руководство по интеграции Azure Active Directory с Qualtrics | Документация Майкрософт"
description: "Узнайте, как toouse Qualtrics с Azure Active Directory tooenable единого входа, автоматизированной подготовки и многое другое!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 4df889ab-2685-4d15-a163-1ba26567eeda
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: 941642e74b90bb13a5ce37ce6665cfa32cd86016
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-qualtrics"></a><span data-ttu-id="388c5-103">Учебник. Интеграция Azure Active Directory с Qualtrics</span><span class="sxs-lookup"><span data-stu-id="388c5-103">Tutorial: Azure Active Directory integration with Qualtrics</span></span>
<span data-ttu-id="388c5-104">Цель этого учебника Hello — tooshow hello интеграцию Azure и Qualtrics.</span><span class="sxs-lookup"><span data-stu-id="388c5-104">hello objective of this tutorial is tooshow hello integration of Azure and Qualtrics.</span></span>  

<span data-ttu-id="388c5-105">Hello сценарий, описанный в этом руководстве предполагается, что уже hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="388c5-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="388c5-106">Действующая подписка на Azure</span><span class="sxs-lookup"><span data-stu-id="388c5-106">A valid Azure subscription</span></span>
* <span data-ttu-id="388c5-107">Подписка Qualtrics с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="388c5-107">A Qualtrics single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="388c5-108">После завершения этого учебника, пользователи hello Azure AD, назначенные tooQualtrics будет может toosingle вход в приложение hello на корпоративном сайте Qualtrics (вход поставщиком услуг инициировал) или с помощью hello [toohello введение Получить доступ к панели](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="388c5-108">After completing this tutorial, hello Azure AD users you have assigned tooQualtrics will be able toosingle sign into hello application at your Qualtrics company site (service provider initiated sign on), or using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="388c5-109">Hello сценарий, описанный в этом руководстве состоит из hello следующие стандартные блоки.</span><span class="sxs-lookup"><span data-stu-id="388c5-109">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

1. <span data-ttu-id="388c5-110">Включение hello интеграции приложений для Qualtrics</span><span class="sxs-lookup"><span data-stu-id="388c5-110">Enabling hello application integration for Qualtrics</span></span>
2. <span data-ttu-id="388c5-111">Настройка единого входа.</span><span class="sxs-lookup"><span data-stu-id="388c5-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="388c5-112">Настройка подготовки учетных записей пользователей</span><span class="sxs-lookup"><span data-stu-id="388c5-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="388c5-113">Назначение пользователей</span><span class="sxs-lookup"><span data-stu-id="388c5-113">Assigning users</span></span>

<span data-ttu-id="388c5-114">![Сценарий](./media/active-directory-saas-qualtrics-tutorial/IC789542.png "Сценарий")</span><span class="sxs-lookup"><span data-stu-id="388c5-114">![Scenario](./media/active-directory-saas-qualtrics-tutorial/IC789542.png "Scenario")</span></span>

## <a name="enabling-hello-application-integration-for-qualtrics"></a><span data-ttu-id="388c5-115">Включение hello интеграции приложений для Qualtrics</span><span class="sxs-lookup"><span data-stu-id="388c5-115">Enabling hello application integration for Qualtrics</span></span>
<span data-ttu-id="388c5-116">Hello цель этого раздела — toooutline как интеграция приложения hello tooenable для Qualtrics.</span><span class="sxs-lookup"><span data-stu-id="388c5-116">hello objective of this section is toooutline how tooenable hello application integration for Qualtrics.</span></span>

<span data-ttu-id="388c5-117">**интеграции приложения hello tooenable для Qualtrics, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="388c5-117">**tooenable hello application integration for Qualtrics, perform hello following steps:**</span></span>

1. <span data-ttu-id="388c5-118">В hello классический портал Azure, hello левой области навигации, выберите **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="388c5-118">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="388c5-119">![Active Directory](./media/active-directory-saas-qualtrics-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="388c5-119">![Active Directory](./media/active-directory-saas-qualtrics-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="388c5-120">Из hello **каталога** список, выберите hello каталога, для которого требуется Интеграция каталогов tooenable.</span><span class="sxs-lookup"><span data-stu-id="388c5-120">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="388c5-121">Щелкните представление приложения hello tooopen в представлении каталога hello **приложений** в верхнем меню hello.</span><span class="sxs-lookup"><span data-stu-id="388c5-121">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
   <span data-ttu-id="388c5-122">![Приложения](./media/active-directory-saas-qualtrics-tutorial/IC700994.png "Приложения")</span><span class="sxs-lookup"><span data-stu-id="388c5-122">![Applications](./media/active-directory-saas-qualtrics-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="388c5-123">Нажмите кнопку **добавить** hello нижней части страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="388c5-123">Click **Add** at hello bottom of hello page.</span></span>
   
   <span data-ttu-id="388c5-124">![Добавление приложения](./media/active-directory-saas-qualtrics-tutorial/IC749321.png "Добавление приложения")</span><span class="sxs-lookup"><span data-stu-id="388c5-124">![Add application](./media/active-directory-saas-qualtrics-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="388c5-125">На hello **что вам требуется toodo** диалоговое окно, нажмите кнопку **добавить приложение из коллекции hello**.</span><span class="sxs-lookup"><span data-stu-id="388c5-125">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
   <span data-ttu-id="388c5-126">![Добавление приложения из коллекции](./media/active-directory-saas-qualtrics-tutorial/IC749322.png "Добавление приложения из коллекции")</span><span class="sxs-lookup"><span data-stu-id="388c5-126">![Add an application from gallerry](./media/active-directory-saas-qualtrics-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="388c5-127">В hello **поле поиска**, тип **Qualtrics**.</span><span class="sxs-lookup"><span data-stu-id="388c5-127">In hello **search box**, type **Qualtrics**.</span></span>
   
   <span data-ttu-id="388c5-128">![Коллекция приложений](./media/active-directory-saas-qualtrics-tutorial/IC789543.png "Коллекция приложений")</span><span class="sxs-lookup"><span data-stu-id="388c5-128">![Application Gallery](./media/active-directory-saas-qualtrics-tutorial/IC789543.png "Application Gallery")</span></span>
7. <span data-ttu-id="388c5-129">В области результатов hello выберите **Qualtrics**и нажмите кнопку **завершить** tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="388c5-129">In hello results pane, select **Qualtrics**, and then click **Complete** tooadd hello application.</span></span>
   
   <span data-ttu-id="388c5-130">![Qualtrics](./media/active-directory-saas-qualtrics-tutorial/IC789544.png "Qualtrics")</span><span class="sxs-lookup"><span data-stu-id="388c5-130">![Qualtrics](./media/active-directory-saas-qualtrics-tutorial/IC789544.png "Qualtrics")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="388c5-131">Настройка единого входа</span><span class="sxs-lookup"><span data-stu-id="388c5-131">Configure single sign-on</span></span>

<span data-ttu-id="388c5-132">Цель этого раздела Hello — toooutline как tooQualtrics tooauthenticate tooenable пользователей с учетной записью в Azure AD, используя федерацию на основе hello SAML протокола.</span><span class="sxs-lookup"><span data-stu-id="388c5-132">hello objective of this section is toooutline how tooenable users tooauthenticate tooQualtrics with their account in Azure AD using federation based on hello SAML protocol.</span></span>

<span data-ttu-id="388c5-133">**tooconfigure единого входа, выполните следующие шаги hello:**</span><span class="sxs-lookup"><span data-stu-id="388c5-133">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="388c5-134">В классический портал Azure, на hello hello **Qualtrics** странице интеграции приложения щелкните **настроить единый вход** tooopen hello **Настройка единого входа** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="388c5-134">In hello Azure classic portal, on hello **Qualtrics** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="388c5-135">![Настройка единого входа](./media/active-directory-saas-qualtrics-tutorial/IC789545.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="388c5-135">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789545.png "Configure Single Sign-On")</span></span>
2. <span data-ttu-id="388c5-136">На hello **предпочитаемый как toosign пользователей на tooQualtrics** выберите **Microsoft Azure AD Single Sign-On**, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="388c5-136">On hello **How would you like users toosign on tooQualtrics** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="388c5-137">![Настройка единого входа](./media/active-directory-saas-qualtrics-tutorial/IC789546.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="388c5-137">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789546.png "Configure Single Sign-On")</span></span>
3. <span data-ttu-id="388c5-138">На hello **настроить URL-адрес приложения** страницы в hello **Qualtrics на URL-адрес входа** в текстовое поле введите URL-адрес (например: «*https://ssotest2ut1.qualtrics.com*») и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="388c5-138">On hello **Configure App URL** page, in hello **Qualtrics Sign On URL** textbox, type your URL (e.g.: “*https://ssotest2ut1.qualtrics.com*"), and then click **Next**.</span></span>
   
   <span data-ttu-id="388c5-139">![Настройка URL-адреса приложения](./media/active-directory-saas-qualtrics-tutorial/IC789547.png "Настройка URL-адреса приложения")</span><span class="sxs-lookup"><span data-stu-id="388c5-139">![Configure App URL](./media/active-directory-saas-qualtrics-tutorial/IC789547.png "Configure App URL")</span></span>
4. <span data-ttu-id="388c5-140">На hello **настройки единого входа в Qualtrics** щелкните **загрузить метаданные**, а затем сохраните файл метаданных hello на компьютере.</span><span class="sxs-lookup"><span data-stu-id="388c5-140">On hello **Configure single sign-on at Qualtrics** page, click **Download metadata**, and then save hello metadata file on your computer.</span></span>
   
   <span data-ttu-id="388c5-141">![Настройка единого входа](./media/active-directory-saas-qualtrics-tutorial/IC789548.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="388c5-141">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789548.png "Configure Single Sign-On")</span></span>
5. <span data-ttu-id="388c5-142">Отправьте hello метаданных файла toohello поддержки qualtrics.</span><span class="sxs-lookup"><span data-stu-id="388c5-142">Send hello metadata file toohello Qualtrics support team.</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="388c5-143">Настройка единого входа Hello имеет toobe выполненных hello поддержки qualtrics.</span><span class="sxs-lookup"><span data-stu-id="388c5-143">hello SSO configuration has toobe performed by hello Qualtrics support team.</span></span> <span data-ttu-id="388c5-144">Сразу после завершения настройки hello, вы получите уведомление.</span><span class="sxs-lookup"><span data-stu-id="388c5-144">You will get a notification as soon as hello configuration has been completed.</span></span>
   > 
   > 
6. <span data-ttu-id="388c5-145">На hello классический портал Azure, выберите Подтверждение настройки единого входа hello и нажмите кнопку **завершить** tooclose hello **Настройка единого входа** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="388c5-145">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="388c5-146">![Настройка единого входа](./media/active-directory-saas-qualtrics-tutorial/IC789549.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="388c5-146">![Configure Single Sign-On](./media/active-directory-saas-qualtrics-tutorial/IC789549.png "Configure Single Sign-On")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="388c5-147">Настроить подготовку учетных записей пользователей</span><span class="sxs-lookup"><span data-stu-id="388c5-147">Configure user provisioning</span></span>

<span data-ttu-id="388c5-148">Нет элемента действия для вас tooconfigure подготовки пользователей tooQualtrics.</span><span class="sxs-lookup"><span data-stu-id="388c5-148">There is no action item for you tooconfigure user provisioning tooQualtrics.</span></span> <span data-ttu-id="388c5-149">Когда назначенный пользователь пытается toolog в Qualtrics с помощью панели доступа hello, Qualtrics проверяет, существует ли пользователь hello.</span><span class="sxs-lookup"><span data-stu-id="388c5-149">When an assigned user tries toolog into Qualtrics using hello access panel, Qualtrics checks whether hello user exists.</span></span>  

<span data-ttu-id="388c5-150">Если учетная запись пользователя отсутствует, Qualtrics автоматически создает ее.</span><span class="sxs-lookup"><span data-stu-id="388c5-150">If there is no user account available yet, it is automatically created by Qualtrics.</span></span>

## <a name="assign-users"></a><span data-ttu-id="388c5-151">Назначить пользователей</span><span class="sxs-lookup"><span data-stu-id="388c5-151">Assign users</span></span>
<span data-ttu-id="388c5-152">tootest конфигурацию, необходимо toogrant hello Azure AD пользователей с помощью tooit доступ вашего приложения путем назначения им tooallow.</span><span class="sxs-lookup"><span data-stu-id="388c5-152">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="388c5-153">**tooQualtrics tooassign пользователей, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="388c5-153">**tooassign users tooQualtrics, perform hello following steps:**</span></span>

1. <span data-ttu-id="388c5-154">В hello классический портал Azure создайте тестовую учетную запись.</span><span class="sxs-lookup"><span data-stu-id="388c5-154">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="388c5-155">На hello **Qualtrics** странице интеграции приложения щелкните **назначить пользователей**.</span><span class="sxs-lookup"><span data-stu-id="388c5-155">On hello **Qualtrics** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="388c5-156">![Назначение пользователей](./media/active-directory-saas-qualtrics-tutorial/IC789550.png "Назначение пользователей")</span><span class="sxs-lookup"><span data-stu-id="388c5-156">![Assign Users](./media/active-directory-saas-qualtrics-tutorial/IC789550.png "Assign Users")</span></span>
3. <span data-ttu-id="388c5-157">Выберите тестового пользователя, нажмите кнопку **назначить**, а затем нажмите кнопку **Да** tooconfirm назначения.</span><span class="sxs-lookup"><span data-stu-id="388c5-157">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
   <span data-ttu-id="388c5-158">![Да](./media/active-directory-saas-qualtrics-tutorial/IC767830.png "Да")</span><span class="sxs-lookup"><span data-stu-id="388c5-158">![Yes](./media/active-directory-saas-qualtrics-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="388c5-159">Tootest параметры единого входа, откройте панель доступа hello.</span><span class="sxs-lookup"><span data-stu-id="388c5-159">If you want tootest your SSO settings, open hello Access Panel.</span></span> <span data-ttu-id="388c5-160">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="388c5-160">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

