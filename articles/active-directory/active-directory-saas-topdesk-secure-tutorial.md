---
title: "Руководство по интеграции Azure Active Directory с TOPdesk — Secure | Документация Майкрософт"
description: "Узнайте, как toouse TOPdesk - Secure с Azure Active Directory tooenable единого входа, автоматизированной подготовки и многое другое!."
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 8e149d2d-7849-48ec-9993-31f4ade5fdb4
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/22/2017
ms.author: jeedes
ms.openlocfilehash: 10fe420d1691c2845b89c779486ffd6fcd736432
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-topdesk---secure"></a><span data-ttu-id="59e50-103">Учебник. Интеграция Azure Active Directory с TOPdesk — Secure</span><span class="sxs-lookup"><span data-stu-id="59e50-103">Tutorial: Azure Active Directory integration with TOPdesk - Secure</span></span>
<span data-ttu-id="59e50-104">Цель этого учебника Hello tooshow hello интеграцию Azure и TOPdesk - Secure.</span><span class="sxs-lookup"><span data-stu-id="59e50-104">hello objective of this tutorial is tooshow hello integration of Azure and TOPdesk - Secure.</span></span>  
<span data-ttu-id="59e50-105">Hello сценарий, описанный в этом руководстве предполагается, что уже hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="59e50-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="59e50-106">Действующая подписка на Azure</span><span class="sxs-lookup"><span data-stu-id="59e50-106">A valid Azure subscription</span></span>
* <span data-ttu-id="59e50-107">Подписка TOPdesk — Secure с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="59e50-107">A TOPdesk - Secure single sign-on enabled subscription</span></span>

