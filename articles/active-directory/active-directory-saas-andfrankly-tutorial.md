---
title: "Руководство. Интеграция Azure Active Directory с &frankly | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в приложении &frankly."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1d702060-1b89-4e9d-9f01-ede4f1171c73
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: ea18a9f9bff258337a3de6d7703b4c548efa37df
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-frankly"></a><span data-ttu-id="cf565-103">Руководство. Интеграция Azure Active Directory с &frankly</span><span class="sxs-lookup"><span data-stu-id="cf565-103">Tutorial: Azure Active Directory integration with &frankly</span></span>

<span data-ttu-id="cf565-104">В этом руководстве описано, как интегрировать &frankly с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="cf565-104">In this tutorial, you learn how to integrate &frankly with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="cf565-105">Интеграция Azure AD с приложением &frankly обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="cf565-105">Integrating &frankly with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="cf565-106">С помощью Azure AD вы можете контролировать доступ к &frankly.</span><span class="sxs-lookup"><span data-stu-id="cf565-106">You can control in Azure AD who has access to &frankly</span></span>
- <span data-ttu-id="cf565-107">Вы можете включить автоматический вход пользователей в &frankly (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cf565-107">You can enable your users to automatically get signed-on to &frankly (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="cf565-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="cf565-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="cf565-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="cf565-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cf565-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="cf565-110">Prerequisites</span></span>

<span data-ttu-id="cf565-111">Чтобы настроить интеграцию Azure AD с приложением &frankly, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="cf565-111">To configure Azure AD integration with &frankly, you need the following items:</span></span>

- <span data-ttu-id="cf565-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="cf565-112">An Azure AD subscription</span></span>
- <span data-ttu-id="cf565-113">подписка &frankly с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="cf565-113">A &frankly single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="cf565-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="cf565-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="cf565-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="cf565-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="cf565-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="cf565-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="cf565-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="cf565-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="cf565-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="cf565-118">Scenario description</span></span>
<span data-ttu-id="cf565-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="cf565-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="cf565-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="cf565-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="cf565-121">Добавление &frankly из коллекции</span><span class="sxs-lookup"><span data-stu-id="cf565-121">Adding &frankly from the gallery</span></span>
2. <span data-ttu-id="cf565-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="cf565-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-frankly-from-the-gallery"></a><span data-ttu-id="cf565-123">Добавление &frankly из коллекции</span><span class="sxs-lookup"><span data-stu-id="cf565-123">Adding &frankly from the gallery</span></span>
<span data-ttu-id="cf565-124">Чтобы настроить интеграцию &frankly с Azure AD, необходимо добавить &frankly из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="cf565-124">To configure the integration of &frankly into Azure AD, you need to add &frankly from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="cf565-125">**Чтобы добавить &frankly из коллекции, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="cf565-125">**To add &frankly from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="cf565-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="cf565-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="cf565-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="cf565-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="cf565-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="cf565-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="cf565-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="cf565-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="cf565-133">В поле поиска введите **&frankly**.</span><span class="sxs-lookup"><span data-stu-id="cf565-133">In the search box, type **&frankly**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_search.png)

5. <span data-ttu-id="cf565-135">На панели результатов выберите **&frankly** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="cf565-135">In the results panel, select **&frankly**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="cf565-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="cf565-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="cf565-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложение &frankly с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cf565-138">In this section, you configure and test Azure AD single sign-on with &frankly based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="cf565-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в &frankly соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cf565-139">For single sign-on to work, Azure AD needs to know what the counterpart user in &frankly is to a user in Azure AD.</span></span> <span data-ttu-id="cf565-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в &frankly.</span><span class="sxs-lookup"><span data-stu-id="cf565-140">In other words, a link relationship between an Azure AD user and the related user in &frankly needs to be established.</span></span>

