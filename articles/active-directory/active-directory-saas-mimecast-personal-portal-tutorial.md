---
title: "Руководство по интеграции Azure Active Directory с Mimecast Personal Portal | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в Mimecast Personal Portal."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 345b22be-d87e-45a4-b4c0-70a67eaf9bfd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: bf46da35a55608d7e4656c9dd3ad9d5f2253e225
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mimecast-personal-portal"></a><span data-ttu-id="13843-103">Руководство по интеграции Azure Active Directory с Mimecast Personal Portal</span><span class="sxs-lookup"><span data-stu-id="13843-103">Tutorial: Azure Active Directory integration with Mimecast Personal Portal</span></span>

<span data-ttu-id="13843-104">В этом руководстве описано, как интегрировать Mimecast Personal Portal с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="13843-104">In this tutorial, you learn how to integrate Mimecast Personal Portal with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="13843-105">Интеграция Azure AD с Mimecast Personal Portal обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="13843-105">Integrating Mimecast Personal Portal with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="13843-106">С помощью Azure AD вы можете контролировать доступ к Mimecast Personal Portal.</span><span class="sxs-lookup"><span data-stu-id="13843-106">You can control in Azure AD who has access to Mimecast Personal Portal</span></span>
- <span data-ttu-id="13843-107">Вы можете включить автоматический вход пользователей в Mimecast Personal Portal (единый вход) с использованием учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="13843-107">You can enable your users to automatically get signed-on to Mimecast Personal Portal (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="13843-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="13843-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="13843-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="13843-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="13843-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="13843-110">Prerequisites</span></span>

<span data-ttu-id="13843-111">Чтобы настроить интеграцию Azure AD с Mimecast Personal Portal, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="13843-111">To configure Azure AD integration with Mimecast Personal Portal, you need the following items:</span></span>

- <span data-ttu-id="13843-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="13843-112">An Azure AD subscription</span></span>
- <span data-ttu-id="13843-113">Подписка на личный портал Mimecast с поддержкой единого входа</span><span class="sxs-lookup"><span data-stu-id="13843-113">A Mimecast Personal Portal single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="13843-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="13843-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="13843-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="13843-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="13843-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="13843-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="13843-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="13843-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="13843-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="13843-118">Scenario description</span></span>
<span data-ttu-id="13843-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="13843-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="13843-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="13843-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="13843-121">Добавление Mimecast Personal Portal из коллекции.</span><span class="sxs-lookup"><span data-stu-id="13843-121">Adding Mimecast Personal Portal from the gallery</span></span>
2. <span data-ttu-id="13843-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="13843-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mimecast-personal-portal-from-the-gallery"></a><span data-ttu-id="13843-123">Добавление Mimecast Personal Portal из коллекции</span><span class="sxs-lookup"><span data-stu-id="13843-123">Adding Mimecast Personal Portal from the gallery</span></span>
<span data-ttu-id="13843-124">Чтобы настроить интеграцию Mimecast Personal Portal с Azure AD, необходимо добавить Mimecast Personal Portal из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="13843-124">To configure the integration of Mimecast Personal Portal into Azure AD, you need to add Mimecast Personal Portal from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="13843-125">**Чтобы добавить Mimecast Personal Portal из коллекции, сделайте следующее.**</span><span class="sxs-lookup"><span data-stu-id="13843-125">**To add Mimecast Personal Portal from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="13843-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="13843-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="13843-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="13843-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="13843-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="13843-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="13843-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="13843-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="13843-133">В поле поиска введите **Mimecast Personal Portal**.</span><span class="sxs-lookup"><span data-stu-id="13843-133">In the search box, type **Mimecast Personal Portal**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_search.png)

5. <span data-ttu-id="13843-135">На панели результатов выберите **Mimecast Personal Portal** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="13843-135">In the results panel, select **Mimecast Personal Portal**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="13843-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="13843-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="13843-138">В этом разделе описана настройка и проверка единого входа Azure AD в Mimecast Personal Portal с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="13843-138">In this section, you configure and test Azure AD single sign-on with Mimecast Personal Portal based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="13843-139">Чтобы единый вход работал, Azure AD необходима информация о том, какой пользователь в Mimecast Personal Portal соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="13843-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Mimecast Personal Portal is to a user in Azure AD.</span></span> <span data-ttu-id="13843-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Mimecast Personal Portal.</span><span class="sxs-lookup"><span data-stu-id="13843-140">In other words, a link relationship between an Azure AD user and the related user in Mimecast Personal Portal needs to be established.</span></span>

