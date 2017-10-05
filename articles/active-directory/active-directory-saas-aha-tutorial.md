---
title: "Руководство. Интеграция Azure Active Directory с Aha! | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и Aha!."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: ad955d3d-896a-41bb-800d-68e8cb5ff48d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: 7723864b2e1ab2d5b69d86f0fa18416b9d3f9aa3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-aha"></a><span data-ttu-id="7bb62-104">Руководство. Интеграция Azure Active Directory с Aha!</span><span class="sxs-lookup"><span data-stu-id="7bb62-104">Tutorial: Azure Active Directory integration with Aha!</span></span>

<span data-ttu-id="7bb62-105">В этом руководстве вы узнаете, как интегрировать Aha!</span><span class="sxs-lookup"><span data-stu-id="7bb62-105">In this tutorial, you learn how to integrate Aha!</span></span> <span data-ttu-id="7bb62-106">с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7bb62-106">with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7bb62-107">Интеграция Aha!</span><span class="sxs-lookup"><span data-stu-id="7bb62-107">Integrating Aha!</span></span> <span data-ttu-id="7bb62-108">с Azure AD обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="7bb62-108">with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7bb62-109">С помощью Azure AD вы можете контролировать доступ к Aha!.</span><span class="sxs-lookup"><span data-stu-id="7bb62-109">You can control in Azure AD who has access to Aha!</span></span>
- <span data-ttu-id="7bb62-110">Вы можете включить автоматический вход пользователей в Aha! (единый вход)</span><span class="sxs-lookup"><span data-stu-id="7bb62-110">You can enable your users to automatically get signed-on to Aha!</span></span> <span data-ttu-id="7bb62-111">с использованием учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7bb62-111">(Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7bb62-112">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="7bb62-112">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="7bb62-113">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7bb62-113">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7bb62-114">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="7bb62-114">Prerequisites</span></span>

<span data-ttu-id="7bb62-115">Чтобы настроить интеграцию Azure AD с Aha!, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="7bb62-115">To configure Azure AD integration with Aha!, you need the following items:</span></span>

- <span data-ttu-id="7bb62-116">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="7bb62-116">An Azure AD subscription</span></span>
- <span data-ttu-id="7bb62-117">Подписка</span><span class="sxs-lookup"><span data-stu-id="7bb62-117">An Aha!</span></span> <span data-ttu-id="7bb62-118">Aha! с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="7bb62-118">single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7bb62-119">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="7bb62-119">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7bb62-120">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="7bb62-120">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7bb62-121">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="7bb62-121">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7bb62-122">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7bb62-122">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7bb62-123">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="7bb62-123">Scenario description</span></span>
<span data-ttu-id="7bb62-124">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="7bb62-124">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7bb62-125">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="7bb62-125">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7bb62-126">Добавление Aha!</span><span class="sxs-lookup"><span data-stu-id="7bb62-126">Adding Aha!</span></span> <span data-ttu-id="7bb62-127">из коллекции</span><span class="sxs-lookup"><span data-stu-id="7bb62-127">from the gallery</span></span>
2. <span data-ttu-id="7bb62-128">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="7bb62-128">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-aha-from-the-gallery"></a><span data-ttu-id="7bb62-129">Добавление Aha!</span><span class="sxs-lookup"><span data-stu-id="7bb62-129">Adding Aha!</span></span> <span data-ttu-id="7bb62-130">из коллекции</span><span class="sxs-lookup"><span data-stu-id="7bb62-130">from the gallery</span></span>
<span data-ttu-id="7bb62-131">Чтобы настроить интеграцию Aha!</span><span class="sxs-lookup"><span data-stu-id="7bb62-131">To configure the integration of Aha!</span></span> <span data-ttu-id="7bb62-132">с Azure AD, необходимо добавить Aha!</span><span class="sxs-lookup"><span data-stu-id="7bb62-132">into Azure AD, you need to add Aha!</span></span> <span data-ttu-id="7bb62-133">из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="7bb62-133">from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7bb62-134">**Чтобы добавить Aha! из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="7bb62-134">**To add Aha! from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7bb62-135">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7bb62-135">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7bb62-137">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="7bb62-137">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7bb62-138">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="7bb62-138">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="7bb62-140">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="7bb62-140">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="7bb62-142">В поле поиска введите **Aha!**.</span><span class="sxs-lookup"><span data-stu-id="7bb62-142">In the search box, type **Aha!**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-aha-tutorial/tutorial_aha_search.png)

