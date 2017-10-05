---
title: "Учебник. Интеграция Azure Active Directory с Coupa | Документация Майкрософт"
description: "Узнайте, как использовать Coupa вместе с Azure Active Directory для реализации единого входа, автоматической подготовки пользователей и выполнения других задач."
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
ms.openlocfilehash: c952975919cfd948f1b9ea93ff2ac2641a53f923
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-coupa"></a><span data-ttu-id="2480c-103">Руководство. Интеграция Azure Active Directory с Coupa</span><span class="sxs-lookup"><span data-stu-id="2480c-103">Tutorial: Azure Active Directory integration with Coupa</span></span>
<span data-ttu-id="2480c-104">Цель данного руководства — показать интеграцию Azure и Coupa.</span><span class="sxs-lookup"><span data-stu-id="2480c-104">The objective of this tutorial is to show the integration of Azure and Coupa.</span></span>  
<span data-ttu-id="2480c-105">Сценарий, описанный в этом учебнике, предполагает, что у вас уже имеется:</span><span class="sxs-lookup"><span data-stu-id="2480c-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="2480c-106">действующая подписка Azure;</span><span class="sxs-lookup"><span data-stu-id="2480c-106">A valid Azure subscription</span></span>
* <span data-ttu-id="2480c-107">Подписка Coupa с поддержкой единого входа</span><span class="sxs-lookup"><span data-stu-id="2480c-107">A Coupa single sign-on (SSO) enabled subscription</span></span>

