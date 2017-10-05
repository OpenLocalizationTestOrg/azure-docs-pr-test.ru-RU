---
title: "Учебник. Интеграция Azure Active Directory с Cisco Webex | Документация Майкрософт"
description: "Узнайте, как использовать Cisco Webex вместе с Azure Active Directory для реализации единого входа, автоматической подготовки пользователей и выполнения других задач."
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
ms.openlocfilehash: b44b1a5b3e988a51db3325ec8a181651fa84e768
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cisco-webex"></a><span data-ttu-id="fe258-103">Руководство. Интеграция Azure Active Directory с Cisco Webex</span><span class="sxs-lookup"><span data-stu-id="fe258-103">Tutorial: Azure Active Directory Integration with Cisco Webex</span></span>
<span data-ttu-id="fe258-104">Цель данного учебника — показать интеграцию Azure и Cisco Webex.</span><span class="sxs-lookup"><span data-stu-id="fe258-104">The objective of this tutorial is to show the integration of Azure and Cisco Webex.</span></span>  
<span data-ttu-id="fe258-105">Сценарий, описанный в этом учебнике, предполагает, что у вас уже имеется:</span><span class="sxs-lookup"><span data-stu-id="fe258-105">The scenario outlined in this tutorial assumes that you already have the following items:</span></span>

* <span data-ttu-id="fe258-106">Действующая подписка на Azure</span><span class="sxs-lookup"><span data-stu-id="fe258-106">A valid Azure subscription</span></span>
* <span data-ttu-id="fe258-107">Клиент Cisco Webex</span><span class="sxs-lookup"><span data-stu-id="fe258-107">A Cisco Webex tenant</span></span>

