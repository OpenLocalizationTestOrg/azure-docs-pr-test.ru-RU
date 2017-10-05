---
title: "Руководство. Интеграция Azure Active Directory с Oneteam | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в Oneteam."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2e94916c-64ae-4e1a-a8b5-bc6ef7d28c29
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: c4381ca3166bd75bda1179b9a67b2224ba58ae68
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-oneteam"></a><span data-ttu-id="568ee-103">Руководство. Интеграция Azure Active Directory с Oneteam</span><span class="sxs-lookup"><span data-stu-id="568ee-103">Tutorial: Azure Active Directory integration with Oneteam</span></span>

<span data-ttu-id="568ee-104">В этом руководстве описано, как интегрировать Oneteam с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="568ee-104">In this tutorial, you learn how to integrate Oneteam with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="568ee-105">Интеграция Oneteam с Azure AD обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="568ee-105">Integrating Oneteam with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="568ee-106">С помощью Azure AD вы можете контролировать доступ к Oneteam.</span><span class="sxs-lookup"><span data-stu-id="568ee-106">You can control in Azure AD who has access to Oneteam</span></span>
- <span data-ttu-id="568ee-107">Вы можете включить автоматический вход пользователей в Oneteam (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="568ee-107">You can enable your users to automatically get signed-on to Oneteam (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="568ee-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="568ee-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="568ee-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="568ee-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="568ee-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="568ee-110">Prerequisites</span></span>

<span data-ttu-id="568ee-111">Чтобы настроить интеграцию Azure AD с Oneteam, вам потребуется следующее:</span><span class="sxs-lookup"><span data-stu-id="568ee-111">To configure Azure AD integration with Oneteam, you need the following items:</span></span>

- <span data-ttu-id="568ee-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="568ee-112">An Azure AD subscription</span></span>
- <span data-ttu-id="568ee-113">подписка Oneteam с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="568ee-113">A Oneteam single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="568ee-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="568ee-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="568ee-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="568ee-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="568ee-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="568ee-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="568ee-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="568ee-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="568ee-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="568ee-118">Scenario description</span></span>
<span data-ttu-id="568ee-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="568ee-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="568ee-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="568ee-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="568ee-121">Добавление Oneteam из коллекции</span><span class="sxs-lookup"><span data-stu-id="568ee-121">Adding Oneteam from the gallery</span></span>
2. <span data-ttu-id="568ee-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="568ee-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-oneteam-from-the-gallery"></a><span data-ttu-id="568ee-123">Добавление Oneteam из коллекции</span><span class="sxs-lookup"><span data-stu-id="568ee-123">Adding Oneteam from the gallery</span></span>
<span data-ttu-id="568ee-124">Чтобы настроить интеграцию Oneteam с Azure AD, необходимо добавить Oneteam из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="568ee-124">To configure the integration of Oneteam into Azure AD, you need to add Oneteam from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="568ee-125">**Чтобы добавить Oneteam из коллекции, выполните следующее.**</span><span class="sxs-lookup"><span data-stu-id="568ee-125">**To add Oneteam from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="568ee-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="568ee-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="568ee-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="568ee-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="568ee-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="568ee-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="568ee-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="568ee-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="568ee-133">В поле поиска введите **Oneteam**.</span><span class="sxs-lookup"><span data-stu-id="568ee-133">In the search box, type **Oneteam**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_search.png)

5. <span data-ttu-id="568ee-135">На панели результатов выберите **Oneteam** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="568ee-135">In the results panel, select **Oneteam**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="568ee-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="568ee-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="568ee-138">В этом разделе описана настройка и проверка единого входа Azure AD в Oneteam с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="568ee-138">In this section, you configure and test Azure AD single sign-on with Oneteam based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="568ee-139">Чтобы единый вход работал, Azure AD необходимо знать, какой пользователь в Oneteam соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="568ee-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Oneteam is to a user in Azure AD.</span></span> <span data-ttu-id="568ee-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Oneteam.</span><span class="sxs-lookup"><span data-stu-id="568ee-140">In other words, a link relationship between an Azure AD user and the related user in Oneteam needs to be established.</span></span>

<span data-ttu-id="568ee-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Oneteam.</span><span class="sxs-lookup"><span data-stu-id="568ee-141">In Oneteam, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="568ee-142">Чтобы настроить и проверить единый вход в Azure AD в Oneteam, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="568ee-142">To configure and test Azure AD single sign-on with Oneteam, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="568ee-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="568ee-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="568ee-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="568ee-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="568ee-145">**[Создание тестового пользователя Oneteam](#creating-a-oneteam-test-user)** требуется для того, чтобы в Oneteam существовал пользователь Britta Simon, связанный с соответствующим представлением в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="568ee-145">**[Creating a Oneteam test user](#creating-a-oneteam-test-user)** - to have a counterpart of Britta Simon in Oneteam that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="568ee-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="568ee-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="568ee-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="568ee-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="568ee-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="568ee-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="568ee-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Oneteam.</span><span class="sxs-lookup"><span data-stu-id="568ee-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Oneteam application.</span></span>

<span data-ttu-id="568ee-150">**Чтобы настроить единый вход Azure AD в Oneteam, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="568ee-150">**To configure Azure AD single sign-on with Oneteam, perform the following steps:**</span></span>

1. <span data-ttu-id="568ee-151">На портале Azure на странице интеграции с приложением **Oneteam** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="568ee-151">In the Azure portal, on the **Oneteam** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="568ee-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="568ee-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_samlbase.png)

