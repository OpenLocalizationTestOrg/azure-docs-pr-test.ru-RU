---
title: "Руководство. Интеграция Azure Active Directory с Syncplicity | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в приложении Syncplicity."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 896a3211-f368-46d7-95b8-e4768c23be08
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 1321fa71bcd625d6ea754432bfb402d3919e38f3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-syncplicity"></a><span data-ttu-id="6b068-103">Учебник. Интеграция Azure Active Directory с Syncplicity</span><span class="sxs-lookup"><span data-stu-id="6b068-103">Tutorial: Azure Active Directory integration with Syncplicity</span></span>

<span data-ttu-id="6b068-104">В этом руководстве описано, как интегрировать Syncplicity с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6b068-104">In this tutorial, you learn how to integrate Syncplicity with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6b068-105">Интеграция Azure AD с приложением Syncplicity обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="6b068-105">Integrating Syncplicity with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6b068-106">С помощью Azure AD вы можете контролировать доступ к Syncplicity.</span><span class="sxs-lookup"><span data-stu-id="6b068-106">You can control in Azure AD who has access to Syncplicity</span></span>
- <span data-ttu-id="6b068-107">Вы можете включить автоматический вход пользователей в Syncplicity (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6b068-107">You can enable your users to automatically get signed-on to Syncplicity (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6b068-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="6b068-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="6b068-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6b068-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6b068-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="6b068-110">Prerequisites</span></span>

<span data-ttu-id="6b068-111">Чтобы настроить интеграцию Azure AD с приложением Syncplicity, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="6b068-111">To configure Azure AD integration with Syncplicity, you need the following items:</span></span>

- <span data-ttu-id="6b068-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="6b068-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6b068-113">подписка Syncplicity с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="6b068-113">A Syncplicity single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6b068-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="6b068-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6b068-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="6b068-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6b068-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="6b068-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6b068-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6b068-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6b068-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="6b068-118">Scenario description</span></span>
<span data-ttu-id="6b068-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="6b068-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6b068-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="6b068-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6b068-121">Добавление Syncplicity из коллекции</span><span class="sxs-lookup"><span data-stu-id="6b068-121">Adding Syncplicity from the gallery</span></span>
2. <span data-ttu-id="6b068-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="6b068-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-syncplicity-from-the-gallery"></a><span data-ttu-id="6b068-123">Добавление Syncplicity из коллекции</span><span class="sxs-lookup"><span data-stu-id="6b068-123">Adding Syncplicity from the gallery</span></span>
<span data-ttu-id="6b068-124">Чтобы настроить интеграцию приложения Syncplicity с Azure AD, вам нужно добавить Syncplicity из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="6b068-124">To configure the integration of Syncplicity into Azure AD, you need to add Syncplicity from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6b068-125">**Чтобы добавить Syncplicity из коллекции, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="6b068-125">**To add Syncplicity from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6b068-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6b068-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6b068-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="6b068-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6b068-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="6b068-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="6b068-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="6b068-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="6b068-133">В поле поиска введите **Syncplicity**.</span><span class="sxs-lookup"><span data-stu-id="6b068-133">In the search box, type **Syncplicity**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_search.png)

5. <span data-ttu-id="6b068-135">На панели результатов выберите **Syncplicity** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="6b068-135">In the results panel, select **Syncplicity**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6b068-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="6b068-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6b068-138">В этом разделе описана настройка и проверка единого входа Azure AD в Syncplicity с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6b068-138">In this section, you configure and test Azure AD single sign-on with Syncplicity based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="6b068-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Syncplicity соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6b068-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Syncplicity is to a user in Azure AD.</span></span> <span data-ttu-id="6b068-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Syncplicity.</span><span class="sxs-lookup"><span data-stu-id="6b068-140">In other words, a link relationship between an Azure AD user and the related user in Syncplicity needs to be established.</span></span>

<span data-ttu-id="6b068-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Syncplicity.</span><span class="sxs-lookup"><span data-stu-id="6b068-141">In Syncplicity, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="6b068-142">Чтобы настроить и проверить единый вход Azure AD в Syncplicity, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="6b068-142">To configure and test Azure AD single sign-on with Syncplicity, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6b068-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="6b068-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6b068-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6b068-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6b068-145">**[Создание тестового пользователя Syncplicity](#creating-a-syncplicity-test-user)** требуется для создания пользователя Britta Simon в Syncplicity, связанного с соответствующим представлением в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6b068-145">**[Creating a Syncplicity test user](#creating-a-syncplicity-test-user)** - to have a counterpart of Britta Simon in Syncplicity that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="6b068-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6b068-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6b068-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="6b068-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6b068-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="6b068-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6b068-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Syncplicity.</span><span class="sxs-lookup"><span data-stu-id="6b068-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Syncplicity application.</span></span>

<span data-ttu-id="6b068-150">**Чтобы настроить единый вход Azure AD в Syncplicity, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="6b068-150">**To configure Azure AD single sign-on with Syncplicity, perform the following steps:**</span></span>

1. <span data-ttu-id="6b068-151">На портале Azure на странице интеграции с приложением **Syncplicity** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="6b068-151">In the Azure portal, on the **Syncplicity** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="6b068-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="6b068-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_samlbase.png)

3. <span data-ttu-id="6b068-155">В разделе **Домены и URL-адреса приложения Syncplicity** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="6b068-155">On the **Syncplicity Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_url.png)

    <span data-ttu-id="6b068-157">а.</span><span class="sxs-lookup"><span data-stu-id="6b068-157">a.</span></span> <span data-ttu-id="6b068-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<companyname>.syncplicity.com`</span><span class="sxs-lookup"><span data-stu-id="6b068-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.syncplicity.com`</span></span>

    <span data-ttu-id="6b068-159">b.</span><span class="sxs-lookup"><span data-stu-id="6b068-159">b.</span></span> <span data-ttu-id="6b068-160">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<companyname>.syncplicity.com/sp`</span><span class="sxs-lookup"><span data-stu-id="6b068-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.syncplicity.com/sp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="6b068-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="6b068-161">These values are not real.</span></span> <span data-ttu-id="6b068-162">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="6b068-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="6b068-163">Чтобы получить эти значения, обратитесь в [службу поддержки клиентов Syncplicity](https://www.syncplicity.com/contact-us).</span><span class="sxs-lookup"><span data-stu-id="6b068-163">Contact [Syncplicity Client support team](https://www.syncplicity.com/contact-us) to get these values.</span></span> 
 

