---
title: "Учебник. Интеграция Azure Active Directory с Cisco Webex | Документация Майкрософт"
description: "Узнайте, как toouse Cisco Webex с Azure Active Directory tooenable единого входа, автоматизированной подготовки и многое другое!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 26704ca7-13ed-4261-bf24-fd6252e2072b
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: 9fc11e58a7acaa6fbfb32eeccbfbf85984950e67
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cisco-webex"></a><span data-ttu-id="19464-103">Руководство. Интеграция Azure Active Directory с Cisco Webex</span><span class="sxs-lookup"><span data-stu-id="19464-103">Tutorial: Azure Active Directory Integration with Cisco Webex</span></span>
<span data-ttu-id="19464-104">Цель этого учебника Hello — tooshow hello интеграцию Azure с Cisco Webex.</span><span class="sxs-lookup"><span data-stu-id="19464-104">hello objective of this tutorial is tooshow hello integration of Azure and Cisco Webex.</span></span>  
<span data-ttu-id="19464-105">Hello сценарий, описанный в этом руководстве предполагается, что уже hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="19464-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="19464-106">Действующая подписка на Azure</span><span class="sxs-lookup"><span data-stu-id="19464-106">A valid Azure subscription</span></span>
* <span data-ttu-id="19464-107">Клиент Cisco Webex</span><span class="sxs-lookup"><span data-stu-id="19464-107">A Cisco Webex tenant</span></span>