5. <span data-ttu-id="7bb62-144">На панели результатов выберите **Aha!** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="7bb62-144">In the results panel, select **Aha!**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-aha-tutorial/tutorial_aha_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7bb62-146">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="7bb62-146">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7bb62-147">В этом разделе описана настройка и проверка единого входа Azure AD в приложение Aha!</span><span class="sxs-lookup"><span data-stu-id="7bb62-147">In this section, you configure and test Azure AD single sign-on with Aha!</span></span> <span data-ttu-id="7bb62-148">с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7bb62-148">based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="7bb62-149">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Aha!</span><span class="sxs-lookup"><span data-stu-id="7bb62-149">For single sign-on to work, Azure AD needs to know what the counterpart user in Aha!</span></span> <span data-ttu-id="7bb62-150">соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7bb62-150">is to a user in Azure AD.</span></span> <span data-ttu-id="7bb62-151">Иными словами, необходимо установить связь между пользователям Azure AD и соответствующим пользователем</span><span class="sxs-lookup"><span data-stu-id="7bb62-151">In other words, a link relationship between an Azure AD user and the related user in Aha!</span></span> <span data-ttu-id="7bb62-152">в Aha!.</span><span class="sxs-lookup"><span data-stu-id="7bb62-152">needs to be established.</span></span>

<span data-ttu-id="7bb62-153">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Aha!.</span><span class="sxs-lookup"><span data-stu-id="7bb62-153">In Aha!, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="7bb62-154">Чтобы настроить и проверить единый вход Azure AD в Aha!, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="7bb62-154">To configure and test Azure AD single sign-on with Aha!, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7bb62-155">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="7bb62-155">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7bb62-156">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7bb62-156">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7bb62-157">**[Создание тестового пользователя Aha!](#creating-an-aha-test-user)** требуется для создания в Aha! пользователя Britta Simon,</span><span class="sxs-lookup"><span data-stu-id="7bb62-157">**[Creating an Aha! test user](#creating-an-aha-test-user)** - to have a counterpart of Britta Simon in Aha!</span></span> <span data-ttu-id="7bb62-158">связанного с соответствующим представлением в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7bb62-158">that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="7bb62-159">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7bb62-159">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7bb62-160">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="7bb62-160">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7bb62-161">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="7bb62-161">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7bb62-162">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в</span><span class="sxs-lookup"><span data-stu-id="7bb62-162">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Aha!</span></span> <span data-ttu-id="7bb62-163">приложении Aha!.</span><span class="sxs-lookup"><span data-stu-id="7bb62-163">application.</span></span>

<span data-ttu-id="7bb62-164">**Чтобы настроить единый вход Azure AD в Aha!, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="7bb62-164">**To configure Azure AD single sign-on with Aha!, perform the following steps:**</span></span>

1. <span data-ttu-id="7bb62-165">На портале Azure на странице интеграции с приложением **Aha!**</span><span class="sxs-lookup"><span data-stu-id="7bb62-165">In the Azure portal, on the **Aha!**</span></span> <span data-ttu-id="7bb62-166">щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="7bb62-166">application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="7bb62-168">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="7bb62-168">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-aha-tutorial/tutorial_aha_samlbase.png)

3. <span data-ttu-id="7bb62-170">В разделе **Домены и URL-адреса приложения Aha!** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="7bb62-170">On the **Aha! Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-aha-tutorial/tutorial_aha_url.png)

    <span data-ttu-id="7bb62-172">а.</span><span class="sxs-lookup"><span data-stu-id="7bb62-172">a.</span></span> <span data-ttu-id="7bb62-173">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<companyname>.aha.io/session/new`</span><span class="sxs-lookup"><span data-stu-id="7bb62-173">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.aha.io/session/new`</span></span>

    <span data-ttu-id="7bb62-174">b.</span><span class="sxs-lookup"><span data-stu-id="7bb62-174">b.</span></span> <span data-ttu-id="7bb62-175">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<companyname>.aha.io`</span><span class="sxs-lookup"><span data-stu-id="7bb62-175">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.aha.io`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7bb62-176">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="7bb62-176">These values are not real.</span></span> <span data-ttu-id="7bb62-177">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="7bb62-177">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="7bb62-178">Обратитесь к [группе поддержки Aha!](https://www.aha.io/company/contact), чтобы получить эти значения.</span><span class="sxs-lookup"><span data-stu-id="7bb62-178">Contact [Aha! Client support team](https://www.aha.io/company/contact) to get these values.</span></span> 
 
4. <span data-ttu-id="7bb62-179">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="7bb62-179">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-aha-tutorial/tutorial_aha_certificate.png) 

5. <span data-ttu-id="7bb62-181">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="7bb62-181">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-aha-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7bb62-183">В другом окне веб-браузера войдите на свой корпоративный веб-сайт Aha!</span><span class="sxs-lookup"><span data-stu-id="7bb62-183">In a different web browser window, log in to your Aha!</span></span> <span data-ttu-id="7bb62-184">в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="7bb62-184">company site as an administrator.</span></span>

