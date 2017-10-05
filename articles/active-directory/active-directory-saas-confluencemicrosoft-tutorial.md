---
title: "Руководство по интеграции Azure Active Directory с Confluence SAML SSO by Microsoft | Документы Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в Confluence SAML SSO by Microsoft."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 1ad1cf90-52bc-4b71-ab2b-9a5a1280fb2d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 56de86df9c915fa7c41e3bf0a545cc528cdcf959
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-confluence-saml-sso-by-microsoft"></a><span data-ttu-id="d59f7-103">Руководство по интеграции Azure Active Directory с Confluence SAML SSO by Microsoft</span><span class="sxs-lookup"><span data-stu-id="d59f7-103">Tutorial: Azure Active Directory integration with Confluence SAML SSO by Microsoft</span></span>

<span data-ttu-id="d59f7-104">В этом руководстве описано, как интегрировать Confluence SAML SSO by Microsoft с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d59f7-104">In this tutorial, you learn how to integrate Confluence SAML SSO by Microsoft with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d59f7-105">Интеграция Azure AD с Confluence SAML SSO by Microsoft обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="d59f7-105">Integrating Confluence SAML SSO by Microsoft with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d59f7-106">С помощью Azure AD вы можете контролировать доступ к Confluence SAML SSO by Microsoft.</span><span class="sxs-lookup"><span data-stu-id="d59f7-106">You can control in Azure AD who has access to Confluence SAML SSO by Microsoft</span></span>
- <span data-ttu-id="d59f7-107">Можно включить автоматический вход пользователей в Confluence SAML SSO by Microsoft, то есть единый вход, с учетными записями Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d59f7-107">You can enable your users to automatically get signed-on to Confluence SAML SSO by Microsoft (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="d59f7-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="d59f7-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="d59f7-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d59f7-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d59f7-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d59f7-110">Prerequisites</span></span>

<span data-ttu-id="d59f7-111">Чтобы настроить интеграцию Azure AD с Confluence SAML SSO by Microsoft, вам потребуется следующее:</span><span class="sxs-lookup"><span data-stu-id="d59f7-111">To configure Azure AD integration with Confluence SAML SSO by Microsoft, you need the following items:</span></span>

- <span data-ttu-id="d59f7-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="d59f7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d59f7-113">серверное приложение Confluence, установленное на 64-разрядной версии сервера Windows (в локальной среде или облачной инфраструктуре IaaS);</span><span class="sxs-lookup"><span data-stu-id="d59f7-113">Confluence server application installed on a Windows 64-bit server (on premise or on the cloud IaaS infrastructure)</span></span>
- <span data-ttu-id="d59f7-114">поддержка HTTPS на сервере Confluence;</span><span class="sxs-lookup"><span data-stu-id="d59f7-114">Confluence server is HTTPS enabled</span></span>
- <span data-ttu-id="d59f7-115">поддерживаемые версии подключаемого модуля Confluence указаны в разделе ниже;</span><span class="sxs-lookup"><span data-stu-id="d59f7-115">Note the supported versions for Confluence Plugin are mentioned in below section.</span></span>
- <span data-ttu-id="d59f7-116">сервер Confluence должен быть доступен через Интернет, в частности, на странице входа Azure AD для аутентификации, и должен иметь возможность получать маркер из Azure AD;</span><span class="sxs-lookup"><span data-stu-id="d59f7-116">Confluence server is reachable on internet particularly to Azure AD Login page for authentication and should able to receive the token from Azure AD</span></span>
- <span data-ttu-id="d59f7-117">в Confluence должны быть настроены учетные данные администратора;</span><span class="sxs-lookup"><span data-stu-id="d59f7-117">Admin credentials are set up in Confluence</span></span>
- <span data-ttu-id="d59f7-118">в Confluence должна быть отключена поддержка WebSudo;</span><span class="sxs-lookup"><span data-stu-id="d59f7-118">WebSudo is disabled in Confluence</span></span>
- <span data-ttu-id="d59f7-119">в серверном приложении Confluence должен быть создан тестовый пользователь.</span><span class="sxs-lookup"><span data-stu-id="d59f7-119">Test user created in the Confluence server application</span></span>

