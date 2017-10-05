---
title: "Учебник. Интеграция Azure Active Directory с Igloo Software | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и Igloo Software."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2eb625c1-d3fc-4ae1-a304-6a6733a10e6e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: ab3891e11eb33b4d233e4fc967a40c7df06e4f4e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-igloo-software"></a><span data-ttu-id="dc0df-103">Учебник. Интеграция Azure Active Directory с Igloo Software</span><span class="sxs-lookup"><span data-stu-id="dc0df-103">Tutorial: Azure Active Directory integration with Igloo Software</span></span>

<span data-ttu-id="dc0df-104">В этом руководстве описано, как интегрировать Igloo Software с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="dc0df-104">In this tutorial, you learn how to integrate Igloo Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="dc0df-105">Интеграция Igloo Software с Azure AD обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="dc0df-105">Integrating Igloo Software with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="dc0df-106">С помощью Azure AD вы можете контролировать доступ к Igloo Software.</span><span class="sxs-lookup"><span data-stu-id="dc0df-106">You can control in Azure AD who has access to Igloo Software</span></span>
- <span data-ttu-id="dc0df-107">Вы можете включить автоматический вход пользователей в Igloo Software (единый вход) под учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dc0df-107">You can enable your users to automatically get signed-on to Igloo Software (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="dc0df-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="dc0df-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="dc0df-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="dc0df-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dc0df-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="dc0df-110">Prerequisites</span></span>

<span data-ttu-id="dc0df-111">Чтобы настроить интеграцию Azure AD с Igloo Software, вам потребуется следующее:</span><span class="sxs-lookup"><span data-stu-id="dc0df-111">To configure Azure AD integration with Igloo Software, you need the following items:</span></span>

- <span data-ttu-id="dc0df-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="dc0df-112">An Azure AD subscription</span></span>
- <span data-ttu-id="dc0df-113">подписка Igloo Software с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="dc0df-113">An Igloo Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="dc0df-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="dc0df-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="dc0df-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="dc0df-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="dc0df-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="dc0df-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="dc0df-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="dc0df-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="dc0df-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="dc0df-118">Scenario description</span></span>
<span data-ttu-id="dc0df-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="dc0df-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="dc0df-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="dc0df-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="dc0df-121">Добавление Igloo Software из коллекции</span><span class="sxs-lookup"><span data-stu-id="dc0df-121">Adding Igloo Software from the gallery</span></span>
2. <span data-ttu-id="dc0df-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="dc0df-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-igloo-software-from-the-gallery"></a><span data-ttu-id="dc0df-123">Добавление Igloo Software из коллекции</span><span class="sxs-lookup"><span data-stu-id="dc0df-123">Adding Igloo Software from the gallery</span></span>
<span data-ttu-id="dc0df-124">Чтобы настроить интеграцию Igloo Software с Azure AD, вам потребуется добавить Igloo Software из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="dc0df-124">To configure the integration of Igloo Software into Azure AD, you need to add Igloo Software from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="dc0df-125">**Чтобы добавить Igloo Software из коллекции, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="dc0df-125">**To add Igloo Software from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="dc0df-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="dc0df-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="dc0df-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="dc0df-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="dc0df-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="dc0df-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="dc0df-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="dc0df-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="dc0df-133">В поле поиска введите **Igloo Software**.</span><span class="sxs-lookup"><span data-stu-id="dc0df-133">In the search box, type **Igloo Software**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_search.png)

5. <span data-ttu-id="dc0df-135">В области результатов выберите **Igloo Software** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="dc0df-135">In the results panel, select **Igloo Software**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="dc0df-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="dc0df-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="dc0df-138">В этом разделе описана настройка и проверка единого входа Azure AD в Igloo Software для тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dc0df-138">In this section, you configure and test Azure AD single sign-on with Igloo Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="dc0df-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Igloo Software соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dc0df-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Igloo Software is to a user in Azure AD.</span></span> <span data-ttu-id="dc0df-140">Иными словами, необходимо установить связь между пользователям Azure AD и соответствующим пользователем в Igloo Software.</span><span class="sxs-lookup"><span data-stu-id="dc0df-140">In other words, a link relationship between an Azure AD user and the related user in Igloo Software needs to be established.</span></span>