<span data-ttu-id="2480c-108">После завершения этого руководства пользователи Azure AD, назначенные Coupa, будут иметь возможность единого входа в приложение с помощью инструкций из статьи [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2480c-108">After completing this tutorial, the Azure AD users you have assigned to Coupa will be able to single sign into the application using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="2480c-109">Сценарий, описанный в этом учебнике, состоит из следующих блоков:</span><span class="sxs-lookup"><span data-stu-id="2480c-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

* <span data-ttu-id="2480c-110">Включение интеграции приложений для Coupa</span><span class="sxs-lookup"><span data-stu-id="2480c-110">Enabling the application integration for Coupa</span></span>
* <span data-ttu-id="2480c-111">Настройка единого входа</span><span class="sxs-lookup"><span data-stu-id="2480c-111">Configuring single sign-on</span></span>
* <span data-ttu-id="2480c-112">Настройка подготовки учетных записей пользователей</span><span class="sxs-lookup"><span data-stu-id="2480c-112">Configuring user provisioning</span></span>
* <span data-ttu-id="2480c-113">Назначение пользователей</span><span class="sxs-lookup"><span data-stu-id="2480c-113">Assigning users</span></span>

<span data-ttu-id="2480c-114">![Сценарий](./media/active-directory-saas-coupa-tutorial/IC791897.png "Сценарий")</span><span class="sxs-lookup"><span data-stu-id="2480c-114">![Scenario](./media/active-directory-saas-coupa-tutorial/IC791897.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-coupa"></a><span data-ttu-id="2480c-115">Включение интеграции приложений для Coupa</span><span class="sxs-lookup"><span data-stu-id="2480c-115">Enable the application integration for Coupa</span></span>
<span data-ttu-id="2480c-116">В этом разделе показано, как включить интеграцию приложений для Coupa.</span><span class="sxs-lookup"><span data-stu-id="2480c-116">The objective of this section is to outline how to enable the application integration for Coupa.</span></span>

<span data-ttu-id="2480c-117">**Чтобы включить интеграцию приложений для Coupa, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="2480c-117">**To enable the application integration for Coupa, perform the following steps:**</span></span>

1. <span data-ttu-id="2480c-118">На классическом портале Azure в области навигации слева щелкните **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="2480c-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="2480c-119">![Active Directory](./media/active-directory-saas-coupa-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="2480c-119">![Active Directory](./media/active-directory-saas-coupa-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="2480c-120">Из списка **Каталог** выберите каталог, для которого нужно включить интеграцию каталогов.</span><span class="sxs-lookup"><span data-stu-id="2480c-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="2480c-121">Чтобы открыть представление приложений, в представлении каталога нажмите **Приложения** в верхнем меню.</span><span class="sxs-lookup"><span data-stu-id="2480c-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="2480c-122">![Приложения](./media/active-directory-saas-coupa-tutorial/IC700994.png "Приложения")</span><span class="sxs-lookup"><span data-stu-id="2480c-122">![Applications](./media/active-directory-saas-coupa-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="2480c-123">В нижней части страницы нажмите кнопку **Добавить** .</span><span class="sxs-lookup"><span data-stu-id="2480c-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="2480c-124">![Добавление приложения](./media/active-directory-saas-coupa-tutorial/IC749321.png "Добавление приложения")</span><span class="sxs-lookup"><span data-stu-id="2480c-124">![Add application](./media/active-directory-saas-coupa-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="2480c-125">В диалоговом окне **Что необходимо сделать?** щелкните **Добавить приложение из коллекции**.</span><span class="sxs-lookup"><span data-stu-id="2480c-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="2480c-126">![Добавление приложения из коллекции](./media/active-directory-saas-coupa-tutorial/IC749322.png "Добавление приложения из коллекции")</span><span class="sxs-lookup"><span data-stu-id="2480c-126">![Add an application from gallerry](./media/active-directory-saas-coupa-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="2480c-127">В **поле поиска** введите **Coupa**.</span><span class="sxs-lookup"><span data-stu-id="2480c-127">In the **search box**, type **Coupa**.</span></span>
   
   <span data-ttu-id="2480c-128">![Коллекция приложений](./media/active-directory-saas-coupa-tutorial/IC791898.png "Коллекция приложений")</span><span class="sxs-lookup"><span data-stu-id="2480c-128">![Application Gallery](./media/active-directory-saas-coupa-tutorial/IC791898.png "Application Gallery")</span></span>
7. <span data-ttu-id="2480c-129">В области результатов выберите **Coupa** и нажмите кнопку **Завершить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="2480c-129">In the results pane, select **Coupa**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="2480c-130">![Coupa](./media/active-directory-saas-coupa-tutorial/IC791899.png "Coupa")</span><span class="sxs-lookup"><span data-stu-id="2480c-130">![Coupa](./media/active-directory-saas-coupa-tutorial/IC791899.png "Coupa")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="2480c-131">Настройка единого входа</span><span class="sxs-lookup"><span data-stu-id="2480c-131">Configure single sign-on</span></span>

<span data-ttu-id="2480c-132">В этом разделе показано, как разрешить пользователям проходить проверку подлинности в Coupa со своей учетной записью Azure AD, используя федерацию на основе протокола SAML.</span><span class="sxs-lookup"><span data-stu-id="2480c-132">The objective of this section is to outline how to enable users to authenticate to Coupa with their account in Azure AD using federation based on the SAML protocol.</span></span>  

<span data-ttu-id="2480c-133">Чтобы настроить единый вход для Coupa, необходимо извлечь значение отпечатка из сертификата.</span><span class="sxs-lookup"><span data-stu-id="2480c-133">Configuring single sign-on for Coupa requires you to retrieve a thumbprint value from a certificate.</span></span> <span data-ttu-id="2480c-134">Если вы не знакомы с этой процедурой, просмотрите видео [Как извлечь значение отпечатка из сертификата](http://youtu.be/YKQF266SAxI).</span><span class="sxs-lookup"><span data-stu-id="2480c-134">If you are not familiar with this procedure, see [How to retrieve a certificate's thumbprint value](http://youtu.be/YKQF266SAxI).</span></span>

<span data-ttu-id="2480c-135">**Чтобы настроить единый вход, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="2480c-135">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="2480c-136">Выполните вход на веб-сайт компании Coupa в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="2480c-136">Sign on to your Coupa company site as an administrator.</span></span>
2. <span data-ttu-id="2480c-137">Последовательно выберите **Setup \> Security Control** (Настройка > Управление безопасностью).</span><span class="sxs-lookup"><span data-stu-id="2480c-137">Go to **Setup \> Security Control**.</span></span>
   
   <span data-ttu-id="2480c-138">![Средства управления безопасностью](./media/active-directory-saas-coupa-tutorial/IC791900.png "Средства управления безопасностью")</span><span class="sxs-lookup"><span data-stu-id="2480c-138">![Security Controls](./media/active-directory-saas-coupa-tutorial/IC791900.png "Security Controls")</span></span>
3. <span data-ttu-id="2480c-139">Чтобы скачать файл метаданных Coupa на свой компьютер, нажмите **Скачать и импортировать метаданные поставщика услуг**.</span><span class="sxs-lookup"><span data-stu-id="2480c-139">To download the Coupa metadata file to your computer, click **Download and import SP metadata**.</span></span>
   
   <span data-ttu-id="2480c-140">![Метаданные Coupa SP](./media/active-directory-saas-coupa-tutorial/IC791901.png "Метаданные Coupa SP")</span><span class="sxs-lookup"><span data-stu-id="2480c-140">![Coupa SP metadata](./media/active-directory-saas-coupa-tutorial/IC791901.png "Coupa SP metadata")</span></span>
4. <span data-ttu-id="2480c-141">В другом окне браузера войдите на классический портал Azure.</span><span class="sxs-lookup"><span data-stu-id="2480c-141">In a different browser window, sign on to the Azure classic portal.</span></span>
5. <span data-ttu-id="2480c-142">На странице интеграции с приложением **Coupa** щелкните **Настройка единого входа**, чтобы открыть диалоговое окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="2480c-142">On the **Coupa** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="2480c-143">![Настройка единого входа](./media/active-directory-saas-coupa-tutorial/IC791902.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="2480c-143">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791902.png "Configure Single Sign-On")</span></span>
6. <span data-ttu-id="2480c-144">На странице **Как пользователи должны входить в Coupa?** выберите **Единый вход Microsoft Azure AD** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="2480c-144">On the **How would you like users to sign on to Coupa** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="2480c-145">![Настройка единого входа](./media/active-directory-saas-coupa-tutorial/IC791903.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="2480c-145">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791903.png "Configure Single Sign-On")</span></span>
7. <span data-ttu-id="2480c-146">На странице **Настройка URL-адреса приложения** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="2480c-146">On the **Configure App URL** page, perform the following steps:</span></span>
   
   <span data-ttu-id="2480c-147">![Настройка URL-адреса приложения](./media/active-directory-saas-coupa-tutorial/IC791904.png "Настройка URL-адреса приложения")</span><span class="sxs-lookup"><span data-stu-id="2480c-147">![Configure App URL](./media/active-directory-saas-coupa-tutorial/IC791904.png "Configure App URL")</span></span>   
   1. <span data-ttu-id="2480c-148">В текстовом поле **URL-адрес для входа** введите URL-адрес, используемый для входа в приложение Coupa (например, *http://компания.Coupa.com*).</span><span class="sxs-lookup"><span data-stu-id="2480c-148">In the **Sign On URL** textbox, type URL used by your users to sign on to your Coupa application (e.g.: “*http://company.Coupa.com*”).</span></span>
   2. <span data-ttu-id="2480c-149">Откройте скачанный файл метаданных Coupa и скопируйте **AssertionConsumerService index/URL**.</span><span class="sxs-lookup"><span data-stu-id="2480c-149">Open your downloaded Coupa metadata file, and then copy the **AssertionConsumerService index/URL**.</span></span>
   3. <span data-ttu-id="2480c-150">Вставьте значение **AssertionConsumerService index/URL** в текстовое поле **URL-адрес ответа Coupa**.</span><span class="sxs-lookup"><span data-stu-id="2480c-150">In the **Coupa Reply URL** textbox, paste the **AssertionConsumerService index/URL** value.</span></span>
   4. <span data-ttu-id="2480c-151">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="2480c-151">Click **Next**.</span></span>
8. <span data-ttu-id="2480c-152">На странице **Настройка единого входа в Coupa** нажмите кнопку **Скачать метаданные**, чтобы скачать файл метаданных, а затем сохраните его на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="2480c-152">On the **Configure single sign-on at Coupa** page, to download your metadata file, click **Download metadata**, and then save the file locally on your computer.</span></span>
   
   <span data-ttu-id="2480c-153">![Настройка единого входа](./media/active-directory-saas-coupa-tutorial/IC791905.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="2480c-153">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791905.png "Configure Single Sign-On")</span></span>
9. <span data-ttu-id="2480c-154">На корпоративном сайте Coupa выберите **Setup \> Security Control** (Настройка > Управление безопасностью).</span><span class="sxs-lookup"><span data-stu-id="2480c-154">On the Coupa company site, go to **Setup \> Security Control**.</span></span>
   
   <span data-ttu-id="2480c-155">![Средства управления безопасностью](./media/active-directory-saas-coupa-tutorial/IC791900.png "Средства управления безопасностью")</span><span class="sxs-lookup"><span data-stu-id="2480c-155">![Security Controls](./media/active-directory-saas-coupa-tutorial/IC791900.png "Security Controls")</span></span>
10. <span data-ttu-id="2480c-156">В разделе **Вход с использованием учетных данных Coupa** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="2480c-156">In the **Log in using Coupa credentials** section, perform the following steps:</span></span>  

   <span data-ttu-id="2480c-157">![Вход с использованием учетных данных Coupa](./media/active-directory-saas-coupa-tutorial/IC791906.png "Вход с использованием учетных данных Coupa")</span><span class="sxs-lookup"><span data-stu-id="2480c-157">![Log in using Coupa credentials](./media/active-directory-saas-coupa-tutorial/IC791906.png "Log in using Coupa credentials")</span></span> 
   1. <span data-ttu-id="2480c-158">Выберите **Вход с помощью SAML**.</span><span class="sxs-lookup"><span data-stu-id="2480c-158">Select **Log in using SAML**.</span></span>
   2. <span data-ttu-id="2480c-159">Чтобы отправить загруженный файл метаданных Azure Active, нажмите кнопку **Обзор** .</span><span class="sxs-lookup"><span data-stu-id="2480c-159">Click **Browse** to upload your downloaded Azure Active metadata file.</span></span>
   3. <span data-ttu-id="2480c-160">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="2480c-160">Click **Save**.</span></span>
11. <span data-ttu-id="2480c-161">На классическом портале Azure выберите подтверждение конфигурации единого входа, а затем нажмите кнопку **Завершить**, чтобы закрыть диалоговое окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="2480c-161">On the Azure classic portal, select the single sign-on configuration confirmation, and then click **Complete** to close the **Configure Single Sign On** dialog.</span></span>
    
   <span data-ttu-id="2480c-162">![Настройка единого входа](./media/active-directory-saas-coupa-tutorial/IC791907.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="2480c-162">![Configure Single Sign-On](./media/active-directory-saas-coupa-tutorial/IC791907.png "Configure Single Sign-On")</span></span>
    
## <a name="configure-user-provisioning"></a><span data-ttu-id="2480c-163">Настроить подготовку учетных записей пользователей</span><span class="sxs-lookup"><span data-stu-id="2480c-163">Configure user provisioning</span></span>

<span data-ttu-id="2480c-164">Чтобы пользователи Azure AD могли выполнять вход в Coupa, они должны быть подготовлены для Coupa.</span><span class="sxs-lookup"><span data-stu-id="2480c-164">In order to enable Azure AD users to log into Coupa, they must be provisioned into Coupa.</span></span>  

* <span data-ttu-id="2480c-165">В случае с Coupa подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="2480c-165">In the case of Coupa, provisioning is a manual task.</span></span>

<span data-ttu-id="2480c-166">**Чтобы настроить подготовку учетных записей пользователей, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="2480c-166">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="2480c-167">Выполните вход на веб-сайт компании **Coupa** в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="2480c-167">Log in to your **Coupa** company site as administrator.</span></span>
2. <span data-ttu-id="2480c-168">В меню вверху щелкните **Setup** (Настройка) и выберите **Users** (Пользователи).</span><span class="sxs-lookup"><span data-stu-id="2480c-168">In the menu on the top, click **Setup**, and then click **Users**.</span></span>
   
   <span data-ttu-id="2480c-169">![Пользователи](./media/active-directory-saas-coupa-tutorial/IC791908.png "Пользователи")</span><span class="sxs-lookup"><span data-stu-id="2480c-169">![Users](./media/active-directory-saas-coupa-tutorial/IC791908.png "Users")</span></span>
3. <span data-ttu-id="2480c-170">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="2480c-170">Click **Create**.</span></span>
   
   <span data-ttu-id="2480c-171">![Создание пользователей](./media/active-directory-saas-coupa-tutorial/IC791909.png "Создание пользователей")</span><span class="sxs-lookup"><span data-stu-id="2480c-171">![Create Users](./media/active-directory-saas-coupa-tutorial/IC791909.png "Create Users")</span></span>
4. <span data-ttu-id="2480c-172">В разделе **Создание пользователя** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="2480c-172">In the **User Create** section, perform the following steps:</span></span>
   
   <span data-ttu-id="2480c-173">![Сведения о пользователе](./media/active-directory-saas-coupa-tutorial/IC791910.png "Сведения о пользователе")</span><span class="sxs-lookup"><span data-stu-id="2480c-173">![User Details](./media/active-directory-saas-coupa-tutorial/IC791910.png "User Details")</span></span>
   
   1. <span data-ttu-id="2480c-174">В соответствующие текстовые поля введите атрибуты **Login** (Имя для входа), **First name** (Имя), **Last Name** (Фамилия), **Single Sign-On ID** (Идентификатор единого входа) и **Email** (Адрес электронной почты) действующей учетной записи Azure Active Directory, которую вы хотите подготовить.</span><span class="sxs-lookup"><span data-stu-id="2480c-174">Type the **Login**, **First name**, **Last Name**, **Single Sign-On ID**, **Email** attributes of a valid Azure Active Directory account you want to provision into the related textboxes.</span></span>
   2. <span data-ttu-id="2480c-175">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="2480c-175">Click **Create**.</span></span>   
   >[!NOTE]
   ><span data-ttu-id="2480c-176">Владелец учетной записи Azure Active Directory получит электронное сообщение со ссылкой для подтверждения учетной записи перед ее активацией.</span><span class="sxs-lookup"><span data-stu-id="2480c-176">The Azure Active Directory account holder will get an email with a link to confirm the account before it becomes active.</span></span> 
   > 

>[!NOTE]
><span data-ttu-id="2480c-177">Вы можете использовать любые другие средства создания учетной записи пользователя Coupa или API, предоставляемые Coupa для подготовки учетных записей пользователя AAD.</span><span class="sxs-lookup"><span data-stu-id="2480c-177">You can use any other Coupa user account creation tools or APIs provided by Coupa to provision AAD user accounts.</span></span> 
> 

## <a name="assign-users"></a><span data-ttu-id="2480c-178">Назначить пользователей</span><span class="sxs-lookup"><span data-stu-id="2480c-178">Assign users</span></span>
<span data-ttu-id="2480c-179">Чтобы проверить свою конфигурацию, предоставьте пользователям Azure AD, которые должны использовать приложение, доступ путем их назначения.</span><span class="sxs-lookup"><span data-stu-id="2480c-179">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="2480c-180">**Чтобы назначить пользователей Coupa, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="2480c-180">**To assign users to Coupa, perform the following steps:**</span></span>

1. <span data-ttu-id="2480c-181">На классическом портале Azure создайте тестовую учетную запись.</span><span class="sxs-lookup"><span data-stu-id="2480c-181">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="2480c-182">На ** Coupa ** странице интеграции приложения щелкните **назначить пользователей**.</span><span class="sxs-lookup"><span data-stu-id="2480c-182">On the **Coupa **application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="2480c-183">![Назначение пользователей](./media/active-directory-saas-coupa-tutorial/IC791911.png "Назначение пользователей")</span><span class="sxs-lookup"><span data-stu-id="2480c-183">![Assign Users](./media/active-directory-saas-coupa-tutorial/IC791911.png "Assign Users")</span></span>
3. <span data-ttu-id="2480c-184">Выберите тестового пользователя, нажмите кнопку **Назначить**, а затем — **Да**, чтобы подтвердить назначение.</span><span class="sxs-lookup"><span data-stu-id="2480c-184">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="2480c-185">![Да](./media/active-directory-saas-coupa-tutorial/IC767830.png "Да")</span><span class="sxs-lookup"><span data-stu-id="2480c-185">![Yes](./media/active-directory-saas-coupa-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="2480c-186">Если вы хотите проверить параметры единого входа, откройте панель доступа.</span><span class="sxs-lookup"><span data-stu-id="2480c-186">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="2480c-187">Дополнительные сведения о панели доступа можно найти в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2480c-187">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