> [!NOTE]
> <span data-ttu-id="d59f7-120">Мы не рекомендуем использовать рабочую среду Confluence для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="d59f7-120">To test the steps in this tutorial, we do not recommend using a production environment of Confluence.</span></span> <span data-ttu-id="d59f7-121">Сначала протестируйте интеграцию в среде разработки или промежуточной среде приложения, а затем используйте ее в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="d59f7-121">Test the integration first in development or staging environment of the application and then use the production environment.</span></span>

<span data-ttu-id="d59f7-122">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="d59f7-122">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d59f7-123">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="d59f7-123">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d59f7-124">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d59f7-124">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="supported-versions-of-confluence"></a><span data-ttu-id="d59f7-125">Поддерживаемые версии Confluence</span><span class="sxs-lookup"><span data-stu-id="d59f7-125">Supported versions of Confluence</span></span> 

<span data-ttu-id="d59f7-126">Сейчас поддерживаются следующие версии Confluence:</span><span class="sxs-lookup"><span data-stu-id="d59f7-126">As of now, following versions of Confluence are supported:</span></span>

- <span data-ttu-id="d59f7-127">Confluence: версии c 5.0 по 5.10</span><span class="sxs-lookup"><span data-stu-id="d59f7-127">Confluence: 5.0 to 5.10</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d59f7-128">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="d59f7-128">Scenario description</span></span>
<span data-ttu-id="d59f7-129">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="d59f7-129">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d59f7-130">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="d59f7-130">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d59f7-131">Добавление Confluence SAML SSO by Microsoft из коллекции</span><span class="sxs-lookup"><span data-stu-id="d59f7-131">Adding Confluence SAML SSO by Microsoft from the gallery</span></span>
2. <span data-ttu-id="d59f7-132">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="d59f7-132">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-confluence-saml-sso-by-microsoft-from-the-gallery"></a><span data-ttu-id="d59f7-133">Добавление Confluence SAML SSO by Microsoft из коллекции</span><span class="sxs-lookup"><span data-stu-id="d59f7-133">Adding Confluence SAML SSO by Microsoft from the gallery</span></span>
<span data-ttu-id="d59f7-134">Чтобы настроить интеграцию Confluence SAML SSO by Microsoft с Azure AD, необходимо добавить Confluence SAML SSO by Microsoft из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="d59f7-134">To configure the integration of Confluence SAML SSO by Microsoft into Azure AD, you need to add Confluence SAML SSO by Microsoft from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d59f7-135">**Чтобы добавить Confluence SAML SSO by Microsoft из коллекции, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="d59f7-135">**To add Confluence SAML SSO by Microsoft from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d59f7-136">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d59f7-136">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="d59f7-138">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="d59f7-138">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d59f7-139">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="d59f7-139">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="d59f7-141">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="d59f7-141">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="d59f7-143">В поле поиска введите **Confluence SAML SSO by Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="d59f7-143">In the search box, type **Confluence SAML SSO by Microsoft**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_search.png)

5. <span data-ttu-id="d59f7-145">На панели результатов выберите **Confluence SAML SSO by Microsoft** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="d59f7-145">In the results panel, select **Confluence SAML SSO by Microsoft**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="d59f7-147">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="d59f7-147">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="d59f7-148">В этом разделе описывается настройка и проверка единого входа Azure AD в Confluence SAML SSO by Microsoft с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d59f7-148">In this section, you configure and test Azure AD single sign-on with Confluence SAML SSO by Microsoft based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d59f7-149">Для работы единого входа Azure AD необходимо знать, какой пользователь в Confluence SAML SSO by Microsoft соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d59f7-149">For single sign-on to work, Azure AD needs to know what the counterpart user in Confluence SAML SSO by Microsoft is to a user in Azure AD.</span></span> <span data-ttu-id="d59f7-150">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Confluence SAML SSO by Microsoft.</span><span class="sxs-lookup"><span data-stu-id="d59f7-150">In other words, a link relationship between an Azure AD user and the related user in Confluence SAML SSO by Microsoft needs to be established.</span></span>

