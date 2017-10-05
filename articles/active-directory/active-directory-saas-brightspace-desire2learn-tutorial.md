---
title: "Руководство. Интеграция Azure Active Directory с Brightspace (разработка Desire2Learn) | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в Brightspace by Desire2Learn."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e2d3065b-1f6c-4c45-af78-0d5da3266999
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 7076b476ba71c5d94ae4728e5f6032b0d7e047ad
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-brightspace-by-desire2learn"></a><span data-ttu-id="e45d7-103">Руководство. Интеграция Azure Active Directory с Brightspace (разработка Desire2Learn)</span><span class="sxs-lookup"><span data-stu-id="e45d7-103">Tutorial: Azure Active Directory integration with Brightspace by Desire2Learn</span></span>

<span data-ttu-id="e45d7-104">В этом руководстве описано, как интегрировать Azure Active Directory (Azure AD) с приложением Brightspace by Desire2Learn.</span><span class="sxs-lookup"><span data-stu-id="e45d7-104">In this tutorial, you learn how to integrate Brightspace by Desire2Learn with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e45d7-105">Интеграция Brightspace by Desire2Learn с Azure AD дает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="e45d7-105">Integrating Brightspace by Desire2Learn with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e45d7-106">С помощью Azure AD вы можете контролировать доступ к Brightspace by Desire2Learn.</span><span class="sxs-lookup"><span data-stu-id="e45d7-106">You can control in Azure AD who has access to Brightspace by Desire2Learn</span></span>
- <span data-ttu-id="e45d7-107">Вы можете включить автоматический вход пользователей в Brightspace by Desire2Learn (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e45d7-107">You can enable your users to automatically get signed-on to Brightspace by Desire2Learn (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e45d7-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="e45d7-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e45d7-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e45d7-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e45d7-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="e45d7-110">Prerequisites</span></span>

<span data-ttu-id="e45d7-111">Чтобы настроить интеграцию Azure AD с Brightspace by Desire2Learn, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="e45d7-111">To configure Azure AD integration with Brightspace by Desire2Learn, you need the following items:</span></span>

- <span data-ttu-id="e45d7-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="e45d7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e45d7-113">Подписка с поддержкой единого входа Brightspace (разработка Desire2Learn)</span><span class="sxs-lookup"><span data-stu-id="e45d7-113">A Brightspace by Desire2Learn single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e45d7-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="e45d7-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e45d7-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="e45d7-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e45d7-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="e45d7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e45d7-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e45d7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e45d7-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="e45d7-118">Scenario description</span></span>
<span data-ttu-id="e45d7-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="e45d7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e45d7-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="e45d7-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e45d7-121">Добавление Brightspace by Desire2Learn из коллекции</span><span class="sxs-lookup"><span data-stu-id="e45d7-121">Adding Brightspace by Desire2Learn from the gallery</span></span>
2. <span data-ttu-id="e45d7-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="e45d7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-brightspace-by-desire2learn-from-the-gallery"></a><span data-ttu-id="e45d7-123">Добавление Brightspace by Desire2Learn из коллекции</span><span class="sxs-lookup"><span data-stu-id="e45d7-123">Adding Brightspace by Desire2Learn from the gallery</span></span>
<span data-ttu-id="e45d7-124">Чтобы настроить интеграцию Brightspace by Desire2Learn с Azure AD, необходимо добавить Brightspace by Desire2Learn из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="e45d7-124">To configure the integration of Brightspace by Desire2Learn into Azure AD, you need to add Brightspace by Desire2Learn from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e45d7-125">**Чтобы добавить Brightspace by Desire2Learn из коллекции, сделайте следующее.**</span><span class="sxs-lookup"><span data-stu-id="e45d7-125">**To add Brightspace by Desire2Learn from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e45d7-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e45d7-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e45d7-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="e45d7-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e45d7-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="e45d7-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="e45d7-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="e45d7-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="e45d7-133">В поле поиска введите **Brightspace by Desire2Learn**.</span><span class="sxs-lookup"><span data-stu-id="e45d7-133">In the search box, type **Brightspace by Desire2Learn**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_brightspacebydesire2learn_search.png)

5. <span data-ttu-id="e45d7-135">На панели результатов выберите **Brightspace by Desire2Learn** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="e45d7-135">In the results panel, select **Brightspace by Desire2Learn**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_brightspacebydesire2learn_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e45d7-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="e45d7-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e45d7-138">В этом разделе описана настройка и проверка единого входа Azure AD в Brightspace by Desire2Learn с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e45d7-138">In this section, you configure and test Azure AD single sign-on with Brightspace by Desire2Learn based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e45d7-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Brightspace by Desire2Learn соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e45d7-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Brightspace by Desire2Learn is to a user in Azure AD.</span></span> <span data-ttu-id="e45d7-140">Иными словами, нужно установить связь между пользователем Azure AD и соответствующим пользователем в Brightspace by Desire2Learn.</span><span class="sxs-lookup"><span data-stu-id="e45d7-140">In other words, a link relationship between an Azure AD user and the related user in Brightspace by Desire2Learn needs to be established.</span></span>

<span data-ttu-id="e45d7-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Brightspace by Desire2Learn.</span><span class="sxs-lookup"><span data-stu-id="e45d7-141">In Brightspace by Desire2Learn, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e45d7-142">Чтобы настроить и проверить единый вход Azure AD в Brightspace by Desire2Learn, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="e45d7-142">To configure and test Azure AD single sign-on with Brightspace by Desire2Learn, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e45d7-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="e45d7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e45d7-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e45d7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e45d7-145">**[Создание тестового пользователя Brightspace by Desire2Learn](#creating-a-brightspace-by-desire2learn-test-user)** нужно для того, чтобы в Brightspace by Desire2Learn также существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e45d7-145">**[Creating a Brightspace by Desire2Learn test user](#creating-a-brightspace-by-desire2learn-test-user)** - to have a counterpart of Britta Simon in Brightspace by Desire2Learn that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e45d7-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e45d7-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e45d7-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="e45d7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e45d7-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="e45d7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e45d7-149">В данном разделе описано, как включить единый вход в Azure AD на портале Azure и настроить его в приложении Brightspace by Desire2Learn.</span><span class="sxs-lookup"><span data-stu-id="e45d7-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Brightspace by Desire2Learn application.</span></span>

<span data-ttu-id="e45d7-150">**Чтобы настроить единый вход Azure AD в Brightspace by Desire2Learn, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="e45d7-150">**To configure Azure AD single sign-on with Brightspace by Desire2Learn, perform the following steps:**</span></span>

1. <span data-ttu-id="e45d7-151">На портале Azure на странице интеграции с приложением **Brightspace by Desire2Learn** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="e45d7-151">In the Azure portal, on the **Brightspace by Desire2Learn** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="e45d7-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="e45d7-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_brightspacebydesire2learn_samlbase.png)

3. <span data-ttu-id="e45d7-155">В разделе **Домены и URL-адреса приложения Brightspace by Desire2Learn** сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="e45d7-155">On the **Brightspace by Desire2Learn Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_brightspacebydesire2learn_url.png)

    <span data-ttu-id="e45d7-157">а.</span><span class="sxs-lookup"><span data-stu-id="e45d7-157">a.</span></span> <span data-ttu-id="e45d7-158">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="e45d7-158">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.tenants.brightspace.com/samlLogin`|
    | `https://<companyname>.desire2learn.com/shibboleth-sp`|

    <span data-ttu-id="e45d7-159">b.</span><span class="sxs-lookup"><span data-stu-id="e45d7-159">b.</span></span> <span data-ttu-id="e45d7-160">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате: `https://<companyname>.desire2learn.com/d2l/lp/auth/login/samlLogin.d2l`.</span><span class="sxs-lookup"><span data-stu-id="e45d7-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.desire2learn.com/d2l/lp/auth/login/samlLogin.d2l`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e45d7-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="e45d7-161">These values are not real.</span></span> <span data-ttu-id="e45d7-162">Измените их на фактические значения идентификатора и URL-адреса ответа.</span><span class="sxs-lookup"><span data-stu-id="e45d7-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="e45d7-163">Чтобы получить эти значения, обратитесь к [группе поддержки Brightspace by Desire2Learn](https://www.d2l.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="e45d7-163">Contact [Brightspace by Desire2Learn support team](https://www.d2l.com/contact/) to get these values.</span></span>
 


4. <span data-ttu-id="e45d7-164">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="e45d7-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_brightspacebydesire2learn_certificate.png) 

5. <span data-ttu-id="e45d7-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="e45d7-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e45d7-168">Чтобы настроить единый вход на стороне **Brightspace by Desire2Learn**, необходимо отправить скачанный **XML-файл метаданных** [группе поддержки Brightspace by Desire2Learn](https://www.d2l.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="e45d7-168">To configure single sign-on on **Brightspace by Desire2Learn** side, you need to send the downloaded **Metadata XML** to [Brightspace by Desire2Learn support team](https://www.d2l.com/contact/).</span></span>

> [!TIP]
> <span data-ttu-id="e45d7-169">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="e45d7-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e45d7-170">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="e45d7-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e45d7-171">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="e45d7-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e45d7-172">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="e45d7-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="e45d7-173">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e45d7-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="e45d7-175">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="e45d7-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e45d7-176">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e45d7-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-brightspace-desire2learn-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e45d7-178">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="e45d7-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-brightspace-desire2learn-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e45d7-180">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="e45d7-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-brightspace-desire2learn-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e45d7-182">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="e45d7-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-brightspace-desire2learn-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e45d7-184">а.</span><span class="sxs-lookup"><span data-stu-id="e45d7-184">a.</span></span> <span data-ttu-id="e45d7-185">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e45d7-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e45d7-186">b.</span><span class="sxs-lookup"><span data-stu-id="e45d7-186">b.</span></span> <span data-ttu-id="e45d7-187">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e45d7-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e45d7-188">c.</span><span class="sxs-lookup"><span data-stu-id="e45d7-188">c.</span></span> <span data-ttu-id="e45d7-189">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="e45d7-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e45d7-190">d.</span><span class="sxs-lookup"><span data-stu-id="e45d7-190">d.</span></span> <span data-ttu-id="e45d7-191">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="e45d7-191">Click **Create**.</span></span>
 
### <a name="creating-a-brightspace-by-desire2learn-test-user"></a><span data-ttu-id="e45d7-192">Создание тестового пользователя Brightspace by Desire2Learn</span><span class="sxs-lookup"><span data-stu-id="e45d7-192">Creating a Brightspace by Desire2Learn test user</span></span>

<span data-ttu-id="e45d7-193">Чтобы пользователи Azure AD могли выполнить вход в Brightspace (разработка Desire2Learn), они должны быть подготовлены для Brightspace (разработка Desire2Learn).</span><span class="sxs-lookup"><span data-stu-id="e45d7-193">In order to enable Azure AD users to log into Brightspace by Desire2Learn, they must be provisioned into Brightspace by Desire2Learn.</span></span>  

<span data-ttu-id="e45d7-194">В случае Brightspace by Desire2Learn учетные записи пользователей должны создаваться [группой поддержки Brightspace by Desire2Learn](https://www.d2l.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="e45d7-194">In the case of Brightspace by Desire2Learn, the user accounts need to be created by your [Brightspace by Desire2Learn support team](https://www.d2l.com/contact/).</span></span>

>[!NOTE]
><span data-ttu-id="e45d7-195">Вы можете использовать любые другие средства создания учетной записи пользователя Brightspace (разработка Desire2Learn) или API, предоставляемые Brightspace (разработка Desire2Learn) для подготовки учетных записей пользователя Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e45d7-195">You can use any other Brightspace by Desire2Learn user account creation tools or APIs provided by Brightspace by Desire2Learn to provision Azure Active Directory user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e45d7-196">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="e45d7-196">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e45d7-197">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к Brightspace by Desire2Learn.</span><span class="sxs-lookup"><span data-stu-id="e45d7-197">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Brightspace by Desire2Learn.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="e45d7-199">**Чтобы назначить пользователя Britta Simon в Brightspace by Desire2Learn, сделайте следующее.**</span><span class="sxs-lookup"><span data-stu-id="e45d7-199">**To assign Britta Simon to Brightspace by Desire2Learn, perform the following steps:**</span></span>

1. <span data-ttu-id="e45d7-200">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="e45d7-200">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="e45d7-202">Из списка приложений выберите **Brightspace by Desire2Learn**.</span><span class="sxs-lookup"><span data-stu-id="e45d7-202">In the applications list, select **Brightspace by Desire2Learn**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_brightspacebydesire2learn_app.png) 

3. <span data-ttu-id="e45d7-204">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="e45d7-204">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="e45d7-206">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="e45d7-206">Click **Add** button.</span></span> <span data-ttu-id="e45d7-207">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="e45d7-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="e45d7-209">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="e45d7-209">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e45d7-210">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="e45d7-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e45d7-211">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="e45d7-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e45d7-212">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="e45d7-212">Testing single sign-on</span></span>

<span data-ttu-id="e45d7-213">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="e45d7-213">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e45d7-214">Щелкнув элемент "Brightspace by Desire2Learn" на панели доступа, вы автоматически войдете в приложение Brightspace by Desire2Learn.</span><span class="sxs-lookup"><span data-stu-id="e45d7-214">When you click the Brightspace by Desire2Learn tile in the Access Panel, you should get automatically signed-on to your Brightspace by Desire2Learn application.</span></span>
<span data-ttu-id="e45d7-215">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e45d7-215">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e45d7-216">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="e45d7-216">Additional resources</span></span>

* [<span data-ttu-id="e45d7-217">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e45d7-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e45d7-218">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e45d7-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-brightspace-desire2learn-tutorial/tutorial_general_203.png

