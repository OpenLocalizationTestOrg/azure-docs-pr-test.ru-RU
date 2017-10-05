---
title: "Руководство по интеграции Azure Active Directory с Degreed | Документы Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и Degreed."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1eda2d1c-b5e2-4c53-ad46-bbeb91cd119a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: ea96edb25e2d7199981ff126bf4b2a3d93c6840a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-degreed"></a><span data-ttu-id="52dbb-103">Учебник. Интеграция Azure Active Directory с Degreed</span><span class="sxs-lookup"><span data-stu-id="52dbb-103">Tutorial: Azure Active Directory integration with Degreed</span></span>

<span data-ttu-id="52dbb-104">В этом руководстве описано, как интегрировать Degreed с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="52dbb-104">In this tutorial, you learn how to integrate Degreed with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="52dbb-105">Интеграция Azure AD с приложением Degreed обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="52dbb-105">Integrating Degreed with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="52dbb-106">С помощью Azure AD вы можете контролировать доступ к Degreed.</span><span class="sxs-lookup"><span data-stu-id="52dbb-106">You can control in Azure AD who has access to Degreed</span></span>
- <span data-ttu-id="52dbb-107">Вы можете включить автоматический вход пользователей в Degreed (единый вход) с использованием учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="52dbb-107">You can enable your users to automatically get signed-on to Degreed (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="52dbb-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="52dbb-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="52dbb-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="52dbb-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="52dbb-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="52dbb-110">Prerequisites</span></span>

<span data-ttu-id="52dbb-111">Чтобы настроить интеграцию Azure AD с Degreed, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="52dbb-111">To configure Azure AD integration with Degreed, you need the following items:</span></span>

- <span data-ttu-id="52dbb-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="52dbb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="52dbb-113">подписка Degreed с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="52dbb-113">A Degreed single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="52dbb-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="52dbb-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="52dbb-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="52dbb-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="52dbb-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="52dbb-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="52dbb-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="52dbb-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="52dbb-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="52dbb-118">Scenario description</span></span>
<span data-ttu-id="52dbb-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="52dbb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="52dbb-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="52dbb-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="52dbb-121">Добавление Degreed из коллекции</span><span class="sxs-lookup"><span data-stu-id="52dbb-121">Adding Degreed from the gallery</span></span>
2. <span data-ttu-id="52dbb-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="52dbb-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-degreed-from-the-gallery"></a><span data-ttu-id="52dbb-123">Добавление Degreed из коллекции</span><span class="sxs-lookup"><span data-stu-id="52dbb-123">Adding Degreed from the gallery</span></span>
<span data-ttu-id="52dbb-124">Чтобы настроить интеграцию Degreed с Azure AD, необходимо добавить Degreed из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="52dbb-124">To configure the integration of Degreed into Azure AD, you need to add Degreed from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="52dbb-125">**Чтобы добавить Degreed из коллекции, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="52dbb-125">**To add Degreed from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="52dbb-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="52dbb-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="52dbb-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="52dbb-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="52dbb-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="52dbb-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="52dbb-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="52dbb-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="52dbb-133">В поле поиска введите **Degreed**.</span><span class="sxs-lookup"><span data-stu-id="52dbb-133">In the search box, type **Degreed**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-degreed-tutorial/tutorial_degreed_search.png)

5. <span data-ttu-id="52dbb-135">На панели результатов выберите **Degreed** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="52dbb-135">In the results panel, select **Degreed**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-degreed-tutorial/tutorial_degreed_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="52dbb-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="52dbb-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="52dbb-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложение Degreed для тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="52dbb-138">In this section, you configure and test Azure AD single sign-on with Degreed based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="52dbb-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Degreed соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="52dbb-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Degreed is to a user in Azure AD.</span></span> <span data-ttu-id="52dbb-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Degreed.</span><span class="sxs-lookup"><span data-stu-id="52dbb-140">In other words, a link relationship between an Azure AD user and the related user in Degreed needs to be established.</span></span>

