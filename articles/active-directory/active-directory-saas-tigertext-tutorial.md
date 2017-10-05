---
title: "Руководство по интеграции Azure Active Directory с TigerText Secure Messenger | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и TigerText Secure Messenger."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 03f1e128-5bcb-4e49-b6a3-fe22eedc6d5e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: jeedes
ms.openlocfilehash: e101e5fc84b032b66dd0636bab8bff128791f77c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tigertext-secure-messenger"></a><span data-ttu-id="c9f17-103">Руководство по интеграции Azure Active Directory с TigerText Secure Messenger</span><span class="sxs-lookup"><span data-stu-id="c9f17-103">Tutorial: Azure Active Directory integration with TigerText Secure Messenger</span></span>

<span data-ttu-id="c9f17-104">В этом руководстве описано, как интегрировать приложение TigerText Secure Messenger с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c9f17-104">In this tutorial, you learn how to integrate TigerText Secure Messenger with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c9f17-105">Интеграция Azure AD с приложением TigerText Secure Messenger обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="c9f17-105">Integrating TigerText Secure Messenger with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c9f17-106">С помощью Azure AD вы можете контролировать доступ к TigerText Secure Messenger.</span><span class="sxs-lookup"><span data-stu-id="c9f17-106">You can control in Azure AD who has access to TigerText Secure Messenger</span></span>
- <span data-ttu-id="c9f17-107">Вы можете включить автоматический вход пользователей в TigerText Secure Messenger (единый вход) с помощью их учетных записей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c9f17-107">You can enable your users to automatically get signed-on to TigerText Secure Messenger (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c9f17-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="c9f17-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c9f17-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c9f17-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c9f17-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c9f17-110">Prerequisites</span></span>

<span data-ttu-id="c9f17-111">Чтобы настроить интеграцию Azure AD с TigerText Secure Messenger, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="c9f17-111">To configure Azure AD integration with TigerText Secure Messenger, you need the following items:</span></span>