7. <span data-ttu-id="7bb62-185">В верхнем меню нажмите пункт **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="7bb62-185">In the menu on the top, click **Settings**.</span></span>

    <span data-ttu-id="7bb62-186">![Параметры](./media/active-directory-saas-aha-tutorial/IC798950.png "Параметры")</span><span class="sxs-lookup"><span data-stu-id="7bb62-186">![Settings](./media/active-directory-saas-aha-tutorial/IC798950.png "Settings")</span></span>

8. <span data-ttu-id="7bb62-187">Выберите раздел **Учетная запись**.</span><span class="sxs-lookup"><span data-stu-id="7bb62-187">Click **Account**.</span></span>
   
    <span data-ttu-id="7bb62-188">![Профиль](./media/active-directory-saas-aha-tutorial/IC798951.png "Профиль")</span><span class="sxs-lookup"><span data-stu-id="7bb62-188">![Profile](./media/active-directory-saas-aha-tutorial/IC798951.png "Profile")</span></span>

9. <span data-ttu-id="7bb62-189">Нажмите **Безопасность и единый вход**.</span><span class="sxs-lookup"><span data-stu-id="7bb62-189">Click **Security and single sign-on**.</span></span>
   
    <span data-ttu-id="7bb62-190">![Безопасность и единый вход](./media/active-directory-saas-aha-tutorial/IC798952.png "Безопасность и единый вход")</span><span class="sxs-lookup"><span data-stu-id="7bb62-190">![Security and single sign-on](./media/active-directory-saas-aha-tutorial/IC798952.png "Security and single sign-on")</span></span>

10. <span data-ttu-id="7bb62-191">В разделе **Единый вход** в качестве **поставщика удостоверений** выберите **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="7bb62-191">In **Single Sign-On** section, as **Identity Provider**, select **SAML2.0**.</span></span>
   
    <span data-ttu-id="7bb62-192">![Безопасность и единый вход](./media/active-directory-saas-aha-tutorial/IC798953.png "Безопасность и единый вход")</span><span class="sxs-lookup"><span data-stu-id="7bb62-192">![Security and single sign-on](./media/active-directory-saas-aha-tutorial/IC798953.png "Security and single sign-on")</span></span>

11. <span data-ttu-id="7bb62-193">На странице настроек **Единый вход** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="7bb62-193">On the **Single Sign-On** configuration page, perform the following steps:</span></span>
    
    <span data-ttu-id="7bb62-194">![Единый вход](./media/active-directory-saas-aha-tutorial/IC798954.png "Единый вход")</span><span class="sxs-lookup"><span data-stu-id="7bb62-194">![Single Sign-On](./media/active-directory-saas-aha-tutorial/IC798954.png "Single Sign-On")</span></span>
    
       <span data-ttu-id="7bb62-195">а.</span><span class="sxs-lookup"><span data-stu-id="7bb62-195">a.</span></span> <span data-ttu-id="7bb62-196">В текстовом поле **Имя** введите имя конфигурации.</span><span class="sxs-lookup"><span data-stu-id="7bb62-196">In the **Name** textbox, type a name for your configuration.</span></span>

       <span data-ttu-id="7bb62-197">b.</span><span class="sxs-lookup"><span data-stu-id="7bb62-197">b.</span></span> <span data-ttu-id="7bb62-198">Для параметра **Configure using** (Использовать при настройке) выберите значение **Файл метаданных**.</span><span class="sxs-lookup"><span data-stu-id="7bb62-198">For **Configure using**, select **Metadata File**.</span></span>
   
       <span data-ttu-id="7bb62-199">c.</span><span class="sxs-lookup"><span data-stu-id="7bb62-199">c.</span></span> <span data-ttu-id="7bb62-200">Чтобы отправить загруженный файл метаданных, нажмите кнопку **Обзор**.</span><span class="sxs-lookup"><span data-stu-id="7bb62-200">To upload your downloaded metadata file, click **Browse**.</span></span>
   
       <span data-ttu-id="7bb62-201">г)</span><span class="sxs-lookup"><span data-stu-id="7bb62-201">d.</span></span> <span data-ttu-id="7bb62-202">Нажмите кнопку **Обновить**.</span><span class="sxs-lookup"><span data-stu-id="7bb62-202">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="7bb62-203">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="7bb62-203">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7bb62-204">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="7bb62-204">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7bb62-205">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="7bb62-205">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7bb62-206">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="7bb62-206">Creating an Azure AD test user</span></span>