4. <span data-ttu-id="6b068-164">В разделе **Сертификат для подписи токена SAML** щелкните **Certificate (Base64)** (Сертификат (Base64)), а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="6b068-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_certificate.png) 

  
5. <span data-ttu-id="6b068-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="6b068-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-syncplicity-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="6b068-168">В разделе **Конфигурация Syncplicity** щелкните **Настроить Syncplicity**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="6b068-168">On the **Syncplicity Configuration** section, click **Configure Syncplicity** to open **Configure sign-on** window.</span></span> <span data-ttu-id="6b068-169">Скопируйте **URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML**  из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="6b068-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_configure.png) 

7. <span data-ttu-id="6b068-171">Войдите в клиент **Syncplicity** .</span><span class="sxs-lookup"><span data-stu-id="6b068-171">Sign in to your **Syncplicity** tenant.</span></span>

8. <span data-ttu-id="6b068-172">В меню в верхней части страницы щелкните **Администрирование**, выберите **Параметры**, а затем — **Личный домен и единый вход**.</span><span class="sxs-lookup"><span data-stu-id="6b068-172">In the menu on the top, click **admin**, select **settings**, and then click **Custom domain and single sign-on**.</span></span>
   
    <span data-ttu-id="6b068-173">![Syncplicity](./media/active-directory-saas-syncplicity-tutorial/ic769545.png "Syncplicity")</span><span class="sxs-lookup"><span data-stu-id="6b068-173">![Syncplicity](./media/active-directory-saas-syncplicity-tutorial/ic769545.png "Syncplicity")</span></span>

