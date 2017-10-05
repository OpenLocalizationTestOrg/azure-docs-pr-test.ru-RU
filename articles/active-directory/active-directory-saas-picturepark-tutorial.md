---
title: "Руководство по интеграции Azure Active Directory с Picturepark | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в приложении Picturepark."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 31c21cd4-9c00-4cad-9538-a13996dc872f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: jeedes
ms.openlocfilehash: 1c009aa1fdd3140a4466cf762b6c9687e74ce4c7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-picturepark"></a><span data-ttu-id="62281-103">Руководство по интеграции Azure Active Directory с Picturepark</span><span class="sxs-lookup"><span data-stu-id="62281-103">Tutorial: Azure Active Directory integration with Picturepark</span></span>

<span data-ttu-id="62281-104">В этом руководстве описано, как интегрировать Picturepark с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="62281-104">In this tutorial, you learn how to integrate Picturepark with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="62281-105">Интеграция Azure AD с приложением Picturepark обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="62281-105">Integrating Picturepark with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="62281-106">С помощью Azure AD вы можете контролировать доступ к Picturepark.</span><span class="sxs-lookup"><span data-stu-id="62281-106">You can control in Azure AD who has access to Picturepark</span></span>
- <span data-ttu-id="62281-107">Вы можете включить автоматический вход пользователей в Picturepark (единый вход) с использованием учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="62281-107">You can enable your users to automatically get signed-on to Picturepark (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="62281-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="62281-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="62281-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="62281-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="62281-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="62281-110">Prerequisites</span></span>

<span data-ttu-id="62281-111">Чтобы настроить интеграцию Azure AD с Picturepark, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="62281-111">To configure Azure AD integration with Picturepark, you need the following items:</span></span>

- <span data-ttu-id="62281-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="62281-112">An Azure AD subscription</span></span>
- <span data-ttu-id="62281-113">подписка Picturepark с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="62281-113">A Picturepark single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="62281-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="62281-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="62281-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="62281-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="62281-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="62281-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="62281-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="62281-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="62281-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="62281-118">Scenario description</span></span>
<span data-ttu-id="62281-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="62281-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="62281-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="62281-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="62281-121">Добавление Picturepark из коллекции.</span><span class="sxs-lookup"><span data-stu-id="62281-121">Adding Picturepark from the gallery</span></span>
2. <span data-ttu-id="62281-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="62281-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-picturepark-from-the-gallery"></a><span data-ttu-id="62281-123">Добавление Picturepark из коллекции</span><span class="sxs-lookup"><span data-stu-id="62281-123">Adding Picturepark from the gallery</span></span>
<span data-ttu-id="62281-124">Чтобы настроить интеграцию Picturepark с Azure AD, необходимо добавить Picturepark из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="62281-124">To configure the integration of Picturepark into Azure AD, you need to add Picturepark from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="62281-125">**Чтобы добавить Picturepark из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="62281-125">**To add Picturepark from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="62281-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="62281-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="62281-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="62281-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="62281-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="62281-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="62281-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="62281-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="62281-133">В поле поиска введите **Picturepark**.</span><span class="sxs-lookup"><span data-stu-id="62281-133">In the search box, type **Picturepark**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_search.png)

5. <span data-ttu-id="62281-135">На панели результатов выберите **Picturepark** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="62281-135">In the results panel, select **Picturepark**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="62281-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="62281-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="62281-138">В этом разделе описана настройка и проверка единого входа Azure AD в Picturepark с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="62281-138">In this section, you configure and test Azure AD single sign-on with Picturepark based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="62281-139">Чтобы единый вход работал, Azure AD необходима информация о том, какой пользователь в Picturepark соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="62281-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Picturepark is to a user in Azure AD.</span></span> <span data-ttu-id="62281-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Picturepark.</span><span class="sxs-lookup"><span data-stu-id="62281-140">In other words, a link relationship between an Azure AD user and the related user in Picturepark needs to be established.</span></span>

<span data-ttu-id="62281-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Picturepark.</span><span class="sxs-lookup"><span data-stu-id="62281-141">In Picturepark, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="62281-142">Чтобы настроить и проверить единый вход Azure AD в Picturepark, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="62281-142">To configure and test Azure AD single sign-on with Picturepark, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="62281-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="62281-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="62281-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="62281-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="62281-145">**[Создание тестового пользователя Picturepark](#creating-a-picturepark-test-user)** требуется для того, чтобы в Picturepark существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="62281-145">**[Creating a Picturepark test user](#creating-a-picturepark-test-user)** - to have a counterpart of Britta Simon in Picturepark that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="62281-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="62281-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="62281-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="62281-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="62281-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="62281-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="62281-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Picturepark.</span><span class="sxs-lookup"><span data-stu-id="62281-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Picturepark application.</span></span>

