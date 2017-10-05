---
title: "Руководство по интеграции Azure Active Directory с Canvas LMS | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в Canvas LMS."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bfed291c-a33e-410d-b919-5b965a631d45
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: jeedes
ms.openlocfilehash: 2212b7a81b66d1afd1aa78d1487b07b6d7b84129
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-canvas-lms"></a><span data-ttu-id="c514f-103">Руководство по интеграции Azure Active Directory с Canvas LMS</span><span class="sxs-lookup"><span data-stu-id="c514f-103">Tutorial: Azure Active Directory integration with Canvas LMS</span></span>

<span data-ttu-id="c514f-104">В этом учебнике описано, как интегрировать Canvas с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c514f-104">In this tutorial, you learn how to integrate Canvas with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c514f-105">Интеграция Azure AD с приложением Canvas обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="c514f-105">Integrating Canvas with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c514f-106">С помощью Azure AD вы можете контролировать доступ к Canvas.</span><span class="sxs-lookup"><span data-stu-id="c514f-106">You can control in Azure AD who has access to Canvas</span></span>
- <span data-ttu-id="c514f-107">Вы можете включить автоматический вход пользователей в Canvas (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c514f-107">You can enable your users to automatically get signed-on to Canvas (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c514f-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="c514f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c514f-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c514f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c514f-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c514f-110">Prerequisites</span></span>

<span data-ttu-id="c514f-111">Чтобы настроить интеграцию Azure AD с Canvas, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="c514f-111">To configure Azure AD integration with Canvas, you need the following items:</span></span>

- <span data-ttu-id="c514f-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="c514f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c514f-113">подписка Canvas с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="c514f-113">A Canvas single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c514f-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="c514f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c514f-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="c514f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c514f-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="c514f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c514f-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c514f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c514f-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="c514f-118">Scenario description</span></span>
<span data-ttu-id="c514f-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="c514f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c514f-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="c514f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c514f-121">Добавление Canvas из коллекции</span><span class="sxs-lookup"><span data-stu-id="c514f-121">Adding Canvas from the gallery</span></span>
2. <span data-ttu-id="c514f-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="c514f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-canvas-from-the-gallery"></a><span data-ttu-id="c514f-123">Добавление Canvas из коллекции</span><span class="sxs-lookup"><span data-stu-id="c514f-123">Adding Canvas from the gallery</span></span>
<span data-ttu-id="c514f-124">Чтобы настроить интеграцию Canvas с Azure AD, необходимо добавить Canvas из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="c514f-124">To configure the integration of Canvas into Azure AD, you need to add Canvas from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c514f-125">**Чтобы добавить Canvas из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="c514f-125">**To add Canvas from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c514f-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c514f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c514f-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="c514f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c514f-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="c514f-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="c514f-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="c514f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="c514f-133">В поле поиска введите **Canvas**.</span><span class="sxs-lookup"><span data-stu-id="c514f-133">In the search box, type **Canvas**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_search.png)

5. <span data-ttu-id="c514f-135">На панели результатов выберите **Canvas** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="c514f-135">In the results panel, select **Canvas**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c514f-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="c514f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c514f-138">В этом разделе описана настройка и проверка единого входа Azure AD в Canvas с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c514f-138">In this section, you configure and test Azure AD single sign-on with Canvas based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c514f-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Canvas соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c514f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Canvas is to a user in Azure AD.</span></span> <span data-ttu-id="c514f-140">Иными словами, необходимо установить связь между пользователям Azure AD и соответствующим пользователем в Canvas.</span><span class="sxs-lookup"><span data-stu-id="c514f-140">In other words, a link relationship between an Azure AD user and the related user in Canvas needs to be established.</span></span>

<span data-ttu-id="c514f-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Canvas.</span><span class="sxs-lookup"><span data-stu-id="c514f-141">In Canvas, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c514f-142">Чтобы настроить и проверить единый вход Azure AD в Canvas, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="c514f-142">To configure and test Azure AD single sign-on with Canvas, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c514f-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="c514f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c514f-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c514f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c514f-145">**[Создание тестового пользователя Canvas](#creating-a-canvas-test-user)** нужно для того, чтобы в Canvas также существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c514f-145">**[Creating a Canvas test user](#creating-a-canvas-test-user)** - to have a counterpart of Britta Simon in Canvas that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c514f-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c514f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c514f-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="c514f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c514f-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="c514f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c514f-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Canvas.</span><span class="sxs-lookup"><span data-stu-id="c514f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Canvas application.</span></span>

<span data-ttu-id="c514f-150">**Чтобы настроить единый вход Azure AD в Canvas, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="c514f-150">**To configure Azure AD single sign-on with Canvas, perform the following steps:**</span></span>

1. <span data-ttu-id="c514f-151">На портале Azure на странице интеграции с приложением **Canvas** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="c514f-151">In the Azure portal, on the **Canvas** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="c514f-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="c514f-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_samlbase.png)

3. <span data-ttu-id="c514f-155">В разделе **Домены и URL-адреса приложения Canvas** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="c514f-155">On the **Canvas Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_url.png)

    <span data-ttu-id="c514f-157">а.</span><span class="sxs-lookup"><span data-stu-id="c514f-157">a.</span></span> <span data-ttu-id="c514f-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<tenant-name>.instructure.com`</span><span class="sxs-lookup"><span data-stu-id="c514f-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.instructure.com`</span></span>

    <span data-ttu-id="c514f-159">b.</span><span class="sxs-lookup"><span data-stu-id="c514f-159">b.</span></span> <span data-ttu-id="c514f-160">В текстовом поле **Идентификатор** введите значение в следующем формате: `https://<tenant-name>.instructure.com/saml2`.</span><span class="sxs-lookup"><span data-stu-id="c514f-160">In the **Identifier** textbox, type the value using the following pattern: `https://<tenant-name>.instructure.com/saml2`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c514f-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="c514f-161">These values are not real.</span></span> <span data-ttu-id="c514f-162">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="c514f-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="c514f-163">Чтобы получить эти значения, обратитесь к [группе поддержки Canvas](https://community.canvaslms.com/community/help).</span><span class="sxs-lookup"><span data-stu-id="c514f-163">Contact [Canvas Client support team](https://community.canvaslms.com/community/help) to get these values.</span></span> 
 