9. <span data-ttu-id="6b068-174">На странице диалогового окна **Единый вход** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="6b068-174">On the **Single Sign-On (SSO)** dialog page, perform the following steps:</span></span>
   
    <span data-ttu-id="6b068-175">![Единый вход\(Единый вход\)](./media/active-directory-saas-syncplicity-tutorial/ic769550.png "Single Sign-On \\\(SSO\\\)")</span><span class="sxs-lookup"><span data-stu-id="6b068-175">![Single Sign-On \(SSO\)](./media/active-directory-saas-syncplicity-tutorial/ic769550.png "Single Sign-On \\\(SSO\\\)")</span></span>   

    <span data-ttu-id="6b068-176">а.</span><span class="sxs-lookup"><span data-stu-id="6b068-176">a.</span></span> <span data-ttu-id="6b068-177">В текстовом поле **Личный домен** введите имя своего домена.</span><span class="sxs-lookup"><span data-stu-id="6b068-177">In the **Custom Domain** textbox, type the name of your domain.</span></span>
  
    <span data-ttu-id="6b068-178">b.</span><span class="sxs-lookup"><span data-stu-id="6b068-178">b.</span></span> <span data-ttu-id="6b068-179">В поле **Состояния единого входа** задайте значение **Включено**.</span><span class="sxs-lookup"><span data-stu-id="6b068-179">Select **Enabled** as **Single Sign-On Status**.</span></span>

    <span data-ttu-id="6b068-180">c.</span><span class="sxs-lookup"><span data-stu-id="6b068-180">c.</span></span> <span data-ttu-id="6b068-181">В текстовое поле **Идентификатор сущности** вставьте значение **идентификатора сущности SAML**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="6b068-181">In the **Entity Id** textbox, Paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="6b068-182">г)</span><span class="sxs-lookup"><span data-stu-id="6b068-182">d.</span></span> <span data-ttu-id="6b068-183">В текстовое поле **URL-адрес страницы входа** вставьте значение **URL-адреса службы единого входа SAML**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="6b068-183">In the **Sign-in page URL** textbox, Paste the **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="6b068-184">д.</span><span class="sxs-lookup"><span data-stu-id="6b068-184">e.</span></span> <span data-ttu-id="6b068-185">В текстовое поле **URL-адрес выхода** вставьте значение **URL-адреса выхода**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="6b068-185">In the **Logout page URL** textbox, Paste the **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="6b068-186">Е.</span><span class="sxs-lookup"><span data-stu-id="6b068-186">f.</span></span> <span data-ttu-id="6b068-187">Напротив пункта **Identity Provider Certificate** (Сертификат поставщика удостоверений) нажмите кнопку **Выбрать файл**, а затем отправьте сертификат, скачанный с портала Azure.</span><span class="sxs-lookup"><span data-stu-id="6b068-187">In **Identity Provider Certificate**, click **Choose file**, and then upload the certificate which you have downloaded from the Azure portal.</span></span> 

    <span data-ttu-id="6b068-188">g.</span><span class="sxs-lookup"><span data-stu-id="6b068-188">g.</span></span> <span data-ttu-id="6b068-189">Нажмите кнопку **Сохранить изменения**.</span><span class="sxs-lookup"><span data-stu-id="6b068-189">Click **SAVE CHANGES**.</span></span>

> [!TIP]
> <span data-ttu-id="6b068-190">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="6b068-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="6b068-191">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="6b068-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="6b068-192">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="6b068-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6b068-193">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="6b068-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="6b068-194">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6b068-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="6b068-196">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="6b068-196">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6b068-197">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6b068-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6b068-199">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="6b068-199">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6b068-201">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="6b068-201">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6b068-203">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="6b068-203">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-syncplicity-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6b068-205">а.</span><span class="sxs-lookup"><span data-stu-id="6b068-205">a.</span></span> <span data-ttu-id="6b068-206">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6b068-206">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6b068-207">b.</span><span class="sxs-lookup"><span data-stu-id="6b068-207">b.</span></span> <span data-ttu-id="6b068-208">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="6b068-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6b068-209">c.</span><span class="sxs-lookup"><span data-stu-id="6b068-209">c.</span></span> <span data-ttu-id="6b068-210">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="6b068-210">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="6b068-211">d.</span><span class="sxs-lookup"><span data-stu-id="6b068-211">d.</span></span> <span data-ttu-id="6b068-212">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="6b068-212">Click **Create**.</span></span>
 
### <a name="creating-a-syncplicity-test-user"></a><span data-ttu-id="6b068-213">Создание тестового пользователя Syncplicity</span><span class="sxs-lookup"><span data-stu-id="6b068-213">Creating a Syncplicity test user</span></span>
<span data-ttu-id="6b068-214">Чтобы пользователи AAD могли входить систему, их необходимо подготовить для Syncplicity.</span><span class="sxs-lookup"><span data-stu-id="6b068-214">For AAD users to be able to sign in, they must be provisioned to Syncplicity application.</span></span> <span data-ttu-id="6b068-215">В этом разделе описывается порядок создания учетных записей пользователей AAD в Syncplicity.</span><span class="sxs-lookup"><span data-stu-id="6b068-215">This section describes how to create AAD user accounts in Syncplicity.</span></span>

<span data-ttu-id="6b068-216">**Чтобы подготовить учетную запись пользователя в Syncplicity, выполните следующее.**</span><span class="sxs-lookup"><span data-stu-id="6b068-216">**To provision a user account to Syncplicity, perform the following steps:**</span></span>

1. <span data-ttu-id="6b068-217">Войдите в клиент **Syncplicity** (например: `https://company.Syncplicity.com`).</span><span class="sxs-lookup"><span data-stu-id="6b068-217">Log in to your **Syncplicity** tenant (for example: `https://company.Syncplicity.com`).</span></span>

2. <span data-ttu-id="6b068-218">Щелкните **Администрирование** и выберите **Учетные записи пользователей**.</span><span class="sxs-lookup"><span data-stu-id="6b068-218">Click **admin** and select **user accounts**.</span></span>

