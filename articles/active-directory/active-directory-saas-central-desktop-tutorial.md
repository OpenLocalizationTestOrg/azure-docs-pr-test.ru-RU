---
title: "Руководство. Интеграция Azure Active Directory с Central Desktop | Документация Майкрософт"
description: "Узнайте, как использовать Central Desktop вместе с Azure Active Directory для реализации единого входа, автоматической подготовки пользователей и выполнения других задач."
services: active-directory
author: jeevansd
documentationcenter: na
manager: femila
ms.assetid: b805d485-93db-49b4-807a-18d446c7090e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/10/2017
ms.author: jeedes
ms.openlocfilehash: fe32c1d68040ceb9d9de2ad6c4a6dc9ea93f5aef
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-central-desktop"></a><span data-ttu-id="ab27d-103">Учебник. Интеграция Azure Active Directory с Central Desktop</span><span class="sxs-lookup"><span data-stu-id="ab27d-103">Tutorial: Azure Active Directory integration with Central Desktop</span></span>
<span data-ttu-id="ab27d-104">Цель данного учебника — показать интеграцию Azure и Central Desktop.</span><span class="sxs-lookup"><span data-stu-id="ab27d-104">The objective of this tutorial is to show the integration of Azure and Central Desktop.</span></span> <span data-ttu-id="ab27d-105">Сценарий, описанный в этом учебнике, предполагает, что у вас уже имеется:</span><span class="sxs-lookup"><span data-stu-id="ab27d-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="ab27d-106">Действующая подписка на Azure</span><span class="sxs-lookup"><span data-stu-id="ab27d-106">A valid Azure subscription</span></span>
* <span data-ttu-id="ab27d-107">Подписка с поддержкой единого входа в Central Desktop/клиент Central Desktop</span><span class="sxs-lookup"><span data-stu-id="ab27d-107">A Central desktop single sign on enabled subscription / Central desktop tenant</span></span>

<span data-ttu-id="ab27d-108">Сценарий, описанный в этом учебнике, состоит из следующих блоков:</span><span class="sxs-lookup"><span data-stu-id="ab27d-108">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

* <span data-ttu-id="ab27d-109">Включение интеграции приложений для Central Desktop</span><span class="sxs-lookup"><span data-stu-id="ab27d-109">Enabling the application integration for Central Desktop</span></span>
* <span data-ttu-id="ab27d-110">Настройка единого входа</span><span class="sxs-lookup"><span data-stu-id="ab27d-110">Configuring single sign-on (SSO)</span></span>
* <span data-ttu-id="ab27d-111">Настройка подготовки учетных записей пользователей</span><span class="sxs-lookup"><span data-stu-id="ab27d-111">Configuring user provisioning</span></span>
* <span data-ttu-id="ab27d-112">Назначение пользователей</span><span class="sxs-lookup"><span data-stu-id="ab27d-112">Assigning users</span></span>

