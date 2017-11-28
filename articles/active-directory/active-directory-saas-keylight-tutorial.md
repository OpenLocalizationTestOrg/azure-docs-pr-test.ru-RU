---
title: "Руководство по интеграции Azure Active Directory с LockPath Keylight | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в LockPath Keylight."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 234a32f1-9f56-4650-9e31-7b38ad734b1a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: e64a966f24411818abc4cc4ab29a428b5577d012
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lockpath-keylight"></a><span data-ttu-id="52eb9-103">Руководство по интеграции Azure Active Directory с LockPath Keylight</span><span class="sxs-lookup"><span data-stu-id="52eb9-103">Tutorial: Azure Active Directory integration with LockPath Keylight</span></span>

<span data-ttu-id="52eb9-104">В этом руководстве описано, как интегрировать LockPath Keylight с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="52eb9-104">In this tutorial, you learn how to integrate LockPath Keylight with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="52eb9-105">Интеграция Azure AD с приложением LockPath Keylight обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="52eb9-105">Integrating LockPath Keylight with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="52eb9-106">С помощью Azure AD вы можете контролировать доступ к LockPath Keylight.</span><span class="sxs-lookup"><span data-stu-id="52eb9-106">You can control in Azure AD who has access to LockPath Keylight</span></span>
- <span data-ttu-id="52eb9-107">Вы можете включить автоматический вход пользователей в LockPath Keylight (единый вход) с использованием учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="52eb9-107">You can enable your users to automatically get signed-on to LockPath Keylight (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="52eb9-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="52eb9-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="52eb9-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="52eb9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="52eb9-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="52eb9-110">Prerequisites</span></span>

<span data-ttu-id="52eb9-111">Чтобы настроить интеграцию Azure AD с LockPath Keylight, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="52eb9-111">To configure Azure AD integration with LockPath Keylight, you need the following items:</span></span>

- <span data-ttu-id="52eb9-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="52eb9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="52eb9-113">подписка LockPath Keylight с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="52eb9-113">A LockPath Keylight single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="52eb9-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="52eb9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="52eb9-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="52eb9-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="52eb9-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="52eb9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="52eb9-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="52eb9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="52eb9-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="52eb9-118">Scenario description</span></span>
<span data-ttu-id="52eb9-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="52eb9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="52eb9-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="52eb9-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="52eb9-121">Добавление LockPath Keylight из коллекции.</span><span class="sxs-lookup"><span data-stu-id="52eb9-121">Adding LockPath Keylight from the gallery</span></span>
2. <span data-ttu-id="52eb9-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="52eb9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lockpath-keylight-from-the-gallery"></a><span data-ttu-id="52eb9-123">Добавление LockPath Keylight из коллекции</span><span class="sxs-lookup"><span data-stu-id="52eb9-123">Adding LockPath Keylight from the gallery</span></span>
<span data-ttu-id="52eb9-124">Чтобы настроить интеграцию LockPath Keylight с Azure AD, необходимо добавить LockPath Keylight из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="52eb9-124">To configure the integration of LockPath Keylight into Azure AD, you need to add LockPath Keylight from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="52eb9-125">**Чтобы добавить LockPath Keylight из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="52eb9-125">**To add LockPath Keylight from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="52eb9-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="52eb9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="52eb9-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="52eb9-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="52eb9-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="52eb9-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="52eb9-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="52eb9-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="52eb9-133">В поле поиска введите **LockPath Keylight**.</span><span class="sxs-lookup"><span data-stu-id="52eb9-133">In the search box, type **LockPath Keylight**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_search.png)

5. <span data-ttu-id="52eb9-135">На панели результатов выберите **LockPath Keylight** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="52eb9-135">In the results panel, select **LockPath Keylight**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="52eb9-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="52eb9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="52eb9-138">В этом разделе описана настройка и проверка единого входа Azure AD в LockPath Keylight с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="52eb9-138">In this section, you configure and test Azure AD single sign-on with LockPath Keylight based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="52eb9-139">Чтобы единый вход работал, Azure AD необходима информация о том, какой пользователь в LockPath Keylight соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="52eb9-139">For single sign-on to work, Azure AD needs to know what the counterpart user in LockPath Keylight is to a user in Azure AD.</span></span> <span data-ttu-id="52eb9-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в LockPath Keylight.</span><span class="sxs-lookup"><span data-stu-id="52eb9-140">In other words, a link relationship between an Azure AD user and the related user in LockPath Keylight needs to be established.</span></span>