<span data-ttu-id="dc0df-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Igloo Software.</span><span class="sxs-lookup"><span data-stu-id="dc0df-141">In Igloo Software, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="dc0df-142">Чтобы настроить и проверить единый вход в Azure AD в Igloo Software, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="dc0df-142">To configure and test Azure AD single sign-on with Igloo Software, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="dc0df-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="dc0df-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="dc0df-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dc0df-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="dc0df-145">**[Создание тестового пользователя Igloo Software](#creating-an-igloo-software-test-user)** требуется для создания дублирующего Britta Simon пользователя в Igloo Software, связанного с представлением этого пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dc0df-145">**[Creating an Igloo Software test user](#creating-an-igloo-software-test-user)** - to have a counterpart of Britta Simon in Igloo Software that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="dc0df-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dc0df-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="dc0df-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="dc0df-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="dc0df-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="dc0df-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="dc0df-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Igloo Software.</span><span class="sxs-lookup"><span data-stu-id="dc0df-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Igloo Software application.</span></span>

<span data-ttu-id="dc0df-150">**Чтобы настроить единый вход в Azure AD для Igloo Software, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="dc0df-150">**To configure Azure AD single sign-on with Igloo Software, perform the following steps:**</span></span>

1. <span data-ttu-id="dc0df-151">На портале Azure на странице интеграции с приложением **Igloo Software** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="dc0df-151">In the Azure portal, on the **Igloo Software** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="dc0df-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="dc0df-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_samlbase.png)

3. <span data-ttu-id="dc0df-155">В разделе **Домены и URL-адреса Igloo Software** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="dc0df-155">On the **Igloo Software Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_url.png)
    
    <span data-ttu-id="dc0df-157">а.</span><span class="sxs-lookup"><span data-stu-id="dc0df-157">a.</span></span> <span data-ttu-id="dc0df-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<company name>.igloocommmunities.com`</span><span class="sxs-lookup"><span data-stu-id="dc0df-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.igloocommmunities.com`</span></span>

    <span data-ttu-id="dc0df-159">b.</span><span class="sxs-lookup"><span data-stu-id="dc0df-159">b.</span></span> <span data-ttu-id="dc0df-160">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<company name>.igloocommmunities.com/saml.digest`</span><span class="sxs-lookup"><span data-stu-id="dc0df-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<company name>.igloocommmunities.com/saml.digest`</span></span>

    <span data-ttu-id="dc0df-161">c.</span><span class="sxs-lookup"><span data-stu-id="dc0df-161">c.</span></span> <span data-ttu-id="dc0df-162">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате: `https://<company name>.igloocommmunities.com/saml.digest`.</span><span class="sxs-lookup"><span data-stu-id="dc0df-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.igloocommmunities.com/saml.digest`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="dc0df-163">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="dc0df-163">These values are not real.</span></span> <span data-ttu-id="dc0df-164">Замените их фактическими значениями идентификатора, URL-адреса ответа и URL-адреса входа.</span><span class="sxs-lookup"><span data-stu-id="dc0df-164">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="dc0df-165">Чтобы получить эти значения, обратитесь в [службу поддержки клиентов Igloo Software](https://www.igloosoftware.com/services/support).</span><span class="sxs-lookup"><span data-stu-id="dc0df-165">Contact [Igloo Software Client support team](https://www.igloosoftware.com/services/support) to get these values.</span></span> 

4. <span data-ttu-id="dc0df-166">В разделе **Сертификат подписи SAML** щелкните **Сертификат (Base64)**, а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="dc0df-166">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_certificate.png) 

5. <span data-ttu-id="dc0df-168">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="dc0df-168">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-igloo-software-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="dc0df-170">В разделе **Настройка Igloo Software** щелкните **Настроить Igloo Software**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="dc0df-170">On the **Igloo Software Configuration** section, click **Configure Igloo Software** to open **Configure sign-on** window.</span></span> <span data-ttu-id="dc0df-171">Скопируйте **URL-адрес выхода и URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="dc0df-171">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_configure.png) 

7. <span data-ttu-id="dc0df-173">В другом окне веб-браузера войдите на веб-сайт Igloo Software организации в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="dc0df-173">In a different web browser window, log in to your Igloo Software company site as an administrator.</span></span>

