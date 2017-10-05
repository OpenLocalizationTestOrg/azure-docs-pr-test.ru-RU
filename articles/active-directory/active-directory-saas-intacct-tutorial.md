---
title: "Учебник. Интеграция Azure Active Directory с Intacct | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в Intacct."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 92518e02-a62c-4b1b-a8e9-2803eb2b49ac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: c203b192b9da0d280cbd7f6c123219242ee4a3d1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-intacct"></a><span data-ttu-id="5ebb0-103">Руководство. Интеграция Azure Active Directory с Intacct</span><span class="sxs-lookup"><span data-stu-id="5ebb0-103">Tutorial: Azure Active Directory integration with Intacct</span></span>

<span data-ttu-id="5ebb0-104">В этом руководстве описано, как интегрировать Intacct с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5ebb0-104">In this tutorial, you learn how to integrate Intacct with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5ebb0-105">Интеграция Azure AD с приложением Intacct обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="5ebb0-105">Integrating Intacct with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5ebb0-106">С помощью Azure AD вы можете контролировать доступ к Intacct.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-106">You can control in Azure AD who has access to Intacct</span></span>
- <span data-ttu-id="5ebb0-107">Вы можете включить автоматический вход пользователей в Intacct (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-107">You can enable your users to automatically get signed-on to Intacct (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5ebb0-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="5ebb0-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5ebb0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5ebb0-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="5ebb0-110">Prerequisites</span></span>

<span data-ttu-id="5ebb0-111">Чтобы настроить интеграцию Azure AD с Intacct, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="5ebb0-111">To configure Azure AD integration with Intacct, you need the following items:</span></span>

- <span data-ttu-id="5ebb0-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="5ebb0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5ebb0-113">подписка с поддержкой единого входа Intacct.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-113">An Intacct single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5ebb0-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5ebb0-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="5ebb0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5ebb0-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5ebb0-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5ebb0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5ebb0-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="5ebb0-118">Scenario description</span></span>
<span data-ttu-id="5ebb0-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5ebb0-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="5ebb0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5ebb0-121">Добавление Intacct из коллекции</span><span class="sxs-lookup"><span data-stu-id="5ebb0-121">Adding Intacct from the gallery</span></span>
2. <span data-ttu-id="5ebb0-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="5ebb0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-intacct-from-the-gallery"></a><span data-ttu-id="5ebb0-123">Добавление Intacct из коллекции</span><span class="sxs-lookup"><span data-stu-id="5ebb0-123">Adding Intacct from the gallery</span></span>
<span data-ttu-id="5ebb0-124">Чтобы настроить интеграцию Intacct с Azure AD, необходимо добавить Intacct из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-124">To configure the integration of Intacct into Azure AD, you need to add Intacct from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5ebb0-125">**Чтобы добавить Intacct из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="5ebb0-125">**To add Intacct from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5ebb0-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5ebb0-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5ebb0-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="5ebb0-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="5ebb0-133">В поле поиска введите **Intacct**.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-133">In the search box, type **Intacct**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_search.png)

5. <span data-ttu-id="5ebb0-135">На панели результатов выберите **Intacct** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-135">In the results panel, select **Intacct**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5ebb0-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="5ebb0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5ebb0-138">В этом разделе описана настройка и проверка единого входа Azure AD в Intacct с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-138">In this section, you configure and test Azure AD single sign-on with Intacct based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5ebb0-139">Чтобы единый вход работал, Azure AD необходимо знать, какой пользователь в Intacct соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Intacct is to a user in Azure AD.</span></span> <span data-ttu-id="5ebb0-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Intacct.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-140">In other words, a link relationship between an Azure AD user and the related user in Intacct needs to be established.</span></span>