4. <span data-ttu-id="c514f-164">В разделе **Сертификат подписи SAML** скопируйте значение **Отпечаток**.</span><span class="sxs-lookup"><span data-stu-id="c514f-164">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_certificate.png) 

5. <span data-ttu-id="c514f-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="c514f-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c514f-168">В разделе **Конфигурация Canvas** щелкните **Настроить Canvas**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="c514f-168">On the **Canvas Configuration** section, click **Configure Canvas** to open **Configure sign-on** window.</span></span> <span data-ttu-id="c514f-169">Скопируйте **URL-адрес изменения пароля, URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="c514f-169">Copy the **Change Password URL, Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_configure.png) 
 
7. <span data-ttu-id="c514f-171">В другом окне веб-браузера войдите на свой корпоративный веб-сайт Canvas в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="c514f-171">In a different web browser window, log in to your Canvas company site as an administrator.</span></span>

8. <span data-ttu-id="c514f-172">Выберите **Курсы \> Управляемые учетные записи \> Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="c514f-172">Go to **Courses \> Managed Accounts \> Microsoft**.</span></span>
   
    <span data-ttu-id="c514f-173">![Canvas](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "Canvas")</span><span class="sxs-lookup"><span data-stu-id="c514f-173">![Canvas](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "Canvas")</span></span>

9. <span data-ttu-id="c514f-174">На панели навигации слева выберите раздел **Проверка подлинности** и нажмите кнопку **Add New SAML Config** (Добавить новую конфигурацию SAML).</span><span class="sxs-lookup"><span data-stu-id="c514f-174">In the navigation pane on the left, select **Authentication**, and then click **Add New SAML Config**.</span></span>
   
    <span data-ttu-id="c514f-175">![Аутентификация](./media/active-directory-saas-canvas-lms-tutorial/IC775991.png "Аутентификация")</span><span class="sxs-lookup"><span data-stu-id="c514f-175">![Authentication](./media/active-directory-saas-canvas-lms-tutorial/IC775991.png "Authentication")</span></span>

