---
title: "Руководство по интеграции Azure Active Directory с QuickHelp | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и QuickHelp."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 655c9ad3-2076-4e2c-8e47-9ed3bf04be56
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: jeedes
ms.openlocfilehash: 1c72b0ddee636090129dab7a5c7ec6ffd452434a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-quickhelp"></a><span data-ttu-id="d62c0-103">Руководство. Интеграция Azure Active Directory с QuickHelp</span><span class="sxs-lookup"><span data-stu-id="d62c0-103">Tutorial: Azure Active Directory integration with QuickHelp</span></span>

<span data-ttu-id="d62c0-104">В этом руководстве описано, как интегрировать QuickHelp с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d62c0-104">In this tutorial, you learn how to integrate QuickHelp with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d62c0-105">Интеграция Azure AD с приложением QuickHelp обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="d62c0-105">Integrating QuickHelp with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d62c0-106">с помощью Azure AD вы можете контролировать доступ к QuickHelp;</span><span class="sxs-lookup"><span data-stu-id="d62c0-106">You can control in Azure AD who has access to QuickHelp</span></span>
- <span data-ttu-id="d62c0-107">вы можете включить автоматический вход пользователей в QuickHelp (единый вход) под учетной записью Azure AD;</span><span class="sxs-lookup"><span data-stu-id="d62c0-107">You can enable your users to automatically get signed-on to QuickHelp (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d62c0-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="d62c0-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d62c0-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d62c0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d62c0-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d62c0-110">Prerequisites</span></span>

<span data-ttu-id="d62c0-111">Чтобы настроить интеграцию Azure AD с QuickHelp, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="d62c0-111">To configure Azure AD integration with QuickHelp, you need the following items:</span></span>

- <span data-ttu-id="d62c0-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="d62c0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d62c0-113">подписка QuickHelp с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="d62c0-113">A QuickHelp single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d62c0-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="d62c0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d62c0-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="d62c0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d62c0-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="d62c0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d62c0-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d62c0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d62c0-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="d62c0-118">Scenario description</span></span>
<span data-ttu-id="d62c0-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="d62c0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d62c0-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="d62c0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d62c0-121">Добавление QuickHelp из коллекции</span><span class="sxs-lookup"><span data-stu-id="d62c0-121">Adding QuickHelp from the gallery</span></span>
2. <span data-ttu-id="d62c0-122">Настройка и проверка единого входа в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d62c0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-quickhelp-from-the-gallery"></a><span data-ttu-id="d62c0-123">Добавление QuickHelp из коллекции</span><span class="sxs-lookup"><span data-stu-id="d62c0-123">Adding QuickHelp from the gallery</span></span>
<span data-ttu-id="d62c0-124">Чтобы настроить интеграцию QuickHelp с Azure AD, необходимо добавить QuickHelp из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="d62c0-124">To configure the integration of QuickHelp into Azure AD, you need to add QuickHelp from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d62c0-125">**Чтобы добавить QuickHelp из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="d62c0-125">**To add QuickHelp from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d62c0-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d62c0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d62c0-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="d62c0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d62c0-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="d62c0-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="d62c0-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="d62c0-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="d62c0-133">В поле поиска введите **QuickHelp**.</span><span class="sxs-lookup"><span data-stu-id="d62c0-133">In the search box, type **QuickHelp**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_search.png)

5. <span data-ttu-id="d62c0-135">На панели результатов выберите **QuickHelp**, а затем нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="d62c0-135">In the results panel, select **QuickHelp**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d62c0-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="d62c0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d62c0-138">В этом разделе описана настройка и проверка единого входа Azure AD в QuickHelp с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d62c0-138">In this section, you configure and test Azure AD single sign-on with QuickHelp based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d62c0-139">Чтобы единый вход работал, Azure AD необходима информация о том, какой пользователь в QuickHelp соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d62c0-139">For single sign-on to work, Azure AD needs to know what the counterpart user in QuickHelp is to a user in Azure AD.</span></span> <span data-ttu-id="d62c0-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в QuickHelp.</span><span class="sxs-lookup"><span data-stu-id="d62c0-140">In other words, a link relationship between an Azure AD user and the related user in QuickHelp needs to be established.</span></span>

<span data-ttu-id="d62c0-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в QuickHelp.</span><span class="sxs-lookup"><span data-stu-id="d62c0-141">In QuickHelp, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d62c0-142">Чтобы настроить и проверить единый вход Azure AD в QuickHelp, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="d62c0-142">To configure and test Azure AD single sign-on with QuickHelp, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d62c0-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="d62c0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d62c0-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d62c0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d62c0-145">**[Создание тестового пользователя QuickHelp](#creating-a-quickhelp-test-user)** требуется для того, чтобы в QuickHelp существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d62c0-145">**[Creating a QuickHelp test user](#creating-a-quickhelp-test-user)** - to have a counterpart of Britta Simon in QuickHelp that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d62c0-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d62c0-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d62c0-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="d62c0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d62c0-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="d62c0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d62c0-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении QuickHelp.</span><span class="sxs-lookup"><span data-stu-id="d62c0-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your QuickHelp application.</span></span>

<span data-ttu-id="d62c0-150">**Чтобы настроить единый вход Azure AD в QuickHelp, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="d62c0-150">**To configure Azure AD single sign-on with QuickHelp, perform the following steps:**</span></span>

1. <span data-ttu-id="d62c0-151">На портале Azure на странице интеграции с приложением **QuickHelp** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="d62c0-151">In the Azure portal, on the **QuickHelp** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="d62c0-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="d62c0-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_samlbase.png)

3. <span data-ttu-id="d62c0-155">В разделе **Домены и URL-адреса приложения QuickHelp** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="d62c0-155">On the **QuickHelp Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_url.png)

    <span data-ttu-id="d62c0-157">а.</span><span class="sxs-lookup"><span data-stu-id="d62c0-157">a.</span></span> <span data-ttu-id="d62c0-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://quickhelp.com/<instancename>/#/Login`</span><span class="sxs-lookup"><span data-stu-id="d62c0-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://quickhelp.com/<instancename>/#/Login`</span></span>

    <span data-ttu-id="d62c0-159">b.</span><span class="sxs-lookup"><span data-stu-id="d62c0-159">b.</span></span> <span data-ttu-id="d62c0-160">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<subdomain>.quickhelp.com`</span><span class="sxs-lookup"><span data-stu-id="d62c0-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.quickhelp.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d62c0-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="d62c0-161">These values are not real.</span></span> <span data-ttu-id="d62c0-162">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="d62c0-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="d62c0-163">Чтобы получить эти значения, обратитесь к [группе поддержки QuickHelp](https://support.quickhelp.com/).</span><span class="sxs-lookup"><span data-stu-id="d62c0-163">Contact [QuickHelp Client support team](https://support.quickhelp.com/) to get these values.</span></span> 
 
4. <span data-ttu-id="d62c0-164">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="d62c0-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_certificate.png) 

5. <span data-ttu-id="d62c0-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="d62c0-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-quickhelp-tutorial/tutorial_general_400.png) 

6. <span data-ttu-id="d62c0-168">Выполните вход на сайт компании QuickHelp в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="d62c0-168">Sign-on to your QuickHelp company site as administrator.</span></span>

7. <span data-ttu-id="d62c0-169">В верхнем меню щелкните **Администратор**.</span><span class="sxs-lookup"><span data-stu-id="d62c0-169">In the menu on the top, click **Admin**.</span></span>
   
    ![Настройка единого входа][21]

8. <span data-ttu-id="d62c0-171">В меню **QuickHelp Admin** (Администратор QuickHelp) щелкните **Settings** (Параметры).</span><span class="sxs-lookup"><span data-stu-id="d62c0-171">In the **QuickHelp Admin** menu, click **Settings**.</span></span>
   
    ![Настройка единого входа][22]

9. <span data-ttu-id="d62c0-173">Щелкните **Authentication Settings**(Параметра аутентификации).</span><span class="sxs-lookup"><span data-stu-id="d62c0-173">Click **Authentication Settings**.</span></span>

10. <span data-ttu-id="d62c0-174">На странице **Параметры проверки подлинности** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="d62c0-174">On the **Authentication Settings** page, perform the following steps</span></span>
   
    ![Настройка единого входа][23]
   
    <span data-ttu-id="d62c0-176">а.</span><span class="sxs-lookup"><span data-stu-id="d62c0-176">a.</span></span> <span data-ttu-id="d62c0-177">Для параметра **SSO Type** (Тип SSO) выберите значение **WSFederation**.</span><span class="sxs-lookup"><span data-stu-id="d62c0-177">As **SSO Type**, select **WSFederation**.</span></span>
   
    <span data-ttu-id="d62c0-178">b.</span><span class="sxs-lookup"><span data-stu-id="d62c0-178">b.</span></span> <span data-ttu-id="d62c0-179">Чтобы передать скачанный файл метаданных Azure, нажмите кнопку **Browse** (Обзор), перейдите к файлу и щелкните **Upload Metadata** (Передать метаданные).</span><span class="sxs-lookup"><span data-stu-id="d62c0-179">To upload your downloaded Azure metadata file, click **Browse**, navigate to the file, end then click **Upload Metadata**.</span></span>
   
    <span data-ttu-id="d62c0-180">c.</span><span class="sxs-lookup"><span data-stu-id="d62c0-180">c.</span></span> <span data-ttu-id="d62c0-181">В текстовое поле **Email** (Электронная почта) введите `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="d62c0-181">In the **Email** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>
   
    <span data-ttu-id="d62c0-182">г)</span><span class="sxs-lookup"><span data-stu-id="d62c0-182">d.</span></span> <span data-ttu-id="d62c0-183">В текстовое поле **First Name** (Имя) введите `type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span><span class="sxs-lookup"><span data-stu-id="d62c0-183">In the **First Name** textbox, `type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span></span>
   
    <span data-ttu-id="d62c0-184">д.</span><span class="sxs-lookup"><span data-stu-id="d62c0-184">e.</span></span> <span data-ttu-id="d62c0-185">В текстовое поле **Last Name** (Фамилия) введите `type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span><span class="sxs-lookup"><span data-stu-id="d62c0-185">In the **Last Name** textbox, `type http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span></span>
   
    <span data-ttu-id="d62c0-186">f.</span><span class="sxs-lookup"><span data-stu-id="d62c0-186">f.</span></span> <span data-ttu-id="d62c0-187">На **панели действий** щелкните **Save** (Сохранить).</span><span class="sxs-lookup"><span data-stu-id="d62c0-187">In the **Action Bar**, click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="d62c0-188">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="d62c0-188">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d62c0-189">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="d62c0-189">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d62c0-190">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="d62c0-190">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d62c0-191">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="d62c0-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="d62c0-192">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d62c0-192">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="d62c0-194">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="d62c0-194">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d62c0-195">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d62c0-195">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-quickhelp-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d62c0-197">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="d62c0-197">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-quickhelp-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d62c0-199">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="d62c0-199">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-quickhelp-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d62c0-201">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="d62c0-201">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-quickhelp-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d62c0-203">а.</span><span class="sxs-lookup"><span data-stu-id="d62c0-203">a.</span></span> <span data-ttu-id="d62c0-204">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d62c0-204">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d62c0-205">b.</span><span class="sxs-lookup"><span data-stu-id="d62c0-205">b.</span></span> <span data-ttu-id="d62c0-206">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d62c0-206">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d62c0-207">c.</span><span class="sxs-lookup"><span data-stu-id="d62c0-207">c.</span></span> <span data-ttu-id="d62c0-208">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="d62c0-208">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d62c0-209">d.</span><span class="sxs-lookup"><span data-stu-id="d62c0-209">d.</span></span> <span data-ttu-id="d62c0-210">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="d62c0-210">Click **Create**.</span></span>
 