<span data-ttu-id="7bb62-207">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7bb62-207">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="7bb62-209">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="7bb62-209">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7bb62-210">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7bb62-210">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-aha-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7bb62-212">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="7bb62-212">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-aha-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7bb62-214">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="7bb62-214">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-aha-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7bb62-216">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="7bb62-216">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-aha-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7bb62-218">а.</span><span class="sxs-lookup"><span data-stu-id="7bb62-218">a.</span></span> <span data-ttu-id="7bb62-219">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7bb62-219">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7bb62-220">b.</span><span class="sxs-lookup"><span data-stu-id="7bb62-220">b.</span></span> <span data-ttu-id="7bb62-221">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="7bb62-221">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="7bb62-222">c.</span><span class="sxs-lookup"><span data-stu-id="7bb62-222">c.</span></span> <span data-ttu-id="7bb62-223">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="7bb62-223">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7bb62-224">d.</span><span class="sxs-lookup"><span data-stu-id="7bb62-224">d.</span></span> <span data-ttu-id="7bb62-225">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="7bb62-225">Click **Create**.</span></span>
 
### <a name="creating-an-aha-test-user"></a><span data-ttu-id="7bb62-226">Создание тестового</span><span class="sxs-lookup"><span data-stu-id="7bb62-226">Creating an Aha!</span></span> <span data-ttu-id="7bb62-227">пользователя Aha!</span><span class="sxs-lookup"><span data-stu-id="7bb62-227">test user</span></span>

<span data-ttu-id="7bb62-228">Чтобы пользователи Azure AD могли выполнять вход в Aha!, они должны быть подготовлены в Aha!.</span><span class="sxs-lookup"><span data-stu-id="7bb62-228">To enable Azure AD users to log in to Aha!, they must be provisioned into Aha!.</span></span>  

<span data-ttu-id="7bb62-229">В случае Aha! подготовка выполняется автоматически.</span><span class="sxs-lookup"><span data-stu-id="7bb62-229">In the case of Aha!, provisioning is an automated task.</span></span> <span data-ttu-id="7bb62-230">С вашей стороны никакие действия не требуются.</span><span class="sxs-lookup"><span data-stu-id="7bb62-230">There is no action item for you.</span></span>

<span data-ttu-id="7bb62-231">В случае необходимости пользователи создаются автоматически при первой попытке входа в систему.</span><span class="sxs-lookup"><span data-stu-id="7bb62-231">Users are automatically created if necessary during the first single sign-on attempt.</span></span>

>[!NOTE]
><span data-ttu-id="7bb62-232">Вы можете использовать любые другие средства создания учетной записи пользователя Aha!</span><span class="sxs-lookup"><span data-stu-id="7bb62-232">You can use any other Aha!</span></span> <span data-ttu-id="7bb62-233">или API, предоставляемые Aha!</span><span class="sxs-lookup"><span data-stu-id="7bb62-233">user account creation tools or APIs provided by Aha!</span></span> <span data-ttu-id="7bb62-234">для подготовки учетных записей пользователя AAD.</span><span class="sxs-lookup"><span data-stu-id="7bb62-234">to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="7bb62-235">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="7bb62-235">Assigning the Azure AD test user</span></span>

<span data-ttu-id="7bb62-236">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к Aha!.</span><span class="sxs-lookup"><span data-stu-id="7bb62-236">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Aha!.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="7bb62-238">**Чтобы назначить пользователя Britta Simon в Aha!, сделайте следующее.**</span><span class="sxs-lookup"><span data-stu-id="7bb62-238">**To assign Britta Simon to Aha!, perform the following steps:**</span></span>

1. <span data-ttu-id="7bb62-239">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="7bb62-239">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="7bb62-241">Из списка приложений выберите **Aha!**.</span><span class="sxs-lookup"><span data-stu-id="7bb62-241">In the applications list, select **Aha!**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-aha-tutorial/tutorial_aha_app.png) 

3. <span data-ttu-id="7bb62-243">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="7bb62-243">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="7bb62-245">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="7bb62-245">Click **Add** button.</span></span> <span data-ttu-id="7bb62-246">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="7bb62-246">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="7bb62-248">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="7bb62-248">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7bb62-249">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="7bb62-249">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7bb62-250">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="7bb62-250">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7bb62-251">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="7bb62-251">Testing single sign-on</span></span>

<span data-ttu-id="7bb62-252">Если вы хотите проверить параметры единого входа, откройте панель доступа.</span><span class="sxs-lookup"><span data-stu-id="7bb62-252">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="7bb62-253">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="7bb62-253">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="7bb62-254">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="7bb62-254">Additional resources</span></span>

* [<span data-ttu-id="7bb62-255">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7bb62-255">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7bb62-256">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7bb62-256">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-aha-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-aha-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-aha-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-aha-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-aha-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-aha-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-aha-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-aha-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-aha-tutorial/tutorial_general_203.png