10. <span data-ttu-id="c514f-176">На странице "Текущая интеграция" выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="c514f-176">On the Current Integration page, perform the following steps:</span></span>
   
    <span data-ttu-id="c514f-177">![Текущая интеграция](./media/active-directory-saas-canvas-lms-tutorial/IC775992.png "Текущая интеграция")</span><span class="sxs-lookup"><span data-stu-id="c514f-177">![Current Integration](./media/active-directory-saas-canvas-lms-tutorial/IC775992.png "Current Integration")</span></span>

    <span data-ttu-id="c514f-178">а.</span><span class="sxs-lookup"><span data-stu-id="c514f-178">a.</span></span> <span data-ttu-id="c514f-179">В текстовое поле **IdP Entity ID** (Идентификатор сущности IdP) вставьте значение **SAML Entity ID** (Идентификатор сущности SAML), скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="c514f-179">In **IdP Entity ID** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="c514f-180">b.</span><span class="sxs-lookup"><span data-stu-id="c514f-180">b.</span></span> <span data-ttu-id="c514f-181">В текстовое поле **Log On URL** (URL-адрес входа) вставьте значение **URL-адрес службы единого входа SAML**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="c514f-181">In **Log On URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal .</span></span>

    <span data-ttu-id="c514f-182">c.</span><span class="sxs-lookup"><span data-stu-id="c514f-182">c.</span></span> <span data-ttu-id="c514f-183">В текстовое поле **Log Out URL** (URL-адрес выхода) вставьте значение **URL-адрес выхода**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="c514f-183">In **Log Out URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="c514f-184">г)</span><span class="sxs-lookup"><span data-stu-id="c514f-184">d.</span></span> <span data-ttu-id="c514f-185">В текстовое поле **Change Password Link** (Ссылка для изменения пароля) вставьте **URL-адрес изменения пароля**, скопированный на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="c514f-185">In **Change Password Link** textbox, paste the value of **Change Password URL** which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="c514f-186">д.</span><span class="sxs-lookup"><span data-stu-id="c514f-186">e.</span></span> <span data-ttu-id="c514f-187">В текстовое поле **Certificate Fingerprint** (Отпечаток сертификата) вставьте значение **Отпечаток**, которое вы скопировали на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="c514f-187">In **Certificate Fingerprint** textbox, paste the **Thumbprint** value of certificate which you have copied from Azure portal.</span></span>      
        
    <span data-ttu-id="c514f-188">f.</span><span class="sxs-lookup"><span data-stu-id="c514f-188">f.</span></span> <span data-ttu-id="c514f-189">В списке **Login Attribute** (Атрибут входа) выберите значение **NameID**.</span><span class="sxs-lookup"><span data-stu-id="c514f-189">From the **Login Attribute** list, select **NameID**.</span></span>

    <span data-ttu-id="c514f-190">ж.</span><span class="sxs-lookup"><span data-stu-id="c514f-190">g.</span></span> <span data-ttu-id="c514f-191">В списке **Identifier Format** (Формат идентификатора) выберите значение **emailAddress**.</span><span class="sxs-lookup"><span data-stu-id="c514f-191">From the **Identifier Format** list, select **emailAddress**.</span></span>

    <span data-ttu-id="c514f-192">h.</span><span class="sxs-lookup"><span data-stu-id="c514f-192">h.</span></span> <span data-ttu-id="c514f-193">Нажмите кнопку **Сохранить параметры проверки подлинности**.</span><span class="sxs-lookup"><span data-stu-id="c514f-193">Click **Save Authentication Settings**.</span></span>

