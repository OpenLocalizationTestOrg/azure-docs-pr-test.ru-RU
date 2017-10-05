---
title: "Учебник. Интеграция Azure Active Directory с Envoy | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и Envoy."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 71f7afcc-1033-4098-9b7e-4f9f2b26f734
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: jeedes
ms.openlocfilehash: 49211b35ab3e28e0df914061e7fa623907935638
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-envoy"></a><span data-ttu-id="89952-103">Руководство. Интеграция Azure Active Directory с Envoy</span><span class="sxs-lookup"><span data-stu-id="89952-103">Tutorial: Azure Active Directory integration with Envoy</span></span>

<span data-ttu-id="89952-104">В этом учебнике описано, как интегрировать Envoy с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="89952-104">In this tutorial, you learn how to integrate Envoy with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="89952-105">Интеграция Azure AD с приложением Envoy обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="89952-105">Integrating Envoy with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="89952-106">С помощью Azure AD вы можете контролировать доступ к Envoy.</span><span class="sxs-lookup"><span data-stu-id="89952-106">You can control in Azure AD who has access to Envoy.</span></span>
- <span data-ttu-id="89952-107">Вы можете включить автоматический вход пользователей в Envoy (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="89952-107">You can enable your users to automatically get signed-on to Envoy (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="89952-108">Вы можете управлять учетными записями централизованно — на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="89952-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="89952-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="89952-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="89952-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="89952-110">Prerequisites</span></span>

<span data-ttu-id="89952-111">Чтобы настроить интеграцию Azure AD с Envoy, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="89952-111">To configure Azure AD integration with Envoy, you need the following items:</span></span>

- <span data-ttu-id="89952-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="89952-112">An Azure AD subscription</span></span>
- <span data-ttu-id="89952-113">подписка Envoy с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="89952-113">An Envoy single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="89952-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="89952-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="89952-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="89952-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="89952-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="89952-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="89952-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="89952-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="89952-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="89952-118">Scenario description</span></span>
<span data-ttu-id="89952-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="89952-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="89952-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="89952-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="89952-121">Добавление Envoy из коллекции</span><span class="sxs-lookup"><span data-stu-id="89952-121">Adding Envoy from the gallery</span></span>
2. <span data-ttu-id="89952-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="89952-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-envoy-from-the-gallery"></a><span data-ttu-id="89952-123">Добавление Envoy из коллекции</span><span class="sxs-lookup"><span data-stu-id="89952-123">Adding Envoy from the gallery</span></span>
<span data-ttu-id="89952-124">Чтобы настроить интеграцию Envoy с Azure AD, необходимо добавить Envoy из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="89952-124">To configure the integration of Envoy into Azure AD, you need to add Envoy from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="89952-125">**Чтобы добавить Envoy из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="89952-125">**To add Envoy from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="89952-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="89952-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка "Azure Active Directory"][1]

2. <span data-ttu-id="89952-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="89952-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="89952-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="89952-129">Then go to **All applications**.</span></span>

    ![Колонка "Корпоративные приложения"][2]
    
3. <span data-ttu-id="89952-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="89952-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Кнопка "Новое приложение"][3]

