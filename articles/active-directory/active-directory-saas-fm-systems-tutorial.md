---
title: "Руководство по интеграции Azure Active Directory с FM:Systems | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и FM:Systems."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f78c58c5-6e98-458b-8991-78624a245665
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: 3a597d228f6c9234ec2fd2644ec3ac50b98f3b6b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-fmsystems"></a><span data-ttu-id="990ee-103">Руководство по интеграции Azure Active Directory с FM:Systems</span><span class="sxs-lookup"><span data-stu-id="990ee-103">Tutorial: Azure Active Directory integration with FM:Systems</span></span>

<span data-ttu-id="990ee-104">В этом учебнике описано, как интегрировать FM:Systems с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="990ee-104">In this tutorial, you learn how to integrate FM:Systems with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="990ee-105">Интеграция FM:Systems с Azure AD обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="990ee-105">Integrating FM:Systems with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="990ee-106">Вы сможете контролировать доступ к FM:Systems с помощью Azure AD</span><span class="sxs-lookup"><span data-stu-id="990ee-106">You can control in Azure AD who has access to FM:Systems</span></span>
- <span data-ttu-id="990ee-107">Вы можете включить автоматический вход пользователей в FM:Systems (единый вход) с учетной записью Azure AD</span><span class="sxs-lookup"><span data-stu-id="990ee-107">You can enable your users to automatically get signed-on to FM:Systems (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="990ee-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="990ee-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="990ee-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="990ee-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="990ee-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="990ee-110">Prerequisites</span></span>

<span data-ttu-id="990ee-111">Чтобы настроить интеграцию Azure AD с FM:Systems, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="990ee-111">To configure Azure AD integration with FM:Systems, you need the following items:</span></span>

- <span data-ttu-id="990ee-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="990ee-112">An Azure AD subscription</span></span>
- <span data-ttu-id="990ee-113">подписка FM:Systems с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="990ee-113">An FM:Systems single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="990ee-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="990ee-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="990ee-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="990ee-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="990ee-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="990ee-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="990ee-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="990ee-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="990ee-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="990ee-118">Scenario description</span></span>
<span data-ttu-id="990ee-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="990ee-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="990ee-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="990ee-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="990ee-121">Добавление FM:Systems из коллекции</span><span class="sxs-lookup"><span data-stu-id="990ee-121">Adding FM:Systems from the gallery</span></span>
2. <span data-ttu-id="990ee-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="990ee-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-fmsystems-from-the-gallery"></a><span data-ttu-id="990ee-123">Добавление FM:Systems из коллекции</span><span class="sxs-lookup"><span data-stu-id="990ee-123">Adding FM:Systems from the gallery</span></span>
<span data-ttu-id="990ee-124">Чтобы настроить интеграцию FM:Systems с Azure AD, необходимо добавить FM:Systems из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="990ee-124">To configure the integration of FM:Systems into Azure AD, you need to add FM:Systems from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="990ee-125">**Чтобы добавить FM:Systems из коллекции, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="990ee-125">**To add FM:Systems from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="990ee-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="990ee-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="990ee-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="990ee-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="990ee-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="990ee-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="990ee-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="990ee-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="990ee-133">В поле поиска введите **FM:Systems**.</span><span class="sxs-lookup"><span data-stu-id="990ee-133">In the search box, type **FM:Systems**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_search.png)

5. <span data-ttu-id="990ee-135">На панели результатов выберите **FM:Systems** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="990ee-135">In the results panel, select **FM:Systems**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="990ee-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="990ee-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="990ee-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложение FM:Systems для тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="990ee-138">In this section, you configure and test Azure AD single sign-on with FM:Systems based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="990ee-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в FM:Systems соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="990ee-139">For single sign-on to work, Azure AD needs to know what the counterpart user in FM:Systems is to a user in Azure AD.</span></span> <span data-ttu-id="990ee-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в FM:Systems.</span><span class="sxs-lookup"><span data-stu-id="990ee-140">In other words, a link relationship between an Azure AD user and the related user in FM:Systems needs to be established.</span></span>

<span data-ttu-id="990ee-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в FM:Systems.</span><span class="sxs-lookup"><span data-stu-id="990ee-141">In FM:Systems, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="990ee-142">Чтобы настроить и проверить единый вход Azure AD в FM:Systems, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="990ee-142">To configure and test Azure AD single sign-on with FM:Systems, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="990ee-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="990ee-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="990ee-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="990ee-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="990ee-145">**[Создание тестового пользователя FM:Systems](#creating-an-fmsystems-test-user)** требуется для создания пользователя Britta Simon в FM:Systems, связанного с представлением этого пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="990ee-145">**[Creating an FM:Systems test user](#creating-an-fmsystems-test-user)** - to have a counterpart of Britta Simon in FM:Systems that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="990ee-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="990ee-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="990ee-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="990ee-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="990ee-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="990ee-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="990ee-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении FM:Systems.</span><span class="sxs-lookup"><span data-stu-id="990ee-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your FM:Systems application.</span></span>