<span data-ttu-id="52eb9-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в LockPath Keylight.</span><span class="sxs-lookup"><span data-stu-id="52eb9-141">In LockPath Keylight, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="52eb9-142">Чтобы настроить и проверить единый вход Azure AD в LockPath Keylight, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="52eb9-142">To configure and test Azure AD single sign-on with LockPath Keylight, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="52eb9-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="52eb9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="52eb9-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="52eb9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="52eb9-145">**[Создание тестового пользователя LockPath Keylight](#creating-a-lockpath-keylight-test-user)** требуется для того, чтобы в LockPath Keylight существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="52eb9-145">**[Creating a LockPath Keylight test user](#creating-a-lockpath-keylight-test-user)** - to have a counterpart of Britta Simon in LockPath Keylight that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="52eb9-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="52eb9-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="52eb9-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="52eb9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="52eb9-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="52eb9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="52eb9-149">В данном разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении LockPath Keylight.</span><span class="sxs-lookup"><span data-stu-id="52eb9-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your LockPath Keylight application.</span></span>

<span data-ttu-id="52eb9-150">**Чтобы настроить единый вход Azure AD в LockPath Keylight, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="52eb9-150">**To configure Azure AD single sign-on with LockPath Keylight, perform the following steps:**</span></span>

1. <span data-ttu-id="52eb9-151">На портале Azure на странице интеграции с приложением **LockPath Keylight** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="52eb9-151">In the Azure portal, on the **LockPath Keylight** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="52eb9-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="52eb9-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_samlbase.png)

3. <span data-ttu-id="52eb9-155">В разделе **Домены и URL-адреса приложения LockPath Keylight** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="52eb9-155">On the **LockPath Keylight Domain and URLs** section, perform the following steps::</span></span>

    ![Настройка единого входа](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_url.png)

    <span data-ttu-id="52eb9-157">а.</span><span class="sxs-lookup"><span data-stu-id="52eb9-157">a.</span></span> <span data-ttu-id="52eb9-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<company name>.keylightgrc.com/`</span><span class="sxs-lookup"><span data-stu-id="52eb9-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.keylightgrc.com/`</span></span>

    <span data-ttu-id="52eb9-159">b.</span><span class="sxs-lookup"><span data-stu-id="52eb9-159">b.</span></span> <span data-ttu-id="52eb9-160">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<company name>.keylightgrc.com`</span><span class="sxs-lookup"><span data-stu-id="52eb9-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.keylightgrc.com`</span></span>

    <span data-ttu-id="52eb9-161">c.</span><span class="sxs-lookup"><span data-stu-id="52eb9-161">c.</span></span> <span data-ttu-id="52eb9-162">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате: `https://<company name>.keylightgrc.com/Login.aspx`.</span><span class="sxs-lookup"><span data-stu-id="52eb9-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.keylightgrc.com/Login.aspx`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="52eb9-163">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="52eb9-163">These values are not real.</span></span> <span data-ttu-id="52eb9-164">Замените их фактическими значениями идентификатора, URL-адреса ответа и URL-адреса входа.</span><span class="sxs-lookup"><span data-stu-id="52eb9-164">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="52eb9-165">Чтобы получить эти значения, обратитесь к [группе поддержки клиентов LockPath Keylight](https://www.lockpath.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="52eb9-165">Contact [LockPath Keylight Client support team](https://www.lockpath.com/contact/) to get these values.</span></span> 

4. <span data-ttu-id="52eb9-166">В разделе **Сертификат подписи SAML** щелкните **Сертификат (необработанный)**, а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="52eb9-166">On the **SAML Signing Certificate** section, click **Certificate(Raw)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_certificate.png) 

5. <span data-ttu-id="52eb9-168">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="52eb9-168">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-keylight-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="52eb9-170">В разделе **Конфигурация LockPath Keylight** щелкните **Настроить LockPath Keylight**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="52eb9-170">On the **LockPath Keylight Configuration** section, click **Configure LockPath Keylight** to open **Configure sign-on** window.</span></span> <span data-ttu-id="52eb9-171">Скопируйте **URL-адрес выхода и URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="52eb9-171">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_configure.png) 

