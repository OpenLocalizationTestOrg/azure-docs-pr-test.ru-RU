---
title: "Руководство по интеграции Azure Active Directory с Replicon | Документация Майкрософт"
description: "Узнайте, как toouse Replicon с Azure Active Directory tooenable единого входа, автоматизированной подготовки и многое другое!"
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: 02a62f15-917c-417c-8d80-fe685e3fd601
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/23/2017
ms.author: jeedes
ms.openlocfilehash: 4949eaf959265cfa4f732a2b73317fffe6312a17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-replicon"></a><span data-ttu-id="8d8ad-103">Учебник. Интеграция Azure Active Directory с Replicon</span><span class="sxs-lookup"><span data-stu-id="8d8ad-103">Tutorial: Azure Active Directory integration with Replicon</span></span>
<span data-ttu-id="8d8ad-104">Цель этого учебника Hello — tooshow hello интеграцию Azure и Replicon.</span><span class="sxs-lookup"><span data-stu-id="8d8ad-104">hello objective of this tutorial is tooshow hello integration of Azure and Replicon.</span></span> <span data-ttu-id="8d8ad-105">Hello сценарий, описанный в этом руководстве предполагается, что уже hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="8d8ad-105">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

* <span data-ttu-id="8d8ad-106">Действующая подписка на Azure</span><span class="sxs-lookup"><span data-stu-id="8d8ad-106">A valid Azure subscription</span></span>
* <span data-ttu-id="8d8ad-107">Клиент Replicon.</span><span class="sxs-lookup"><span data-stu-id="8d8ad-107">A Replicon tenant</span></span>

