---
title: "Руководство по интеграции Azure Active Directory с Wikispaces | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в Wikispaces."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 665b95aa-f7f5-4406-9e2a-6fc299a1599c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: d01543955bdf6a274571f67eafdff5f637863d5c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-wikispaces"></a><span data-ttu-id="dfb4b-103">Руководство. Интеграция Azure Active Directory с Wikispaces</span><span class="sxs-lookup"><span data-stu-id="dfb4b-103">Tutorial: Azure Active Directory integration with Wikispaces</span></span>

<span data-ttu-id="dfb4b-104">В этом руководстве описано, как интегрировать приложение Wikispaces с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="dfb4b-104">In this tutorial, you learn how to integrate Wikispaces with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="dfb4b-105">Интеграция Azure AD с приложением Wikispaces обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="dfb4b-105">Integrating Wikispaces with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="dfb4b-106">С помощью Azure AD вы можете контролировать доступ к Wikispaces.</span><span class="sxs-lookup"><span data-stu-id="dfb4b-106">You can control in Azure AD who has access to Wikispaces</span></span>
- <span data-ttu-id="dfb4b-107">Вы можете включить автоматический вход пользователей в Wikispaces (единый вход) с применением учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dfb4b-107">You can enable your users to automatically get signed-on to Wikispaces (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="dfb4b-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="dfb4b-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="dfb4b-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="dfb4b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dfb4b-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="dfb4b-110">Prerequisites</span></span>

<span data-ttu-id="dfb4b-111">Чтобы настроить интеграцию Azure AD с Wikispaces, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="dfb4b-111">To configure Azure AD integration with Wikispaces, you need the following items:</span></span>

- <span data-ttu-id="dfb4b-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="dfb4b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="dfb4b-113">Подписка Wikispaces с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="dfb4b-113">A Wikispaces single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="dfb4b-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="dfb4b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="dfb4b-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="dfb4b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="dfb4b-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="dfb4b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="dfb4b-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="dfb4b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="dfb4b-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="dfb4b-118">Scenario description</span></span>
<span data-ttu-id="dfb4b-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="dfb4b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="dfb4b-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="dfb4b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="dfb4b-121">Добавление Wikispaces из коллекции.</span><span class="sxs-lookup"><span data-stu-id="dfb4b-121">Adding Wikispaces from the gallery</span></span>
2. <span data-ttu-id="dfb4b-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="dfb4b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-wikispaces-from-the-gallery"></a><span data-ttu-id="dfb4b-123">Добавление Wikispaces из коллекции</span><span class="sxs-lookup"><span data-stu-id="dfb4b-123">Adding Wikispaces from the gallery</span></span>
<span data-ttu-id="dfb4b-124">Чтобы настроить интеграцию Wikispaces с Azure AD, необходимо добавить Wikispaces из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="dfb4b-124">To configure the integration of Wikispaces into Azure AD, you need to add Wikispaces from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="dfb4b-125">**Чтобы добавить Wikispaces из коллекции, сделайте следующее.**</span><span class="sxs-lookup"><span data-stu-id="dfb4b-125">**To add Wikispaces from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="dfb4b-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="dfb4b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="dfb4b-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="dfb4b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="dfb4b-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="dfb4b-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="dfb4b-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="dfb4b-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="dfb4b-133">В поле поиска введите **Wikispaces**.</span><span class="sxs-lookup"><span data-stu-id="dfb4b-133">In the search box, type **Wikispaces**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_search.png)

5. <span data-ttu-id="dfb4b-135">На панели результатов выберите **Wikispaces** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="dfb4b-135">In the results panel, select **Wikispaces**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="dfb4b-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="dfb4b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="dfb4b-138">В этом разделе описана настройка и проверка единого входа Azure AD в Wikispaces с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dfb4b-138">In this section, you configure and test Azure AD single sign-on with Wikispaces based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="dfb4b-139">Чтобы единый вход работал, Azure AD необходима информация о том, какой пользователь в Wikispaces соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dfb4b-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Wikispaces is to a user in Azure AD.</span></span> <span data-ttu-id="dfb4b-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Wikispaces.</span><span class="sxs-lookup"><span data-stu-id="dfb4b-140">In other words, a link relationship between an Azure AD user and the related user in Wikispaces needs to be established.</span></span>