<span data-ttu-id="d59f7-151">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Confluence SAML SSO by Microsoft.</span><span class="sxs-lookup"><span data-stu-id="d59f7-151">In Confluence SAML SSO by Microsoft, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d59f7-152">Чтобы настроить и проверить единый вход Microsoft Azure AD в Confluence SAML SSO by Microsoft, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="d59f7-152">To configure and test Azure AD single sign-on with Confluence SAML SSO by Microsoft, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d59f7-153">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="d59f7-153">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d59f7-154">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d59f7-154">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d59f7-155">**[Создание тестового пользователя Confluence SAML SSO by Microsoft](#creating-a-confluence-saml-sso-by-microsoft-test-user)** требуется для того, чтобы в Confluence SAML SSO by Microsoft существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d59f7-155">**[Creating a Confluence SAML SSO by Microsoft test user](#creating-a-confluence-saml-sso-by-microsoft-test-user)** - to have a counterpart of Britta Simon in Confluence SAML SSO by Microsoft that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d59f7-156">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d59f7-156">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d59f7-157">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="d59f7-157">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="d59f7-158">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="d59f7-158">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="d59f7-159">В данном разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Confluence SAML SSO by Microsoft.</span><span class="sxs-lookup"><span data-stu-id="d59f7-159">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Confluence SAML SSO by Microsoft application.</span></span>

<span data-ttu-id="d59f7-160">**Чтобы настроить единый вход Azure AD в Confluence SAML SSO by Microsoft, сделайте следующее.**</span><span class="sxs-lookup"><span data-stu-id="d59f7-160">**To configure Azure AD single sign-on with Confluence SAML SSO by Microsoft, perform the following steps:**</span></span>

1. <span data-ttu-id="d59f7-161">На портале Azure на странице интеграции с приложением **Confluence SAML SSO by Microsoft** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="d59f7-161">In the Azure portal, on the **Confluence SAML SSO by Microsoft** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="d59f7-163">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="d59f7-163">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_samlbase.png)

3. <span data-ttu-id="d59f7-165">В разделе **Домены и URL-адреса приложения Confluence SAML SSO by Microsoft** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="d59f7-165">On the **Confluence SAML SSO by Microsoft Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_url.png)

    <span data-ttu-id="d59f7-167">а.</span><span class="sxs-lookup"><span data-stu-id="d59f7-167">a.</span></span> <span data-ttu-id="d59f7-168">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<domain:port>/plugins/servlet/saml/auth`</span><span class="sxs-lookup"><span data-stu-id="d59f7-168">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<domain:port>/plugins/servlet/saml/auth`</span></span>

    <span data-ttu-id="d59f7-169">b.</span><span class="sxs-lookup"><span data-stu-id="d59f7-169">b.</span></span> <span data-ttu-id="d59f7-170">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<domain:port>/`</span><span class="sxs-lookup"><span data-stu-id="d59f7-170">In the **Identifier** textbox, type a URL using the following pattern: `https://<domain:port>/`</span></span>

    <span data-ttu-id="d59f7-171">c.</span><span class="sxs-lookup"><span data-stu-id="d59f7-171">c.</span></span> <span data-ttu-id="d59f7-172">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате: `https://<domain:port>/plugins/servlet/saml/auth`.</span><span class="sxs-lookup"><span data-stu-id="d59f7-172">In the **Reply URL** textbox, type a URL using the following pattern: `https://<domain:port>/plugins/servlet/saml/auth`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d59f7-173">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="d59f7-173">These values are not real.</span></span> <span data-ttu-id="d59f7-174">Замените их фактическими значениями идентификатора, URL-адреса ответа и URL-адреса входа.</span><span class="sxs-lookup"><span data-stu-id="d59f7-174">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="d59f7-175">Если это именованный URL-адрес, то порт указывать необязательно.</span><span class="sxs-lookup"><span data-stu-id="d59f7-175">Port is optional in case it’s a named URL.</span></span> <span data-ttu-id="d59f7-176">Эти значения предоставляются во время настройки подключаемого модуля Confluence, которая описывается далее в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="d59f7-176">These values are received during the configuration of Confluence plugin, which is explained later in the tutorial.</span></span>
 

