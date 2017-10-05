---
title: "Учебник. Интеграция Azure Active Directory с ClickTime | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и ClickTime."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d437b5ab-4d71-4c13-96d0-79018cebbbd4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: jeedes
ms.openlocfilehash: 0e0123a40d52dfd7a2e29c29cb2239e979089ca9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-clicktime"></a><span data-ttu-id="0d0ae-103">Руководство. Интеграция Azure Active Directory с ClickTime</span><span class="sxs-lookup"><span data-stu-id="0d0ae-103">Tutorial: Azure Active Directory integration with ClickTime</span></span>

<span data-ttu-id="0d0ae-104">В этом руководстве описано, как интегрировать ClickTime с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0d0ae-104">In this tutorial, you learn how to integrate ClickTime with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0d0ae-105">Интеграция ClickTime с Azure AD обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-105">Integrating ClickTime with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0d0ae-106">С помощью Azure AD вы можете контролировать доступ к ClickTime.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-106">You can control in Azure AD who has access to ClickTime</span></span>
- <span data-ttu-id="0d0ae-107">Вы можете включить автоматический вход пользователей в ClickTime (единый вход) под учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-107">You can enable your users to automatically get signed-on to ClickTime (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0d0ae-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="0d0ae-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0d0ae-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0d0ae-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="0d0ae-110">Prerequisites</span></span>

<span data-ttu-id="0d0ae-111">Чтобы настроить интеграцию Azure AD с ClickTime, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="0d0ae-111">To configure Azure AD integration with ClickTime, you need the following items:</span></span>

- <span data-ttu-id="0d0ae-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="0d0ae-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0d0ae-113">подписка ClickTime с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-113">A ClickTime single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0d0ae-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0d0ae-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="0d0ae-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0d0ae-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0d0ae-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0d0ae-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0d0ae-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="0d0ae-118">Scenario description</span></span>
<span data-ttu-id="0d0ae-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0d0ae-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="0d0ae-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0d0ae-121">Добавление ClickTime из коллекции.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-121">Adding ClickTime from the gallery</span></span>
2. <span data-ttu-id="0d0ae-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="0d0ae-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-clicktime-from-the-gallery"></a><span data-ttu-id="0d0ae-123">Добавление ClickTime из коллекции.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-123">Adding ClickTime from the gallery</span></span>
<span data-ttu-id="0d0ae-124">Чтобы настроить интеграцию ClickTime с Azure AD, необходимо добавить ClickTime из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-124">To configure the integration of ClickTime into Azure AD, you need to add ClickTime from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0d0ae-125">**Чтобы добавить ClickTime из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="0d0ae-125">**To add ClickTime from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="0d0ae-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка "Azure Active Directory"][1]

2. <span data-ttu-id="0d0ae-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="0d0ae-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-129">Then go to **All applications**.</span></span>

    ![Колонка "Корпоративные приложения"][2]
    
3. <span data-ttu-id="0d0ae-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Кнопка "Новое приложение"][3]