<span data-ttu-id="62281-150">**Чтобы настроить единый вход Azure AD в Picturepark, выполните следующее.**</span><span class="sxs-lookup"><span data-stu-id="62281-150">**To configure Azure AD single sign-on with Picturepark, perform the following steps:**</span></span>

1. <span data-ttu-id="62281-151">На портале Azure на странице интеграции с приложением **Picturepark** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="62281-151">In the Azure portal, on the **Picturepark** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="62281-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="62281-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_samlbase.png)

3. <span data-ttu-id="62281-155">В разделе **Домены и URL-адреса приложения Picturepark** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="62281-155">On the **Picturepark Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_url.png)

    <span data-ttu-id="62281-157">а.</span><span class="sxs-lookup"><span data-stu-id="62281-157">a.</span></span> <span data-ttu-id="62281-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<companyname>.picturepark.com`</span><span class="sxs-lookup"><span data-stu-id="62281-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.picturepark.com`</span></span>

    <span data-ttu-id="62281-159">b.</span><span class="sxs-lookup"><span data-stu-id="62281-159">b.</span></span> <span data-ttu-id="62281-160">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="62281-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span> 
    
    |  |
    |--|
    | `https://<companyname>.current-picturepark.com`|
    | `https://<companyname>.picturepark.com`|
    | `https://<companyname>.next-picturepark.com`|
    | |

    > [!NOTE] 
    > <span data-ttu-id="62281-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="62281-161">These values are not real.</span></span> <span data-ttu-id="62281-162">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="62281-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="62281-163">Чтобы получить эти значения, обратитесь к [группе поддержки клиентов Picturepark](https://picturepark.com/about/contact/).</span><span class="sxs-lookup"><span data-stu-id="62281-163">Contact [Picturepark Client support team](https://picturepark.com/about/contact/) to get these values.</span></span> 
 
4. <span data-ttu-id="62281-164">В разделе **Сертификат подписи SAML** скопируйте значение **Отпечаток**.</span><span class="sxs-lookup"><span data-stu-id="62281-164">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_certificate.png) 

5. <span data-ttu-id="62281-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="62281-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-picturepark-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="62281-168">В разделе **Конфигурация Picturepark** щелкните **Настроить Picturepark**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="62281-168">On the **Picturepark Configuration** section, click **Configure Picturepark** to open **Configure sign-on** window.</span></span> <span data-ttu-id="62281-169">Скопируйте **URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="62281-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_configure.png) 

7. <span data-ttu-id="62281-171">В другом окне веб-браузера войдите на сайт Picturepark своей компании в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="62281-171">In a different web browser window, log into your Picturepark company site as an administrator.</span></span>

8. <span data-ttu-id="62281-172">Щелкните **Administrative tools** (Администрирование) на панели инструментов в верхней части страницы и выберите **Management Console** (Консоль управления).</span><span class="sxs-lookup"><span data-stu-id="62281-172">In the toolbar on the top, click **Administrative tools**, and then click **Management Console**.</span></span>
   
    <span data-ttu-id="62281-173">![Консоль управления](./media/active-directory-saas-picturepark-tutorial/ic795062.png "Консоль управления")</span><span class="sxs-lookup"><span data-stu-id="62281-173">![Management Console](./media/active-directory-saas-picturepark-tutorial/ic795062.png "Management Console")</span></span>

9. <span data-ttu-id="62281-174">Щелкните **Authentication** (Аутентификация), а затем выберите **Identity providers** (Поставщики удостоверений).</span><span class="sxs-lookup"><span data-stu-id="62281-174">Click **Authentication**, and then click **Identity providers**.</span></span>
   
    <span data-ttu-id="62281-175">![Аутентификация](./media/active-directory-saas-picturepark-tutorial/ic795063.png "Аутентификация")</span><span class="sxs-lookup"><span data-stu-id="62281-175">![Authentication](./media/active-directory-saas-picturepark-tutorial/ic795063.png "Authentication")</span></span>