> [!TIP]
> <span data-ttu-id="c514f-194">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="c514f-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c514f-195">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="c514f-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c514f-196">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="c514f-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c514f-197">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="c514f-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="c514f-198">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c514f-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="c514f-200">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="c514f-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c514f-201">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c514f-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c514f-203">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="c514f-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c514f-205">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="c514f-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c514f-207">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="c514f-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-canvas-lms-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c514f-209">а.</span><span class="sxs-lookup"><span data-stu-id="c514f-209">a.</span></span> <span data-ttu-id="c514f-210">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c514f-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c514f-211">b.</span><span class="sxs-lookup"><span data-stu-id="c514f-211">b.</span></span> <span data-ttu-id="c514f-212">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c514f-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c514f-213">c.</span><span class="sxs-lookup"><span data-stu-id="c514f-213">c.</span></span> <span data-ttu-id="c514f-214">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="c514f-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c514f-215">d.</span><span class="sxs-lookup"><span data-stu-id="c514f-215">d.</span></span> <span data-ttu-id="c514f-216">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="c514f-216">Click **Create**.</span></span>
 
### <a name="creating-a-canvas-test-user"></a><span data-ttu-id="c514f-217">Создание тестового пользователя Canvas</span><span class="sxs-lookup"><span data-stu-id="c514f-217">Creating a Canvas test user</span></span>

<span data-ttu-id="c514f-218">Чтобы пользователи Azure AD могли выполнить вход в Canvas, они должны быть подготовлены в Canvas.</span><span class="sxs-lookup"><span data-stu-id="c514f-218">To enable Azure AD users to log in to Canvas, they must be provisioned into Canvas.</span></span>

<span data-ttu-id="c514f-219">В случае Canvas подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="c514f-219">In case of Canvas, user provisioning is a manual task.</span></span>

<span data-ttu-id="c514f-220">**Чтобы подготовить учетную запись пользователя, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="c514f-220">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="c514f-221">Выполните вход в клиент **Canvas** .</span><span class="sxs-lookup"><span data-stu-id="c514f-221">Log in to your **Canvas** tenant.</span></span>

2. <span data-ttu-id="c514f-222">Выберите **Курсы \> Управляемые учетные записи \> Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="c514f-222">Go to **Courses \> Managed Accounts \> Microsoft**.</span></span>
   
   <span data-ttu-id="c514f-223">![Canvas](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "Canvas")</span><span class="sxs-lookup"><span data-stu-id="c514f-223">![Canvas](./media/active-directory-saas-canvas-lms-tutorial/IC775990.png "Canvas")</span></span>

3. <span data-ttu-id="c514f-224">Выберите раздел **Пользователи**.</span><span class="sxs-lookup"><span data-stu-id="c514f-224">Click **Users**.</span></span>
   
   <span data-ttu-id="c514f-225">![Пользователи](./media/active-directory-saas-canvas-lms-tutorial/IC775995.png "Пользователи")</span><span class="sxs-lookup"><span data-stu-id="c514f-225">![Users](./media/active-directory-saas-canvas-lms-tutorial/IC775995.png "Users")</span></span>

4. <span data-ttu-id="c514f-226">Нажмите кнопку **Add New User**(Добавить нового пользователя).</span><span class="sxs-lookup"><span data-stu-id="c514f-226">Click **Add New User**.</span></span>
   
   <span data-ttu-id="c514f-227">![Пользователи](./media/active-directory-saas-canvas-lms-tutorial/IC775996.png "Пользователи")</span><span class="sxs-lookup"><span data-stu-id="c514f-227">![Users](./media/active-directory-saas-canvas-lms-tutorial/IC775996.png "Users")</span></span>

