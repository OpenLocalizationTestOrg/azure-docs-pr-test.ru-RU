---
title: "Учебник. Интеграция Azure Active Directory с Intralinks | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в Intralinks."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 147f2bf9-166b-402e-adc4-4b19dd336883
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: ee7fd5b88ac806104002ffb41af11bab4fd1b2dc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-intralinks"></a><span data-ttu-id="ff68d-103">Руководство. Интеграция Azure Active Directory с Intralinks</span><span class="sxs-lookup"><span data-stu-id="ff68d-103">Tutorial: Azure Active Directory integration with Intralinks</span></span>

<span data-ttu-id="ff68d-104">В этом руководстве описано, как интегрировать Intralinks с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ff68d-104">In this tutorial, you learn how to integrate Intralinks with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ff68d-105">Интеграция Azure AD с приложением Intralinks обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="ff68d-105">Integrating Intralinks with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ff68d-106">С помощью Azure AD вы можете контролировать доступ к Intralinks.</span><span class="sxs-lookup"><span data-stu-id="ff68d-106">You can control in Azure AD who has access to Intralinks</span></span>
- <span data-ttu-id="ff68d-107">Вы можете включить автоматический вход пользователей в Intralinks (единый вход) с использованием учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ff68d-107">You can enable your users to automatically get signed-on to Intralinks (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ff68d-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="ff68d-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ff68d-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ff68d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ff68d-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ff68d-110">Prerequisites</span></span>

<span data-ttu-id="ff68d-111">Чтобы настроить интеграцию Azure AD с Intralinks, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="ff68d-111">To configure Azure AD integration with Intralinks, you need the following items:</span></span>

- <span data-ttu-id="ff68d-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="ff68d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ff68d-113">подписка Intralinks с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="ff68d-113">An Intralinks single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ff68d-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="ff68d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ff68d-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="ff68d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ff68d-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="ff68d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ff68d-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ff68d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ff68d-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="ff68d-118">Scenario description</span></span>
<span data-ttu-id="ff68d-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="ff68d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ff68d-120">Сценарий, описанный в этом руководстве, состоит из двух стандартных блоков.</span><span class="sxs-lookup"><span data-stu-id="ff68d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ff68d-121">Добавление Intralinks из коллекции.</span><span class="sxs-lookup"><span data-stu-id="ff68d-121">Adding Intralinks from the gallery</span></span>
2. <span data-ttu-id="ff68d-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ff68d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-intralinks-from-the-gallery"></a><span data-ttu-id="ff68d-123">Добавление Intralinks из коллекции.</span><span class="sxs-lookup"><span data-stu-id="ff68d-123">Adding Intralinks from the gallery</span></span>
<span data-ttu-id="ff68d-124">Чтобы настроить интеграцию Intralinks с Azure AD, необходимо добавить Intralinks из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="ff68d-124">To configure the integration of Intralinks into Azure AD, you need to add Intralinks from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ff68d-125">**Чтобы добавить Intralinks из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="ff68d-125">**To add Intralinks from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ff68d-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ff68d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ff68d-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="ff68d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ff68d-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="ff68d-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="ff68d-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="ff68d-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="ff68d-133">В поле поиска введите **Intralinks**.</span><span class="sxs-lookup"><span data-stu-id="ff68d-133">In the search box, type **Intralinks**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_search.png)

5. <span data-ttu-id="ff68d-135">На панели результатов выберите **Intralinks** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="ff68d-135">In the results panel, select **Intralinks**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ff68d-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ff68d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ff68d-138">В этом разделе описана настройка и проверка единого входа Azure AD в Intralinks с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ff68d-138">In this section, you configure and test Azure AD single sign-on with Intralinks based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ff68d-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Intralinks соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ff68d-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Intralinks is to a user in Azure AD.</span></span> <span data-ttu-id="ff68d-140">Иными словами, необходимо установить связь между пользователям Azure AD и соответствующим пользователем в Intralinks.</span><span class="sxs-lookup"><span data-stu-id="ff68d-140">In other words, a link relationship between an Azure AD user and the related user in Intralinks needs to be established.</span></span>