<span data-ttu-id="fe258-108">После выполнения действий, описанных в этом руководстве, пользователи Azure AD, которых вы прикрепите к Cisco Webex, смогут использовать единый вход в приложение на веб-сайте Cisco Webex вашей организации (вход, инициированный поставщиком услуг) или на панели доступа, как описано в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="fe258-108">After completing this tutorial, the Azure AD users you have assigned to Cisco Webex will be able to single sign into the application at your Cisco Webex company site (service provider initiated sign on), or using the [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

<span data-ttu-id="fe258-109">Сценарий, описанный в этом учебнике, состоит из следующих блоков:</span><span class="sxs-lookup"><span data-stu-id="fe258-109">The scenario outlined in this tutorial consists of the following building blocks:</span></span>

* <span data-ttu-id="fe258-110">Включение интеграции приложений для Cisco Webex</span><span class="sxs-lookup"><span data-stu-id="fe258-110">Enabling the application integration for Cisco Webex</span></span>
* <span data-ttu-id="fe258-111">Настройка единого входа</span><span class="sxs-lookup"><span data-stu-id="fe258-111">Configuring single sign-on (SSO)</span></span>
* <span data-ttu-id="fe258-112">Настройка подготовки учетных записей пользователей</span><span class="sxs-lookup"><span data-stu-id="fe258-112">Configuring user provisioning</span></span>
* <span data-ttu-id="fe258-113">Назначение пользователей</span><span class="sxs-lookup"><span data-stu-id="fe258-113">Assigning users</span></span>

<span data-ttu-id="fe258-114">![Сценарий](./media/active-directory-saas-cisco-webex-tutorial/IC777614.png "Сценарий")</span><span class="sxs-lookup"><span data-stu-id="fe258-114">![Scenario](./media/active-directory-saas-cisco-webex-tutorial/IC777614.png "Scenario")</span></span>

## <a name="enable-the-application-integration-for-cisco-webex"></a><span data-ttu-id="fe258-115">Включение интеграции приложений для Cisco Webex</span><span class="sxs-lookup"><span data-stu-id="fe258-115">Enable the application integration for Cisco Webex</span></span>
<span data-ttu-id="fe258-116">В этом разделе показано, как включить интеграцию приложений для Cisco Webex.</span><span class="sxs-lookup"><span data-stu-id="fe258-116">The objective of this section is to outline how to enable the application integration for Cisco Webex.</span></span>

<span data-ttu-id="fe258-117">**Чтобы включить интеграцию приложений для Cisco Webex, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="fe258-117">**To enable the application integration for Cisco Webex, perform the following steps:**</span></span>

1. <span data-ttu-id="fe258-118">На классическом портале Azure в области навигации слева щелкните **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fe258-118">In the Azure classic portal, on the left navigation pane, click **Active Directory**.</span></span>
   
   <span data-ttu-id="fe258-119">![Active Directory](./media/active-directory-saas-cisco-webex-tutorial/IC700993.png "Active Directory")</span><span class="sxs-lookup"><span data-stu-id="fe258-119">![Active Directory](./media/active-directory-saas-cisco-webex-tutorial/IC700993.png "Active Directory")</span></span>
2. <span data-ttu-id="fe258-120">Из списка **Каталог** выберите каталог, для которого нужно включить интеграцию каталогов.</span><span class="sxs-lookup"><span data-stu-id="fe258-120">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
3. <span data-ttu-id="fe258-121">Чтобы открыть представление приложений, в представлении каталога нажмите **Приложения** в верхнем меню.</span><span class="sxs-lookup"><span data-stu-id="fe258-121">To open the applications view, in the directory view, click **Applications** in the top menu.</span></span>
   
   <span data-ttu-id="fe258-122">![Приложения](./media/active-directory-saas-cisco-webex-tutorial/IC700994.png "Приложения")</span><span class="sxs-lookup"><span data-stu-id="fe258-122">![Applications](./media/active-directory-saas-cisco-webex-tutorial/IC700994.png "Applications")</span></span>
4. <span data-ttu-id="fe258-123">В нижней части страницы нажмите кнопку **Добавить** .</span><span class="sxs-lookup"><span data-stu-id="fe258-123">Click **Add** at the bottom of the page.</span></span>
   
   <span data-ttu-id="fe258-124">![Добавление приложения](./media/active-directory-saas-cisco-webex-tutorial/IC749321.png "Добавление приложения")</span><span class="sxs-lookup"><span data-stu-id="fe258-124">![Add application](./media/active-directory-saas-cisco-webex-tutorial/IC749321.png "Add application")</span></span>
5. <span data-ttu-id="fe258-125">В диалоговом окне **Что необходимо сделать?** щелкните **Добавить приложение из коллекции**.</span><span class="sxs-lookup"><span data-stu-id="fe258-125">On the **What do you want to do** dialog, click **Add an application from the gallery**.</span></span>
   
   <span data-ttu-id="fe258-126">![Добавление приложения из коллекции](./media/active-directory-saas-cisco-webex-tutorial/IC749322.png "Добавление приложения из коллекции")</span><span class="sxs-lookup"><span data-stu-id="fe258-126">![Add an application from gallerry](./media/active-directory-saas-cisco-webex-tutorial/IC749322.png "Add an application from gallerry")</span></span>
6. <span data-ttu-id="fe258-127">В **поле поиска** введите **Cisco Webex**.</span><span class="sxs-lookup"><span data-stu-id="fe258-127">In the **search box**, type **Cisco Webex**.</span></span>
   
   <span data-ttu-id="fe258-128">![Коллекция приложений](./media/active-directory-saas-cisco-webex-tutorial/IC777615.png "Коллекция приложений")</span><span class="sxs-lookup"><span data-stu-id="fe258-128">![Application Gallery](./media/active-directory-saas-cisco-webex-tutorial/IC777615.png "Application Gallery")</span></span>
7. <span data-ttu-id="fe258-129">В области результатов выберите **Cisco Webex** и нажмите кнопку **Завершить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="fe258-129">In the results pane, select **Cisco Webex**, and then click **Complete** to add the application.</span></span>
   
   <span data-ttu-id="fe258-130">![Cisco Webex](./media/active-directory-saas-cisco-webex-tutorial/IC777616.png "Cisco Webex")</span><span class="sxs-lookup"><span data-stu-id="fe258-130">![Cisco Webex](./media/active-directory-saas-cisco-webex-tutorial/IC777616.png "Cisco Webex")</span></span>
   
## <a name="configure-single-sign-on"></a><span data-ttu-id="fe258-131">Настройка единого входа</span><span class="sxs-lookup"><span data-stu-id="fe258-131">Configure single sign-on</span></span>

<span data-ttu-id="fe258-132">В этом разделе показано, как разрешить пользователям проходить проверку подлинности в Cisco Webex со своей учетной записью Azure AD, используя федерацию на основе протокола SAML.</span><span class="sxs-lookup"><span data-stu-id="fe258-132">The objective of this section is to outline how to enable users to authenticate to Cisco Webex with their account in Azure AD using federation based on the SAML protocol.</span></span>  

<span data-ttu-id="fe258-133">В рамках этой процедуры потребуется создать сертификат в кодировке Base-64.</span><span class="sxs-lookup"><span data-stu-id="fe258-133">As part of this procedure, you are required to create a base-64 encoded certificate.</span></span> <span data-ttu-id="fe258-134">Если вы не знакомы с этой процедурой, просмотрите видео [Как преобразовать двоичный сертификат в текстовый файл](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="fe258-134">If you are not familiar with this procedure, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>

<span data-ttu-id="fe258-135">**Чтобы настроить единый вход, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="fe258-135">**To configure single sign-on, perform the following steps:**</span></span>

1. <span data-ttu-id="fe258-136">На странице интеграции с приложением **Cisco Webex** классического портала Azure щелкните **Настройка единого входа**, чтобы открыть диалоговое окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="fe258-136">In the Azure classic portal, on the **Cisco Webex** application integration page, click **Configure single sign-on** to open the **Configure Single Sign On** dialog.</span></span>
   
   <span data-ttu-id="fe258-137">![Настройка единого входа](./media/active-directory-saas-cisco-webex-tutorial/IC777617.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="fe258-137">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777617.png "Configure single sign-on")</span></span>
2. <span data-ttu-id="fe258-138">На странице **Как пользователи должны входить в Cisco Webex?** выберите **Единый вход Microsoft Azure AD** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="fe258-138">On the **How would you like users to sign on to Cisco Webex** page, select **Microsoft Azure AD Single Sign-On**, and then click **Next**.</span></span>
   
   <span data-ttu-id="fe258-139">![Настройка единого входа](./media/active-directory-saas-cisco-webex-tutorial/IC777618.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="fe258-139">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777618.png "Configure single sign-on")</span></span>
3. <span data-ttu-id="fe258-140">На странице **Настроить URL-адрес приложения** выполните следующие действия и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="fe258-140">On the **Configure App URL** page, perform the following steps, and then click **Next**.</span></span>
   
   <span data-ttu-id="fe258-141">![Настройка URL-адреса приложения](./media/active-directory-saas-cisco-webex-tutorial/IC777619.png "Настройка URL-адреса приложения")</span><span class="sxs-lookup"><span data-stu-id="fe258-141">![Configure app URL](./media/active-directory-saas-cisco-webex-tutorial/IC777619.png "Configure app URL")</span></span>   
   1. <span data-ttu-id="fe258-142">В текстовом поле **URL-адрес для входа** введите URL-адрес клиента Cisco Webex (например, *http://contoso.webex.com*).</span><span class="sxs-lookup"><span data-stu-id="fe258-142">In the **Sing On URL** textbox, type your Cisco Webex tenant URL (e.g.: *http://contoso.webex.com*).</span></span>
   2. <span data-ttu-id="fe258-143">В текстовом поле **URL-адрес ответа Cisco Webex** введите **URL-адрес службы AssertionConsumerService Cisco Webex** (например, *https://компания.webex.com/dispatcher/SAML2AuthService?siteurl=company*).</span><span class="sxs-lookup"><span data-stu-id="fe258-143">In the **Cisco Webex Reply URL** textbox, type your **Cisco Webex AssertionConsumerService URL** (e.g.: *https://company.webex.com/dispatcher/SAML2AuthService?siteurl=company*).</span></span>
4. <span data-ttu-id="fe258-144">На странице **Настройка единого входа в Cisco Webex** нажмите кнопку **Скачать сертификат** и сохраните файл сертификата на своем компьютере.</span><span class="sxs-lookup"><span data-stu-id="fe258-144">On the **Configure single sign-on at Cisco Webex** page, to download your certificate, click **Download certificate**, and then save the certificate file on your computer.</span></span>
   
   <span data-ttu-id="fe258-145">![Настройка единого входа](./media/active-directory-saas-cisco-webex-tutorial/IC777620.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="fe258-145">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777620.png "Configure single sign-on")</span></span>
5. <span data-ttu-id="fe258-146">В другом окне веб-браузера войдите на свой корпоративный веб-сайт Cisco Webex в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="fe258-146">In a different web browser window, log into your Cisco Webex company site as an administrator.</span></span>
6. <span data-ttu-id="fe258-147">В верхнем меню нажмите **Администрирование веб-сайта**.</span><span class="sxs-lookup"><span data-stu-id="fe258-147">In the menu on the top, click **Site Administration**.</span></span>
   
   <span data-ttu-id="fe258-148">![Администрирование сайта](./media/active-directory-saas-cisco-webex-tutorial/IC777621.png "Администрирование сайта")</span><span class="sxs-lookup"><span data-stu-id="fe258-148">![Site Administration](./media/active-directory-saas-cisco-webex-tutorial/IC777621.png "Site Administration")</span></span>
7. <span data-ttu-id="fe258-149">В разделе **Управление сайтом** выберите **SSO Configuration** (Настройка единого входа).</span><span class="sxs-lookup"><span data-stu-id="fe258-149">In the **Manage Site** section, click **SSO Configuration**.</span></span>
   
   <span data-ttu-id="fe258-150">![Настройка единого входа](./media/active-directory-saas-cisco-webex-tutorial/IC777622.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="fe258-150">![SSO Configuration](./media/active-directory-saas-cisco-webex-tutorial/IC777622.png "SSO Configuration")</span></span>
8. <span data-ttu-id="fe258-151">В разделе "Настройка федеративного единого входа в Интернете" выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="fe258-151">In the Federated Web SSO Configuration section, perform the following steps:</span></span>
   
   <span data-ttu-id="fe258-152">![Настройка федеративного единого входа](./media/active-directory-saas-cisco-webex-tutorial/IC777623.png "Настройка федеративного единого входа")</span><span class="sxs-lookup"><span data-stu-id="fe258-152">![Federated SSO Configuration](./media/active-directory-saas-cisco-webex-tutorial/IC777623.png "Federated SSO Configuration")</span></span>  
   1. <span data-ttu-id="fe258-153">В списке **Federation Protocol** (Протокол федерации) выберите пункт **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="fe258-153">From the **Federation Protocol** list, select **SAML 2.0**.</span></span>
   2. <span data-ttu-id="fe258-154">Создайте файл **в кодировке Base-64** из скачанного сертификата.</span><span class="sxs-lookup"><span data-stu-id="fe258-154">Create a **Base-64 encoded** file from your downloaded certificate.</span></span>  
    >[!TIP]
    ><span data-ttu-id="fe258-155">Дополнительные сведения можно узнать из видео [Как преобразовать двоичный сертификат в текстовый файл](http://youtu.be/PlgrzUZ-Y1o)</span><span class="sxs-lookup"><span data-stu-id="fe258-155">For more details, see [How to convert a binary certificate into a text file](http://youtu.be/PlgrzUZ-Y1o)</span></span>
    >  
   3. <span data-ttu-id="fe258-156">Откройте сертификат в кодировке Base-64 в блокноте и скопируйте его содержимое.</span><span class="sxs-lookup"><span data-stu-id="fe258-156">Open your base-64 encoded certificate in notepad, and then copy the content of it.</span></span>
   4. <span data-ttu-id="fe258-157">Нажмите **Импорт метаданных SAML**и вставьте сертификат в кодировке Base-64.</span><span class="sxs-lookup"><span data-stu-id="fe258-157">Click **Import SAML Metadata**, and then paste your base-64 encoded certificate.</span></span>
   5. <span data-ttu-id="fe258-158">На странице диалогового окна **Настройка единого входа в Cisco Webex** классического портала Azure скопируйте значение поля **URL-адрес издателя** и вставьте его в текстовое поле **Issuer for SAML (IdP ID)** (Издатель для SAML (идентификатор поставщика удостоверений)).</span><span class="sxs-lookup"><span data-stu-id="fe258-158">In the Azure classic portal, on the **Configure single sign-on at Cisco Webex** dialog page, copy the **Issuer URL** value, and then paste it into the **Issuer for SAML (IdP ID)** textbox.</span></span>
   6. <span data-ttu-id="fe258-159">На странице диалогового окна **Настройка единого входа в Cisco Webex** классического портала Azure скопируйте значение поля **URL-адрес удаленного входа** и вставьте его в текстовое поле **Customer SSO Service Login URL** (URL-адрес входа в клиентскую службу единого входа).</span><span class="sxs-lookup"><span data-stu-id="fe258-159">In the Azure classic portal, on the **Configure single sign-on at Cisco Webex** dialog page, copy the **Remote Login URL** value, and then paste it into the **Customer SSO Service Login URL** textbox.</span></span>
   7. <span data-ttu-id="fe258-160">В списке **NameID Format** (Формат элемента NameID) выберите пункт **Адрес электронной почты**.</span><span class="sxs-lookup"><span data-stu-id="fe258-160">From the **NameID Format** list, select **Email address**.</span></span>
   8. <span data-ttu-id="fe258-161">В текстовом поле **AuthnContextClassRef** введите **urn:oasis:names:tc:SAML:2.0:ac:classes:Password**.</span><span class="sxs-lookup"><span data-stu-id="fe258-161">In the **AuthnContextClassRef** textbox, type **urn:oasis:names:tc:SAML:2.0:ac:classes:Password**.</span></span>
   9. <span data-ttu-id="fe258-162">На странице диалогового окна **Настройка единого входа в Cisco Webex** классического портала Azure скопируйте значение поля **URL-адрес удаленного выхода** и вставьте его в текстовое поле **Customer SSO Service Logout URL** (URL-адрес выхода для клиентской службы единого входа).</span><span class="sxs-lookup"><span data-stu-id="fe258-162">In the Azure classic portal, on the **Configure single sign-on at Cisco Webex** dialog page, copy the **Remote Logout URL** value, and then paste it into the **Customer SSO Service Logout URL** textbox.</span></span>
   10. <span data-ttu-id="fe258-163">Нажмите кнопку **Обновить**.</span><span class="sxs-lookup"><span data-stu-id="fe258-163">Click **Update**.</span></span>
9. <span data-ttu-id="fe258-164">На странице диалогового окна **Настройка единого входа в Cisco Webex** классического портала Azure выберите подтверждение настройки единого входа и нажмите кнопку **Завершить**.</span><span class="sxs-lookup"><span data-stu-id="fe258-164">In the Azure classic portal, on the **Configure single sign-on at Cisco Webex** dialog page, select the single sign-on configuration confirmation, and then click **Complete**.</span></span>
   
   <span data-ttu-id="fe258-165">![Настройка единого входа](./media/active-directory-saas-cisco-webex-tutorial/IC777624.png "Настройка единого входа")</span><span class="sxs-lookup"><span data-stu-id="fe258-165">![Configure single sign-on](./media/active-directory-saas-cisco-webex-tutorial/IC777624.png "Configure single sign-on")</span></span>
   
## <a name="configure-user-provisioning"></a><span data-ttu-id="fe258-166">Настроить подготовку учетных записей пользователей</span><span class="sxs-lookup"><span data-stu-id="fe258-166">Configure user provisioning</span></span>

<span data-ttu-id="fe258-167">Чтобы пользователи Azure AD могли выполнить вход в Cisco Webex, они должны быть подготовлены для Cisco Webex.</span><span class="sxs-lookup"><span data-stu-id="fe258-167">In order to enable Azure AD users to log into Cisco Webex, they must be provisioned into Cisco Webex.</span></span>  

* <span data-ttu-id="fe258-168">В случае с Cisco Webex подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="fe258-168">In the case of Cisco Webex, provisioning is a manual task.</span></span>

<span data-ttu-id="fe258-169">**Чтобы подготовить учетные записи пользователей, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="fe258-169">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="fe258-170">Войдите в клиент **Cisco Webex** .</span><span class="sxs-lookup"><span data-stu-id="fe258-170">Log in to your **Cisco Webex** tenant.</span></span>
2. <span data-ttu-id="fe258-171">Последовательно выберите пункты **Manage Users \> Add User** (Управление пользователями > Добавить пользователя).</span><span class="sxs-lookup"><span data-stu-id="fe258-171">Go to **Manage Users \> Add User**.</span></span>
   
   <span data-ttu-id="fe258-172">![Добавление пользователей](./media/active-directory-saas-cisco-webex-tutorial/IC777625.png "Добавление пользователей")</span><span class="sxs-lookup"><span data-stu-id="fe258-172">![Add users](./media/active-directory-saas-cisco-webex-tutorial/IC777625.png "Add users")</span></span>
3. <span data-ttu-id="fe258-173">В разделе "Добавить пользователя" выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="fe258-173">On the Add User section, perform the following steps:</span></span>
   
   <span data-ttu-id="fe258-174">![Добавление пользователя](./media/active-directory-saas-cisco-webex-tutorial/IC777626.png "Добавление пользователя")</span><span class="sxs-lookup"><span data-stu-id="fe258-174">![Add user](./media/active-directory-saas-cisco-webex-tutorial/IC777626.png "Add user")</span></span>   
   1. <span data-ttu-id="fe258-175">Для параметра **Тип учетной записи** выберите значение **Узел**.</span><span class="sxs-lookup"><span data-stu-id="fe258-175">As **Account Type**, select **Host**.</span></span>
   2. <span data-ttu-id="fe258-176">Введите данные действующего пользователя Azure AD в следующие текстовые поля: **Имя, Фамилия**, **Имя пользователя**, **Адрес электронной почты**, **Пароль**, **Подтвердите пароль**.</span><span class="sxs-lookup"><span data-stu-id="fe258-176">Type the information of an existing Azure AD user into the following textboxes: **First name, Last name**, **User name**, **Email**, **Password**, **Confirm Password**.</span></span>
   3. <span data-ttu-id="fe258-177">Щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="fe258-177">Click **Add**.</span></span>

>[!NOTE]
><span data-ttu-id="fe258-178">Вы можете использовать любые другие инструменты создания учетной записи пользователя Cisco Webex или API, предоставляемые Cisco Webex для подготовки учетных записей пользователя AAD.</span><span class="sxs-lookup"><span data-stu-id="fe258-178">You can use any other Cisco Webex user account creation tools or APIs provided by Cisco Webex to provision AAD user accounts.</span></span> 
> 

## <a name="assign-users"></a><span data-ttu-id="fe258-179">Назначить пользователей</span><span class="sxs-lookup"><span data-stu-id="fe258-179">Assign users</span></span>
<span data-ttu-id="fe258-180">Чтобы проверить свою конфигурацию, предоставьте пользователям Azure AD, которые должны использовать приложение, доступ путем их назначения.</span><span class="sxs-lookup"><span data-stu-id="fe258-180">To test your configuration, you need to grant the Azure AD users you want to allow using your application access to it by assigning them.</span></span>

<span data-ttu-id="fe258-181">**Чтобы назначить пользователей Cisco Webex, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="fe258-181">**To assign users to Cisco Webex, perform the following steps:**</span></span>

1. <span data-ttu-id="fe258-182">На классическом портале Azure создайте тестовую учетную запись.</span><span class="sxs-lookup"><span data-stu-id="fe258-182">In the Azure classic portal, create a test account.</span></span>
2. <span data-ttu-id="fe258-183">На странице интеграции с приложением **Cisco Webex** нажмите кнопку **Назначить пользователей**.</span><span class="sxs-lookup"><span data-stu-id="fe258-183">On the **Cisco Webex** application integration page, click **Assign users**.</span></span>
   
   <span data-ttu-id="fe258-184">![Назначение пользователей](./media/active-directory-saas-cisco-webex-tutorial/IC777627.png "Назначение пользователей")</span><span class="sxs-lookup"><span data-stu-id="fe258-184">![Assign users](./media/active-directory-saas-cisco-webex-tutorial/IC777627.png "Assign users")</span></span>
3. <span data-ttu-id="fe258-185">Выберите тестового пользователя, нажмите кнопку **Назначить**, а затем — **Да**, чтобы подтвердить назначение.</span><span class="sxs-lookup"><span data-stu-id="fe258-185">Select your test user, click **Assign**, and then click **Yes** to confirm your assignment.</span></span>
   
   <span data-ttu-id="fe258-186">![Да](./media/active-directory-saas-cisco-webex-tutorial/IC767830.png "Да")</span><span class="sxs-lookup"><span data-stu-id="fe258-186">![Yes](./media/active-directory-saas-cisco-webex-tutorial/IC767830.png "Yes")</span></span>

<span data-ttu-id="fe258-187">Если вы хотите проверить параметры единого входа, откройте панель доступа.</span><span class="sxs-lookup"><span data-stu-id="fe258-187">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="fe258-188">Дополнительные сведения о панели доступа можно найти в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="fe258-188">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