<span data-ttu-id="5ebb0-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Intacct.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-141">In Intacct, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="5ebb0-142">Чтобы настроить и проверить единый вход Azure AD в Intacct, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="5ebb0-142">To configure and test Azure AD single sign-on with Intacct, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5ebb0-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5ebb0-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5ebb0-145">**[Создание тестового пользователя Intacct](#creating-an-intacct-test-user)** требуется для создания пользователя Britta Simon в Intacct, связанного с соответствующим представлением в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-145">**[Creating an Intacct test user](#creating-an-intacct-test-user)** - to have a counterpart of Britta Simon in Intacct that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="5ebb0-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5ebb0-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5ebb0-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="5ebb0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5ebb0-149">В данном разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Intacct.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Intacct application.</span></span>

<span data-ttu-id="5ebb0-150">**Чтобы настроить единый вход Azure AD в Intacct, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="5ebb0-150">**To configure Azure AD single sign-on with Intacct, perform the following steps:**</span></span>

1. <span data-ttu-id="5ebb0-151">На портале Azure на странице интеграции с приложением **Intacct** выберите **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-151">In the Azure portal, on the **Intacct** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="5ebb0-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_samlbase.png)

3. <span data-ttu-id="5ebb0-155">В разделе **Домены и URL-адреса приложения Intacct** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="5ebb0-155">On the **Intacct Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_url.png)

    <span data-ttu-id="5ebb0-157">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="5ebb0-157">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.intacct.com/ia/acct/sso_response.phtml`|
    | `https://www.intacct.com/ia/acct/sso_response.phtml` |

    > [!NOTE] 
    > <span data-ttu-id="5ebb0-158">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-158">This value is not real.</span></span> <span data-ttu-id="5ebb0-159">Вместо него нужно указать фактический URL-адрес ответа.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-159">Update this value with the actual Reply URL.</span></span> <span data-ttu-id="5ebb0-160">Чтобы получить эти значения, обратитесь в [службу поддержки Intacct](https://us.intacct.com/support).</span><span class="sxs-lookup"><span data-stu-id="5ebb0-160">Contact [Intacct support team](https://us.intacct.com/support) to get this value.</span></span>

4. <span data-ttu-id="5ebb0-161">В разделе **Сертификат подписи SAML** щелкните **Сертификат (Base64)**, а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_certificate.png) 

5. <span data-ttu-id="5ebb0-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="5ebb0-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-intacct-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5ebb0-165">В разделе **Конфигурация Intacct** щелкните **Настроить Intacct**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-165">On the **Intacct Configuration** section, click **Configure Intacct** to open **Configure sign-on** window.</span></span> <span data-ttu-id="5ebb0-166">Скопируйте **идентификатор сущности SAML и URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-166">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_configure.png) 

7. <span data-ttu-id="5ebb0-168">В другом окне веб-браузера войдите на корпоративный сайт Intacct в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-168">In a different web browser window, sign in to your Intacct company site as an administrator.</span></span>

8. <span data-ttu-id="5ebb0-169">Откройте вкладку **Company** (Компания) и выберите **Company Info** (Сведения о компании).</span><span class="sxs-lookup"><span data-stu-id="5ebb0-169">Click the **Company** tab, and then click **Company Info**.</span></span>

    <span data-ttu-id="5ebb0-170">![Организация](./media/active-directory-saas-intacct-tutorial/ic790037.png "Организация")</span><span class="sxs-lookup"><span data-stu-id="5ebb0-170">![Company](./media/active-directory-saas-intacct-tutorial/ic790037.png "Company")</span></span>

9. <span data-ttu-id="5ebb0-171">Откройте вкладку **Security** (Безопасность) и нажмите кнопку **Edit** (Изменить).</span><span class="sxs-lookup"><span data-stu-id="5ebb0-171">Click the **Security** tab, and then click **Edit**.</span></span>

    <span data-ttu-id="5ebb0-172">![Безопасность](./media/active-directory-saas-intacct-tutorial/ic790038.png "Безопасность")</span><span class="sxs-lookup"><span data-stu-id="5ebb0-172">![Security](./media/active-directory-saas-intacct-tutorial/ic790038.png "Security")</span></span>

