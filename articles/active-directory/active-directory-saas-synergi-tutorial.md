---
title: "Руководство по интеграции Azure Active Directory с Synergi | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в Synergi."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 73c970e1-f1ba-420b-b225-414fdf93b140
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: jeedes
ms.openlocfilehash: dedbe96fbb26bc34c4d7e213892b318f0e6fef12
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-synergi"></a><span data-ttu-id="29ce9-103">Руководство. Интеграция Azure Active Directory с Synergi</span><span class="sxs-lookup"><span data-stu-id="29ce9-103">Tutorial: Azure Active Directory integration with Synergi</span></span>

<span data-ttu-id="29ce9-104">В этом руководстве описано, как интегрировать Synergi с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="29ce9-104">In this tutorial, you learn how to integrate Synergi with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="29ce9-105">Интеграция Azure AD с Synergi обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="29ce9-105">Integrating Synergi with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="29ce9-106">С помощью Azure AD можно контролировать доступ к Synergi.</span><span class="sxs-lookup"><span data-stu-id="29ce9-106">You can control in Azure AD who has access to Synergi.</span></span>
- <span data-ttu-id="29ce9-107">Вы можете включить автоматический вход пользователей в Synergi (единый вход) с использованием учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="29ce9-107">You can enable your users to automatically get signed-on to Synergi (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="29ce9-108">Вы можете управлять учетными записями централизованно — на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="29ce9-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="29ce9-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="29ce9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="29ce9-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="29ce9-110">Prerequisites</span></span>

<span data-ttu-id="29ce9-111">Чтобы настроить интеграцию Azure AD с Synergi, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="29ce9-111">To configure Azure AD integration with Synergi, you need the following items:</span></span>

- <span data-ttu-id="29ce9-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="29ce9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="29ce9-113">подписка на Synergi с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="29ce9-113">A Synergi single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="29ce9-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="29ce9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="29ce9-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="29ce9-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="29ce9-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="29ce9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="29ce9-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="29ce9-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="29ce9-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="29ce9-118">Scenario description</span></span>
<span data-ttu-id="29ce9-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="29ce9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="29ce9-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="29ce9-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="29ce9-121">Добавление Synergi из коллекции.</span><span class="sxs-lookup"><span data-stu-id="29ce9-121">Adding Synergi from the gallery</span></span>
2. <span data-ttu-id="29ce9-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="29ce9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-synergi-from-the-gallery"></a><span data-ttu-id="29ce9-123">Добавление Synergi из коллекции.</span><span class="sxs-lookup"><span data-stu-id="29ce9-123">Adding Synergi from the gallery</span></span>
<span data-ttu-id="29ce9-124">Чтобы настроить интеграцию Synergi с Azure AD, необходимо добавить это приложение из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="29ce9-124">To configure the integration of Synergi into Azure AD, you need to add Synergi from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="29ce9-125">**Чтобы добавить Synergi из коллекции, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="29ce9-125">**To add Synergi from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="29ce9-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="29ce9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка "Azure Active Directory"][1]

2. <span data-ttu-id="29ce9-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="29ce9-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="29ce9-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="29ce9-129">Then go to **All applications**.</span></span>

    ![Колонка "Корпоративные приложения"][2]
    
3. <span data-ttu-id="29ce9-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="29ce9-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Кнопка "Новое приложение"][3]