7. <span data-ttu-id="52eb9-173">Чтобы включить единый вход в LockPath Keylight, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="52eb9-173">To enable SSO in LockPath Keylight, perform the following steps:</span></span>
   
    <span data-ttu-id="52eb9-174">а.</span><span class="sxs-lookup"><span data-stu-id="52eb9-174">a.</span></span> <span data-ttu-id="52eb9-175">Войдите в учетную запись LockPath Keylight в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="52eb9-175">Sign-on to your LockPath Keylight account as administrator.</span></span>
    
    <span data-ttu-id="52eb9-176">b.</span><span class="sxs-lookup"><span data-stu-id="52eb9-176">b.</span></span> <span data-ttu-id="52eb9-177">В меню вверху щелкните **Person** (Пользователь) и выберите **Keylight Setup** (Настройка Keylight).</span><span class="sxs-lookup"><span data-stu-id="52eb9-177">In the menu on the top, click **Person**, and select **Keylight Setup**.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-keylight-tutorial/401.png) 

    <span data-ttu-id="52eb9-179">c.</span><span class="sxs-lookup"><span data-stu-id="52eb9-179">c.</span></span> <span data-ttu-id="52eb9-180">В представлении в виде дерева слева щелкните **SAML**.</span><span class="sxs-lookup"><span data-stu-id="52eb9-180">In the treeview on the left, click **SAML**.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-keylight-tutorial/402.png) 

    <span data-ttu-id="52eb9-182">d.</span><span class="sxs-lookup"><span data-stu-id="52eb9-182">d.</span></span> <span data-ttu-id="52eb9-183">В диалоговом окне **SAML Settings** (Параметры SAML) нажмите кнопку **Edit** (Изменить).</span><span class="sxs-lookup"><span data-stu-id="52eb9-183">On the **SAML Settings** dialog, click **Edit**.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-keylight-tutorial/404.png) 