10. <span data-ttu-id="5ebb0-173">В разделе **Единый вход** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="5ebb0-173">In the **Single sign on (SSO)** section, perform the following steps:</span></span>

    <span data-ttu-id="5ebb0-174">![Единый вход](./media/active-directory-saas-intacct-tutorial/ic790039.png "Единый вход")</span><span class="sxs-lookup"><span data-stu-id="5ebb0-174">![Single sign on](./media/active-directory-saas-intacct-tutorial/ic790039.png "single sign on")</span></span>

    <span data-ttu-id="5ebb0-175">а.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-175">a.</span></span> <span data-ttu-id="5ebb0-176">Установите флажок **Включить единый вход**.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-176">Select **Enable single sign on**.</span></span>

    <span data-ttu-id="5ebb0-177">b.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-177">b.</span></span> <span data-ttu-id="5ebb0-178">Выберите для параметра **Identity provider type** (Тип поставщика удостоверений) значение **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-178">As **Identity provider type**, select **SAML 2.0**.</span></span>

    <span data-ttu-id="5ebb0-179">c.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-179">c.</span></span> <span data-ttu-id="5ebb0-180">В текстовое поле **URL-адрес издателя** вставьте значение **идентификатора сущности SAML**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-180">In **Issuer URL** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="5ebb0-181">г)</span><span class="sxs-lookup"><span data-stu-id="5ebb0-181">d.</span></span> <span data-ttu-id="5ebb0-182">В текстовое поле **URL-адрес входа** вставьте значение **URL-адреса службы единого входа SAML**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-182">In **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="5ebb0-183">д.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-183">e.</span></span> <span data-ttu-id="5ebb0-184">Откройте в блокноте **сертификат в кодировке Base-64**, скопируйте его содержимое в буфер обмена, а затем вставьте его в поле **Сертификат**.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-184">Open your **base-64** encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **Certificate** box.</span></span>
   
    <span data-ttu-id="5ebb0-185">f.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-185">f.</span></span> <span data-ttu-id="5ebb0-186">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-186">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="5ebb0-187">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-187">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="5ebb0-188">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-188">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="5ebb0-189">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="5ebb0-189">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5ebb0-190">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="5ebb0-190">Creating an Azure AD test user</span></span>
<span data-ttu-id="5ebb0-191">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-191">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="5ebb0-193">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="5ebb0-193">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5ebb0-194">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-194">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-intacct-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5ebb0-196">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-196">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-intacct-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5ebb0-198">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-198">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-intacct-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5ebb0-200">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-200">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-intacct-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5ebb0-202">а.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-202">a.</span></span> <span data-ttu-id="5ebb0-203">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-203">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5ebb0-204">b.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-204">b.</span></span> <span data-ttu-id="5ebb0-205">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-205">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5ebb0-206">c.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-206">c.</span></span> <span data-ttu-id="5ebb0-207">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-207">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="5ebb0-208">d.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-208">d.</span></span> <span data-ttu-id="5ebb0-209">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-209">Click **Create**.</span></span>
 
### <a name="creating-an-intacct-test-user"></a><span data-ttu-id="5ebb0-210">Создание тестового пользователя Intacct</span><span class="sxs-lookup"><span data-stu-id="5ebb0-210">Creating an Intacct test user</span></span>

<span data-ttu-id="5ebb0-211">Чтобы пользователи Azure AD могли входить в Intacct, их необходимо подготовить для Intacct.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-211">To set up Azure AD users so they can sign in to Intacct, they must be provisioned into Intacct.</span></span> <span data-ttu-id="5ebb0-212">Эта подготовка для Intacct выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-212">For Intacct, provisioning is a manual task.</span></span>

<span data-ttu-id="5ebb0-213">**Чтобы подготовить учетные записи пользователей, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="5ebb0-213">**To provision user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="5ebb0-214">Войдите в клиент **Intacct**.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-214">Sign in to your **Intacct** tenant.</span></span>

2. <span data-ttu-id="5ebb0-215">Откройте вкладку **Company** (Компания) и выберите **Users** (Пользователи).</span><span class="sxs-lookup"><span data-stu-id="5ebb0-215">Click the **Company** tab, and then click **Users**.</span></span>

    <span data-ttu-id="5ebb0-216">![Пользователи](./media/active-directory-saas-intacct-tutorial/ic790041.png "Пользователи")</span><span class="sxs-lookup"><span data-stu-id="5ebb0-216">![Users](./media/active-directory-saas-intacct-tutorial/ic790041.png "Users")</span></span>