<span data-ttu-id="13843-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Mimecast Personal Portal.</span><span class="sxs-lookup"><span data-stu-id="13843-141">In Mimecast Personal Portal, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="13843-142">Чтобы настроить и проверить единый вход Azure AD в Mimecast Personal Portal, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="13843-142">To configure and test Azure AD single sign-on with Mimecast Personal Portal, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="13843-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="13843-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="13843-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="13843-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="13843-145">**[Создание тестового пользователя Mimecast Personal Portal](#creating-a-mimecast-personal-portal-test-user)** требуется для того, чтобы в Mimecast Personal Portal существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="13843-145">**[Creating a Mimecast Personal Portal test user](#creating-a-mimecast-personal-portal-test-user)** - to have a counterpart of Britta Simon in Mimecast Personal Portal that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="13843-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="13843-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="13843-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="13843-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="13843-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="13843-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="13843-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Mimecast Personal Portal.</span><span class="sxs-lookup"><span data-stu-id="13843-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Mimecast Personal Portal application.</span></span>

<span data-ttu-id="13843-150">**Чтобы настроить единый вход Azure AD в Mimecast Personal Portal, сделайте следующее.**</span><span class="sxs-lookup"><span data-stu-id="13843-150">**To configure Azure AD single sign-on with Mimecast Personal Portal, perform the following steps:**</span></span>

1. <span data-ttu-id="13843-151">На портале Azure на странице интеграции с приложением **Mimecast Personal Portal** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="13843-151">In the Azure portal, on the **Mimecast Personal Portal** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="13843-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="13843-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_samlbase.png)

