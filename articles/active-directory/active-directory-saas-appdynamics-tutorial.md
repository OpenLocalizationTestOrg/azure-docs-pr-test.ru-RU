---
title: "Руководство. Интеграция Azure Active Directory с AppDynamics | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в приложении AppDynamics."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 25fd1df0-411c-4f55-8be3-4273b543100f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 634e68bdb937eba68b27b824dc62fe2677e24ffe
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-appdynamics"></a><span data-ttu-id="603b0-103">Руководство. Интеграция Azure Active Directory с AppDynamics</span><span class="sxs-lookup"><span data-stu-id="603b0-103">Tutorial: Azure Active Directory integration with AppDynamics</span></span>

<span data-ttu-id="603b0-104">В этом руководстве описано, как интегрировать приложение AppDynamics с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="603b0-104">In this tutorial, you learn how to integrate AppDynamics with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="603b0-105">Интеграция AppDynamics с Azure AD обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="603b0-105">Integrating AppDynamics with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="603b0-106">С помощью Azure AD вы можете контролировать доступ к AppDynamics.</span><span class="sxs-lookup"><span data-stu-id="603b0-106">You can control in Azure AD who has access to AppDynamics</span></span>
- <span data-ttu-id="603b0-107">Вы можете включить автоматический вход пользователей в AppDynamics (единый вход) с использованием учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="603b0-107">You can enable your users to automatically get signed-on to AppDynamics (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="603b0-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="603b0-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="603b0-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="603b0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="603b0-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="603b0-110">Prerequisites</span></span>

<span data-ttu-id="603b0-111">Чтобы настроить интеграцию Azure AD с AppDynamics, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="603b0-111">To configure Azure AD integration with AppDynamics, you need the following items:</span></span>

- <span data-ttu-id="603b0-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="603b0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="603b0-113">Подписка с поддержкой единого входа AppDynamics</span><span class="sxs-lookup"><span data-stu-id="603b0-113">An AppDynamics single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="603b0-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="603b0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="603b0-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="603b0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="603b0-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="603b0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="603b0-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="603b0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="603b0-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="603b0-118">Scenario description</span></span>
<span data-ttu-id="603b0-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="603b0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="603b0-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="603b0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="603b0-121">Добавление AppDynamics из коллекции</span><span class="sxs-lookup"><span data-stu-id="603b0-121">Adding AppDynamics from the gallery</span></span>
2. <span data-ttu-id="603b0-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="603b0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-appdynamics-from-the-gallery"></a><span data-ttu-id="603b0-123">Добавление AppDynamics из коллекции</span><span class="sxs-lookup"><span data-stu-id="603b0-123">Adding AppDynamics from the gallery</span></span>
<span data-ttu-id="603b0-124">Чтобы настроить интеграцию AppDynamics с Azure AD, необходимо добавить AppDynamics из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="603b0-124">To configure the integration of AppDynamics into Azure AD, you need to add AppDynamics from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="603b0-125">**Чтобы добавить AppDynamics из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="603b0-125">**To add AppDynamics from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="603b0-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="603b0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="603b0-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="603b0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="603b0-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="603b0-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="603b0-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="603b0-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="603b0-133">В поле поиска введите **AppDynamics**.</span><span class="sxs-lookup"><span data-stu-id="603b0-133">In the search box, type **AppDynamics**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_search.png)

5. <span data-ttu-id="603b0-135">На панели результатов выберите **AppDynamics** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="603b0-135">In the results panel, select **AppDynamics**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="603b0-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="603b0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="603b0-138">В этом разделе описана настройка и проверка единого входа Azure AD в AppDynamics с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="603b0-138">In this section, you configure and test Azure AD single sign-on with AppDynamics based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="603b0-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в AppDynamics соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="603b0-139">For single sign-on to work, Azure AD needs to know what the counterpart user in AppDynamics is to a user in Azure AD.</span></span> <span data-ttu-id="603b0-140">Иными словами, необходимо установить связь между пользователям Azure AD и соответствующим пользователем в AppDynamics.</span><span class="sxs-lookup"><span data-stu-id="603b0-140">In other words, a link relationship between an Azure AD user and the related user in AppDynamics needs to be established.</span></span>

