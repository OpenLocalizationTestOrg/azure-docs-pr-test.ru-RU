---
title: "Руководство по интеграции Azure Active Directory с 10,000ft Plans | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в 10,000ft Plans."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b60c955e-8fa3-4872-a897-c4e81fd7beac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: c81a6adb3abad58af149bbef6f5dff736c142f51
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-10000ft-plans"></a><span data-ttu-id="462c9-103">Учебник. Интеграция Azure Active Directory с 10,000ft Plans</span><span class="sxs-lookup"><span data-stu-id="462c9-103">Tutorial: Azure Active Directory integration with 10,000ft Plans</span></span>

<span data-ttu-id="462c9-104">В этом учебнике описано, как интегрировать приложение 10,000ft Plans с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="462c9-104">In this tutorial, you learn how to integrate 10,000ft Plans with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="462c9-105">Интеграция 10,000ft Plans с Azure AD обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="462c9-105">Integrating 10,000ft Plans with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="462c9-106">С помощью Azure AD вы можете контролировать доступ к 10,000ft Plans.</span><span class="sxs-lookup"><span data-stu-id="462c9-106">You can control in Azure AD who has access to 10,000ft Plans</span></span>
- <span data-ttu-id="462c9-107">Вы можете включить автоматический вход пользователей в 10,000ft Plans (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="462c9-107">You can enable your users to automatically get signed-on to 10,000ft Plans (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="462c9-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="462c9-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="462c9-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="462c9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="462c9-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="462c9-110">Prerequisites</span></span>

<span data-ttu-id="462c9-111">Чтобы настроить интеграцию Azure AD с 10,000ft Plans, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="462c9-111">To configure Azure AD integration with 10,000ft Plans, you need the following items:</span></span>

- <span data-ttu-id="462c9-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="462c9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="462c9-113">подписка 10,000ft Plans с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="462c9-113">A 10,000ft Plans single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="462c9-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="462c9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="462c9-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="462c9-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="462c9-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="462c9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="462c9-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="462c9-117">If you don't have an Azure AD trial environment, you can get a one-month trial here [trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="462c9-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="462c9-118">Scenario description</span></span>
<span data-ttu-id="462c9-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="462c9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="462c9-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="462c9-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="462c9-121">Добавление 10,000ft Plans из коллекции</span><span class="sxs-lookup"><span data-stu-id="462c9-121">Adding 10,000ft Plans from the gallery</span></span>
2. <span data-ttu-id="462c9-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="462c9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-10000ft-plans-from-the-gallery"></a><span data-ttu-id="462c9-123">Добавление 10,000ft Plans из коллекции</span><span class="sxs-lookup"><span data-stu-id="462c9-123">Adding 10,000ft Plans from the gallery</span></span>
<span data-ttu-id="462c9-124">Чтобы настроить интеграцию 10,000ft Plans с Azure AD, необходимо добавить 10,000ft Plans из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="462c9-124">To configure the integration of 10,000ft Plans into Azure AD, you need to add 10,000ft Plans from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="462c9-125">**Чтобы добавить 10,000ft Plans из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="462c9-125">**To add 10,000ft Plans from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="462c9-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="462c9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="462c9-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="462c9-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="462c9-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="462c9-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="462c9-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="462c9-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="462c9-133">В поле поиска введите **10,000ft Plans**.</span><span class="sxs-lookup"><span data-stu-id="462c9-133">In the search box, type **10,000ft Plans**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_search.png)

5. <span data-ttu-id="462c9-135">На панели результатов выберите **10,000ft Plans** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="462c9-135">In the results panel, select **10,000ft Plans**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="462c9-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="462c9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="462c9-138">В этом разделе описана настройка и проверка единого входа Azure AD в 10,000ft Plans с помощью тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="462c9-138">In this section, you configure and test Azure AD single sign-on with 10,000ft Plans based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="462c9-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в 10,000ft Plans соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="462c9-139">For single sign-on to work, Azure AD needs to know what the counterpart user in 10,000ft Plans is to a user in Azure AD.</span></span> <span data-ttu-id="462c9-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в 10,000ft Plans.</span><span class="sxs-lookup"><span data-stu-id="462c9-140">In other words, a link relationship between an Azure AD user and the related user in 10,000ft Plans needs to be established.</span></span>

<span data-ttu-id="462c9-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в 10,000ft Plans.</span><span class="sxs-lookup"><span data-stu-id="462c9-141">In 10,000ft Plans, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="462c9-142">Чтобы настроить и проверить единый вход Azure AD в 10,000ft Plans, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="462c9-142">To configure and test Azure AD single sign-on with 10,000ft Plans, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="462c9-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="462c9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="462c9-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="462c9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="462c9-145">**[Создание тестового пользователя 10,000ft Plans](#creating-a-10000ft-plans-test-user)** требуется для создания пользователя Britta Simon в 10,000ft Plans, связанного с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="462c9-145">**[Creating a 10,000ft Plans test user](#creating-a-10000ft-plans-test-user)** - to have a counterpart of Britta Simon in 10,000ft Plans that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="462c9-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="462c9-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="462c9-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="462c9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="462c9-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="462c9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="462c9-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении 10,000ft Plans.</span><span class="sxs-lookup"><span data-stu-id="462c9-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your 10,000ft Plans application.</span></span>

<span data-ttu-id="462c9-150">**Чтобы настроить единый вход Azure AD в 10,000ft Plans, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="462c9-150">**To configure Azure AD single sign-on with 10,000ft Plans, perform the following steps:**</span></span>

1. <span data-ttu-id="462c9-151">На портале Azure на странице интеграции с приложением **10,000ft Plans** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="462c9-151">In the Azure portal, on the **10,000ft Plans** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="462c9-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="462c9-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_samlbase.png)