<span data-ttu-id="cf565-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в &frankly.</span><span class="sxs-lookup"><span data-stu-id="cf565-141">In &frankly, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="cf565-142">Чтобы настроить и проверить единый вход Azure AD в &frankly, выполните следующие стандартные действия.</span><span class="sxs-lookup"><span data-stu-id="cf565-142">To configure and test Azure AD single sign-on with &frankly, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="cf565-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="cf565-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="cf565-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cf565-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="cf565-145">**[Создание тестового пользователя &frankly](#creating-a-frankly-test-user)** нужно для того, чтобы в &frankly также существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cf565-145">**[Creating a &frankly test user](#creating-a-frankly-test-user)** - to have a counterpart of Britta Simon in &frankly that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="cf565-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cf565-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="cf565-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="cf565-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="cf565-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="cf565-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="cf565-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении &frankly.</span><span class="sxs-lookup"><span data-stu-id="cf565-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your &frankly application.</span></span>

<span data-ttu-id="cf565-150">**Чтобы настроить единый вход Azure AD в &frankly, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="cf565-150">**To configure Azure AD single sign-on with &frankly, perform the following steps:**</span></span>

1. <span data-ttu-id="cf565-151">На портале Azure на странице интеграции с приложением **&frankly** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="cf565-151">In the Azure portal, on the **&frankly** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="cf565-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="cf565-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_samlbase.png)

3. <span data-ttu-id="cf565-155">Если вы хотите настроить приложение в **режиме, инициируемом IdP**, то в разделе **Домены и URL-адреса приложения &frankly** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="cf565-155">On the **&frankly Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_url.png)

    <span data-ttu-id="cf565-157">а.</span><span class="sxs-lookup"><span data-stu-id="cf565-157">a.</span></span> <span data-ttu-id="cf565-158">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://andfrankly.com/saml/simplesaml/www/module.php/saml/sp/metadata.php/<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="cf565-158">In the **Identifier** textbox, type a URL using the following pattern: `https://andfrankly.com/saml/simplesaml/www/module.php/saml/sp/metadata.php/<tenant id>`</span></span>

    <span data-ttu-id="cf565-159">b.</span><span class="sxs-lookup"><span data-stu-id="cf565-159">b.</span></span> <span data-ttu-id="cf565-160">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате: `https://andfrankly.com/saml/simplesaml/www/module.php/saml/sp/saml2-acs.php/<tenant id>`.</span><span class="sxs-lookup"><span data-stu-id="cf565-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://andfrankly.com/saml/simplesaml/www/module.php/saml/sp/saml2-acs.php/<tenant id>`</span></span>

4. <span data-ttu-id="cf565-161">Установите флажок **Показать дополнительные параметры URL-адресов**,</span><span class="sxs-lookup"><span data-stu-id="cf565-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="cf565-162">если хотите настроить приложение для работы в режиме, инициируемом **поставщиком услуг**.</span><span class="sxs-lookup"><span data-stu-id="cf565-162">If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_url1.png)

    <span data-ttu-id="cf565-164">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://andfrankly.com/saml/okta/?saml_sso=<tenant id>`</span><span class="sxs-lookup"><span data-stu-id="cf565-164">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://andfrankly.com/saml/okta/?saml_sso=<tenant id>`</span></span>
    > [!NOTE] 
    > <span data-ttu-id="cf565-165">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="cf565-165">These values are not real.</span></span> <span data-ttu-id="cf565-166">Измените их, указав фактические значения идентификатора и URL-адресов входа и ответа.</span><span class="sxs-lookup"><span data-stu-id="cf565-166">Update these values with the actual Identifier, Sign-on, and Reply URL.</span></span> <span data-ttu-id="cf565-167">Чтобы получить эти значения, обратитесь к [группе поддержки &frankly](mailto:help@andfrankly.com).</span><span class="sxs-lookup"><span data-stu-id="cf565-167">Contact [andfrankly support team](mailto:help@andfrankly.com) to get these values.</span></span>

5. <span data-ttu-id="cf565-168">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="cf565-168">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_certificate.png) 