8. <span data-ttu-id="52eb9-185">На странице диалогового окна **Изменение параметров SAML** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="52eb9-185">On the **Edit SAML Settings** dialog page, perform the following steps:</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-keylight-tutorial/405.png) 
   
    <span data-ttu-id="52eb9-187">а.</span><span class="sxs-lookup"><span data-stu-id="52eb9-187">a.</span></span> <span data-ttu-id="52eb9-188">Задайте для параметра **SAML authentication** (Аутентификация SAML) значение **Active** (Активно).</span><span class="sxs-lookup"><span data-stu-id="52eb9-188">Set **SAML authentication** to **Active**.</span></span>

    <span data-ttu-id="52eb9-189">b.</span><span class="sxs-lookup"><span data-stu-id="52eb9-189">b.</span></span> <span data-ttu-id="52eb9-190">Вставьте значение **SAML Single Sign-On Service URL** (URL-адрес службы единого входа SAML), скопированное на портале Azure, в текстовое поле **Identity Provider Login URL** (URL-адрес входа поставщика удостоверений).</span><span class="sxs-lookup"><span data-stu-id="52eb9-190">Paste the **SAML Single Sign-On Service URL** value which you have copied from the Azure portal into the **Identity Provider Login URL** textbox.</span></span>

    <span data-ttu-id="52eb9-191">c.</span><span class="sxs-lookup"><span data-stu-id="52eb9-191">c.</span></span> <span data-ttu-id="52eb9-192">Вставьте значение **URL-адрес службы единого выхода**, скопированное на портале Azure, в текстовое поле **Identity Provider Logout URL** (URL-адрес выхода поставщика удостоверений).</span><span class="sxs-lookup"><span data-stu-id="52eb9-192">Paste the **Single Sign-Out Service URL** value which you have copied from the Azure portal into the **Identity Provider Logout URL** textbox.</span></span>

    <span data-ttu-id="52eb9-193">г)</span><span class="sxs-lookup"><span data-stu-id="52eb9-193">d.</span></span> <span data-ttu-id="52eb9-194">Щелкните **Choose File** (Выбрать файл), чтобы выбрать скачанный сертификат LockPath Keylight, а затем нажмите кнопку **Open** (Открыть), чтобы передать этот сертификат.</span><span class="sxs-lookup"><span data-stu-id="52eb9-194">Click **Choose File** to select your downloaded LockPath Keylight certificate, and then click **Open** to upload the certificate.</span></span>

    <span data-ttu-id="52eb9-195">д.</span><span class="sxs-lookup"><span data-stu-id="52eb9-195">e.</span></span> <span data-ttu-id="52eb9-196">В поле **SAML User Id location** (Расположение идентификатора пользователя SAML) выберите значение **NameIdentifier element of the subject statement** (Элемент NameIdentifier оператора Subject).</span><span class="sxs-lookup"><span data-stu-id="52eb9-196">Set **SAML User Id location** to **NameIdentifier element of the subject statement**.</span></span>
    
    <span data-ttu-id="52eb9-197">f.</span><span class="sxs-lookup"><span data-stu-id="52eb9-197">f.</span></span> <span data-ttu-id="52eb9-198">Введите значение **Keylight Service Provider** (Поставщик услуг Keylight), используя следующий формат: **https://&lt;название_компании&gt;.keylightgrc.com**.</span><span class="sxs-lookup"><span data-stu-id="52eb9-198">Provide the **Keylight Service Provider** using the following pattern: **https://&lt;CompanyName&gt;.keylightgrc.com**.</span></span>
    
    <span data-ttu-id="52eb9-199">g.</span><span class="sxs-lookup"><span data-stu-id="52eb9-199">g.</span></span> <span data-ttu-id="52eb9-200">Задайте для параметра **Auto-provision users** (Автоматическая подготовка пользователей) значение **Active** (Активно).</span><span class="sxs-lookup"><span data-stu-id="52eb9-200">Set **Auto-provision users** to **Active**.</span></span>

    <span data-ttu-id="52eb9-201">h.</span><span class="sxs-lookup"><span data-stu-id="52eb9-201">h.</span></span> <span data-ttu-id="52eb9-202">Задайте для параметра **Auto-provision account type** (Тип учетной записи для автоматической подготовки) значение **Full User** (С полным доступом).</span><span class="sxs-lookup"><span data-stu-id="52eb9-202">Set **Auto-provision account type** to **Full User**.</span></span>

    <span data-ttu-id="52eb9-203">i.</span><span class="sxs-lookup"><span data-stu-id="52eb9-203">i.</span></span> <span data-ttu-id="52eb9-204">Задайте для параметра **Auto-provision security role** (Роль безопасности для автоматической подготовки) значение **Standard User with SAML** (Права обычного пользователя с SAML).</span><span class="sxs-lookup"><span data-stu-id="52eb9-204">Set **Auto-provision security role**, select **Standard User with SAML**.</span></span>
    
    <span data-ttu-id="52eb9-205">j.</span><span class="sxs-lookup"><span data-stu-id="52eb9-205">j.</span></span> <span data-ttu-id="52eb9-206">Задайте для параметра **Auto-provision security config** (Конфигурация безопасности для автоматической подготовки) значение **Standard User Configuration** (Конфигурация обычного пользователя).</span><span class="sxs-lookup"><span data-stu-id="52eb9-206">Set **Auto-provision security config**, select **Standard User Configuration**.</span></span>
     
    <span data-ttu-id="52eb9-207">k.</span><span class="sxs-lookup"><span data-stu-id="52eb9-207">k.</span></span> <span data-ttu-id="52eb9-208">В текстовое поле **Email Attribute** (Атрибут электронной почты) введите `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span><span class="sxs-lookup"><span data-stu-id="52eb9-208">In the **Email attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`.</span></span>
    
    <span data-ttu-id="52eb9-209">l.</span><span class="sxs-lookup"><span data-stu-id="52eb9-209">l.</span></span> <span data-ttu-id="52eb9-210">В текстовое поле **First name attribute** (Атрибут имени) введите значение `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span><span class="sxs-lookup"><span data-stu-id="52eb9-210">In the **First name attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname`.</span></span>
    
    <span data-ttu-id="52eb9-211">m.</span><span class="sxs-lookup"><span data-stu-id="52eb9-211">m.</span></span> <span data-ttu-id="52eb9-212">В текстовое поле **Last name attribute** (Атрибут фамилии) введите значение `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span><span class="sxs-lookup"><span data-stu-id="52eb9-212">In the **Last name attribute** textbox, type `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname`.</span></span>
    
    <span data-ttu-id="52eb9-213">n.</span><span class="sxs-lookup"><span data-stu-id="52eb9-213">n.</span></span> <span data-ttu-id="52eb9-214">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="52eb9-214">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="52eb9-215">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="52eb9-215">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="52eb9-216">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="52eb9-216">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="52eb9-217">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="52eb9-217">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="52eb9-218">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="52eb9-218">Creating an Azure AD test user</span></span>
<span data-ttu-id="52eb9-219">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="52eb9-219">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="52eb9-221">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="52eb9-221">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="52eb9-222">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="52eb9-222">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-keylight-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="52eb9-224">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="52eb9-224">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-keylight-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="52eb9-226">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="52eb9-226">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-keylight-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="52eb9-228">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="52eb9-228">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-keylight-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="52eb9-230">а.</span><span class="sxs-lookup"><span data-stu-id="52eb9-230">a.</span></span> <span data-ttu-id="52eb9-231">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="52eb9-231">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="52eb9-232">b.</span><span class="sxs-lookup"><span data-stu-id="52eb9-232">b.</span></span> <span data-ttu-id="52eb9-233">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="52eb9-233">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="52eb9-234">c.</span><span class="sxs-lookup"><span data-stu-id="52eb9-234">c.</span></span> <span data-ttu-id="52eb9-235">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="52eb9-235">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="52eb9-236">d.</span><span class="sxs-lookup"><span data-stu-id="52eb9-236">d.</span></span> <span data-ttu-id="52eb9-237">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="52eb9-237">Click **Create**.</span></span>
 
### <a name="creating-a-lockpath-keylight-test-user"></a><span data-ttu-id="52eb9-238">Создание тестового пользователя LockPath Keylight</span><span class="sxs-lookup"><span data-stu-id="52eb9-238">Creating a LockPath Keylight test user</span></span>

<span data-ttu-id="52eb9-239">В этом разделе описано, как создать пользователя Britta Simon в приложении LockPath Keylight.</span><span class="sxs-lookup"><span data-stu-id="52eb9-239">In this section, you create a user called Britta Simon in LockPath Keylight.</span></span> <span data-ttu-id="52eb9-240">LockPath Keylight поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="52eb9-240">LockPath Keylight supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="52eb9-241">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="52eb9-241">There is no action item for you in this section.</span></span> <span data-ttu-id="52eb9-242">Если пользователь не существует, то он создается при доступе к LockPath Keylight.</span><span class="sxs-lookup"><span data-stu-id="52eb9-242">A new user is created when accessing LockPath Keylight if the user doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="52eb9-243">Если вам нужно вручную создать пользователя, необходимо обратиться к [группе поддержки клиентов LockPath Keylight](https://www.lockpath.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="52eb9-243">If you need to create a user manually, you need to contact the [LockPath Keylight Client support team](https://www.lockpath.com/contact/).</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="52eb9-244">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="52eb9-244">Assigning the Azure AD test user</span></span>

<span data-ttu-id="52eb9-245">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к LockPath Keylight.</span><span class="sxs-lookup"><span data-stu-id="52eb9-245">In this section, you enable Britta Simon to use Azure single sign-on by granting access to LockPath Keylight.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="52eb9-247">**Чтобы назначить пользователя Britta Simon в LockPath Keylight, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="52eb9-247">**To assign Britta Simon to LockPath Keylight, perform the following steps:**</span></span>

1. <span data-ttu-id="52eb9-248">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="52eb9-248">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="52eb9-250">Из списка приложений выберите **LockPath Keylight**.</span><span class="sxs-lookup"><span data-stu-id="52eb9-250">In the applications list, select **LockPath Keylight**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-keylight-tutorial/tutorial_keylight_app.png) 

3. <span data-ttu-id="52eb9-252">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="52eb9-252">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="52eb9-254">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="52eb9-254">Click **Add** button.</span></span> <span data-ttu-id="52eb9-255">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="52eb9-255">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="52eb9-257">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="52eb9-257">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="52eb9-258">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="52eb9-258">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="52eb9-259">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="52eb9-259">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="52eb9-260">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="52eb9-260">Testing single sign-on</span></span>

<span data-ttu-id="52eb9-261">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="52eb9-261">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="52eb9-262">Щелкнув элемент "LockPath Keylight" на панели доступа, вы автоматически войдете в приложение LockPath Keylight.</span><span class="sxs-lookup"><span data-stu-id="52eb9-262">When you click the LockPath Keylight tile in the Access Panel, you should get automatically signed-on to your LockPath Keylight application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="52eb9-263">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="52eb9-263">Additional resources</span></span>

* [<span data-ttu-id="52eb9-264">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="52eb9-264">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="52eb9-265">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="52eb9-265">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-keylight-tutorial/tutorial_general_203.png

