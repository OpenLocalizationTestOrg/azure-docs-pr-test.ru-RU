---
title: "Учебник. Интеграция Azure Active Directory с InsideView | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в приложении InsideView."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c489a7ab-6b1f-4efb-8a66-8bc13bca78c3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: f2b0a1d4bc44f8d0cd57c61e2d78950cb6a99854
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-insideview"></a><span data-ttu-id="9bcbd-103">Руководство. Интеграция Azure Active Directory с InsideView</span><span class="sxs-lookup"><span data-stu-id="9bcbd-103">Tutorial: Azure Active Directory integration with InsideView</span></span>

<span data-ttu-id="9bcbd-104">В этом руководстве описано, как интегрировать InsideView с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9bcbd-104">In this tutorial, you learn how to integrate InsideView with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="9bcbd-105">Интеграция InsideView с Azure AD обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="9bcbd-105">Integrating InsideView with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="9bcbd-106">С помощью Azure AD вы можете контролировать доступ к InsideView.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-106">You can control in Azure AD who has access to InsideView</span></span>
- <span data-ttu-id="9bcbd-107">Вы можете включить автоматический вход пользователей в InsideView (единый вход) с использованием учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-107">You can enable your users to automatically get signed-on to InsideView (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="9bcbd-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="9bcbd-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="9bcbd-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9bcbd-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="9bcbd-110">Prerequisites</span></span>

<span data-ttu-id="9bcbd-111">Чтобы настроить интеграцию Azure AD с InsideView, вам нужно:</span><span class="sxs-lookup"><span data-stu-id="9bcbd-111">To configure Azure AD integration with InsideView, you need the following items:</span></span>

- <span data-ttu-id="9bcbd-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="9bcbd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="9bcbd-113">подписка с поддержкой единого входа InsideView.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-113">A InsideView single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="9bcbd-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="9bcbd-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="9bcbd-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="9bcbd-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="9bcbd-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9bcbd-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="9bcbd-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="9bcbd-118">Scenario description</span></span>
<span data-ttu-id="9bcbd-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="9bcbd-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="9bcbd-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="9bcbd-121">Добавление InsideView из коллекции.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-121">Adding InsideView from the gallery</span></span>
2. <span data-ttu-id="9bcbd-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="9bcbd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-insideview-from-the-gallery"></a><span data-ttu-id="9bcbd-123">Добавление InsideView из коллекции</span><span class="sxs-lookup"><span data-stu-id="9bcbd-123">Adding InsideView from the gallery</span></span>
<span data-ttu-id="9bcbd-124">Чтобы настроить интеграцию InsideView с Azure AD, нужно добавить InsideView из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-124">To configure the integration of InsideView in to Azure AD, you need to add InsideView from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="9bcbd-125">**Чтобы добавить InsideView из коллекции, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="9bcbd-125">**To add InsideView from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="9bcbd-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="9bcbd-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="9bcbd-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="9bcbd-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="9bcbd-133">В поле поиска введите **InsideView**.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-133">In the search box, type **InsideView**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_search.png)

5. <span data-ttu-id="9bcbd-135">На панели результатов выберите **InsideView** и выберите **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-135">In the results panel, select **InsideView**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="9bcbd-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="9bcbd-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="9bcbd-138">В этом разделе описана настройка и проверка единого входа Azure AD в InsideView с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-138">In this section, you configure and test Azure AD single sign-on with InsideView based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="9bcbd-139">Чтобы единый вход работал, Azure AD необходимо знать, какой пользователь в InsideView соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-139">For single sign-on to work, Azure AD needs to know what the counterpart user in InsideView is to a user in Azure AD.</span></span> <span data-ttu-id="9bcbd-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в InsideView.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-140">In other words, a link relationship between an Azure AD user and the related user in InsideView needs to be established.</span></span>

<span data-ttu-id="9bcbd-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в InsideView.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-141">In InsideView, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="9bcbd-142">Чтобы настроить и проверить единый вход Azure AD в InsideView, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="9bcbd-142">To configure and test Azure AD single sign-on with InsideView, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="9bcbd-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="9bcbd-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="9bcbd-145">**[Создание тестового пользователя InsideView](#creating-a-insideview-test-user)** требуется для создания в InsideView пользователя Britta Simon, связанного с представлением этого пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-145">**[Creating a InsideView test user](#creating-a-insideview-test-user)** - to have a counterpart of Britta Simon in InsideView that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="9bcbd-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="9bcbd-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="9bcbd-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="9bcbd-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="9bcbd-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении InsideView.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your InsideView application.</span></span>

<span data-ttu-id="9bcbd-150">**Чтобы настроить единый вход Azure AD в InsideView, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="9bcbd-150">**To configure Azure AD single sign-on with InsideView, perform the following steps:**</span></span>

1. <span data-ttu-id="9bcbd-151">На портале Azure на странице интеграции с приложением **InsideView** выберите **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-151">In the Azure portal, on the **InsideView** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="9bcbd-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_samlbase.png)

