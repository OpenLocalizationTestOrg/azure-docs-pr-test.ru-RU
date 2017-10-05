---
title: "Руководство по интеграции Azure Active Directory с JIRA SAML SSO by Microsoft | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в JIRA SAML SSO by Microsoft."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0dc847b9-eec4-4c31-845e-0144ddedc4a7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: b5f7813c8244d2964b6894ae49cd64e0ee71b704
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jira-saml-sso-by-microsoft"></a><span data-ttu-id="ef481-103">Руководство по интеграции Azure Active Directory с JIRA SAML SSO by Microsoft</span><span class="sxs-lookup"><span data-stu-id="ef481-103">Tutorial: Azure Active Directory integration with JIRA SAML SSO by Microsoft</span></span>

<span data-ttu-id="ef481-104">В этом руководстве описано, как интегрировать JIRA SAML SSO by Microsoft с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ef481-104">In this tutorial, you learn how to integrate JIRA SAML SSO by Microsoft with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ef481-105">Интеграция Azure AD с JIRA SAML SSO by Microsoft обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="ef481-105">Integrating JIRA SAML SSO by Microsoft with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ef481-106">С помощью Azure AD вы можете контролировать доступ к JIRA SAML SSO by Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ef481-106">You can control in Azure AD who has access to JIRA SAML SSO by Microsoft</span></span>
- <span data-ttu-id="ef481-107">Можно включить автоматический вход пользователей в JIRA SAML SSO by Microsoft, то есть единый вход, с учетными записями Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ef481-107">You can enable your users to automatically get signed-on to JIRA SAML SSO by Microsoft (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ef481-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="ef481-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ef481-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ef481-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ef481-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ef481-110">Prerequisites</span></span>

<span data-ttu-id="ef481-111">Чтобы настроить интеграцию Azure AD с JIRA SAML SSO by Microsoft, вам потребуется следующее:</span><span class="sxs-lookup"><span data-stu-id="ef481-111">To configure Azure AD integration with JIRA SAML SSO by Microsoft, you need the following items:</span></span>

- <span data-ttu-id="ef481-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="ef481-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ef481-113">серверное приложение JIRA, установленное на 64-разрядной версии сервера Windows (в локальной среде или облачной инфраструктуре IaaS);</span><span class="sxs-lookup"><span data-stu-id="ef481-113">JIRA server application installed on a Windows 64-bit server (on premise or on the cloud IaaS infrastructure)</span></span>
- <span data-ttu-id="ef481-114">поддержка HTTPS на сервере JIRA;</span><span class="sxs-lookup"><span data-stu-id="ef481-114">JIRA server is HTTPS enabled</span></span>
- <span data-ttu-id="ef481-115">поддерживаемые версии подключаемого модуля JIRA указаны в разделе ниже;</span><span class="sxs-lookup"><span data-stu-id="ef481-115">Note the supported versions for JIRA Plugin are mentioned in below section.</span></span>
- <span data-ttu-id="ef481-116">сервер JIRA должен быть доступен через Интернет, в частности, на странице входа Azure AD для аутентификации, и должен иметь возможность получать маркер из Azure AD;</span><span class="sxs-lookup"><span data-stu-id="ef481-116">JIRA server is reachable on internet particularly to Azure AD Login page for authentication and should able to receive the token from Azure AD</span></span>
- <span data-ttu-id="ef481-117">в JIRA должны быть настроены учетные данные администратора;</span><span class="sxs-lookup"><span data-stu-id="ef481-117">Admin credentials are set up in JIRA</span></span>
- <span data-ttu-id="ef481-118">в JIRA должна быть отключена поддержка WebSudo;</span><span class="sxs-lookup"><span data-stu-id="ef481-118">WebSudo is disabled in JIRA</span></span>
- <span data-ttu-id="ef481-119">в серверном приложении JIRA должен быть создан тестовый пользователь.</span><span class="sxs-lookup"><span data-stu-id="ef481-119">Test user created in the JIRA server application</span></span>