5. <span data-ttu-id="c514f-228">На странице диалогового окна "Добавление пользователя" выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="c514f-228">On the Add a New User dialog page, perform the following steps:</span></span>
   
   <span data-ttu-id="c514f-229">![Добавление пользователя](./media/active-directory-saas-canvas-lms-tutorial/IC775997.png "Добавление пользователя")</span><span class="sxs-lookup"><span data-stu-id="c514f-229">![Add User](./media/active-directory-saas-canvas-lms-tutorial/IC775997.png "Add User")</span></span>
   
   <span data-ttu-id="c514f-230">а.</span><span class="sxs-lookup"><span data-stu-id="c514f-230">a.</span></span> <span data-ttu-id="c514f-231">В текстовое поле **Full Name** (Полное имя) введите имя, например **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c514f-231">In the **Full Name** textbox, enter the name of user like **BrittaSimon**.</span></span>

   <span data-ttu-id="c514f-232">b.</span><span class="sxs-lookup"><span data-stu-id="c514f-232">b.</span></span> <span data-ttu-id="c514f-233">В текстовое поле **Email** (Электронная почта) введите адрес электронной почты пользователя, например **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="c514f-233">In the **Email** textbox, enter the email of user like **brittasimon@contoso.com**.</span></span>

   <span data-ttu-id="c514f-234">c.</span><span class="sxs-lookup"><span data-stu-id="c514f-234">c.</span></span> <span data-ttu-id="c514f-235">В текстовом поле **Login** (Имя для входа) введите адрес электронной почты пользователя в Azure AD, например **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="c514f-235">In the **Login** textbox, enter the user’s Azure AD email address like **brittasimon@contoso.com**.</span></span>

   <span data-ttu-id="c514f-236">г)</span><span class="sxs-lookup"><span data-stu-id="c514f-236">d.</span></span> <span data-ttu-id="c514f-237">Установите флажок **Email the user about this account creation**(Сообщить пользователю о создании этой учетной записи по электронной почте).</span><span class="sxs-lookup"><span data-stu-id="c514f-237">Select **Email the user about this account creation**.</span></span>

   <span data-ttu-id="c514f-238">д.</span><span class="sxs-lookup"><span data-stu-id="c514f-238">e.</span></span> <span data-ttu-id="c514f-239">Нажмите кнопку **Add User**(Добавить пользователя).</span><span class="sxs-lookup"><span data-stu-id="c514f-239">Click **Add User**.</span></span>

>[!NOTE]
><span data-ttu-id="c514f-240">Вы можете использовать любые другие средства создания учетной записи пользователя Canvas или API, предоставляемые Canvas для подготовки учетных записей пользователя AAD.</span><span class="sxs-lookup"><span data-stu-id="c514f-240">You can use any other Canvas user account creation tools or APIs provided by Canvas to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c514f-241">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="c514f-241">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c514f-242">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к Canvas.</span><span class="sxs-lookup"><span data-stu-id="c514f-242">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Canvas.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="c514f-244">**Чтобы назначить пользователя Britta Simon в Canvas, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="c514f-244">**To assign Britta Simon to Canvas, perform the following steps:**</span></span>

1. <span data-ttu-id="c514f-245">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="c514f-245">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="c514f-247">Из списка приложений выберите **Canvas**.</span><span class="sxs-lookup"><span data-stu-id="c514f-247">In the applications list, select **Canvas**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-canvas-lms-tutorial/tutorial_canvaslms_app.png) 

3. <span data-ttu-id="c514f-249">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="c514f-249">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="c514f-251">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="c514f-251">Click **Add** button.</span></span> <span data-ttu-id="c514f-252">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="c514f-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="c514f-254">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="c514f-254">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c514f-255">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="c514f-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c514f-256">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="c514f-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c514f-257">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="c514f-257">Testing single sign-on</span></span>

<span data-ttu-id="c514f-258">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="c514f-258">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c514f-259">Щелкнув элемент "Canvas" на панели доступа, вы автоматически войдете в приложение Canvas.</span><span class="sxs-lookup"><span data-stu-id="c514f-259">When you click the Canvas tile in the Access Panel, you should get automatically signed-on to your Canvas application.</span></span>
<span data-ttu-id="c514f-260">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c514f-260">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c514f-261">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="c514f-261">Additional resources</span></span>

* [<span data-ttu-id="c514f-262">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c514f-262">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c514f-263">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c514f-263">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-canvas-lms-tutorial/tutorial_general_203.png