3. <span data-ttu-id="13843-155">В разделе **Домены и URL-адреса приложения Mimecast Personal Portal** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="13843-155">On the **Mimecast Personal Portal Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_url.png)

    <span data-ttu-id="13843-157">а.</span><span class="sxs-lookup"><span data-stu-id="13843-157">a.</span></span> <span data-ttu-id="13843-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="13843-158">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span> 
    | |     
    | ----------------------------------------|
    | `https://webmail-uk.mimecast.com`|
    | `https://webmail-us.mimecast.com`|
    | |
   
    <span data-ttu-id="13843-159">b.</span><span class="sxs-lookup"><span data-stu-id="13843-159">b.</span></span> <span data-ttu-id="13843-160">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="13843-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span>

    | |     
    | --- |
    | `https://webmail-us.mimecast.com/sso/<companyname>`|
    | `https://webmail-uk.mimecast.com/sso/<companyname>`|    
    | `https://webmail-za.mimecast.com/sso/<companyname>`|
    | `https://webmail.mimecast-offshore.com/sso/<companyname>`|
    ||                                                 
    
    > [!NOTE] 
    > <span data-ttu-id="13843-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="13843-161">These values are not real.</span></span> <span data-ttu-id="13843-162">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="13843-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="13843-163">Чтобы получить эти значения, обратитесь к [группе поддержки клиентов Mimecast Personal Portal](https://www.mimecast.com/customer-success/technical-support/).</span><span class="sxs-lookup"><span data-stu-id="13843-163">Contact [Mimecast Personal Portal Client support team](https://www.mimecast.com/customer-success/technical-support/) to get these values.</span></span> 
 


4. <span data-ttu-id="13843-164">В разделе **Сертификат подписи SAML** щелкните **Сертификат (Base64)**, а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="13843-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_certificate.png) 

5. <span data-ttu-id="13843-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="13843-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="13843-168">В разделе **Конфигурация Mimecast Personal Portal** щелкните **Настроить Mimecast Personal Portal**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="13843-168">On the **Mimecast Personal Portal Configuration** section, click **Configure Mimecast Personal Portal** to open **Configure sign-on** window.</span></span> <span data-ttu-id="13843-169">Скопируйте **URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML**  из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="13843-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_configure.png) 

7. <span data-ttu-id="13843-171">В другом окне веб-браузера войдите в личный портал Mimecast в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="13843-171">In a different web browser window, log into your Mimecast Personal Portal as an administrator.</span></span>

8. <span data-ttu-id="13843-172">Выберите **Services \> Application** ("Службы" > "Приложение").</span><span class="sxs-lookup"><span data-stu-id="13843-172">Go to **Services \> Applications**.</span></span>
   
    <span data-ttu-id="13843-173">![Приложения](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794998.png "Приложения")</span><span class="sxs-lookup"><span data-stu-id="13843-173">![Applications](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794998.png "Applications")</span></span>

9. <span data-ttu-id="13843-174">Щелкните **Профили проверки подлинности**.</span><span class="sxs-lookup"><span data-stu-id="13843-174">Click **Authentication Profiles**.</span></span>
   
    <span data-ttu-id="13843-175">![Authentication Profiles](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794999.png "Authentication Profiles") (Профили аутентификации)</span><span class="sxs-lookup"><span data-stu-id="13843-175">![Authentication Profiles](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic794999.png "Authentication Profiles")</span></span>

10. <span data-ttu-id="13843-176">Щелкните **Новый профиль проверки подлинности**.</span><span class="sxs-lookup"><span data-stu-id="13843-176">Click **New Authentication Profile**.</span></span>
   
    <span data-ttu-id="13843-177">![Создание профиля аутентификации](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795000.png "New Authentication Profile")</span><span class="sxs-lookup"><span data-stu-id="13843-177">![New Authentication Profile](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795000.png "New Authentication Profile")</span></span>

11. <span data-ttu-id="13843-178">В разделе **Профиль проверки подлинности** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="13843-178">In the **Authentication Profile** section, perform the following steps:</span></span>
   
    <span data-ttu-id="13843-179">![Authentication Profile](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795001.png "Authentication Profile") (Профиль аутентификации)</span><span class="sxs-lookup"><span data-stu-id="13843-179">![Authentication Profile](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795001.png "Authentication Profile")</span></span>
   
    <span data-ttu-id="13843-180">а.</span><span class="sxs-lookup"><span data-stu-id="13843-180">a.</span></span> <span data-ttu-id="13843-181">В текстовом поле **Описание** введите имя конфигурации.</span><span class="sxs-lookup"><span data-stu-id="13843-181">In the **Description** textbox, type a name for your configuration.</span></span>
   
    <span data-ttu-id="13843-182">b.</span><span class="sxs-lookup"><span data-stu-id="13843-182">b.</span></span> <span data-ttu-id="13843-183">Выберите **Обязательное использование проверки подлинности SAML для личного портала Mimecast**.</span><span class="sxs-lookup"><span data-stu-id="13843-183">Select **Enforce SAML Authentication for Mimecast Personal Portal**.</span></span>
   
    <span data-ttu-id="13843-184">c.</span><span class="sxs-lookup"><span data-stu-id="13843-184">c.</span></span> <span data-ttu-id="13843-185">В поле **Provider** (Поставщик) выберите **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="13843-185">As **Provider**, select **Azure Active Directory**.</span></span>
   
    <span data-ttu-id="13843-186">г)</span><span class="sxs-lookup"><span data-stu-id="13843-186">d.</span></span> <span data-ttu-id="13843-187">В текстовое поле **Issuer URL** (URL-адрес издателя) вставьте значение **SAML Entity ID** (Идентификатор сущности SAML), скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="13843-187">In **Issuer URL** textbox, paste the value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="13843-188">д.</span><span class="sxs-lookup"><span data-stu-id="13843-188">e.</span></span> <span data-ttu-id="13843-189">В текстовое поле **Login URL** (URL-адрес входа) вставьте значение **SAML Single Sign-On Service URL** (URL-адрес службы единого входа SAML), скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="13843-189">In **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="13843-190">f.</span><span class="sxs-lookup"><span data-stu-id="13843-190">f.</span></span> <span data-ttu-id="13843-191">В текстовое поле **Logout URL** (URL-адрес выхода) вставьте значение **URL-адрес выхода**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="13843-191">In **Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="13843-192">g.</span><span class="sxs-lookup"><span data-stu-id="13843-192">g.</span></span> <span data-ttu-id="13843-193">Откройте в Блокноте сертификат в кодировке **Base64**, скачанный с портала Azure, скопируйте его в буфер обмена и вставьте в текстовое поле **Identity Provider Certificate (Metadata)** (Сертификат поставщика удостоверений (метаданные)).</span><span class="sxs-lookup"><span data-stu-id="13843-193">Open your **base-64** encoded certificate in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **Identity Provider Certificate (Metadata)** textbox.</span></span>

    <span data-ttu-id="13843-194">h.</span><span class="sxs-lookup"><span data-stu-id="13843-194">h.</span></span> <span data-ttu-id="13843-195">Установите флажок **Разрешить единый вход**.</span><span class="sxs-lookup"><span data-stu-id="13843-195">Select **Allow Single Sign On**.</span></span>
   
    <span data-ttu-id="13843-196">i.</span><span class="sxs-lookup"><span data-stu-id="13843-196">i.</span></span> <span data-ttu-id="13843-197">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="13843-197">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="13843-198">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="13843-198">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="13843-199">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="13843-199">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="13843-200">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="13843-200">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="13843-201">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="13843-201">Creating an Azure AD test user</span></span>