6. <span data-ttu-id="cf565-170">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="cf565-170">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-andfrankly-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="cf565-172">Чтобы настроить единый вход на стороне **&frankly**, отправьте [группе поддержки &frankly](mailto:help@andfrankly.com) скачанный **XML-файл метаданных**.</span><span class="sxs-lookup"><span data-stu-id="cf565-172">To configure single sign-on on **&frankly** side, you need to send the downloaded **Metadata XML** to [andfrankly support team](mailto:help@andfrankly.com).</span></span> 

> [!TIP]
> <span data-ttu-id="cf565-173">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="cf565-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="cf565-174">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="cf565-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="cf565-175">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="cf565-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="cf565-176">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="cf565-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="cf565-177">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="cf565-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="cf565-179">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="cf565-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="cf565-180">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="cf565-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-andfrankly-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="cf565-182">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="cf565-182">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-andfrankly-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="cf565-184">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="cf565-184">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-andfrankly-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="cf565-186">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="cf565-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-andfrankly-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="cf565-188">а.</span><span class="sxs-lookup"><span data-stu-id="cf565-188">a.</span></span> <span data-ttu-id="cf565-189">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="cf565-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="cf565-190">b.</span><span class="sxs-lookup"><span data-stu-id="cf565-190">b.</span></span> <span data-ttu-id="cf565-191">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="cf565-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="cf565-192">c.</span><span class="sxs-lookup"><span data-stu-id="cf565-192">c.</span></span> <span data-ttu-id="cf565-193">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="cf565-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="cf565-194">d.</span><span class="sxs-lookup"><span data-stu-id="cf565-194">d.</span></span> <span data-ttu-id="cf565-195">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="cf565-195">Click **Create**.</span></span>
 
### <a name="creating-a-frankly-test-user"></a><span data-ttu-id="cf565-196">Создание тестового пользователя приложения &frankly</span><span class="sxs-lookup"><span data-stu-id="cf565-196">Creating a &frankly test user</span></span>

<span data-ttu-id="cf565-197">В этом разделе описано, как создать пользователя Britta Simon в приложении &frankly.</span><span class="sxs-lookup"><span data-stu-id="cf565-197">In this section, you create a user called Britta Simon in &frankly.</span></span> <span data-ttu-id="cf565-198">Чтобы добавить пользователей на платформе &frankly, обратитесь к [группе поддержки &frankly](mailto:help@andfrankly.com).</span><span class="sxs-lookup"><span data-stu-id="cf565-198">Work with  [andfrankly support team](mailto:help@andfrankly.com) to add the users in the &frankly platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="cf565-199">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="cf565-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="cf565-200">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к &frankly.</span><span class="sxs-lookup"><span data-stu-id="cf565-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to &frankly.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="cf565-202">**Чтобы назначить пользователя Britta Simon в &frankly, сделайте следующее.**</span><span class="sxs-lookup"><span data-stu-id="cf565-202">**To assign Britta Simon to &frankly, perform the following steps:**</span></span>

1. <span data-ttu-id="cf565-203">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="cf565-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="cf565-205">В списке приложений выберите **&frankly**.</span><span class="sxs-lookup"><span data-stu-id="cf565-205">In the applications list, select **&frankly**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-andfrankly-tutorial/tutorial_andfrankly_app.png) 

3. <span data-ttu-id="cf565-207">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="cf565-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="cf565-209">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="cf565-209">Click **Add** button.</span></span> <span data-ttu-id="cf565-210">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="cf565-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="cf565-212">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="cf565-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="cf565-213">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="cf565-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="cf565-214">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="cf565-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="cf565-215">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="cf565-215">Testing single sign-on</span></span>

<span data-ttu-id="cf565-216">Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="cf565-216">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="cf565-217">Щелкнув элемент "&frankly" на панели доступа, вы автоматически войдете в приложение &frankly.</span><span class="sxs-lookup"><span data-stu-id="cf565-217">When you click the &frankly tile in the Access Panel, you should get automatically signed-on to your &frankly application</span></span>

## <a name="additional-resources"></a><span data-ttu-id="cf565-218">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="cf565-218">Additional resources</span></span>

* [<span data-ttu-id="cf565-219">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="cf565-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="cf565-220">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="cf565-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-andfrankly-tutorial/tutorial_general_203.png

