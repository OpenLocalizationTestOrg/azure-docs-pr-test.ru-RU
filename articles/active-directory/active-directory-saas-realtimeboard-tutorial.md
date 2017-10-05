---
title: "Руководство по интеграции Azure Active Directory с RealtimeBoard | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в приложении RealtimeBoard."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: a37fc1c0-4bae-4173-989b-00de53a0076f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: jeedes
ms.openlocfilehash: d3ba8cb1f7e1d4332f7912848e8b6902d9acf909
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-realtimeboard"></a><span data-ttu-id="38093-103">Руководство по интеграции Azure Active Directory с RealtimeBoard</span><span class="sxs-lookup"><span data-stu-id="38093-103">Tutorial: Azure Active Directory integration with RealtimeBoard</span></span>

<span data-ttu-id="38093-104">В этом руководстве описано, как интегрировать приложение RealtimeBoard с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="38093-104">In this tutorial, you learn how to integrate RealtimeBoard with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="38093-105">Интеграция Azure AD с приложением RealtimeBoard обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="38093-105">Integrating RealtimeBoard with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="38093-106">C помощью Azure AD вы можете контролировать доступ к RealtimeBoard.</span><span class="sxs-lookup"><span data-stu-id="38093-106">You can control in Azure AD who has access to RealtimeBoard.</span></span>
- <span data-ttu-id="38093-107">Вы можете включить автоматический вход пользователей в RealtimeBoard (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="38093-107">You can enable your users to automatically get signed-on to RealtimeBoard (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="38093-108">Вы можете управлять учетными записями централизованно — на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="38093-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="38093-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="38093-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="38093-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="38093-110">Prerequisites</span></span>

<span data-ttu-id="38093-111">Чтобы настроить интеграцию Azure AD с RealtimeBoard, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="38093-111">To configure Azure AD integration with RealtimeBoard, you need the following items:</span></span>

- <span data-ttu-id="38093-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="38093-112">An Azure AD subscription</span></span>
- <span data-ttu-id="38093-113">подписка RealtimeBoard с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="38093-113">A RealtimeBoard single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="38093-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="38093-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="38093-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="38093-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="38093-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="38093-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="38093-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="38093-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="38093-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="38093-118">Scenario description</span></span>
<span data-ttu-id="38093-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="38093-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="38093-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="38093-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="38093-121">Добавление RealtimeBoard из коллекции</span><span class="sxs-lookup"><span data-stu-id="38093-121">Adding RealtimeBoard from the gallery</span></span>
2. <span data-ttu-id="38093-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="38093-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-realtimeboard-from-the-gallery"></a><span data-ttu-id="38093-123">Добавление RealtimeBoard из коллекции</span><span class="sxs-lookup"><span data-stu-id="38093-123">Adding RealtimeBoard from the gallery</span></span>
<span data-ttu-id="38093-124">Чтобы настроить интеграцию RealtimeBoard с Azure AD, необходимо добавить RealtimeBoard из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="38093-124">To configure the integration of RealtimeBoard into Azure AD, you need to add RealtimeBoard from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="38093-125">**Чтобы добавить RealtimeBoard из коллекции, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="38093-125">**To add RealtimeBoard from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="38093-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="38093-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка "Azure Active Directory"][1]

2. <span data-ttu-id="38093-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="38093-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="38093-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="38093-129">Then go to **All applications**.</span></span>

    ![Колонка "Корпоративные приложения"][2]
    
3. <span data-ttu-id="38093-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="38093-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Кнопка "Новое приложение"][3]