4. <span data-ttu-id="29ce9-133">В поле поиска введите **Synergi**, выберите **Synergi** на панели результатов и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="29ce9-133">In the search box, type **Synergi**, select **Synergi** from result panel then click **Add** button to add the application.</span></span>

    ![Synergi в списке результатов](./media/active-directory-saas-synergi-tutorial/tutorial_synergi_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="29ce9-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="29ce9-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="29ce9-136">В этом разделе описана настройка и проверка единого входа Azure AD в Synergi с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="29ce9-136">In this section, you configure and test Azure AD single sign-on with Synergi based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="29ce9-137">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Synergi соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="29ce9-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Synergi is to a user in Azure AD.</span></span> <span data-ttu-id="29ce9-138">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Synergi.</span><span class="sxs-lookup"><span data-stu-id="29ce9-138">In other words, a link relationship between an Azure AD user and the related user in Synergi needs to be established.</span></span>

<span data-ttu-id="29ce9-139">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Synergi.</span><span class="sxs-lookup"><span data-stu-id="29ce9-139">In Synergi, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="29ce9-140">Чтобы настроить и проверить единый вход Azure AD в Synergi, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="29ce9-140">To configure and test Azure AD single sign-on with Synergi, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="29ce9-141">**[Настройка единого входа Azure AD](#configure-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="29ce9-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="29ce9-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="29ce9-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="29ce9-143">**[Создание тестового пользователя Synergi](#create-a-synergi-test-user)** требуется для создания пользователя Britta Simon в Synergi, связанного с соответствующим пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="29ce9-143">**[Create a Synergi test user](#create-a-synergi-test-user)** - to have a counterpart of Britta Simon in Synergi that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="29ce9-144">**[Назначение тестового пользователя Azure AD](#assign-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход Azure AD.</span><span class="sxs-lookup"><span data-stu-id="29ce9-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="29ce9-145">**[Проверка единого входа](#test-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="29ce9-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="29ce9-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="29ce9-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="29ce9-147">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Synergi.</span><span class="sxs-lookup"><span data-stu-id="29ce9-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Synergi application.</span></span>

<span data-ttu-id="29ce9-148">**Чтобы настроить единый вход Azure AD в Synergi, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="29ce9-148">**To configure Azure AD single sign-on with Synergi, perform the following steps:**</span></span>

1. <span data-ttu-id="29ce9-149">На портале Azure на странице интеграции с приложением **Synergi** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="29ce9-149">In the Azure portal, on the **Synergi** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="29ce9-151">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="29ce9-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-synergi-tutorial/tutorial_synergi_samlbase.png)

3. <span data-ttu-id="29ce9-153">В разделе **Домены и URL-адреса приложения Synergi** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="29ce9-153">On the **Synergi Domain and URLs** section, perform the following steps:</span></span>

    ![Сведения о домене и URL-адресах единого входа приложения Synergi](./media/active-directory-saas-synergi-tutorial/tutorial_synergi_url.png)

    <span data-ttu-id="29ce9-155">а.</span><span class="sxs-lookup"><span data-stu-id="29ce9-155">a.</span></span> <span data-ttu-id="29ce9-156">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<company name>.irmsecurity.com`</span><span class="sxs-lookup"><span data-stu-id="29ce9-156">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.irmsecurity.com`</span></span>

    <span data-ttu-id="29ce9-157">b.</span><span class="sxs-lookup"><span data-stu-id="29ce9-157">b.</span></span> <span data-ttu-id="29ce9-158">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате: `https://<company name>.irmsecurity.com/sso/<organization id>`.</span><span class="sxs-lookup"><span data-stu-id="29ce9-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.irmsecurity.com/sso/<organization id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="29ce9-159">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="29ce9-159">These values are not real.</span></span> <span data-ttu-id="29ce9-160">Измените их на фактические значения идентификатора и URL-адреса ответа.</span><span class="sxs-lookup"><span data-stu-id="29ce9-160">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="29ce9-161">Чтобы получить эти значения, обратитесь в [службу поддержки Synergi](https://www.irmsecurity.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="29ce9-161">Contact [Synergi support team](https://www.irmsecurity.com/contact/) to get these values.</span></span>

4. <span data-ttu-id="29ce9-162">В разделе **Сертификат подписи SAML** щелкните **Сертификат (Base64)**, а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="29ce9-162">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Ссылка для скачивания сертификата](./media/active-directory-saas-synergi-tutorial/tutorial_synergi_certificate.png) 

5. <span data-ttu-id="29ce9-164">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="29ce9-164">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-synergi-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="29ce9-166">В разделе **Настройка Synergi** щелкните **Настроить Synergi**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="29ce9-166">On the **Synergi Configuration** section, click **Configure Synergi** to open **Configure sign-on** window.</span></span> <span data-ttu-id="29ce9-167">Скопируйте **URL-адрес выхода и идентификатор сущности SAM** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="29ce9-167">Copy the **Sign-Out URL and SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![Настройка Synergi](./media/active-directory-saas-synergi-tutorial/tutorial_synergi_configure.png) 

7. <span data-ttu-id="29ce9-169">Чтобы настроить единый вход на стороне **Synergi**, необходимо отправить загруженный **сертификат (Base64), а также URL-адрес выхода и идентификатор сущности SAML** в [службу поддержки Synergi](https://www.irmsecurity.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="29ce9-169">To configure single sign-on on **Synergi** side, you need to send the downloaded **Certificate(Base64), Sign-Out URL, and SAML Entity ID** to [Synergi support team](https://www.irmsecurity.com/contact/).</span></span>

> [!TIP]
> <span data-ttu-id="29ce9-170">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="29ce9-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="29ce9-171">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="29ce9-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="29ce9-172">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="29ce9-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="29ce9-173">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="29ce9-173">Create an Azure AD test user</span></span>

<span data-ttu-id="29ce9-174">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="29ce9-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="29ce9-176">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="29ce9-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="29ce9-177">На портале Azure в области слева нажмите кнопку **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="29ce9-177">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Кнопка "Azure Active Directory"](./media/active-directory-saas-synergi-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="29ce9-179">Чтобы открыть список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="29ce9-179">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Ссылки "Пользователи и группы" и "Все пользователи"](./media/active-directory-saas-synergi-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="29ce9-181">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна **Все пользователи** щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="29ce9-181">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Кнопка "Добавить"](./media/active-directory-saas-synergi-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="29ce9-183">В диалоговом окне **Пользователь** сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="29ce9-183">In the **User** dialog box, perform the following steps:</span></span>

    ![Диалоговое окно "Пользователь"](./media/active-directory-saas-synergi-tutorial/create_aaduser_04.png)

    <span data-ttu-id="29ce9-185">а.</span><span class="sxs-lookup"><span data-stu-id="29ce9-185">a.</span></span> <span data-ttu-id="29ce9-186">В поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="29ce9-186">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="29ce9-187">b.</span><span class="sxs-lookup"><span data-stu-id="29ce9-187">b.</span></span> <span data-ttu-id="29ce9-188">В поле **Имя пользователя** введите адрес электронной почты для пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="29ce9-188">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="29ce9-189">c.</span><span class="sxs-lookup"><span data-stu-id="29ce9-189">c.</span></span> <span data-ttu-id="29ce9-190">Установите флажок **Показать пароль** и запишите значение, которое отображается в поле **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="29ce9-190">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="29ce9-191">г)</span><span class="sxs-lookup"><span data-stu-id="29ce9-191">d.</span></span> <span data-ttu-id="29ce9-192">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="29ce9-192">Click **Create**.</span></span>
  
### <a name="create-a-synergi-test-user"></a><span data-ttu-id="29ce9-193">Создание тестового пользователя Synergi</span><span class="sxs-lookup"><span data-stu-id="29ce9-193">Create a Synergi test user</span></span>

<span data-ttu-id="29ce9-194">В этом разделе описано, как создать пользователя Britta Simon в приложении Synergi.</span><span class="sxs-lookup"><span data-stu-id="29ce9-194">In this section, you create a user called Britta Simon in Synergi.</span></span> <span data-ttu-id="29ce9-195">Обратитесь в [службу поддержки Synergi](https://www.irmsecurity.com/contact/), чтобы добавить пользователей на платформу Synergi.</span><span class="sxs-lookup"><span data-stu-id="29ce9-195">Work with [Synergi support team](https://www.irmsecurity.com/contact/) to add the users in the Synergi platform.</span></span> <span data-ttu-id="29ce9-196">Перед использованием единого входа необходимо создать и активировать пользователей.</span><span class="sxs-lookup"><span data-stu-id="29ce9-196">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="29ce9-197">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="29ce9-197">Assign the Azure AD test user</span></span>

<span data-ttu-id="29ce9-198">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к Synergi.</span><span class="sxs-lookup"><span data-stu-id="29ce9-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Synergi.</span></span>

![Назначение роли пользователя][200] 

<span data-ttu-id="29ce9-200">**Чтобы назначить пользователя Britta Simon в Synergi, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="29ce9-200">**To assign Britta Simon to Synergi, perform the following steps:**</span></span>

1. <span data-ttu-id="29ce9-201">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="29ce9-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="29ce9-203">В списке приложений выберите **Synergi**.</span><span class="sxs-lookup"><span data-stu-id="29ce9-203">In the applications list, select **Synergi**.</span></span>

    ![Ссылка на Synergi в списке "Приложения"](./media/active-directory-saas-synergi-tutorial/tutorial_synergi_app.png)  

3. <span data-ttu-id="29ce9-205">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="29ce9-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Ссылка "Пользователи и группы"][202]

4. <span data-ttu-id="29ce9-207">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="29ce9-207">Click **Add** button.</span></span> <span data-ttu-id="29ce9-208">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="29ce9-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Область "Добавление назначения"][203]

5. <span data-ttu-id="29ce9-210">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="29ce9-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="29ce9-211">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="29ce9-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="29ce9-212">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="29ce9-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="29ce9-213">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="29ce9-213">Test single sign-on</span></span>

<span data-ttu-id="29ce9-214">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="29ce9-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="29ce9-215">Щелкнув плитку Synergi на панели доступа, вы автоматически войдете в приложение Synergi.</span><span class="sxs-lookup"><span data-stu-id="29ce9-215">When you click the Synergi tile in the Access Panel, you should get automatically signed-on to your Synergi application.</span></span>
<span data-ttu-id="29ce9-216">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="29ce9-216">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="29ce9-217">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="29ce9-217">Additional resources</span></span>

* [<span data-ttu-id="29ce9-218">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="29ce9-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="29ce9-219">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="29ce9-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-synergi-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-synergi-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-synergi-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-synergi-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-synergi-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-synergi-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-synergi-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-synergi-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-synergi-tutorial/tutorial_general_203.png