10. <span data-ttu-id="62281-176">В разделе **Конфигурация поставщика удостоверений** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="62281-176">In the **Identity provider configuration** section, perform the following steps:</span></span>
   
    <span data-ttu-id="62281-177">![Конфигурация поставщика удостоверений](./media/active-directory-saas-picturepark-tutorial/ic795064.png "Конфигурация поставщика удостоверений")</span><span class="sxs-lookup"><span data-stu-id="62281-177">![Identity provider configuration](./media/active-directory-saas-picturepark-tutorial/ic795064.png "Identity provider configuration")</span></span>
   
    <span data-ttu-id="62281-178">а.</span><span class="sxs-lookup"><span data-stu-id="62281-178">a.</span></span> <span data-ttu-id="62281-179">Щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="62281-179">Click **Add**.</span></span>
  
    <span data-ttu-id="62281-180">b.</span><span class="sxs-lookup"><span data-stu-id="62281-180">b.</span></span> <span data-ttu-id="62281-181">Введите имя конфигурации.</span><span class="sxs-lookup"><span data-stu-id="62281-181">Type a name for your configuration.</span></span>
   
    <span data-ttu-id="62281-182">c.</span><span class="sxs-lookup"><span data-stu-id="62281-182">c.</span></span> <span data-ttu-id="62281-183">Выберите **По умолчанию**.</span><span class="sxs-lookup"><span data-stu-id="62281-183">Select **Set as default**.</span></span>
   
    <span data-ttu-id="62281-184">г)</span><span class="sxs-lookup"><span data-stu-id="62281-184">d.</span></span> <span data-ttu-id="62281-185">В текстовое поле **Issuer URI** (URI издателя) вставьте значение **SAML Single Sign-On Service URL** (URL-адрес службы единого входа SAML), скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="62281-185">In **Issuer URI** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="62281-186">д.</span><span class="sxs-lookup"><span data-stu-id="62281-186">e.</span></span> <span data-ttu-id="62281-187">В текстовое поле **Trusted Issuer Thumb Print** (Отпечаток доверенного издателя) вставьте значение **Отпечаток**, скопированное в разделе **Сертификат подписи SAML**.</span><span class="sxs-lookup"><span data-stu-id="62281-187">In **Trusted Issuer Thumb Print** textbox, paste the value of **Thumbprint** which you have copied from **SAML Signing Certificate** section.</span></span> 

11. <span data-ttu-id="62281-188">Щелкните **JoinDefaultUsersGroup**.</span><span class="sxs-lookup"><span data-stu-id="62281-188">Click **JoinDefaultUsersGroup**.</span></span>