> [!NOTE]
> <span data-ttu-id="ef481-120">Мы не рекомендуем использовать рабочую среду JIRA для проверки действий в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="ef481-120">To test the steps in this tutorial, we do not recommend using a production environment of JIRA.</span></span> <span data-ttu-id="ef481-121">Сначала протестируйте интеграцию в среде разработки или промежуточной среде приложения, а затем используйте ее в рабочей среде.</span><span class="sxs-lookup"><span data-stu-id="ef481-121">Test the integration first in development or staging environment of the application and then use the production environment.</span></span>

<span data-ttu-id="ef481-122">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="ef481-122">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ef481-123">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="ef481-123">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ef481-124">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ef481-124">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="supported-versions-of-jira"></a><span data-ttu-id="ef481-125">Поддерживаемые версии JIRA</span><span class="sxs-lookup"><span data-stu-id="ef481-125">Supported versions of JIRA</span></span> 

<span data-ttu-id="ef481-126">Сейчас поддерживаются следующие версии JIRA:</span><span class="sxs-lookup"><span data-stu-id="ef481-126">As of now, following versions of JIRA are supported:</span></span>

- <span data-ttu-id="ef481-127">JIRA Core и JIRA Software: 6.0–7.2.0;</span><span class="sxs-lookup"><span data-stu-id="ef481-127">JIRA Core and Software: 6.0 to 7.2.0</span></span>
- <span data-ttu-id="ef481-128">JIRA Service Desk: 3.0–3.2.</span><span class="sxs-lookup"><span data-stu-id="ef481-128">JIRA Service Desk: 3.0 to 3.2</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ef481-129">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="ef481-129">Scenario description</span></span>
<span data-ttu-id="ef481-130">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="ef481-130">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ef481-131">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="ef481-131">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ef481-132">Добавление JIRA SAML SSO by Microsoft из коллекции.</span><span class="sxs-lookup"><span data-stu-id="ef481-132">Adding JIRA SAML SSO by Microsoft from the gallery</span></span>
2. <span data-ttu-id="ef481-133">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ef481-133">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jira-saml-sso-by-microsoft-from-the-gallery"></a><span data-ttu-id="ef481-134">Добавление JIRA SAML SSO by Microsoft из коллекции</span><span class="sxs-lookup"><span data-stu-id="ef481-134">Adding JIRA SAML SSO by Microsoft from the gallery</span></span>
<span data-ttu-id="ef481-135">Чтобы настроить интеграцию JIRA SAML SSO by Microsoft с Azure AD, необходимо добавить JIRA SAML SSO by Microsoft из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="ef481-135">To configure the integration of JIRA SAML SSO by Microsoft into Azure AD, you need to add JIRA SAML SSO by Microsoft from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ef481-136">**Чтобы добавить JIRA SAML SSO by Microsoft из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="ef481-136">**To add JIRA SAML SSO by Microsoft from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ef481-137">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ef481-137">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ef481-139">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="ef481-139">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ef481-140">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="ef481-140">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="ef481-142">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="ef481-142">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="ef481-144">В поле поиска введите **JIRA SAML SSO by Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="ef481-144">In the search box, type **JIRA SAML SSO by Microsoft**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_search.png)

5. <span data-ttu-id="ef481-146">На панели результатов выберите **JIRA SAML SSO by Microsoft** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="ef481-146">In the results panel, select **JIRA SAML SSO by Microsoft**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ef481-148">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ef481-148">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ef481-149">В этом разделе описана настройка и проверка единого входа Azure AD в JIRA SAML SSO by Microsoft с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ef481-149">In this section, you configure and test Azure AD single sign-on with JIRA SAML SSO by Microsoft based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ef481-150">Чтобы единый вход работал, Azure AD необходимо знать, какой пользователь в JIRA SAML SSO by Microsoft соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ef481-150">For single sign-on to work, Azure AD needs to know what the counterpart user in JIRA SAML SSO by Microsoft is to a user in Azure AD.</span></span> <span data-ttu-id="ef481-151">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в JIRA SAML SSO by Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ef481-151">In other words, a link relationship between an Azure AD user and the related user in JIRA SAML SSO by Microsoft needs to be established.</span></span>