<span data-ttu-id="603b0-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в AppDynamics.</span><span class="sxs-lookup"><span data-stu-id="603b0-141">In AppDynamics, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="603b0-142">Чтобы настроить и проверить единый вход Azure AD в AppDynamics, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="603b0-142">To configure and test Azure AD single sign-on with AppDynamics, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="603b0-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="603b0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="603b0-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="603b0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="603b0-145">**[Создание тестового пользователя AppDynamics](#creating-an-appdynamics-test-user)** нужно для того, чтобы в AppDynamics также существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="603b0-145">**[Creating an AppDynamics test user](#creating-an-appdynamics-test-user)** - to have a counterpart of Britta Simon in AppDynamics that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="603b0-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="603b0-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="603b0-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="603b0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="603b0-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="603b0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="603b0-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении AppDynamics.</span><span class="sxs-lookup"><span data-stu-id="603b0-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your AppDynamics application.</span></span>

<span data-ttu-id="603b0-150">**Чтобы настроить единый вход Azure AD в AppDynamics, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="603b0-150">**To configure Azure AD single sign-on with AppDynamics, perform the following steps:**</span></span>

1. <span data-ttu-id="603b0-151">На портале Azure на странице интеграции с приложением **AppDynamics** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="603b0-151">In the Azure portal, on the **AppDynamics** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="603b0-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="603b0-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_samlbase.png)

3. <span data-ttu-id="603b0-155">В разделе **Домены и URL-адреса приложения AppDynamics** сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="603b0-155">On the **AppDynamics Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_url.png)

    <span data-ttu-id="603b0-157">а.</span><span class="sxs-lookup"><span data-stu-id="603b0-157">a.</span></span> <span data-ttu-id="603b0-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<companyname>.saas.appdynamics.com`</span><span class="sxs-lookup"><span data-stu-id="603b0-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.saas.appdynamics.com`</span></span>

    <span data-ttu-id="603b0-159">b.</span><span class="sxs-lookup"><span data-stu-id="603b0-159">b.</span></span> <span data-ttu-id="603b0-160">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<companyname>.saas.appdynamics.com/controller`</span><span class="sxs-lookup"><span data-stu-id="603b0-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.saas.appdynamics.com/controller`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="603b0-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="603b0-161">These values are not real.</span></span> <span data-ttu-id="603b0-162">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="603b0-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="603b0-163">Чтобы получить эти значения, обратитесь к [группе поддержки AppDynamics](https://www.appdynamics.com/support/).</span><span class="sxs-lookup"><span data-stu-id="603b0-163">Contact [AppDynamics Client support team](https://www.appdynamics.com/support/) to get these values.</span></span> 
 
4. <span data-ttu-id="603b0-164">В разделе **Сертификат для подписи токена SAML** щелкните **Certificate (Base64)** (Сертификат (Base64)), а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="603b0-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_certificate.png) 

5. <span data-ttu-id="603b0-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="603b0-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-appdynamics-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="603b0-168">В разделе **Настройка AppDynamics** щелкните **Настроить AppDynamics**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="603b0-168">On the **AppDynamics Configuration** section, click **Configure AppDynamics** to open **Configure sign-on** window.</span></span> <span data-ttu-id="603b0-169">Скопируйте **URL-адрес выхода и URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="603b0-169">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_configure.png) 

7. <span data-ttu-id="603b0-171">В другом окне веб-браузера войдите на свой корпоративный веб-сайт AppDynamics в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="603b0-171">In a different web browser window, log in to your AppDynamics company site as an administrator.</span></span>

8. <span data-ttu-id="603b0-172">Выберите меню **Settings** (Параметры) на панели инструментов в верхней части экрана и щелкните пункт **Administration** (Администрирование).</span><span class="sxs-lookup"><span data-stu-id="603b0-172">In the toolbar on the top, click **Settings**, and then click **Administration**.</span></span>
   
    <span data-ttu-id="603b0-173">![Администрирование](./media/active-directory-saas-appdynamics-tutorial/ic790216.png "Администрирование")</span><span class="sxs-lookup"><span data-stu-id="603b0-173">![Administration](./media/active-directory-saas-appdynamics-tutorial/ic790216.png "Administration")</span></span>

9. <span data-ttu-id="603b0-174">Откройте вкладку **Authentication Provider** (Поставщик проверки подлинности).</span><span class="sxs-lookup"><span data-stu-id="603b0-174">Click the **Authentication Provider** tab.</span></span>
   
    <span data-ttu-id="603b0-175">![Поставщик проверки подлинности](./media/active-directory-saas-appdynamics-tutorial/ic790224.png "Поставщик проверки подлинности")</span><span class="sxs-lookup"><span data-stu-id="603b0-175">![Authentication Provider](./media/active-directory-saas-appdynamics-tutorial/ic790224.png "Authentication Provider")</span></span>