8. <span data-ttu-id="dc0df-174">Перейдите в раздел **Панель управления**.</span><span class="sxs-lookup"><span data-stu-id="dc0df-174">Go to the **Control Panel**.</span></span>
   
     <span data-ttu-id="dc0df-175">![Панель управления](./media/active-directory-saas-igloo-software-tutorial/ic799949.png "Панель управления")</span><span class="sxs-lookup"><span data-stu-id="dc0df-175">![Control Panel](./media/active-directory-saas-igloo-software-tutorial/ic799949.png "Control Panel")</span></span>

9. <span data-ttu-id="dc0df-176">На вкладке **Членство** щелкните **Параметры входа**.</span><span class="sxs-lookup"><span data-stu-id="dc0df-176">In the **Membership** tab, click **Sign In Settings**.</span></span>
   
    <span data-ttu-id="dc0df-177">![Параметры входа](./media/active-directory-saas-igloo-software-tutorial/ic783968.png "Параметры входа")</span><span class="sxs-lookup"><span data-stu-id="dc0df-177">![Sign in Settings](./media/active-directory-saas-igloo-software-tutorial/ic783968.png "Sign in Settings")</span></span>

10. <span data-ttu-id="dc0df-178">В разделе настройки SAML нажмите **Настройка проверки подлинности SAML**.</span><span class="sxs-lookup"><span data-stu-id="dc0df-178">In the SAML Configuration section, click **Configure SAML Authentication**.</span></span>
   
    <span data-ttu-id="dc0df-179">![Настройка SAML](./media/active-directory-saas-igloo-software-tutorial/ic783969.png "Настройка SAML")</span><span class="sxs-lookup"><span data-stu-id="dc0df-179">![SAML Configuration](./media/active-directory-saas-igloo-software-tutorial/ic783969.png "SAML Configuration")</span></span>
   
11. <span data-ttu-id="dc0df-180">В разделе **Общая конфигурация** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="dc0df-180">In the **General Configuration** section, perform the following steps:</span></span>
   
    <span data-ttu-id="dc0df-181">![Общая конфигурация](./media/active-directory-saas-igloo-software-tutorial/ic783970.png "Общая конфигурация")</span><span class="sxs-lookup"><span data-stu-id="dc0df-181">![General Configuration](./media/active-directory-saas-igloo-software-tutorial/ic783970.png "General Configuration")</span></span>

    <span data-ttu-id="dc0df-182">а.</span><span class="sxs-lookup"><span data-stu-id="dc0df-182">a.</span></span> <span data-ttu-id="dc0df-183">Придумайте имя для конфигурации и введите его в текстовое поле **Имя подключения** .</span><span class="sxs-lookup"><span data-stu-id="dc0df-183">In the **Connection Name** textbox, type a custom name for your configuration.</span></span>
   
    <span data-ttu-id="dc0df-184">b.</span><span class="sxs-lookup"><span data-stu-id="dc0df-184">b.</span></span> <span data-ttu-id="dc0df-185">В текстовое поле **URL-адрес входа поставщика удостоверений** вставьте значение **URL-адреса службы единого входа SAML**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="dc0df-185">In the **IdP Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="dc0df-186">c.</span><span class="sxs-lookup"><span data-stu-id="dc0df-186">c.</span></span> <span data-ttu-id="dc0df-187">В текстовое поле **URL-адрес выхода поставщика удостоверений** вставьте значение **URL-адреса выхода**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="dc0df-187">In the **IdP Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="dc0df-188">г)</span><span class="sxs-lookup"><span data-stu-id="dc0df-188">d.</span></span> <span data-ttu-id="dc0df-189">Для параметра **Тип HTTP запроса и ответа о выходе** укажите значение **POST**.</span><span class="sxs-lookup"><span data-stu-id="dc0df-189">Select **Logout Response and Request HTTP Type** as **POST**.</span></span>
   
    <span data-ttu-id="dc0df-190">д.</span><span class="sxs-lookup"><span data-stu-id="dc0df-190">e.</span></span> <span data-ttu-id="dc0df-191">Откройте в блокноте сертификат в кодировке **Base-64**, скачанный с портала Azure, скопируйте его в буфер обмена и вставьте в текстовое поле **Открытый сертификат**.</span><span class="sxs-lookup"><span data-stu-id="dc0df-191">Open your **base-64** encoded certificate in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **Public Certificate** textbox.</span></span>
    
