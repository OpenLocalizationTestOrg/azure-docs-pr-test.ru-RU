---
title: "Руководство по интеграции Azure Active Directory с Cezanne HR Software | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в Cezanne HR Software."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: fb8f95bf-c3c1-4e1f-b2b3-3b67526be72d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 623c438edfce5f98c2d32d8bb25a97d86aa77909
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-integrate-azure-active-directory-with-cezanne-hr-software"></a><span data-ttu-id="fd026-103">Руководство по интеграции Azure Active Directory с Cezanne HR Software</span><span class="sxs-lookup"><span data-stu-id="fd026-103">Tutorial: Integrate Azure Active Directory with Cezanne HR software</span></span>

<span data-ttu-id="fd026-104">В этом руководстве описано, как интегрировать Cezanne HR Software с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fd026-104">In this tutorial, you learn how to integrate Cezanne HR software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fd026-105">Интеграция Cezanne HR Software с Azure AD обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="fd026-105">Integrating Cezanne HR software with Azure AD provides you with the following benefits.</span></span> <span data-ttu-id="fd026-106">Вы можете:</span><span class="sxs-lookup"><span data-stu-id="fd026-106">You can:</span></span>

- <span data-ttu-id="fd026-107">С помощью Azure AD можно контролировать доступ к Cezanne HR Software.</span><span class="sxs-lookup"><span data-stu-id="fd026-107">Control in Azure AD who has access to Cezanne HR software.</span></span>
- <span data-ttu-id="fd026-108">Вы можете включить автоматический вход пользователей в Cezanne HR Software (единый вход) с использованием учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fd026-108">Enable your users to automatically sign in to Cezanne HR software with single sign-on (SSO) with their Azure AD accounts.</span></span>
- <span data-ttu-id="fd026-109">Централизованное управление учетными записями через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="fd026-109">Manage your accounts in one central location: the Azure portal.</span></span>