4. <span data-ttu-id="38093-133">В поле поиска введите **RealtimeBoard**, выберите **RealtimeBoard** на панели результатов и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="38093-133">In the search box, type **RealtimeBoard**, select **RealtimeBoard** from result panel then click **Add** button to add the application.</span></span>

    ![RealtimeBoard в списке результатов](./media/active-directory-saas-realtimeboard-tutorial/tutorial_realtimeboard_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="38093-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="38093-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="38093-136">В этом разделе описана настройка и проверка единого входа Azure AD в RealtimeBoard с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="38093-136">In this section, you configure and test Azure AD single sign-on with RealtimeBoard based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="38093-137">Для работы единого входа в Azure AD необходимо знать, какой пользователь в RealtimeBoard соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="38093-137">For single sign-on to work, Azure AD needs to know what the counterpart user in RealtimeBoard is to a user in Azure AD.</span></span> <span data-ttu-id="38093-138">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в RealtimeBoard.</span><span class="sxs-lookup"><span data-stu-id="38093-138">In other words, a link relationship between an Azure AD user and the related user in RealtimeBoard needs to be established.</span></span>

<span data-ttu-id="38093-139">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в RealtimeBoard.</span><span class="sxs-lookup"><span data-stu-id="38093-139">In RealtimeBoard, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="38093-140">Чтобы настроить и проверить единый вход Azure AD в RealtimeBoard, выполните действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="38093-140">To configure and test Azure AD single sign-on with RealtimeBoard, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="38093-141">**[Настройка единого входа Azure AD](#configure-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="38093-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="38093-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="38093-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="38093-143">**[Создание тестового пользователя RealtimeBoard](#create-a-realtimeboard-test-user)** требуется для того, чтобы в RealtimeBoard существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="38093-143">**[Create a RealtimeBoard test user](#create-a-realtimeboard-test-user)** - to have a counterpart of Britta Simon in RealtimeBoard that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="38093-144">**[Назначение тестового пользователя Azure AD](#assign-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход Azure AD.</span><span class="sxs-lookup"><span data-stu-id="38093-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="38093-145">**[Проверка единого входа](#test-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="38093-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="38093-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="38093-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="38093-147">В этом разделе мы включим на портале Azure единый вход Azure AD и настроим его в приложении RealtimeBoard.</span><span class="sxs-lookup"><span data-stu-id="38093-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your RealtimeBoard application.</span></span>

<span data-ttu-id="38093-148">**Чтобы настроить единый вход Azure AD в RealtimeBoard, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="38093-148">**To configure Azure AD single sign-on with RealtimeBoard, perform the following steps:**</span></span>

1. <span data-ttu-id="38093-149">На портале Azure на странице интеграции с приложением **RealtimeBoard** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="38093-149">In the Azure portal, on the **RealtimeBoard** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="38093-151">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="38093-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-realtimeboard-tutorial/tutorial_realtimeboard_samlbase.png)

3. <span data-ttu-id="38093-153">Если вы хотите настроить приложение в **режиме, инициированном поставщиком удостоверений**, в разделе **Домены и URL-адреса приложения RealtimeBoard** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="38093-153">On the **RealtimeBoard Domain and URLs** section, if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Сведения о домене и URL-адресах единого входа для приложения RealtimeBoard](./media/active-directory-saas-realtimeboard-tutorial/tutorial_realtimeboard_url.png)

    <span data-ttu-id="38093-155">В текстовом поле **Идентификатор** введите URL-адрес в формате `https://realtimeboard.com/`.</span><span class="sxs-lookup"><span data-stu-id="38093-155">In the **Identifier** textbox, type a URL as: `https://realtimeboard.com/`</span></span>

4. <span data-ttu-id="38093-156">Установите флажок **Показать дополнительные параметры URL-адресов**, если вы хотите настроить приложение для работы в режиме, инициируемом **поставщиком услуг**.</span><span class="sxs-lookup"><span data-stu-id="38093-156">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-realtimeboard-tutorial/tutorial_realtimeboard_url2.png)

    <span data-ttu-id="38093-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в формате `https://realtimeboard.com/sso/saml`.</span><span class="sxs-lookup"><span data-stu-id="38093-158">In the **Sign-on URL** textbox, type a URL as: `https://realtimeboard.com/sso/saml`</span></span>

5. <span data-ttu-id="38093-159">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="38093-159">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Ссылка для скачивания сертификата](./media/active-directory-saas-realtimeboard-tutorial/tutorial_realtimeboard_certificate.png) 

6. <span data-ttu-id="38093-161">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="38093-161">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="38093-163">Чтобы настроить единый вход на стороне **RealtimeBoard**, отправьте в [службу поддержки RealtimeBoard](mailto:support@realtimeboard.com) скачанный **XML-файл метаданных**.</span><span class="sxs-lookup"><span data-stu-id="38093-163">To configure single sign-on on **RealtimeBoard** side, you need to send the downloaded **Metadata XML** to [RealtimeBoard support team](mailto:support@realtimeboard.com).</span></span> <span data-ttu-id="38093-164">Специалисты службы поддержки настроят подключение единого входа SAML на обеих сторонах.</span><span class="sxs-lookup"><span data-stu-id="38093-164">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="38093-165">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="38093-165">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="38093-166">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="38093-166">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="38093-167">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="38093-167">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="38093-168">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="38093-168">Create an Azure AD test user</span></span>

