---
title: "Руководство. Интеграция Azure Active Directory с ZIVVER | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и ZIVVER."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 64cb7ea0-df6c-4963-84d8-6f435980e2de
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: d27c773baaae64922fc8ad2c8f65bab177769f67
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zivver"></a><span data-ttu-id="00fc9-103">Руководство. Интеграция Azure Active Directory с ZIVVER</span><span class="sxs-lookup"><span data-stu-id="00fc9-103">Tutorial: Azure Active Directory integration with ZIVVER</span></span>

<span data-ttu-id="00fc9-104">В этом руководстве описано, как интегрировать ZIVVER с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="00fc9-104">In this tutorial, you learn how to integrate ZIVVER with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="00fc9-105">Интеграция Azure AD с приложением ZIVVER обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="00fc9-105">Integrating ZIVVER with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="00fc9-106">С помощью Azure AD вы можете контролировать доступ к ZIVVER.</span><span class="sxs-lookup"><span data-stu-id="00fc9-106">You can control in Azure AD who has access to ZIVVER.</span></span>
- <span data-ttu-id="00fc9-107">Вы можете включить автоматический вход пользователей в ZIVVER (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="00fc9-107">You can enable your users to automatically get signed-on to ZIVVER (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="00fc9-108">Вы можете управлять учетными записями централизованно — на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="00fc9-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="00fc9-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="00fc9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="00fc9-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="00fc9-110">Prerequisites</span></span>

<span data-ttu-id="00fc9-111">Чтобы настроить интеграцию Azure AD с ZIVVER, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="00fc9-111">To configure Azure AD integration with ZIVVER, you need the following items:</span></span>

- <span data-ttu-id="00fc9-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="00fc9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="00fc9-113">подписка с поддержкой единого входа ZIVVER.</span><span class="sxs-lookup"><span data-stu-id="00fc9-113">A ZIVVER single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="00fc9-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="00fc9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="00fc9-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="00fc9-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="00fc9-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="00fc9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="00fc9-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="00fc9-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="00fc9-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="00fc9-118">Scenario description</span></span>
<span data-ttu-id="00fc9-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="00fc9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="00fc9-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="00fc9-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="00fc9-121">Добавление ZIVVER из коллекции</span><span class="sxs-lookup"><span data-stu-id="00fc9-121">Adding ZIVVER from the gallery</span></span>
2. <span data-ttu-id="00fc9-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="00fc9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zivver-from-the-gallery"></a><span data-ttu-id="00fc9-123">Добавление ZIVVER из коллекции</span><span class="sxs-lookup"><span data-stu-id="00fc9-123">Adding ZIVVER from the gallery</span></span>
<span data-ttu-id="00fc9-124">Чтобы настроить интеграцию ZIVVER с Azure AD, необходимо добавить ZIVVER из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="00fc9-124">To configure the integration of ZIVVER into Azure AD, you need to add ZIVVER from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="00fc9-125">**Чтобы добавить ZIVVER из коллекции, сделайте следующее.**</span><span class="sxs-lookup"><span data-stu-id="00fc9-125">**To add ZIVVER from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="00fc9-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="00fc9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка "Azure Active Directory"][1]

2. <span data-ttu-id="00fc9-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="00fc9-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="00fc9-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="00fc9-129">Then go to **All applications**.</span></span>

    ![Колонка "Корпоративные приложения"][2]
    
3. <span data-ttu-id="00fc9-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="00fc9-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Кнопка "Новое приложение"][3]