<span data-ttu-id="52dbb-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Degreed.</span><span class="sxs-lookup"><span data-stu-id="52dbb-141">In Degreed, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="52dbb-142">Чтобы настроить и проверить единый вход Azure AD в Degreed, вам потребуется выполнить действия в указанных далее стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="52dbb-142">To configure and test Azure AD single sign-on with Degreed, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="52dbb-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы позволить пользователям использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="52dbb-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="52dbb-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="52dbb-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="52dbb-145">**[Создание тестового пользователя Degreed](#creating-a-degreed-test-user)** требуется для создания пользователя Britta Simon в Degreed, связанного с представлением этого пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="52dbb-145">**[Creating a Degreed test user](#creating-a-degreed-test-user)** - to have a counterpart of Britta Simon in Degreed that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="52dbb-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="52dbb-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="52dbb-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="52dbb-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="52dbb-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="52dbb-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="52dbb-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Degreed.</span><span class="sxs-lookup"><span data-stu-id="52dbb-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Degreed application.</span></span>

<span data-ttu-id="52dbb-150">**Чтобы настроить единый вход Azure AD в Degreed, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="52dbb-150">**To configure Azure AD single sign-on with Degreed, perform the following steps:**</span></span>

1. <span data-ttu-id="52dbb-151">На портале Azure на странице интеграции с приложением **Degreed** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="52dbb-151">In the Azure portal, on the **Degreed** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="52dbb-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="52dbb-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-degreed-tutorial/tutorial_degreed_samlbase.png)

3. <span data-ttu-id="52dbb-155">В разделе **Домены и URL-адреса Degreed** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="52dbb-155">On the **Degreed Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-degreed-tutorial/tutorial_degreed_url.png)

    <span data-ttu-id="52dbb-157">а.</span><span class="sxs-lookup"><span data-stu-id="52dbb-157">a.</span></span> <span data-ttu-id="52dbb-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://degreed.com/?orgsso=<company code>`</span><span class="sxs-lookup"><span data-stu-id="52dbb-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://degreed.com/?orgsso=<company code>`</span></span>

    <span data-ttu-id="52dbb-159">b.</span><span class="sxs-lookup"><span data-stu-id="52dbb-159">b.</span></span> <span data-ttu-id="52dbb-160">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://degreed.com/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="52dbb-160">In the **Identifier** textbox, type a URL using the following pattern: `https://degreed.com/<instancename>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="52dbb-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="52dbb-161">These values are not real.</span></span> <span data-ttu-id="52dbb-162">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="52dbb-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="52dbb-163">Чтобы получить эти значения, обратитесь в [службу поддержки клиентов Degreed](mailTo:admin@degreed.com).</span><span class="sxs-lookup"><span data-stu-id="52dbb-163">Contact [Degreed Client support team](mailTo:admin@degreed.com) to get these values.</span></span> 
 


4. <span data-ttu-id="52dbb-164">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="52dbb-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-degreed-tutorial/tutorial_degreed_certificate.png) 

5. <span data-ttu-id="52dbb-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="52dbb-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-degreed-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="52dbb-168">Чтобы настроить единый вход на стороне **Degreed**, отправьте в [службу поддержки Degreed](mailTo:admin@degreed.com) скачанный **XML-файл метаданных**.</span><span class="sxs-lookup"><span data-stu-id="52dbb-168">To configure single sign-on on **Degreed** side, you need to send the downloaded **Metadata XML** to [Degreed support team](mailTo:admin@degreed.com).</span></span> <span data-ttu-id="52dbb-169">Специалисты службы поддержки настроят подключение единого входа SAML на обеих сторонах подключения.</span><span class="sxs-lookup"><span data-stu-id="52dbb-169">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="52dbb-170">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="52dbb-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="52dbb-171">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="52dbb-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="52dbb-172">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="52dbb-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="52dbb-173">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="52dbb-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="52dbb-174">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="52dbb-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="52dbb-176">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="52dbb-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="52dbb-177">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="52dbb-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-degreed-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="52dbb-179">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="52dbb-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-degreed-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="52dbb-181">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="52dbb-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-degreed-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="52dbb-183">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="52dbb-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-degreed-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="52dbb-185">а.</span><span class="sxs-lookup"><span data-stu-id="52dbb-185">a.</span></span> <span data-ttu-id="52dbb-186">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="52dbb-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="52dbb-187">b.</span><span class="sxs-lookup"><span data-stu-id="52dbb-187">b.</span></span> <span data-ttu-id="52dbb-188">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="52dbb-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="52dbb-189">c.</span><span class="sxs-lookup"><span data-stu-id="52dbb-189">c.</span></span> <span data-ttu-id="52dbb-190">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="52dbb-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="52dbb-191">d.</span><span class="sxs-lookup"><span data-stu-id="52dbb-191">d.</span></span> <span data-ttu-id="52dbb-192">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="52dbb-192">Click **Create**.</span></span>
 