<span data-ttu-id="19464-108">После завершения этого учебника, Здравствуйте, пользователи Azure AD, назначенные tooCisco будет Webex может toosingle входа в приложение hello на корпоративном сайте Cisco Webex (инициированный поставщиком вход службы) или с помощью hello [toohello введение Получить доступ к панели](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="19464-108">After completing this tutorial, hello Azure AD users you have assigned tooCisco Webex will be able toosingle sign into hello application at your Cisco Webex company site (service provider initiated sign on), or using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="19464-109">Hello сценарий, описанный в этом руководстве состоит из hello следующие стандартные блоки.</span><span class="sxs-lookup"><span data-stu-id="19464-109">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

* <span data-ttu-id="19464-110">Включение интеграции приложений hello для Cisco Webex</span><span class="sxs-lookup"><span data-stu-id="19464-110">Enabling hello application integration for Cisco Webex</span></span>
* <span data-ttu-id="19464-111">Настройка единого входа.</span><span class="sxs-lookup"><span data-stu-id="19464-111">Configuring single sign-on (SSO)</span></span>
* <span data-ttu-id="19464-112">Настройка подготовки учетных записей пользователей</span><span class="sxs-lookup"><span data-stu-id="19464-112">Configuring user provisioning</span></span>
* <span data-ttu-id="19464-113">Назначение пользователей</span><span class="sxs-lookup"><span data-stu-id="19464-113">Assigning users</span></span>

<span data-ttu-id="19464-114">![Сценарий](./media/active-directory-saas-cisco-webex-tutorial/IC777614.png "Сценарий")</span><span class="sxs-lookup"><span data-stu-id="19464-114">![Scenario](./media/active-directory-saas-cisco-webex-tutorial/IC777614.png "Scenario")</span></span>

## <a name="enable-hello-application-integration-for-cisco-webex"></a><span data-ttu-id="19464-115">Включить hello интеграции приложений для Cisco Webex</span><span class="sxs-lookup"><span data-stu-id="19464-115">Enable hello application integration for Cisco Webex</span></span>
<span data-ttu-id="19464-116">Hello цель этого раздела — toooutline как интеграция приложения hello tooenable для Cisco Webex.</span><span class="sxs-lookup"><span data-stu-id="19464-116">hello objective of this section is toooutline how tooenable hello application integration for Cisco Webex.</span></span>

<span data-ttu-id="19464-117">**Интеграция приложения hello tooenable для Cisco Webex, выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="19464-117">**tooenable hello application integration for Cisco Webex, perform hello following steps:**</span></span>

1. <span data-ttu-id="19464-118">В hello классический портал Azure, hello левой области навигации, выберите **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="19464-118">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="19464-119">![Active Directory](./media/active-directory-saas-cisco-webex-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="19464-119">![Active Directory](./media/active-directory-saas-cisco-webex-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="19464-120">Из hello **каталога** список, выберите hello каталога, для которого требуется Интеграция каталогов tooenable.</span><span class="sxs-lookup"><span data-stu-id="19464-120">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="19464-121">Щелкните представление приложения hello tooopen в представлении каталога hello **приложений** в верхнем меню hello.</span><span class="sxs-lookup"><span data-stu-id="19464-121">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
   <span data-ttu-id="19464-122">![Приложения](./media/active-directory-saas-cisco-webex-tutorial/IC700994.png "Приложения")</span><span class="sxs-lookup"><span data-stu-id="19464-122">![Applications](./media/active-directory-saas-cisco-webex-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="19464-123">Нажмите кнопку **добавить** hello нижней части страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="19464-123">Click **Add** at hello bottom of hello page.</span></span>
   
   <span data-ttu-id="19464-124">![Добавление приложения](./media/active-directory-saas-cisco-webex-tutorial/IC749321.png "Добавление приложения")</span><span class="sxs-lookup"><span data-stu-id="19464-124">![Add application](./media/active-directory-saas-cisco-webex-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="19464-125">На hello **что вам требуется toodo** диалоговое окно, нажмите кнопку **добавить приложение из коллекции hello**.</span><span class="sxs-lookup"><span data-stu-id="19464-125">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
   <span data-ttu-id="19464-126">![Добавление приложения из коллекции](./media/active-directory-saas-cisco-webex-tutorial/IC749322.png "Добавление приложения из коллекции")</span><span class="sxs-lookup"><span data-stu-id="19464-126">![Add an application from gallerry](./media/active-directory-saas-cisco-webex-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="19464-127">В hello **поле поиска**, тип **Cisco Webex**.</span><span class="sxs-lookup"><span data-stu-id="19464-127">In hello **search box**, type **Cisco Webex**.</span></span>
   
   <span data-ttu-id="19464-128">![Коллекция приложений](./media/active-directory-saas-cisco-webex-tutorial/IC777615.png "Коллекция приложений")</span><span class="sxs-lookup"><span data-stu-id="19464-128">![Application Gallery](./media/active-directory-saas-cisco-webex-tutorial/IC777615.png "Application Gallery")</span></span>
7. <span data-ttu-id="19464-129">В области результатов hello выберите **Cisco Webex**и нажмите кнопку **завершить** tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="19464-129">In hello results pane, select **Cisco Webex**, and then click **Complete** tooadd hello application.</span></span>
   
   <span data-ttu-id="19464-130">![Cisco Webex](./media/active-directory-saas-cisco-webex-tutorial/IC777616.png "Cisco Webex")</span><span class="sxs-lookup"><span data-stu-id="19464-130">![Cisco Webex](./media/active-directory-saas-cisco-webex-tutorial/IC777616.png "Cisco Webex")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="19464-131">Настройка единого входа</span><span class="sxs-lookup"><span data-stu-id="19464-131">Configure single sign-on</span></span>

<span data-ttu-id="19464-132">Цель этого раздела Hello — toooutline, каким образом пользователи tooenable tooauthenticate tooCisco Webex с помощью учетной записи в Azure AD, используя федерацию на основе hello SAML протокола.</span><span class="sxs-lookup"><span data-stu-id="19464-132">hello objective of this section is toooutline how tooenable users tooauthenticate tooCisco Webex with their account in Azure AD using federation based on hello SAML protocol.</span></span>  

<span data-ttu-id="19464-133">В рамках этой процедуры не toocreate требуется файл сертификата в кодировке base-64.</span><span class="sxs-lookup"><span data-stu-id="19464-133">As part of this procedure, you are required toocreate a base-64 encoded certificate.</span></span> <span data-ttu-id="19464-134">Если вы не знакомы с этой процедурой, см. раздел [как tooconvert двоичные данные сертификата в текстовый файл](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="19464-134">If you are not familiar with this procedure, see [How tooconvert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>

<span data-ttu-id="19464-135">**tooconfigure единого входа, выполните следующие шаги hello:**</span><span class="sxs-lookup"><span data-stu-id="19464-135">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="19464-136">В классический портал Azure, на hello hello **Cisco Webex** странице интеграции приложения щелкните **настроить единый вход** tooopen hello **Настройка единого входа** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="19464-136">In hello Azure classic portal, on hello **Cisco Webex** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="19464-137">![Настройка единого входа](./media/active-directory-saas-cisco-webex-tutorial/IC777617.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="19464-137">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777617.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="19464-138">На hello **предпочитаемый как toosign пользователей на tooCisco Webex** выберите **Microsoft Azure AD Single Sign-On**, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="19464-138">On hello **How would you like users toosign on tooCisco Webex** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="19464-139">![Настройка единого входа](./media/active-directory-saas-cisco-webex-tutorial/IC777618.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="19464-139">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777618.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="19464-140">На hello **настроить URL-адрес приложения** страницы, выполните следующие шаги hello и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="19464-140">On hello **Configure App URL** page, perform hello following steps, and then click **Next**.</span></span>
   
   <span data-ttu-id="19464-141">![Настройка URL-адреса приложения](./media/active-directory-saas-cisco-webex-tutorial/IC777619.png "Настройка URL-адреса приложения")</span><span class="sxs-lookup"><span data-stu-id="19464-141">![Configure app URL](./media/active-directory-saas-cisco-webex-tutorial/IC777619.png "Configure app URL")</span></span>   
   1. <span data-ttu-id="19464-142">В hello **проигрывать на URL-адрес** текстовом поле введите URL-адрес клиента Cisco Webex (например: *http://contoso.webex.com*).</span><span class="sxs-lookup"><span data-stu-id="19464-142">In hello **Sing On URL** textbox, type your Cisco Webex tenant URL (e.g.: *http://contoso.webex.com*).</span></span>
   2. <span data-ttu-id="19464-143">В hello **URL-адрес ответа Cisco Webex** введите ваш **URL-адрес Cisco Webex AssertionConsumerService** (например: *https://company.webex.com/dispatcher/SAML2AuthService?siteurl=company* ).</span><span class="sxs-lookup"><span data-stu-id="19464-143">In hello **Cisco Webex Reply URL** textbox, type your **Cisco Webex AssertionConsumerService URL** (e.g.: *https://company.webex.com/dispatcher/SAML2AuthService?siteurl=company*).</span></span>
4. <span data-ttu-id="19464-144">На hello **настройки единого входа в Cisco Webex** страницы, toodownload свой сертификат, нажмите кнопку **загрузки сертификата**, а затем сохраните файл сертификата hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="19464-144">On hello **Configure single sign-on at Cisco Webex** page, toodownload your certificate, click **Download certificate**, and then save hello certificate file on your computer.</span></span>
   
   <span data-ttu-id="19464-145">![Настройка единого входа](./media/active-directory-saas-cisco-webex-tutorial/IC777620.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="19464-145">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777620.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="19464-146">В другом окне веб-браузера войдите на свой корпоративный веб-сайт Cisco Webex в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="19464-146">In a different web browser window, log into your Cisco Webex company site as an administrator.</span></span>
6. <span data-ttu-id="19464-147">В меню в верхней части hello hello выберите **Администрирование сайта**.</span><span class="sxs-lookup"><span data-stu-id="19464-147">In hello menu on hello top, click **Site Administration**.</span></span>
   
   <span data-ttu-id="19464-148">![Администрирование сайта](./media/active-directory-saas-cisco-webex-tutorial/IC777621.png "Администрирование сайта")</span><span class="sxs-lookup"><span data-stu-id="19464-148">![Site Administration](./media/active-directory-saas-cisco-webex-tutorial/IC777621.png "Site Administration")</span></span>
7. <span data-ttu-id="19464-149">В hello **Управление сайтом** щелкните **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="19464-149">In hello **Manage Site** section, click **SSO Configuration**.</span></span>
   
   <span data-ttu-id="19464-150">![Настройка единого входа](./media/active-directory-saas-cisco-webex-tutorial/IC777622.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="19464-150">![SSO Configuration](./media/active-directory-saas-cisco-webex-tutorial/IC777622.png "SSO Configuration")</span></span>
8. <span data-ttu-id="19464-151">В hello раздел федеративного единого входа веб-конфигурации выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="19464-151">In hello Federated Web SSO Configuration section, perform hello following steps:</span></span>
   
   <span data-ttu-id="19464-152">![Настройка федеративного единого входа](./media/active-directory-saas-cisco-webex-tutorial/IC777623.png "Настройка федеративного единого входа")</span><span class="sxs-lookup"><span data-stu-id="19464-152">![Federated SSO Configuration](./media/active-directory-saas-cisco-webex-tutorial/IC777623.png "Federated SSO Configuration")</span></span>  
   1. <span data-ttu-id="19464-153">Из hello **протокол федерации** выберите **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="19464-153">From hello **Federation Protocol** list, select **SAML 2.0**.</span></span>
   2. <span data-ttu-id="19464-154">Создайте файл **в кодировке Base-64** из скачанного сертификата.</span><span class="sxs-lookup"><span data-stu-id="19464-154">Create a **Base-64 encoded** file from your downloaded certificate.</span></span>  
    >[!TIP]
    ><span data-ttu-id="19464-155">Дополнительные сведения см. в разделе [как tooconvert двоичные данные сертификата в текстовый файл](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="19464-155">For more details, see [How tooconvert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>
    >  
   3. <span data-ttu-id="19464-156">Откройте сертификат в кодировке base-64 в блокноте, а затем hello копирования содержимого его.</span><span class="sxs-lookup"><span data-stu-id="19464-156">Open your base-64 encoded certificate in notepad, and then copy hello content of it.</span></span>
   4. <span data-ttu-id="19464-157">Нажмите **Импорт метаданных SAML**и вставьте сертификат в кодировке Base-64.</span><span class="sxs-lookup"><span data-stu-id="19464-157">Click **Import SAML Metadata**, and then paste your base-64 encoded certificate.</span></span>
   5. <span data-ttu-id="19464-158">В классический портал Azure, на hello hello **настройки единого входа в Cisco Webex** странице диалогового окна, hello копирования **URL-адрес издателя** значение, а затем вставьте его в hello **издатель для SAML (ИД IdP)** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="19464-158">In hello Azure classic portal, on hello **Configure single sign-on at Cisco Webex** dialog page, copy hello **Issuer URL** value, and then paste it into hello **Issuer for SAML (IdP ID)** textbox.</span></span>
   6. <span data-ttu-id="19464-159">В классический портал Azure, на hello hello **настройки единого входа в Cisco Webex** странице диалогового окна, hello копирования **URL-адрес удаленного входа** значение, а затем вставьте его в hello **входа службы единого входа клиента URL-адрес** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="19464-159">In hello Azure classic portal, on hello **Configure single sign-on at Cisco Webex** dialog page, copy hello **Remote Login URL** value, and then paste it into hello **Customer SSO Service Login URL** textbox.</span></span>
   7. <span data-ttu-id="19464-160">Из hello **формата идентификатора имени** выберите **адрес электронной почты**.</span><span class="sxs-lookup"><span data-stu-id="19464-160">From hello **NameID Format** list, select **Email address**.</span></span>
   8. <span data-ttu-id="19464-161">В hello **AuthnContextClassRef** введите **urn: oasis: имена: tc: SAML:2.0:ac:classes:Password**.</span><span class="sxs-lookup"><span data-stu-id="19464-161">In hello **AuthnContextClassRef** textbox, type **urn:oasis:names:tc:SAML:2.0:ac:classes:Password**.</span></span>
   9. <span data-ttu-id="19464-162">В классический портал Azure, на hello hello **настройки единого входа в Cisco Webex** странице диалогового окна, hello копирования **URL-адрес удаленного выхода** значение, а затем вставьте его в hello **выхода службы единого входа клиента URL-адрес** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="19464-162">In hello Azure classic portal, on hello **Configure single sign-on at Cisco Webex** dialog page, copy hello **Remote Logout URL** value, and then paste it into hello **Customer SSO Service Logout URL** textbox.</span></span>
   10. <span data-ttu-id="19464-163">Нажмите кнопку **Обновить**.</span><span class="sxs-lookup"><span data-stu-id="19464-163">Click **Update**.</span></span>
9. <span data-ttu-id="19464-164">В классический портал Azure, на hello hello **настройки единого входа в Cisco Webex** странице диалогового окна выберите Подтверждение настройки единого входа hello и нажмите кнопку **завершить**.</span><span class="sxs-lookup"><span data-stu-id="19464-164">In hello Azure classic portal, on hello **Configure single sign-on at Cisco Webex** dialog page, select hello single sign-on configuration confirmation, and then click **Complete**.</span></span>
   
   <span data-ttu-id="19464-165">![Настройка единого входа](./media/active-directory-saas-cisco-webex-tutorial/IC777624.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="19464-165">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777624.png "Configure single sign-on")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="19464-166">Настроить подготовку учетных записей пользователей</span><span class="sxs-lookup"><span data-stu-id="19464-166">Configure user provisioning</span></span>

<span data-ttu-id="19464-167">В порядке tooenable toolog пользователей Azure AD в Cisco Webex их необходимо подготовить в Cisco Webex.</span><span class="sxs-lookup"><span data-stu-id="19464-167">In order tooenable Azure AD users toolog into Cisco Webex, they must be provisioned into Cisco Webex.</span></span>  

* <span data-ttu-id="19464-168">В случае hello Cisco Webex Подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="19464-168">In hello case of Cisco Webex, provisioning is a manual task.</span></span>

<span data-ttu-id="19464-169">**tooprovision учетных записей пользователей, выполните следующие действия hello:**</span><span class="sxs-lookup"><span data-stu-id="19464-169">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="19464-170">Войдите в tooyour **Cisco Webex** клиента.</span><span class="sxs-lookup"><span data-stu-id="19464-170">Log in tooyour **Cisco Webex** tenant.</span></span>
2. <span data-ttu-id="19464-171">Go слишком**Управление пользователями \> добавить пользователя**.</span><span class="sxs-lookup"><span data-stu-id="19464-171">Go too**Manage Users \> Add User**.</span></span>
   
   <span data-ttu-id="19464-172">![Добавление пользователей](./media/active-directory-saas-cisco-webex-tutorial/IC777625.png "Добавление пользователей")</span><span class="sxs-lookup"><span data-stu-id="19464-172">![Add users](./media/active-directory-saas-cisco-webex-tutorial/IC777625.png "Add users")</span></span>
3. <span data-ttu-id="19464-173">На hello раздел добавить пользователя выполните hello следующие шаги.</span><span class="sxs-lookup"><span data-stu-id="19464-173">On hello Add User section, perform hello following steps:</span></span>
   
   <span data-ttu-id="19464-174">![Добавление пользователя](./media/active-directory-saas-cisco-webex-tutorial/IC777626.png "Добавление пользователя")</span><span class="sxs-lookup"><span data-stu-id="19464-174">![Add user](./media/active-directory-saas-cisco-webex-tutorial/IC777626.png "Add user")</span></span>   
   1. <span data-ttu-id="19464-175">Для параметра **Тип учетной записи** выберите значение **Узел**.</span><span class="sxs-lookup"><span data-stu-id="19464-175">As **Account Type**, select **Host**.</span></span>
   2. <span data-ttu-id="19464-176">Введите сведения hello существующего пользователя Azure AD в следующие текстовые поля hello: **имя и фамилию пользователя**, **имя пользователя**, **электронной почты**, **пароля**, **Подтверждение пароля**.</span><span class="sxs-lookup"><span data-stu-id="19464-176">Type hello information of an existing Azure AD user into hello following textboxes: **First name, Last name**, **User name**, **Email**, **Password**, **Confirm Password**.</span></span>
   3. <span data-ttu-id="19464-177">Щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="19464-177">Click **Add**.</span></span>

>[!NOTE]
><span data-ttu-id="19464-178">Можно использовать любые другие Cisco Webex пользователя средства создания учетных записей или интерфейсы API, предоставляемые Cisco Webex tooprovision учетных записей пользователей AAD.</span><span class="sxs-lookup"><span data-stu-id="19464-178">You can use any other Cisco Webex user account creation tools or APIs provided by Cisco Webex tooprovision AAD user accounts.</span></span> 
> 

## <a name="assign-users"></a><span data-ttu-id="19464-179">Назначить пользователей</span><span class="sxs-lookup"><span data-stu-id="19464-179">Assign users</span></span>
<span data-ttu-id="19464-180">tootest конфигурацию, необходимо toogrant hello Azure AD пользователей с помощью tooit доступ вашего приложения путем назначения им tooallow.</span><span class="sxs-lookup"><span data-stu-id="19464-180">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="19464-181">**Пользователи tooassign tooCisco Webex, выполните hello следующие шаги.**</span><span class="sxs-lookup"><span data-stu-id="19464-181">**tooassign users tooCisco Webex, perform hello following steps:**</span></span>

1. <span data-ttu-id="19464-182">В hello классический портал Azure создайте тестовую учетную запись.</span><span class="sxs-lookup"><span data-stu-id="19464-182">In hello Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="19464-183">На hello **Cisco Webex** странице интеграции приложения щелкните **назначить пользователей**.</span><span class="sxs-lookup"><span data-stu-id="19464-183">On hello **Cisco Webex** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="19464-184">![Назначение пользователей](./media/active-directory-saas-cisco-webex-tutorial/IC777627.png "Назначение пользователей")</span><span class="sxs-lookup"><span data-stu-id="19464-184">![Assign users](./media/active-directory-saas-cisco-webex-tutorial/IC777627.png "Assign users")</span></span>
3. <span data-ttu-id="19464-185">Выберите тестового пользователя, нажмите кнопку **назначить**, а затем нажмите кнопку **Да** tooconfirm назначения.</span><span class="sxs-lookup"><span data-stu-id="19464-185">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
   <span data-ttu-id="19464-186">![Да](./media/active-directory-saas-cisco-webex-tutorial/IC767830.png "Да")</span><span class="sxs-lookup"><span data-stu-id="19464-186">![Yes](./media/active-directory-saas-cisco-webex-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="19464-187">Tootest параметры единого входа, откройте панель доступа hello.</span><span class="sxs-lookup"><span data-stu-id="19464-187">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="19464-188">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="19464-188">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

