---
title: "Учебник. Интеграция Azure Active Directory с Coupa | Документация Майкрософт"
description: "Узнайте, как toouse Coupa с Azure Active Directory tooenable единого входа, автоматизированной подготовки и многое другое!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 47f27746-9057-4b9c-991e-3abf77710f73
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 87e98573718d27d408c886466a374a987f58faa2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-coupa"></a><span data-ttu-id="9acc9-103">Руководство. Интеграция Azure Active Directory с Coupa</span><span class="sxs-lookup"><span data-stu-id="9acc9-103">Tutorial: Azure Active Directory integration with Coupa</span></span>
<span data-ttu-id="9acc9-104">Цель этого учебника Hello — tooshow hello интеграцию Azure и Coupa.</span><span class="sxs-lookup"><span data-stu-id="9acc9-104">hello objective of this tutorial is tooshow hello integration of Azure and Coupa.</span></span>  
<span data-ttu-id="9acc9-105">Hello сценарий, описанный в этом руководстве предполагается, что уже hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="9acc9-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="9acc9-106">Действующая подписка на Azure</span><span class="sxs-lookup"><span data-stu-id="9acc9-106">A valid Azure subscription</span></span>
* <span data-ttu-id="9acc9-107">Подписка Coupa с поддержкой единого входа</span><span class="sxs-lookup"><span data-stu-id="9acc9-107">A Coupa single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="9acc9-108">После завершения этого учебника, пользователи hello Azure AD, назначенные tooCoupa будут может toosingle входа в приложение hello hello [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9acc9-108">After completing this tutorial, hello Azure AD users you have assigned tooCoupa will be able toosingle sign into hello application using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="9acc9-109">Hello сценарий, описанный в этом руководстве состоит из hello следующие стандартные блоки.</span><span class="sxs-lookup"><span data-stu-id="9acc9-109">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

* <span data-ttu-id="9acc9-110">Включение hello интеграции приложений для Coupa</span><span class="sxs-lookup"><span data-stu-id="9acc9-110">Enabling hello application integration for Coupa</span></span>
* <span data-ttu-id="9acc9-111">Настройка единого входа</span><span class="sxs-lookup"><span data-stu-id="9acc9-111">Configuring single sign-on</span></span>
* <span data-ttu-id="9acc9-112">Настройка подготовки учетных записей пользователей</span><span class="sxs-lookup"><span data-stu-id="9acc9-112">Configuring user provisioning</span></span>
* <span data-ttu-id="9acc9-113">Назначение пользователей</span><span class="sxs-lookup"><span data-stu-id="9acc9-113">Assigning users</span></span>

<span data-ttu-id="9acc9-114">![Сценарий](./media/active-directory-saas-coupa-tutorial/IC791897.png "Сценарий")</span><span class="sxs-lookup"><span data-stu-id="9acc9-114">![Scenario](./media/active-directory-saas-coupa-tutorial/IC791897.png "Scenario")</span></span>

## <a name="enable-hello-application-integration-for-coupa"></a><span data-ttu-id="9acc9-115">Включить hello интеграции приложений для Coupa</span><span class="sxs-lookup"><span data-stu-id="9acc9-115">Enable hello application integration for Coupa</span></span>
<span data-ttu-id="9acc9-116">Hello цель этого раздела — toooutline как интеграции приложения hello tooenable для Coupa.</span><span class="sxs-lookup"><span data-stu-id="9acc9-116">hello objective of this section is toooutline how tooenable hello application integration for Coupa.</span></span>

<span data-ttu-id="9acc9-117">**интеграции приложения hello tooenable для Coupa, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="9acc9-117">**tooenable hello application integration for Coupa, perform hello following steps:**</span></span>

1. <span data-ttu-id="9acc9-118">В hello классический портал Azure, hello левой области навигации, выберите **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9acc9-118">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="9acc9-119">![Active Directory](./media/active-directory-saas-coupa-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="9acc9-119">![Active Directory](./media/active-directory-saas-coupa-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="9acc9-120">Из hello **каталога** список, выберите hello каталога, для которого требуется Интеграция каталогов tooenable.</span><span class="sxs-lookup"><span data-stu-id="9acc9-120">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="9acc9-121">Щелкните представление приложения hello tooopen в представлении каталога hello **приложений** в верхнем меню hello.</span><span class="sxs-lookup"><span data-stu-id="9acc9-121">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
   <span data-ttu-id="9acc9-122">![Приложения](./media/active-directory-saas-coupa-tutorial/IC700994.png "Приложения")</span><span class="sxs-lookup"><span data-stu-id="9acc9-122">![Applications](./media/active-directory-saas-coupa-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="9acc9-123">Нажмите кнопку **добавить** hello нижней части страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="9acc9-123">Click **Add** at hello bottom of hello page.</span></span>
   
   <span data-ttu-id="9acc9-124">![Добавление приложения](./media/active-directory-saas-coupa-tutorial/IC749321.png "Добавление приложения")</span><span class="sxs-lookup"><span data-stu-id="9acc9-124">![Add application](./media/active-directory-saas-coupa-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="9acc9-125">На hello **что вам требуется toodo** диалоговое окно, нажмите кнопку **добавить приложение из коллекции hello**.</span><span class="sxs-lookup"><span data-stu-id="9acc9-125">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
   <span data-ttu-id="9acc9-126">![Добавление приложения из коллекции](./media/active-directory-saas-coupa-tutorial/IC749322.png "Добавление приложения из коллекции")</span><span class="sxs-lookup"><span data-stu-id="9acc9-126">![Add an application from gallerry](./media/active-directory-saas-coupa-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="9acc9-127">В hello **поле поиска**, тип **Coupa**.</span><span class="sxs-lookup"><span data-stu-id="9acc9-127">In hello **search box**, type **Coupa**.</span></span>
   
   <span data-ttu-id="9acc9-128">![Коллекция приложений](./media/active-directory-saas-coupa-tutorial/IC791898.png "Коллекция приложений")</span><span class="sxs-lookup"><span data-stu-id="9acc9-128">![Application Gallery](./media/active-directory-saas-coupa-tutorial/IC791898.png "Application Gallery")</span></span>
7. <span data-ttu-id="9acc9-129">В области результатов hello выберите **Coupa**и нажмите кнопку **завершить** tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="9acc9-129">In hello results pane, select **Coupa**, and then click **Complete** tooadd hello application.</span></span>
   
   <span data-ttu-id="9acc9-130">![Coupa](./media/active-directory-saas-coupa-tutorial/IC791899.png "Coupa")</span><span class="sxs-lookup"><span data-stu-id="9acc9-130">![Coupa](./media/active-directory-saas-coupa-tutorial/IC791899.png "Coupa")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="9acc9-131">Настройка единого входа</span><span class="sxs-lookup"><span data-stu-id="9acc9-131">Configure single sign-on</span></span>

<span data-ttu-id="9acc9-132">Цель этого раздела Hello — toooutline как tooCoupa tooauthenticate tooenable пользователей с учетной записью в Azure AD, используя федерацию на основе hello SAML протокола.</span><span class="sxs-lookup"><span data-stu-id="9acc9-132">hello objective of this section is toooutline how tooenable users tooauthenticate tooCoupa with their account in Azure AD using federation based on hello SAML protocol.</span></span>  

<span data-ttu-id="9acc9-133">Настройка единого входа для Coupa требуется tooretrieve значение отпечатка из сертификата.</span><span class="sxs-lookup"><span data-stu-id="9acc9-133">Configuring single sign-on for Coupa requires you tooretrieve a thumbprint value from a certificate.</span></span> <span data-ttu-id="9acc9-134">Если вы не знакомы с этой процедурой, см. раздел [как tooretrieve значение отпечатка сертификата](http://youtu.be/YKQF266SAxI).</span><span class="sxs-lookup"><span data-stu-id="9acc9-134">If you are not familiar with this procedure, see [How tooretrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span></span>

<span data-ttu-id="9acc9-135">**tooconfigure единого входа, выполните следующие шаги hello:**</span><span class="sxs-lookup"><span data-stu-id="9acc9-135">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="9acc9-136">Войдите на tooyour сайт Coupa компании от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="9acc9-136">Sign on tooyour Coupa company site as an administrator.</span></span>
2. <span data-ttu-id="9acc9-137">Go слишком**установки \> управления безопасностью**.</span><span class="sxs-lookup"><span data-stu-id="9acc9-137">Go too**Setup \> Security Control**.</span></span>
   
   <span data-ttu-id="9acc9-138">![Средства управления безопасностью](./media/active-directory-saas-coupa-tutorial/IC791900.png "Средства управления безопасностью")</span><span class="sxs-lookup"><span data-stu-id="9acc9-138">![Security Controls](./media/active-directory-saas-coupa-tutorial/IC791900.png "Security Controls")</span></span>
3. <span data-ttu-id="9acc9-139">toodownload hello Coupa метаданных файла tooyour компьютера, нажмите кнопку **загрузить и импортировать метаданные SP**.</span><span class="sxs-lookup"><span data-stu-id="9acc9-139">toodownload hello Coupa metadata file tooyour computer, click **Download and import SP metadata**.</span></span>
   
   <span data-ttu-id="9acc9-140">![Метаданные Coupa SP](./media/active-directory-saas-coupa-tutorial/IC791901.png "Метаданные Coupa SP")</span><span class="sxs-lookup"><span data-stu-id="9acc9-140">![Coupa SP metadata](./media/active-directory-saas-coupa-tutorial/IC791901.png "Coupa SP metadata")</span></span>
4. <span data-ttu-id="9acc9-141">В другом окне браузера Войдите на классический портал Azure toohello.</span><span class="sxs-lookup"><span data-stu-id="9acc9-141">In a different browser window, sign on toohello Azure classic portal.</span></span>
5. <span data-ttu-id="9acc9-142">На hello **Coupa** странице интеграции приложения щелкните **настроить единый вход** tooopen hello **Настройка единого входа** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="9acc9-142">On hello **Coupa** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="9acc9-143">![Настройка единого входа](./media/active-directory-saas-coupa-tutorial/IC791902.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="9acc9-143">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791902.png "Configure Single Sign-On")</span></span>
6. <span data-ttu-id="9acc9-144">На hello **предпочитаемый как toosign пользователей на tooCoupa** выберите **Microsoft Azure AD Single Sign-On**, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="9acc9-144">On hello **How would you like users toosign on tooCoupa** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="9acc9-145">![Настройка единого входа](./media/active-directory-saas-coupa-tutorial/IC791903.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="9acc9-145">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791903.png "Configure Single Sign-On")</span></span>
7. <span data-ttu-id="9acc9-146">На hello **настроить URL-адрес приложения** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="9acc9-146">On hello **Configure App URL** page, perform hello following steps:</span></span>
   
   <span data-ttu-id="9acc9-147">![Настройка URL-адреса приложения](./media/active-directory-saas-coupa-tutorial/IC791904.png "Настройка URL-адреса приложения")</span><span class="sxs-lookup"><span data-stu-id="9acc9-147">![Configure App URL](./media/active-directory-saas-coupa-tutorial/IC791904.png "Configure App URL")</span></span>   
   1. <span data-ttu-id="9acc9-148">В hello **на URL-адрес входа** текстовом поле введите URL-адрес, используемый вашей toosign пользователей на tooyour приложение Coupa (например: «*http://company.Coupa.com*»).</span><span class="sxs-lookup"><span data-stu-id="9acc9-148">In hello **Sign On URL** textbox, type URL used by your users toosign on tooyour Coupa application (e.g.: “*http://company.Coupa.com*”).</span></span>
   2. <span data-ttu-id="9acc9-149">Откройте скачанный файл метаданных Coupa и скопируйте hello **AssertionConsumerService index/URL**.</span><span class="sxs-lookup"><span data-stu-id="9acc9-149">Open your downloaded Coupa metadata file, and then copy hello **AssertionConsumerService index/URL**.</span></span>
   3. <span data-ttu-id="9acc9-150">В hello **URL-адрес ответа Coupa** текстовое поле, вставить hello **AssertionConsumerService index/URL** значение.</span><span class="sxs-lookup"><span data-stu-id="9acc9-150">In hello **Coupa Reply URL** textbox, paste hello **AssertionConsumerService index/URL** value.</span></span>
   4. <span data-ttu-id="9acc9-151">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="9acc9-151">Click **Next**.</span></span>
8. <span data-ttu-id="9acc9-152">На hello **настройки единого входа в Coupa** страницы, toodownload файл метаданных, нажмите кнопку **загрузить метаданные**, а затем сохраните файл hello на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="9acc9-152">On hello **Configure single sign-on at Coupa** page, toodownload your metadata file, click **Download metadata**, and then save hello file locally on your computer.</span></span>
   
   <span data-ttu-id="9acc9-153">![Настройка единого входа](./media/active-directory-saas-coupa-tutorial/IC791905.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="9acc9-153">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791905.png "Configure Single Sign-On")</span></span>
9. <span data-ttu-id="9acc9-154">На сайте Coupa компании hello перейдите слишком**установки \> управления безопасностью**.</span><span class="sxs-lookup"><span data-stu-id="9acc9-154">On hello Coupa company site, go too**Setup \> Security Control**.</span></span>
   
   <span data-ttu-id="9acc9-155">![Средства управления безопасностью](./media/active-directory-saas-coupa-tutorial/IC791900.png "Средства управления безопасностью")</span><span class="sxs-lookup"><span data-stu-id="9acc9-155">![Security Controls](./media/active-directory-saas-coupa-tutorial/IC791900.png "Security Controls")</span></span>
10. <span data-ttu-id="9acc9-156">В hello **вход с использованием учетных данных Coupa** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="9acc9-156">In hello **Log in using Coupa credentials** section, perform hello following steps:</span></span>  

   <span data-ttu-id="9acc9-157">![Вход с использованием учетных данных Coupa](./media/active-directory-saas-coupa-tutorial/IC791906.png "Вход с использованием учетных данных Coupa")</span><span class="sxs-lookup"><span data-stu-id="9acc9-157">![Log in using Coupa credentials](./media/active-directory-saas-coupa-tutorial/IC791906.png "Log in using Coupa credentials")</span></span> 
   1. <span data-ttu-id="9acc9-158">Выберите **Вход с помощью SAML**.</span><span class="sxs-lookup"><span data-stu-id="9acc9-158">Select **Log in using SAML**.</span></span>
   2. <span data-ttu-id="9acc9-159">Нажмите кнопку **Обзор** tooupload скачанный файл метаданных Azure Active.</span><span class="sxs-lookup"><span data-stu-id="9acc9-159">Click **Browse** tooupload your downloaded Azure Active metadata file.</span></span>
   3. <span data-ttu-id="9acc9-160">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="9acc9-160">Click **Save**.</span></span>
11. <span data-ttu-id="9acc9-161">На hello классический портал Azure, выберите Подтверждение настройки единого входа hello и нажмите кнопку **завершить** tooclose hello **Настройка единого входа** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="9acc9-161">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
    
   <span data-ttu-id="9acc9-162">![Настройка единого входа](./media/active-directory-saas-coupa-tutorial/IC791907.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="9acc9-162">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791907.png "Configure Single Sign-On")</span></span>
    
## <a name="configure-user-provisioning"></a><span data-ttu-id="9acc9-163">Настроить подготовку учетных записей пользователей</span><span class="sxs-lookup"><span data-stu-id="9acc9-163">Configure user provisioning</span></span>

<span data-ttu-id="9acc9-164">В порядке tooenable toolog пользователей Azure AD в Coupa их необходимо подготовить в Coupa.</span><span class="sxs-lookup"><span data-stu-id="9acc9-164">In order tooenable Azure AD users toolog into Coupa, they must be provisioned into Coupa.</span></span>  

* <span data-ttu-id="9acc9-165">В случае hello объекта Coupa Подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="9acc9-165">In hello case of Coupa, provisioning is a manual task.</span></span>

<span data-ttu-id="9acc9-166">**tooconfigure подготовки пользователей, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="9acc9-166">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="9acc9-167">Войдите в tooyour **Coupa** сайт компании от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="9acc9-167">Log in tooyour **Coupa** company site as administrator.</span></span>
2. <span data-ttu-id="9acc9-168">В меню в верхней части hello hello выберите **установки**и нажмите кнопку **пользователей**.</span><span class="sxs-lookup"><span data-stu-id="9acc9-168">In hello menu on hello top, click **Setup**, and then click **Users**.</span></span>
   
   <span data-ttu-id="9acc9-169">![Пользователи](./media/active-directory-saas-coupa-tutorial/IC791908.png "Пользователи")</span><span class="sxs-lookup"><span data-stu-id="9acc9-169">![Users](./media/active-directory-saas-coupa-tutorial/IC791908.png "Users")</span></span>
3. <span data-ttu-id="9acc9-170">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="9acc9-170">Click **Create**.</span></span>
   
   <span data-ttu-id="9acc9-171">![Создание пользователей](./media/active-directory-saas-coupa-tutorial/IC791909.png "Создание пользователей")</span><span class="sxs-lookup"><span data-stu-id="9acc9-171">![Create Users](./media/active-directory-saas-coupa-tutorial/IC791909.png "Create Users")</span></span>
4. <span data-ttu-id="9acc9-172">В hello **создать пользователя** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="9acc9-172">In hello **User Create** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="9acc9-173">![Сведения о пользователе](./media/active-directory-saas-coupa-tutorial/IC791910.png "Сведения о пользователе")</span><span class="sxs-lookup"><span data-stu-id="9acc9-173">![User Details](./media/active-directory-saas-coupa-tutorial/IC791910.png "User Details")</span></span>
   
   1. <span data-ttu-id="9acc9-174">Тип hello **входа**, **имя**, **Фамилия**, **идентификатор-**, **электронной почты** атрибуты допустимую учетную запись Azure Active Directory, требуется tooprovision в hello связанные текстовые поля.</span><span class="sxs-lookup"><span data-stu-id="9acc9-174">Type hello **Login**, **First name**, **Last Name**, **Single Sign-On ID**, **Email** attributes of a valid Azure Active Directory account you want tooprovision into hello related textboxes.</span></span>
   2. <span data-ttu-id="9acc9-175">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="9acc9-175">Click **Create**.</span></span>   
   >[!NOTE]
   ><span data-ttu-id="9acc9-176">Владелец учетной записи Hello Azure Active Directory получит сообщение электронной почты с учетной записью hello tooconfirm ссылку, чтобы она стала активной.</span><span class="sxs-lookup"><span data-stu-id="9acc9-176">hello Azure Active Directory account holder will get an email with a link tooconfirm hello account before it becomes active.</span></span> 
   > 

>[!NOTE]
><span data-ttu-id="9acc9-177">Можно использовать любые другие Coupa пользователя средства создания учетных записей или интерфейсы API, предоставляемые Coupa tooprovision учетных записей пользователей AAD.</span><span class="sxs-lookup"><span data-stu-id="9acc9-177">You can use any other Coupa user account creation tools or APIs provided by Coupa tooprovision AAD user accounts.</span></span> 
> 

## <a name="assign-users"></a><span data-ttu-id="9acc9-178">Назначить пользователей</span><span class="sxs-lookup"><span data-stu-id="9acc9-178">Assign users</span></span>
<span data-ttu-id="9acc9-179">tootest конфигурацию, необходимо toogrant hello Azure AD пользователей с помощью tooit доступ вашего приложения путем назначения им tooallow.</span><span class="sxs-lookup"><span data-stu-id="9acc9-179">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="9acc9-180">**tooCoupa tooassign пользователей, выполните следующие шаги hello:**</span><span class="sxs-lookup"><span data-stu-id="9acc9-180">**tooassign users tooCoupa, perform hello following steps:**</span></span>

1. <span data-ttu-id="9acc9-181">В hello классический портал Azure создайте тестовую учетную запись.</span><span class="sxs-lookup"><span data-stu-id="9acc9-181">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="9acc9-182">На hello ** Coupa ** странице интеграции приложения щелкните **назначить пользователей**.</span><span class="sxs-lookup"><span data-stu-id="9acc9-182">On hello **Coupa **application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="9acc9-183">![Назначение пользователей](./media/active-directory-saas-coupa-tutorial/IC791911.png "Назначение пользователей")</span><span class="sxs-lookup"><span data-stu-id="9acc9-183">![Assign Users](./media/active-directory-saas-coupa-tutorial/IC791911.png "Assign Users")</span></span>
3. <span data-ttu-id="9acc9-184">Выберите тестового пользователя, нажмите кнопку **назначить**, а затем нажмите кнопку **Да** tooconfirm назначения.</span><span class="sxs-lookup"><span data-stu-id="9acc9-184">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
   <span data-ttu-id="9acc9-185">![Да](./media/active-directory-saas-coupa-tutorial/IC767830.png "Да")</span><span class="sxs-lookup"><span data-stu-id="9acc9-185">![Yes](./media/active-directory-saas-coupa-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="9acc9-186">Tootest параметры единого входа, откройте панель доступа hello.</span><span class="sxs-lookup"><span data-stu-id="9acc9-186">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="9acc9-187">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="9acc9-187">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

