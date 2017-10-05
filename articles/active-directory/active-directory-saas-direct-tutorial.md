---
title: "Учебник. Интеграция Azure Active Directory с Direct | Документы Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и Direct."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7c2cd1f0-d14c-42f0-94a8-9b800008b285
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 84582492592613320bd3ec2bdffe08519852d7c9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-direct"></a><span data-ttu-id="3a3be-103">Учебник. Интеграция Azure Active Directory с Direct</span><span class="sxs-lookup"><span data-stu-id="3a3be-103">Tutorial: Azure Active Directory integration with Direct</span></span>

<span data-ttu-id="3a3be-104">В этом руководстве описано, как интегрировать Direct с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3a3be-104">In this tutorial, you learn how to integrate Direct with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3a3be-105">Интеграция Azure AD с приложением Direct обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="3a3be-105">Integrating Direct with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3a3be-106">С помощью Azure AD вы можете контролировать доступ к Direct.</span><span class="sxs-lookup"><span data-stu-id="3a3be-106">You can control in Azure AD who has access to Direct</span></span>
- <span data-ttu-id="3a3be-107">Вы можете включить автоматический вход пользователей в Direct (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3a3be-107">You can enable your users to automatically get signed-on to Direct (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3a3be-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="3a3be-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="3a3be-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3a3be-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3a3be-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="3a3be-110">Prerequisites</span></span>

<span data-ttu-id="3a3be-111">Чтобы настроить интеграцию Azure AD с Direct, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="3a3be-111">To configure Azure AD integration with Direct, you need the following items:</span></span>

- <span data-ttu-id="3a3be-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="3a3be-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3a3be-113">подписка с поддержкой единого входа Direct.</span><span class="sxs-lookup"><span data-stu-id="3a3be-113">A Direct single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3a3be-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="3a3be-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3a3be-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="3a3be-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3a3be-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="3a3be-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3a3be-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3a3be-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3a3be-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="3a3be-118">Scenario description</span></span>
<span data-ttu-id="3a3be-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="3a3be-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3a3be-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="3a3be-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3a3be-121">Добавление Direct из коллекции</span><span class="sxs-lookup"><span data-stu-id="3a3be-121">Adding Direct from the gallery</span></span>
2. <span data-ttu-id="3a3be-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="3a3be-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-direct-from-the-gallery"></a><span data-ttu-id="3a3be-123">Добавление Direct из коллекции</span><span class="sxs-lookup"><span data-stu-id="3a3be-123">Adding Direct from the gallery</span></span>
<span data-ttu-id="3a3be-124">Чтобы настроить интеграцию Direct с Azure AD, необходимо добавить Direct из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="3a3be-124">To configure the integration of Direct into Azure AD, you need to add Direct from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3a3be-125">**Чтобы добавить Direct из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="3a3be-125">**To add Direct from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3a3be-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3a3be-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3a3be-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="3a3be-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3a3be-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="3a3be-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="3a3be-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="3a3be-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="3a3be-133">В поле поиска введите **Direct**.</span><span class="sxs-lookup"><span data-stu-id="3a3be-133">In the search box, type **Direct**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-direct-tutorial/tutorial_direct_search.png)

5. <span data-ttu-id="3a3be-135">На панели результатов выберите **Direct** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="3a3be-135">In the results panel, select **Direct**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-direct-tutorial/tutorial_direct_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3a3be-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="3a3be-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3a3be-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложение Direct с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3a3be-138">In this section, you configure and test Azure AD single sign-on with Direct based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="3a3be-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Direct соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3a3be-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Direct is to a user in Azure AD.</span></span> <span data-ttu-id="3a3be-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Direct.</span><span class="sxs-lookup"><span data-stu-id="3a3be-140">In other words, a link relationship between an Azure AD user and the related user in Direct needs to be established.</span></span>

<span data-ttu-id="3a3be-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Direct.</span><span class="sxs-lookup"><span data-stu-id="3a3be-141">In Direct, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="3a3be-142">Чтобы настроить и проверить единый вход Azure AD в Direct, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="3a3be-142">To configure and test Azure AD single sign-on with Direct, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3a3be-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="3a3be-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3a3be-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3a3be-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3a3be-145">**[Создание тестового пользователя Direct](#creating-a-direct-test-user)** требуется для создания пользователя Britta Simon в Direct, связанного с соответствующим представлением в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3a3be-145">**[Creating a Direct test user](#creating-a-direct-test-user)** - to have a counterpart of Britta Simon in Direct that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="3a3be-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3a3be-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3a3be-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="3a3be-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3a3be-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="3a3be-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3a3be-149">В этом разделе описано, как включить единый вход Azure AD на новом портале Azure и настроить его в приложении Direct.</span><span class="sxs-lookup"><span data-stu-id="3a3be-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Direct application.</span></span>

<span data-ttu-id="3a3be-150">**Чтобы настроить единый вход Azure AD в Direct, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="3a3be-150">**To configure Azure AD single sign-on with Direct, perform the following steps:**</span></span>

1. <span data-ttu-id="3a3be-151">На портале Azure на странице интеграции с приложением **Direct** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="3a3be-151">In the Azure portal, on the **Direct** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="3a3be-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="3a3be-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-direct-tutorial/tutorial_direct_samlbase.png)

3. <span data-ttu-id="3a3be-155">Если вы хотите настроить приложение в **режиме, инициированном поставщиком удостоверений**, то в разделе **Домены и URL-адреса приложения Direct** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="3a3be-155">On the **Direct Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-direct-tutorial/tutorial_direct_url.png)

    <span data-ttu-id="3a3be-157">В текстовом поле **Идентификатор** введите URL-адрес: `https://direct4b.com/`</span><span class="sxs-lookup"><span data-stu-id="3a3be-157">In the **Identifier** textbox, type the URL: `https://direct4b.com/`</span></span>

