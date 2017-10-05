---
title: "Руководство по интеграции Azure Active Directory с TalentLMS | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в TalentLMS."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c903d20d-18e3-42b0-b997-6349c5412dde
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: f28d6fbfad9dae578a20db7218b7e3b174ed859c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-talentlms"></a><span data-ttu-id="d98ed-103">Руководство по интеграции Azure Active Directory с TalentLMS</span><span class="sxs-lookup"><span data-stu-id="d98ed-103">Tutorial: Azure Active Directory integration with TalentLMS</span></span>

<span data-ttu-id="d98ed-104">В этом руководстве описано, как интегрировать приложение TalentLMS с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d98ed-104">In this tutorial, you learn how to integrate TalentLMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d98ed-105">Интеграция Azure AD с приложением TalentLMS обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="d98ed-105">Integrating TalentLMS with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d98ed-106">С помощью Azure AD вы можете контролировать доступ к TalentLMS.</span><span class="sxs-lookup"><span data-stu-id="d98ed-106">You can control in Azure AD who has access to TalentLMS</span></span>
- <span data-ttu-id="d98ed-107">Вы можете включить автоматический вход пользователей в TalentLMS (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d98ed-107">You can enable your users to automatically get signed-on to TalentLMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d98ed-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="d98ed-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d98ed-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d98ed-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d98ed-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d98ed-110">Prerequisites</span></span>

<span data-ttu-id="d98ed-111">Чтобы настроить интеграцию Azure AD с TalentLMS, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="d98ed-111">To configure Azure AD integration with TalentLMS, you need the following items:</span></span>

- <span data-ttu-id="d98ed-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="d98ed-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d98ed-113">подписка TalentLMS с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="d98ed-113">A TalentLMS single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d98ed-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="d98ed-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d98ed-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="d98ed-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d98ed-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="d98ed-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d98ed-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d98ed-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d98ed-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="d98ed-118">Scenario description</span></span>
<span data-ttu-id="d98ed-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="d98ed-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d98ed-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="d98ed-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d98ed-121">Добавление TalentLMS из коллекции.</span><span class="sxs-lookup"><span data-stu-id="d98ed-121">Adding TalentLMS from the gallery</span></span>
2. <span data-ttu-id="d98ed-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="d98ed-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-talentlms-from-the-gallery"></a><span data-ttu-id="d98ed-123">Добавление TalentLMS из коллекции</span><span class="sxs-lookup"><span data-stu-id="d98ed-123">Adding TalentLMS from the gallery</span></span>
<span data-ttu-id="d98ed-124">Чтобы настроить интеграцию TalentLMS с Azure AD, необходимо добавить TalentLMS из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="d98ed-124">To configure the integration of TalentLMS into Azure AD, you need to add TalentLMS from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d98ed-125">**Чтобы добавить TalentLMS из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="d98ed-125">**To add TalentLMS from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d98ed-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d98ed-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d98ed-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="d98ed-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d98ed-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="d98ed-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="d98ed-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="d98ed-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="d98ed-133">В поле поиска введите **TalentLMS**.</span><span class="sxs-lookup"><span data-stu-id="d98ed-133">In the search box, type **TalentLMS**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_search.png)

5. <span data-ttu-id="d98ed-135">На панели результатов выберите **TalentLMS** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="d98ed-135">In the results panel, select **TalentLMS**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d98ed-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="d98ed-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d98ed-138">В этом разделе описана настройка и проверка единого входа Azure AD в TalentLMS с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d98ed-138">In this section, you configure and test Azure AD single sign-on with TalentLMS based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="d98ed-139">Чтобы единый вход работал, Azure AD необходима информация о том, какой пользователь в TalentLMS соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d98ed-139">For single sign-on to work, Azure AD needs to know what the counterpart user in TalentLMS is to a user in Azure AD.</span></span> <span data-ttu-id="d98ed-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в TalentLMS.</span><span class="sxs-lookup"><span data-stu-id="d98ed-140">In other words, a link relationship between an Azure AD user and the related user in TalentLMS needs to be established.</span></span>

<span data-ttu-id="d98ed-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в TalentLMS.</span><span class="sxs-lookup"><span data-stu-id="d98ed-141">In TalentLMS, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d98ed-142">Чтобы настроить и проверить единый вход Azure AD в TalentLMS, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="d98ed-142">To configure and test Azure AD single sign-on with TalentLMS, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d98ed-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="d98ed-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d98ed-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d98ed-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d98ed-145">**[Создание тестового пользователя TalentLMS](#creating-a-talentlms-test-user)** требуется для того, чтобы в TalentLMS существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d98ed-145">**[Creating a TalentLMS test user](#creating-a-talentlms-test-user)** - to have a counterpart of Britta Simon in TalentLMS that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d98ed-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d98ed-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d98ed-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="d98ed-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d98ed-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="d98ed-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d98ed-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении TalentLMS.</span><span class="sxs-lookup"><span data-stu-id="d98ed-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TalentLMS application.</span></span>

<span data-ttu-id="d98ed-150">**Чтобы настроить единый вход Azure AD в TalentLMS, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="d98ed-150">**To configure Azure AD single sign-on with TalentLMS, perform the following steps:**</span></span>

1. <span data-ttu-id="d98ed-151">На портале Azure на странице интеграции с приложением **TalentLMS** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="d98ed-151">In the Azure portal, on the **TalentLMS** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="d98ed-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="d98ed-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_samlbase.png)

3. <span data-ttu-id="d98ed-155">В разделе **Домены и URL-адреса приложения TalentLMS** сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="d98ed-155">On the **TalentLMS Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_url.png)

    <span data-ttu-id="d98ed-157">а.</span><span class="sxs-lookup"><span data-stu-id="d98ed-157">a.</span></span> <span data-ttu-id="d98ed-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<tenant-name>.TalentLMSapp.com`</span><span class="sxs-lookup"><span data-stu-id="d98ed-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.TalentLMSapp.com`</span></span>

    <span data-ttu-id="d98ed-159">b.</span><span class="sxs-lookup"><span data-stu-id="d98ed-159">b.</span></span> <span data-ttu-id="d98ed-160">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `http://<tenant-name>.talentlms.com`</span><span class="sxs-lookup"><span data-stu-id="d98ed-160">In the **Identifier** textbox, type a URL using the following pattern: `http://<tenant-name>.talentlms.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d98ed-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="d98ed-161">These values are not real.</span></span> <span data-ttu-id="d98ed-162">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="d98ed-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="d98ed-163">Чтобы получить эти значения, обратитесь к [группе поддержки TalentLMS](https://www.talentlms.com/contact).</span><span class="sxs-lookup"><span data-stu-id="d98ed-163">Contact [TalentLMS Client support team](https://www.talentlms.com/contact) to get these values.</span></span> 
 