3. <span data-ttu-id="6b068-219">Нажмите кнопку **Добавить пользователя**.</span><span class="sxs-lookup"><span data-stu-id="6b068-219">Click **ADD A USER**.</span></span>
   
    <span data-ttu-id="6b068-220">![Управление пользователями](./media/active-directory-saas-syncplicity-tutorial/ic769764.png "Управление пользователями")</span><span class="sxs-lookup"><span data-stu-id="6b068-220">![Manage Users](./media/active-directory-saas-syncplicity-tutorial/ic769764.png "Manage Users")</span></span>

4. <span data-ttu-id="6b068-221">Введите **адреса электронной почты** учетной записи AAD, которую необходимо подготовить, задайте значение **Пользователь** в поле **Роль**, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="6b068-221">Type the **Email addressess** of an AAD account you want to provision, select **User** as **Role**, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="6b068-222">![Сведения об учетной записи](./media/active-directory-saas-syncplicity-tutorial/ic769765.png "Сведения об учетной записи")</span><span class="sxs-lookup"><span data-stu-id="6b068-222">![Account Information](./media/active-directory-saas-syncplicity-tutorial/ic769765.png "Account Information")</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="6b068-223">Владелец учетной записи AAD получит электронное сообщение, содержащее ссылку для подтверждения и активации учетной записи.</span><span class="sxs-lookup"><span data-stu-id="6b068-223">The AAD account holder  gets an email including a link to confirm and activate the account.</span></span> 
    > 

5. <span data-ttu-id="6b068-224">Выберите группу в организации, в которую будет входить новый пользователь, а затем нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="6b068-224">Select a group in your company that your new user should become a member of, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="6b068-225">![Участие в группах](./media/active-directory-saas-syncplicity-tutorial/ic769772.png "Участие в группах")</span><span class="sxs-lookup"><span data-stu-id="6b068-225">![Group Membership](./media/active-directory-saas-syncplicity-tutorial/ic769772.png "Group Membership")</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="6b068-226">Если список групп пуст, просто нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="6b068-226">If there are no groups listed, click **NEXT**.</span></span> 
    > 

6. <span data-ttu-id="6b068-227">Выберите папки, которые будут находиться под управлением Syncplicity на компьютере пользователя, и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="6b068-227">Select the folders you would like to place under Syncplicity’s control on the user’s computer, and then click **NEXT**.</span></span>
   
    <span data-ttu-id="6b068-228">![Папки Syncplicity](./media/active-directory-saas-syncplicity-tutorial/ic769773.png "Папки Syncplicity")</span><span class="sxs-lookup"><span data-stu-id="6b068-228">![Syncplicity Folders](./media/active-directory-saas-syncplicity-tutorial/ic769773.png "Syncplicity Folders")</span></span>

>[!NOTE]
><span data-ttu-id="6b068-229">Вы можете использовать любые другие средства создания учетной записи пользователя Syncplicity или API-интерфейсы, предоставляемые Syncplicity для подготовки учетных записей пользователя AAD.</span><span class="sxs-lookup"><span data-stu-id="6b068-229">You can use any other Syncplicity user account creation tools or APIs provided by Syncplicity to provision AAD user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="6b068-230">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="6b068-230">Assigning the Azure AD test user</span></span>

<span data-ttu-id="6b068-231">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure путем предоставления доступа к Syncplicity.</span><span class="sxs-lookup"><span data-stu-id="6b068-231">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Syncplicity.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="6b068-233">**Чтобы назначить пользователя Britta Simon приложению Syncplicity, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="6b068-233">**To assign Britta Simon to Syncplicity, perform the following steps:**</span></span>

1. <span data-ttu-id="6b068-234">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="6b068-234">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="6b068-236">В списке приложений выберите **Syncplicity**.</span><span class="sxs-lookup"><span data-stu-id="6b068-236">In the applications list, select **Syncplicity**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-syncplicity-tutorial/tutorial_syncplicity_app.png) 

3. <span data-ttu-id="6b068-238">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="6b068-238">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="6b068-240">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="6b068-240">Click **Add** button.</span></span> <span data-ttu-id="6b068-241">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="6b068-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="6b068-243">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="6b068-243">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="6b068-244">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="6b068-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6b068-245">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="6b068-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6b068-246">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="6b068-246">Testing single sign-on</span></span>

<span data-ttu-id="6b068-247">Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="6b068-247">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="6b068-248">Щелкнув элемент Syncplicity на панели доступа, вы автоматически войдете в приложение Syncplicity.</span><span class="sxs-lookup"><span data-stu-id="6b068-248">When you click the Syncplicity tile in the Access Panel, you should get automatically signed-on to your Syncplicity application.</span></span>
## <a name="additional-resources"></a><span data-ttu-id="6b068-249">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="6b068-249">Additional resources</span></span>

* [<span data-ttu-id="6b068-250">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6b068-250">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6b068-251">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6b068-251">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-syncplicity-tutorial/tutorial_general_203.png