<span data-ttu-id="59e50-108">Изучив этот учебник, пользователи Azure AD hello назначенные tooTOPdesk - безопасный будет быть может toosingle входа в приложение hello в версию TOPdesk - сайте компании безопасной (инициированный поставщиком вход службы) или с помощью hello [введение Панель доступа toohello](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="59e50-108">After completing this tutorial, hello Azure AD users you have assigned tooTOPdesk - Secure will be able toosingle sign into hello application at your TOPdesk - Secure company site (service provider initiated sign on), or using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="59e50-109">Hello сценарий, описанный в этом руководстве состоит из hello следующие стандартные блоки.</span><span class="sxs-lookup"><span data-stu-id="59e50-109">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

1. <span data-ttu-id="59e50-110">Включение интеграции приложений hello для безопасной версии TOPdesk</span><span class="sxs-lookup"><span data-stu-id="59e50-110">Enabling hello application integration for TOPdesk - Secure</span></span>
2. <span data-ttu-id="59e50-111">Настройка единого входа</span><span class="sxs-lookup"><span data-stu-id="59e50-111">Configuring single sign-on</span></span>
3. <span data-ttu-id="59e50-112">Настройка подготовки учетных записей пользователей</span><span class="sxs-lookup"><span data-stu-id="59e50-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="59e50-113">Назначение пользователей</span><span class="sxs-lookup"><span data-stu-id="59e50-113">Assigning users</span></span>

<span data-ttu-id="59e50-114">![Сценарий](./media/active-directory-saas-topdesk-secure-tutorial/IC790596.png "Сценарий")</span><span class="sxs-lookup"><span data-stu-id="59e50-114">![Scenario](./media/active-directory-saas-topdesk-secure-tutorial/IC790596.png "Scenario")</span></span>

## <a name="enabling-hello-application-integration-for-topdesk---secure"></a><span data-ttu-id="59e50-115">Включение интеграции приложений hello для безопасной версии TOPdesk</span><span class="sxs-lookup"><span data-stu-id="59e50-115">Enabling hello application integration for TOPdesk - Secure</span></span>
<span data-ttu-id="59e50-116">Hello цель этого раздела — toooutline как интеграции приложения hello tooenable для безопасной версии TOPdesk.</span><span class="sxs-lookup"><span data-stu-id="59e50-116">hello objective of this section is toooutline how tooenable hello application integration for TOPdesk - Secure.</span></span>

### <a name="tooenable-hello-application-integration-for-topdesk---secure-perform-hello-following-steps"></a><span data-ttu-id="59e50-117">tooenable hello приложения интеграции для версии TOPdesk — безопасный, выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="59e50-117">tooenable hello application integration for TOPdesk - Secure, perform hello following steps:</span></span>
1. <span data-ttu-id="59e50-118">В hello классический портал Azure, hello левой области навигации, выберите **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="59e50-118">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="59e50-119">![Active Directory](./media/active-directory-saas-topdesk-secure-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="59e50-119">![Active Directory](./media/active-directory-saas-topdesk-secure-tutorial/IC700993.png "Active Directory")</span></span>

2. <span data-ttu-id="59e50-120">Из hello **каталога** список, выберите hello каталога, для которого требуется Интеграция каталогов tooenable.</span><span class="sxs-lookup"><span data-stu-id="59e50-120">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>

3. <span data-ttu-id="59e50-121">Щелкните представление приложения hello tooopen в представлении каталога hello **приложений** в верхнем меню hello.</span><span class="sxs-lookup"><span data-stu-id="59e50-121">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    <span data-ttu-id="59e50-122">![Приложения](./media/active-directory-saas-topdesk-secure-tutorial/IC700994.png "Приложения")</span><span class="sxs-lookup"><span data-stu-id="59e50-122">![Applications](./media/active-directory-saas-topdesk-secure-tutorial/IC700994.png "Applications")</span></span>

4. <span data-ttu-id="59e50-123">Нажмите кнопку **добавить** hello нижней части страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="59e50-123">Click **Add** at hello bottom of hello page.</span></span>
   
    <span data-ttu-id="59e50-124">![Добавление приложения](./media/active-directory-saas-topdesk-secure-tutorial/IC749321.png "Добавление приложения")</span><span class="sxs-lookup"><span data-stu-id="59e50-124">![Add application](./media/active-directory-saas-topdesk-secure-tutorial/IC749321.png "Add application")</span></span>

5. <span data-ttu-id="59e50-125">На hello **что вам требуется toodo** диалоговое окно, нажмите кнопку **добавить приложение из коллекции hello**.</span><span class="sxs-lookup"><span data-stu-id="59e50-125">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    <span data-ttu-id="59e50-126">![Добавление приложения из коллекции](./media/active-directory-saas-topdesk-secure-tutorial/IC749322.png "Добавление приложения из коллекции")</span><span class="sxs-lookup"><span data-stu-id="59e50-126">![Add an application from gallerry](./media/active-directory-saas-topdesk-secure-tutorial/IC749322.png "Add an application from gallerry")</span></span>

6. <span data-ttu-id="59e50-127">В hello **поле поиска**, тип **безопасной версии TOPdesk**.</span><span class="sxs-lookup"><span data-stu-id="59e50-127">In hello **search box**, type **TOPdesk - Secure**.</span></span>
   
    <span data-ttu-id="59e50-128">![Коллекция приложений](./media/active-directory-saas-topdesk-secure-tutorial/IC790597.png "Коллекция приложений")</span><span class="sxs-lookup"><span data-stu-id="59e50-128">![Application Gallery](./media/active-directory-saas-topdesk-secure-tutorial/IC790597.png "Application Gallery")</span></span>

7. <span data-ttu-id="59e50-129">В области результатов hello выберите **безопасной версии TOPdesk**и нажмите кнопку **завершить** tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="59e50-129">In hello results pane, select **TOPdesk - Secure**, and then click **Complete** tooadd hello application.</span></span>
   
    <span data-ttu-id="59e50-130">![TOPdesk — Secure](./media/active-directory-saas-topdesk-secure-tutorial/IC791933.png "TOPdesk — Secure")</span><span class="sxs-lookup"><span data-stu-id="59e50-130">![TOPdesk - Secure](./media/active-directory-saas-topdesk-secure-tutorial/IC791933.png "TOPdesk - Secure")</span></span>

## <a name="configuring-single-sign-on"></a><span data-ttu-id="59e50-131">Настройка единого входа</span><span class="sxs-lookup"><span data-stu-id="59e50-131">Configuring single sign-on</span></span>
<span data-ttu-id="59e50-132">Hello цель этого раздела — toooutline как tooTOPdesk tooauthenticate пользователей tooenable - защитить с помощью учетной записи в Azure AD, используя федерацию основании hello протокола SAML.</span><span class="sxs-lookup"><span data-stu-id="59e50-132">hello objective of this section is toooutline how tooenable users tooauthenticate tooTOPdesk - Secure with their account in Azure AD using federation based on hello SAML protocol.</span></span>  
<span data-ttu-id="59e50-133">Настройка единого входа для безопасной версии TOPdesk требуется tooupload файл значка логотипа.</span><span class="sxs-lookup"><span data-stu-id="59e50-133">Configuring single sign-on for TOPdesk - Secure requires you tooupload a logo icon file.</span></span> <span data-ttu-id="59e50-134">файл значка hello tooget, поддержки topdesk контактов hello.</span><span class="sxs-lookup"><span data-stu-id="59e50-134">tooget hello icon file, contact hello TOPdesk support team.</span></span>

### <a name="tooconfigure-single-sign-on-perform-hello-following-steps"></a><span data-ttu-id="59e50-135">tooconfigure единого входа, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="59e50-135">tooconfigure single sign-on, perform hello following steps:</span></span>
1. <span data-ttu-id="59e50-136">Войдите на tooyour **безопасной версии TOPdesk** сайт компании от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="59e50-136">Sign on tooyour **TOPdesk - Secure** company site as an administrator.</span></span>
2. <span data-ttu-id="59e50-137">В hello **TOPdesk** меню, нажмите кнопку **параметры**.</span><span class="sxs-lookup"><span data-stu-id="59e50-137">In hello **TOPdesk** menu, click **Settings**.</span></span>
   
    <span data-ttu-id="59e50-138">![Параметры](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "Параметры")</span><span class="sxs-lookup"><span data-stu-id="59e50-138">![Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "Settings")</span></span>

3. <span data-ttu-id="59e50-139">Щелкните **Параметры входа**.</span><span class="sxs-lookup"><span data-stu-id="59e50-139">Click **Login Settings**.</span></span>
   
    <span data-ttu-id="59e50-140">![Параметры входа](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "Параметры входа")</span><span class="sxs-lookup"><span data-stu-id="59e50-140">![Login Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "Login Settings")</span></span>

4. <span data-ttu-id="59e50-141">Разверните hello **параметры входа** меню, а затем нажмите **Общие**.</span><span class="sxs-lookup"><span data-stu-id="59e50-141">Expand hello **Login Settings** menu, and then click **General**.</span></span>
   
    <span data-ttu-id="59e50-142">![Общие](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "Общие")</span><span class="sxs-lookup"><span data-stu-id="59e50-142">![General](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "General")</span></span>

5. <span data-ttu-id="59e50-143">В hello **Secure** раздел hello **входа SAML** конфигурации выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="59e50-143">In hello **Secure** section of hello **SAML login** configuration section, perform hello following steps:</span></span>
   
    <span data-ttu-id="59e50-144">![Технические параметры](./media/active-directory-saas-topdesk-secure-tutorial/IC790855.png "Технические параметры")</span><span class="sxs-lookup"><span data-stu-id="59e50-144">![Technical Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790855.png "Technical Settings")</span></span>
   
    <span data-ttu-id="59e50-145">а.</span><span class="sxs-lookup"><span data-stu-id="59e50-145">a.</span></span> <span data-ttu-id="59e50-146">Нажмите кнопку **загрузки** toodownload hello общедоступный файл метаданных, а затем сохраните его локально на компьютере.</span><span class="sxs-lookup"><span data-stu-id="59e50-146">Click **Download** toodownload hello public metadata file, and then save it locally on your computer.</span></span>
   
    <span data-ttu-id="59e50-147">b.</span><span class="sxs-lookup"><span data-stu-id="59e50-147">b.</span></span> <span data-ttu-id="59e50-148">Откройте файл метаданных hello, а затем найдите hello **AssertionConsumerService** узла.</span><span class="sxs-lookup"><span data-stu-id="59e50-148">Open hello metadata file, and then locate hello **AssertionConsumerService** node.</span></span>
    
    <span data-ttu-id="59e50-149">![Служба обработчика утверждений](./media/active-directory-saas-topdesk-secure-tutorial/IC790856.png "Служба обработчика утверждений")</span><span class="sxs-lookup"><span data-stu-id="59e50-149">![Assertion Consumer Service](./media/active-directory-saas-topdesk-secure-tutorial/IC790856.png "Assertion Consumer Service")</span></span>
   
    <span data-ttu-id="59e50-150">c.</span><span class="sxs-lookup"><span data-stu-id="59e50-150">c.</span></span> <span data-ttu-id="59e50-151">Копировать hello **AssertionConsumerService** значение.</span><span class="sxs-lookup"><span data-stu-id="59e50-151">Copy hello **AssertionConsumerService** value.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="59e50-152">Будет необходимо hello значение в hello **настроить URL-адрес приложения** далее в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="59e50-152">You will need hello value in hello **Configure App URL** section later in this tutorial.</span></span>
    > 
    > 

6. <span data-ttu-id="59e50-153">В другом окне веб-браузера войдите на **классический портал Azure** в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="59e50-153">In a different web browser window, log into your **Azure classic portal** as an administrator.</span></span>

7. <span data-ttu-id="59e50-154">На hello **безопасной версии TOPdesk** странице интеграции приложения щелкните **настроить единый вход** tooopen hello ** Настройка единого входа ** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="59e50-154">On hello **TOPdesk - Secure** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On ** dialog.</span></span>
   
    <span data-ttu-id="59e50-155">![Настройка единого входа](./media/active-directory-saas-topdesk-secure-tutorial/IC790602.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="59e50-155">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790602.png "Configure Single Sign-On")</span></span>

8. <span data-ttu-id="59e50-156">На hello **как как toosign пользователей на tooTOPdesk - Secure** выберите **Microsoft Azure AD Single Sign-On**, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="59e50-156">On hello **How would you like users toosign on tooTOPdesk - Secure** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="59e50-157">![Настройка единого входа](./media/active-directory-saas-topdesk-secure-tutorial/IC790603.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="59e50-157">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790603.png "Configure Single Sign-On")</span></span>

9. <span data-ttu-id="59e50-158">На hello **настроить URL-адрес приложения** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="59e50-158">On hello **Configure App URL** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="59e50-159">![Настройка URL-адреса приложения](./media/active-directory-saas-topdesk-secure-tutorial/IC790604.png "Настройка URL-адреса приложения")</span><span class="sxs-lookup"><span data-stu-id="59e50-159">![Configure App URL](./media/active-directory-saas-topdesk-secure-tutorial/IC790604.png "Configure App URL")</span></span>
   
    <span data-ttu-id="59e50-160">а.</span><span class="sxs-lookup"><span data-stu-id="59e50-160">a.</span></span> <span data-ttu-id="59e50-161">В hello **TOPdesk - Secure на URL-адрес входа** textbox hello введите URL-адрес, используемый вашей toosign пользователей в вашей безопасную версию TOPdesk (например: «*https://qssolutions.topdesk.net*»).</span><span class="sxs-lookup"><span data-stu-id="59e50-161">In hello **TOPdesk - Secure Sign On URL** textbox, type hello URL used by your users toosign into your TOPdesk - Secure application (e.g.: "*https://qssolutions.topdesk.net*").</span></span>
   
    <span data-ttu-id="59e50-162">b.</span><span class="sxs-lookup"><span data-stu-id="59e50-162">b.</span></span> <span data-ttu-id="59e50-163">В hello **TOPdesk — общедоступный URL-адрес ответа** текстовое поле, вставить hello **TOPdesk - Secure URL-адрес AssertionConsumerService** (например: «*https://qssolutions.topdesk.net/tas/public/login/saml*")</span><span class="sxs-lookup"><span data-stu-id="59e50-163">In hello **TOPdesk – Public Reply URL** textbox, paste hello **TOPdesk - Secure AssertionConsumerService URL** (e.g.: "*https://qssolutions.topdesk.net/tas/public/login/saml*")</span></span>
   
    <span data-ttu-id="59e50-164">c.</span><span class="sxs-lookup"><span data-stu-id="59e50-164">c.</span></span> <span data-ttu-id="59e50-165">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="59e50-165">Click **Next**.</span></span>

10. <span data-ttu-id="59e50-166">На hello **настройки единого входа в безопасную версию TOPdesk** страницы, toodownload файл метаданных, нажмите кнопку **загрузить метаданные**, а затем сохраните файл hello на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="59e50-166">On hello **Configure single sign-on at TOPdesk - Secure** page, toodownload your metadata file, click **Download metadata**, and then save hello file locally on your computer.</span></span>
    
    <span data-ttu-id="59e50-167">![Настройка единого входа](./media/active-directory-saas-topdesk-secure-tutorial/IC790605.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="59e50-167">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790605.png "Configure Single Sign-On")</span></span>

11. <span data-ttu-id="59e50-168">toocreate файлом сертификата, выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="59e50-168">toocreate a certificate file, perform hello following steps:</span></span>
    
    <span data-ttu-id="59e50-169">![Сертификат](./media/active-directory-saas-topdesk-secure-tutorial/IC790606.png "Сертификат")</span><span class="sxs-lookup"><span data-stu-id="59e50-169">![Certificate](./media/active-directory-saas-topdesk-secure-tutorial/IC790606.png "Certificate")</span></span>
    
    <span data-ttu-id="59e50-170">а.</span><span class="sxs-lookup"><span data-stu-id="59e50-170">a.</span></span> <span data-ttu-id="59e50-171">Откройте hello скачанный файл метаданных.</span><span class="sxs-lookup"><span data-stu-id="59e50-171">Open hello downloaded metadata file.</span></span>
    <span data-ttu-id="59e50-172">b.</span><span class="sxs-lookup"><span data-stu-id="59e50-172">b.</span></span> <span data-ttu-id="59e50-173">Разверните hello **RoleDescriptor** узла, имеющего **xsi: Type** из **fed: ApplicationServiceType**.</span><span class="sxs-lookup"><span data-stu-id="59e50-173">Expand hello **RoleDescriptor** node that has a **xsi:type** of **fed:ApplicationServiceType**.</span></span>
    <span data-ttu-id="59e50-174">c.</span><span class="sxs-lookup"><span data-stu-id="59e50-174">c.</span></span> <span data-ttu-id="59e50-175">Скопируйте значение hello hello **X509Certificate** узла.</span><span class="sxs-lookup"><span data-stu-id="59e50-175">Copy hello value of hello **X509Certificate** node.</span></span>
    <span data-ttu-id="59e50-176">d.</span><span class="sxs-lookup"><span data-stu-id="59e50-176">d.</span></span> <span data-ttu-id="59e50-177">Сохранить hello копируются **X509Certificate** значение на локальном компьютере в файле.</span><span class="sxs-lookup"><span data-stu-id="59e50-177">Save hello copied **X509Certificate** value locally on your computer in a file.</span></span>

12. <span data-ttu-id="59e50-178">В версии TOPdesk - Secure корпоративный сайт в hello **TOPdesk** меню, нажмите кнопку **параметры**.</span><span class="sxs-lookup"><span data-stu-id="59e50-178">On your TOPdesk - Secure company site, in hello **TOPdesk** menu, click **Settings**.</span></span>
    
    <span data-ttu-id="59e50-179">![Параметры](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "Параметры")</span><span class="sxs-lookup"><span data-stu-id="59e50-179">![Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790598.png "Settings")</span></span>

13. <span data-ttu-id="59e50-180">Щелкните **Параметры входа**.</span><span class="sxs-lookup"><span data-stu-id="59e50-180">Click **Login Settings**.</span></span>
    
    <span data-ttu-id="59e50-181">![Параметры входа](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "Параметры входа")</span><span class="sxs-lookup"><span data-stu-id="59e50-181">![Login Settings](./media/active-directory-saas-topdesk-secure-tutorial/IC790599.png "Login Settings")</span></span>

14. <span data-ttu-id="59e50-182">Разверните hello **параметры входа** меню, а затем нажмите **Общие**.</span><span class="sxs-lookup"><span data-stu-id="59e50-182">Expand hello **Login Settings** menu, and then click **General**.</span></span>
    
    <span data-ttu-id="59e50-183">![Общие](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "Общие")</span><span class="sxs-lookup"><span data-stu-id="59e50-183">![General](./media/active-directory-saas-topdesk-secure-tutorial/IC790600.png "General")</span></span>

15. <span data-ttu-id="59e50-184">В hello **открытый** щелкните **добавить**.</span><span class="sxs-lookup"><span data-stu-id="59e50-184">In hello **Public** section, click **Add**.</span></span>
    
    <span data-ttu-id="59e50-185">![Добавление](./media/active-directory-saas-topdesk-secure-tutorial/IC790607.png "Добавление")</span><span class="sxs-lookup"><span data-stu-id="59e50-185">![Add](./media/active-directory-saas-topdesk-secure-tutorial/IC790607.png "Add")</span></span>

16. <span data-ttu-id="59e50-186">На hello **помощник по настройке SAML** диалогового окна выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="59e50-186">On hello **SAML configuration assistant** dialog page, perform hello following steps:</span></span>
    
    <span data-ttu-id="59e50-187">![Помощник по настройке SAML](./media/active-directory-saas-topdesk-secure-tutorial/IC790608.png "Помощник по настройке SAML")</span><span class="sxs-lookup"><span data-stu-id="59e50-187">![SAML Configuration Assistant](./media/active-directory-saas-topdesk-secure-tutorial/IC790608.png "SAML Configuration Assistant")</span></span>
    
    <span data-ttu-id="59e50-188">а.</span><span class="sxs-lookup"><span data-stu-id="59e50-188">a.</span></span> <span data-ttu-id="59e50-189">tooupload метаданные загруженного файла в разделе **метаданные федерации**, нажмите кнопку **Обзор**.</span><span class="sxs-lookup"><span data-stu-id="59e50-189">tooupload your downloaded metadata file, under **Federation Metadata**, click **Browse**.</span></span>

    <span data-ttu-id="59e50-190">b.</span><span class="sxs-lookup"><span data-stu-id="59e50-190">b.</span></span> <span data-ttu-id="59e50-191">файл сертификата, в разделе tooupload **сертификат (RSA)**, нажмите кнопку **Обзор**.</span><span class="sxs-lookup"><span data-stu-id="59e50-191">tooupload your certificate file, under **Certificate (RSA)**, click **Browse**.</span></span>

    <span data-ttu-id="59e50-192">c.</span><span class="sxs-lookup"><span data-stu-id="59e50-192">c.</span></span> <span data-ttu-id="59e50-193">Файл эмблемы hello tooupload, полученного от поддержки topdesk hello в разделе **значок логотипа**, нажмите кнопку **Обзор**.</span><span class="sxs-lookup"><span data-stu-id="59e50-193">tooupload hello logo file you got from hello TOPdesk support team, under **Logo icon**, click **Browse**.</span></span>

    <span data-ttu-id="59e50-194">d.</span><span class="sxs-lookup"><span data-stu-id="59e50-194">d.</span></span> <span data-ttu-id="59e50-195">В hello **атрибут имени пользователя** введите **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="59e50-195">In hello **User name attribute** textbox, type **http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress**.</span></span>

    <span data-ttu-id="59e50-196">д.</span><span class="sxs-lookup"><span data-stu-id="59e50-196">e.</span></span> <span data-ttu-id="59e50-197">В hello **отображаемое имя** текстовом поле введите имя для конфигурации.</span><span class="sxs-lookup"><span data-stu-id="59e50-197">In hello **Display name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="59e50-198">f.</span><span class="sxs-lookup"><span data-stu-id="59e50-198">f.</span></span> <span data-ttu-id="59e50-199">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="59e50-199">Click **Save**.</span></span>

17. <span data-ttu-id="59e50-200">На hello классический портал Azure, выберите Подтверждение настройки единого входа hello и нажмите кнопку **завершить** tooclose hello **Настройка единого входа** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="59e50-200">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="59e50-201">![Настройка единого входа](./media/active-directory-saas-topdesk-secure-tutorial/IC790609.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="59e50-201">![Configure Single Sign-On](./media/active-directory-saas-topdesk-secure-tutorial/IC790609.png "Configure Single Sign-On")</span></span>

## <a name="configuring-user-provisioning"></a><span data-ttu-id="59e50-202">Настройка подготовки учетных записей пользователей</span><span class="sxs-lookup"><span data-stu-id="59e50-202">Configuring user provisioning</span></span>
<span data-ttu-id="59e50-203">В порядке tooenable Azure AD пользователи toolog в версии TOPdesk - уровень безопасности, их необходимо подготовить в безопасной версии TOPdesk.</span><span class="sxs-lookup"><span data-stu-id="59e50-203">In order tooenable Azure AD users toolog into TOPdesk - Secure, they must be provisioned into TOPdesk - Secure.</span></span>  
<span data-ttu-id="59e50-204">В случае TOPdesk - hello безопасный, Подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="59e50-204">In hello case of TOPdesk - Secure, provisioning is a manual task.</span></span>

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a><span data-ttu-id="59e50-205">tooconfigure подготовки пользователей, выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="59e50-205">tooconfigure user provisioning, perform hello following steps:</span></span>
1. <span data-ttu-id="59e50-206">Войдите на tooyour **безопасной версии TOPdesk** сайт компании от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="59e50-206">Sign on tooyour **TOPdesk - Secure** company site as administrator.</span></span>
2. <span data-ttu-id="59e50-207">В меню в верхней части hello hello выберите **TOPdesk \> New \> файлы поддержки \> оператор**.</span><span class="sxs-lookup"><span data-stu-id="59e50-207">In hello menu on hello top, click **TOPdesk \> New \> Support Files \> Operator**.</span></span>
   
    <span data-ttu-id="59e50-208">![Оператор](./media/active-directory-saas-topdesk-secure-tutorial/IC790610.png "Оператор")</span><span class="sxs-lookup"><span data-stu-id="59e50-208">![Operator](./media/active-directory-saas-topdesk-secure-tutorial/IC790610.png "Operator")</span></span>

3. <span data-ttu-id="59e50-209">На hello **оператор New** диалоговое окно, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="59e50-209">On hello **New Operator** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="59e50-210">![Новый оператор](./media/active-directory-saas-topdesk-secure-tutorial/IC790611.png "Новый оператор")</span><span class="sxs-lookup"><span data-stu-id="59e50-210">![New Operator](./media/active-directory-saas-topdesk-secure-tutorial/IC790611.png "New Operator")</span></span>
   
    <span data-ttu-id="59e50-211">а.</span><span class="sxs-lookup"><span data-stu-id="59e50-211">a.</span></span> <span data-ttu-id="59e50-212">Щелкните вкладку Общие hello.</span><span class="sxs-lookup"><span data-stu-id="59e50-212">Click hello General tab.</span></span>
   
    <span data-ttu-id="59e50-213">b.</span><span class="sxs-lookup"><span data-stu-id="59e50-213">b.</span></span> <span data-ttu-id="59e50-214">В hello **Фамилия** текстового поля из hello **Общие** раздел, имя последнего типа hello действительной учетной записи Azure Active Directory требуется tooprovision.</span><span class="sxs-lookup"><span data-stu-id="59e50-214">In hello **Surname** textbox of hello **General** section, type hello last name of a valid Azure Active Directory account you want tooprovision.</span></span>
   
    <span data-ttu-id="59e50-215">c.</span><span class="sxs-lookup"><span data-stu-id="59e50-215">c.</span></span> <span data-ttu-id="59e50-216">Выберите **сайта** для учетной записи hello в hello **расположение** раздела.</span><span class="sxs-lookup"><span data-stu-id="59e50-216">Select a **Site** for hello account in hello **Location** section.</span></span>
   
    <span data-ttu-id="59e50-217">d.</span><span class="sxs-lookup"><span data-stu-id="59e50-217">d.</span></span> <span data-ttu-id="59e50-218">В hello **имя входа** текстового поля из hello **учетные данные TOPdesk** введите имя входа для пользователя.</span><span class="sxs-lookup"><span data-stu-id="59e50-218">In hello **Login Name** textbox of hello **TOPdesk Login** section, type a login name for your user.</span></span>
   
    <span data-ttu-id="59e50-219">д.</span><span class="sxs-lookup"><span data-stu-id="59e50-219">e.</span></span> <span data-ttu-id="59e50-220">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="59e50-220">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="59e50-221">Можно использовать любые другие версии TOPdesk - учетная запись безопасности пользователя, инструменты для создания или API-интерфейсы, предоставляемые версией TOPdesk - Secure tooprovision учетных записей пользователей AAD.</span><span class="sxs-lookup"><span data-stu-id="59e50-221">You can use any other TOPdesk - Secure user account creation tools or APIs provided by TOPdesk - Secure tooprovision AAD user accounts.</span></span>
> 
> 

## <a name="assigning-users"></a><span data-ttu-id="59e50-222">Назначение пользователей</span><span class="sxs-lookup"><span data-stu-id="59e50-222">Assigning users</span></span>
<span data-ttu-id="59e50-223">tootest конфигурацию, необходимо toogrant hello Azure AD пользователей с помощью tooit доступ вашего приложения путем назначения им tooallow.</span><span class="sxs-lookup"><span data-stu-id="59e50-223">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

### <a name="tooassign-users-tootopdesk---secure-perform-hello-following-steps"></a><span data-ttu-id="59e50-224">tooTOPdesk пользователи tooassign - безопасной, выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="59e50-224">tooassign users tooTOPdesk - Secure, perform hello following steps:</span></span>
1. <span data-ttu-id="59e50-225">В hello классический портал Azure создайте тестовую учетную запись.</span><span class="sxs-lookup"><span data-stu-id="59e50-225">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="59e50-226">На hello ** безопасной версии TOPdesk ** странице интеграции приложения щелкните **назначить пользователей**.</span><span class="sxs-lookup"><span data-stu-id="59e50-226">On hello **TOPdesk - Secure **application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="59e50-227">![Назначение пользователей](./media/active-directory-saas-topdesk-secure-tutorial/IC790612.png "Назначение пользователей")</span><span class="sxs-lookup"><span data-stu-id="59e50-227">![Assign Users](./media/active-directory-saas-topdesk-secure-tutorial/IC790612.png "Assign Users")</span></span>

3. <span data-ttu-id="59e50-228">Выберите тестового пользователя, нажмите кнопку **назначить**, а затем нажмите кнопку **Да** tooconfirm назначения.</span><span class="sxs-lookup"><span data-stu-id="59e50-228">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
    <span data-ttu-id="59e50-229">![Да](./media/active-directory-saas-topdesk-secure-tutorial/IC767830.png "Да")</span><span class="sxs-lookup"><span data-stu-id="59e50-229">![Yes](./media/active-directory-saas-topdesk-secure-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="59e50-230">Tootest параметры единого входа, откройте панель доступа hello.</span><span class="sxs-lookup"><span data-stu-id="59e50-230">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="59e50-231">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="59e50-231">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