<span data-ttu-id="ef481-152">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в JIRA SAML SSO by Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ef481-152">In JIRA SAML SSO by Microsoft, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="ef481-153">Чтобы настроить и проверить единый вход Microsoft Azure AD в JIRA SAML SSO by Microsoft, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="ef481-153">To configure and test Azure AD single sign-on with JIRA SAML SSO by Microsoft, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ef481-154">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="ef481-154">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ef481-155">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ef481-155">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ef481-156">**[Создание тестового пользователя JIRA SAML SSO by Microsoft](#creating-a-jira-saml-sso-by-microsoft-test-user)** требуется для того, чтобы в JIRA SAML SSO by Microsoft существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ef481-156">**[Creating a JIRA SAML SSO by Microsoft test user](#creating-a-jira-saml-sso-by-microsoft-test-user)** - to have a counterpart of Britta Simon in JIRA SAML SSO by Microsoft that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ef481-157">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ef481-157">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ef481-158">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="ef481-158">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ef481-159">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ef481-159">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ef481-160">В данном разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении JIRA SAML SSO by Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ef481-160">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your JIRA SAML SSO by Microsoft application.</span></span>

<span data-ttu-id="ef481-161">**Чтобы настроить единый вход Azure AD в JIRA SAML SSO by Microsoft, сделайте следующее.**</span><span class="sxs-lookup"><span data-stu-id="ef481-161">**To configure Azure AD single sign-on with JIRA SAML SSO by Microsoft, perform the following steps:**</span></span>

1. <span data-ttu-id="ef481-162">На портале Azure на странице интеграции с приложением **JIRA SAML SSO by Microsoft** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="ef481-162">In the Azure portal, on the **JIRA SAML SSO by Microsoft** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="ef481-164">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="ef481-164">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_samlbase.png)

3. <span data-ttu-id="ef481-166">В разделе **Домены и URL-адреса приложения JIRA SAML SSO by Microsoft** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="ef481-166">On the **JIRA SAML SSO by Microsoft Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_url.png)

    <span data-ttu-id="ef481-168">а.</span><span class="sxs-lookup"><span data-stu-id="ef481-168">a.</span></span> <span data-ttu-id="ef481-169">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<domain:port>/plugins/servlet/saml/auth`</span><span class="sxs-lookup"><span data-stu-id="ef481-169">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<domain:port>/plugins/servlet/saml/auth`</span></span>

    <span data-ttu-id="ef481-170">b.</span><span class="sxs-lookup"><span data-stu-id="ef481-170">b.</span></span> <span data-ttu-id="ef481-171">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<domain:port>/`</span><span class="sxs-lookup"><span data-stu-id="ef481-171">In the **Identifier** textbox, type a URL using the following pattern: `https://<domain:port>/`</span></span>

    <span data-ttu-id="ef481-172">c.</span><span class="sxs-lookup"><span data-stu-id="ef481-172">c.</span></span> <span data-ttu-id="ef481-173">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате: `https://<domain:port>/plugins/servlet/saml/auth`.</span><span class="sxs-lookup"><span data-stu-id="ef481-173">In the **Reply URL** textbox, type a URL using the following pattern: `https://<domain:port>/plugins/servlet/saml/auth`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ef481-174">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="ef481-174">These values are not real.</span></span> <span data-ttu-id="ef481-175">Замените их фактическими значениями идентификатора, URL-адреса ответа и URL-адреса входа.</span><span class="sxs-lookup"><span data-stu-id="ef481-175">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="ef481-176">Если это именованный URL-адрес, то порт указывать необязательно.</span><span class="sxs-lookup"><span data-stu-id="ef481-176">Port is optional in case it’s a named URL.</span></span> <span data-ttu-id="ef481-177">Эти значения предоставляются во время настройки подключаемого модуля JIRA, которая описывается далее в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="ef481-177">These values are received during the configuration of Jira plugin, which is explained later in the tutorial.</span></span>
 