<span data-ttu-id="13843-202">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="13843-202">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="13843-204">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="13843-204">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="13843-205">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="13843-205">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="13843-207">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="13843-207">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="13843-209">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="13843-209">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="13843-211">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="13843-211">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mimecast-personal-portal-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="13843-213">а.</span><span class="sxs-lookup"><span data-stu-id="13843-213">a.</span></span> <span data-ttu-id="13843-214">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="13843-214">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="13843-215">b.</span><span class="sxs-lookup"><span data-stu-id="13843-215">b.</span></span> <span data-ttu-id="13843-216">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="13843-216">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="13843-217">c.</span><span class="sxs-lookup"><span data-stu-id="13843-217">c.</span></span> <span data-ttu-id="13843-218">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="13843-218">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="13843-219">d.</span><span class="sxs-lookup"><span data-stu-id="13843-219">d.</span></span> <span data-ttu-id="13843-220">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="13843-220">Click **Create**.</span></span>
 
### <a name="creating-a-mimecast-personal-portal-test-user"></a><span data-ttu-id="13843-221">Создание тестового пользователя Mimecast Personal Portal</span><span class="sxs-lookup"><span data-stu-id="13843-221">Creating a Mimecast Personal Portal test user</span></span>

<span data-ttu-id="13843-222">Чтобы разрешить пользователям Azure AD вход в личный портал Mimecast, они должны быть подготовлены для личного портала Mimecast.</span><span class="sxs-lookup"><span data-stu-id="13843-222">In order to enable Azure AD users to log into Mimecast Personal Portal, they must be provisioned into Mimecast Personal Portal.</span></span> <span data-ttu-id="13843-223">В случае с личным порталом Mimecast подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="13843-223">In the case of Mimecast Personal Portal, provisioning is a manual task.</span></span>

<span data-ttu-id="13843-224">Перед созданием пользователей необходимо зарегистрировать домен.</span><span class="sxs-lookup"><span data-stu-id="13843-224">You need to register a domain before you can create users.</span></span>

<span data-ttu-id="13843-225">**Чтобы настроить подготовку учетных записей пользователей, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="13843-225">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="13843-226">Войдите на **Mimecast Personal Portal** в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="13843-226">Sign on to your **Mimecast Personal Portal** as administrator.</span></span>

2. <span data-ttu-id="13843-227">Выберите **Directories \> Internal** (Каталоги > Внутренние).</span><span class="sxs-lookup"><span data-stu-id="13843-227">Go to **Directories \> Internal**.</span></span>
   
    <span data-ttu-id="13843-228">![Directories](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795003.png "Directories") (Каталоги)</span><span class="sxs-lookup"><span data-stu-id="13843-228">![Directories](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795003.png "Directories")</span></span>

3. <span data-ttu-id="13843-229">Щелкните **Зарегистрировать новый домен**.</span><span class="sxs-lookup"><span data-stu-id="13843-229">Click **Register New Domain**.</span></span>
   
    <span data-ttu-id="13843-230">![Register New Domain](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795004.png "Register New Domain") (Зарегистрировать новый домен)</span><span class="sxs-lookup"><span data-stu-id="13843-230">![Register New Domain](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795004.png "Register New Domain")</span></span>

4. <span data-ttu-id="13843-231">После создания нового домена щелкните **Новый адрес**.</span><span class="sxs-lookup"><span data-stu-id="13843-231">After your new domain has been created, click **New Address**.</span></span>
   
    <span data-ttu-id="13843-232">![New Address](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795005.png "New Address") (Новый адрес)</span><span class="sxs-lookup"><span data-stu-id="13843-232">![New Address](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795005.png "New Address")</span></span>