4. <span data-ttu-id="3a3be-158">Установите флажок **Показать дополнительные параметры URL-адресов**, если хотите настроить приложение для работы в режиме, инициируемом **поставщиком услуг**:</span><span class="sxs-lookup"><span data-stu-id="3a3be-158">Check **Show advanced URL settings**, If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-direct-tutorial/tutorial_direct_url1.png)

     <span data-ttu-id="3a3be-160">В текстовом поле **URL-адрес для входа** введите URL-адрес: `https://direct4b.com/sso`</span><span class="sxs-lookup"><span data-stu-id="3a3be-160">In the **Sign-on URL** textbox, type the URL: `https://direct4b.com/sso`</span></span> 
    
5. <span data-ttu-id="3a3be-161">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="3a3be-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-direct-tutorial/tutorial_direct_certificate.png) 

6. <span data-ttu-id="3a3be-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="3a3be-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-direct-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="3a3be-165">Чтобы настроить единый вход на стороне **Direct**, отправьте в [службу поддержки Direct](https://direct4b.com/ja/support.html#inquiry) скачанный **XML-файл метаданных**.</span><span class="sxs-lookup"><span data-stu-id="3a3be-165">To configure single sign-on on **Direct** side, you need to send the downloaded **Metadata XML** to [Direct support team](https://direct4b.com/ja/support.html#inquiry).</span></span> 

> [!TIP]
> <span data-ttu-id="3a3be-166">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="3a3be-166">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3a3be-167">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="3a3be-167">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3a3be-168">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="3a3be-168">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3a3be-169">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="3a3be-169">Creating an Azure AD test user</span></span>
<span data-ttu-id="3a3be-170">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3a3be-170">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="3a3be-172">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="3a3be-172">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3a3be-173">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3a3be-173">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-direct-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3a3be-175">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="3a3be-175">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-direct-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3a3be-177">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="3a3be-177">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-direct-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3a3be-179">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="3a3be-179">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-direct-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3a3be-181">а.</span><span class="sxs-lookup"><span data-stu-id="3a3be-181">a.</span></span> <span data-ttu-id="3a3be-182">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3a3be-182">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3a3be-183">b.</span><span class="sxs-lookup"><span data-stu-id="3a3be-183">b.</span></span> <span data-ttu-id="3a3be-184">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="3a3be-184">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3a3be-185">c.</span><span class="sxs-lookup"><span data-stu-id="3a3be-185">c.</span></span> <span data-ttu-id="3a3be-186">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="3a3be-186">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="3a3be-187">d.</span><span class="sxs-lookup"><span data-stu-id="3a3be-187">d.</span></span> <span data-ttu-id="3a3be-188">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="3a3be-188">Click **Create**.</span></span>
 
### <a name="creating-a-direct-test-user"></a><span data-ttu-id="3a3be-189">Создание тестового пользователя Direct</span><span class="sxs-lookup"><span data-stu-id="3a3be-189">Creating a Direct test user</span></span>

<span data-ttu-id="3a3be-190">В этом разделе описано, как создать пользователя Britta Simon в приложении Direct.</span><span class="sxs-lookup"><span data-stu-id="3a3be-190">In this section, you create a user called Britta Simon in Direct.</span></span> <span data-ttu-id="3a3be-191">Обратитесь в [службу поддержки Direct](https://direct4b.com/ja/support.html#inquiry), чтобы добавить пользователей на платформу Direct.</span><span class="sxs-lookup"><span data-stu-id="3a3be-191">Work with [Direct support team](https://direct4b.com/ja/support.html#inquiry) to add the users in the Direct platform.</span></span> <span data-ttu-id="3a3be-192">Перед использованием единого входа необходимо создать и активировать пользователей.</span><span class="sxs-lookup"><span data-stu-id="3a3be-192">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="3a3be-193">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="3a3be-193">Assigning the Azure AD test user</span></span>

<span data-ttu-id="3a3be-194">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure путем предоставления доступа к Direct.</span><span class="sxs-lookup"><span data-stu-id="3a3be-194">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Direct.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="3a3be-196">**Чтобы назначить пользователя Britta Simon в Direct, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="3a3be-196">**To assign Britta Simon to Direct, perform the following steps:**</span></span>

1. <span data-ttu-id="3a3be-197">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="3a3be-197">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="3a3be-199">В списке приложений выберите **Direct**.</span><span class="sxs-lookup"><span data-stu-id="3a3be-199">In the applications list, select **Direct**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-direct-tutorial/tutorial_direct_app.png) 

3. <span data-ttu-id="3a3be-201">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="3a3be-201">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="3a3be-203">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="3a3be-203">Click **Add** button.</span></span> <span data-ttu-id="3a3be-204">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="3a3be-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="3a3be-206">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="3a3be-206">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3a3be-207">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="3a3be-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3a3be-208">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="3a3be-208">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3a3be-209">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="3a3be-209">Testing single sign-on</span></span>

<span data-ttu-id="3a3be-210">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="3a3be-210">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

1. <span data-ttu-id="3a3be-211">Если вы хотите протестировать в **режиме, инициируемом поставщиком удостоверений**:</span><span class="sxs-lookup"><span data-stu-id="3a3be-211">If you wish to test in **IDP Initiated Mode**:</span></span>

    <span data-ttu-id="3a3be-212">Щелкнув элемент **Direct** на панели доступа, вы автоматически войдете в приложение **Direct**.</span><span class="sxs-lookup"><span data-stu-id="3a3be-212">When you click the **Direct** tile in the Access Panel, you should get automatically signed-on to your **Direct** application.</span></span>

2. <span data-ttu-id="3a3be-213">Если вы хотите протестировать в **режиме, инициируемом поставщиком услуг**:</span><span class="sxs-lookup"><span data-stu-id="3a3be-213">If you wish to test in **SP Initiated Mode**:</span></span>
    
    <span data-ttu-id="3a3be-214">а.</span><span class="sxs-lookup"><span data-stu-id="3a3be-214">a.</span></span> <span data-ttu-id="3a3be-215">Щелкните элемент **Direct** на панели доступа, и вы будете перенаправлены на страницу входа приложения.</span><span class="sxs-lookup"><span data-stu-id="3a3be-215">Click on the **Direct** tile in the Access Panel and you will be redirected to the application sign-on page.</span></span>

    <span data-ttu-id="3a3be-216">b.</span><span class="sxs-lookup"><span data-stu-id="3a3be-216">b.</span></span> <span data-ttu-id="3a3be-217">Введите свой `subdomain` в отображаемом текстовом поле и нажмите клавишу "次へ (Далее)"; вы автоматически войдете в приложение **Direct**.</span><span class="sxs-lookup"><span data-stu-id="3a3be-217">Input your `subdomain` in the textbox displayed and press '次へ (Next)' and you should get automatically signed-on to your **Direct** application .</span></span>
    
<span data-ttu-id="3a3be-218">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3a3be-218">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3a3be-219">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="3a3be-219">Additional resources</span></span>

* [<span data-ttu-id="3a3be-220">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3a3be-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3a3be-221">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3a3be-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-direct-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-direct-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-direct-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-direct-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-direct-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-direct-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-direct-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-direct-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-direct-tutorial/tutorial_general_203.png