4. <span data-ttu-id="ef481-178">Для создания URL-адреса **метаданных** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="ef481-178">To generate the **Metadata** url, perform the following steps:</span></span>

    <span data-ttu-id="ef481-179">а.</span><span class="sxs-lookup"><span data-stu-id="ef481-179">a.</span></span> <span data-ttu-id="ef481-180">Щелкните **Регистрация приложений**.</span><span class="sxs-lookup"><span data-stu-id="ef481-180">Click **App registrations**.</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-jiramicrosoft-tutorial/appregistrations.png)
   
    <span data-ttu-id="ef481-182">b.</span><span class="sxs-lookup"><span data-stu-id="ef481-182">b.</span></span> <span data-ttu-id="ef481-183">Щелкните **Конечные точки**, чтобы открыть диалоговое окно **Конечные точки**.</span><span class="sxs-lookup"><span data-stu-id="ef481-183">Click **Endpoints** to open **Endpoints** dialog box.</span></span>  
    
    ![Настройка единого входа](./media/active-directory-saas-jiramicrosoft-tutorial/endpointicon.png)

    <span data-ttu-id="ef481-185">c.</span><span class="sxs-lookup"><span data-stu-id="ef481-185">c.</span></span> <span data-ttu-id="ef481-186">Нажмите кнопку "Копировать", чтобы скопировать URL-адрес **документа метаданных федерации**, а затем вставьте его в блокнот.</span><span class="sxs-lookup"><span data-stu-id="ef481-186">Click the copy button to copy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-jiramicrosoft-tutorial/endpoint.png)
     
    <span data-ttu-id="ef481-188">г)</span><span class="sxs-lookup"><span data-stu-id="ef481-188">d.</span></span> <span data-ttu-id="ef481-189">Теперь перейдите к странице свойств **JIRA SAML SSO by Microsoft** и скопируйте **идентификатор приложения** с помощью кнопки **Копировать**, а затем вставьте его в Блокнот.</span><span class="sxs-lookup"><span data-stu-id="ef481-189">Now go to the property page of **JIRA SAML SSO by Microsoft** and copy the **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-jiramicrosoft-tutorial/appid.png)

    <span data-ttu-id="ef481-191">д.</span><span class="sxs-lookup"><span data-stu-id="ef481-191">e.</span></span> <span data-ttu-id="ef481-192">Создайте **URL-адрес метаданных** в формате `<FEDERATION METADATA DOCUMENT url>?appid=<application id>` и скопируйте это значение в Блокнот, так как оно будет использовано позже для настройки подключаемого модуля.</span><span class="sxs-lookup"><span data-stu-id="ef481-192">Generate the **Metadata URL** using the following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>` and copy this value in notepad as it is used later for the configuration of the plugin.</span></span>

5. <span data-ttu-id="ef481-193">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="ef481-193">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ef481-195">Обратитесь к [корпорации Майкрософт](mailto:waadpartners@microsoft.com), предоставив следующие данные подключаемого модуля JIRA:</span><span class="sxs-lookup"><span data-stu-id="ef481-195">Contact [Microsoft](mailto:waadpartners@microsoft.com) with the following information for the JIRA plugin.</span></span>
    
    *   <span data-ttu-id="ef481-196">имя клиента;</span><span class="sxs-lookup"><span data-stu-id="ef481-196">Customer Name:</span></span>
    *   <span data-ttu-id="ef481-197">Основное доменное имя:</span><span class="sxs-lookup"><span data-stu-id="ef481-197">Primary domain name:</span></span>
    *   <span data-ttu-id="ef481-198">Azure AD Premium: да или нет (подключаемый модуль будет доступен для всех клиентов с номерами SKU уровня "Бесплатный", "Базовый" и "Премиум")</span><span class="sxs-lookup"><span data-stu-id="ef481-198">Azure AD Premium: Yes/No (Plugin will be available to all     the customer Free, Basic, and Premium SKU)</span></span>
    *   <span data-ttu-id="ef481-199">число пользователей, которые будут использовать данную интеграцию;</span><span class="sxs-lookup"><span data-stu-id="ef481-199">Number of users who will be using this integration:</span></span>
    *   <span data-ttu-id="ef481-200">версия JIRA;</span><span class="sxs-lookup"><span data-stu-id="ef481-200">JIRA Version:</span></span>
    *   <span data-ttu-id="ef481-201">комментарии.</span><span class="sxs-lookup"><span data-stu-id="ef481-201">Comments:</span></span>

7. <span data-ttu-id="ef481-202">В другом окне веб-браузера войдите в свой экземпляр JIRA в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="ef481-202">In a different web browser window, log in to your JIRA instance as an administrator.</span></span>

8. <span data-ttu-id="ef481-203">Наведите указатель мыши на шестеренку и щелкните **Add-ons** (Надстройки).</span><span class="sxs-lookup"><span data-stu-id="ef481-203">Hover on cog and click the **Add-ons**.</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-jiramicrosoft-tutorial/addon1.png)

9. <span data-ttu-id="ef481-205">На вкладке "Надстройки" щелкните **Управление надстройками**.</span><span class="sxs-lookup"><span data-stu-id="ef481-205">Under Add-ons tab section, click **Manage add-ons**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-jiramicrosoft-tutorial/addon7.png)

10. <span data-ttu-id="ef481-207">Вручную отправьте подключаемый модуль, предоставленный корпорацией Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="ef481-207">Manually upload the plugin provided by Microsoft.</span></span> <span data-ttu-id="ef481-208">После установки подключаемый модуль появится в разделе **Управление надстройками**, подраздел **Установленные пользователем**.</span><span class="sxs-lookup"><span data-stu-id="ef481-208">Once the plugin is installed, it appears in **User Installed** add-ons section of **Manage Add-on** section.</span></span>

11. <span data-ttu-id="ef481-209">Щелкните **Configure** (Настройка), чтобы настроить новый подключаемый модуль.</span><span class="sxs-lookup"><span data-stu-id="ef481-209">Click **Configure** to configure the new plugin.</span></span>

12. <span data-ttu-id="ef481-210">Выполните следующие действия на странице настройки:</span><span class="sxs-lookup"><span data-stu-id="ef481-210">Perform following steps on configuration page:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-jiramicrosoft-tutorial/addon5.png)
 
    <span data-ttu-id="ef481-212">а.</span><span class="sxs-lookup"><span data-stu-id="ef481-212">a.</span></span> <span data-ttu-id="ef481-213">В поле **URL-адрес метаданных** вставьте **URL-адрес метаданных**, созданный в Azure AD, и нажмите кнопку **Разрешить**.</span><span class="sxs-lookup"><span data-stu-id="ef481-213">In **Metadata URL** paste the **Metadata URL** generated from Azure AD and click the **Resolve** button.</span></span> <span data-ttu-id="ef481-214">Будет прочитан URL-адрес метаданных поставщика удостоверений, а также будут заполнены все поля сведений.</span><span class="sxs-lookup"><span data-stu-id="ef481-214">It reads the IdP metadata URL and populates all the fields information.</span></span>

    > [!Note]
    > <span data-ttu-id="ef481-215">По умолчанию идентификатор пользователя SAML указан в идентификаторе имени.</span><span class="sxs-lookup"><span data-stu-id="ef481-215">Default SAML User ID location is Name Identifier.</span></span> <span data-ttu-id="ef481-216">Его можно заменить атрибутом и ввести имя соответствующего атрибута.</span><span class="sxs-lookup"><span data-stu-id="ef481-216">You can change this to an attribute option and enter the appropriate attribute name.</span></span>

    > [!TIP]
    > <span data-ttu-id="ef481-217">Убедитесь, что с приложением сопоставлен только один сертификат, чтобы при разрешении метаданных не возникла ошибка.</span><span class="sxs-lookup"><span data-stu-id="ef481-217">Ensure that there is only one certificate mapped against the app so that there is no error in resolving the metadata.</span></span> <span data-ttu-id="ef481-218">Если имеется несколько сертификатов, то при разрешении метаданных администратор увидит сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="ef481-218">If there are multiple certificates, upon resolving the metadata, admin gets an error.</span></span>
    
    <span data-ttu-id="ef481-219">b.</span><span class="sxs-lookup"><span data-stu-id="ef481-219">b.</span></span> <span data-ttu-id="ef481-220">Скопируйте значения **идентификатора, URL-адреса ответа и URL-адреса входа** и вставьте их в соответствующие поля **идентификатора, URL-адреса ответа и URL-адреса входа** в разделе **Домены и URL-адреса приложения JIRA SAML SSO by Microsoft** на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="ef481-220">Copy the **Identifier, Reply URL and Sign on URL** values and paste them in **Identifier, Reply URL and Sign on URL** textboxes respectively in **JIRA SAML SSO by Microsoft Domain and URLs** section on Azure portal.</span></span>

    <span data-ttu-id="ef481-221">c.</span><span class="sxs-lookup"><span data-stu-id="ef481-221">c.</span></span> <span data-ttu-id="ef481-222">В поле **Имя кнопки входа** введите имя кнопки, которую должны видеть на экране входа пользователи вашей организации.</span><span class="sxs-lookup"><span data-stu-id="ef481-222">In **Login Button Name** type the name of button your organization wants the users to see on login screen.</span></span>

    <span data-ttu-id="ef481-223">г)</span><span class="sxs-lookup"><span data-stu-id="ef481-223">d.</span></span> <span data-ttu-id="ef481-224">Для параметра **SAML User ID Locations** (Расположения идентификатора пользователя SAML) выберите значение **User ID is in the NameIdentifier element of the Subject statement** (Идентификатор пользователя указан в элементе NameIdentifier утверждения Subject) или **User ID is in an Attribute element** (Идентификатор пользователя указан в элементе Attribute).</span><span class="sxs-lookup"><span data-stu-id="ef481-224">In **SAML User ID Locations** select either **User ID is in the NameIdentifier element of the Subject statement** or **User ID is in an Attribute element**.</span></span>  <span data-ttu-id="ef481-225">Этим идентификатором должен быть идентификатор пользователя JIRA.</span><span class="sxs-lookup"><span data-stu-id="ef481-225">This ID has to be the JIRA user id.</span></span> <span data-ttu-id="ef481-226">Если идентификатор пользователя не совпадет, система не позволит пользователям выполнить вход.</span><span class="sxs-lookup"><span data-stu-id="ef481-226">If the user id is not matched, then system will not allow users to log in.</span></span> 
    
    <span data-ttu-id="ef481-227">д.</span><span class="sxs-lookup"><span data-stu-id="ef481-227">e.</span></span> <span data-ttu-id="ef481-228">Если выбран параметр **Идентификатор пользователя указан в элементе Attribute**, то в текстовом поле **Имя атрибута** введите имя атрибута, в котором ожидается идентификатор пользователя.</span><span class="sxs-lookup"><span data-stu-id="ef481-228">If you select **User ID is in an Attribute element** option, then in **Attribute name** textbox type the name of the attribute where User Id is expected.</span></span> 

    <span data-ttu-id="ef481-229">f.</span><span class="sxs-lookup"><span data-stu-id="ef481-229">f.</span></span> <span data-ttu-id="ef481-230">При использовании федеративного домена (например, AD FS и т. д.) для Azure AD выберите параметр **Включить обнаружение домашней области** и настройте **доменное имя**.</span><span class="sxs-lookup"><span data-stu-id="ef481-230">If you are using the federated domain (like ADFS etc.) with Azure AD, then click on the **Enable Home Realm Discovery** option and configure the **Domain Name**.</span></span>
    
    <span data-ttu-id="ef481-231">g.</span><span class="sxs-lookup"><span data-stu-id="ef481-231">g.</span></span> <span data-ttu-id="ef481-232">В поле **Доменное имя** введите доменное имя, если вы используете вход на основе AD FS.</span><span class="sxs-lookup"><span data-stu-id="ef481-232">In **Domain Name** type the domain name here in case of the ADFS-based login.</span></span>

    <span data-ttu-id="ef481-233">h.</span><span class="sxs-lookup"><span data-stu-id="ef481-233">h.</span></span> <span data-ttu-id="ef481-234">Установите флажок **Enable Single Sign out** (Включить единый выход), если после выхода пользователя из JIRA требуется выходить и из Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ef481-234">Check **Enable Single Sign out** if you wish to log out from Azure AD when a user logs out from JIRA.</span></span> 

    <span data-ttu-id="ef481-235">i.</span><span class="sxs-lookup"><span data-stu-id="ef481-235">i.</span></span> <span data-ttu-id="ef481-236">Нажмите кнопку **Сохранить**, чтобы сохранить изменения.</span><span class="sxs-lookup"><span data-stu-id="ef481-236">Click **Save** button to save the settings.</span></span>

> [!TIP]
> <span data-ttu-id="ef481-237">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="ef481-237">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ef481-238">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="ef481-238">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ef481-239">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="ef481-239">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ef481-240">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="ef481-240">Creating an Azure AD test user</span></span>
<span data-ttu-id="ef481-241">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ef481-241">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="ef481-243">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="ef481-243">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ef481-244">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ef481-244">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ef481-246">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="ef481-246">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ef481-248">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="ef481-248">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ef481-250">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="ef481-250">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jiramicrosoft-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ef481-252">а.</span><span class="sxs-lookup"><span data-stu-id="ef481-252">a.</span></span> <span data-ttu-id="ef481-253">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ef481-253">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ef481-254">b.</span><span class="sxs-lookup"><span data-stu-id="ef481-254">b.</span></span> <span data-ttu-id="ef481-255">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ef481-255">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ef481-256">c.</span><span class="sxs-lookup"><span data-stu-id="ef481-256">c.</span></span> <span data-ttu-id="ef481-257">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="ef481-257">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ef481-258">d.</span><span class="sxs-lookup"><span data-stu-id="ef481-258">d.</span></span> <span data-ttu-id="ef481-259">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="ef481-259">Click **Create**.</span></span>
 
### <a name="creating-a-jira-saml-sso-by-microsoft-test-user"></a><span data-ttu-id="ef481-260">Создание тестового пользователя JIRA SAML SSO by Microsoft</span><span class="sxs-lookup"><span data-stu-id="ef481-260">Creating a JIRA SAML SSO by Microsoft test user</span></span>

<span data-ttu-id="ef481-261">Чтобы пользователи Azure AD могли выполнять вход на локальный сервер JIRA, их необходимо подготовить в JIRA SAML SSO by Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ef481-261">To enable Azure AD users to log in to JIRA on-premise server, they must be provisioned into JIRA SAML SSO by Microsoft.</span></span> <span data-ttu-id="ef481-262">Для JIRA SAML SSO by Microsoft подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="ef481-262">For JIRA SAML SSO by Microsoft, provisioning is a manual task.</span></span>

<span data-ttu-id="ef481-263">**Чтобы подготовить учетную запись пользователя, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="ef481-263">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="ef481-264">Войдите на локальный сервер JIRA в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="ef481-264">Log in to your JIRA on-premise server as an administrator.</span></span>

2. <span data-ttu-id="ef481-265">Наведите указатель мыши на шестеренку и щелкните **User management** (Управление пользователями).</span><span class="sxs-lookup"><span data-stu-id="ef481-265">Hover on cog and click the **User management**.</span></span>

    ![Добавление сотрудника](./media/active-directory-saas-jiramicrosoft-tutorial/user1.png) 

3. <span data-ttu-id="ef481-267">Вы будете перенаправлены на страницу доступа с правами администратора. Введите **пароль** и нажмите кнопку **Confirm** (Подтвердить).</span><span class="sxs-lookup"><span data-stu-id="ef481-267">You are redirected to Administrator Access page to enter **Password** and click **Confirm** button.</span></span>

    ![Добавление сотрудника](./media/active-directory-saas-jiramicrosoft-tutorial/user2.png) 

4. <span data-ttu-id="ef481-269">В разделе **User management** (Управление пользователями) щелкните **Create user** (Создать пользователя).</span><span class="sxs-lookup"><span data-stu-id="ef481-269">Under **User management** tab section, click **create user**.</span></span>

    ![Добавление сотрудника](./media/active-directory-saas-jiramicrosoft-tutorial/user3.png) 

5. <span data-ttu-id="ef481-271">На странице **Create New User** (Создание пользователя) выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="ef481-271">On the **“Create new user”** dialog page, perform the following steps:</span></span>

    ![Добавление сотрудника](./media/active-directory-saas-jiramicrosoft-tutorial/user4.png) 

    <span data-ttu-id="ef481-273">а.</span><span class="sxs-lookup"><span data-stu-id="ef481-273">a.</span></span> <span data-ttu-id="ef481-274">В текстовом поле **Email address** (Адрес электронной почты) введите адрес электронной почты пользователя, например Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="ef481-274">In the **Email address** textbox, type the email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="ef481-275">b.</span><span class="sxs-lookup"><span data-stu-id="ef481-275">b.</span></span> <span data-ttu-id="ef481-276">В текстовом поле **Full Name** (Полное имя) введите полное имя пользователя, например Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ef481-276">In the **Full Name** textbox, type full name of the user like Britta Simon.</span></span>

    <span data-ttu-id="ef481-277">c.</span><span class="sxs-lookup"><span data-stu-id="ef481-277">c.</span></span> <span data-ttu-id="ef481-278">В текстовом поле **Username** (Имя пользователя) введите электронный адрес пользователя, например Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="ef481-278">In the **Username** textbox, type the email of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="ef481-279">г)</span><span class="sxs-lookup"><span data-stu-id="ef481-279">d.</span></span> <span data-ttu-id="ef481-280">В текстовом поле **Password** (Пароль) введите пароль пользователя.</span><span class="sxs-lookup"><span data-stu-id="ef481-280">In the **Password** textbox, type the password of user.</span></span>

    <span data-ttu-id="ef481-281">д.</span><span class="sxs-lookup"><span data-stu-id="ef481-281">e.</span></span> <span data-ttu-id="ef481-282">Щелкните **Create user** (Создать пользователя).</span><span class="sxs-lookup"><span data-stu-id="ef481-282">Click **Create user**.</span></span>   

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ef481-283">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="ef481-283">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ef481-284">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к JIRA SAML SSO by Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ef481-284">In this section, you enable Britta Simon to use Azure single sign-on by granting access to JIRA SAML SSO by Microsoft.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="ef481-286">**Чтобы назначить пользователя Britta Simon в JIRA SAML SSO by Microsoft, сделайте следующее.**</span><span class="sxs-lookup"><span data-stu-id="ef481-286">**To assign Britta Simon to JIRA SAML SSO by Microsoft, perform the following steps:**</span></span>

1. <span data-ttu-id="ef481-287">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="ef481-287">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="ef481-289">Из списка приложений выберите **JIRA SAML SSO by Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="ef481-289">In the applications list, select **JIRA SAML SSO by Microsoft**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_jiramicrosoft_app.png) 

3. <span data-ttu-id="ef481-291">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="ef481-291">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="ef481-293">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="ef481-293">Click **Add** button.</span></span> <span data-ttu-id="ef481-294">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="ef481-294">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="ef481-296">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="ef481-296">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ef481-297">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="ef481-297">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ef481-298">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="ef481-298">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ef481-299">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="ef481-299">Testing single sign-on</span></span>

<span data-ttu-id="ef481-300">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="ef481-300">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ef481-301">Щелкнув элемент "JIRA SAML SSO by Microsoft" на панели доступа, вы автоматически войдете в приложение JIRA SAML SSO by Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ef481-301">When you click the JIRA SAML SSO by Microsoft tile in the Access Panel, you should get automatically signed-on to your JIRA SAML SSO by Microsoft application.</span></span>
<span data-ttu-id="ef481-302">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ef481-302">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ef481-303">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="ef481-303">Additional resources</span></span>

* [<span data-ttu-id="ef481-304">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ef481-304">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ef481-305">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ef481-305">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jiramicrosoft-tutorial/tutorial_general_203.png