12. <span data-ttu-id="62281-189">Чтобы задать атрибут **Emailaddress** в текстовом поле **Claim** (Утверждение), введите `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress` и нажмите кнопку **Save** (Сохранить).</span><span class="sxs-lookup"><span data-stu-id="62281-189">To set the **Emailaddress** attribute in the **Claim** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress` and click **Save**.</span></span>

      <span data-ttu-id="62281-190">![Конфигурация](./media/active-directory-saas-picturepark-tutorial/ic795065.png "Конфигурация")</span><span class="sxs-lookup"><span data-stu-id="62281-190">![Configuration](./media/active-directory-saas-picturepark-tutorial/ic795065.png "Configuration")</span></span>

> [!TIP]
> <span data-ttu-id="62281-191">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="62281-191">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="62281-192">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="62281-192">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="62281-193">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="62281-193">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="62281-194">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="62281-194">Creating an Azure AD test user</span></span>
<span data-ttu-id="62281-195">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="62281-195">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="62281-197">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="62281-197">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="62281-198">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="62281-198">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-picturepark-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="62281-200">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="62281-200">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-picturepark-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="62281-202">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="62281-202">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-picturepark-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="62281-204">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="62281-204">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-picturepark-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="62281-206">а.</span><span class="sxs-lookup"><span data-stu-id="62281-206">a.</span></span> <span data-ttu-id="62281-207">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="62281-207">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="62281-208">b.</span><span class="sxs-lookup"><span data-stu-id="62281-208">b.</span></span> <span data-ttu-id="62281-209">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="62281-209">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="62281-210">c.</span><span class="sxs-lookup"><span data-stu-id="62281-210">c.</span></span> <span data-ttu-id="62281-211">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="62281-211">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="62281-212">d.</span><span class="sxs-lookup"><span data-stu-id="62281-212">d.</span></span> <span data-ttu-id="62281-213">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="62281-213">Click **Create**.</span></span>
 
### <a name="creating-a-picturepark-test-user"></a><span data-ttu-id="62281-214">Создание тестового пользователя Picturepark</span><span class="sxs-lookup"><span data-stu-id="62281-214">Creating a Picturepark test user</span></span>

<span data-ttu-id="62281-215">Чтобы пользователи Azure AD могли выполнять вход в Picturepark, они должны быть подготовлены для Picturepark.</span><span class="sxs-lookup"><span data-stu-id="62281-215">In order to enable Azure AD users to log into Picturepark, they must be provisioned into Picturepark.</span></span> <span data-ttu-id="62281-216">В случае с Picturepark подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="62281-216">In the case of Picturepark, provisioning is a manual task.</span></span>

<span data-ttu-id="62281-217">**Чтобы подготовить учетную запись пользователя, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="62281-217">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="62281-218">Выполните вход в клиент **Picturepark** .</span><span class="sxs-lookup"><span data-stu-id="62281-218">Log in to your **Picturepark** tenant.</span></span>

2. <span data-ttu-id="62281-219">Щелкните **Administrative tools** (Администрирование) на панели инструментов в верхней части страницы и выберите **Users** (Пользователи).</span><span class="sxs-lookup"><span data-stu-id="62281-219">In the toolbar on the top, click **Administrative tools**, and then click **Users**.</span></span>
   
    <span data-ttu-id="62281-220">![Пользователи](./media/active-directory-saas-picturepark-tutorial/ic795067.png "Пользователи")</span><span class="sxs-lookup"><span data-stu-id="62281-220">![Users](./media/active-directory-saas-picturepark-tutorial/ic795067.png "Users")</span></span>

3. <span data-ttu-id="62281-221">На вкладке **Users overview** (Обзор пользователей) щелкните **New** (Создать).</span><span class="sxs-lookup"><span data-stu-id="62281-221">In the **Users overview** tab, click **New**.</span></span>
   
    <span data-ttu-id="62281-222">![Управление пользователями](./media/active-directory-saas-picturepark-tutorial/ic795068.png "Управление пользователями")</span><span class="sxs-lookup"><span data-stu-id="62281-222">![User management](./media/active-directory-saas-picturepark-tutorial/ic795068.png "User management")</span></span>

4. <span data-ttu-id="62281-223">В диалоговом окне **Create User** (Создание пользователя) введите приведенные ниже данные действительной учетной записи Azure AD, которую необходимо подготовить.</span><span class="sxs-lookup"><span data-stu-id="62281-223">On the **Create User** dialog, perform the following steps of a valid Azure Active Directory User you want to provision:</span></span>
   
    <span data-ttu-id="62281-224">![Создание пользователя](./media/active-directory-saas-picturepark-tutorial/ic795069.png "Создание пользователя")</span><span class="sxs-lookup"><span data-stu-id="62281-224">![Create User](./media/active-directory-saas-picturepark-tutorial/ic795069.png "Create User")</span></span>
   
    <span data-ttu-id="62281-225">а.</span><span class="sxs-lookup"><span data-stu-id="62281-225">a.</span></span> <span data-ttu-id="62281-226">В текстовое поле **Email Address** (Адрес электронной почты) введите **адрес электронной почты** пользователя, например **BrittaSimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="62281-226">In the **Email Address** textbox, type the **email address** of the user **BrittaSimon@contoso.com**.</span></span>  
   
    <span data-ttu-id="62281-227">b.</span><span class="sxs-lookup"><span data-stu-id="62281-227">b.</span></span> <span data-ttu-id="62281-228">В текстовые поля **Password** (Пароль) и **Confirm Password** (Подтверждение пароля) введите **пароль** пользователя BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="62281-228">In the **Password** and **Confirm Password** textboxes, type the **password** of BrittaSimon.</span></span> 
   
    <span data-ttu-id="62281-229">c.</span><span class="sxs-lookup"><span data-stu-id="62281-229">c.</span></span> <span data-ttu-id="62281-230">В текстовое поле **First Name** (Имя) введите **имя пользователя**, **Britta**.</span><span class="sxs-lookup"><span data-stu-id="62281-230">In the **First Name** textbox, type the **First Name** of the user **Britta**.</span></span> 
   
    <span data-ttu-id="62281-231">г)</span><span class="sxs-lookup"><span data-stu-id="62281-231">d.</span></span> <span data-ttu-id="62281-232">В текстовое поле **Last Name** (Фамилия) введите **фамилию** пользователя, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="62281-232">In the **Last Name** textbox, type the **Last Name** of the user **Simon**.</span></span>
   
    <span data-ttu-id="62281-233">д.</span><span class="sxs-lookup"><span data-stu-id="62281-233">e.</span></span> <span data-ttu-id="62281-234">В текстовое поле **Company** (Компания) введите **название компании** пользователя.</span><span class="sxs-lookup"><span data-stu-id="62281-234">In the **Company** textbox, type the **Company name** of the user.</span></span> 
   
    <span data-ttu-id="62281-235">f.</span><span class="sxs-lookup"><span data-stu-id="62281-235">f.</span></span> <span data-ttu-id="62281-236">В текстовом поле **Country** (Страна) выберите **страну** пользователя.</span><span class="sxs-lookup"><span data-stu-id="62281-236">In the **Country** textbox, select the **Country** of the user.</span></span>
  
    <span data-ttu-id="62281-237">g.</span><span class="sxs-lookup"><span data-stu-id="62281-237">g.</span></span> <span data-ttu-id="62281-238">В текстовое поле **ZIP** (Почтовый индекс) введите **почтовый индекс** города.</span><span class="sxs-lookup"><span data-stu-id="62281-238">In the **ZIP** textbox, type the **ZIP code** of the city.</span></span>
   
    <span data-ttu-id="62281-239">h.</span><span class="sxs-lookup"><span data-stu-id="62281-239">h.</span></span> <span data-ttu-id="62281-240">В текстовое поле **City** (Город) введите **название города** пользователя.</span><span class="sxs-lookup"><span data-stu-id="62281-240">In the **City** textbox, type the **City name** of the user.</span></span>

    <span data-ttu-id="62281-241">i.</span><span class="sxs-lookup"><span data-stu-id="62281-241">i.</span></span> <span data-ttu-id="62281-242">В поле **Язык**укажите язык.</span><span class="sxs-lookup"><span data-stu-id="62281-242">Select a **Language**.</span></span>
   
    <span data-ttu-id="62281-243">j.</span><span class="sxs-lookup"><span data-stu-id="62281-243">j.</span></span> <span data-ttu-id="62281-244">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="62281-244">Click **Create**.</span></span>

>[!NOTE]
><span data-ttu-id="62281-245">Вы можете использовать любые другие инструменты создания учетных записей пользователя Picturepark или API, предоставляемые Picturepark для подготовки учетных записей пользователя Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="62281-245">You can use any other Picturepark user account creation tools or APIs provided by Picturepark to provision Azure AD user accounts.</span></span>
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="62281-246">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="62281-246">Assigning the Azure AD test user</span></span>

<span data-ttu-id="62281-247">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к Picturepark.</span><span class="sxs-lookup"><span data-stu-id="62281-247">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Picturepark.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="62281-249">**Чтобы назначить пользователя Britta Simon в Picturepark, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="62281-249">**To assign Britta Simon to Picturepark, perform the following steps:**</span></span>

1. <span data-ttu-id="62281-250">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="62281-250">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="62281-252">Из списка приложений выберите **Picturepark**.</span><span class="sxs-lookup"><span data-stu-id="62281-252">In the applications list, select **Picturepark**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-picturepark-tutorial/tutorial_picturepark_app.png) 

3. <span data-ttu-id="62281-254">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="62281-254">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="62281-256">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="62281-256">Click **Add** button.</span></span> <span data-ttu-id="62281-257">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="62281-257">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="62281-259">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="62281-259">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="62281-260">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="62281-260">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="62281-261">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="62281-261">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="62281-262">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="62281-262">Testing single sign-on</span></span>

<span data-ttu-id="62281-263">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="62281-263">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="62281-264">Щелкнув элемент "Picturepark" на панели доступа, вы автоматически войдете в приложение Picturepark.</span><span class="sxs-lookup"><span data-stu-id="62281-264">When you click the Picturepark tile in the Access Panel, you should get automatically signed-on to your Picturepark application.</span></span> <span data-ttu-id="62281-265">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="62281-265">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="62281-266">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="62281-266">Additional resources</span></span>

* [<span data-ttu-id="62281-267">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="62281-267">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="62281-268">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="62281-268">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-picturepark-tutorial/tutorial_general_203.png