<span data-ttu-id="990ee-150">**Чтобы настроить единый вход Azure AD в FM:Systems, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="990ee-150">**To configure Azure AD single sign-on with FM:Systems, perform the following steps:**</span></span>

1. <span data-ttu-id="990ee-151">На портале Azure на странице интеграции с приложением **FM:Systems** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="990ee-151">In the Azure portal, on the **FM:Systems** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="990ee-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="990ee-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_samlbase.png)

3. <span data-ttu-id="990ee-155">В разделе **Домены и URL-адреса FM:Systems** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="990ee-155">On the **FM:Systems Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_url.png)

    <span data-ttu-id="990ee-157">В текстовом поле **URL-адрес ответа** введите **URL-адрес ответа** FM:Systems в следующем формате: `https://<companyname>.fmshosted.com/fminteract/ConsumerService2.aspx`.</span><span class="sxs-lookup"><span data-stu-id="990ee-157">In the **Reply URL** textbox, type your FM:Systems **Reply URL**, type the URL using the following pattern: `https://<companyname>.fmshosted.com/fminteract/ConsumerService2.aspx`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="990ee-158">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="990ee-158">This value is not real.</span></span> <span data-ttu-id="990ee-159">Вместо него нужно указать фактический URL-адрес ответа.</span><span class="sxs-lookup"><span data-stu-id="990ee-159">Update this value with the actual Reply URL.</span></span> <span data-ttu-id="990ee-160">Чтобы получить это значение, обратитесь в [службу поддержки FM:Systems](https://fmsystems.com/ask-us/).</span><span class="sxs-lookup"><span data-stu-id="990ee-160">Contact [FM:Systems support team](https://fmsystems.com/ask-us/) to get this value.</span></span>
 
4. <span data-ttu-id="990ee-161">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="990ee-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_certificate.png) 

5. <span data-ttu-id="990ee-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="990ee-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-fm-systems-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="990ee-165">Чтобы настроить единый вход на стороне **FM:Systems**, отправьте в [службу поддержки FM:Systems](https://fmsystems.com/ask-us/) скачанный **XML-файл метаданных**.</span><span class="sxs-lookup"><span data-stu-id="990ee-165">To configure single sign-on on **FM:Systems** side, you need to send the downloaded **Metadata XML** to [FM:Systems support team](https://fmsystems.com/ask-us/).</span></span> <span data-ttu-id="990ee-166">Специалисты службы поддержки настроят подключение единого входа SAML на обеих сторонах подключения.</span><span class="sxs-lookup"><span data-stu-id="990ee-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span> <span data-ttu-id="990ee-167">Как только единый вход для вашей подписки будет включен, вы получите уведомление.</span><span class="sxs-lookup"><span data-stu-id="990ee-167">You will get a notification when SSO has been enabled for your subscription.</span></span>

> [!TIP]
> <span data-ttu-id="990ee-168">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="990ee-168">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="990ee-169">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="990ee-169">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="990ee-170">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="990ee-170">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="990ee-171">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="990ee-171">Creating an Azure AD test user</span></span>
<span data-ttu-id="990ee-172">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="990ee-172">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="990ee-174">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="990ee-174">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="990ee-175">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="990ee-175">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-fm-systems-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="990ee-177">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="990ee-177">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-fm-systems-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="990ee-179">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="990ee-179">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-fm-systems-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="990ee-181">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="990ee-181">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-fm-systems-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="990ee-183">а.</span><span class="sxs-lookup"><span data-stu-id="990ee-183">a.</span></span> <span data-ttu-id="990ee-184">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="990ee-184">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="990ee-185">b.</span><span class="sxs-lookup"><span data-stu-id="990ee-185">b.</span></span> <span data-ttu-id="990ee-186">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="990ee-186">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="990ee-187">c.</span><span class="sxs-lookup"><span data-stu-id="990ee-187">c.</span></span> <span data-ttu-id="990ee-188">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="990ee-188">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="990ee-189">d.</span><span class="sxs-lookup"><span data-stu-id="990ee-189">d.</span></span> <span data-ttu-id="990ee-190">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="990ee-190">Click **Create**.</span></span>
 
### <a name="creating-an-fmsystems-test-user"></a><span data-ttu-id="990ee-191">Создание тестового пользователя FM:Systems</span><span class="sxs-lookup"><span data-stu-id="990ee-191">Creating an FM:Systems test user</span></span>

1. <span data-ttu-id="990ee-192">В другом окне веб-браузера войдите на ваш корпоративный веб-сайт FM: Systems в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="990ee-192">In a web browser window, log into your FM:Systems company site as an administrator.</span></span>

2. <span data-ttu-id="990ee-193">Последовательно выберите **System Administration \> Manage Security \> Users \> User list** (Системное администрирование > Управление безопасностью > Пользователи > Список пользователей).</span><span class="sxs-lookup"><span data-stu-id="990ee-193">Go to **System Administration \> Manage Security \> Users \> User list**.</span></span>
   
    <span data-ttu-id="990ee-194">![Администрирование системы](./media/active-directory-saas-fm-systems-tutorial/ic795905.png "Администрирование системы")</span><span class="sxs-lookup"><span data-stu-id="990ee-194">![System Administration](./media/active-directory-saas-fm-systems-tutorial/ic795905.png "System Administration")</span></span>

3. <span data-ttu-id="990ee-195">Нажмите **Создать нового пользователя**.</span><span class="sxs-lookup"><span data-stu-id="990ee-195">Click **Create new user**.</span></span>
   
    <span data-ttu-id="990ee-196">![Создание пользователя](./media/active-directory-saas-fm-systems-tutorial/ic795906.png "Создание пользователя")</span><span class="sxs-lookup"><span data-stu-id="990ee-196">![Create New User](./media/active-directory-saas-fm-systems-tutorial/ic795906.png "Create New User")</span></span>

4. <span data-ttu-id="990ee-197">В разделе **Создание пользователя** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="990ee-197">In the **Create User** section, perform the following steps:</span></span>
   
    <span data-ttu-id="990ee-198">![Создание пользователя](./media/active-directory-saas-fm-systems-tutorial/ic795907.png "Создание пользователя")</span><span class="sxs-lookup"><span data-stu-id="990ee-198">![Create User](./media/active-directory-saas-fm-systems-tutorial/ic795907.png "Create User")</span></span>
   
    <span data-ttu-id="990ee-199">а.</span><span class="sxs-lookup"><span data-stu-id="990ee-199">a.</span></span> <span data-ttu-id="990ee-200">В текстовых полях **Имя пользователя**, **Пароль**, **Подтверждение пароля**, **Адрес электронной почты** и **Идентификатор сотрудника** введите соответствующие данные для действующей учетной записи Azure Active Directory, которую хотите подготовить.</span><span class="sxs-lookup"><span data-stu-id="990ee-200">Type the **UserName**, the **Password**, **Confirm Password**, **E-mail** and the **Employee ID** of a valid Azure Active Directory account you want to provision into the related textboxes.</span></span>
   
    <span data-ttu-id="990ee-201">b.</span><span class="sxs-lookup"><span data-stu-id="990ee-201">b.</span></span> <span data-ttu-id="990ee-202">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="990ee-202">Click **Next**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="990ee-203">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="990ee-203">Assigning the Azure AD test user</span></span>

<span data-ttu-id="990ee-204">В этом разделе описано, как включить единый вход Azure для пользователя Britta Simon, предоставив этому пользователю доступ к FM:Systems.</span><span class="sxs-lookup"><span data-stu-id="990ee-204">In this section, you enable Britta Simon to use Azure single sign-on by granting access to FM:Systems.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="990ee-206">**Чтобы назначить пользователя Britta Simon в FM:Systems, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="990ee-206">**To assign Britta Simon to FM:Systems, perform the following steps:**</span></span>

1. <span data-ttu-id="990ee-207">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="990ee-207">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="990ee-209">В списке приложений выберите **FM:Systems**.</span><span class="sxs-lookup"><span data-stu-id="990ee-209">In the applications list, select **FM:Systems**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-fm-systems-tutorial/tutorial_fmsystems_app.png) 

3. <span data-ttu-id="990ee-211">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="990ee-211">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="990ee-213">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="990ee-213">Click **Add** button.</span></span> <span data-ttu-id="990ee-214">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="990ee-214">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="990ee-216">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="990ee-216">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="990ee-217">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="990ee-217">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="990ee-218">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="990ee-218">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="990ee-219">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="990ee-219">Testing single sign-on</span></span>

<span data-ttu-id="990ee-220">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="990ee-220">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="990ee-221">Щелкнув элемент FM:Systems на панели доступа, вы автоматически войдете в приложение FM:Systems.</span><span class="sxs-lookup"><span data-stu-id="990ee-221">When you click the FM:Systems tile in the Access Panel, you should get automatically signed-on to your FM:Systems application.</span></span>
<span data-ttu-id="990ee-222">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="990ee-222">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="990ee-223">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="990ee-223">Additional resources</span></span>

* [<span data-ttu-id="990ee-224">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="990ee-224">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="990ee-225">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="990ee-225">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-fm-systems-tutorial/tutorial_general_203.png