3. <span data-ttu-id="9bcbd-155">В разделе **Домены и URL-адреса приложения InsideView** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="9bcbd-155">On the **InsideView Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_url.png)
    
    <span data-ttu-id="9bcbd-157">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате: `https://my.insideview.com/iv/<STS Name>/login.iv`.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://my.insideview.com/iv/<STS Name>/login.iv`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="9bcbd-158">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-158">This value is not real.</span></span> <span data-ttu-id="9bcbd-159">Вместо него нужно указать фактический URL-адрес ответа.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-159">Update this value with the actual Reply URL.</span></span> <span data-ttu-id="9bcbd-160">Чтобы получить это значение, обратитесь в [службу поддержки InsideView](mailto:support@insideview.com).</span><span class="sxs-lookup"><span data-stu-id="9bcbd-160">Contact [InsideView support team ](mailto:support@insideview.com) to get this value.</span></span>
 
4. <span data-ttu-id="9bcbd-161">В разделе **Сертификат подписи SAML** щелкните **Certificate (Raw)** (Сертификат (необработанный)), а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-161">On the **SAML Signing Certificate** section, click **Certificate (Raw)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_certificate.png) 

5. <span data-ttu-id="9bcbd-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="9bcbd-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-insideview-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="9bcbd-165">В разделе **Настройка InsideView** выберите **Настроить InsideView**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-165">On the **InsideView Configuration** section, click **Configure InsideView** to open **Configure sign-on** window.</span></span> <span data-ttu-id="9bcbd-166">Скопируйте **URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-166">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_configure.png) 

7. <span data-ttu-id="9bcbd-168">В другом окне веб-браузера войдите на свой корпоративный веб-сайт InsideView в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-168">In a different web browser window, log in to your InsideView company site as an administrator.</span></span>

8. <span data-ttu-id="9bcbd-169">На панели инструментов в верхней части экрана щелкните **Admin** (Администрирование), **SingleSignOn Settings** (Параметры единого входа) и выберите **Add SAML** (Добавить SAML).</span><span class="sxs-lookup"><span data-stu-id="9bcbd-169">In the toolbar on the top, click **Admin**, **SingleSignOn Settings**, and then click **Add SAML**.</span></span>
   
   <span data-ttu-id="9bcbd-170">![Параметры единого входа SAML](./media/active-directory-saas-insideview-tutorial/ic794135.png "Параметры единого входа SAML")</span><span class="sxs-lookup"><span data-stu-id="9bcbd-170">![SAML Single Sign On Settings](./media/active-directory-saas-insideview-tutorial/ic794135.png "SAML Single Sign On Settings")</span></span>

9. <span data-ttu-id="9bcbd-171">В разделе **Добавить SAML** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="9bcbd-171">In the **Add a New SAML** section, perform the following steps:</span></span>

    <span data-ttu-id="9bcbd-172">![Добавление SAML](./media/active-directory-saas-insideview-tutorial/ic794136.png "Добавление SAML")</span><span class="sxs-lookup"><span data-stu-id="9bcbd-172">![Add a New SAML](./media/active-directory-saas-insideview-tutorial/ic794136.png "Add a New SAML")</span></span>
   
    <span data-ttu-id="9bcbd-173">а.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-173">a.</span></span> <span data-ttu-id="9bcbd-174">В текстовом поле **Имя службы токенов безопасности** введите имя конфигурации.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-174">In the **STS Name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="9bcbd-175">b.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-175">b.</span></span> <span data-ttu-id="9bcbd-176">В текстовое поле **SamlP/WS-Fed Unsolicited EndPoint** (Незапрашиваемая конечная точка WS-Fed/SamlP) вставьте значение **URL-адреса службы единого входа SAML**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-176">In **SamlP/WS-Fed Unsolicited EndPoint** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="9bcbd-177">c.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-177">c.</span></span> <span data-ttu-id="9bcbd-178">Откройте сертификат в кодировке Base-64, скачанный на портале Azure, скопируйте его содержимое в буфер обмена, а затем вставьте его в текстовое поле **STS Certificate** (Сертификат STS).</span><span class="sxs-lookup"><span data-stu-id="9bcbd-178">Open your base-64 encoded certificate, which you have downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **STS Certificate** textbox.</span></span>

    <span data-ttu-id="9bcbd-179">г)</span><span class="sxs-lookup"><span data-stu-id="9bcbd-179">d.</span></span> <span data-ttu-id="9bcbd-180">В **Crm User Id Mapping** (Сопоставление идентификаторов пользователей Crm) введите `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-180">In the **Crm User Id Mapping** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>
        
    <span data-ttu-id="9bcbd-181">д.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-181">e.</span></span> <span data-ttu-id="9bcbd-182">В **Crm Email Mapping** (Сопоставление адресов электронной почты CRM) введите `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-182">In the **Crm Email Mapping** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>

    <span data-ttu-id="9bcbd-183">f.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-183">f.</span></span> <span data-ttu-id="9bcbd-184">В **Crm First Name Mapping** (Сопоставление имен CRM) введите `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-184">In the **Crm First Name Mapping** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span></span>
    
    <span data-ttu-id="9bcbd-185">ж.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-185">g.</span></span> <span data-ttu-id="9bcbd-186">В **Crm lastName Mapping** (Сопоставление фамилий CRM) введите `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-186">In the **Crm lastName Mapping** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span></span>  

    <span data-ttu-id="9bcbd-187">h.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-187">h.</span></span> <span data-ttu-id="9bcbd-188">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-188">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="9bcbd-189">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="9bcbd-190">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="9bcbd-191">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="9bcbd-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="9bcbd-192">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="9bcbd-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="9bcbd-193">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="9bcbd-195">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="9bcbd-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="9bcbd-196">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-insideview-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="9bcbd-198">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-insideview-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="9bcbd-200">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-insideview-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="9bcbd-202">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-insideview-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="9bcbd-204">а.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-204">a.</span></span> <span data-ttu-id="9bcbd-205">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="9bcbd-206">b.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-206">b.</span></span> <span data-ttu-id="9bcbd-207">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="9bcbd-208">c.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-208">c.</span></span> <span data-ttu-id="9bcbd-209">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="9bcbd-210">d.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-210">d.</span></span> <span data-ttu-id="9bcbd-211">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-211">Click **Create**.</span></span>
 