<span data-ttu-id="dfb4b-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Wikispaces.</span><span class="sxs-lookup"><span data-stu-id="dfb4b-141">In Wikispaces, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="dfb4b-142">Чтобы настроить и проверить единый вход Azure AD в Wikispaces, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="dfb4b-142">To configure and test Azure AD single sign-on with Wikispaces, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="dfb4b-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="dfb4b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="dfb4b-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dfb4b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="dfb4b-145">**[Создание тестового пользователя Wikispaces](#creating-a-wikispaces-test-user)** требуется для того, чтобы в Wikispaces существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dfb4b-145">**[Creating a Wikispaces test user](#creating-a-wikispaces-test-user)** - to have a counterpart of Britta Simon in Wikispaces that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="dfb4b-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dfb4b-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="dfb4b-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="dfb4b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="dfb4b-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="dfb4b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="dfb4b-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Wikispaces.</span><span class="sxs-lookup"><span data-stu-id="dfb4b-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Wikispaces application.</span></span>

<span data-ttu-id="dfb4b-150">**Чтобы настроить единый вход Azure AD в Wikispaces, сделайте следующее.**</span><span class="sxs-lookup"><span data-stu-id="dfb4b-150">**To configure Azure AD single sign-on with Wikispaces, perform the following steps:**</span></span>

1. <span data-ttu-id="dfb4b-151">На портале Azure на странице интеграции с приложением **Wikispaces** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="dfb4b-151">In the Azure portal, on the **Wikispaces** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="dfb4b-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="dfb4b-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_samlbase.png)

3. <span data-ttu-id="dfb4b-155">В разделе **Домены и URL-адреса приложения Wikispaces** сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="dfb4b-155">On the **Wikispaces Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_url.png)

    <span data-ttu-id="dfb4b-157">а.</span><span class="sxs-lookup"><span data-stu-id="dfb4b-157">a.</span></span> <span data-ttu-id="dfb4b-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<companyname>.wikispaces.net`</span><span class="sxs-lookup"><span data-stu-id="dfb4b-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.wikispaces.net`</span></span>

    <span data-ttu-id="dfb4b-159">b.</span><span class="sxs-lookup"><span data-stu-id="dfb4b-159">b.</span></span> <span data-ttu-id="dfb4b-160">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://session.wikispaces.net/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="dfb4b-160">In the **Identifier** textbox, type a URL using the following pattern: `https://session.wikispaces.net/<instancename>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="dfb4b-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="dfb4b-161">These values are not real.</span></span> <span data-ttu-id="dfb4b-162">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="dfb4b-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="dfb4b-163">Чтобы получить эти значения, обратитесь к [группе поддержки клиентов Wikispaces](https://www.wikispaces.com/site/help).</span><span class="sxs-lookup"><span data-stu-id="dfb4b-163">Contact [Wikispaces Client support team](https://www.wikispaces.com/site/help) to get these values.</span></span> 

4. <span data-ttu-id="dfb4b-164">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="dfb4b-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_certificate.png) 