4. <span data-ttu-id="d98ed-164">В разделе **Сертификат подписи SAML** скопируйте значение **Отпечаток** сертификата.</span><span class="sxs-lookup"><span data-stu-id="d98ed-164">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value from the certificate.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_certificate.png) 

5. <span data-ttu-id="d98ed-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="d98ed-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-talentlms-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d98ed-168">В разделе **Конфигурация TalentLMS** щелкните **Настроить TalentLMS**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="d98ed-168">On the **TalentLMS Configuration** section, click **Configure TalentLMS** to open **Configure sign-on** window.</span></span> <span data-ttu-id="d98ed-169">Скопируйте **URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML**  из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="d98ed-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_configure.png)  

7. <span data-ttu-id="d98ed-171">В другом окне веб-браузера войдите на свой корпоративный веб-сайт TalentLMS в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="d98ed-171">In a different web browser window, log in to your TalentLMS company site as an administrator.</span></span>

8. <span data-ttu-id="d98ed-172">В разделе **Учетная запись и параметры** выберите вкладку **Пользователи**.</span><span class="sxs-lookup"><span data-stu-id="d98ed-172">In the **Account & Settings** section, click the **Users** tab.</span></span>
   
    <span data-ttu-id="d98ed-173">![Учетная запись и параметры](./media/active-directory-saas-talentlms-tutorial/IC777296.png "Учетная запись и параметры")</span><span class="sxs-lookup"><span data-stu-id="d98ed-173">![Account & Settings](./media/active-directory-saas-talentlms-tutorial/IC777296.png "Account & Settings")</span></span>

9. <span data-ttu-id="d98ed-174">Щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="d98ed-174">Click **Single Sign-On (SSO)**,</span></span>