3. <span data-ttu-id="5ebb0-217">Откройте вкладку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-217">Click the **Add** tab.</span></span>

    <span data-ttu-id="5ebb0-218">![Добавление](./media/active-directory-saas-intacct-tutorial/ic790042.png "Добавление")</span><span class="sxs-lookup"><span data-stu-id="5ebb0-218">![Add](./media/active-directory-saas-intacct-tutorial/ic790042.png "Add")</span></span>
4. <span data-ttu-id="5ebb0-219">В разделе **Информация о пользователе** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="5ebb0-219">In the **User Information** section, perform the following steps:</span></span>

    <span data-ttu-id="5ebb0-220">![Сведения о пользователе](./media/active-directory-saas-intacct-tutorial/ic790043.png "Сведения о пользователе")</span><span class="sxs-lookup"><span data-stu-id="5ebb0-220">![User Information](./media/active-directory-saas-intacct-tutorial/ic790043.png "User Information")</span></span>

    <span data-ttu-id="5ebb0-221">а.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-221">a.</span></span> <span data-ttu-id="5ebb0-222">В разделе **User Information** (Сведения пользователя) введите значения **User ID** (Идентификатор пользователя), **Last Name** (Фамилия), **First name** (Имя), **Email address** (Адрес электронной почты), **Title** (Обращение) и **Phone** (Телефон) учетной записи Azure AD, которую вы хотите подготовить.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-222">Enter the **User ID**, the **Last name**, **First name**, the **Email address**, the **Title**, and the **Phone** of an Azure AD account that you want to provision into the **User Information** section.</span></span>

    <span data-ttu-id="5ebb0-223">b.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-223">b.</span></span> <span data-ttu-id="5ebb0-224">Выберите параметр **Полномочия администратора** для учетной записи Azure AD, которую требуется подготовить.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-224">Select the **Admin privileges** of an Azure AD account that you want to provision.</span></span>
   
    <span data-ttu-id="5ebb0-225">c.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-225">c.</span></span> <span data-ttu-id="5ebb0-226">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-226">Click **Save**.</span></span> <span data-ttu-id="5ebb0-227">Владелец учетной записи Azure AD получит по электронной почте сообщение со ссылкой для активации учетной записи.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-227">The Azure AD account holder receives an email and follows a link to confirm their account before it becomes active.</span></span>

>[!NOTE]
><span data-ttu-id="5ebb0-228">Для подготовки учетных записей пользователя Azure AD вы можете использовать любые другие средства создания учетной записи пользователя Intacct или API, предоставляемые Intacct.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-228">To provision Azure AD user accounts, you can use other Intacct user account creation tools or APIs that are provided by Intacct.</span></span>
        
### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="5ebb0-229">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="5ebb0-229">Assigning the Azure AD test user</span></span>

<span data-ttu-id="5ebb0-230">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив ему доступ к Intacct.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-230">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Intacct.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="5ebb0-232">**Чтобы назначить пользователя Britta Simon в Intacct, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="5ebb0-232">**To assign Britta Simon to Intacct, perform the following steps:**</span></span>

1. <span data-ttu-id="5ebb0-233">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-233">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="5ebb0-235">В списке приложений выберите **Intacct**.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-235">In the applications list, select **Intacct**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-intacct-tutorial/tutorial_intacct_app.png) 

3. <span data-ttu-id="5ebb0-237">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-237">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="5ebb0-239">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-239">Click **Add** button.</span></span> <span data-ttu-id="5ebb0-240">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-240">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="5ebb0-242">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-242">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5ebb0-243">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-243">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5ebb0-244">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-244">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5ebb0-245">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="5ebb0-245">Testing single sign-on</span></span>

<span data-ttu-id="5ebb0-246">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-246">In this section, you test your Azure AD single sign-on configuration by using the Access Panel.</span></span>

<span data-ttu-id="5ebb0-247">Если вы щелкните плитку Intacct на панели доступа, вы автоматически войдете в приложение Intacct.</span><span class="sxs-lookup"><span data-stu-id="5ebb0-247">When you click the Intacct tile in the Access Panel, you should be automatically signed in to your Intacct application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5ebb0-248">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="5ebb0-248">Additional resources</span></span>

* [<span data-ttu-id="5ebb0-249">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5ebb0-249">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5ebb0-250">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5ebb0-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-intacct-tutorial/tutorial_general_203.png