- <span data-ttu-id="c9f17-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="c9f17-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c9f17-113">подписка TigerText Secure Messenger с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="c9f17-113">A TigerText Secure Messenger single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c9f17-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="c9f17-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c9f17-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="c9f17-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c9f17-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="c9f17-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c9f17-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c9f17-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c9f17-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="c9f17-118">Scenario description</span></span>
<span data-ttu-id="c9f17-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="c9f17-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c9f17-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="c9f17-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c9f17-121">Добавление TigerText Secure Messenger из коллекции</span><span class="sxs-lookup"><span data-stu-id="c9f17-121">Add TigerText Secure Messenger from the gallery</span></span>
2. <span data-ttu-id="c9f17-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="c9f17-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-tigertext-secure-messenger-from-the-gallery"></a><span data-ttu-id="c9f17-123">Добавление TigerText Secure Messenger из коллекции</span><span class="sxs-lookup"><span data-stu-id="c9f17-123">Add TigerText Secure Messenger from the gallery</span></span>
<span data-ttu-id="c9f17-124">Чтобы настроить интеграцию TigerText Secure Messenger с Azure AD, необходимо добавить TigerText Secure Messenger из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="c9f17-124">To configure the integration of TigerText Secure Messenger into Azure AD, you need to add TigerText Secure Messenger from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c9f17-125">**Чтобы добавить TigerText Secure Messenger из коллекции, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="c9f17-125">**To add TigerText Secure Messenger from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c9f17-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c9f17-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c9f17-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="c9f17-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c9f17-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="c9f17-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="c9f17-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="c9f17-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="c9f17-133">В поле поиска введите **TigerText Secure Messenger**, выберите **TigerText Secure Messenger** на панели результатов и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="c9f17-133">In the search box, type **TigerText Secure Messenger**, select **TigerText Secure Messenger** from result panel then click **Add** button to add the application.</span></span>

    ![Добавление из коллекции](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="c9f17-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="c9f17-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="c9f17-136">В этом разделе описана настройка и проверка единого входа Azure AD в TigerText Secure Messenger с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c9f17-136">In this section, you configure and test Azure AD single sign-on with TigerText Secure Messenger based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c9f17-137">Для работы единого входа в Azure AD необходимо знать, какой пользователь в TigerText Secure Messenger соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c9f17-137">For single sign-on to work, Azure AD needs to know what the counterpart user in TigerText Secure Messenger is to a user in Azure AD.</span></span> <span data-ttu-id="c9f17-138">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в TigerText Secure Messenger.</span><span class="sxs-lookup"><span data-stu-id="c9f17-138">In other words, a link relationship between an Azure AD user and the related user in TigerText Secure Messenger needs to be established.</span></span>

<span data-ttu-id="c9f17-139">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в TigerText Secure Messenger.</span><span class="sxs-lookup"><span data-stu-id="c9f17-139">In TigerText Secure Messenger, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c9f17-140">Чтобы настроить и проверить единый вход Azure AD в TigerText Secure Messenger, выполните действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="c9f17-140">To configure and test Azure AD single sign-on with TigerText Secure Messenger, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c9f17-141">**[Настройка единого входа Azure AD](#configure-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="c9f17-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c9f17-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c9f17-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c9f17-143">**[Создание тестового пользователя TigerText Secure Messenger](#create-a-tigertext-secure-messenger-test-user)** требуется для того, чтобы в TigerText Secure Messenger существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c9f17-143">**[Create a TigerText Secure Messenger test user](#create-a-tigertext-secure-messenger-test-user)** - to have a counterpart of Britta Simon in TigerText Secure Messenger that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c9f17-144">**[Назначение тестового пользователя Azure AD](#assign-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c9f17-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c9f17-145">**[Проверка единого входа](#test-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="c9f17-145">**[Test Single Sign-On](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="c9f17-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="c9f17-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="c9f17-147">В этом разделе мы включим на портале Azure единый вход Azure AD и настроим его в приложении TigerText Secure Messenger.</span><span class="sxs-lookup"><span data-stu-id="c9f17-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TigerText Secure Messenger application.</span></span>

<span data-ttu-id="c9f17-148">**Чтобы настроить единый вход Azure AD в TigerText Secure Messenger, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="c9f17-148">**To configure Azure AD single sign-on with TigerText Secure Messenger, perform the following steps:**</span></span>

1. <span data-ttu-id="c9f17-149">На портале Azure на странице интеграции с приложением **TigerText Secure Messenger** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="c9f17-149">In the Azure portal, on the **TigerText Secure Messenger** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="c9f17-151">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="c9f17-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Параметр "Вход на основе SAML"](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_samlbase.png)

3. <span data-ttu-id="c9f17-153">В разделе **Домены и URL-адреса приложения TigerText Secure Messenger** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="c9f17-153">On the **TigerText Secure Messenger Domain and URLs** section, perform the following steps:</span></span>

    ![Раздел "Домены и URL-адреса приложения TigerText Secure Messenger"](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_url.png)

    <span data-ttu-id="c9f17-155">а.</span><span class="sxs-lookup"><span data-stu-id="c9f17-155">a.</span></span> <span data-ttu-id="c9f17-156">В текстовое поле **URL-адрес для входа** введите URL-адрес в формате `https://home.tigertext.com`.</span><span class="sxs-lookup"><span data-stu-id="c9f17-156">In the **Sign-on URL** textbox, type URL as: `https://home.tigertext.com`</span></span>

    <span data-ttu-id="c9f17-157">b.</span><span class="sxs-lookup"><span data-stu-id="c9f17-157">b.</span></span> <span data-ttu-id="c9f17-158">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://saml-lb.tigertext.me/v1/organization/<instance Id>`</span><span class="sxs-lookup"><span data-stu-id="c9f17-158">In the **Identifier** textbox, type a URL using the following pattern: `https://saml-lb.tigertext.me/v1/organization/<instance Id>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c9f17-159">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="c9f17-159">This value is not real.</span></span> <span data-ttu-id="c9f17-160">Вместо него нужно указать фактический идентификатор.</span><span class="sxs-lookup"><span data-stu-id="c9f17-160">Update this value with the actual Identifier.</span></span> <span data-ttu-id="c9f17-161">Чтобы получить это значение, обратитесь к [группе поддержки клиентов TigerText Secure Messenger](mailTo:prosupport@tigertext.com).</span><span class="sxs-lookup"><span data-stu-id="c9f17-161">Contact [TigerText Secure Messenger Client support team](mailTo:prosupport@tigertext.com) to get this value.</span></span> 
 
4. <span data-ttu-id="c9f17-162">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="c9f17-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Раздел "Сертификат подписи SAML"](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_certificate.png) 

5. <span data-ttu-id="c9f17-164">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="c9f17-164">Click **Save** button.</span></span>

    ![Кнопка "Сохранить"](./media/active-directory-saas-tigertext-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="c9f17-166">Для настройки единого входа в вашем приложении обратитесь в [службу поддержки TigerText Secure Messenger](mailTo:prosupport@tigertext.com) и предоставьте **скачанный файл метаданных**.</span><span class="sxs-lookup"><span data-stu-id="c9f17-166">To get single sign-on configured for your application, contact [TigerText Secure Messenger support team](mailTo:prosupport@tigertext.com) and provide them the **Downloaded metadata**.</span></span>

> [!TIP]
> <span data-ttu-id="c9f17-167">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="c9f17-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c9f17-168">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="c9f17-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c9f17-169">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="c9f17-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="c9f17-170">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="c9f17-170">Create an Azure AD test user</span></span>
<span data-ttu-id="c9f17-171">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c9f17-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="c9f17-173">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="c9f17-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c9f17-174">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c9f17-174">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-tigertext-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c9f17-176">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="c9f17-176">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    !["Пользователи и группы" -> "Все пользователи"](./media/active-directory-saas-tigertext-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c9f17-178">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="c9f17-178">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Кнопка "Добавить"](./media/active-directory-saas-tigertext-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c9f17-180">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="c9f17-180">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Диалоговое окно пользователя](./media/active-directory-saas-tigertext-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c9f17-182">а.</span><span class="sxs-lookup"><span data-stu-id="c9f17-182">a.</span></span> <span data-ttu-id="c9f17-183">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c9f17-183">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c9f17-184">b.</span><span class="sxs-lookup"><span data-stu-id="c9f17-184">b.</span></span> <span data-ttu-id="c9f17-185">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c9f17-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c9f17-186">c.</span><span class="sxs-lookup"><span data-stu-id="c9f17-186">c.</span></span> <span data-ttu-id="c9f17-187">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="c9f17-187">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c9f17-188">d.</span><span class="sxs-lookup"><span data-stu-id="c9f17-188">d.</span></span> <span data-ttu-id="c9f17-189">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="c9f17-189">Click **Create**.</span></span>
 
### <a name="create-a-tigertext-secure-messenger-test-user"></a><span data-ttu-id="c9f17-190">Создание тестового пользователя TigerText Secure Messenger</span><span class="sxs-lookup"><span data-stu-id="c9f17-190">Create a TigerText Secure Messenger test user</span></span>

<span data-ttu-id="c9f17-191">В этом разделе описано, как создать пользователя Britta Simon в приложении TigerText.</span><span class="sxs-lookup"><span data-stu-id="c9f17-191">In this section, you create a user called Britta Simon in TigerText.</span></span> <span data-ttu-id="c9f17-192">Обратитесь в [службу поддержки TigerText Secure Messenger](mailTo:prosupport@tigertext.com), чтобы добавить пользователей для платформы TigerText.</span><span class="sxs-lookup"><span data-stu-id="c9f17-192">Please reach out to [TigerText Secure Messenger Client support team](mailTo:prosupport@tigertext.com) to add the users in the TigerText platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="c9f17-193">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="c9f17-193">Assign the Azure AD test user</span></span>

<span data-ttu-id="c9f17-194">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив доступ к TigerText Secure Messenger.</span><span class="sxs-lookup"><span data-stu-id="c9f17-194">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TigerText Secure Messenger.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="c9f17-196">**Чтобы назначить пользователя Britta Simon в TigerText Secure Messenger, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="c9f17-196">**To assign Britta Simon to TigerText Secure Messenger, perform the following steps:**</span></span>

1. <span data-ttu-id="c9f17-197">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="c9f17-197">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="c9f17-199">В списке приложений выберите **TigerText Secure Messenger**.</span><span class="sxs-lookup"><span data-stu-id="c9f17-199">In the applications list, select **TigerText Secure Messenger**.</span></span>

    ![TigerText Secure Messenger в списке приложений](./media/active-directory-saas-tigertext-tutorial/tutorial_tigertext_app.png) 

3. <span data-ttu-id="c9f17-201">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="c9f17-201">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="c9f17-203">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="c9f17-203">Click **Add** button.</span></span> <span data-ttu-id="c9f17-204">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="c9f17-204">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="c9f17-206">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="c9f17-206">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c9f17-207">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="c9f17-207">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c9f17-208">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="c9f17-208">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="c9f17-209">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="c9f17-209">Test single sign-on</span></span>

<span data-ttu-id="c9f17-210">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="c9f17-210">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c9f17-211">Щелкнув элемент TigerText на панели доступа, вы автоматически войдете в приложение TigerText.</span><span class="sxs-lookup"><span data-stu-id="c9f17-211">When you click the TigerText tile in the Access Panel, you should get automatically signed-on to your TigerText application.</span></span> <span data-ttu-id="c9f17-212">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c9f17-212">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c9f17-213">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="c9f17-213">Additional resources</span></span>

* [<span data-ttu-id="c9f17-214">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c9f17-214">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c9f17-215">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c9f17-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tigertext-tutorial/tutorial_general_203.png