10. <span data-ttu-id="d98ed-175">В разделе "Единый вход" выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="d98ed-175">In the Single Sign-On section, perform the following steps:</span></span>
   
    <span data-ttu-id="d98ed-176">![Единый вход](./media/active-directory-saas-talentlms-tutorial/IC777297.png "Единый вход")</span><span class="sxs-lookup"><span data-stu-id="d98ed-176">![Single Sign-On](./media/active-directory-saas-talentlms-tutorial/IC777297.png "Single Sign-On")</span></span>   

    <span data-ttu-id="d98ed-177">а.</span><span class="sxs-lookup"><span data-stu-id="d98ed-177">a.</span></span> <span data-ttu-id="d98ed-178">Из списка **Тип интеграции единого входа** выберите **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="d98ed-178">From the **SSO integration type** list, select **SAML 2.0**.</span></span>

    <span data-ttu-id="d98ed-179">b.</span><span class="sxs-lookup"><span data-stu-id="d98ed-179">b.</span></span> <span data-ttu-id="d98ed-180">В текстовое поле **Identity Provider (IDP)** (Поставщик удостоверений (IdP)) вставьте значение **SAML Entity ID** (Идентификатор сущности SAML), скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="d98ed-180">In the **Identity provider (IDP)** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>
 
    <span data-ttu-id="d98ed-181">c.</span><span class="sxs-lookup"><span data-stu-id="d98ed-181">c.</span></span> <span data-ttu-id="d98ed-182">Вставьте значение **Отпечаток** с портала Azure в текстовое поле **Certificate Fingerprint** (Отпечаток сертификата).</span><span class="sxs-lookup"><span data-stu-id="d98ed-182">Paste the **Thumbprint** value from Azure portal into the **Certificate fingerprint** textbox.</span></span>    

    <span data-ttu-id="d98ed-183">г)</span><span class="sxs-lookup"><span data-stu-id="d98ed-183">d.</span></span>  <span data-ttu-id="d98ed-184">В текстовое поле **Remote sign-in URL** (URL-адрес удаленного входа) вставьте значение **SAML Single Sign-On Service URL** (URL-адрес службы единого входа SAML), скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="d98ed-184">In the **Remote sign-in URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
 
    <span data-ttu-id="d98ed-185">д.</span><span class="sxs-lookup"><span data-stu-id="d98ed-185">e.</span></span> <span data-ttu-id="d98ed-186">В текстовое поле **Remote sign-out URL** (URL-адрес удаленного выхода) вставьте значение **URL-адрес выхода**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="d98ed-186">In the **Remote sign-out URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="d98ed-187">f.</span><span class="sxs-lookup"><span data-stu-id="d98ed-187">f.</span></span> <span data-ttu-id="d98ed-188">Укажите следующие сведения.</span><span class="sxs-lookup"><span data-stu-id="d98ed-188">Fill in the following:</span></span> 

    * <span data-ttu-id="d98ed-189">В текстовое поле **TargetedID** (Целевой идентификатор) введите `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="d98ed-189">In the **TargetedID** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`</span></span>
     
    * <span data-ttu-id="d98ed-190">В текстовое поле **First Name** (Имя) введите `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span><span class="sxs-lookup"><span data-stu-id="d98ed-190">In the **First name** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`</span></span>
    
    * <span data-ttu-id="d98ed-191">В текстовое поле **Last Name** (Фамилия) введите `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span><span class="sxs-lookup"><span data-stu-id="d98ed-191">In the **Last name** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`</span></span>
    
    * <span data-ttu-id="d98ed-192">В текстовое поле **Email** (Электронная почта) введите `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="d98ed-192">In the **Email** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`</span></span>
    
11. <span data-ttu-id="d98ed-193">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="d98ed-193">Click **Save**.</span></span>
 
> [!TIP]
> <span data-ttu-id="d98ed-194">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="d98ed-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d98ed-195">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="d98ed-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d98ed-196">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="d98ed-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d98ed-197">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="d98ed-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="d98ed-198">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d98ed-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="d98ed-200">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="d98ed-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d98ed-201">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d98ed-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-talentlms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d98ed-203">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="d98ed-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-talentlms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d98ed-205">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="d98ed-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-talentlms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d98ed-207">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="d98ed-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-talentlms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d98ed-209">а.</span><span class="sxs-lookup"><span data-stu-id="d98ed-209">a.</span></span> <span data-ttu-id="d98ed-210">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d98ed-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d98ed-211">b.</span><span class="sxs-lookup"><span data-stu-id="d98ed-211">b.</span></span> <span data-ttu-id="d98ed-212">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d98ed-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d98ed-213">c.</span><span class="sxs-lookup"><span data-stu-id="d98ed-213">c.</span></span> <span data-ttu-id="d98ed-214">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="d98ed-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d98ed-215">d.</span><span class="sxs-lookup"><span data-stu-id="d98ed-215">d.</span></span> <span data-ttu-id="d98ed-216">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="d98ed-216">Click **Create**.</span></span>
 
### <a name="creating-a-talentlms-test-user"></a><span data-ttu-id="d98ed-217">Создание тестового пользователя TalentLMS</span><span class="sxs-lookup"><span data-stu-id="d98ed-217">Creating a TalentLMS test user</span></span>

<span data-ttu-id="d98ed-218">Чтобы пользователи Azure AD могли выполнить вход в TalentLMS, они должны быть подготовлены в TalentLMS.</span><span class="sxs-lookup"><span data-stu-id="d98ed-218">To enable Azure AD users to log in to TalentLMS, they must be provisioned into TalentLMS.</span></span> <span data-ttu-id="d98ed-219">В случае использования TalentLMS подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="d98ed-219">In the case of TalentLMS, provisioning is a manual task.</span></span>

