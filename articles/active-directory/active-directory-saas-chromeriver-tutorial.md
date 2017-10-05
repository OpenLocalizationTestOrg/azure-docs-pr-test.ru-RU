---
title: "Учебник. Интеграция Azure Active Directory с Chromeriver | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в Chromeriver."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 445c5600-e340-4724-a9cb-3cfaf5770b70
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: jeedes
ms.openlocfilehash: 6ee3316a8258ee27e4fa4ec22badbf4fe047a844
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-chromeriver"></a><span data-ttu-id="ed7ba-103">Руководство. Интеграция Azure Active Directory с Chromeriver</span><span class="sxs-lookup"><span data-stu-id="ed7ba-103">Tutorial: Azure Active Directory integration with Chromeriver</span></span>

<span data-ttu-id="ed7ba-104">В этом руководстве описано, как интегрировать Chromeriver с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ed7ba-104">In this tutorial, you learn how to integrate Chromeriver with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ed7ba-105">Интеграция Chromeriver с Azure AD обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="ed7ba-105">Integrating Chromeriver with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ed7ba-106">С помощью Azure AD вы можете контролировать доступ к Chromeriver.</span><span class="sxs-lookup"><span data-stu-id="ed7ba-106">You can control in Azure AD who has access to Chromeriver</span></span>
- <span data-ttu-id="ed7ba-107">Вы можете включить автоматический вход пользователей в Chromeriver (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ed7ba-107">You can enable your users to automatically get signed-on to Chromeriver (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ed7ba-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="ed7ba-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ed7ba-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ed7ba-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ed7ba-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ed7ba-110">Prerequisites</span></span>

<span data-ttu-id="ed7ba-111">Чтобы настроить интеграцию Azure AD с Chromeriver, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="ed7ba-111">To configure Azure AD integration with Chromeriver, you need the following items:</span></span>

- <span data-ttu-id="ed7ba-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="ed7ba-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ed7ba-113">подписка Chromeriver с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="ed7ba-113">A Chromeriver single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ed7ba-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="ed7ba-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ed7ba-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="ed7ba-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ed7ba-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="ed7ba-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ed7ba-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ed7ba-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ed7ba-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="ed7ba-118">Scenario description</span></span>
<span data-ttu-id="ed7ba-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="ed7ba-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ed7ba-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="ed7ba-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ed7ba-121">Добавление Chromeriver из коллекции</span><span class="sxs-lookup"><span data-stu-id="ed7ba-121">Adding Chromeriver from the gallery</span></span>
2. <span data-ttu-id="ed7ba-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ed7ba-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-chromeriver-from-the-gallery"></a><span data-ttu-id="ed7ba-123">Добавление Chromeriver из коллекции</span><span class="sxs-lookup"><span data-stu-id="ed7ba-123">Adding Chromeriver from the gallery</span></span>
<span data-ttu-id="ed7ba-124">Чтобы настроить интеграцию Chromeriver с Azure AD, необходимо добавить Chromeriver из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="ed7ba-124">To configure the integration of Chromeriver into Azure AD, you need to add Chromeriver from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ed7ba-125">**Чтобы добавить Chromeriver из коллекции, сделайте следующее.**</span><span class="sxs-lookup"><span data-stu-id="ed7ba-125">**To add Chromeriver from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ed7ba-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ed7ba-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ed7ba-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="ed7ba-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ed7ba-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="ed7ba-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="ed7ba-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="ed7ba-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="ed7ba-133">В поле поиска введите **Chromeriver**.</span><span class="sxs-lookup"><span data-stu-id="ed7ba-133">In the search box, type **Chromeriver**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-chromeriver-tutorial/tutorial_chromeriver_search.png)

5. <span data-ttu-id="ed7ba-135">На панели результатов выберите **Chromeriver** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="ed7ba-135">In the results panel, select **Chromeriver**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-chromeriver-tutorial/tutorial_chromeriver_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ed7ba-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ed7ba-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ed7ba-138">В этом разделе описана настройка и проверка единого входа Azure AD в Chromeriver с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ed7ba-138">In this section, you configure and test Azure AD single sign-on with Chromeriver based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ed7ba-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Chromeriver соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ed7ba-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Chromeriver is to a user in Azure AD.</span></span> <span data-ttu-id="ed7ba-140">Иными словами, необходимо установить связь между пользователям Azure AD и соответствующим пользователем в Chromeriver.</span><span class="sxs-lookup"><span data-stu-id="ed7ba-140">In other words, a link relationship between an Azure AD user and the related user in Chromeriver needs to be established.</span></span>

<span data-ttu-id="ed7ba-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Chromeriver.</span><span class="sxs-lookup"><span data-stu-id="ed7ba-141">In Chromeriver, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="ed7ba-142">Чтобы настроить и проверить единый вход Azure AD в Chromeriver, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="ed7ba-142">To configure and test Azure AD single sign-on with Chromeriver, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ed7ba-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="ed7ba-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ed7ba-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ed7ba-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ed7ba-145">**[Создание тестового пользователя Chromeriver](#creating-a-chromeriver-test-user)** нужно для того, чтобы в Chromeriver также существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ed7ba-145">**[Creating a Chromeriver test user](#creating-a-chromeriver-test-user)** - to have a counterpart of Britta Simon in Chromeriver that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ed7ba-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ed7ba-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ed7ba-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="ed7ba-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ed7ba-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ed7ba-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ed7ba-149">В этом разделе описано, как включить единый вход Azure AD на новом портале Azure и настроить его в приложении Chromeriver.</span><span class="sxs-lookup"><span data-stu-id="ed7ba-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Chromeriver application.</span></span>

<span data-ttu-id="ed7ba-150">**Чтобы настроить единый вход Azure AD в Chromeriver, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="ed7ba-150">**To configure Azure AD single sign-on with Chromeriver, perform the following steps:**</span></span>

1. <span data-ttu-id="ed7ba-151">На портале Azure на странице интеграции с приложением **Chromeriver** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="ed7ba-151">In the Azure portal, on the **Chromeriver** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="ed7ba-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="ed7ba-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-chromeriver-tutorial/tutorial_chromeriver_samlbase.png)

3. <span data-ttu-id="ed7ba-155">В разделе **Домены и URL-адреса приложения Chromeriver** сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="ed7ba-155">On the **Chromeriver Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-chromeriver-tutorial/tutorial_chromeriver_url.png)

    <span data-ttu-id="ed7ba-157">а.</span><span class="sxs-lookup"><span data-stu-id="ed7ba-157">a.</span></span> <span data-ttu-id="ed7ba-158">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<subdomain>.chromeriver.com`</span><span class="sxs-lookup"><span data-stu-id="ed7ba-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.chromeriver.com`</span></span>

    <span data-ttu-id="ed7ba-159">b.</span><span class="sxs-lookup"><span data-stu-id="ed7ba-159">b.</span></span> <span data-ttu-id="ed7ba-160">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате: `https://<subdomain>.chromeriver.com/login/sso/saml/consume?customerId=<uniqueid>`.</span><span class="sxs-lookup"><span data-stu-id="ed7ba-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.chromeriver.com/login/sso/saml/consume?customerId=<uniqueid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ed7ba-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="ed7ba-161">These values are not real.</span></span> <span data-ttu-id="ed7ba-162">Измените их на фактические значения идентификатора и URL-адреса ответа.</span><span class="sxs-lookup"><span data-stu-id="ed7ba-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="ed7ba-163">Чтобы получить эти значения, обратитесь к [группе поддержки Chromeriver](https://www.chromeriver.com/services/support).</span><span class="sxs-lookup"><span data-stu-id="ed7ba-163">Contact [Chromeriver support team](https://www.chromeriver.com/services/support) to get these values.</span></span>
 


4. <span data-ttu-id="ed7ba-164">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="ed7ba-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-chromeriver-tutorial/tutorial_chromeriver_certificate.png) 

5. <span data-ttu-id="ed7ba-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="ed7ba-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-chromeriver-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ed7ba-168">Чтобы настроить единый вход на стороне **Chromeriver**, отправьте скачанный **XML-файл метаданных** [группе поддержки Chromeriver](https://www.chromeriver.com/services/support).</span><span class="sxs-lookup"><span data-stu-id="ed7ba-168">To configure single sign-on on **Chromeriver** side, you need to send the downloaded **Metadata XML** to [Chromeriver support team](https://www.chromeriver.com/services/support).</span></span> <span data-ttu-id="ed7ba-169">Как только единый вход для вашей подписки будет включен, вы получите уведомление.</span><span class="sxs-lookup"><span data-stu-id="ed7ba-169">You will get a notification when SSO has been enabled for your subscription.</span></span>

> [!TIP]
> <span data-ttu-id="ed7ba-170">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="ed7ba-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ed7ba-171">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="ed7ba-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ed7ba-172">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="ed7ba-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ed7ba-173">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="ed7ba-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="ed7ba-174">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ed7ba-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="ed7ba-176">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="ed7ba-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ed7ba-177">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ed7ba-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-chromeriver-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ed7ba-179">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="ed7ba-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-chromeriver-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ed7ba-181">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="ed7ba-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-chromeriver-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ed7ba-183">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="ed7ba-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-chromeriver-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ed7ba-185">а.</span><span class="sxs-lookup"><span data-stu-id="ed7ba-185">a.</span></span> <span data-ttu-id="ed7ba-186">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ed7ba-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ed7ba-187">b.</span><span class="sxs-lookup"><span data-stu-id="ed7ba-187">b.</span></span> <span data-ttu-id="ed7ba-188">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ed7ba-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ed7ba-189">c.</span><span class="sxs-lookup"><span data-stu-id="ed7ba-189">c.</span></span> <span data-ttu-id="ed7ba-190">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="ed7ba-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ed7ba-191">d.</span><span class="sxs-lookup"><span data-stu-id="ed7ba-191">d.</span></span> <span data-ttu-id="ed7ba-192">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="ed7ba-192">Click **Create**.</span></span>
 
### <a name="creating-a-chromeriver-test-user"></a><span data-ttu-id="ed7ba-193">Создание тестового пользователя Chromeriver</span><span class="sxs-lookup"><span data-stu-id="ed7ba-193">Creating a Chromeriver test user</span></span>

<span data-ttu-id="ed7ba-194">Чтобы пользователи Azure AD могли выполнить вход в Chromeriver, они должны быть подготовлены в Chromeriver.</span><span class="sxs-lookup"><span data-stu-id="ed7ba-194">To enable Azure AD users to log in to Chromeriver, they must be provisioned into Chromeriver.</span></span>  

<span data-ttu-id="ed7ba-195">В случае Chromeriver учетные записи пользователей должны быть созданы [группой поддержки Chromeriver](https://www.chromeriver.com/services/support).</span><span class="sxs-lookup"><span data-stu-id="ed7ba-195">In the case of Chromeriver, the user accounts need to be created by your [Chromeriver support team](https://www.chromeriver.com/services/support).</span></span>

>[!NOTE]
><span data-ttu-id="ed7ba-196">Вы можете использовать любые другие инструменты создания учетных записей пользователя Chromeriver или API, предоставляемые Chromeriver для подготовки учетных записей пользователя Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ed7ba-196">You can use any other Chromeriver user account creation tools or APIs provided by Chromeriver to provision Azure Active Directory user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ed7ba-197">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="ed7ba-197">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ed7ba-198">В этом разделе описано, как позволить пользователю Britta Simon использовать единый вход Azure, предоставив ему доступ к Chromeriver.</span><span class="sxs-lookup"><span data-stu-id="ed7ba-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Chromeriver.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="ed7ba-200">**Чтобы назначить пользователя Britta Simon в Chromeriver, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="ed7ba-200">**To assign Britta Simon to Chromeriver, perform the following steps:**</span></span>

1. <span data-ttu-id="ed7ba-201">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="ed7ba-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="ed7ba-203">Из списка приложений выберите **Chromeriver**.</span><span class="sxs-lookup"><span data-stu-id="ed7ba-203">In the applications list, select **Chromeriver**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-chromeriver-tutorial/tutorial_chromeriver_app.png) 

3. <span data-ttu-id="ed7ba-205">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="ed7ba-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="ed7ba-207">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="ed7ba-207">Click **Add** button.</span></span> <span data-ttu-id="ed7ba-208">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="ed7ba-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="ed7ba-210">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="ed7ba-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ed7ba-211">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="ed7ba-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ed7ba-212">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="ed7ba-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ed7ba-213">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="ed7ba-213">Testing single sign-on</span></span>

<span data-ttu-id="ed7ba-214">Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="ed7ba-214">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ed7ba-215">Щелкнув элемент "Chromeriver" на панели доступа, вы автоматически войдете в приложение Chromeriver.</span><span class="sxs-lookup"><span data-stu-id="ed7ba-215">When you click the Chromeriver tile in the Access Panel, you should get automatically signed-on to your Chromeriver application.</span></span> <span data-ttu-id="ed7ba-216">Дополнительные сведения о панели доступа можно найти в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ed7ba-216">For more details about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ed7ba-217">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="ed7ba-217">Additional resources</span></span>

* [<span data-ttu-id="ed7ba-218">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ed7ba-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ed7ba-219">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ed7ba-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-chromeriver-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-chromeriver-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-chromeriver-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-chromeriver-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-chromeriver-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-chromeriver-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-chromeriver-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-chromeriver-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-chromeriver-tutorial/tutorial_general_203.png

