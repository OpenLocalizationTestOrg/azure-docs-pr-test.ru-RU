---
title: "Руководство по интеграции Azure Active Directory с приложением CS Stars | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и CS Stars."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5704d151-afb8-40a4-b286-8bacd4f279ee
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: jeedes
ms.openlocfilehash: acc9160f86e58c7af4779a8bab5627dc5c5ad721
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cs-stars"></a><span data-ttu-id="f10ae-103">Руководство. Интеграция Azure Active Directory с CS Stars</span><span class="sxs-lookup"><span data-stu-id="f10ae-103">Tutorial: Azure Active Directory integration with CS Stars</span></span>

<span data-ttu-id="f10ae-104">В этом учебнике описано, как интегрировать приложение CS Stars с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f10ae-104">In this tutorial, you learn how to integrate CS Stars with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f10ae-105">Интеграция Azure AD с приложением CS Stars обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="f10ae-105">Integrating CS Stars with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f10ae-106">С помощью Azure AD вы можете контролировать доступ к CS Stars.</span><span class="sxs-lookup"><span data-stu-id="f10ae-106">You can control in Azure AD who has access to CS Stars</span></span>
- <span data-ttu-id="f10ae-107">Вы можете включить автоматический вход пользователей в CS Stars (единый вход) под учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f10ae-107">You can enable your users to automatically get signed-on to CS Stars (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f10ae-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="f10ae-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f10ae-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f10ae-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f10ae-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="f10ae-110">Prerequisites</span></span>

<span data-ttu-id="f10ae-111">Чтобы настроить интеграцию Azure AD с CS Stars, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="f10ae-111">To configure Azure AD integration with CS Stars, you need the following items:</span></span>

- <span data-ttu-id="f10ae-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="f10ae-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f10ae-113">подписка CS Stars с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="f10ae-113">A CS Stars single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f10ae-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="f10ae-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f10ae-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="f10ae-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f10ae-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="f10ae-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f10ae-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f10ae-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f10ae-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="f10ae-118">Scenario description</span></span>
<span data-ttu-id="f10ae-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="f10ae-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f10ae-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="f10ae-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f10ae-121">Добавление CS Stars из коллекции</span><span class="sxs-lookup"><span data-stu-id="f10ae-121">Adding CS Stars from the gallery</span></span>
2. <span data-ttu-id="f10ae-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="f10ae-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cs-stars-from-the-gallery"></a><span data-ttu-id="f10ae-123">Добавление CS Stars из коллекции</span><span class="sxs-lookup"><span data-stu-id="f10ae-123">Adding CS Stars from the gallery</span></span>
<span data-ttu-id="f10ae-124">Чтобы настроить интеграцию CS Stars с Azure AD, необходимо добавить CS Stars из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="f10ae-124">To configure the integration of CS Stars into Azure AD, you need to add CS Stars from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f10ae-125">**Чтобы добавить CS Stars из коллекции, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="f10ae-125">**To add CS Stars from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f10ae-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f10ae-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f10ae-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="f10ae-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f10ae-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="f10ae-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="f10ae-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="f10ae-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="f10ae-133">В поле поиска введите **CS Stars**.</span><span class="sxs-lookup"><span data-stu-id="f10ae-133">In the search box, type **CS Stars**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cs-stars-tutorial/tutorial_csstars_search.png)

5. <span data-ttu-id="f10ae-135">На панели результатов выберите **CS Stars** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="f10ae-135">In the results panel, select **CS Stars**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cs-stars-tutorial/tutorial_csstars_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f10ae-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="f10ae-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f10ae-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложение CS Stars для тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f10ae-138">In this section, you configure and test Azure AD single sign-on with CS Stars based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f10ae-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в CS Stars соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f10ae-139">For single sign-on to work, Azure AD needs to know what the counterpart user in CS Stars is to a user in Azure AD.</span></span> <span data-ttu-id="f10ae-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в CS Stars.</span><span class="sxs-lookup"><span data-stu-id="f10ae-140">In other words, a link relationship between an Azure AD user and the related user in CS Stars needs to be established.</span></span>