### <a name="creating-a-insideview-test-user"></a><span data-ttu-id="9bcbd-212">Создание тестового пользователя InsideView</span><span class="sxs-lookup"><span data-stu-id="9bcbd-212">Creating a InsideView test user</span></span>

<span data-ttu-id="9bcbd-213">Чтобы пользователи Azure AD могли выполнять вход в InsideView, им нужна определенная информация об InsideView.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-213">To enable Azure AD users to log in to InsideView, they must be provisioned in to InsideView.</span></span> <span data-ttu-id="9bcbd-214">В случае с InsideView подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-214">In the case of InsideView, provisioning is a manual task.</span></span>

<span data-ttu-id="9bcbd-215">Чтобы создать контакты и пользователей в InsideView, обратитесь в [службу поддержки InsideView](mailto:support@insideview.com).</span><span class="sxs-lookup"><span data-stu-id="9bcbd-215">To get users or contacts created in InsideView, Contact [InsideView support team](mailto:support@insideview.com).</span></span>

>[!NOTE]
><span data-ttu-id="9bcbd-216">Вы можете использовать любые другие инструменты создания учетных записей пользователя InsideView или API, предоставляемые InsideView для подготовки учетных записей пользователя AAD.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-216">You can use any other InsideView user account creation tools or APIs provided by InsideView to provision Azure AD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="9bcbd-217">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="9bcbd-217">Assigning the Azure AD test user</span></span>

<span data-ttu-id="9bcbd-218">В этом разделе описано, как предоставить пользователю Britta Simon доступ к InsideView, чтобы он мог использовать единый вход Azure.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-218">In this section, you enable Britta Simon to use Azure single sign-on by granting access to InsideView.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="9bcbd-220">**Чтобы назначить пользователя Britta Simon в InsideView, выполните следующие указания:**</span><span class="sxs-lookup"><span data-stu-id="9bcbd-220">**To assign Britta Simon to InsideView, perform the following steps:**</span></span>

1. <span data-ttu-id="9bcbd-221">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-221">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="9bcbd-223">В списке приложений выберите **InsideView**.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-223">In the applications list, select **InsideView**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-insideview-tutorial/tutorial_insideview_app.png) 

3. <span data-ttu-id="9bcbd-225">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-225">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="9bcbd-227">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-227">Click **Add** button.</span></span> <span data-ttu-id="9bcbd-228">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-228">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="9bcbd-230">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-230">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="9bcbd-231">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-231">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="9bcbd-232">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-232">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="9bcbd-233">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="9bcbd-233">Testing single sign-on</span></span>

<span data-ttu-id="9bcbd-234">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-234">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="9bcbd-235">Щелкнув элемент InsideView на панели доступа, вы автоматически войдете в приложение InsideView.</span><span class="sxs-lookup"><span data-stu-id="9bcbd-235">When you click the InsideView tile in the Access Panel, you should get automatically signed-on to your InsideView application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="9bcbd-236">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="9bcbd-236">Additional resources</span></span>

* [<span data-ttu-id="9bcbd-237">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9bcbd-237">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="9bcbd-238">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="9bcbd-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-insideview-tutorial/tutorial_general_203.png