<span data-ttu-id="ff68d-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Intralinks.</span><span class="sxs-lookup"><span data-stu-id="ff68d-141">In Intralinks, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="ff68d-142">Чтобы настроить и проверить единый вход Azure AD в Intralinks, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="ff68d-142">To configure and test Azure AD single sign-on with Intralinks, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ff68d-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="ff68d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ff68d-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ff68d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ff68d-145">**[Создание тестового пользователя Intralinks](#creating-an-intralinks-test-user)** требуется для того, чтобы в Intralinks существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ff68d-145">**[Creating an Intralinks test user](#creating-an-intralinks-test-user)** - to have a counterpart of Britta Simon in Intralinks that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ff68d-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ff68d-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ff68d-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="ff68d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ff68d-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ff68d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ff68d-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Intralinks.</span><span class="sxs-lookup"><span data-stu-id="ff68d-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Intralinks application.</span></span>

<span data-ttu-id="ff68d-150">**Чтобы настроить единый вход Azure AD в Intralinks, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="ff68d-150">**To configure Azure AD single sign-on with Intralinks, perform the following steps:**</span></span>

1. <span data-ttu-id="ff68d-151">На портале Azure на странице интеграции с приложением **Intralinks** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="ff68d-151">In the Azure portal, on the **Intralinks** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="ff68d-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="ff68d-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_samlbase.png)

3. <span data-ttu-id="ff68d-155">В разделе **Домены и URL-адреса приложения Intralinks** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="ff68d-155">On the **Intralinks Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_url.png)

    <span data-ttu-id="ff68d-157">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<company name>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/<AzureADTenantID>`.</span><span class="sxs-lookup"><span data-stu-id="ff68d-157">In the **Sign-on URL** textbox, type a URL using the following pattern:  `https://<company name>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/<AzureADTenantID>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ff68d-158">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="ff68d-158">This value is not real.</span></span> <span data-ttu-id="ff68d-159">Вместо него необходимо указать фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="ff68d-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="ff68d-160">Для получения данного значения обратитесь к [группе поддержки Intralinks](https://www.intralinks.com/contact-1).</span><span class="sxs-lookup"><span data-stu-id="ff68d-160">Contact [Intralinks Client support team](https://www.intralinks.com/contact-1) to get this value.</span></span> 
 
4. <span data-ttu-id="ff68d-161">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="ff68d-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_certificate.png) 

5. <span data-ttu-id="ff68d-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="ff68d-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-intralinks-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ff68d-165">Чтобы настроить единый вход на стороне **Intralinks**, отправьте [группе поддержки Intralinks](https://www.intralinks.com/contact-1) скачанный **XML-файл метаданных**.</span><span class="sxs-lookup"><span data-stu-id="ff68d-165">To configure single sign-on on **Intralinks** side, you need to send the downloaded **Metadata XML** [Intralinks support team](https://www.intralinks.com/contact-1).</span></span> <span data-ttu-id="ff68d-166">Специалисты службы поддержки настроят подключение единого входа SAML на обеих сторонах.</span><span class="sxs-lookup"><span data-stu-id="ff68d-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="ff68d-167">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="ff68d-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ff68d-168">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="ff68d-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ff68d-169">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="ff68d-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ff68d-170">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="ff68d-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="ff68d-171">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ff68d-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="ff68d-173">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="ff68d-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ff68d-174">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ff68d-174">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-intralinks-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ff68d-176">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="ff68d-176">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-intralinks-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ff68d-178">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="ff68d-178">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-intralinks-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ff68d-180">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="ff68d-180">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-intralinks-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ff68d-182">а.</span><span class="sxs-lookup"><span data-stu-id="ff68d-182">a.</span></span> <span data-ttu-id="ff68d-183">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ff68d-183">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ff68d-184">b.</span><span class="sxs-lookup"><span data-stu-id="ff68d-184">b.</span></span> <span data-ttu-id="ff68d-185">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ff68d-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ff68d-186">c.</span><span class="sxs-lookup"><span data-stu-id="ff68d-186">c.</span></span> <span data-ttu-id="ff68d-187">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="ff68d-187">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ff68d-188">d.</span><span class="sxs-lookup"><span data-stu-id="ff68d-188">d.</span></span> <span data-ttu-id="ff68d-189">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="ff68d-189">Click **Create**.</span></span>
 