<span data-ttu-id="d98ed-220">**Чтобы подготовить учетную запись пользователя, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="d98ed-220">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="d98ed-221">Войдите в клиент **TalentLMS** .</span><span class="sxs-lookup"><span data-stu-id="d98ed-221">Log in to your **TalentLMS** tenant.</span></span>

2. <span data-ttu-id="d98ed-222">Щелкните **Пользователи**, а затем — **Добавить пользователя**.</span><span class="sxs-lookup"><span data-stu-id="d98ed-222">Click **Users**, and then click **Add User**.</span></span>

3. <span data-ttu-id="d98ed-223">На странице диалогового окна **Добавление пользователя** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="d98ed-223">On the **Add user** dialog page, perform the following steps:</span></span>
   
    <span data-ttu-id="d98ed-224">![Добавление пользователя](./media/active-directory-saas-talentlms-tutorial/IC777299.png "Добавление пользователя")</span><span class="sxs-lookup"><span data-stu-id="d98ed-224">![Add User](./media/active-directory-saas-talentlms-tutorial/IC777299.png "Add User")</span></span>  

    <span data-ttu-id="d98ed-225">а.</span><span class="sxs-lookup"><span data-stu-id="d98ed-225">a.</span></span> <span data-ttu-id="d98ed-226">В текстовое поле **First name** (Имя) введите имя пользователя, например **Britta**.</span><span class="sxs-lookup"><span data-stu-id="d98ed-226">In the **First name** textbox, enter the first name of user like **Britta**.</span></span>

    <span data-ttu-id="d98ed-227">b.</span><span class="sxs-lookup"><span data-stu-id="d98ed-227">b.</span></span> <span data-ttu-id="d98ed-228">В текстовое поле **Last name** (Фамилия) введите фамилию пользователя, например **Simon**.</span><span class="sxs-lookup"><span data-stu-id="d98ed-228">In the **Last name** textbox, enter the last name of user like **Simon**.</span></span>
 
    <span data-ttu-id="d98ed-229">c.</span><span class="sxs-lookup"><span data-stu-id="d98ed-229">c.</span></span> <span data-ttu-id="d98ed-230">В текстовое поле **Email address** (Адрес электронной почты) введите адрес электронной почты пользователя, например **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="d98ed-230">In the **Email address** textbox, enter the email of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="d98ed-231">г)</span><span class="sxs-lookup"><span data-stu-id="d98ed-231">d.</span></span> <span data-ttu-id="d98ed-232">Нажмите кнопку **Add User**(Добавить пользователя).</span><span class="sxs-lookup"><span data-stu-id="d98ed-232">Click **Add User**.</span></span>

>[!NOTE]
><span data-ttu-id="d98ed-233">Вы можете использовать любые другие средства создания учетной записи пользователя TalentLMS или API-интерфейсы, предоставляемые TalentLMS для подготовки учетных записей пользователя AAD.</span><span class="sxs-lookup"><span data-stu-id="d98ed-233">You can use any other TalentLMS user account creation tools or APIs provided by TalentLMS to provision AAD user accounts.</span></span>
 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d98ed-234">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="d98ed-234">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d98ed-235">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к TalentLMS.</span><span class="sxs-lookup"><span data-stu-id="d98ed-235">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TalentLMS.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="d98ed-237">**Чтобы назначить пользователя Britta Simon в TalentLMS, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="d98ed-237">**To assign Britta Simon to TalentLMS, perform the following steps:**</span></span>

1. <span data-ttu-id="d98ed-238">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="d98ed-238">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="d98ed-240">Из списка приложений выберите **TalentLMS**.</span><span class="sxs-lookup"><span data-stu-id="d98ed-240">In the applications list, select **TalentLMS**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-talentlms-tutorial/tutorial_talentlms_app.png) 

3. <span data-ttu-id="d98ed-242">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="d98ed-242">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="d98ed-244">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="d98ed-244">Click **Add** button.</span></span> <span data-ttu-id="d98ed-245">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="d98ed-245">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="d98ed-247">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="d98ed-247">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d98ed-248">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="d98ed-248">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d98ed-249">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="d98ed-249">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d98ed-250">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="d98ed-250">Testing single sign-on</span></span>

<span data-ttu-id="d98ed-251">Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="d98ed-251">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d98ed-252">Щелкнув элемент "TalentLMS" на панели доступа, вы автоматически войдете в приложение TalentLMS.</span><span class="sxs-lookup"><span data-stu-id="d98ed-252">When you click the TalentLMS tile in the Access Panel, you should get automatically signed-on to your TalentLMS application</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d98ed-253">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="d98ed-253">Additional resources</span></span>

* [<span data-ttu-id="d98ed-254">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d98ed-254">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d98ed-255">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d98ed-255">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-talentlms-tutorial/tutorial_general_203.png