12. <span data-ttu-id="dc0df-192">В области **Конфигурация ответа и проверки подлинности**выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="dc0df-192">In the **Response and Authentication Configuration**, perform the following steps:</span></span>
    
    <span data-ttu-id="dc0df-193">![Конфигурация ответа и проверки подлинности](./media/active-directory-saas-igloo-software-tutorial/IC783971.png "Конфигурация ответа и проверки подлинности")</span><span class="sxs-lookup"><span data-stu-id="dc0df-193">![Response and Authentication Configuration](./media/active-directory-saas-igloo-software-tutorial/IC783971.png "Response and Authentication Configuration")</span></span>
  
      <span data-ttu-id="dc0df-194">а.</span><span class="sxs-lookup"><span data-stu-id="dc0df-194">a.</span></span> <span data-ttu-id="dc0df-195">Выберите для параметра **Поставщик удостоверений** значение **Microsoft ADFS**.</span><span class="sxs-lookup"><span data-stu-id="dc0df-195">As **Identity Provider**, select **Microsoft ADFS**.</span></span>
      
      <span data-ttu-id="dc0df-196">b.</span><span class="sxs-lookup"><span data-stu-id="dc0df-196">b.</span></span> <span data-ttu-id="dc0df-197">Выберите для параметра **Тип идентификатора** значение **Адрес электронной почты**.</span><span class="sxs-lookup"><span data-stu-id="dc0df-197">As **Identifier Type**, select **Email Address**.</span></span> 

      <span data-ttu-id="dc0df-198">c.</span><span class="sxs-lookup"><span data-stu-id="dc0df-198">c.</span></span> <span data-ttu-id="dc0df-199">В текстовом поле **Email Attribute** (Атрибут электронной почты) введите значение **emailaddress**.</span><span class="sxs-lookup"><span data-stu-id="dc0df-199">In the **Email Attribute** textbox, type **emailaddress**.</span></span>

      <span data-ttu-id="dc0df-200">г)</span><span class="sxs-lookup"><span data-stu-id="dc0df-200">d.</span></span> <span data-ttu-id="dc0df-201">В текстовое поле **Атрибут имени** введите значение **givenname**.</span><span class="sxs-lookup"><span data-stu-id="dc0df-201">In the **First Name Attribute** textbox, type **givenname**.</span></span>

      <span data-ttu-id="dc0df-202">д.</span><span class="sxs-lookup"><span data-stu-id="dc0df-202">e.</span></span> <span data-ttu-id="dc0df-203">В текстовое поле **Атрибут фамилии** введите значение **surname**.</span><span class="sxs-lookup"><span data-stu-id="dc0df-203">In the **Last Name Attribute** textbox, type **surname**.</span></span>

13. <span data-ttu-id="dc0df-204">Выполните следующие действия для завершения настройки:</span><span class="sxs-lookup"><span data-stu-id="dc0df-204">Perform the following steps to complete the configuration:</span></span>
    
    <span data-ttu-id="dc0df-205">![Создание пользователя при входе](./media/active-directory-saas-igloo-software-tutorial/IC783972.png "Создание пользователя при входе")</span><span class="sxs-lookup"><span data-stu-id="dc0df-205">![User creation on Sign in](./media/active-directory-saas-igloo-software-tutorial/IC783972.png "User creation on Sign in")</span></span> 

     <span data-ttu-id="dc0df-206">а.</span><span class="sxs-lookup"><span data-stu-id="dc0df-206">a.</span></span> <span data-ttu-id="dc0df-207">Выберите для параметра **Создание пользователя при входе** значение **Создать нового пользователя на веб-сайте при входе**.</span><span class="sxs-lookup"><span data-stu-id="dc0df-207">As **User creation on Sign in**, select **Create a new user in your site when they sign in**.</span></span>

     <span data-ttu-id="dc0df-208">b.</span><span class="sxs-lookup"><span data-stu-id="dc0df-208">b.</span></span> <span data-ttu-id="dc0df-209">Выберите для параметра **Параметры входа** значение **Использовать кнопку SAML на экране входа**.</span><span class="sxs-lookup"><span data-stu-id="dc0df-209">As **Sign in Settings**, select **Use SAML button on “Sign in” screen**.</span></span>

     <span data-ttu-id="dc0df-210">c.</span><span class="sxs-lookup"><span data-stu-id="dc0df-210">c.</span></span> <span data-ttu-id="dc0df-211">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="dc0df-211">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="dc0df-212">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="dc0df-212">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="dc0df-213">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="dc0df-213">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="dc0df-214">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="dc0df-214">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="dc0df-215">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="dc0df-215">Creating an Azure AD test user</span></span>