5. <span data-ttu-id="13843-233">В диалоговом окне "New Address" (Новый адрес) введите соответствующие данные действующей учетной записи Azure AD, которую необходимо подготовить.</span><span class="sxs-lookup"><span data-stu-id="13843-233">In the new address dialog, perform the following steps of a valid Azure AD account you want to provision:</span></span>
   
    <span data-ttu-id="13843-234">![Сохранить](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795006.png "Сохранить")</span><span class="sxs-lookup"><span data-stu-id="13843-234">![Save](./media/active-directory-saas-mimecast-personal-portal-tutorial/ic795006.png "Save")</span></span>
   
    <span data-ttu-id="13843-235">а.</span><span class="sxs-lookup"><span data-stu-id="13843-235">a.</span></span> <span data-ttu-id="13843-236">В текстовое поле **Email Address** (Адрес электронной почты) введите **адрес электронной почты** пользователя, например **BrittaSimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="13843-236">In the **Email Address** textbox, type **Email Address** of the user as **BrittaSimon@contoso.com**.</span></span>
    
    <span data-ttu-id="13843-237">b.</span><span class="sxs-lookup"><span data-stu-id="13843-237">b.</span></span> <span data-ttu-id="13843-238">В текстовое поле **Global Name** (Глобальное имя) введите **имя пользователя** **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="13843-238">In the **Global Name** textbox, type the **username** as **BrittaSimon**.</span></span>

    <span data-ttu-id="13843-239">c.</span><span class="sxs-lookup"><span data-stu-id="13843-239">c.</span></span> <span data-ttu-id="13843-240">В текстовые поля **Password** (Пароль) и **Confirm Password** (Подтверждение пароля) введите **пароль** пользователя.</span><span class="sxs-lookup"><span data-stu-id="13843-240">In the **Password**, and **Confirm Password** textboxes, type the **Password** of the user.</span></span>
   
    <span data-ttu-id="13843-241">b.</span><span class="sxs-lookup"><span data-stu-id="13843-241">b.</span></span> <span data-ttu-id="13843-242">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="13843-242">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="13843-243">Вы можете использовать любые другие инструменты создания учетных записей пользователя Mimecast Personal Portal или API, предоставляемые Mimecast Personal Portal для подготовки учетных записей пользователя Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="13843-243">You can use any other Mimecast Personal Portal user account creation tools or APIs provided by Mimecast Personal Portal to provision Azure AD user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="13843-244">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="13843-244">Assigning the Azure AD test user</span></span>

<span data-ttu-id="13843-245">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к Mimecast Personal Portal.</span><span class="sxs-lookup"><span data-stu-id="13843-245">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Mimecast Personal Portal.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="13843-247">**Чтобы назначить пользователя Britta Simon в Mimecast Personal Portal, сделайте следующее.**</span><span class="sxs-lookup"><span data-stu-id="13843-247">**To assign Britta Simon to Mimecast Personal Portal, perform the following steps:**</span></span>

1. <span data-ttu-id="13843-248">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="13843-248">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="13843-250">Из списка приложений выберите **Mimecast Personal Portal**.</span><span class="sxs-lookup"><span data-stu-id="13843-250">In the applications list, select **Mimecast Personal Portal**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_mimecastpersonalportal_app.png) 

3. <span data-ttu-id="13843-252">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="13843-252">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="13843-254">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="13843-254">Click **Add** button.</span></span> <span data-ttu-id="13843-255">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="13843-255">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="13843-257">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="13843-257">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="13843-258">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="13843-258">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="13843-259">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="13843-259">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="13843-260">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="13843-260">Testing single sign-on</span></span>
<span data-ttu-id="13843-261">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="13843-261">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="13843-262">Щелкнув элемент "Mimecast Personal Portal" на панели доступа, вы автоматически войдете в приложение Mimecast Personal Portal.</span><span class="sxs-lookup"><span data-stu-id="13843-262">When you click the Mimecast Personal Portal tile in the Access Panel, you should get automatically signed-on to your Mimecast Personal Portal application.</span></span> <span data-ttu-id="13843-263">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="13843-263">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="13843-264">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="13843-264">Additional resources</span></span>

* [<span data-ttu-id="13843-265">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="13843-265">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="13843-266">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="13843-266">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mimecast-personal-portal-tutorial/tutorial_general_203.png