<span data-ttu-id="38093-169">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="38093-169">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="38093-171">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="38093-171">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="38093-172">На портале Azure в области слева нажмите кнопку **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="38093-172">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Кнопка "Azure Active Directory"](./media/active-directory-saas-realtimeboard-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="38093-174">Чтобы открыть список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="38093-174">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Ссылки "Пользователи и группы" и "Все пользователи"](./media/active-directory-saas-realtimeboard-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="38093-176">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна **Все пользователи** щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="38093-176">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Кнопка "Добавить"](./media/active-directory-saas-realtimeboard-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="38093-178">В диалоговом окне **Пользователь** сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="38093-178">In the **User** dialog box, perform the following steps:</span></span>

    ![Диалоговое окно "Пользователь"](./media/active-directory-saas-realtimeboard-tutorial/create_aaduser_04.png)

    <span data-ttu-id="38093-180">а.</span><span class="sxs-lookup"><span data-stu-id="38093-180">a.</span></span> <span data-ttu-id="38093-181">В поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="38093-181">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="38093-182">b.</span><span class="sxs-lookup"><span data-stu-id="38093-182">b.</span></span> <span data-ttu-id="38093-183">В поле **Имя пользователя** введите адрес электронной почты для пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="38093-183">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="38093-184">c.</span><span class="sxs-lookup"><span data-stu-id="38093-184">c.</span></span> <span data-ttu-id="38093-185">Установите флажок **Показать пароль** и запишите значение, которое отображается в поле **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="38093-185">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="38093-186">г)</span><span class="sxs-lookup"><span data-stu-id="38093-186">d.</span></span> <span data-ttu-id="38093-187">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="38093-187">Click **Create**.</span></span>
 
### <a name="create-a-realtimeboard-test-user"></a><span data-ttu-id="38093-188">Создание тестового пользователя RealtimeBoard</span><span class="sxs-lookup"><span data-stu-id="38093-188">Create a RealtimeBoard test user</span></span>

<span data-ttu-id="38093-189">Цель этого раздела — создать пользователя с именем Britta Simon в RealtimeBoard.</span><span class="sxs-lookup"><span data-stu-id="38093-189">The objective of this section is to create a user called Britta Simon in RealtimeBoard.</span></span> <span data-ttu-id="38093-190">Приложение RealtimeBoard поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="38093-190">RealtimeBoard supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="38093-191">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="38093-191">There is no action item for you in this section.</span></span> <span data-ttu-id="38093-192">Если пользователь еще не существует в RealtimeBoard, он создается при попытке доступа к приложению RealtimeBoard.</span><span class="sxs-lookup"><span data-stu-id="38093-192">If a user doesn't already exist in RealtimeBoard, a new one is created when you attempt to access RealtimeBoard.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="38093-193">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="38093-193">Assign the Azure AD test user</span></span>

<span data-ttu-id="38093-194">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к RealtimeBoard.</span><span class="sxs-lookup"><span data-stu-id="38093-194">In this section, you enable Britta Simon to use Azure single sign-on by granting access to RealtimeBoard.</span></span>

![Назначение роли пользователя][200] 

<span data-ttu-id="38093-196">**Чтобы назначить пользователя Britta Simon в RealtimeBoard, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="38093-196">**To assign Britta Simon to RealtimeBoard, perform the following steps:**</span></span>

1. <span data-ttu-id="38093-197">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="38093-197">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="38093-199">В списке приложений выберите **RealtimeBoard**.</span><span class="sxs-lookup"><span data-stu-id="38093-199">In the applications list, select **RealtimeBoard**.</span></span>

    ![Ссылка на RealtimeBoard в списке "Приложения"](./media/active-directory-saas-realtimeboard-tutorial/tutorial_realtimeboard_app.png)  

3. <span data-ttu-id="38093-201">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="38093-201">In the menu on the left, click **Users and groups**.</span></span>

    ![Ссылка "Пользователи и группы"][202]

4. <span data-ttu-id="38093-203">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="38093-203">Click **Add** button.</span></span> <span data-ttu-id="38093-204">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="38093-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Область "Добавление назначения"][203]

5. <span data-ttu-id="38093-206">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="38093-206">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="38093-207">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="38093-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="38093-208">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="38093-208">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="38093-209">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="38093-209">Test single sign-on</span></span>

<span data-ttu-id="38093-210">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="38093-210">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="38093-211">Щелкнув плитку RealtimeBoard на панели доступа, вы автоматически войдете в приложение RealtimeBoard.</span><span class="sxs-lookup"><span data-stu-id="38093-211">When you click the RealtimeBoard tile in the Access Panel, you should get automatically signed-on to your RealtimeBoard application.</span></span>
<span data-ttu-id="38093-212">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="38093-212">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="38093-213">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="38093-213">Additional resources</span></span>

* [<span data-ttu-id="38093-214">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="38093-214">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="38093-215">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="38093-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-realtimeboard-tutorial/tutorial_general_203.png