4. <span data-ttu-id="89952-133">В поле поиска введите **Envoy**, выберите **Envoy** на панели результатов и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="89952-133">In the search box, type **Envoy**, select **Envoy** from result panel then click **Add** button to add the application.</span></span>

    ![Envoy в списке результатов](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="89952-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="89952-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="89952-136">В этом разделе описана настройка и проверка единого входа Azure AD в приложение Envoy с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="89952-136">In this section, you configure and test Azure AD single sign-on with Envoy based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="89952-137">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Envoy соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="89952-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Envoy is to a user in Azure AD.</span></span> <span data-ttu-id="89952-138">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Envoy.</span><span class="sxs-lookup"><span data-stu-id="89952-138">In other words, a link relationship between an Azure AD user and the related user in Envoy needs to be established.</span></span>

<span data-ttu-id="89952-139">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Envoy.</span><span class="sxs-lookup"><span data-stu-id="89952-139">In Envoy, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="89952-140">Чтобы настроить и проверить единый вход Azure AD в Envoy, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="89952-140">To configure and test Azure AD single sign-on with Envoy, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="89952-141">**[Настройка единого входа Azure AD](#configure-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="89952-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="89952-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="89952-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="89952-143">**[Создание тестового пользователя Envoy](#create-an-envoy-test-user)** нужно для того, чтобы в Envoy существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="89952-143">**[Create an Envoy test user](#create-an-envoy-test-user)** - to have a counterpart of Britta Simon in Envoy that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="89952-144">**[Назначение тестового пользователя Azure AD](#assign-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход Azure AD.</span><span class="sxs-lookup"><span data-stu-id="89952-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="89952-145">**[Проверка единого входа](#test-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="89952-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="89952-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="89952-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="89952-147">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в Envoy.</span><span class="sxs-lookup"><span data-stu-id="89952-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Envoy application.</span></span>

<span data-ttu-id="89952-148">**Чтобы настроить единый вход Azure AD в Envoy, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="89952-148">**To configure Azure AD single sign-on with Envoy, perform the following steps:**</span></span>

1. <span data-ttu-id="89952-149">На портале Azure на странице интеграции с приложением **Envoy** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="89952-149">In the Azure portal, on the **Envoy** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="89952-151">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="89952-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_samlbase.png)

3. <span data-ttu-id="89952-153">В разделе **Домены и URL-адреса приложения Envoy** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="89952-153">On the **Envoy Domain and URLs** section, perform the following steps:</span></span>

    ![Сведения о домене и URL-адресах единого входа приложения Envoy](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_url.png)

    <span data-ttu-id="89952-155">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<tenant-name>.Envoy.com`</span><span class="sxs-lookup"><span data-stu-id="89952-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenant-name>.Envoy.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="89952-156">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="89952-156">This value is not real.</span></span> <span data-ttu-id="89952-157">Вместо него необходимо указать фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="89952-157">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="89952-158">Для получения этого значения обратитесь в [службу поддержки клиентов Envoy](https://envoy.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="89952-158">Contact [Envoy Client support team](https://envoy.com/contact/) to get this value.</span></span>

4. <span data-ttu-id="89952-159">В разделе **Сертификат подписи SAML** скопируйте значение **Отпечаток**.</span><span class="sxs-lookup"><span data-stu-id="89952-159">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate..</span></span>

    ![Ссылка для скачивания сертификата](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_certificate.png) 

5. <span data-ttu-id="89952-161">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="89952-161">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-envoy-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="89952-163">В разделе **Конфигурация Envoy** щелкните **Настроить Envoy**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="89952-163">On the **Envoy Configuration** section, click **Configure Envoy** to open **Configure sign-on** window.</span></span> <span data-ttu-id="89952-164">Скопируйте **URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="89952-164">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Конфигурация Envoy](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_configure.png)

7. <span data-ttu-id="89952-166">В другом окне веб-браузера войдите на свой корпоративный веб-сайт Envoy в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="89952-166">In a different web browser window, log into your Envoy company site as an administrator.</span></span>

8. <span data-ttu-id="89952-167">На панели инструментов в верхней части экрана нажмите **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="89952-167">In the toolbar on the top, click **Settings**.</span></span>

    <span data-ttu-id="89952-168">![Envoy](./media/active-directory-saas-envoy-tutorial/ic776782.png "Envoy")</span><span class="sxs-lookup"><span data-stu-id="89952-168">![Envoy](./media/active-directory-saas-envoy-tutorial/ic776782.png "Envoy")</span></span>

9. <span data-ttu-id="89952-169">Нажмите **Компания**.</span><span class="sxs-lookup"><span data-stu-id="89952-169">Click **Company**.</span></span>

    <span data-ttu-id="89952-170">![Организация](./media/active-directory-saas-envoy-tutorial/ic776783.png "Организация")</span><span class="sxs-lookup"><span data-stu-id="89952-170">![Company](./media/active-directory-saas-envoy-tutorial/ic776783.png "Company")</span></span>

10. <span data-ttu-id="89952-171">Нажмите кнопку **SAML**.</span><span class="sxs-lookup"><span data-stu-id="89952-171">Click **SAML**.</span></span>

    <span data-ttu-id="89952-172">![SAML](./media/active-directory-saas-envoy-tutorial/ic776784.png "SAML")</span><span class="sxs-lookup"><span data-stu-id="89952-172">![SAML](./media/active-directory-saas-envoy-tutorial/ic776784.png "SAML")</span></span>

11. <span data-ttu-id="89952-173">В разделе конфигурации **Проверка подлинности SAML** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="89952-173">In the **SAML Authentication** configuration section, perform the following steps:</span></span>

    <span data-ttu-id="89952-174">![Аутентификация SAML](./media/active-directory-saas-envoy-tutorial/ic776785.png "Аутентификация SAML")</span><span class="sxs-lookup"><span data-stu-id="89952-174">![SAML authentication](./media/active-directory-saas-envoy-tutorial/ic776785.png "SAML authentication")</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="89952-175">Значение для идентификатора расположения штаб-квартиры автоматически создается приложением.</span><span class="sxs-lookup"><span data-stu-id="89952-175">The value for the HQ location ID is auto generated by the application.</span></span>
    
    <span data-ttu-id="89952-176">а.</span><span class="sxs-lookup"><span data-stu-id="89952-176">a.</span></span> <span data-ttu-id="89952-177">В текстовое поле **Fingerprint** (Отпечаток) вставьте значение **Отпечаток**, которое вы скопировали на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="89952-177">In **Fingerprint** textbox, paste the **Thumbprint** value of certificate, which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="89952-178">b.</span><span class="sxs-lookup"><span data-stu-id="89952-178">b.</span></span> <span data-ttu-id="89952-179">Вставьте значение **SAML Single Sign-On Service URL** (URL-адрес службы единого входа SAML), скопированное на портале Azure, в текстовое поле **IDENTITY PROVIDER HTTP SAML URL** (URL-адрес входа поставщика удостоверений HTTP).</span><span class="sxs-lookup"><span data-stu-id="89952-179">Paste **SAML Single Sign-On Service URL** value, which you have copied form the Azure portal into the **IDENTITY PROVIDER HTTP SAML URL** textbox.</span></span>
    
    <span data-ttu-id="89952-180">c.</span><span class="sxs-lookup"><span data-stu-id="89952-180">c.</span></span> <span data-ttu-id="89952-181">Нажмите кнопку **Сохранить изменения**.</span><span class="sxs-lookup"><span data-stu-id="89952-181">Click **Save changes**.</span></span>

> [!TIP]
> <span data-ttu-id="89952-182">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="89952-182">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="89952-183">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="89952-183">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="89952-184">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="89952-184">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="89952-185">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="89952-185">Create an Azure AD test user</span></span>

<span data-ttu-id="89952-186">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="89952-186">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="89952-188">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="89952-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="89952-189">На портале Azure в области слева нажмите кнопку **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="89952-189">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Кнопка "Azure Active Directory"](./media/active-directory-saas-envoy-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="89952-191">Чтобы открыть список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="89952-191">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Ссылки "Пользователи и группы" и "Все пользователи"](./media/active-directory-saas-envoy-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="89952-193">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна **Все пользователи** щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="89952-193">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Кнопка "Добавить"](./media/active-directory-saas-envoy-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="89952-195">В диалоговом окне **Пользователь** сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="89952-195">In the **User** dialog box, perform the following steps:</span></span>

    ![Диалоговое окно "Пользователь"](./media/active-directory-saas-envoy-tutorial/create_aaduser_04.png)

    <span data-ttu-id="89952-197">а.</span><span class="sxs-lookup"><span data-stu-id="89952-197">a.</span></span> <span data-ttu-id="89952-198">В поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="89952-198">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="89952-199">b.</span><span class="sxs-lookup"><span data-stu-id="89952-199">b.</span></span> <span data-ttu-id="89952-200">В поле **Имя пользователя** введите адрес электронной почты для пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="89952-200">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="89952-201">c.</span><span class="sxs-lookup"><span data-stu-id="89952-201">c.</span></span> <span data-ttu-id="89952-202">Установите флажок **Показать пароль** и запишите значение, которое отображается в поле **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="89952-202">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="89952-203">г)</span><span class="sxs-lookup"><span data-stu-id="89952-203">d.</span></span> <span data-ttu-id="89952-204">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="89952-204">Click **Create**.</span></span>
 
### <a name="create-an-envoy-test-user"></a><span data-ttu-id="89952-205">Создание тестового пользователя Envoy</span><span class="sxs-lookup"><span data-stu-id="89952-205">Create an Envoy test user</span></span>

<span data-ttu-id="89952-206">Элемент действия для настройки подготовки пользователей в Envoy отсутствует.</span><span class="sxs-lookup"><span data-stu-id="89952-206">There is no action item for you to configure user provisioning to Envoy.</span></span> <span data-ttu-id="89952-207">Когда назначенный пользователь пытается войти в Envoy с помощью панели доступа, Envoy проверяет, существует ли данный пользователь.</span><span class="sxs-lookup"><span data-stu-id="89952-207">When an assigned user tries to log into Envoy using the access panel, Envoy checks whether the user exists.</span></span> <span data-ttu-id="89952-208">Если учетная запись пользователя отсутствует, Envoy автоматически создает ее.</span><span class="sxs-lookup"><span data-stu-id="89952-208">If there is no user account available yet, it is automatically created by Envoy.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="89952-209">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="89952-209">Assign the Azure AD test user</span></span>

<span data-ttu-id="89952-210">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure путем предоставления доступа к Envoy.</span><span class="sxs-lookup"><span data-stu-id="89952-210">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Envoy.</span></span>

![Назначение роли пользователя][200] 

<span data-ttu-id="89952-212">**Чтобы назначить пользователя Britta Simon в Envoy, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="89952-212">**To assign Britta Simon to Envoy, perform the following steps:**</span></span>

1. <span data-ttu-id="89952-213">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="89952-213">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="89952-215">В списке приложений выберите **Envoy**.</span><span class="sxs-lookup"><span data-stu-id="89952-215">In the applications list, select **Envoy**.</span></span>

    ![Ссылка на Envoy в списке "Приложения"](./media/active-directory-saas-envoy-tutorial/tutorial_envoy_app.png)  

3. <span data-ttu-id="89952-217">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="89952-217">In the menu on the left, click **Users and groups**.</span></span>

    ![Ссылка "Пользователи и группы"][202]

4. <span data-ttu-id="89952-219">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="89952-219">Click **Add** button.</span></span> <span data-ttu-id="89952-220">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="89952-220">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Область "Добавление назначения"][203]

5. <span data-ttu-id="89952-222">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="89952-222">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="89952-223">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="89952-223">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="89952-224">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="89952-224">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="89952-225">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="89952-225">Test single sign-on</span></span>

<span data-ttu-id="89952-226">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="89952-226">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="89952-227">Щелкнув элемент Envoy на панели доступа, вы автоматически войдете в приложение Envoy.</span><span class="sxs-lookup"><span data-stu-id="89952-227">When you click the Envoy tile in the Access Panel, you should get automatically signed-on to your Envoy application.</span></span>
<span data-ttu-id="89952-228">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="89952-228">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="89952-229">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="89952-229">Additional resources</span></span>

* [<span data-ttu-id="89952-230">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="89952-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="89952-231">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="89952-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-envoy-tutorial/tutorial_general_203.png