4. <span data-ttu-id="00fc9-133">В поле поиска введите **ZIVVER**, выберите **ZIVVER** на панели результатов и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="00fc9-133">In the search box, type **ZIVVER**, select **ZIVVER** from result panel then click **Add** button to add the application.</span></span>

    ![ZIVVER в списке результатов](./media/active-directory-saas-zivver-tutorial/tutorial_zivver_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="00fc9-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="00fc9-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="00fc9-136">В этом разделе описана настройка и проверка единого входа Azure AD в приложение ZIVVER с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="00fc9-136">In this section, you configure and test Azure AD single sign-on with ZIVVER based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="00fc9-137">Для работы единого входа в Azure AD необходимо знать, какой пользователь в ZIVVER соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="00fc9-137">For single sign-on to work, Azure AD needs to know what the counterpart user in ZIVVER is to a user in Azure AD.</span></span> <span data-ttu-id="00fc9-138">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в ZIVVER.</span><span class="sxs-lookup"><span data-stu-id="00fc9-138">In other words, a link relationship between an Azure AD user and the related user in ZIVVER needs to be established.</span></span>

<span data-ttu-id="00fc9-139">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в ZIVVER.</span><span class="sxs-lookup"><span data-stu-id="00fc9-139">In ZIVVER, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="00fc9-140">Чтобы настроить и проверить единый вход Azure AD в ZIVVER, выполните действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="00fc9-140">To configure and test Azure AD single sign-on with ZIVVER, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="00fc9-141">**[Настройка единого входа Azure AD](#configure-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="00fc9-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="00fc9-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="00fc9-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="00fc9-143">**[Создание тестового пользователя ZIVVER](#create-a-zivver-test-user)** требуется для того, чтобы в ZIVVER существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="00fc9-143">**[Create a ZIVVER test user](#create-a-zivver-test-user)** - to have a counterpart of Britta Simon in ZIVVER that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="00fc9-144">**[Назначение тестового пользователя Azure AD](#assign-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход Azure AD.</span><span class="sxs-lookup"><span data-stu-id="00fc9-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="00fc9-145">**[Проверка единого входа](#test-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="00fc9-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="00fc9-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="00fc9-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="00fc9-147">В этом разделе мы включим на портале Azure единый вход Azure AD и настроим его в приложении ZIVVER.</span><span class="sxs-lookup"><span data-stu-id="00fc9-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ZIVVER application.</span></span>

<span data-ttu-id="00fc9-148">**Чтобы настроить единый вход Azure AD в ZIVVER, сделайте следующее.**</span><span class="sxs-lookup"><span data-stu-id="00fc9-148">**To configure Azure AD single sign-on with ZIVVER, perform the following steps:**</span></span>

1. <span data-ttu-id="00fc9-149">На портале Azure на странице интеграции с приложением **ZIVVER** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="00fc9-149">In the Azure portal, on the **ZIVVER** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="00fc9-151">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="00fc9-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-zivver-tutorial/tutorial_zivver_samlbase.png)

3. <span data-ttu-id="00fc9-153">В разделе **Домены и URL-адреса приложения ZIVVER** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="00fc9-153">On the **ZIVVER Domain and URLs** section, perform the following steps:</span></span>

    ![Сведения о домене и URL-адресах единого входа приложения ZIVVER](./media/active-directory-saas-zivver-tutorial/tutorial_zivver_url.png)

    <span data-ttu-id="00fc9-155">В текстовом поле **Идентификатор** введите URL-адрес `https://app.zivver.com/SAML/Zivver`.</span><span class="sxs-lookup"><span data-stu-id="00fc9-155">In the **Identifier** textbox, type the URL: `https://app.zivver.com/SAML/Zivver`</span></span>

4. <span data-ttu-id="00fc9-156">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="00fc9-156">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Ссылка для скачивания сертификата](./media/active-directory-saas-zivver-tutorial/tutorial_zivver_certificate.png) 

5. <span data-ttu-id="00fc9-158">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="00fc9-158">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-zivver-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="00fc9-160">Чтобы настроить единый вход на стороне **ZIVVER**, отправьте в [службу поддержки ZIVVER](https://support.zivver.com) скачанный **XML-файл метаданных**.</span><span class="sxs-lookup"><span data-stu-id="00fc9-160">To configure single sign-on on **ZIVVER** side, you need to send the downloaded **Metadata XML** to [ZIVVER support team](https://support.zivver.com).</span></span> <span data-ttu-id="00fc9-161">Специалисты службы поддержки настроят подключение единого входа SAML на обеих сторонах.</span><span class="sxs-lookup"><span data-stu-id="00fc9-161">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="00fc9-162">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="00fc9-162">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="00fc9-163">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="00fc9-163">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="00fc9-164">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="00fc9-164">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="00fc9-165">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="00fc9-165">Create an Azure AD test user</span></span>

<span data-ttu-id="00fc9-166">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="00fc9-166">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="00fc9-168">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="00fc9-168">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="00fc9-169">На портале Azure в области слева нажмите кнопку **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="00fc9-169">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Кнопка "Azure Active Directory"](./media/active-directory-saas-zivver-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="00fc9-171">Чтобы открыть список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="00fc9-171">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Ссылки "Пользователи и группы" и "Все пользователи"](./media/active-directory-saas-zivver-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="00fc9-173">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна **Все пользователи** щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="00fc9-173">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Кнопка "Добавить"](./media/active-directory-saas-zivver-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="00fc9-175">В диалоговом окне **Пользователь** сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="00fc9-175">In the **User** dialog box, perform the following steps:</span></span>

    ![Диалоговое окно "Пользователь"](./media/active-directory-saas-zivver-tutorial/create_aaduser_04.png)

    <span data-ttu-id="00fc9-177">а.</span><span class="sxs-lookup"><span data-stu-id="00fc9-177">a.</span></span> <span data-ttu-id="00fc9-178">В поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="00fc9-178">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="00fc9-179">b.</span><span class="sxs-lookup"><span data-stu-id="00fc9-179">b.</span></span> <span data-ttu-id="00fc9-180">В поле **Имя пользователя** введите адрес электронной почты для пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="00fc9-180">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="00fc9-181">c.</span><span class="sxs-lookup"><span data-stu-id="00fc9-181">c.</span></span> <span data-ttu-id="00fc9-182">Установите флажок **Показать пароль** и запишите значение, которое отображается в поле **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="00fc9-182">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="00fc9-183">г)</span><span class="sxs-lookup"><span data-stu-id="00fc9-183">d.</span></span> <span data-ttu-id="00fc9-184">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="00fc9-184">Click **Create**.</span></span>
  
### <a name="create-a-zivver-test-user"></a><span data-ttu-id="00fc9-185">Создание тестового пользователя ZIVVER</span><span class="sxs-lookup"><span data-stu-id="00fc9-185">Create a ZIVVER test user</span></span>

<span data-ttu-id="00fc9-186">В этом разделе описано, как создать пользователя Britta Simon в приложении ZIVVER.</span><span class="sxs-lookup"><span data-stu-id="00fc9-186">In this section, you create a user called Britta Simon in ZIVVER.</span></span> <span data-ttu-id="00fc9-187">Обратитесь в [службу поддержки ZIVVER](https://support.zivver.com), чтобы добавить пользователей на платформу ZIVVER.</span><span class="sxs-lookup"><span data-stu-id="00fc9-187">Work with [ZIVVER support team](https://support.zivver.com) to add the users in the ZIVVER platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="00fc9-188">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="00fc9-188">Assign the Azure AD test user</span></span>

<span data-ttu-id="00fc9-189">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив доступ к ZIVVER.</span><span class="sxs-lookup"><span data-stu-id="00fc9-189">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ZIVVER.</span></span>

![Назначение роли пользователя][200] 

<span data-ttu-id="00fc9-191">**Чтобы назначить пользователя Britta Simon в приложении ZIVVER, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="00fc9-191">**To assign Britta Simon to ZIVVER, perform the following steps:**</span></span>

1. <span data-ttu-id="00fc9-192">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="00fc9-192">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="00fc9-194">В списке приложений выберите **ZIVVER**.</span><span class="sxs-lookup"><span data-stu-id="00fc9-194">In the applications list, select **ZIVVER**.</span></span>

    ![Ссылка на ZIVVER в списке "Приложения"](./media/active-directory-saas-zivver-tutorial/tutorial_zivver_app.png)  

3. <span data-ttu-id="00fc9-196">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="00fc9-196">In the menu on the left, click **Users and groups**.</span></span>

    ![Ссылка "Пользователи и группы"][202]

4. <span data-ttu-id="00fc9-198">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="00fc9-198">Click **Add** button.</span></span> <span data-ttu-id="00fc9-199">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="00fc9-199">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Область "Добавление назначения"][203]

5. <span data-ttu-id="00fc9-201">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="00fc9-201">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="00fc9-202">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="00fc9-202">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="00fc9-203">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="00fc9-203">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="00fc9-204">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="00fc9-204">Test single sign-on</span></span>

<span data-ttu-id="00fc9-205">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="00fc9-205">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="00fc9-206">Щелкнув плитку ZIVVER на панели доступа, вы автоматически войдете в приложение ZIVVER.</span><span class="sxs-lookup"><span data-stu-id="00fc9-206">When you click the ZIVVER tile in the Access Panel, you should get automatically signed-on to your ZIVVER application.</span></span>
<span data-ttu-id="00fc9-207">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="00fc9-207">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="00fc9-208">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="00fc9-208">Additional resources</span></span>

* [<span data-ttu-id="00fc9-209">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="00fc9-209">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="00fc9-210">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="00fc9-210">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zivver-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zivver-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zivver-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zivver-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zivver-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zivver-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zivver-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zivver-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zivver-tutorial/tutorial_general_203.png