### <a name="creating-an-intralinks-test-user"></a><span data-ttu-id="ff68d-190">Создание тестового пользователя Intralinks</span><span class="sxs-lookup"><span data-stu-id="ff68d-190">Creating an Intralinks test user</span></span>

<span data-ttu-id="ff68d-191">В этом разделе описано, как создать пользователя Britta Simon в приложении Intralinks.</span><span class="sxs-lookup"><span data-stu-id="ff68d-191">In this section, you create a user called Britta Simon in Intralinks.</span></span> <span data-ttu-id="ff68d-192">Обратитесь к [группе поддержки Intralinks](https://www.intralinks.com/contact-1), чтобы добавить пользователей на платформу Intralinks.</span><span class="sxs-lookup"><span data-stu-id="ff68d-192">Please work with [Intralinks support team](https://www.intralinks.com/contact-1) to add the users in the Intralinks platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ff68d-193">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="ff68d-193">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ff68d-194">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к Intralinks.</span><span class="sxs-lookup"><span data-stu-id="ff68d-194">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Intralinks.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="ff68d-196">**Чтобы назначить пользователя Britta Simon в Intralinks, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="ff68d-196">**To assign Britta Simon to Intralinks, perform the following steps:**</span></span>

1. <span data-ttu-id="ff68d-197">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="ff68d-197">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="ff68d-199">В списке приложений выберите **Intralinks**.</span><span class="sxs-lookup"><span data-stu-id="ff68d-199">In the applications list, select **Intralinks**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_app.png) 

3. <span data-ttu-id="ff68d-201">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="ff68d-201">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="ff68d-203">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="ff68d-203">Click **Add** button.</span></span> <span data-ttu-id="ff68d-204">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="ff68d-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="ff68d-206">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="ff68d-206">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ff68d-207">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="ff68d-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ff68d-208">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="ff68d-208">Click **Assign** button on **Add Assignment** dialog.</span></span>

### <a name="add-intralinks-via-or-elite-application"></a><span data-ttu-id="ff68d-209">Добавление приложения Intralinks VIA или Elite</span><span class="sxs-lookup"><span data-stu-id="ff68d-209">Add Intralinks VIA or Elite application</span></span>

<span data-ttu-id="ff68d-210">Для всех приложений Intralinks используется одна платформа удостоверений единого входа, за исключением приложения Deal Nexus.</span><span class="sxs-lookup"><span data-stu-id="ff68d-210">Intralinks uses the same SSO identity platform for all other Intralinks applications excluding Deal Nexus application.</span></span> <span data-ttu-id="ff68d-211">Поэтому, если вы планируете использовать любое другое приложение Intralinks, сначала необходимо настроить единый вход для одного основного приложения Intralinks с помощью процедуры, описанной выше.</span><span class="sxs-lookup"><span data-stu-id="ff68d-211">So if you plan to use any other Intralinks application then first you have to configure SSO for one Primary Intralinks application using the procedure described above.</span></span>

<span data-ttu-id="ff68d-212">После этого вы можете выполнить описанные ниже действия, чтобы добавить другое приложение Intralinks в клиент, который может использовать это основное приложение для единого входа.</span><span class="sxs-lookup"><span data-stu-id="ff68d-212">After that you can follow the below procedure to add another Intralinks application in your tenant which can leverage this primary application for SSO.</span></span> 

>[!NOTE]
><span data-ttu-id="ff68d-213">Эта функция доступна только для клиентов SKU Azure AD уровня "Премиум" и недоступна для клиентов SKU уровня "Бесплатный" или "Базовый".</span><span class="sxs-lookup"><span data-stu-id="ff68d-213">This feature is available only to Azure AD Premium SKU Customers and not available for Free or Basic SKU customers.</span></span>

1. <span data-ttu-id="ff68d-214">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ff68d-214">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]