<span data-ttu-id="fd026-110">Чтобы узнать больше об интеграции приложений SaaS с Azure AD, прочитайте статью [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="fd026-110">To learn more about software as a service (SaaS) app integration with Azure AD, see [What is application access and SSO with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fd026-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="fd026-111">Prerequisites</span></span>

<span data-ttu-id="fd026-112">Чтобы настроить интеграцию Azure AD с Cezanne HR Software, вам потребуется следующее:</span><span class="sxs-lookup"><span data-stu-id="fd026-112">To configure Azure AD integration with Cezanne HR software, you need the following items:</span></span>

- <span data-ttu-id="fd026-113">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="fd026-113">An Azure AD subscription</span></span>
- <span data-ttu-id="fd026-114">подписка Cezanne HR Software с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="fd026-114">A Cezanne HR software SSO-enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fd026-115">Мы не рекомендуем использовать рабочую среду для тестирования действий, выполняемых в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="fd026-115">To test the steps in this tutorial, we recommend that you do not use a production environment.</span></span>

<span data-ttu-id="fd026-116">При проверке действий в этом руководстве соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="fd026-116">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="fd026-117">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="fd026-117">Don't use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fd026-118">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fd026-118">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fd026-119">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="fd026-119">Scenario description</span></span>
<span data-ttu-id="fd026-120">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="fd026-120">In this tutorial, you test Azure AD SSO in a test environment.</span></span> 

<span data-ttu-id="fd026-121">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="fd026-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

* <span data-ttu-id="fd026-122">Добавление Cezanne HR Software из коллекции.</span><span class="sxs-lookup"><span data-stu-id="fd026-122">Adding Cezanne HR software from the gallery</span></span>
* <span data-ttu-id="fd026-123">Настройка и проверка единого входа Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fd026-123">Configuring and testing Azure AD SSO</span></span>

## <a name="add-cezanne-hr-software-from-the-gallery"></a><span data-ttu-id="fd026-124">Добавление Cezanne HR Software из коллекции</span><span class="sxs-lookup"><span data-stu-id="fd026-124">Add Cezanne HR software from the gallery</span></span>
<span data-ttu-id="fd026-125">Чтобы настроить интеграцию Cezanne HR Software с Azure AD, добавьте Cezanne HR Software из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="fd026-125">To configure the integration of Cezanne HR software into Azure AD, add Cezanne HR software from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="fd026-126">Чтобы добавить Cezanne HR Software из коллекции, сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="fd026-126">To add Cezanne HR software from the gallery, do the following:</span></span>

1. <span data-ttu-id="fd026-127">На **[портале Azure](https://portal.azure.com)** в области слева нажмите кнопку **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fd026-127">In the **[Azure portal](https://portal.azure.com)**, in the left pane, select the **Azure Active Directory** button.</span></span> 

    ![Кнопка Azure Active Directory][1]

2. <span data-ttu-id="fd026-129">Щелкните **Корпоративные приложения** > **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="fd026-129">Select **Enterprise applications** > **All applications**.</span></span>

    ![Ссылка "Все приложения"][2]
    
3. <span data-ttu-id="fd026-131">Чтобы добавить новое приложение, в верхней части диалогового окна **Все приложения** нажмите кнопку **Новое приложение**.</span><span class="sxs-lookup"><span data-stu-id="fd026-131">To add a new application, at the top of the **All applications** dialog box, select **New application**.</span></span>

    ![Кнопка "Новое приложение"][3]

4. <span data-ttu-id="fd026-133">В поле поиска введите **Cezanne HR Software**.</span><span class="sxs-lookup"><span data-stu-id="fd026-133">In the search box, type **Cezanne HR Software**.</span></span>

    ![Поле поиска](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_search.png)

5. <span data-ttu-id="fd026-135">Из списка результатов выберите **Cezanne HR Software** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="fd026-135">In the results list, select **Cezanne HR Software** and then select the **Add** button to add the application.</span></span>

    ![Список результатов](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="fd026-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="fd026-137">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="fd026-138">В этом разделе описано, как настроить и проверить единый вход Azure AD в Cezanne HR Software с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fd026-138">In this section, you configure and test Azure AD SSO with Cezanne HR software based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="fd026-139">Чтобы единый вход работал, в Azure AD необходимо указать, какой пользователь в Cezanne HR Software соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fd026-139">For SSO to work, Azure AD needs to know the Cezanne HR software counterpart to the Azure AD user.</span></span> <span data-ttu-id="fd026-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Cezanne HR Software.</span><span class="sxs-lookup"><span data-stu-id="fd026-140">In other words, you must establish a link relationship between an Azure AD user and the related user in the Cezanne HR software.</span></span>

<span data-ttu-id="fd026-141">Чтобы установить эту связь, присвойте **имени пользователя** в Azure AD значение **имени пользователя** в Cezanne HR Software.</span><span class="sxs-lookup"><span data-stu-id="fd026-141">To establish the link relationship, assign the Cezanne HR software **user name** value as the Azure AD **Username** value.</span></span>

<span data-ttu-id="fd026-142">Чтобы настроить и проверить единый вход Azure AD в Cezanne HR Software, выполните действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="fd026-142">To configure and test Azure AD SSO by using Cezanne HR software, complete the following building blocks.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="fd026-143">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="fd026-143">Configure Azure AD SSO</span></span>

<span data-ttu-id="fd026-144">В этом разделе описывается, как включить единый вход Azure AD на портале Azure и настроить единый вход в приложении Cezanne HR Software. Для этого выполните следующее.</span><span class="sxs-lookup"><span data-stu-id="fd026-144">In this section, you can enable Azure AD SSO in the Azure portal and configure SSO in your Cezanne HR software application by doing the following:</span></span>

1. <span data-ttu-id="fd026-145">На портале Azure на странице интеграции с приложением **Cezanne HR Software** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="fd026-145">In the Azure portal, on the **Cezanne HR Software** application integration page, select **Single sign-on**.</span></span>

    ![Команда "Единый вход"][4]

2. <span data-ttu-id="fd026-147">В диалоговом окне **Единый вход** из списка **Режим** выберите значение **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="fd026-147">To enable SSO, in the **Single sign-on** dialog box, select the **Mode** as **SAML-based Sign-on**.</span></span>
 
    ![Поле "Режим"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_samlbase.png)

3. <span data-ttu-id="fd026-149">В разделе **Домены и URL-адреса приложения Cezanne HR Software** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="fd026-149">Under **Cezanne HR Software Domain and URLs**, do the following:</span></span>

    ![Раздел "Домены и URL-адреса приложения Cezanne HR Software"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_url.png)

    <span data-ttu-id="fd026-151">а.</span><span class="sxs-lookup"><span data-stu-id="fd026-151">a.</span></span> <span data-ttu-id="fd026-152">В поле **URL-адрес для входа** введите URL-адрес, используя следующий синтаксис: `https://w3.cezanneondemand.com/cezannehr/-/<tenant id>`.</span><span class="sxs-lookup"><span data-stu-id="fd026-152">In the **Sign-on URL** box, type a URL that has the following syntax: `https://w3.cezanneondemand.com/cezannehr/-/<tenant id>`</span></span>

    <span data-ttu-id="fd026-153">b.</span><span class="sxs-lookup"><span data-stu-id="fd026-153">b.</span></span> <span data-ttu-id="fd026-154">В поле **URL-адрес ответа** введите URL-адрес, используя следующий синтаксис: `https://w3.cezanneondemand.com:443/<tenantid>`.</span><span class="sxs-lookup"><span data-stu-id="fd026-154">In the **Reply URL** box, type a URL that has the following syntax: `https://w3.cezanneondemand.com:443/<tenantid>`</span></span>    
     
    > [!NOTE] 
    > <span data-ttu-id="fd026-155">Приведенные выше значения используются только для примера.</span><span class="sxs-lookup"><span data-stu-id="fd026-155">The preceding values are not real.</span></span> <span data-ttu-id="fd026-156">Замените их фактическими значениями URL-адреса ответа и URL-адреса входа.</span><span class="sxs-lookup"><span data-stu-id="fd026-156">Update them with the actual reply URL and the sign-on URL.</span></span> <span data-ttu-id="fd026-157">Чтобы получить эти значения, обратитесь к [группе поддержки клиентов Cezanne HR Software](mailto:info@cezannehr.com).</span><span class="sxs-lookup"><span data-stu-id="fd026-157">To obtain the values, contact the [Cezanne HR software client support team](mailto:info@cezannehr.com).</span></span>

4. <span data-ttu-id="fd026-158">В разделе **Сертификат подписи SAML** щелкните **Сертификат (Base64)** и сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="fd026-158">Under **SAML Signing Certificate**, select **Certificate (Base64)**, and then save the certificate file on your computer.</span></span>

    ![Раздел "Сертификат подписи SAML"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_certificate.png) 

5. <span data-ttu-id="fd026-160">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="fd026-160">Select **Save**.</span></span>

    ![Кнопка "Сохранить"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="fd026-162">В разделе **Конфигурация Cezanne HR Software** щелкните **Настроить Cezanne HR Software**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="fd026-162">Under **Cezanne HR Software Configuration**, select **Configure Cezanne HR Software** to open the **Configure sign-on** window.</span></span> <span data-ttu-id="fd026-163">Скопируйте **идентификатор сущности SAML** и **URL-адрес службы единого входа SAM**L из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="fd026-163">Copy the **SAML Entity ID** and **SAML Single Sign-On Service** URL from the **Quick Reference** section.</span></span>

    ![Раздел "Конфигурация Cezanne HR Software"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_configure.png) 

7. <span data-ttu-id="fd026-165">В другом окне веб-браузера войдите в свой клиент Cezanne HR Software в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="fd026-165">In a different web browser window, sign on to your Cezanne HR software tenant as an administrator.</span></span>

8. <span data-ttu-id="fd026-166">В левой области щелкните **System Setup** (Настройка системы).</span><span class="sxs-lookup"><span data-stu-id="fd026-166">In the left pane, select **System Setup**.</span></span> <span data-ttu-id="fd026-167">Выберите **Security Settings** > **Single Sign-On Configuration** ("Параметры безопасности" > "Конфигурация единого входа").</span><span class="sxs-lookup"><span data-stu-id="fd026-167">Select **Security Settings** > **Single Sign-On Configuration**.</span></span>

    ![Ссылка "Single Sign-On Configuration" (Конфигурация единого входа)](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_000.png)

9. <span data-ttu-id="fd026-169">В области **Allow users to log in using the following Single Sign-On (SSO) Service** (Разрешить пользователям вход с использованием следующей службы единого входа) установите флажок **SAML 2.0** и выберите параметр **Advanced Configuration** (Расширенная конфигурация).</span><span class="sxs-lookup"><span data-stu-id="fd026-169">In the **Allow users to log in using the following Single Sign-On (SSO) services** pane, select the **SAML 2.0** check box and select the **Advanced Configuration** option.</span></span>

    ![Параметры служб единого входа](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_001.png)

10. <span data-ttu-id="fd026-171">Нажмите кнопку **Add New** (Добавить).</span><span class="sxs-lookup"><span data-stu-id="fd026-171">Select **Add New**.</span></span>

    ![Кнопка "Add New" (Добавить)](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_002.png)

11. <span data-ttu-id="fd026-173">В разделе **SAML 2.0 Identity Providers** (Поставщики удостоверений SAML 2.0) выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="fd026-173">Under **SAML 2.0 Identity Providers**, do the following:</span></span>

    ![Раздел "SAML 2.0 Identity Providers" (Поставщики удостоверений SAML 2.0)](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_003.png)
    
    <span data-ttu-id="fd026-175">а.</span><span class="sxs-lookup"><span data-stu-id="fd026-175">a.</span></span> <span data-ttu-id="fd026-176">Введите имя поставщика удостоверений в поле **Display Name** (Отображаемое имя).</span><span class="sxs-lookup"><span data-stu-id="fd026-176">In the **Display Name** box, enter the name of your identity provider.</span></span>

    <span data-ttu-id="fd026-177">b.</span><span class="sxs-lookup"><span data-stu-id="fd026-177">b.</span></span> <span data-ttu-id="fd026-178">В поле **Entity Identifier** (Идентификатор сущности) вставьте **идентификатор сущности SAML**, скопированный на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="fd026-178">In the **Entity Identifier** box, paste the **SAML Entity ID** that you copied from the Azure portal.</span></span> 

    <span data-ttu-id="fd026-179">c.</span><span class="sxs-lookup"><span data-stu-id="fd026-179">c.</span></span> <span data-ttu-id="fd026-180">Из списка **SAML Binding** (Привязка SAML) выберите пункт **POST**.</span><span class="sxs-lookup"><span data-stu-id="fd026-180">In the **SAML Binding** list box, select **POST**.</span></span>

    <span data-ttu-id="fd026-181">d.</span><span class="sxs-lookup"><span data-stu-id="fd026-181">d.</span></span> <span data-ttu-id="fd026-182">Вставьте **URL-адрес службы единого входа SAML**, который вы скопировали на портале Azure, в поле **Security Token Service Endpoint** (Конечная точка службы токенов безопасности).</span><span class="sxs-lookup"><span data-stu-id="fd026-182">In the **Security Token Service Endpoint** box, paste the **SAML Single Sign-On Service** URL that you copied from the Azure portal.</span></span> 
    
    <span data-ttu-id="fd026-183">д.</span><span class="sxs-lookup"><span data-stu-id="fd026-183">e.</span></span> <span data-ttu-id="fd026-184">В текстовом поле **User ID Attribute Name** (Имя атрибута идентификатора пользователя) введите `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span><span class="sxs-lookup"><span data-stu-id="fd026-184">In the **User ID Attribute Name** box, enter `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name`.</span></span>
    
    <span data-ttu-id="fd026-185">f.</span><span class="sxs-lookup"><span data-stu-id="fd026-185">f.</span></span> <span data-ttu-id="fd026-186">Чтобы передать сертификат, скачанный с Azure AD, нажмите кнопку **Upload** (Передать).</span><span class="sxs-lookup"><span data-stu-id="fd026-186">To upload the downloaded certificate from Azure AD, select the **Upload** button.</span></span>
    
    <span data-ttu-id="fd026-187">g.</span><span class="sxs-lookup"><span data-stu-id="fd026-187">g.</span></span> <span data-ttu-id="fd026-188">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="fd026-188">Select **OK**.</span></span> 

12. <span data-ttu-id="fd026-189">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="fd026-189">Select **Save**.</span></span>

    ![Кнопка "Сохранить"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_004.png)

> [!TIP]
> <span data-ttu-id="fd026-191">Настроив приложение, вы можете прочитать краткую версию предыдущих инструкций на [портале Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fd026-191">As you set up the app, you can read a concise version of the preceding instructions in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="fd026-192">После добавления этого приложения из раздела **Active Directory** > **Корпоративные приложения** выберите вкладку **Единый вход**. Откройте встроенную документацию из раздела **Настройка**.</span><span class="sxs-lookup"><span data-stu-id="fd026-192">After you add the app from the **Active Directory** > **Enterprise applications** section, select the **Single sign-on** tab. Then access the embedded documentation from the **Configuration** section.</span></span> 

<span data-ttu-id="fd026-193">Чтобы узнать больше, ознакомьтесь со [встроенной документацией Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="fd026-193">To learn more about the embedded documentation feature, see [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="fd026-194">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="fd026-194">Create an Azure AD test user</span></span>
<span data-ttu-id="fd026-195">В этом разделе вы создадите на портале Azure тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fd026-195">In this section, you create test user Britta Simon in the Azure portal.</span></span>

![Тестовый пользователь Britta Simon][100]

<span data-ttu-id="fd026-197">Чтобы создать тестового пользователя в Azure AD, выполните следующее.</span><span class="sxs-lookup"><span data-stu-id="fd026-197">To create a test user in Azure AD, do the following:</span></span>

1. <span data-ttu-id="fd026-198">На **портале Azure** в области слева нажмите кнопку **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fd026-198">In the **Azure portal**, in the left pane, select the **Azure Active Directory** button.</span></span>

    ![Кнопка Azure Active Directory](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="fd026-200">Чтобы отобразить список пользователей, выберите **Пользователи и группы** > **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="fd026-200">To display the list of users, select **Users and groups** > **All users**.</span></span>
    
    ![Ссылка "Все пользователи"](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_02.png) 
    
    <span data-ttu-id="fd026-202">Откроется диалоговое окно **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="fd026-202">The **All users** dialog box opens.</span></span>

3. <span data-ttu-id="fd026-203">Щелкните **Добавить**, чтобы открыть диалоговое окно **Пользователь**.</span><span class="sxs-lookup"><span data-stu-id="fd026-203">To open the **User** dialog box, select **Add**.</span></span>
 
    ![Кнопка "Добавить"](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="fd026-205">В диалоговом окне **Пользователь** сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="fd026-205">In the **User** dialog box, do the following:</span></span>
 
    ![Диалоговое окно "Пользователь"](./media/active-directory-saas-cezannehrsoftware-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="fd026-207">а.</span><span class="sxs-lookup"><span data-stu-id="fd026-207">a.</span></span> <span data-ttu-id="fd026-208">В поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fd026-208">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fd026-209">b.</span><span class="sxs-lookup"><span data-stu-id="fd026-209">b.</span></span> <span data-ttu-id="fd026-210">В поле **Имя пользователя** введите **адрес электронной почты** пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fd026-210">In the **User name** box, type user Britta Simon's **email address**.</span></span>

    <span data-ttu-id="fd026-211">c.</span><span class="sxs-lookup"><span data-stu-id="fd026-211">c.</span></span> <span data-ttu-id="fd026-212">Установите флажок **Показать пароль** и запишите значение, созданное в поле **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="fd026-212">Select the **Show Password** check box, and then note the value that was generated in the **Password** box.</span></span>

    <span data-ttu-id="fd026-213">d.</span><span class="sxs-lookup"><span data-stu-id="fd026-213">d.</span></span> <span data-ttu-id="fd026-214">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="fd026-214">Select **Create**.</span></span>
 
### <a name="create-a-cezanne-hr-software-test-user"></a><span data-ttu-id="fd026-215">Создание тестового пользователя Cezanne HR Software</span><span class="sxs-lookup"><span data-stu-id="fd026-215">Create a Cezanne HR software test user</span></span>

<span data-ttu-id="fd026-216">Чтобы пользователи Azure AD могли входить в Cezanne HR Software, их необходимо подготовить в Cezanne HR Software.</span><span class="sxs-lookup"><span data-stu-id="fd026-216">To enable Azure AD users to sign in to Cezanne HR software, they must be provisioned into Cezanne HR software.</span></span> <span data-ttu-id="fd026-217">В случае Cezanne HR Software подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="fd026-217">In the case of Cezanne HR software, provisioning is a manual task.</span></span>

<span data-ttu-id="fd026-218">Чтобы подготовить учетную запись пользователя, сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="fd026-218">Provision a user account by doing the following:</span></span>

1.  <span data-ttu-id="fd026-219">Войдите на корпоративный сайт Cezanne HR Software своей организации в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="fd026-219">Sign in to your Cezanne HR software company site as an administrator.</span></span>

2.  <span data-ttu-id="fd026-220">В левой области выберите **System Setup** > **Manage Users** > **Add New User** ("Настройка системы" > "Управление пользователями" > "Добавить пользователя").</span><span class="sxs-lookup"><span data-stu-id="fd026-220">In the left pane, select **System Setup** > **Manage Users** > **Add New User**.</span></span>

    <span data-ttu-id="fd026-221">![Ссылка "Add New User" (Добавить пользователя)](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_005.png "Создание пользователя")</span><span class="sxs-lookup"><span data-stu-id="fd026-221">![The "Add New User" link](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_005.png "New User")</span></span>

3.  <span data-ttu-id="fd026-222">В разделе **Person Details** (Сведения о пользователе) выполните следующее.</span><span class="sxs-lookup"><span data-stu-id="fd026-222">Under **Person Details**, do the following:</span></span>

    <span data-ttu-id="fd026-223">![Раздел "Person Details" (Сведения о пользователе)](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_006.png "Создание пользователя")</span><span class="sxs-lookup"><span data-stu-id="fd026-223">![The "Person Details" section](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_006.png "New User")</span></span>
    
    <span data-ttu-id="fd026-224">а.</span><span class="sxs-lookup"><span data-stu-id="fd026-224">a.</span></span> <span data-ttu-id="fd026-225">Установите для параметра **Internal User** (Внутренний пользователь) значение **OFF** (Выключено).</span><span class="sxs-lookup"><span data-stu-id="fd026-225">Set **Internal User** as **OFF**.</span></span>
    
    <span data-ttu-id="fd026-226">b.</span><span class="sxs-lookup"><span data-stu-id="fd026-226">b.</span></span> <span data-ttu-id="fd026-227">В поле **First Name** (Имя) введите имя пользователя, например **Britta**.</span><span class="sxs-lookup"><span data-stu-id="fd026-227">In the **First Name** box, type the user's first name, for example, **Britta**.</span></span>  
 
    <span data-ttu-id="fd026-228">c.</span><span class="sxs-lookup"><span data-stu-id="fd026-228">c.</span></span> <span data-ttu-id="fd026-229">В поле **Last Name** (Фамилия) введите фамилию пользователя, например **Simon**.</span><span class="sxs-lookup"><span data-stu-id="fd026-229">In the **Last Name** box, type the user's last name, for example, **Simon**.</span></span>
    
    <span data-ttu-id="fd026-230">d.</span><span class="sxs-lookup"><span data-stu-id="fd026-230">d.</span></span> <span data-ttu-id="fd026-231">В поле **E-mail** (Адрес электронной почты) введите адрес электронной почты пользователя, например Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="fd026-231">In the **E-mail** box, type the user's email address, for example, Brittasimon@contoso.com.</span></span>

4.  <span data-ttu-id="fd026-232">В разделе **Account Information** (Сведения об учетной записи) выполните следующее.</span><span class="sxs-lookup"><span data-stu-id="fd026-232">Under **Account Information**, do the following:</span></span>

    <span data-ttu-id="fd026-233">![Раздел "Account Information" (Сведения об учетной записи)](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_007.png "Создание пользователя")</span><span class="sxs-lookup"><span data-stu-id="fd026-233">![The "Account Information" section](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_007.png "New User")</span></span>
    
    <span data-ttu-id="fd026-234">а.</span><span class="sxs-lookup"><span data-stu-id="fd026-234">a.</span></span> <span data-ttu-id="fd026-235">В поле **Username** (Имя пользователя) введите адрес электронной почты пользователя, например Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="fd026-235">In the **Username** box, type the user's email address, for example, Brittasimon@contoso.com.</span></span>
    
    <span data-ttu-id="fd026-236">b.</span><span class="sxs-lookup"><span data-stu-id="fd026-236">b.</span></span> <span data-ttu-id="fd026-237">В поле **Password** (Пароль) введите пароль пользователя.</span><span class="sxs-lookup"><span data-stu-id="fd026-237">In the **Password** box, type the user's password.</span></span>
    
    <span data-ttu-id="fd026-238">c.</span><span class="sxs-lookup"><span data-stu-id="fd026-238">c.</span></span> <span data-ttu-id="fd026-239">В поле **Security Role** (Роль безопасности) выберите **HR Professional** (Специалист отдела кадров).</span><span class="sxs-lookup"><span data-stu-id="fd026-239">In the **Security Role** box, select **HR Professional**.</span></span>
    
    <span data-ttu-id="fd026-240">d.</span><span class="sxs-lookup"><span data-stu-id="fd026-240">d.</span></span> <span data-ttu-id="fd026-241">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="fd026-241">Select **OK**.</span></span>

5. <span data-ttu-id="fd026-242">Перейдите на вкладку **Single sign-on** (Единый вход) и в разделе **SAML 2.0 Identifiers** (Идентификаторы SAML 2.0) нажмите кнопку **Add New** (Добавить).</span><span class="sxs-lookup"><span data-stu-id="fd026-242">On the **Single sign-on** tab, in the **SAML 2.0 Identifiers** section, select **Add New**.</span></span>

    <span data-ttu-id="fd026-243">![Кнопка "Add New" (Добавить)](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_008.png "Пользователь")</span><span class="sxs-lookup"><span data-stu-id="fd026-243">![The "Add New" button](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_008.png "User")</span></span>

6. <span data-ttu-id="fd026-244">Из списка **Identity Provider** (Поставщик удостоверений) выберите поставщик удостоверений.</span><span class="sxs-lookup"><span data-stu-id="fd026-244">In the **Identity Provider** list box, select your identity provider.</span></span> <span data-ttu-id="fd026-245">В поле **User Identifier** (Идентификатор пользователя) введите адрес электронной почты учетной записи тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fd026-245">In the **User Identifier** box, enter the email address for test user Britta Simon's account.</span></span>

    <span data-ttu-id="fd026-246">![Поля "Identity Provider" (Поставщик удостоверений) и "User Identifier" (Идентификатор пользователя)](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_009.png "Пользователь")</span><span class="sxs-lookup"><span data-stu-id="fd026-246">![The "Identity Provider" and "User Identifier" boxes](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_009.png "User")</span></span>
    
7. <span data-ttu-id="fd026-247">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="fd026-247">Select **Save**.</span></span>

    <span data-ttu-id="fd026-248">![Кнопка "Save" (Сохранить)](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_010.png "Пользователь")</span><span class="sxs-lookup"><span data-stu-id="fd026-248">![The "Save" button](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_010.png "User")</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="fd026-249">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="fd026-249">Assign the Azure AD test user</span></span>

<span data-ttu-id="fd026-250">В этом разделе описано, как разрешить тестовому пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к Cezanne HR Software.</span><span class="sxs-lookup"><span data-stu-id="fd026-250">In this section, you enable test user Britta Simon to use Azure SSO by granting access to Cezanne HR software.</span></span>

![Проверка доступа пользователей][200] 

1. <span data-ttu-id="fd026-252">На портале Azure откройте представление приложений и перейдите к представлению каталога.</span><span class="sxs-lookup"><span data-stu-id="fd026-252">In the Azure portal, open the applications view and then go to the directory view.</span></span> <span data-ttu-id="fd026-253">Щелкните **Корпоративные приложения** > **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="fd026-253">Select **Enterprise applications** > **All applications**.</span></span>

    ![Ссылка "Все приложения"][201] 

2. <span data-ttu-id="fd026-255">В списке приложений выберите **Cezanne HR Software**.</span><span class="sxs-lookup"><span data-stu-id="fd026-255">In the applications list, select **Cezanne HR Software**.</span></span>

    ![Список "Приложения"](./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_cezannehrsoftware_app.png) 

3. <span data-ttu-id="fd026-257">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="fd026-257">In the menu on the left, select **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="fd026-259">Выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="fd026-259">Select **Add**.</span></span> <span data-ttu-id="fd026-260">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="fd026-260">Then in the **Add Assignment** dialog box, select **Users and groups**.</span></span>

    ![Ссылка "Пользователи и группы"][203]

5. <span data-ttu-id="fd026-262">В диалоговом окне **Пользователи и группы** в списке **Пользователи** выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="fd026-262">In the **Users and groups** dialog box, in the **Users** list, select **Britta Simon**.</span></span>

6. <span data-ttu-id="fd026-263">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="fd026-263">In the **Users and groups** dialog box, select **Select**.</span></span>

7. <span data-ttu-id="fd026-264">В диалоговом окне **Добавление назначения** выберите **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="fd026-264">In the **Add Assignment** dialog box, select **Assign**.</span></span>
    
### <a name="test-sso"></a><span data-ttu-id="fd026-265">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="fd026-265">Test SSO</span></span>

<span data-ttu-id="fd026-266">В этом разделе вы с помощью панели доступа выполните проверку конфигурации единого входа Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fd026-266">In this section, you test your Azure AD SSO configuration by using the Access Panel.</span></span>

<span data-ttu-id="fd026-267">Щелкнув элемент "Cezanne HR Software" на панели доступа, вы автоматически войдете в приложение "Cezanne HR Software".</span><span class="sxs-lookup"><span data-stu-id="fd026-267">When you select the Cezanne HR software tile in the Access Panel, you sign on automatically to your Cezanne HR software application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fd026-268">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fd026-268">Next steps</span></span>

* [<span data-ttu-id="fd026-269">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fd026-269">List of tutorials on how to integrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fd026-270">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="fd026-270">What is application access and SSO with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cezannehrsoftware-tutorial/tutorial_general_203.png