4. <span data-ttu-id="0d0ae-133">В поле поиска введите **ClickTime**, выберите **ClickTime** на панели результатов и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-133">In the search box, type **ClickTime**, select **ClickTime** from result panel then click **Add** button to add the application.</span></span>

    ![ClickTime в списке результатов](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="0d0ae-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="0d0ae-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="0d0ae-136">В этом разделе описана настройка и проверка единого входа Azure AD в ClickTime с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-136">In this section, you configure and test Azure AD single sign-on with ClickTime based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0d0ae-137">Для работы единого входа Azure AD необходимо знать, какой пользователь в ClickTime соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-137">For single sign-on to work, Azure AD needs to know what the counterpart user in ClickTime is to a user in Azure AD.</span></span> <span data-ttu-id="0d0ae-138">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в ClickTime.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-138">In other words, a link relationship between an Azure AD user and the related user in ClickTime needs to be established.</span></span>

<span data-ttu-id="0d0ae-139">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в ClickTime.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-139">In ClickTime, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="0d0ae-140">Чтобы настроить и проверить единый вход Azure AD в ClickTime, вам потребуется выполнить действия в указанных далее стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-140">To configure and test Azure AD single sign-on with ClickTime, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0d0ae-141">**[Настройка единого входа Azure AD](#configure-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="0d0ae-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0d0ae-143">**[Создание тестового пользователя ClickTime](#create-a-clicktime-test-user)** требуется для создания в ClickTime пользователя Britta Simon, связанного с соответствующим представлением в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-143">**[Create a ClickTime test user](#create-a-clicktime-test-user)** - to have a counterpart of Britta Simon in ClickTime that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="0d0ae-144">**[Назначение тестового пользователя Azure AD](#assign-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0d0ae-145">**[Проверка единого входа](#test-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="0d0ae-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="0d0ae-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="0d0ae-147">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении ClickTime.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ClickTime application.</span></span>

<span data-ttu-id="0d0ae-148">**Чтобы настроить единый вход Azure AD в ClickTime, сделайте следующее.**</span><span class="sxs-lookup"><span data-stu-id="0d0ae-148">**To configure Azure AD single sign-on with ClickTime, perform the following steps:**</span></span>

1. <span data-ttu-id="0d0ae-149">На портале Azure на странице интеграции с приложением **ClickTime** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-149">In the Azure portal, on the **ClickTime** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="0d0ae-151">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_samlbase.png)

3. <span data-ttu-id="0d0ae-153">В разделе **Домены и URL-адреса приложения ClickTime** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="0d0ae-153">On the **ClickTime Domain and URLs** section, perform the following steps:</span></span>

    ![Сведения о домене и URL-адресах единого входа приложения ClickTime](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_url.png)

    <span data-ttu-id="0d0ae-155">а.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-155">a.</span></span> <span data-ttu-id="0d0ae-156">В текстовом поле **Идентификатор** введите URL-адрес в формате `https://app.clicktime.com/sp/`.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-156">In the **Identifier** textbox, type a URL as: `https://app.clicktime.com/sp/`</span></span>
    
    <span data-ttu-id="0d0ae-157">b.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-157">b.</span></span> <span data-ttu-id="0d0ae-158">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="0d0ae-158">In the **Reply URL** textbox, type a URL using the following patterns:</span></span> 

    | |
    |--|
    | `https://app.clicktime.com/Login/` |
    | `https://app.clicktime.com/App/Login/Consume.aspx` |

4. <span data-ttu-id="0d0ae-159">В разделе **Сертификат подписи SAML** щелкните **Сертификат (Base64)**, а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-159">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Ссылка для скачивания сертификата](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_certificate.png) 

5. <span data-ttu-id="0d0ae-161">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="0d0ae-161">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-clicktime-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="0d0ae-163">В разделе **Конфигурация ClickTime** щелкните **Настроить ClickTime**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-163">On the **ClickTime Configuration** section, click **Configure ClickTime** to open **Configure sign-on** window.</span></span> <span data-ttu-id="0d0ae-164">Скопируйте **URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-164">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка ClickTime](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_configure.png) 

7. <span data-ttu-id="0d0ae-166">В другом окне веб-браузера войдите на свой корпоративный веб-сайт ClickTime в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-166">In a different web browser window, log into your ClickTime company site as an administrator.</span></span>

8. <span data-ttu-id="0d0ae-167">На панели инструментов в верхней части экрана щелкните **Preferences** (Параметры) и выберите **Security Settings** (Параметры безопасности).</span><span class="sxs-lookup"><span data-stu-id="0d0ae-167">In the toolbar on the top, click **Preferences**, and then click **Security Settings**.</span></span>

9. <span data-ttu-id="0d0ae-168">В разделе **Настройки единого входа** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-168">In the **Single Sign-On Preferences** configuration section, perform the following steps:</span></span>
   
    <span data-ttu-id="0d0ae-169">![Параметры безопасности](./media/active-directory-saas-clicktime-tutorial/tic777280.png "Параметры безопасности")</span><span class="sxs-lookup"><span data-stu-id="0d0ae-169">![Security Settings](./media/active-directory-saas-clicktime-tutorial/tic777280.png "Security Settings")</span></span>
   
    <span data-ttu-id="0d0ae-170">а.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-170">a.</span></span>  <span data-ttu-id="0d0ae-171">Выберите "**Allow** sign-in using Single Sign-On (SSO) with **Azure AD**" (Разрешить единый вход (SSO) с помощью Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0d0ae-171">Select **Allow** sign-in using Single Sign-On (SSO) with **Azure AD**.</span></span>
   
    <span data-ttu-id="0d0ae-172">b.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-172">b.</span></span> <span data-ttu-id="0d0ae-173">В текстовое поле **Identity Provider Endpoint** (Конечная точка входа поставщика удостоверений) вставьте значение **URL-адрес службы единого входа SAML**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-173">In the **Identity Provider Endpoint** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="0d0ae-174">c.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-174">c.</span></span>  <span data-ttu-id="0d0ae-175">Откройте в **Блокноте** скачанный с портала Azure**сертификат в кодировке Base-64**, скопируйте его содержимое, а затем вставьте его в текстовое поле **X.509 Certificate** (Сертификат X.509).</span><span class="sxs-lookup"><span data-stu-id="0d0ae-175">Open the **base-64 encoded certificate** downloaded from Azure portal in **Notepad**, copy the content, and then paste it into the **X.509 Certificate** textbox.</span></span>
   
    <span data-ttu-id="0d0ae-176">d.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-176">d.</span></span>  <span data-ttu-id="0d0ae-177">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-177">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="0d0ae-178">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-178">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="0d0ae-179">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-179">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="0d0ae-180">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="0d0ae-180">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="0d0ae-181">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="0d0ae-181">Create an Azure AD test user</span></span>
<span data-ttu-id="0d0ae-182">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-182">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="0d0ae-184">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="0d0ae-184">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0d0ae-185">На портале Azure в области слева нажмите кнопку **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-185">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Кнопка "Azure Active Directory"](./media/active-directory-saas-clicktime-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0d0ae-187">Чтобы открыть список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-187">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>
    
    ![Ссылки "Пользователи и группы" и "Все пользователи"](./media/active-directory-saas-clicktime-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0d0ae-189">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна **Все пользователи** щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-189">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>
 
    ![Кнопка "Добавить"](./media/active-directory-saas-clicktime-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0d0ae-191">В диалоговом окне **Пользователь** сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-191">In the **User** dialog box, perform the following steps:</span></span>
 
    ![Диалоговое окно "Пользователь"](./media/active-directory-saas-clicktime-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0d0ae-193">а.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-193">a.</span></span> <span data-ttu-id="0d0ae-194">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-194">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0d0ae-195">b.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-195">b.</span></span> <span data-ttu-id="0d0ae-196">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-196">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0d0ae-197">c.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-197">c.</span></span> <span data-ttu-id="0d0ae-198">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-198">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="0d0ae-199">d.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-199">d.</span></span> <span data-ttu-id="0d0ae-200">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-200">Click **Create**.</span></span>
 
### <a name="create-a-clicktime-test-user"></a><span data-ttu-id="0d0ae-201">Создание тестового пользователя ClickTime</span><span class="sxs-lookup"><span data-stu-id="0d0ae-201">Create a ClickTime test user</span></span>

<span data-ttu-id="0d0ae-202">Чтобы пользователи Azure AD могли выполнить вход в ClickTime, они должны быть подготовлены для ClickTime.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-202">In order to enable Azure AD users to log into ClickTime, they must be provisioned into ClickTime.</span></span>  
<span data-ttu-id="0d0ae-203">В случае с ClickTime подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-203">In the case of ClickTime, provisioning is a manual task.</span></span>

> [!NOTE]
> <span data-ttu-id="0d0ae-204">Вы можете использовать любые другие инструменты создания учетной записи пользователя ClickTime или API, предоставляемые ClickTime для подготовки учетных записей пользователя Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-204">You can use any other ClickTime user account creation tools or APIs provided by ClickTime to provision Azure AD user accounts.</span></span>

<span data-ttu-id="0d0ae-205">**Чтобы подготовить учетную запись пользователя, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="0d0ae-205">**To provision a user account, perform the following steps:**</span></span>
1. <span data-ttu-id="0d0ae-206">Войдите в клиент **ClickTime** .</span><span class="sxs-lookup"><span data-stu-id="0d0ae-206">Log in to your **ClickTime** tenant.</span></span>
2. <span data-ttu-id="0d0ae-207">На панели инструментов в верхней части экрана щелкните **Company** (Компания), а затем — **People** (Пользователи).</span><span class="sxs-lookup"><span data-stu-id="0d0ae-207">In the toolbar on the top, click **Company**, and then click **People**.</span></span>
   
    <span data-ttu-id="0d0ae-208">![Люди](./media/active-directory-saas-clicktime-tutorial/tic777282.png "Люди")</span><span class="sxs-lookup"><span data-stu-id="0d0ae-208">![People](./media/active-directory-saas-clicktime-tutorial/tic777282.png "People")</span></span>
3. <span data-ttu-id="0d0ae-209">Нажмите кнопку **Добавить пользователя**.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-209">Click **Add Person**.</span></span>
   
    <span data-ttu-id="0d0ae-210">![Добавление пользователя](./media/active-directory-saas-clicktime-tutorial/tic777283.png "Добавление пользователя")</span><span class="sxs-lookup"><span data-stu-id="0d0ae-210">![Add Person](./media/active-directory-saas-clicktime-tutorial/tic777283.png "Add Person")</span></span>
4. <span data-ttu-id="0d0ae-211">В разделе "Новый пользователь" выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-211">In the New Person section, perform the following steps:</span></span>
   
    <span data-ttu-id="0d0ae-212">![Люди](./media/active-directory-saas-clicktime-tutorial/tic777284.png "Люди")</span><span class="sxs-lookup"><span data-stu-id="0d0ae-212">![People](./media/active-directory-saas-clicktime-tutorial/tic777284.png "People")</span></span>
   
    <span data-ttu-id="0d0ae-213">а.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-213">a.</span></span>  <span data-ttu-id="0d0ae-214">В текстовом поле **Full Name** (Полное имя) введите полное имя пользователя, например **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-214">In the **full name** textbox, type full name of user like **Britta Simon**.</span></span> 
  
    <span data-ttu-id="0d0ae-215">b.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-215">b.</span></span>  <span data-ttu-id="0d0ae-216">В текстовом поле **Email address** (Электронная почта) введите адрес электронной почты пользователя, например **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-216">In the **email address** textbox, type the email of user like **brittasimon@contoso.com**.</span></span>
       
    > [!NOTE]
    > <span data-ttu-id="0d0ae-217">При необходимости задайте для нового пользователя дополнительные свойства.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-217">If you want to, you can set additional properties of the new person object.</span></span>
   
    <span data-ttu-id="0d0ae-218">c.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-218">c.</span></span>  <span data-ttu-id="0d0ae-219">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-219">Click **Save**.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="0d0ae-220">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="0d0ae-220">Assign the Azure AD test user</span></span>

<span data-ttu-id="0d0ae-221">В этом разделе описано, как позволить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к ClickTime.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-221">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ClickTime.</span></span>

![Назначение роли пользователя][200] 

<span data-ttu-id="0d0ae-223">**Чтобы назначить пользователя Britta Simon в ClickTime, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="0d0ae-223">**To assign Britta Simon to ClickTime, perform the following steps:**</span></span>

1. <span data-ttu-id="0d0ae-224">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-224">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="0d0ae-226">В списке приложений выберите **ClickTime**.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-226">In the applications list, select **ClickTime**.</span></span>

    ![Ссылка на ClickTime в списке "Приложения"](./media/active-directory-saas-clicktime-tutorial/tutorial_clicktime_app.png) 

3. <span data-ttu-id="0d0ae-228">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-228">In the menu on the left, click **Users and groups**.</span></span>

    ![Ссылка "Пользователи и группы"][202] 

4. <span data-ttu-id="0d0ae-230">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-230">Click **Add** button.</span></span> <span data-ttu-id="0d0ae-231">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Область "Добавление назначения"][203]

5. <span data-ttu-id="0d0ae-233">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="0d0ae-234">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0d0ae-235">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="0d0ae-236">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="0d0ae-236">Test single sign-on</span></span>

<span data-ttu-id="0d0ae-237">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-237">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="0d0ae-238">Щелкнув плитку ClickTime на панели доступа, вы автоматически войдете в приложение ClickTime.</span><span class="sxs-lookup"><span data-stu-id="0d0ae-238">When you click the ClickTime tile in the Access Panel, you should get automatically signed-on to your ClickTime application.</span></span>
<span data-ttu-id="0d0ae-239">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0d0ae-239">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0d0ae-240">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="0d0ae-240">Additional resources</span></span>

* [<span data-ttu-id="0d0ae-241">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0d0ae-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0d0ae-242">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0d0ae-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-clicktime-tutorial/tutorial_general_203.png