10. <span data-ttu-id="603b0-176">В разделе **Authentication Provider** (Поставщик проверки подлинности) выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="603b0-176">In the **Authentication Provider** section, perform the following steps:</span></span>
   
    <span data-ttu-id="603b0-177">![Настройка SAML](./media/active-directory-saas-appdynamics-tutorial/ic790225.png "Настройка SAML")</span><span class="sxs-lookup"><span data-stu-id="603b0-177">![SAML Configuration](./media/active-directory-saas-appdynamics-tutorial/ic790225.png "SAML Configuration")</span></span>   

    <span data-ttu-id="603b0-178">а.</span><span class="sxs-lookup"><span data-stu-id="603b0-178">a.</span></span> <span data-ttu-id="603b0-179">Для параметра **Authentication Provider** (Поставщик проверки подлинности) выберите значение **SAML**.</span><span class="sxs-lookup"><span data-stu-id="603b0-179">As **Authentication Provider**, select **SAML**.</span></span>

    <span data-ttu-id="603b0-180">b.</span><span class="sxs-lookup"><span data-stu-id="603b0-180">b.</span></span> <span data-ttu-id="603b0-181">В текстовое поле **Login URL** (URL-адрес входа) вставьте значение **URL-адрес службы единого входа SAML**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="603b0-181">In the **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="603b0-182">c.</span><span class="sxs-lookup"><span data-stu-id="603b0-182">c.</span></span> <span data-ttu-id="603b0-183">В текстовое поле **Logout URL** (URL-адрес выхода) вставьте значение **URL-адрес выхода**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="603b0-183">In the **Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
       
    <span data-ttu-id="603b0-184">г)</span><span class="sxs-lookup"><span data-stu-id="603b0-184">d.</span></span> <span data-ttu-id="603b0-185">Откройте сертификат в кодировке Base-64 в Блокноте, скопируйте его содержимое в буфер обмена, а затем вставьте его в текстовое поле **Сертификат** .</span><span class="sxs-lookup"><span data-stu-id="603b0-185">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **Certificate** textbox</span></span>

    <span data-ttu-id="603b0-186">д.</span><span class="sxs-lookup"><span data-stu-id="603b0-186">e.</span></span> <span data-ttu-id="603b0-187">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="603b0-187">Click **Save**.</span></span>

     <span data-ttu-id="603b0-188">![Сохранить](./media/active-directory-saas-appdynamics-tutorial/ic777673.png "Сохранить")</span><span class="sxs-lookup"><span data-stu-id="603b0-188">![Save](./media/active-directory-saas-appdynamics-tutorial/ic777673.png "Save")</span></span>

> [!TIP]
> <span data-ttu-id="603b0-189">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="603b0-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="603b0-190">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="603b0-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="603b0-191">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="603b0-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="603b0-192">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="603b0-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="603b0-193">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="603b0-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="603b0-195">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="603b0-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="603b0-196">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="603b0-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-appdynamics-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="603b0-198">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="603b0-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-appdynamics-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="603b0-200">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="603b0-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-appdynamics-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="603b0-202">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="603b0-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-appdynamics-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="603b0-204">а.</span><span class="sxs-lookup"><span data-stu-id="603b0-204">a.</span></span> <span data-ttu-id="603b0-205">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="603b0-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="603b0-206">b.</span><span class="sxs-lookup"><span data-stu-id="603b0-206">b.</span></span> <span data-ttu-id="603b0-207">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="603b0-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="603b0-208">c.</span><span class="sxs-lookup"><span data-stu-id="603b0-208">c.</span></span> <span data-ttu-id="603b0-209">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="603b0-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="603b0-210">d.</span><span class="sxs-lookup"><span data-stu-id="603b0-210">d.</span></span> <span data-ttu-id="603b0-211">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="603b0-211">Click **Create**.</span></span>
 
### <a name="creating-an-appdynamics-test-user"></a><span data-ttu-id="603b0-212">Создание тестового пользователя AppDynamics</span><span class="sxs-lookup"><span data-stu-id="603b0-212">Creating an AppDynamics test user</span></span>

<span data-ttu-id="603b0-213">Чтобы пользователи Azure AD могли выполнять вход в AppDynamics, они должны быть подготовлены в AppDynamics.</span><span class="sxs-lookup"><span data-stu-id="603b0-213">To enable Azure AD users to log in to AppDynamics, they must be provisioned into AppDynamics.</span></span> <span data-ttu-id="603b0-214">В случае с AppDynamics подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="603b0-214">In the case of AppDynamics, provisioning is a manual task.</span></span>