<span data-ttu-id="f10ae-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в CS Stars.</span><span class="sxs-lookup"><span data-stu-id="f10ae-141">In CS Stars, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f10ae-142">Чтобы настроить и проверить единый вход Azure AD в CS Stars, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="f10ae-142">To configure and test Azure AD single sign-on with CS Stars, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f10ae-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="f10ae-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f10ae-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f10ae-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f10ae-145">**[Создание тестового пользователя CS Stars](#creating-a-cs-stars-test-user)** требуется для создания пользователя Britta Simon в CS Stars, связанного с представлением этого пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f10ae-145">**[Creating a CS Stars test user](#creating-a-cs-stars-test-user)** - to have a counterpart of Britta Simon in CS Stars that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f10ae-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f10ae-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f10ae-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="f10ae-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f10ae-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="f10ae-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f10ae-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении CS Stars.</span><span class="sxs-lookup"><span data-stu-id="f10ae-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your CS Stars application.</span></span>

<span data-ttu-id="f10ae-150">**Чтобы настроить единый вход Azure AD в CS Stars, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="f10ae-150">**To configure Azure AD single sign-on with CS Stars, perform the following steps:**</span></span>

1. <span data-ttu-id="f10ae-151">На портале Azure на странице интеграции с приложением **CS Stars** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="f10ae-151">In the Azure portal, on the **CS Stars** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="f10ae-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="f10ae-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-cs-stars-tutorial/tutorial_csstars_samlbase.png)