3. <span data-ttu-id="462c9-155">В разделе **Домены и URL-адреса приложения 10,000ft Plans** выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="462c9-155">On the **10,000ft Plans Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_url.png)

    <span data-ttu-id="462c9-157">а.</span><span class="sxs-lookup"><span data-stu-id="462c9-157">a.</span></span> <span data-ttu-id="462c9-158">В текстовом поле **URL-адрес для входа** введите URL-адрес: `https://app.10000ft.com`</span><span class="sxs-lookup"><span data-stu-id="462c9-158">In the **Sign-on URL** textbox, type the URL: `https://app.10000ft.com`</span></span>

    <span data-ttu-id="462c9-159">b.</span><span class="sxs-lookup"><span data-stu-id="462c9-159">b.</span></span> <span data-ttu-id="462c9-160">В текстовом поле **Идентификатор** введите URL-адрес: `https://app.10000ft.com/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="462c9-160">In the **Identifier** textbox, type the URL: `https://app.10000ft.com/saml/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="462c9-161">Значение для **идентификатора** отличается, если у вас есть личный домен.</span><span class="sxs-lookup"><span data-stu-id="462c9-161">The value for **Identifier** is different if you have a custom domain.</span></span> <span data-ttu-id="462c9-162">Чтобы получить это значение, обратитесь в [службу поддержки 10,000ft Plans](https://www.10000ft.com/plans/support).</span><span class="sxs-lookup"><span data-stu-id="462c9-162">Contact [10,000ft Plans support team](https://www.10000ft.com/plans/support) to get this value.</span></span> 
 
4. <span data-ttu-id="462c9-163">В разделе **Сертификат подписи SAML** щелкните **Сертификат (необработанный)**, а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="462c9-163">On the **SAML Signing Certificate** section, click **Certificate(Raw)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_certificate.png) 

5. <span data-ttu-id="462c9-165">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="462c9-165">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="462c9-167">В разделе **Настройка 10,000ft Plans** щелкните **Настроить 10,000ft Plans**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="462c9-167">On the **10,000ft Plans Configuration** section, click **Configure 10,000ft Plans** to open **Configure sign-on** window.</span></span> <span data-ttu-id="462c9-168">Скопируйте **URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML**  из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="462c9-168">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_configure.png) 