3. <span data-ttu-id="568ee-155">Если вы хотите настроить приложение в **режиме, инициированном поставщиком удостоверений**, то в разделе **Домены и URL-адреса приложения Oneteam** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="568ee-155">On the **Oneteam Domain and URLs** section, if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_url.png)

    <span data-ttu-id="568ee-157">а.</span><span class="sxs-lookup"><span data-stu-id="568ee-157">a.</span></span> <span data-ttu-id="568ee-158">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://api.one-team.io/teams/<team name>`</span><span class="sxs-lookup"><span data-stu-id="568ee-158">In the **Identifier** textbox, type a URL using the following pattern: `https://api.one-team.io/teams/<team name>`</span></span>

    <span data-ttu-id="568ee-159">b.</span><span class="sxs-lookup"><span data-stu-id="568ee-159">b.</span></span> <span data-ttu-id="568ee-160">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате: `https://api.one-team.io/teams/<team name>/auth/saml/callback`.</span><span class="sxs-lookup"><span data-stu-id="568ee-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://api.one-team.io/teams/<team name>/auth/saml/callback`</span></span>

4. <span data-ttu-id="568ee-161">Установите флажок **Показать дополнительные параметры URL-адресов**, если вы хотите настроить приложение для работы в режиме, инициируемом **поставщиком услуг**.</span><span class="sxs-lookup"><span data-stu-id="568ee-161">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_url1.png)

    <span data-ttu-id="568ee-163">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<team name>.one-team.io/`</span><span class="sxs-lookup"><span data-stu-id="568ee-163">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<team name>.one-team.io/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="568ee-164">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="568ee-164">These values are not real.</span></span> <span data-ttu-id="568ee-165">Замените их фактическими значениями идентификатора, URL-адреса ответа и URL-адреса входа.</span><span class="sxs-lookup"><span data-stu-id="568ee-165">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="568ee-166">Чтобы получить их, обратитесь в [службу поддержки клиентов Oneteam](https://support.one-team.com/hc/requests/new).</span><span class="sxs-lookup"><span data-stu-id="568ee-166">Contact [Oneteam Client support team](https://support.one-team.com/hc/requests/new) to get these values.</span></span> 



5. <span data-ttu-id="568ee-167">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="568ee-167">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_certificate.png) 

6. <span data-ttu-id="568ee-169">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="568ee-169">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-oneteam-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="568ee-171">Чтобы настроить единый вход для своего приложения, вы можете отправить запрос в [службу поддержки Oneteam](https://support.one-team.com/hc/requests/new), добавив в него скачанный файл **метаданных**.</span><span class="sxs-lookup"><span data-stu-id="568ee-171">To get SSO configured for your application, you can raise the support ticket with [Oneteam support team](https://support.one-team.com/hc/requests/new) and provide them the downloaded **Metadata**.</span></span> 

> [!TIP]
> <span data-ttu-id="568ee-172">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="568ee-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="568ee-173">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="568ee-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="568ee-174">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="568ee-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="568ee-175">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="568ee-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="568ee-176">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="568ee-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="568ee-178">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="568ee-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="568ee-179">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="568ee-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-oneteam-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="568ee-181">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="568ee-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-oneteam-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="568ee-183">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="568ee-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-oneteam-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="568ee-185">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="568ee-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-oneteam-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="568ee-187">а.</span><span class="sxs-lookup"><span data-stu-id="568ee-187">a.</span></span> <span data-ttu-id="568ee-188">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="568ee-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="568ee-189">b.</span><span class="sxs-lookup"><span data-stu-id="568ee-189">b.</span></span> <span data-ttu-id="568ee-190">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="568ee-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="568ee-191">c.</span><span class="sxs-lookup"><span data-stu-id="568ee-191">c.</span></span> <span data-ttu-id="568ee-192">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="568ee-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="568ee-193">d.</span><span class="sxs-lookup"><span data-stu-id="568ee-193">d.</span></span> <span data-ttu-id="568ee-194">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="568ee-194">Click **Create**.</span></span>
 
### <a name="creating-a-oneteam-test-user"></a><span data-ttu-id="568ee-195">Создание тестового пользователя Oneteam</span><span class="sxs-lookup"><span data-stu-id="568ee-195">Creating a Oneteam test user</span></span>

<span data-ttu-id="568ee-196">Цель этого раздела — создать пользователя Britta Simon в Oneteam.</span><span class="sxs-lookup"><span data-stu-id="568ee-196">The objective of this section is to create a user called Britta Simon in Oneteam.</span></span> <span data-ttu-id="568ee-197">Приложение Oneteam поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="568ee-197">Oneteam supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="568ee-198">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="568ee-198">There is no action item for you in this section.</span></span> <span data-ttu-id="568ee-199">Пользователь будет создан при попытке получить доступ к Oneteam (если он еще не создан).</span><span class="sxs-lookup"><span data-stu-id="568ee-199">A new user will be created during an attempt to access Oneteam, if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="568ee-200">Если необходимо создать пользователя вручную, можно отправить запрос [службе поддержки Oneteam](https://support.one-team.com/hc/requests/new).</span><span class="sxs-lookup"><span data-stu-id="568ee-200">If you need to create an user manually, you can raise the support ticket with [Oneteam support team](https://support.one-team.com/hc/requests/new).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="568ee-201">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="568ee-201">Assigning the Azure AD test user</span></span>

<span data-ttu-id="568ee-202">В этом разделе описано, как предоставить пользователю Britta Simon доступ к Oneteam, чтобы он мог использовать единый вход Azure.</span><span class="sxs-lookup"><span data-stu-id="568ee-202">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Oneteam.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="568ee-204">**Чтобы назначить пользователя Britta Simon в Oneteam, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="568ee-204">**To assign Britta Simon to Oneteam, perform the following steps:**</span></span>

1. <span data-ttu-id="568ee-205">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="568ee-205">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="568ee-207">Из списка приложений выберите **Oneteam**.</span><span class="sxs-lookup"><span data-stu-id="568ee-207">In the applications list, select **Oneteam**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-oneteam-tutorial/tutorial_oneteam_app.png) 

3. <span data-ttu-id="568ee-209">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="568ee-209">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="568ee-211">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="568ee-211">Click **Add** button.</span></span> <span data-ttu-id="568ee-212">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="568ee-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="568ee-214">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="568ee-214">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="568ee-215">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="568ee-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="568ee-216">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="568ee-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="568ee-217">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="568ee-217">Testing single sign-on</span></span>

<span data-ttu-id="568ee-218">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="568ee-218">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="568ee-219">Щелкнув элемент Oneteam на панели доступа, вы автоматически войдете в приложение Oneteam.</span><span class="sxs-lookup"><span data-stu-id="568ee-219">When you click the Oneteam tile in the Access Panel, you should get automatically signed-on to your Oneteam application.</span></span>
<span data-ttu-id="568ee-220">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="568ee-220">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="568ee-221">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="568ee-221">Additional resources</span></span>

* [<span data-ttu-id="568ee-222">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="568ee-222">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="568ee-223">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="568ee-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-oneteam-tutorial/tutorial_general_203.png