### <a name="creating-a-quickhelp-test-user"></a><span data-ttu-id="d62c0-211">Создание тестового пользователя QuickHelp</span><span class="sxs-lookup"><span data-stu-id="d62c0-211">Creating a QuickHelp test user</span></span>

<span data-ttu-id="d62c0-212">Цель этого раздела — создать пользователя с именем Britta Simon в QuickHelp.</span><span class="sxs-lookup"><span data-stu-id="d62c0-212">The objective of this section is to create a user called Britta Simon in QuickHelp.</span></span>
<span data-ttu-id="d62c0-213">Чтобы единый вход работал, Azure AD необходима информация о том, какой пользователь в QuickHelp соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d62c0-213">For single sign-on to work, Azure AD needs to know what the counterpart user in QuickHelp to a user in Azure AD is.</span></span> <span data-ttu-id="d62c0-214">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в QuickHelp.</span><span class="sxs-lookup"><span data-stu-id="d62c0-214">In other words, a link relationship between an Azure AD user and the related user in QuickHelp needs to be established.</span></span>

<span data-ttu-id="d62c0-215">QuickHelp поддерживает JIT-подготовку.</span><span class="sxs-lookup"><span data-stu-id="d62c0-215">QuickHelp supports just-in-time provisioning.</span></span> <span data-ttu-id="d62c0-216">Это означает, что при необходимости учетная запись пользователя автоматически создается в QuickHelp и связывается с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d62c0-216">This means, if necessary, a user account is automatically created in QuickHelp and the account is linked to the Azure AD account.</span></span>