3. <span data-ttu-id="f10ae-155">В разделе **Домены и URL-адреса CS Stars** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="f10ae-155">On the **CS Stars Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-cs-stars-tutorial/tutorial_csstars_url.png)

    <span data-ttu-id="f10ae-157">а.</span><span class="sxs-lookup"><span data-stu-id="f10ae-157">a.</span></span> <span data-ttu-id="f10ae-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<subdomain>.csstars.com/enterprise/default.cmdx?ssoclient=<uniqueid>`</span><span class="sxs-lookup"><span data-stu-id="f10ae-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.csstars.com/enterprise/default.cmdx?ssoclient=<uniqueid>`</span></span>

    <span data-ttu-id="f10ae-159">b.</span><span class="sxs-lookup"><span data-stu-id="f10ae-159">b.</span></span> <span data-ttu-id="f10ae-160">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<subdomain>.csstars.com/enterprise/`</span><span class="sxs-lookup"><span data-stu-id="f10ae-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.csstars.com/enterprise/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f10ae-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="f10ae-161">These values are not real.</span></span> <span data-ttu-id="f10ae-162">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="f10ae-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="f10ae-163">Чтобы получить эти значения, обратитесь в [службу поддержки клиентов CS Stars](http://www.marshclearsight.com/support/).</span><span class="sxs-lookup"><span data-stu-id="f10ae-163">Contact [CS Stars Client support team](http://www.marshclearsight.com/support/) to get these values.</span></span> 
 
4. <span data-ttu-id="f10ae-164">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="f10ae-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-cs-stars-tutorial/tutorial_csstars_certificate.png) 

5. <span data-ttu-id="f10ae-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="f10ae-166">Click **Save** button.</span></span>

    <span data-ttu-id="f10ae-167">![Настройка единого входа](./media/active-directory-saas-cs-stars-tutorial/tutorial_general_400.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="f10ae-167">![Configure Single Sign-On](./media/active-directory-saas-cs-stars-tutorial/tutorial_general_400.png) 
<CS></span></span>
6. <span data-ttu-id="f10ae-168">Чтобы настроить единый вход на стороне **CS Stars**, отправьте в [службу поддержки CS Stars](http://www.marshclearsight.com/support/) скачанный **XML-файл метаданных**.</span><span class="sxs-lookup"><span data-stu-id="f10ae-168">To configure single sign-on on **CS Stars** side, you need to send the downloaded **Metadata XML** to [CS Stars support team](http://www.marshclearsight.com/support/).</span></span> 
<CE>

> [!TIP]
> <span data-ttu-id="f10ae-169">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="f10ae-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f10ae-170">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="f10ae-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f10ae-171">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="f10ae-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f10ae-172">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="f10ae-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="f10ae-173">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f10ae-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="f10ae-175">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="f10ae-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f10ae-176">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f10ae-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cs-stars-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f10ae-178">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="f10ae-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cs-stars-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f10ae-180">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="f10ae-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cs-stars-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f10ae-182">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="f10ae-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cs-stars-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f10ae-184">а.</span><span class="sxs-lookup"><span data-stu-id="f10ae-184">a.</span></span> <span data-ttu-id="f10ae-185">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f10ae-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f10ae-186">b.</span><span class="sxs-lookup"><span data-stu-id="f10ae-186">b.</span></span> <span data-ttu-id="f10ae-187">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f10ae-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f10ae-188">c.</span><span class="sxs-lookup"><span data-stu-id="f10ae-188">c.</span></span> <span data-ttu-id="f10ae-189">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="f10ae-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f10ae-190">d.</span><span class="sxs-lookup"><span data-stu-id="f10ae-190">d.</span></span> <span data-ttu-id="f10ae-191">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="f10ae-191">Click **Create**.</span></span>
 
### <a name="creating-a-cs-stars-test-user"></a><span data-ttu-id="f10ae-192">Создание тестового пользователя CS Stars</span><span class="sxs-lookup"><span data-stu-id="f10ae-192">Creating a CS Stars test user</span></span>

<span data-ttu-id="f10ae-193">Цель этого раздела — создать пользователя с именем Britta Simon в CS Stars.</span><span class="sxs-lookup"><span data-stu-id="f10ae-193">The objective of this section is to create a user called Britta Simon in CS Stars.</span></span>

<span data-ttu-id="f10ae-194">Чтобы создать пользователя в CS Stars, обратитесь в [службу поддержки CS Stars](http://www.marshclearsight.com/support/).</span><span class="sxs-lookup"><span data-stu-id="f10ae-194">To get a user created in CS Stars, you need to contact your [CS Stars support team](http://www.marshclearsight.com/support/).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f10ae-195">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="f10ae-195">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f10ae-196">В этом разделе описано, как включить единый вход Azure для пользователя Britta Simon, предоставив этому пользователю доступ к CS Stars.</span><span class="sxs-lookup"><span data-stu-id="f10ae-196">In this section, you enable Britta Simon to use Azure single sign-on by granting access to CS Stars.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="f10ae-198">**Чтобы назначить пользователя Britta Simon в CS Stars, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="f10ae-198">**To assign Britta Simon to CS Stars, perform the following steps:**</span></span>

1. <span data-ttu-id="f10ae-199">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="f10ae-199">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="f10ae-201">В списке приложений выберите **CS Stars**.</span><span class="sxs-lookup"><span data-stu-id="f10ae-201">In the applications list, select **CS Stars**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-cs-stars-tutorial/tutorial_csstars_app.png) 

3. <span data-ttu-id="f10ae-203">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="f10ae-203">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="f10ae-205">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="f10ae-205">Click **Add** button.</span></span> <span data-ttu-id="f10ae-206">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="f10ae-206">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="f10ae-208">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="f10ae-208">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f10ae-209">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="f10ae-209">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f10ae-210">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="f10ae-210">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f10ae-211">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="f10ae-211">Testing single sign-on</span></span>

<span data-ttu-id="f10ae-212">Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="f10ae-212">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="f10ae-213">Щелкнув элемент CS Stars на панели доступа, вы автоматически войдете в приложение CS Stars.</span><span class="sxs-lookup"><span data-stu-id="f10ae-213">When you click the CS Stars tile in the Access Panel, you should get automatically signed-on to your CS Stars application.</span></span>
 

## <a name="additional-resources"></a><span data-ttu-id="f10ae-214">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="f10ae-214">Additional resources</span></span>

* [<span data-ttu-id="f10ae-215">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f10ae-215">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f10ae-216">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f10ae-216">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-cs-stars-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cs-stars-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cs-stars-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cs-stars-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cs-stars-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cs-stars-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cs-stars-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cs-stars-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cs-stars-tutorial/tutorial_general_203.png