### <a name="creating-a-degreed-test-user"></a><span data-ttu-id="52dbb-193">Создание тестового пользователя Degreed</span><span class="sxs-lookup"><span data-stu-id="52dbb-193">Creating a Degreed test user</span></span>

<span data-ttu-id="52dbb-194">Цель этого раздела — создать пользователя с именем Britta Simon в Degreed.</span><span class="sxs-lookup"><span data-stu-id="52dbb-194">The objective of this section is to create a user called Britta Simon in Degreed.</span></span> <span data-ttu-id="52dbb-195">Приложение Degreed поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="52dbb-195">Degreed supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="52dbb-196">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="52dbb-196">There is no action item for you in this section.</span></span> <span data-ttu-id="52dbb-197">Новый пользователь будет создан при попытке получить доступ к приложению Degreed (если он еще не создан).</span><span class="sxs-lookup"><span data-stu-id="52dbb-197">A new user is created during an attempt to access Degreed if it doesn't exist yet.</span></span>

> [!NOTE]
> <span data-ttu-id="52dbb-198">Чтобы создать пользователя вручную, необходимо обратиться в [службу поддержки Degreed](mailTo:admin@degreed.com).</span><span class="sxs-lookup"><span data-stu-id="52dbb-198">If you need to create a user manually, you need to contact the [Degreed support team](mailTo:admin@degreed.com).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="52dbb-199">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="52dbb-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="52dbb-200">В этом разделе описано, как включить единый вход Azure для пользователя Britta Simon, предоставив этому пользователю доступ к Degreed.</span><span class="sxs-lookup"><span data-stu-id="52dbb-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Degreed.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="52dbb-202">**Чтобы назначить пользователя Britta Simon в Degreed, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="52dbb-202">**To assign Britta Simon to Degreed, perform the following steps:**</span></span>

1. <span data-ttu-id="52dbb-203">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="52dbb-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="52dbb-205">В списке приложений выберите **Degreed**.</span><span class="sxs-lookup"><span data-stu-id="52dbb-205">In the applications list, select **Degreed**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-degreed-tutorial/tutorial_degreed_app.png) 

3. <span data-ttu-id="52dbb-207">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="52dbb-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="52dbb-209">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="52dbb-209">Click **Add** button.</span></span> <span data-ttu-id="52dbb-210">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="52dbb-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="52dbb-212">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="52dbb-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="52dbb-213">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="52dbb-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="52dbb-214">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="52dbb-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="52dbb-215">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="52dbb-215">Testing single sign-on</span></span>

<span data-ttu-id="52dbb-216">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="52dbb-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="52dbb-217">Щелкнув элемент Degreed на панели доступа, вы автоматически войдете в приложение Degreed.</span><span class="sxs-lookup"><span data-stu-id="52dbb-217">When you click the Degreed tile in the Access Panel, you should get automatically signed-on to your Degreed application.</span></span>
<span data-ttu-id="52dbb-218">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="52dbb-218">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="52dbb-219">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="52dbb-219">Additional resources</span></span>

* [<span data-ttu-id="52dbb-220">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="52dbb-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="52dbb-221">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="52dbb-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-degreed-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-degreed-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-degreed-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-degreed-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-degreed-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-degreed-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-degreed-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-degreed-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-degreed-tutorial/tutorial_general_203.png