5. <span data-ttu-id="dfb4b-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="dfb4b-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-wikispaces-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="dfb4b-168">Чтобы настроить единый вход на стороне **Wikispaces**, отправьте [группе поддержки Wikispaces](https://www.wikispaces.com/site/help) скачанный **XML-файл метаданных**.</span><span class="sxs-lookup"><span data-stu-id="dfb4b-168">To configure single sign-on on **Wikispaces** side, you need to send the downloaded **Metadata XML** to [Wikispaces support team](https://www.wikispaces.com/site/help).</span></span> <span data-ttu-id="dfb4b-169">Сразу же после завершения настройки вы получите уведомление.</span><span class="sxs-lookup"><span data-stu-id="dfb4b-169">You will get a notification as soon as the configuration has been completed.</span></span>

> [!TIP]
> <span data-ttu-id="dfb4b-170">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="dfb4b-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="dfb4b-171">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="dfb4b-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="dfb4b-172">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="dfb4b-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="dfb4b-173">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="dfb4b-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="dfb4b-174">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dfb4b-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="dfb4b-176">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="dfb4b-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="dfb4b-177">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="dfb4b-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-wikispaces-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="dfb4b-179">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="dfb4b-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-wikispaces-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="dfb4b-181">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="dfb4b-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-wikispaces-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="dfb4b-183">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="dfb4b-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-wikispaces-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="dfb4b-185">а.</span><span class="sxs-lookup"><span data-stu-id="dfb4b-185">a.</span></span> <span data-ttu-id="dfb4b-186">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="dfb4b-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="dfb4b-187">b.</span><span class="sxs-lookup"><span data-stu-id="dfb4b-187">b.</span></span> <span data-ttu-id="dfb4b-188">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="dfb4b-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="dfb4b-189">c.</span><span class="sxs-lookup"><span data-stu-id="dfb4b-189">c.</span></span> <span data-ttu-id="dfb4b-190">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="dfb4b-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="dfb4b-191">d.</span><span class="sxs-lookup"><span data-stu-id="dfb4b-191">d.</span></span> <span data-ttu-id="dfb4b-192">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="dfb4b-192">Click **Create**.</span></span>
 
### <a name="creating-a-wikispaces-test-user"></a><span data-ttu-id="dfb4b-193">Создание тестового пользователя Wikispaces</span><span class="sxs-lookup"><span data-stu-id="dfb4b-193">Creating a Wikispaces test user</span></span>

<span data-ttu-id="dfb4b-194">Чтобы пользователи Azure AD могли выполнять вход в Wikispaces, они должны быть подготовлены в Wikispaces.</span><span class="sxs-lookup"><span data-stu-id="dfb4b-194">In order to enable Azure AD users to log in to Wikispaces, they must be provisioned into Wikispaces.</span></span> <span data-ttu-id="dfb4b-195">В случае использования Wikispaces подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="dfb4b-195">In the case of Wikispaces, provisioning is a manual task.</span></span>

### <a name="to-provision-a-user-accounts-perform-the-following-steps"></a><span data-ttu-id="dfb4b-196">Чтобы подготовить учетные записи пользователей, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="dfb4b-196">To provision a user accounts, perform the following steps:</span></span>
1. <span data-ttu-id="dfb4b-197">Выполните вход на сайт компании **Wikispaces** в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="dfb4b-197">Log in to your **Wikispaces** company site as an administrator.</span></span>

2. <span data-ttu-id="dfb4b-198">Перейдите в раздел **Участники**.</span><span class="sxs-lookup"><span data-stu-id="dfb4b-198">Go to **Members**.</span></span>
   
    <span data-ttu-id="dfb4b-199">![Участники](./media/active-directory-saas-wikispaces-tutorial/ic787193.png "Участники")</span><span class="sxs-lookup"><span data-stu-id="dfb4b-199">![Members](./media/active-directory-saas-wikispaces-tutorial/ic787193.png "Members")</span></span>

3. <span data-ttu-id="dfb4b-200">Щелкните **Пригласить пользователей**.</span><span class="sxs-lookup"><span data-stu-id="dfb4b-200">Click the **Invite People**.</span></span>
   
    <span data-ttu-id="dfb4b-201">![Приглашение участников](./media/active-directory-saas-wikispaces-tutorial/ic787194.png "приглашение участников")</span><span class="sxs-lookup"><span data-stu-id="dfb4b-201">![Invite People](./media/active-directory-saas-wikispaces-tutorial/ic787194.png "Invite People")</span></span>

4. <span data-ttu-id="dfb4b-202">В разделе **Пригласить пользователей** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="dfb4b-202">In the **Invite People** section, perform the following steps:</span></span>
   
    <span data-ttu-id="dfb4b-203">![Приглашение участников](./media/active-directory-saas-wikispaces-tutorial/ic787208.png "приглашение участников")</span><span class="sxs-lookup"><span data-stu-id="dfb4b-203">![Invite People](./media/active-directory-saas-wikispaces-tutorial/ic787208.png "Invite People")</span></span>
   
    <span data-ttu-id="dfb4b-204">а.</span><span class="sxs-lookup"><span data-stu-id="dfb4b-204">a.</span></span> <span data-ttu-id="dfb4b-205">Введите **имя пользователя или электронный адрес** для действующей учетной записи AAD, которую вы хотите подготовить, в соответствующие текстовые поля.</span><span class="sxs-lookup"><span data-stu-id="dfb4b-205">Type the **Usernames or Email Address** of a valid AAD account you want to provision into the related textboxes.</span></span>
   
    <span data-ttu-id="dfb4b-206">b.</span><span class="sxs-lookup"><span data-stu-id="dfb4b-206">b.</span></span> <span data-ttu-id="dfb4b-207">Нажмите кнопку **Send**(Отправить).</span><span class="sxs-lookup"><span data-stu-id="dfb4b-207">Click **Send**.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="dfb4b-208">Владелец учетной записи Azure Active Directory получит электронное сообщение со ссылкой для подтверждения учетной записи перед ее активацией.</span><span class="sxs-lookup"><span data-stu-id="dfb4b-208">The Azure Active Directory account holder receives an email including a link to confirm the account before it becomes active.</span></span>
    
> [!NOTE]
> <span data-ttu-id="dfb4b-209">Вы можете использовать любые другие средства создания учетной записи пользователя Wikispaces или API-интерфейсы, предоставляемые Wikispaces, для подготовки учетных записей пользователей AAD.</span><span class="sxs-lookup"><span data-stu-id="dfb4b-209">You can use any other Wikispaces user account creation tools or APIs provided by Wikispaces to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="dfb4b-210">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="dfb4b-210">Assigning the Azure AD test user</span></span>

<span data-ttu-id="dfb4b-211">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к Wikispaces.</span><span class="sxs-lookup"><span data-stu-id="dfb4b-211">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Wikispaces.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="dfb4b-213">**Чтобы назначить пользователя Britta Simon в Wikispaces, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="dfb4b-213">**To assign Britta Simon to Wikispaces, perform the following steps:**</span></span>

1. <span data-ttu-id="dfb4b-214">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="dfb4b-214">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="dfb4b-216">Из списка приложений выберите **Wikispaces**.</span><span class="sxs-lookup"><span data-stu-id="dfb4b-216">In the applications list, select **Wikispaces**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-wikispaces-tutorial/tutorial_wikispaces_app.png) 

3. <span data-ttu-id="dfb4b-218">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="dfb4b-218">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="dfb4b-220">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="dfb4b-220">Click **Add** button.</span></span> <span data-ttu-id="dfb4b-221">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="dfb4b-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="dfb4b-223">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="dfb4b-223">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="dfb4b-224">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="dfb4b-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="dfb4b-225">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="dfb4b-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="dfb4b-226">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="dfb4b-226">Testing single sign-on</span></span>

<span data-ttu-id="dfb4b-227">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="dfb4b-227">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="dfb4b-228">Щелкнув элемент "Wikispaces" на панели доступа, вы автоматически войдете в приложение Wikispaces.</span><span class="sxs-lookup"><span data-stu-id="dfb4b-228">When you click the Wikispaces tile in the Access Panel, you should get automatically signed-on to your Wikispaces application.</span></span>
<span data-ttu-id="dfb4b-229">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="dfb4b-229">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="dfb4b-230">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="dfb4b-230">Additional resources</span></span>

* [<span data-ttu-id="dfb4b-231">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dfb4b-231">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="dfb4b-232">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="dfb4b-232">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-wikispaces-tutorial/tutorial_general_203.png