<span data-ttu-id="dc0df-216">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dc0df-216">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="dc0df-218">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="dc0df-218">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="dc0df-219">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="dc0df-219">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="dc0df-221">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="dc0df-221">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="dc0df-223">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="dc0df-223">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="dc0df-225">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="dc0df-225">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-igloo-software-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="dc0df-227">а.</span><span class="sxs-lookup"><span data-stu-id="dc0df-227">a.</span></span> <span data-ttu-id="dc0df-228">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="dc0df-228">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="dc0df-229">b.</span><span class="sxs-lookup"><span data-stu-id="dc0df-229">b.</span></span> <span data-ttu-id="dc0df-230">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="dc0df-230">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="dc0df-231">c.</span><span class="sxs-lookup"><span data-stu-id="dc0df-231">c.</span></span> <span data-ttu-id="dc0df-232">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="dc0df-232">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="dc0df-233">d.</span><span class="sxs-lookup"><span data-stu-id="dc0df-233">d.</span></span> <span data-ttu-id="dc0df-234">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="dc0df-234">Click **Create**.</span></span>
 
### <a name="creating-an-igloo-software-test-user"></a><span data-ttu-id="dc0df-235">Создание тестового пользователя Igloo Software</span><span class="sxs-lookup"><span data-stu-id="dc0df-235">Creating an Igloo Software test user</span></span>

<span data-ttu-id="dc0df-236">Элемент действия для настройки подготовки пользователей в Igloo Software отсутствует.</span><span class="sxs-lookup"><span data-stu-id="dc0df-236">There is no action item for you to configure user provisioning to Igloo Software.</span></span>  

<span data-ttu-id="dc0df-237">Когда назначенный пользователь пытается войти в Igloo Software с помощью панели доступа, Igloo Software проверяет, существует ли данный пользователь.</span><span class="sxs-lookup"><span data-stu-id="dc0df-237">When an assigned user tries to log in to Igloo Software using the access panel, Igloo Software checks whether the user exists.</span></span>  <span data-ttu-id="dc0df-238">Если учетная запись пользователя отсутствует, Igloo Software автоматически создает ее.</span><span class="sxs-lookup"><span data-stu-id="dc0df-238">If there is no user account available yet, it is automatically created by Igloo Software.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="dc0df-239">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="dc0df-239">Assigning the Azure AD test user</span></span>

<span data-ttu-id="dc0df-240">В этом разделе описано, как включить единый вход Azure для пользователя Britta Simon и предоставить этому пользователю доступ к Igloo Software.</span><span class="sxs-lookup"><span data-stu-id="dc0df-240">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Igloo Software.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="dc0df-242">**Чтобы назначить Britta Simon для Igloo Software, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="dc0df-242">**To assign Britta Simon to Igloo Software, perform the following steps:**</span></span>

1. <span data-ttu-id="dc0df-243">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="dc0df-243">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="dc0df-245">В списке приложений выберите **Igloo Software**.</span><span class="sxs-lookup"><span data-stu-id="dc0df-245">In the applications list, select **Igloo Software**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-igloo-software-tutorial/tutorial_igloosoftware_app.png) 

3. <span data-ttu-id="dc0df-247">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="dc0df-247">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="dc0df-249">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="dc0df-249">Click **Add** button.</span></span> <span data-ttu-id="dc0df-250">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="dc0df-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="dc0df-252">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="dc0df-252">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="dc0df-253">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="dc0df-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="dc0df-254">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="dc0df-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="dc0df-255">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="dc0df-255">Testing single sign-on</span></span>

<span data-ttu-id="dc0df-256">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="dc0df-256">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="dc0df-257">Щелкнув элемент Igloo Software на панели доступа, вы автоматически войдете в приложение Igloo Software.</span><span class="sxs-lookup"><span data-stu-id="dc0df-257">When you click the Igloo Software tile in the Access Panel, you should get automatically signed-on to your Igloo Software application.</span></span>
<span data-ttu-id="dc0df-258">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="dc0df-258">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="dc0df-259">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="dc0df-259">Additional resources</span></span>

* [<span data-ttu-id="dc0df-260">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dc0df-260">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="dc0df-261">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="dc0df-261">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-igloo-software-tutorial/tutorial_general_203.png