4. <span data-ttu-id="d59f7-177">Для создания URL-адреса **метаданных** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="d59f7-177">To generate the **Metadata** url, perform the following steps:</span></span>

    <span data-ttu-id="d59f7-178">а.</span><span class="sxs-lookup"><span data-stu-id="d59f7-178">a.</span></span> <span data-ttu-id="d59f7-179">Щелкните **Регистрация приложений**.</span><span class="sxs-lookup"><span data-stu-id="d59f7-179">Click **App registrations**.</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-Confluencemicrosoft-tutorial/appregistrations.png)
   
    <span data-ttu-id="d59f7-181">b.</span><span class="sxs-lookup"><span data-stu-id="d59f7-181">b.</span></span> <span data-ttu-id="d59f7-182">Щелкните **Конечные точки**, чтобы открыть диалоговое окно **Конечные точки**.</span><span class="sxs-lookup"><span data-stu-id="d59f7-182">Click **Endpoints** to open **Endpoints** dialog box.</span></span>  
    
    ![Настройка единого входа](./media/active-directory-saas-Confluencemicrosoft-tutorial/endpointicon.png)

    <span data-ttu-id="d59f7-184">c.</span><span class="sxs-lookup"><span data-stu-id="d59f7-184">c.</span></span> <span data-ttu-id="d59f7-185">Нажмите кнопку "Копировать", чтобы скопировать URL-адрес **документа метаданных федерации**, а затем вставьте его в блокнот.</span><span class="sxs-lookup"><span data-stu-id="d59f7-185">Click the copy button to copy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-Confluencemicrosoft-tutorial/endpoint.png)
     
    <span data-ttu-id="d59f7-187">г)</span><span class="sxs-lookup"><span data-stu-id="d59f7-187">d.</span></span> <span data-ttu-id="d59f7-188">Теперь перейдите к странице свойств **Confluence SAML SSO by Microsoft** и скопируйте **Идентификатор приложения** с помощью кнопки **Копировать**, а затем вставьте его в Блокнот.</span><span class="sxs-lookup"><span data-stu-id="d59f7-188">Now go to the property page of **Confluence SAML SSO by Microsoft** and copy the **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-Confluencemicrosoft-tutorial/appid.png)

    <span data-ttu-id="d59f7-190">д.</span><span class="sxs-lookup"><span data-stu-id="d59f7-190">e.</span></span> <span data-ttu-id="d59f7-191">Создайте **URL-адрес метаданных** в формате `<FEDERATION METADATA DOCUMENT url>?appid=<application id>` и скопируйте это значение в Блокнот, так как оно будет использовано позже для настройки подключаемого модуля.</span><span class="sxs-lookup"><span data-stu-id="d59f7-191">Generate the **Metadata URL** using the following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>` and copy this value in notepad as it is used later for the configuration of the plugin.</span></span>

5. <span data-ttu-id="d59f7-192">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="d59f7-192">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-Confluencemicrosoft-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d59f7-194">Обратитесь в [службу поддержки Майкрософт](mailto:waadpartners@microsoft.com), предоставив следующие данные подключаемого модуля Confluence.</span><span class="sxs-lookup"><span data-stu-id="d59f7-194">Contact [Microsoft](mailto:waadpartners@microsoft.com) with the following information for the Confluence plugin.</span></span>
    
    *   <span data-ttu-id="d59f7-195">Имя клиента:</span><span class="sxs-lookup"><span data-stu-id="d59f7-195">Customer Name:</span></span>
    *   <span data-ttu-id="d59f7-196">Основное доменное имя:</span><span class="sxs-lookup"><span data-stu-id="d59f7-196">Primary domain name:</span></span>
    *   <span data-ttu-id="d59f7-197">Azure AD Premium: да или нет (подключаемый модуль будет доступен для всех клиентов с номерами SKU уровня "Бесплатный", "Базовый" и "Премиум")</span><span class="sxs-lookup"><span data-stu-id="d59f7-197">Azure AD Premium: Yes/No (Plugin will be available to all     the customer Free, Basic, and Premium SKU)</span></span>
    *   <span data-ttu-id="d59f7-198">Число пользователей, которые будут использовать данную интеграцию:</span><span class="sxs-lookup"><span data-stu-id="d59f7-198">Number of users who will be using this integration:</span></span>
    *   <span data-ttu-id="d59f7-199">Версия Confluence:</span><span class="sxs-lookup"><span data-stu-id="d59f7-199">Confluence Version:</span></span>
    *   <span data-ttu-id="d59f7-200">Комментарии.</span><span class="sxs-lookup"><span data-stu-id="d59f7-200">Comments:</span></span>

7. <span data-ttu-id="d59f7-201">В другом окне браузера войдите в свой экземпляр Confluence в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="d59f7-201">In a different web browser window, log in to your Confluence instance as an administrator.</span></span>

8. <span data-ttu-id="d59f7-202">Наведите указатель мыши на шестеренку и щелкните **Add-ons** (Надстройки).</span><span class="sxs-lookup"><span data-stu-id="d59f7-202">Hover on cog and click the **Add-ons**.</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-Confluencemicrosoft-tutorial/addon1.png)

9. <span data-ttu-id="d59f7-204">На вкладке "Надстройки" щелкните **Управление надстройками**.</span><span class="sxs-lookup"><span data-stu-id="d59f7-204">Under Add-ons tab section, click **Manage add-ons**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-Confluencemicrosoft-tutorial/addon72.png)

10. <span data-ttu-id="d59f7-206">Вручную отправьте подключаемый модуль, предоставленный корпорацией Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="d59f7-206">Manually upload the plugin provided by Microsoft.</span></span> <span data-ttu-id="d59f7-207">После установки подключаемый модуль появится в разделе **Управление надстройками**, подраздел **Установленные пользователем**.</span><span class="sxs-lookup"><span data-stu-id="d59f7-207">Once the plugin is installed, it appears in **User Installed** add-ons section of **Manage Add-on** section.</span></span>

11. <span data-ttu-id="d59f7-208">Щелкните **Configure** (Настройка), чтобы настроить новый подключаемый модуль.</span><span class="sxs-lookup"><span data-stu-id="d59f7-208">Click **Configure** to configure the new plugin.</span></span>

12. <span data-ttu-id="d59f7-209">Выполните следующие действия на странице настройки:</span><span class="sxs-lookup"><span data-stu-id="d59f7-209">Perform following steps on configuration page:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-Confluencemicrosoft-tutorial/addon5.png)
 
    <span data-ttu-id="d59f7-211">а.</span><span class="sxs-lookup"><span data-stu-id="d59f7-211">a.</span></span> <span data-ttu-id="d59f7-212">В поле **URL-адрес метаданных** вставьте **URL-адрес метаданных**, созданный в Azure AD, и нажмите кнопку **Разрешить**.</span><span class="sxs-lookup"><span data-stu-id="d59f7-212">In **Metadata URL** paste the **Metadata URL** generated from Azure AD and click the **Resolve** button.</span></span> <span data-ttu-id="d59f7-213">Будет прочитан URL-адрес метаданных поставщика удостоверений, а также будут заполнены все поля сведений.</span><span class="sxs-lookup"><span data-stu-id="d59f7-213">It reads the IdP metadata URL and populates all the fields information.</span></span>

    > [!Note]
    > <span data-ttu-id="d59f7-214">По умолчанию идентификатор пользователя SAML указан в идентификаторе имени.</span><span class="sxs-lookup"><span data-stu-id="d59f7-214">Default SAML User ID location is Name Identifier.</span></span> <span data-ttu-id="d59f7-215">Его можно заменить атрибутом и ввести имя соответствующего атрибута.</span><span class="sxs-lookup"><span data-stu-id="d59f7-215">You can change this to an attribute option and enter the appropriate attribute name.</span></span>

    > [!TIP]
    > <span data-ttu-id="d59f7-216">Убедитесь, что с приложением сопоставлен только один сертификат, чтобы при разрешении метаданных не возникла ошибка.</span><span class="sxs-lookup"><span data-stu-id="d59f7-216">Ensure that there is only one certificate mapped against the app so that there is no error in resolving the metadata.</span></span> <span data-ttu-id="d59f7-217">Если имеется несколько сертификатов, то при разрешении метаданных администратор увидит сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="d59f7-217">If there are multiple certificates, upon resolving the metadata, admin gets an error.</span></span>
    
    <span data-ttu-id="d59f7-218">b.</span><span class="sxs-lookup"><span data-stu-id="d59f7-218">b.</span></span> <span data-ttu-id="d59f7-219">Скопируйте значения **идентификатора, URL-адреса ответа и URL-адреса входа** и вставьте их в соответствующие поля **идентификатора, URL-адреса ответа и URL-адреса входа** в разделе **Домены и URL-адреса приложения Confluence SAML SSO by Microsoft** на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="d59f7-219">Copy the **Identifier, Reply URL and Sign on URL** values and paste them in **Identifier, Reply URL and Sign on URL** textboxes respectively in **Confluence SAML SSO by Microsoft Domain and URLs** section on Azure portal.</span></span>

    <span data-ttu-id="d59f7-220">c.</span><span class="sxs-lookup"><span data-stu-id="d59f7-220">c.</span></span> <span data-ttu-id="d59f7-221">В поле **Имя кнопки входа** введите имя кнопки, которую должны видеть на экране входа пользователи вашей организации.</span><span class="sxs-lookup"><span data-stu-id="d59f7-221">In **Login Button Name** type the name of button your organization wants the users to see on login screen.</span></span>

    <span data-ttu-id="d59f7-222">г)</span><span class="sxs-lookup"><span data-stu-id="d59f7-222">d.</span></span> <span data-ttu-id="d59f7-223">Для параметра **Расположения идентификатора пользователя SAML** укажите значение **Идентификатор пользователя указан в элементе NameIdentifier утверждения Subject** или **Идентификатор пользователя указан в элементе Attribute**.</span><span class="sxs-lookup"><span data-stu-id="d59f7-223">In **SAML User ID Locations** select either **User ID is in the NameIdentifier element of the Subject statement** or **User ID is in an Attribute element**.</span></span>  <span data-ttu-id="d59f7-224">Этим идентификатором должен быть идентификатор пользователя Confluence.</span><span class="sxs-lookup"><span data-stu-id="d59f7-224">This ID has to be the Confluence user id.</span></span> <span data-ttu-id="d59f7-225">Если идентификатор пользователя не совпадет, система не позволит пользователям выполнить вход.</span><span class="sxs-lookup"><span data-stu-id="d59f7-225">If the user id is not matched, then system will not allow users to log in.</span></span> 
    
    <span data-ttu-id="d59f7-226">д.</span><span class="sxs-lookup"><span data-stu-id="d59f7-226">e.</span></span> <span data-ttu-id="d59f7-227">Если выбран параметр **Идентификатор пользователя указан в элементе Attribute**, то в текстовом поле **Имя атрибута** введите имя атрибута, в котором ожидается идентификатор пользователя.</span><span class="sxs-lookup"><span data-stu-id="d59f7-227">If you select **User ID is in an Attribute element** option, then in **Attribute name** textbox type the name of the attribute where User Id is expected.</span></span> 

    <span data-ttu-id="d59f7-228">f.</span><span class="sxs-lookup"><span data-stu-id="d59f7-228">f.</span></span> <span data-ttu-id="d59f7-229">При использовании федеративного домена (например, AD FS и т. д.) для Azure AD выберите параметр **Включить обнаружение домашней области** и настройте **доменное имя**.</span><span class="sxs-lookup"><span data-stu-id="d59f7-229">If you are using the federated domain (like ADFS etc.) with Azure AD, then click on the **Enable Home Realm Discovery** option and configure the **Domain Name**.</span></span>
    
    <span data-ttu-id="d59f7-230">g.</span><span class="sxs-lookup"><span data-stu-id="d59f7-230">g.</span></span> <span data-ttu-id="d59f7-231">В поле **Доменное имя** введите доменное имя, если вы используете вход на основе AD FS.</span><span class="sxs-lookup"><span data-stu-id="d59f7-231">In **Domain Name** type the domain name here in case of the ADFS-based login.</span></span>

    <span data-ttu-id="d59f7-232">h.</span><span class="sxs-lookup"><span data-stu-id="d59f7-232">h.</span></span> <span data-ttu-id="d59f7-233">Установите флажок **Включить единый выход**, если после выхода пользователя из Confluence требуется выходить и из Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d59f7-233">Check **Enable Single Sign out** if you wish to log out from Azure AD when a user logs out from Confluence.</span></span> 

    <span data-ttu-id="d59f7-234">i.</span><span class="sxs-lookup"><span data-stu-id="d59f7-234">i.</span></span> <span data-ttu-id="d59f7-235">Нажмите кнопку **Сохранить**, чтобы сохранить изменения.</span><span class="sxs-lookup"><span data-stu-id="d59f7-235">Click **Save** button to save the settings.</span></span>


> [!TIP]
> <span data-ttu-id="d59f7-236">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="d59f7-236">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d59f7-237">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="d59f7-237">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d59f7-238">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="d59f7-238">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="d59f7-239">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="d59f7-239">Creating an Azure AD test user</span></span>
<span data-ttu-id="d59f7-240">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d59f7-240">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="d59f7-242">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="d59f7-242">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d59f7-243">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d59f7-243">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-confluencemicrosoft-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="d59f7-245">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="d59f7-245">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-confluencemicrosoft-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="d59f7-247">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="d59f7-247">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-confluencemicrosoft-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="d59f7-249">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="d59f7-249">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-confluencemicrosoft-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="d59f7-251">а.</span><span class="sxs-lookup"><span data-stu-id="d59f7-251">a.</span></span> <span data-ttu-id="d59f7-252">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d59f7-252">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d59f7-253">b.</span><span class="sxs-lookup"><span data-stu-id="d59f7-253">b.</span></span> <span data-ttu-id="d59f7-254">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="d59f7-254">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="d59f7-255">c.</span><span class="sxs-lookup"><span data-stu-id="d59f7-255">c.</span></span> <span data-ttu-id="d59f7-256">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="d59f7-256">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="d59f7-257">d.</span><span class="sxs-lookup"><span data-stu-id="d59f7-257">d.</span></span> <span data-ttu-id="d59f7-258">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="d59f7-258">Click **Create**.</span></span>
 
### <a name="creating-a-confluence-saml-sso-by-microsoft-test-user"></a><span data-ttu-id="d59f7-259">Создание тестового пользователя Confluence SAML SSO by Microsoft</span><span class="sxs-lookup"><span data-stu-id="d59f7-259">Creating a Confluence SAML SSO by Microsoft test user</span></span>

<span data-ttu-id="d59f7-260">Чтобы пользователи Azure AD могли входить на локальный сервер Confluence, их необходимо подготовить в Confluence SAML SSO by Microsoft.</span><span class="sxs-lookup"><span data-stu-id="d59f7-260">To enable Azure AD users to log in to Confluence on premise server, they must be provisioned into Confluence SAML SSO by Microsoft.</span></span> <span data-ttu-id="d59f7-261">Для Confluence SAML SSO by Microsoft подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="d59f7-261">For Confluence SAML SSO by Microsoft, provisioning is a manual task.</span></span>

<span data-ttu-id="d59f7-262">**Чтобы подготовить учетную запись пользователя, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="d59f7-262">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="d59f7-263">Войдите на локальный сервер Confluence как администратор.</span><span class="sxs-lookup"><span data-stu-id="d59f7-263">Log in to your Confluence on premise server as an administrator.</span></span>

2. <span data-ttu-id="d59f7-264">Наведите указатель мыши на шестеренку и щелкните **User management** (Управление пользователями).</span><span class="sxs-lookup"><span data-stu-id="d59f7-264">Hover on cog and click the **User management**.</span></span>

    ![Добавление сотрудника](./media/active-directory-saas-confluencemicrosoft-tutorial/user1.png) 

3. <span data-ttu-id="d59f7-266">В разделе "Users" (Пользователи) выберите вкладку **Add users** (Добавление пользователей).</span><span class="sxs-lookup"><span data-stu-id="d59f7-266">Under Users section, click **Add users** tab.</span></span> <span data-ttu-id="d59f7-267">На диалоговой странице **Add a User** (Добавление пользователя) выполните следующее.</span><span class="sxs-lookup"><span data-stu-id="d59f7-267">On the **“Add a User”** dialog page, perform the following steps:</span></span>

    ![Добавление сотрудника](./media/active-directory-saas-confluencemicrosoft-tutorial/user2.png) 

    <span data-ttu-id="d59f7-269">а.</span><span class="sxs-lookup"><span data-stu-id="d59f7-269">a.</span></span> <span data-ttu-id="d59f7-270">В текстовом поле **Username** (Имя пользователя) введите электронный адрес пользователя, например Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d59f7-270">In the **Username** textbox, type the email of user like Britta Simon.</span></span>

    <span data-ttu-id="d59f7-271">b.</span><span class="sxs-lookup"><span data-stu-id="d59f7-271">b.</span></span> <span data-ttu-id="d59f7-272">В текстовом поле **Full Name** (Полное имя) введите полное имя пользователя, например Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d59f7-272">In the **Full Name** textbox, type the full name of user like Britta Simon.</span></span>

    <span data-ttu-id="d59f7-273">c.</span><span class="sxs-lookup"><span data-stu-id="d59f7-273">c.</span></span> <span data-ttu-id="d59f7-274">В текстовом поле **Email** (Электронная почта) введите адрес электронной почты пользователя, например Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="d59f7-274">In the **Email** textbox, type the email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="d59f7-275">г)</span><span class="sxs-lookup"><span data-stu-id="d59f7-275">d.</span></span> <span data-ttu-id="d59f7-276">В текстовом поле **Password** (Пароль) введите пароль пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d59f7-276">In the **Password** textbox, type the password for Britta Simon.</span></span>

    <span data-ttu-id="d59f7-277">д.</span><span class="sxs-lookup"><span data-stu-id="d59f7-277">e.</span></span> <span data-ttu-id="d59f7-278">Щелкните **Confirm Password** (Подтвердить пароль) и повторно введите пароль.</span><span class="sxs-lookup"><span data-stu-id="d59f7-278">Click **Confirm Password** reenter the password.</span></span>
    
    <span data-ttu-id="d59f7-279">f.</span><span class="sxs-lookup"><span data-stu-id="d59f7-279">f.</span></span> <span data-ttu-id="d59f7-280">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="d59f7-280">Click **Add** button.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="d59f7-281">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="d59f7-281">Assigning the Azure AD test user</span></span>

<span data-ttu-id="d59f7-282">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к Confluence SAML SSO by Microsoft.</span><span class="sxs-lookup"><span data-stu-id="d59f7-282">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Confluence SAML SSO by Microsoft.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="d59f7-284">**Чтобы назначить пользователя Britta Simon в Confluence SAML SSO by Microsoft, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="d59f7-284">**To assign Britta Simon to Confluence SAML SSO by Microsoft, perform the following steps:**</span></span>

1. <span data-ttu-id="d59f7-285">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="d59f7-285">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="d59f7-287">Из списка приложений выберите **Confluence SAML SSO by Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="d59f7-287">In the applications list, select **Confluence SAML SSO by Microsoft**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_confluencemicrosoft_app.png) 

3. <span data-ttu-id="d59f7-289">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="d59f7-289">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="d59f7-291">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="d59f7-291">Click **Add** button.</span></span> <span data-ttu-id="d59f7-292">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="d59f7-292">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="d59f7-294">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="d59f7-294">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d59f7-295">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="d59f7-295">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d59f7-296">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="d59f7-296">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="d59f7-297">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="d59f7-297">Testing single sign-on</span></span>

<span data-ttu-id="d59f7-298">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="d59f7-298">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d59f7-299">Щелкнув элемент "Confluence SAML SSO by Microsoft" на панели доступа, вы автоматически войдете в приложение Confluence SAML SSO by Microsoft.</span><span class="sxs-lookup"><span data-stu-id="d59f7-299">When you click the Confluence SAML SSO by Microsoft tile in the Access Panel, you should get automatically signed-on to your Confluence SAML SSO by Microsoft application.</span></span>
<span data-ttu-id="d59f7-300">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d59f7-300">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d59f7-301">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="d59f7-301">Additional resources</span></span>

* [<span data-ttu-id="d59f7-302">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d59f7-302">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d59f7-303">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d59f7-303">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-confluencemicrosoft-tutorial/tutorial_general_203.png

