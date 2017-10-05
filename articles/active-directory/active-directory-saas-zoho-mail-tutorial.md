---
title: "Руководство по интеграции Azure Active Directory с Zoho | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и Zoho."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 9874e1f3-ade5-42e7-a700-e08b3731236a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: jeedes
ms.openlocfilehash: f0688cb75584ada805b944d2ef5409d66ab37339
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zoho"></a><span data-ttu-id="e042a-103">Руководство по интеграции Azure Active Directory с Zoho</span><span class="sxs-lookup"><span data-stu-id="e042a-103">Tutorial: Azure Active Directory integration with Zoho</span></span>

<span data-ttu-id="e042a-104">В этом руководстве описано, как интегрировать Zoho с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e042a-104">In this tutorial, you learn how to integrate Zoho with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e042a-105">Интеграция Azure AD с приложением Zoho обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="e042a-105">Integrating Zoho with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e042a-106">С помощью Azure AD вы можете контролировать доступ к Zoho.</span><span class="sxs-lookup"><span data-stu-id="e042a-106">You can control in Azure AD who has access to Zoho.</span></span>
- <span data-ttu-id="e042a-107">Вы можете включить автоматический вход пользователей в Zoho (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e042a-107">You can enable your users to automatically get signed-on to Zoho (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="e042a-108">Вы можете управлять учетными записями централизованно — на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="e042a-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="e042a-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e042a-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e042a-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="e042a-110">Prerequisites</span></span>

<span data-ttu-id="e042a-111">Чтобы настроить интеграцию Azure AD с Zoho, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="e042a-111">To configure Azure AD integration with Zoho, you need the following items:</span></span>

- <span data-ttu-id="e042a-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="e042a-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e042a-113">подписка Zoho с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="e042a-113">A Zoho single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e042a-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="e042a-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e042a-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="e042a-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e042a-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="e042a-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e042a-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e042a-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e042a-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="e042a-118">Scenario description</span></span>
<span data-ttu-id="e042a-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="e042a-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e042a-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="e042a-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e042a-121">Добавление Zoho из коллекции</span><span class="sxs-lookup"><span data-stu-id="e042a-121">Adding Zoho from the gallery</span></span>
2. <span data-ttu-id="e042a-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="e042a-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zoho-from-the-gallery"></a><span data-ttu-id="e042a-123">Добавление Zoho из коллекции</span><span class="sxs-lookup"><span data-stu-id="e042a-123">Adding Zoho from the gallery</span></span>
<span data-ttu-id="e042a-124">Чтобы настроить интеграцию Zoho с Azure AD, необходимо добавить Zoho из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="e042a-124">To configure the integration of Zoho into Azure AD, you need to add Zoho from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e042a-125">**Чтобы добавить Zoho из коллекции, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="e042a-125">**To add Zoho from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e042a-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e042a-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка "Azure Active Directory"][1]

2. <span data-ttu-id="e042a-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="e042a-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e042a-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="e042a-129">Then go to **All applications**.</span></span>

    ![Колонка "Корпоративные приложения"][2]
    
3. <span data-ttu-id="e042a-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="e042a-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Кнопка "Новое приложение"][3]