<span data-ttu-id="603b0-215">**Чтобы настроить подготовку учетных записей пользователей, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="603b0-215">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="603b0-216">Войдите на свой корпоративный веб-сайт AppDynamics в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="603b0-216">Log in to your AppDynamics company site as an administrator.</span></span>

2. <span data-ttu-id="603b0-217">Откройте раздел **Users** (Пользователи) и щелкните значок **+**, чтобы открыть диалоговое окно **Create User** (Создание пользователя).</span><span class="sxs-lookup"><span data-stu-id="603b0-217">Go to **Users**, and then click **+** to open the **Create User** dialog.</span></span>
   
    <span data-ttu-id="603b0-218">![Пользователи](./media/active-directory-saas-appdynamics-tutorial/ic790229.png "Пользователи")</span><span class="sxs-lookup"><span data-stu-id="603b0-218">![Users](./media/active-directory-saas-appdynamics-tutorial/ic790229.png "Users")</span></span>

3. <span data-ttu-id="603b0-219">В разделе **Создание пользователя** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="603b0-219">In the **Create User** section, perform the following steps:</span></span>
   
    <span data-ttu-id="603b0-220">![Создание пользователя](./media/active-directory-saas-appdynamics-tutorial/ic790230.png "Создание пользователя")</span><span class="sxs-lookup"><span data-stu-id="603b0-220">![Create User](./media/active-directory-saas-appdynamics-tutorial/ic790230.png "Create User")</span></span>
   
    <span data-ttu-id="603b0-221">а.</span><span class="sxs-lookup"><span data-stu-id="603b0-221">a.</span></span> <span data-ttu-id="603b0-222">Введите в текстовых полях **Username** (Имя пользователя), **Name** (Имя), **Email** (Адрес электронной почты), **New Password** (Новый пароль) и **Repeat New Password** (Введите новый пароль еще раз) соответствующие данные действующей учетной записи AAD, которую вы хотите подготовить.</span><span class="sxs-lookup"><span data-stu-id="603b0-222">Type the **Username**, **Name**, **Email**, **New Password**, **Repeat New Password** of a valid AAD account you want to provision into the related textboxes.</span></span>

    <span data-ttu-id="603b0-223">b.</span><span class="sxs-lookup"><span data-stu-id="603b0-223">b.</span></span> <span data-ttu-id="603b0-224">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="603b0-224">Click **Save**.</span></span>

    >[!NOTE]
    ><span data-ttu-id="603b0-225">Вы можете использовать любые другие средства создания учетной записи пользователя AppDynamics или API, предоставляемые AppDynamics для подготовки учетных записей пользователя AAD.</span><span class="sxs-lookup"><span data-stu-id="603b0-225">You can use any other AppDynamics user account creation tools or APIs provided by AppDynamics to provision Azure AD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="603b0-226">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="603b0-226">Assigning the Azure AD test user</span></span>

<span data-ttu-id="603b0-227">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к AppDynamics.</span><span class="sxs-lookup"><span data-stu-id="603b0-227">In this section, you enable Britta Simon to use Azure single sign-on by granting access to AppDynamics.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="603b0-229">**Чтобы назначить пользователя Britta Simon в AppDynamics, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="603b0-229">**To assign Britta Simon to AppDynamics, perform the following steps:**</span></span>

1. <span data-ttu-id="603b0-230">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="603b0-230">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="603b0-232">Из списка приложений выберите **AppDynamics**.</span><span class="sxs-lookup"><span data-stu-id="603b0-232">In the applications list, select **AppDynamics**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-appdynamics-tutorial/tutorial_appdynamics_app.png) 

3. <span data-ttu-id="603b0-234">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="603b0-234">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="603b0-236">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="603b0-236">Click **Add** button.</span></span> <span data-ttu-id="603b0-237">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="603b0-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="603b0-239">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="603b0-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="603b0-240">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="603b0-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="603b0-241">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="603b0-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="603b0-242">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="603b0-242">Testing single sign-on</span></span>

<span data-ttu-id="603b0-243">Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="603b0-243">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="603b0-244">Щелкнув элемент "AppDynamics" на панели доступа, вы автоматически войдете в приложение AppDynamics.</span><span class="sxs-lookup"><span data-stu-id="603b0-244">When you click the AppDynamics tile in the Access Panel, you should get automatically signed-on to your AppDynamics application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="603b0-245">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="603b0-245">Additional resources</span></span>

* [<span data-ttu-id="603b0-246">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="603b0-246">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="603b0-247">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="603b0-247">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-appdynamics-tutorial/tutorial_general_203.png