2. <span data-ttu-id="ff68d-216">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="ff68d-216">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ff68d-217">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="ff68d-217">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="ff68d-219">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="ff68d-219">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="ff68d-221">В поле поиска введите **Intralinks**.</span><span class="sxs-lookup"><span data-stu-id="ff68d-221">In the search box, type **Intralinks**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_search.png)

5. <span data-ttu-id="ff68d-223">На странице **Intralinks Add app** (Добавление приложения Intralinks) выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="ff68d-223">On **Intralinks Add app** perform the following steps:</span></span>

    ![Добавление приложения Intralinks VIA или Elite](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_addapp.png)

    <span data-ttu-id="ff68d-225">а.</span><span class="sxs-lookup"><span data-stu-id="ff68d-225">a.</span></span> <span data-ttu-id="ff68d-226">В текстовое поле **Имя** введите соответствующее имя приложения, например **Intralinks Elite**.</span><span class="sxs-lookup"><span data-stu-id="ff68d-226">In **Name** textbox, enter appropriate name of the application e.g. **Intralinks Elite**.</span></span>

    <span data-ttu-id="ff68d-227">b.</span><span class="sxs-lookup"><span data-stu-id="ff68d-227">b.</span></span> <span data-ttu-id="ff68d-228">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="ff68d-228">Click **Add** button.</span></span>

6.  <span data-ttu-id="ff68d-229">На портале Azure на странице интеграции с приложением **Intralinks** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="ff68d-229">In the Azure portal, on the **Intralinks** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

7. <span data-ttu-id="ff68d-231">В диалоговом окне **Единый вход** для параметра **Режим** выберите значение **Вход по ссылке**.</span><span class="sxs-lookup"><span data-stu-id="ff68d-231">On the **Single sign-on** dialog, select **Mode** as **Linked Sign-on**.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_linkedsignon.png)

8. <span data-ttu-id="ff68d-233">Получите от [команды Intralinks](https://www.intralinks.com/contact-1) URL-адрес единого входа, инициируемого поставщиком услуг, для другого приложения Intralinks. Затем введите этот URL-адрес в разделе **Настройка URL-адреса для единого входа**, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="ff68d-233">Get the the SP Initiated SSO URL from [Intralinks team](https://www.intralinks.com/contact-1) for the other Intralinks application and enter it in **Configure Sign-on URL** as shown below.</span></span> 
    
     ![Настройка единого входа](./media/active-directory-saas-intralinks-tutorial/tutorial_intralinks_customappurl.png)
    
     <span data-ttu-id="ff68d-235">В текстовом поле "URL-адрес входа" введите URL-адрес, с помощью которого пользователи входят в приложение Intralinks, в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="ff68d-235">In the Sign On URL textbox, type the URL used by your users to sign-on to your Intralinks application using the following pattern:</span></span>
   
    `https://<company name>.Intralinks.com/?PartnerIdpId=https://sts.windows.net/<AzureADTenantID>`

9. <span data-ttu-id="ff68d-236">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="ff68d-236">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-intralinks-tutorial/tutorial_general_400.png)

10. <span data-ttu-id="ff68d-238">Назначьте приложения пользователям или группам, как показано в разделе **[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)**.</span><span class="sxs-lookup"><span data-stu-id="ff68d-238">Assign the application to user or groups as shown in the section **[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)**.</span></span>

### <a name="testing-single-sign-on"></a><span data-ttu-id="ff68d-239">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="ff68d-239">Testing single sign-on</span></span>

<span data-ttu-id="ff68d-240">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="ff68d-240">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ff68d-241">Щелкнув плитку Intralinks на панели доступа, вы автоматически войдете в приложение Intralinks.</span><span class="sxs-lookup"><span data-stu-id="ff68d-241">When you click the Intralinks tile in the Access Panel, you should get automatically signed-on to your Intralinks application.</span></span>
<span data-ttu-id="ff68d-242">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ff68d-242">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ff68d-243">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="ff68d-243">Additional resources</span></span>

* [<span data-ttu-id="ff68d-244">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ff68d-244">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ff68d-245">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ff68d-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-intralinks-tutorial/tutorial_general_203.png