4. <span data-ttu-id="e042a-133">В поле поиска введите **Zoho**, выберите **Zoho** на панели результатов и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="e042a-133">In the search box, type **Zoho**, select **Zoho** from result panel then click **Add** button to add the application.</span></span>

    ![Zoho в списке результатов](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="e042a-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="e042a-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="e042a-136">В этом разделе описана настройка и проверка единого входа Azure AD в приложение Zoho с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e042a-136">In this section, you configure and test Azure AD single sign-on with Zoho based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e042a-137">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Zoho соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e042a-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Zoho is to a user in Azure AD.</span></span> <span data-ttu-id="e042a-138">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Zoho.</span><span class="sxs-lookup"><span data-stu-id="e042a-138">In other words, a link relationship between an Azure AD user and the related user in Zoho needs to be established.</span></span>

<span data-ttu-id="e042a-139">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Zoho.</span><span class="sxs-lookup"><span data-stu-id="e042a-139">In Zoho, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e042a-140">Чтобы настроить и проверить единый вход Azure AD в Zoho, выполните действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="e042a-140">To configure and test Azure AD single sign-on with Zoho, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e042a-141">**[Настройка единого входа Azure AD](#configure-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="e042a-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e042a-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e042a-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e042a-143">**[Создание тестового пользователя приложения Zoho](#create-a-zoho-test-user)** требуется для того, чтобы в Zoho существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e042a-143">**[Create a Zoho test user](#create-a-zoho-test-user)** - to have a counterpart of Britta Simon in Zoho that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e042a-144">**[Назначение тестового пользователя Azure AD](#assign-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e042a-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e042a-145">**[Проверка единого входа](#test-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="e042a-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="e042a-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="e042a-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="e042a-147">В этом разделе мы включим на портале Azure единый вход Azure AD и настроим его в приложении Zoho.</span><span class="sxs-lookup"><span data-stu-id="e042a-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Zoho application.</span></span>

<span data-ttu-id="e042a-148">**Чтобы настроить единый вход Azure AD в Zoho, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="e042a-148">**To configure Azure AD single sign-on with Zoho, perform the following steps:**</span></span>

1. <span data-ttu-id="e042a-149">На портале Azure на странице интеграции с приложением **Zoho** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="e042a-149">In the Azure portal, on the **Zoho** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="e042a-151">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="e042a-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_samlbase.png)

3. <span data-ttu-id="e042a-153">В разделе **Домены и URL-адреса приложения Zoho** сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="e042a-153">On the **Zoho Domain and URLs** section, perform the following steps:</span></span>

    ![Сведения о домене и URL-адресах единого входа для приложения Zoho](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_url.png)

    <span data-ttu-id="e042a-155">а.</span><span class="sxs-lookup"><span data-stu-id="e042a-155">a.</span></span> <span data-ttu-id="e042a-156">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<company name>.zohomail.com`</span><span class="sxs-lookup"><span data-stu-id="e042a-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.zohomail.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e042a-157">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="e042a-157">This value is not real.</span></span> <span data-ttu-id="e042a-158">Вместо него необходимо указать фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="e042a-158">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="e042a-159">Чтобы получить это значение, обратитесь к [группе поддержки клиентов Zoho](https://www.zoho.com/mail/contact.html).</span><span class="sxs-lookup"><span data-stu-id="e042a-159">Contact [Zoho Client support team](https://www.zoho.com/mail/contact.html) to get this value.</span></span> 
 
4. <span data-ttu-id="e042a-160">В разделе **Сертификат подписи SAML** щелкните **Сертификат (Base64)**, а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="e042a-160">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Ссылка для скачивания сертификата](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_certificate.png) 

5. <span data-ttu-id="e042a-162">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="e042a-162">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e042a-164">В разделе **Конфигурация Zoho** щелкните **Настроить Zoho**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="e042a-164">On the **Zoho Configuration** section, click **Configure Zoho** to open **Configure sign-on** window.</span></span> <span data-ttu-id="e042a-165">Скопируйте **URL-адрес выхода, URL-адрес изменения пароля и URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="e042a-165">Copy the **Sign-Out URL, Change Password URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка Zoho](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_configure.png) 

7. <span data-ttu-id="e042a-167">В другом окне браузера войдите на свой корпоративный сайт Zoho Mail в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="e042a-167">In a different web browser window, log into your Zoho Mail company site as an administrator.</span></span>

8. <span data-ttu-id="e042a-168">Перейдите в раздел **Панель управления**.</span><span class="sxs-lookup"><span data-stu-id="e042a-168">Go to the **Control panel**.</span></span>
   
    <span data-ttu-id="e042a-169">![Панель управления](./media/active-directory-saas-zoho-mail-tutorial/ic789607.png "Панель управления")</span><span class="sxs-lookup"><span data-stu-id="e042a-169">![Control Panel](./media/active-directory-saas-zoho-mail-tutorial/ic789607.png "Control Panel")</span></span>

9. <span data-ttu-id="e042a-170">Щелкните вкладку **Проверка подлинности SAML** .</span><span class="sxs-lookup"><span data-stu-id="e042a-170">Click the **SAML Authentication** tab.</span></span>
   
    <span data-ttu-id="e042a-171">![Аутентификация SAML](./media/active-directory-saas-zoho-mail-tutorial/ic789608.png "Аутентификация SAML")</span><span class="sxs-lookup"><span data-stu-id="e042a-171">![SAML Authentication](./media/active-directory-saas-zoho-mail-tutorial/ic789608.png "SAML Authentication")</span></span>

10. <span data-ttu-id="e042a-172">В разделе **Информация о проверке подлинности SAML** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="e042a-172">In the **SAML Authentication Details** section, perform the following steps:</span></span>
   
    <span data-ttu-id="e042a-173">![Параметры аутентификации SAML](./media/active-directory-saas-zoho-mail-tutorial/ic789609.png "Параметры аутентификации SAML")</span><span class="sxs-lookup"><span data-stu-id="e042a-173">![SAML Authentication Details](./media/active-directory-saas-zoho-mail-tutorial/ic789609.png "SAML Authentication Details")</span></span>
   
    <span data-ttu-id="e042a-174">а.</span><span class="sxs-lookup"><span data-stu-id="e042a-174">a.</span></span> <span data-ttu-id="e042a-175">В текстовое поле **Login URL** (URL-адрес входа) вставьте значение **URL-адрес службы единого входа SAML**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="e042a-175">In the **Login URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="e042a-176">b.</span><span class="sxs-lookup"><span data-stu-id="e042a-176">b.</span></span> <span data-ttu-id="e042a-177">В текстовое поле **Logout URL** (URL-адрес выхода) вставьте значение **URL-адрес выхода**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="e042a-177">In the **Logout URL** textbox, paste **Sign-Out URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="e042a-178">c.</span><span class="sxs-lookup"><span data-stu-id="e042a-178">c.</span></span> <span data-ttu-id="e042a-179">В текстовое поле **Change Password URL** (URL-адрес для изменения пароля) вставьте **URL-адрес изменения пароля**, скопированный на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="e042a-179">In the **Change Password URL** textbox, paste **Change Password URL** which you have copied from Azure portal.</span></span>
       
    <span data-ttu-id="e042a-180">d.</span><span class="sxs-lookup"><span data-stu-id="e042a-180">d.</span></span> <span data-ttu-id="e042a-181">Откройте в Блокноте сертификат в кодировке Base-64, скачанный с портала Azure, скопируйте его содержимое в буфер обмена, а затем вставьте в текстовое поле **PublicKey** (Открытый ключ).</span><span class="sxs-lookup"><span data-stu-id="e042a-181">Open your base-64 encoded certificate downloaded from Azure portal in notepad, copy the content of it into your clipboard, and then paste it to the **PublicKey** textbox.</span></span>
   
    <span data-ttu-id="e042a-182">д.</span><span class="sxs-lookup"><span data-stu-id="e042a-182">e.</span></span> <span data-ttu-id="e042a-183">В поле **Algorithm** (Алгоритм) задайте значение **RSA**.</span><span class="sxs-lookup"><span data-stu-id="e042a-183">As **Algorithm**, select **RSA**.</span></span>
   
    <span data-ttu-id="e042a-184">f.</span><span class="sxs-lookup"><span data-stu-id="e042a-184">f.</span></span> <span data-ttu-id="e042a-185">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="e042a-185">Click **OK**.</span></span>

> [!TIP]
> <span data-ttu-id="e042a-186">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="e042a-186">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e042a-187">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="e042a-187">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e042a-188">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="e042a-188">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="e042a-189">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="e042a-189">Create an Azure AD test user</span></span>

<span data-ttu-id="e042a-190">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e042a-190">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="e042a-192">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="e042a-192">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e042a-193">На портале Azure в области слева нажмите кнопку **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e042a-193">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Кнопка "Azure Active Directory"](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="e042a-195">Чтобы открыть список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="e042a-195">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Ссылки "Пользователи и группы" и "Все пользователи"](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="e042a-197">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна **Все пользователи** щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="e042a-197">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Кнопка "Добавить"](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="e042a-199">В диалоговом окне **Пользователь** сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="e042a-199">In the **User** dialog box, perform the following steps:</span></span>

    ![Диалоговое окно "Пользователь"](./media/active-directory-saas-zoho-mail-tutorial/create_aaduser_04.png)

    <span data-ttu-id="e042a-201">а.</span><span class="sxs-lookup"><span data-stu-id="e042a-201">a.</span></span> <span data-ttu-id="e042a-202">В поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e042a-202">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e042a-203">b.</span><span class="sxs-lookup"><span data-stu-id="e042a-203">b.</span></span> <span data-ttu-id="e042a-204">В поле **Имя пользователя** введите адрес электронной почты для пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e042a-204">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="e042a-205">c.</span><span class="sxs-lookup"><span data-stu-id="e042a-205">c.</span></span> <span data-ttu-id="e042a-206">Установите флажок **Показать пароль** и запишите значение, которое отображается в поле **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="e042a-206">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="e042a-207">г)</span><span class="sxs-lookup"><span data-stu-id="e042a-207">d.</span></span> <span data-ttu-id="e042a-208">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="e042a-208">Click **Create**.</span></span>
 
### <a name="create-a-zoho-test-user"></a><span data-ttu-id="e042a-209">Создание тестового пользователя Zoho</span><span class="sxs-lookup"><span data-stu-id="e042a-209">Create a Zoho test user</span></span>

<span data-ttu-id="e042a-210">Чтобы пользователи Azure AD могли выполнить вход в Zoho Mail, они должны быть подготовлены для Zoho Mail.</span><span class="sxs-lookup"><span data-stu-id="e042a-210">In order to enable Azure AD users to log into Zoho Mail, they must be provisioned into Zoho Mail.</span></span> <span data-ttu-id="e042a-211">В случае с Zoho Mail подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="e042a-211">In the case of Zoho Mail, provisioning is a manual task.</span></span>

> [!NOTE]
> <span data-ttu-id="e042a-212">Вы можете использовать любые другие средства создания учетной записи пользователя Zoho Mail или API, предоставляемые Zoho Mail, для подготовки учетных записей пользователей AAD.</span><span class="sxs-lookup"><span data-stu-id="e042a-212">You can use any other Zoho Mail user account creation tools or APIs provided by Zoho Mail to provision AAD user accounts.</span></span>

### <a name="to-provision-a-user-account-perform-the-following-steps"></a><span data-ttu-id="e042a-213">Чтобы подготовить учетную запись пользователя, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="e042a-213">To provision a user account, perform the following steps:</span></span>

1. <span data-ttu-id="e042a-214">Войдите на веб-сайт **Zoho Mail** компании в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="e042a-214">Log in to your **Zoho Mail** company site as an administrator.</span></span>

2. <span data-ttu-id="e042a-215">Выберите **Панель управления \> Mail & Docs** (Почта и документы).</span><span class="sxs-lookup"><span data-stu-id="e042a-215">Go to **Control Panel \> Mail & Docs**.</span></span>

3. <span data-ttu-id="e042a-216">Щелкните **User Details (Сведения о пользователе) \> Add User (Добавить пользователя)**.</span><span class="sxs-lookup"><span data-stu-id="e042a-216">Go to **User Details \> Add User**.</span></span>
   
    <span data-ttu-id="e042a-217">![Добавление пользователя](./media/active-directory-saas-zoho-mail-tutorial/ic789611.png "Добавление пользователя")</span><span class="sxs-lookup"><span data-stu-id="e042a-217">![Add User](./media/active-directory-saas-zoho-mail-tutorial/ic789611.png "Add User")</span></span>

4. <span data-ttu-id="e042a-218">В диалоговом окне **Добавление пользователей** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="e042a-218">On the **Add users** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="e042a-219">![Добавление пользователя](./media/active-directory-saas-zoho-mail-tutorial/ic789612.png "Добавление пользователя")</span><span class="sxs-lookup"><span data-stu-id="e042a-219">![Add User](./media/active-directory-saas-zoho-mail-tutorial/ic789612.png "Add User")</span></span>
   
    <span data-ttu-id="e042a-220">а.</span><span class="sxs-lookup"><span data-stu-id="e042a-220">a.</span></span> <span data-ttu-id="e042a-221">В текстовом поле **First Name** (Имя) введите имя пользователя, например **Britta**.</span><span class="sxs-lookup"><span data-stu-id="e042a-221">In the **First Name** textbox, type the first name of user like **Britta**.</span></span>

    <span data-ttu-id="e042a-222">b.</span><span class="sxs-lookup"><span data-stu-id="e042a-222">b.</span></span> <span data-ttu-id="e042a-223">В текстовом поле **Last Name** (Фамилия) введите фамилию пользователя, например **Simon**.</span><span class="sxs-lookup"><span data-stu-id="e042a-223">In the **Last Name** textbox, type the last name of user like **Simon**.</span></span>

    <span data-ttu-id="e042a-224">c.</span><span class="sxs-lookup"><span data-stu-id="e042a-224">c.</span></span> <span data-ttu-id="e042a-225">В текстовом поле **Email** (Электронная почта) введите адрес электронной почты пользователя, например **brittasimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="e042a-225">In the **Email ID** textbox, type the email id of user like **brittasimon@contoso.com**.</span></span>

    <span data-ttu-id="e042a-226">d.</span><span class="sxs-lookup"><span data-stu-id="e042a-226">d.</span></span> <span data-ttu-id="e042a-227">В текстовом поле **Password** (Пароль) введите пароль пользователя.</span><span class="sxs-lookup"><span data-stu-id="e042a-227">In the **Password** textbox, enter password of user.</span></span>
   
    <span data-ttu-id="e042a-228">д.</span><span class="sxs-lookup"><span data-stu-id="e042a-228">e.</span></span> <span data-ttu-id="e042a-229">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="e042a-229">Click **OK**.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="e042a-230">Владелец учетной записи Azure Active Directory получит электронное сообщение со ссылкой для подтверждения учетной записи перед ее активацией.</span><span class="sxs-lookup"><span data-stu-id="e042a-230">The Azure Active Directory account holder will receive an email with a link to confirm the account before it becomes active.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="e042a-231">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="e042a-231">Assign the Azure AD test user</span></span>

<span data-ttu-id="e042a-232">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure путем предоставления доступа к Zoho.</span><span class="sxs-lookup"><span data-stu-id="e042a-232">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Zoho.</span></span>

![Назначение роли пользователя][200] 

<span data-ttu-id="e042a-234">**Чтобы назначить пользователя Britta Simon в Zoho, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="e042a-234">**To assign Britta Simon to Zoho, perform the following steps:**</span></span>

1. <span data-ttu-id="e042a-235">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="e042a-235">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="e042a-237">В списке приложений выберите **Zoho**.</span><span class="sxs-lookup"><span data-stu-id="e042a-237">In the applications list, select **Zoho**.</span></span>

    ![Ссылка на Zoho в списке приложений](./media/active-directory-saas-zoho-mail-tutorial/tutorial_zoho_app.png)  

3. <span data-ttu-id="e042a-239">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="e042a-239">In the menu on the left, click **Users and groups**.</span></span>

    ![Ссылка "Пользователи и группы"][202]

4. <span data-ttu-id="e042a-241">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="e042a-241">Click **Add** button.</span></span> <span data-ttu-id="e042a-242">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="e042a-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Область "Добавление назначения"][203]

5. <span data-ttu-id="e042a-244">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="e042a-244">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e042a-245">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="e042a-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e042a-246">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="e042a-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="e042a-247">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="e042a-247">Test single sign-on</span></span>

<span data-ttu-id="e042a-248">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="e042a-248">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e042a-249">Щелкнув плитку Zoho на панели доступа, вы автоматически войдете в приложение Zoho.</span><span class="sxs-lookup"><span data-stu-id="e042a-249">When you click the Zoho tile in the Access Panel, you should get automatically signed-on to your Zoho application.</span></span>
<span data-ttu-id="e042a-250">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e042a-250">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="e042a-251">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="e042a-251">Additional resources</span></span>

* [<span data-ttu-id="e042a-252">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e042a-252">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e042a-253">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e042a-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zoho-mail-tutorial/tutorial_general_203.png