7. <span data-ttu-id="462c9-170">Чтобы настроить единый вход на стороне **10,000ft Plans**, нужно отправить скачанный **сертификат (необработанный), URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML** в [службу поддержки 10,000ft Plans](https://www.10000ft.com/plans/support).</span><span class="sxs-lookup"><span data-stu-id="462c9-170">To configure single sign-on on **10,000ft Plans** side, you need to send the downloaded **Certificate(Raw), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [10,000ft Plans support team](https://www.10000ft.com/plans/support).</span></span>

> [!TIP]
> <span data-ttu-id="462c9-171">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="462c9-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="462c9-172">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="462c9-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="462c9-173">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="462c9-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="462c9-174">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="462c9-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="462c9-175">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="462c9-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="462c9-177">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="462c9-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="462c9-178">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="462c9-178">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-10000ftplans-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="462c9-180">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="462c9-180">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-10000ftplans-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="462c9-182">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="462c9-182">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-10000ftplans-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="462c9-184">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="462c9-184">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-10000ftplans-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="462c9-186">а.</span><span class="sxs-lookup"><span data-stu-id="462c9-186">a.</span></span> <span data-ttu-id="462c9-187">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="462c9-187">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="462c9-188">b.</span><span class="sxs-lookup"><span data-stu-id="462c9-188">b.</span></span> <span data-ttu-id="462c9-189">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="462c9-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="462c9-190">c.</span><span class="sxs-lookup"><span data-stu-id="462c9-190">c.</span></span> <span data-ttu-id="462c9-191">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="462c9-191">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="462c9-192">d.</span><span class="sxs-lookup"><span data-stu-id="462c9-192">d.</span></span> <span data-ttu-id="462c9-193">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="462c9-193">Click **Create**.</span></span>
 
### <a name="creating-a-10000ft-plans-test-user"></a><span data-ttu-id="462c9-194">Создание тестового пользователя 10,000ft Plans</span><span class="sxs-lookup"><span data-stu-id="462c9-194">Creating a 10,000ft Plans test user</span></span>

<span data-ttu-id="462c9-195">Цель этого раздела — создать пользователя с именем Britta Simon в 10,000ft Plans.</span><span class="sxs-lookup"><span data-stu-id="462c9-195">The objective of this section is to create a user called Britta Simon in 10,000ft Plans.</span></span> <span data-ttu-id="462c9-196">Приложение 10,000ft Plans поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="462c9-196">10,000ft Plans supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="462c9-197">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="462c9-197">There is no action item for you in this section.</span></span> <span data-ttu-id="462c9-198">При попытке получить доступ к 10,000ft Plans создается пользователь (если он еще не создан).</span><span class="sxs-lookup"><span data-stu-id="462c9-198">A new user is created during an attempt to access 10,000ft Plans if it doesn't exist yet.</span></span> 

> [!NOTE]
> <span data-ttu-id="462c9-199">Если вам нужно вручную создать пользователя, обратитесь в [службу поддержки 10,000ft Plans](https://www.10000ft.com/plans/support).</span><span class="sxs-lookup"><span data-stu-id="462c9-199">If you need to create a user manually, you need to contact the [10,000ft Plans support team](https://www.10000ft.com/plans/support).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="462c9-200">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="462c9-200">Assigning the Azure AD test user</span></span>

<span data-ttu-id="462c9-201">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив ему доступ к 10,000ft Plans.</span><span class="sxs-lookup"><span data-stu-id="462c9-201">In this section, you enable Britta Simon to use Azure single sign-on by granting access to 10,000ft Plans.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="462c9-203">**Чтобы назначить пользователя Britta Simon в 10,000ft Plans, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="462c9-203">**To assign Britta Simon to 10,000ft Plans, perform the following steps:**</span></span>

1. <span data-ttu-id="462c9-204">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="462c9-204">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="462c9-206">В списке приложений выберите **10,000ft Plans**.</span><span class="sxs-lookup"><span data-stu-id="462c9-206">In the applications list, select **10,000ft Plans**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-10000ftplans-tutorial/tutorial_10,000ftplans_app.png) 

3. <span data-ttu-id="462c9-208">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="462c9-208">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="462c9-210">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="462c9-210">Click **Add** button.</span></span> <span data-ttu-id="462c9-211">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="462c9-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="462c9-213">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="462c9-213">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="462c9-214">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="462c9-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="462c9-215">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="462c9-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="462c9-216">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="462c9-216">Testing single sign-on</span></span>

<span data-ttu-id="462c9-217">Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="462c9-217">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="462c9-218">Щелкнув элемент 10,000ft Plans на панели доступа, вы автоматически войдете в приложение 10,000ft Plans.</span><span class="sxs-lookup"><span data-stu-id="462c9-218">When you click the 10,000ft Plans tile in the Access Panel, you should get automatically signed-on to your 10,000ft Plans application.</span></span>
 
## <a name="additional-resources"></a><span data-ttu-id="462c9-219">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="462c9-219">Additional resources</span></span>

* [<span data-ttu-id="462c9-220">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="462c9-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="462c9-221">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="462c9-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-10000ftplans-tutorial/tutorial_general_203.png