<span data-ttu-id="ab27d-113">![Сценарий](./media/active-directory-saas-central-desktop-tutorial/IC769558.png "Сценарий")</span><span class="sxs-lookup"><span data-stu-id="ab27d-113">![Scenario](./media/active-directory-saas-central-desktop-tutorial/IC769558.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-central-desktop"></a><span data-ttu-id="ab27d-114">Включение интеграции приложений для Central Desktop</span><span class="sxs-lookup"><span data-stu-id="ab27d-114">Enable the application integration for Central Desktop</span></span>
<span data-ttu-id="ab27d-115">В этом разделе показано, как включить интеграцию приложений для Central Desktop.</span><span class="sxs-lookup"><span data-stu-id="ab27d-115">The objective of this section is to outline how to enable the application integration for Central Desktop.</span></span>

<span data-ttu-id="ab27d-116">**Чтобы включить интеграцию приложений для Central Desktop, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="ab27d-116">**To enable the application integration for Central Desktop, perform the following steps:**</span></span>

1. <span data-ttu-id="ab27d-117">На классическом портале Azure в области навигации слева щелкните **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ab27d-117">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="ab27d-118">![Active Directory](./media/active-directory-saas-central-desktop-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="ab27d-118">![Active Directory](./media/active-directory-saas-central-desktop-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="ab27d-119">Из списка **Каталог** выберите каталог, для которого нужно включить интеграцию каталогов.</span><span class="sxs-lookup"><span data-stu-id="ab27d-119">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="ab27d-120">Чтобы открыть представление приложений, в представлении каталога нажмите **Приложения** в верхнем меню.</span><span class="sxs-lookup"><span data-stu-id="ab27d-120">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="ab27d-121">![Приложения](./media/active-directory-saas-central-desktop-tutorial/IC700994.png "Приложения")</span><span class="sxs-lookup"><span data-stu-id="ab27d-121">![Applications](./media/active-directory-saas-central-desktop-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="ab27d-122">В нижней части страницы нажмите кнопку **Добавить** .</span><span class="sxs-lookup"><span data-stu-id="ab27d-122">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="ab27d-123">![Добавление приложения](./media/active-directory-saas-central-desktop-tutorial/IC749321.png "Добавление приложения")</span><span class="sxs-lookup"><span data-stu-id="ab27d-123">![Add application](./media/active-directory-saas-central-desktop-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="ab27d-124">В диалоговом окне **Что необходимо сделать?** щелкните **Добавить приложение из коллекции**.</span><span class="sxs-lookup"><span data-stu-id="ab27d-124">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="ab27d-125">![Добавление приложения из коллекции](./media/active-directory-saas-central-desktop-tutorial/IC749322.png "Добавление приложения из коллекции")</span><span class="sxs-lookup"><span data-stu-id="ab27d-125">![Add an application from gallerry](./media/active-directory-saas-central-desktop-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="ab27d-126">В **поле поиска** введите **Central Desktop**.</span><span class="sxs-lookup"><span data-stu-id="ab27d-126">In the **search box**, type **Central Desktop**.</span></span>
   
   <span data-ttu-id="ab27d-127">![Коллекция приложений](./media/active-directory-saas-central-desktop-tutorial/IC769559.png "Коллекция приложений")</span><span class="sxs-lookup"><span data-stu-id="ab27d-127">![Application gallery](./media/active-directory-saas-central-desktop-tutorial/IC769559.png "Application gallery")</span></span>
7. <span data-ttu-id="ab27d-128">В области результатов выберите **Central Desktop** и нажмите кнопку **Завершить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="ab27d-128">In the results pane, select **Central Desktop**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="ab27d-129">![Central Desktop](./media/active-directory-saas-central-desktop-tutorial/IC769560.png "Central Desktop")</span><span class="sxs-lookup"><span data-stu-id="ab27d-129">![Central Desktop](./media/active-directory-saas-central-desktop-tutorial/IC769560.png "Central Desktop")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="ab27d-130">Настройка единого входа</span><span class="sxs-lookup"><span data-stu-id="ab27d-130">Configure single sign-on</span></span>

<span data-ttu-id="ab27d-131">В этом разделе показано, как разрешить пользователям проходить проверку подлинности в Central Desktop со своей учетной записью Azure AD, используя федерацию на основе протокола SAML.</span><span class="sxs-lookup"><span data-stu-id="ab27d-131">The objective of this section is to outline how to enable users to authenticate to Central Desktop with their account in Azure AD using federation based on the SAML protocol.</span></span>

<span data-ttu-id="ab27d-132">В рамках этой процедуры потребуется передать в клиент Central Desktop сертификат в кодировке Base-64.</span><span class="sxs-lookup"><span data-stu-id="ab27d-132">As part of this procedure, you are required to upload a base-64 encoded certificate to your Central Desktop tenant.</span></span>  
<span data-ttu-id="ab27d-133">Если вы не знакомы с этой процедурой, посмотрите видео [Как преобразовать двоичный сертификат в текстовый файл](http://youtu.be/PlgrzUZ-Y1o).</span><span class="sxs-lookup"><span data-stu-id="ab27d-133">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o).</span></span>

<span data-ttu-id="ab27d-134">**Чтобы настроить единый вход, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="ab27d-134">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="ab27d-135">В классическом портале Azure на **Central Desktop** странице интеграции приложения щелкните **настроить единый вход** Открытие ** Настройка единого входа ** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="ab27d-135">In the Azure classic portal, on the **Central Desktop** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On ** dialog.</span></span>
   
   <span data-ttu-id="ab27d-136">![Настройка единого входа](./media/active-directory-saas-central-desktop-tutorial/IC749323.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="ab27d-136">![Configure single sign-on](./media/active-directory-saas-central-desktop-tutorial/IC749323.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="ab27d-137">На странице **Как пользователи должны входить в Central Desktop?** выберите **Единый вход Microsoft Azure AD** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="ab27d-137">On the **How would you like users to sign on to Central Desktop** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="ab27d-138">![Настройка единого входа](./media/active-directory-saas-central-desktop-tutorial/IC777628.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="ab27d-138">![Configure single sign-on](./media/active-directory-saas-central-desktop-tutorial/IC777628.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="ab27d-139">На странице **Настроить URL-адрес приложения** выполните следующие действия, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="ab27d-139">On the **Configure App URL** page, perform the following steps, and then click **Next**:</span></span> 
   
   1. <span data-ttu-id="ab27d-140">В текстовом поле **URL-адрес входа в Central Desktop** введите URL-адрес своего клиента Central Desktop (например, *http://contoso.centraldesktop.com*).</span><span class="sxs-lookup"><span data-stu-id="ab27d-140">In the **Central Desktop Sign In URL** textbox, type the URL of your Central Desktop tenant (e.g.: *http://contoso.centraldesktop.com*).</span></span>
   2. <span data-ttu-id="ab27d-141">В текстовом поле "URL-адрес ответа Central Desktop" введите URL-адрес службы AssertionConsumerService Central Desktop (например, https://contoso.centraldesktop.com/saml2-assertion.php).</span><span class="sxs-lookup"><span data-stu-id="ab27d-141">In the Central  Desktop Reply URL textbox, type your Central Desktop AssertionConsumerService URL (e.g.:  https://contoso.centraldesktop.com/saml2-assertion.php).</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="ab27d-142">Это значение можно найти в метаданных Central Desktop (например, *http://contoso.centraldesktop.com*).</span><span class="sxs-lookup"><span data-stu-id="ab27d-142">You can get the value from the central desktop metadata (e.g.: *http://contoso.centraldesktop.com*).</span></span>
   >  
   
   <span data-ttu-id="ab27d-143">![Настройка URL-адреса приложения](./media/active-directory-saas-central-desktop-tutorial/IC769561.png "Настройка URL-адреса приложения")</span><span class="sxs-lookup"><span data-stu-id="ab27d-143">![Configure app URL](./media/active-directory-saas-central-desktop-tutorial/IC769561.png "Configure app URL")</span></span>
4. <span data-ttu-id="ab27d-144">На странице **Настройка единого входа в Central Desktop** нажмите кнопку **Скачать сертификат** и сохраните файл сертификата локально на своем компьютере.</span><span class="sxs-lookup"><span data-stu-id="ab27d-144">On the **Configure single sign-on at Central Desktop** page, to download your certificate, click **Download certificate**, and then save the certificate file on your computer.</span></span>
   
  <span data-ttu-id="ab27d-145">![Настройка единого входа](./media/active-directory-saas-central-desktop-tutorial/IC769562.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="ab27d-145">![Configure single sign-on](./media/active-directory-saas-central-desktop-tutorial/IC769562.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="ab27d-146">Выполните вход в клиент **Central Desktop** .</span><span class="sxs-lookup"><span data-stu-id="ab27d-146">Log in to your **Central Desktop** tenant.</span></span>
6. <span data-ttu-id="ab27d-147">Выберите **Параметры**, **Дополнительно** и **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="ab27d-147">Go to **Settings**, click **Advanced**, and then click **Single Sign On**.</span></span>
   
  <span data-ttu-id="ab27d-148">![Настройка — Дополнительно](./media/active-directory-saas-central-desktop-tutorial/IC769563.png "Настройка — Дополнительно")</span><span class="sxs-lookup"><span data-stu-id="ab27d-148">![Setup - Advanced](./media/active-directory-saas-central-desktop-tutorial/IC769563.png "Setup - Advanced")</span></span>
7. <span data-ttu-id="ab27d-149">На странице **Параметры единого входа** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="ab27d-149">On the **Single Sign On Settings** page, perform the following steps:</span></span>
   
  <span data-ttu-id="ab27d-150">![Параметры единого входа](./media/active-directory-saas-central-desktop-tutorial/IC769564.png "Параметры единого входа")</span><span class="sxs-lookup"><span data-stu-id="ab27d-150">![Single Sign On Settings](./media/active-directory-saas-central-desktop-tutorial/IC769564.png "Single Sign On Settings")</span></span>
   
  1. <span data-ttu-id="ab27d-151">Установите флажок **Разрешить единый вход SAML версии 2**.</span><span class="sxs-lookup"><span data-stu-id="ab27d-151">Select **Enable SAML v2 Single Sign On**.</span></span>
  2. <span data-ttu-id="ab27d-152">На странице **Настройка единого входа в Central Desktop** классического портала Azure скопируйте значение поля **URL-адрес издателя** и вставьте его в текстовое поле **SSO URL** (URL-адрес единого входа).</span><span class="sxs-lookup"><span data-stu-id="ab27d-152">In the Azure classic portal, on the **Configure single sign-on at Central Desktop** page, copy the **Issuer URL** value, and then paste it into the **SSO URL** textbox.</span></span>
  3. <span data-ttu-id="ab27d-153">На странице **Настройка единого входа в Central Desktop** классического портала Azure скопируйте значение поля **URL-адрес удаленного входа** и вставьте его в текстовое поле **SSO Login URL** (URL-адрес единого входа).</span><span class="sxs-lookup"><span data-stu-id="ab27d-153">In the Azure classic portal, on the **Configure single sign-on at Central Desktop** page, copy the **Remote Login URL** value, and then paste it into the **SSO Login URL** textbox.</span></span>
  4. <span data-ttu-id="ab27d-154">На странице **Настройка единого входа в Central Desktop** классического портала Azure скопируйте значение поля **URL-адрес службы единого выхода** и вставьте его в текстовое поле **SSO Logout URL** (URL-адрес единого выхода).</span><span class="sxs-lookup"><span data-stu-id="ab27d-154">In the Azure classic portal, on the **Configure single sign-on at Central Desktop** page, copy the **Single Sign-Out Service URL** value, and then paste it into the **SSO Logout URL** textbox.</span></span>
8. <span data-ttu-id="ab27d-155">В разделе **Метод проверки подписей в сообщениях** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="ab27d-155">In the **Message Signature Verification Method** section, perform the following steps:</span></span>
   
   <span data-ttu-id="ab27d-156">![Метод проверки подписей в сообщениях](./media/active-directory-saas-central-desktop-tutorial/IC769565.png "Метод проверки подписей в сообщениях")</span><span class="sxs-lookup"><span data-stu-id="ab27d-156">![Message Signature Verification Method](./media/active-directory-saas-central-desktop-tutorial/IC769565.png "Message Signature Verification Method")</span></span>
   
  1. <span data-ttu-id="ab27d-157">Выберите **Сертификат**.</span><span class="sxs-lookup"><span data-stu-id="ab27d-157">Select **Certificate**.</span></span>
  2. <span data-ttu-id="ab27d-158">В списке **SSO Certificate** (Сертификат единого входа) выберите значение **RSH SHA256**.</span><span class="sxs-lookup"><span data-stu-id="ab27d-158">From the **SSO Certificate** list, select **RSH SHA256**.</span></span>
  3. <span data-ttu-id="ab27d-159">Создайте текстовый файл из загруженного сертификата, скопируйте содержимое текстового файла и вставьте его в поле **Сертификат единого входа** .</span><span class="sxs-lookup"><span data-stu-id="ab27d-159">Create a text file from the downloaded certificate, copy the content of the text file, and then paste it into the **SSO Certificate** field.</span></span>  
     >[!TIP]
     ><span data-ttu-id="ab27d-160">Дополнительные сведения можно узнать из видео [Как преобразовать двоичный сертификат в текстовый файл](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="ab27d-160">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>
      >  
   4. <span data-ttu-id="ab27d-161">Установите флажок **Отображать ссылку на страницу входа SAML версии 2**.</span><span class="sxs-lookup"><span data-stu-id="ab27d-161">Select **Display a link to your SAMLv2 login page**.</span></span>
9. <span data-ttu-id="ab27d-162">Нажмите кнопку **Обновить**.</span><span class="sxs-lookup"><span data-stu-id="ab27d-162">Click **Update**.</span></span>
10. <span data-ttu-id="ab27d-163">На классическом портале Azure выберите подтверждение конфигурации единого входа, а затем нажмите кнопку **Завершить**, чтобы закрыть диалоговое окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="ab27d-163">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
    
    <span data-ttu-id="ab27d-164">![Настройка единого входа](./media/active-directory-saas-central-desktop-tutorial/IC769566.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="ab27d-164">![Configure single sign-on](./media/active-directory-saas-central-desktop-tutorial/IC769566.png "Configure single sign-on")</span></span>
    
## <a name="configure-user-provisioning"></a><span data-ttu-id="ab27d-165">Настроить подготовку учетных записей пользователей</span><span class="sxs-lookup"><span data-stu-id="ab27d-165">Configure user provisioning</span></span>

<span data-ttu-id="ab27d-166">Чтобы пользователи AAD могли входить систему, их необходимо подготовить для Central Desktop.</span><span class="sxs-lookup"><span data-stu-id="ab27d-166">For AAD users to be able to sign in, they must be provisioned to the Central Desktop application.</span></span> <span data-ttu-id="ab27d-167">В этом разделе описывается порядок создания учетных записей пользователей AAD в Central Desktop.</span><span class="sxs-lookup"><span data-stu-id="ab27d-167">This section describes how to create AAD user accounts in Central Desktop.</span></span>

<span data-ttu-id="ab27d-168">**Чтобы подготовить учетные записи пользователей для Central Desktop, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="ab27d-168">**To provision user accounts to Central Desktop:**</span></span>
1. <span data-ttu-id="ab27d-169">Выполните вход в клиент Central Desktop.</span><span class="sxs-lookup"><span data-stu-id="ab27d-169">Log in to your Central Desktop tenant.</span></span>
2. <span data-ttu-id="ab27d-170">Выберите **Пользователи \> Internal Members** (Внутренние участники).</span><span class="sxs-lookup"><span data-stu-id="ab27d-170">Go to **People \> Internal Members**.</span></span>
3. <span data-ttu-id="ab27d-171">Нажмите кнопку **Добавить внутренних участников**.</span><span class="sxs-lookup"><span data-stu-id="ab27d-171">Click **Add Internal Members**.</span></span>
   
  <span data-ttu-id="ab27d-172">![Люди](./media/active-directory-saas-central-desktop-tutorial/IC781051.png "Люди")</span><span class="sxs-lookup"><span data-stu-id="ab27d-172">![People](./media/active-directory-saas-central-desktop-tutorial/IC781051.png "People")</span></span>
4. <span data-ttu-id="ab27d-173">В текстовом поле **Email Address of New Members** (Адреса электронной почты новых участников) введите учетную запись AAD, которую вы хотите подготовить, и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="ab27d-173">In the **Email Address of New Members** textbox, type an AAD account you want to provision, and then click **Next**.</span></span>
   
  <span data-ttu-id="ab27d-174">![Адреса электронной почты новых участников](./media/active-directory-saas-central-desktop-tutorial/IC781052.png "Адреса электронной почты новых участников")</span><span class="sxs-lookup"><span data-stu-id="ab27d-174">![Email Addresses of New Members](./media/active-directory-saas-central-desktop-tutorial/IC781052.png "Email Addresses of New Members")</span></span>
5. <span data-ttu-id="ab27d-175">Нажмите кнопку **Добавить внутренних участников**.</span><span class="sxs-lookup"><span data-stu-id="ab27d-175">Click **Add Internal member(s)**.</span></span>
   
  <span data-ttu-id="ab27d-176">![Добавление внутренних участников](./media/active-directory-saas-central-desktop-tutorial/IC781053.png "Добавление внутренних участников")</span><span class="sxs-lookup"><span data-stu-id="ab27d-176">![Add Internal Member](./media/active-directory-saas-central-desktop-tutorial/IC781053.png "Add Internal Member")</span></span>
   
   >[!NOTE]
   ><span data-ttu-id="ab27d-177">Добавленные пользователи получат сообщение электронной почты со ссылкой для активации учетной записи.</span><span class="sxs-lookup"><span data-stu-id="ab27d-177">The users you have added will receive an email that includes a confirmation link they need to click to activate the account.</span></span>
   > 

>[!NOTE]
><span data-ttu-id="ab27d-178">Вы можете использовать любые другие средства создания учетной записи пользователя Central Desktop или API, предоставляемые Central Desktop для подготовки учетных записей пользователя AAD.</span><span class="sxs-lookup"><span data-stu-id="ab27d-178">You can use any other Central Desktop user account creation tools or APIs provided by Central Desktop to provision AAD user accounts</span></span>
>  

## <a name="assign-users"></a><span data-ttu-id="ab27d-179">Назначить пользователей</span><span class="sxs-lookup"><span data-stu-id="ab27d-179">Assign users</span></span>
<span data-ttu-id="ab27d-180">Чтобы проверить свою конфигурацию, предоставьте пользователям Azure AD, которые должны использовать приложение, доступ путем их назначения.</span><span class="sxs-lookup"><span data-stu-id="ab27d-180">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="ab27d-181">**Чтобы назначить пользователей Central Desktop, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="ab27d-181">**To assign users to Central Desktop, perform the following steps:**</span></span>

1. <span data-ttu-id="ab27d-182">На классическом портале Azure создайте тестовую учетную запись.</span><span class="sxs-lookup"><span data-stu-id="ab27d-182">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="ab27d-183">На странице интеграции с приложением **Central Desktop** нажмите **Назначить пользователей**.</span><span class="sxs-lookup"><span data-stu-id="ab27d-183">On the **Central Desktop** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="ab27d-184">![Назначение пользователей](./media/active-directory-saas-central-desktop-tutorial/IC769567.png "Назначение пользователей")</span><span class="sxs-lookup"><span data-stu-id="ab27d-184">![Assign users](./media/active-directory-saas-central-desktop-tutorial/IC769567.png "Assign users")</span></span>
3. <span data-ttu-id="ab27d-185">Выберите тестового пользователя, нажмите кнопку **Назначить**, а затем — **Да**, чтобы подтвердить назначение.</span><span class="sxs-lookup"><span data-stu-id="ab27d-185">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="ab27d-186">![Да](./media/active-directory-saas-central-desktop-tutorial/IC767830.png "Да")</span><span class="sxs-lookup"><span data-stu-id="ab27d-186">![Yes](./media/active-directory-saas-central-desktop-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="ab27d-187">Если вы хотите проверить параметры единого входа, откройте панель доступа.</span><span class="sxs-lookup"><span data-stu-id="ab27d-187">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="ab27d-188">Дополнительные сведения о панели доступа можно найти в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ab27d-188">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