<span data-ttu-id="d62c0-217">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="d62c0-217">There is no action item for you in this section.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d62c0-218">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="d62c0-218">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d62c0-219">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к QuickHelp.</span><span class="sxs-lookup"><span data-stu-id="d62c0-219">In this section, you enable Britta Simon to use Azure single sign-on by granting access to QuickHelp.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="d62c0-221">**Чтобы назначить пользователя Britta Simon в QuickHelp, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="d62c0-221">**To assign Britta Simon to QuickHelp, perform the following steps:**</span></span>

1. <span data-ttu-id="d62c0-222">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="d62c0-222">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="d62c0-224">В списке приложений выберите **QuickHelp**.</span><span class="sxs-lookup"><span data-stu-id="d62c0-224">In the applications list, select **QuickHelp**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_app.png) 

3. <span data-ttu-id="d62c0-226">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="d62c0-226">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="d62c0-228">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="d62c0-228">Click **Add** button.</span></span> <span data-ttu-id="d62c0-229">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="d62c0-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="d62c0-231">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="d62c0-231">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d62c0-232">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="d62c0-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d62c0-233">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="d62c0-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d62c0-234">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="d62c0-234">Testing single sign-on</span></span>

<span data-ttu-id="d62c0-235">Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="d62c0-235">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  

<span data-ttu-id="d62c0-236">Щелкнув плитку QuickHelp на панели доступа, вы автоматически войдете в приложение QuickHelp.</span><span class="sxs-lookup"><span data-stu-id="d62c0-236">When you click the QuickHelp tile in the Access Panel, you should get automatically signed-on to your QuickHelp application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="d62c0-237">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="d62c0-237">Additional resources</span></span>

* [<span data-ttu-id="d62c0-238">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d62c0-238">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d62c0-239">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d62c0-239">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_general_203.png
[21]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_05.png
[22]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_06.png
[23]: ./media/active-directory-saas-quickhelp-tutorial/tutorial_quickhelp_07.png