<span data-ttu-id="8d8ad-108">После завершения этого учебника, пользователи hello Azure AD, назначенные tooReplicon будет может toosingle вход в приложение hello на свой корпоративный сайт Replicon (инициированный поставщиком вход службы) или с помощью hello [toohello введение доступа Панель](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8d8ad-108">After completing this tutorial, hello Azure AD users you have assigned tooReplicon will be able toosingle sign into hello application at your Replicon company site (service provider initiated sign on), or using hello [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="8d8ad-109">Hello сценарий, описанный в этом руководстве состоит из hello следующие стандартные блоки.</span><span class="sxs-lookup"><span data-stu-id="8d8ad-109">hello scenario outlined in this tutorial consists of hello following building blocks:</span></span>

1. <span data-ttu-id="8d8ad-110">Включение hello интеграции приложений для Replicon</span><span class="sxs-lookup"><span data-stu-id="8d8ad-110">Enabling hello application integration for Replicon</span></span>
2. <span data-ttu-id="8d8ad-111">Настройка единого входа.</span><span class="sxs-lookup"><span data-stu-id="8d8ad-111">Configuring single sign-on (SSO)</span></span>
3. <span data-ttu-id="8d8ad-112">Настройка подготовки учетных записей пользователей</span><span class="sxs-lookup"><span data-stu-id="8d8ad-112">Configuring user provisioning</span></span>
4. <span data-ttu-id="8d8ad-113">Назначение пользователей</span><span class="sxs-lookup"><span data-stu-id="8d8ad-113">Assigning users</span></span>

<span data-ttu-id="8d8ad-114">![Сценарий](./media/active-directory-saas-replicon-tutorial/IC777798.png "Сценарий")</span><span class="sxs-lookup"><span data-stu-id="8d8ad-114">![Scenario](./media/active-directory-saas-replicon-tutorial/IC777798.png "Scenario")</span></span>

## <a name="enable-hello-application-integration-for-replicon"></a><span data-ttu-id="8d8ad-115">Включить hello интеграции приложений для Replicon</span><span class="sxs-lookup"><span data-stu-id="8d8ad-115">Enable hello application integration for Replicon</span></span>
<span data-ttu-id="8d8ad-116">Hello цель этого раздела — toooutline как интеграция приложения hello tooenable для Replicon.</span><span class="sxs-lookup"><span data-stu-id="8d8ad-116">hello objective of this section is toooutline how tooenable hello application integration for Replicon.</span></span>

<span data-ttu-id="8d8ad-117">**интеграции приложения hello tooenable для Replicon, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="8d8ad-117">**tooenable hello application integration for Replicon, perform hello following steps:**</span></span>

1. <span data-ttu-id="8d8ad-118">В hello классический портал Azure, hello левой области навигации, выберите **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8d8ad-118">In hello Azure classic portal, on hello left navigation pane, click **Active Directory**.</span></span>
   
    <span data-ttu-id="8d8ad-119">![Active Directory](./media/active-directory-saas-replicon-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="8d8ad-119">![Active Directory](./media/active-directory-saas-replicon-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="8d8ad-120">Из hello **каталога** список, выберите hello каталога, для которого требуется Интеграция каталогов tooenable.</span><span class="sxs-lookup"><span data-stu-id="8d8ad-120">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
3. <span data-ttu-id="8d8ad-121">Щелкните представление приложения hello tooopen в представлении каталога hello **приложений** в верхнем меню hello.</span><span class="sxs-lookup"><span data-stu-id="8d8ad-121">tooopen hello applications view, in hello directory view, click **Applications** in hello top menu.</span></span>
   
    <span data-ttu-id="8d8ad-122">![Приложения](./media/active-directory-saas-replicon-tutorial/IC700994.png "Приложения")</span><span class="sxs-lookup"><span data-stu-id="8d8ad-122">![Applications](./media/active-directory-saas-replicon-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="8d8ad-123">Нажмите кнопку **добавить** hello нижней части страницы приветствия.</span><span class="sxs-lookup"><span data-stu-id="8d8ad-123">Click **Add** at hello bottom of hello page.</span></span>
   
    <span data-ttu-id="8d8ad-124">![Добавление приложения](./media/active-directory-saas-replicon-tutorial/IC749321.png "Добавление приложения")</span><span class="sxs-lookup"><span data-stu-id="8d8ad-124">![Add application](./media/active-directory-saas-replicon-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="8d8ad-125">На hello **что вам требуется toodo** диалоговое окно, нажмите кнопку **добавить приложение из коллекции hello**.</span><span class="sxs-lookup"><span data-stu-id="8d8ad-125">On hello **What do you want toodo** dialog, click **Add an application from hello gallery**.</span></span>
   
    <span data-ttu-id="8d8ad-126">![Добавление приложения из коллекции](./media/active-directory-saas-replicon-tutorial/IC749322.png "Добавление приложения из коллекции")</span><span class="sxs-lookup"><span data-stu-id="8d8ad-126">![Add an application from gallerry](./media/active-directory-saas-replicon-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="8d8ad-127">В hello **поле поиска**, тип **Replicon**.</span><span class="sxs-lookup"><span data-stu-id="8d8ad-127">In hello **search box**, type **Replicon**.</span></span>
   
    <span data-ttu-id="8d8ad-128">![Коллекция приложений](./media/active-directory-saas-replicon-tutorial/IC777799.png "Коллекция приложений")</span><span class="sxs-lookup"><span data-stu-id="8d8ad-128">![Application gallery](./media/active-directory-saas-replicon-tutorial/IC777799.png "Application gallery")</span></span>
7. <span data-ttu-id="8d8ad-129">В области результатов hello выберите **Replicon**и нажмите кнопку **завершить** tooadd приложения hello.</span><span class="sxs-lookup"><span data-stu-id="8d8ad-129">In hello results pane, select **Replicon**, and then click **Complete** tooadd hello application.</span></span>
   
    <span data-ttu-id="8d8ad-130">![Replicon](./media/active-directory-saas-replicon-tutorial/IC777800.png "Replicon")</span><span class="sxs-lookup"><span data-stu-id="8d8ad-130">![Replicon](./media/active-directory-saas-replicon-tutorial/IC777800.png "Replicon")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="8d8ad-131">Настройка единого входа</span><span class="sxs-lookup"><span data-stu-id="8d8ad-131">Configure single sign-on</span></span>

<span data-ttu-id="8d8ad-132">Цель этого раздела Hello — toooutline как tooReplicon tooauthenticate tooenable пользователей с учетной записью в Azure AD, используя федерацию на основе hello SAML протокола.</span><span class="sxs-lookup"><span data-stu-id="8d8ad-132">hello objective of this section is toooutline how tooenable users tooauthenticate tooReplicon with their account in Azure AD using federation based on hello SAML protocol.</span></span>

<span data-ttu-id="8d8ad-133">**tooconfigure единого входа, выполните следующие шаги hello:**</span><span class="sxs-lookup"><span data-stu-id="8d8ad-133">**tooconfigure single sign-on, perform hello following steps:**</span></span>

1. <span data-ttu-id="8d8ad-134">В классический портал Azure, на hello hello **Replicon** странице интеграции приложения щелкните **настроить единый вход** tooopen hello **Настройка единого входа** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="8d8ad-134">In hello Azure classic portal, on hello **Replicon** application integration page, click **Configure single sign-on** tooopen hello **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="8d8ad-135">![Настройка единого входа](./media/active-directory-saas-replicon-tutorial/IC777801.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="8d8ad-135">![Configure single sign-on](./media/active-directory-saas-replicon-tutorial/IC777801.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="8d8ad-136">На hello **предпочитаемый как toosign пользователей на tooReplicon** выберите **Microsoft Azure AD Single Sign-On**, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="8d8ad-136">On hello **How would you like users toosign on tooReplicon** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
    <span data-ttu-id="8d8ad-137">![Настройка единого входа](./media/active-directory-saas-replicon-tutorial/IC777802.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="8d8ad-137">![Configure single sign-on](./media/active-directory-saas-replicon-tutorial/IC777802.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="8d8ad-138">На hello **настроить URL-адрес приложения** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="8d8ad-138">On hello **Configure App URL** page, perform hello following steps:</span></span>
   
    <span data-ttu-id="8d8ad-139">![Настройка URL-адреса приложения](./media/active-directory-saas-replicon-tutorial/IC777803.png "Настройка URL-адреса приложения")</span><span class="sxs-lookup"><span data-stu-id="8d8ad-139">![Configure app URL](./media/active-directory-saas-replicon-tutorial/IC777803.png "Configure app URL")</span></span>
  1. <span data-ttu-id="8d8ad-140">В hello **Replicon на URL-адрес входа** текстовом поле введите URL-адрес клиента Replicon (например: *https://na2.replicon.com/company/saml2/sp-sso/post*).</span><span class="sxs-lookup"><span data-stu-id="8d8ad-140">In hello **Replicon Sign On URL** textbox, type your Replicon tenant URL (e.g.: *https://na2.replicon.com/company/saml2/sp-sso/post*).</span></span>
  2. <span data-ttu-id="8d8ad-141">В hello **URL-адрес ответа Replicon** текстовом поле введите ваш Replicon **AssertionConsumerService** URL-адрес (например: *https://global.replicon.com/! / saml2 или компании или единого входа и после*).</span><span class="sxs-lookup"><span data-stu-id="8d8ad-141">In hello **Replicon Reply URL** textbox, type your Replicon **AssertionConsumerService** URL(e.g.: *https://global.replicon.com/!/saml2/company/sso/post*).</span></span>  
      
     >[!NOTE]
     ><span data-ttu-id="8d8ad-142">Hello URL-адрес можно получить из метаданных Replicon hello по адресу: **https://global.replicon.com/! /saml2/\<YourCompanyKey\>**.</span><span class="sxs-lookup"><span data-stu-id="8d8ad-142">You can get hello URL from hello Replicon metadata at: **https://global.replicon.com/!/saml2/\<YourCompanyKey\>**.</span></span>
     > 
     > 
 
  3. <span data-ttu-id="8d8ad-143">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="8d8ad-143">Click **Next**.</span></span>

4. <span data-ttu-id="8d8ad-144">На hello **настройки единого входа в Replicon** страницы, toodownload метаданные, нажмите кнопку **загрузить метаданные**, а затем сохраните метаданные hello на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="8d8ad-144">On hello **Configure single sign-on at Replicon** page, toodownload your metadata, click **Download metadata**, and then save hello metadata on your computer.</span></span>
   
    <span data-ttu-id="8d8ad-145">![Настройка единого входа](./media/active-directory-saas-replicon-tutorial/IC777804.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="8d8ad-145">![Configure single sign-on](./media/active-directory-saas-replicon-tutorial/IC777804.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="8d8ad-146">В другом окне веб-браузера войдите на сайт Replicon своей компании в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="8d8ad-146">In a different web browser window, log into your Replicon company site as an administrator.</span></span>

6. <span data-ttu-id="8d8ad-147">tooconfigure SAML 2.0, выполните следующие шаги hello.</span><span class="sxs-lookup"><span data-stu-id="8d8ad-147">tooconfigure SAML 2.0, perform hello following steps:</span></span>
   
    <span data-ttu-id="8d8ad-148">![Включение аутентификации SAML](./media/active-directory-saas-replicon-tutorial/IC777805.png "Включение аутентификации SAML")</span><span class="sxs-lookup"><span data-stu-id="8d8ad-148">![Enable SAML authentication](./media/active-directory-saas-replicon-tutorial/IC777805.png "Enable SAML authentication")</span></span>
  
  1. <span data-ttu-id="8d8ad-149">toodisplay hello **EnableSAML Authentication2** диалоговое окно, добавьте следующие tooyour URL-адрес после ключа вашей компании hello: **/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**</span><span class="sxs-lookup"><span data-stu-id="8d8ad-149">toodisplay hello **EnableSAML Authentication2** dialog, append hello following tooyour URL, after your company key: **/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**</span></span>  
    * <span data-ttu-id="8d8ad-150">Hello ниже показан hello схема hello полный URL-адреса:</span><span class="sxs-lookup"><span data-stu-id="8d8ad-150">hello following shows hello schema of hello complete URL:</span></span>  
   <span data-ttu-id="8d8ad-151">**https://na2.replicon.com/\<ключ_вашей_орагнизации\>/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**</span><span class="sxs-lookup"><span data-stu-id="8d8ad-151">**https://na2.replicon.com/\<YourCompanyKey\>/services/SecurityService1.svc/help/test/EnableSAMLAuthentication2**</span></span>
   2. <span data-ttu-id="8d8ad-152">Нажмите кнопку hello  **+**  tooexpand hello **v20Configuration** раздела.</span><span class="sxs-lookup"><span data-stu-id="8d8ad-152">Click hello **+** tooexpand hello **v20Configuration** section.</span></span>
   3. <span data-ttu-id="8d8ad-153">Нажмите кнопку hello  **+**  tooexpand hello **metaDataConfiguration** раздела.</span><span class="sxs-lookup"><span data-stu-id="8d8ad-153">Click hello **+** tooexpand hello **metaDataConfiguration** section.</span></span>
   4. <span data-ttu-id="8d8ad-154">Нажмите кнопку **выбрать файл**, tooselect XML-файл метаданных поставщика удостоверений и нажмите кнопку **отправить**.</span><span class="sxs-lookup"><span data-stu-id="8d8ad-154">Click **Choose File**, tooselect your identity provider metadata XML file, and click **Submit**.</span></span>

7. <span data-ttu-id="8d8ad-155">На hello классический портал Azure, выберите Подтверждение настройки единого входа hello и нажмите кнопку **завершить** tooclose hello **Настройка единого входа** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="8d8ad-155">On hello Azure classic portal, select hello single sign-on configuration confirmation, and then click **Complete** tooclose hello **Configure Single Sign On** dialog.</span></span>
   
    <span data-ttu-id="8d8ad-156">![Настройка единого входа](./media/active-directory-saas-replicon-tutorial/IC778418.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="8d8ad-156">![Configure single sign-on](./media/active-directory-saas-replicon-tutorial/IC778418.png "Configure single sign-on")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="8d8ad-157">Настроить подготовку учетных записей пользователей</span><span class="sxs-lookup"><span data-stu-id="8d8ad-157">Configure user provisioning</span></span>

<span data-ttu-id="8d8ad-158">В порядке tooenable toolog пользователей Azure AD в Replicon их необходимо подготовить в Replicon.</span><span class="sxs-lookup"><span data-stu-id="8d8ad-158">In order tooenable Azure AD users toolog into Replicon, they must be provisioned into Replicon.</span></span>  

<span data-ttu-id="8d8ad-159">В случае Replicon hello Подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="8d8ad-159">In hello case of Replicon, provisioning is a manual task.</span></span>

<span data-ttu-id="8d8ad-160">**tooconfigure подготовки пользователей, выполните следующие шаги hello.**</span><span class="sxs-lookup"><span data-stu-id="8d8ad-160">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="8d8ad-161">В окне веб-браузера войдите на сайт Replicon своей компании в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="8d8ad-161">In a web browser window, log into your Replicon company site as an administrator.</span></span>
2. <span data-ttu-id="8d8ad-162">Go слишком**администрирования \> пользователей**.</span><span class="sxs-lookup"><span data-stu-id="8d8ad-162">Go too**Administration \> Users**.</span></span>
   
    <span data-ttu-id="8d8ad-163">![Пользователи](./media/active-directory-saas-replicon-tutorial/IC777806.png "Пользователи")</span><span class="sxs-lookup"><span data-stu-id="8d8ad-163">![Users](./media/active-directory-saas-replicon-tutorial/IC777806.png "Users")</span></span>
3. <span data-ttu-id="8d8ad-164">Нажмите кнопку **+ Добавить пользователя**.</span><span class="sxs-lookup"><span data-stu-id="8d8ad-164">Click **+Add User**.</span></span>
   
    <span data-ttu-id="8d8ad-165">![Добавление пользователя](./media/active-directory-saas-replicon-tutorial/IC777807.png "Добавление пользователя")</span><span class="sxs-lookup"><span data-stu-id="8d8ad-165">![Add User](./media/active-directory-saas-replicon-tutorial/IC777807.png "Add User")</span></span>
4. <span data-ttu-id="8d8ad-166">В hello **профиля пользователя** выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="8d8ad-166">In hello **User Profile** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="8d8ad-167">![Профиль пользователя](./media/active-directory-saas-replicon-tutorial/IC777808.png "Профиль пользователя")</span><span class="sxs-lookup"><span data-stu-id="8d8ad-167">![User profile](./media/active-directory-saas-replicon-tutorial/IC777808.png "User profile")</span></span>
   
  1. <span data-ttu-id="8d8ad-168">В hello **имя входа** текстового поля, типа hello Azure AD адрес электронной почты пользователя hello Azure AD будет tooprovision.</span><span class="sxs-lookup"><span data-stu-id="8d8ad-168">In hello **Login Name** textbox, type hello Azure AD email address of hello Azure AD user you want tooprovision.</span></span>
  2. <span data-ttu-id="8d8ad-169">Для параметра **Authentication Type** (Тип аутентификации) выберите значение **SSO** (Единый вход).</span><span class="sxs-lookup"><span data-stu-id="8d8ad-169">As **Authentication Type**, select **SSO**.</span></span>
  3. <span data-ttu-id="8d8ad-170">В hello **отдел** текстовом поле введите отдел пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="8d8ad-170">In hello **Department** textbox, type hello user’s department.</span></span>
  4. <span data-ttu-id="8d8ad-171">Для параметра **Employee Type** (Тип сотрудника) выберите значение **Administrator** (Администратор).</span><span class="sxs-lookup"><span data-stu-id="8d8ad-171">As **Employee Type**, select **Administrator**.</span></span>
  5. <span data-ttu-id="8d8ad-172">Нажмите кнопку **Сохранить профиль пользователя**.</span><span class="sxs-lookup"><span data-stu-id="8d8ad-172">Click **Save User Profile**.</span></span>

>[!NOTE]
><span data-ttu-id="8d8ad-173">Можно использовать любые другие Replicon пользователя средства создания учетных записей или интерфейсы API, предоставляемые Replicon tooprovision учетных записей пользователей AAD.</span><span class="sxs-lookup"><span data-stu-id="8d8ad-173">You can use any other Replicon user account creation tools or APIs provided by Replicon tooprovision AAD user accounts.</span></span>
> 
> 

## <a name="assign-users"></a><span data-ttu-id="8d8ad-174">Назначить пользователей</span><span class="sxs-lookup"><span data-stu-id="8d8ad-174">Assign users</span></span>
<span data-ttu-id="8d8ad-175">tootest конфигурацию, необходимо toogrant hello Azure AD пользователей с помощью tooit доступ вашего приложения путем назначения им tooallow.</span><span class="sxs-lookup"><span data-stu-id="8d8ad-175">tootest your configuration, you need toogrant hello Azure AD users you want tooallow using your application access tooit by assigning them.</span></span>

<span data-ttu-id="8d8ad-176">**tooReplicon tooassign пользователей, выполните следующие шаги hello:**</span><span class="sxs-lookup"><span data-stu-id="8d8ad-176">**tooassign users tooReplicon, perform hello following steps:**</span></span>

1. <span data-ttu-id="8d8ad-177">В hello классический портал Azure создайте тестовую учетную запись.</span><span class="sxs-lookup"><span data-stu-id="8d8ad-177">In hello Azure classic portal, create a test account.</span></span>

2. <span data-ttu-id="8d8ad-178">На hello **Replicon** странице интеграции приложения щелкните **назначить пользователей**.</span><span class="sxs-lookup"><span data-stu-id="8d8ad-178">On hello **Replicon** application integration page, click **Assign users**.</span></span>
   
    <span data-ttu-id="8d8ad-179">![Назначение пользователей](./media/active-directory-saas-replicon-tutorial/IC777809.png "Назначение пользователей")</span><span class="sxs-lookup"><span data-stu-id="8d8ad-179">![Assign users](./media/active-directory-saas-replicon-tutorial/IC777809.png "Assign users")</span></span>

3. <span data-ttu-id="8d8ad-180">Выберите тестового пользователя, нажмите кнопку **назначить**, а затем нажмите кнопку **Да** tooconfirm назначения.</span><span class="sxs-lookup"><span data-stu-id="8d8ad-180">Select your test user, click **Assign**, and then click **Yes** tooconfirm your assignment.</span></span>
   
    <span data-ttu-id="8d8ad-181">![Да](./media/active-directory-saas-replicon-tutorial/IC767830.png "Да")</span><span class="sxs-lookup"><span data-stu-id="8d8ad-181">![Yes](./media/active-directory-saas-replicon-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="8d8ad-182">Tootest параметры единого входа, откройте панель доступа hello.</span><span class="sxs-lookup"><span data-stu-id="8d8ad-182">If you want tootest your single sign-on settings, open hello Access Panel.</span></span> <span data-ttu-id="8d8ad-183">Дополнительные сведения о панели доступа hello см. в разделе [toohello введение панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8d8ad-183">For more details about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

