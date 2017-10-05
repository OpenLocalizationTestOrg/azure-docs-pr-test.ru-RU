---
title: "Руководство по интеграции Azure Active Directory с Blackboard Learn — Shibboleth | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в Blackboard Learn — Shibboleth."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e435cbb4-c0f0-400e-943c-5c923fa8ddf2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: jeedes
ms.openlocfilehash: 014b0671eb8604235a823c2cf4324a49d94df702
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-blackboard-learn---shibboleth"></a><span data-ttu-id="3d0a8-103">Руководство. Интеграция Azure Active Directory с Blackboard Learn — Shibboleth</span><span class="sxs-lookup"><span data-stu-id="3d0a8-103">Tutorial: Azure Active Directory integration with Blackboard Learn - Shibboleth</span></span>

<span data-ttu-id="3d0a8-104">В этом руководстве описано, как интегрировать Blackboard Learn — Shibboleth с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3d0a8-104">In this tutorial, you learn how to integrate Blackboard Learn - Shibboleth with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3d0a8-105">Интеграция Blackboard Learn — Shibboleth с Azure AD обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="3d0a8-105">Integrating Blackboard Learn - Shibboleth with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3d0a8-106">С помощью Azure AD вы можете контролировать доступ к Blackboard Learn — Shibboleth.</span><span class="sxs-lookup"><span data-stu-id="3d0a8-106">You can control in Azure AD who has access to Blackboard Learn - Shibboleth</span></span>
- <span data-ttu-id="3d0a8-107">Вы можете включить автоматический вход пользователей в Blackboard Learn — Shibboleth (единый вход) с использованием учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3d0a8-107">You can enable your users to automatically get signed-on to Blackboard Learn - Shibboleth (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3d0a8-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="3d0a8-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="3d0a8-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3d0a8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3d0a8-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="3d0a8-110">Prerequisites</span></span>

<span data-ttu-id="3d0a8-111">Чтобы настроить интеграцию Azure AD с Blackboard Learn — Shibboleth, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="3d0a8-111">To configure Azure AD integration with Blackboard Learn - Shibboleth, you need the following items:</span></span>

- <span data-ttu-id="3d0a8-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="3d0a8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3d0a8-113">подписка на Blackboard Learn — Shibboleth с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="3d0a8-113">A Blackboard Learn - Shibboleth single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3d0a8-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="3d0a8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3d0a8-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="3d0a8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3d0a8-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="3d0a8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3d0a8-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3d0a8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3d0a8-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="3d0a8-118">Scenario description</span></span>
<span data-ttu-id="3d0a8-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="3d0a8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3d0a8-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="3d0a8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3d0a8-121">Добавление Blackboard Learn — Shibboleth из коллекции</span><span class="sxs-lookup"><span data-stu-id="3d0a8-121">Adding Blackboard Learn - Shibboleth from the gallery</span></span>
2. <span data-ttu-id="3d0a8-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="3d0a8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-blackboard-learn---shibboleth-from-the-gallery"></a><span data-ttu-id="3d0a8-123">Добавление Blackboard Learn — Shibboleth из коллекции</span><span class="sxs-lookup"><span data-stu-id="3d0a8-123">Adding Blackboard Learn - Shibboleth from the gallery</span></span>
<span data-ttu-id="3d0a8-124">Чтобы настроить интеграцию Blackboard Learn — Shibboleth с Azure AD, необходимо добавить Blackboard Learn — Shibboleth из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="3d0a8-124">To configure the integration of Blackboard Learn - Shibboleth into Azure AD, you need to add Blackboard Learn - Shibboleth from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3d0a8-125">**Чтобы добавить Blackboard Learn — Shibboleth из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="3d0a8-125">**To add Blackboard Learn - Shibboleth from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3d0a8-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3d0a8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3d0a8-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="3d0a8-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3d0a8-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="3d0a8-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="3d0a8-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="3d0a8-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="3d0a8-133">В поле поиска введите **Blackboard Learn — Shibboleth**.</span><span class="sxs-lookup"><span data-stu-id="3d0a8-133">In the search box, type **Blackboard Learn - Shibboleth**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_search.png)

5. <span data-ttu-id="3d0a8-135">В области результатов выберите **Blackboard Learn — Shibboleth** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="3d0a8-135">In the results panel, select **Blackboard Learn - Shibboleth**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3d0a8-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="3d0a8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3d0a8-138">В этом разделе описана настройка и проверка единого входа Azure AD в Blackboard Learn — Shibboleth с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3d0a8-138">In this section, you configure and test Azure AD single sign-on with Blackboard Learn - Shibboleth based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="3d0a8-139">Для работы единого входа Azure AD необходимо знать, какой пользователь в Blackboard Learn — Shibboleth соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3d0a8-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Blackboard Learn - Shibboleth is to a user in Azure AD.</span></span> <span data-ttu-id="3d0a8-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Blackboard Learn — Shibboleth.</span><span class="sxs-lookup"><span data-stu-id="3d0a8-140">In other words, a link relationship between an Azure AD user and the related user in Blackboard Learn - Shibboleth needs to be established.</span></span>

<span data-ttu-id="3d0a8-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Blackboard Learn — Shibboleth.</span><span class="sxs-lookup"><span data-stu-id="3d0a8-141">In Blackboard Learn - Shibboleth, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="3d0a8-142">Чтобы настроить и проверить единый вход Azure AD в Blackboard Learn — Shibboleth, вам потребуется выполнить следующие действия.</span><span class="sxs-lookup"><span data-stu-id="3d0a8-142">To configure and test Azure AD single sign-on with Blackboard Learn - Shibboleth, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3d0a8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="3d0a8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3d0a8-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3d0a8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3d0a8-145">**[Создание тестового пользователя Blackboard Learn — Shibboleth](#creating-a-blackboard-learn---shibboleth-test-user)** нужно для того, чтобы в Blackboard Learn - Shibboleth также существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3d0a8-145">**[Creating a Blackboard Learn - Shibboleth test user](#creating-a-blackboard-learn---shibboleth-test-user)** - to have a counterpart of Britta Simon in Blackboard Learn - Shibboleth that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="3d0a8-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3d0a8-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3d0a8-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="3d0a8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3d0a8-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="3d0a8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3d0a8-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Blackboard Learn — Shibboleth.</span><span class="sxs-lookup"><span data-stu-id="3d0a8-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Blackboard Learn - Shibboleth application.</span></span>

<span data-ttu-id="3d0a8-150">**Чтобы настроить единый вход Azure AD в Blackboard Learn — Shibboleth, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="3d0a8-150">**To configure Azure AD single sign-on with Blackboard Learn - Shibboleth, perform the following steps:**</span></span>

1. <span data-ttu-id="3d0a8-151">На портале Azure на странице интеграции с приложением **Blackboard Learn — Shibboleth** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="3d0a8-151">In the Azure portal, on the **Blackboard Learn - Shibboleth** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="3d0a8-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="3d0a8-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_samlbase.png)

3. <span data-ttu-id="3d0a8-155">В разделе **Домены и URL-адреса приложения Blackboard Learn — Shibboleth** сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="3d0a8-155">On the **Blackboard Learn - Shibboleth Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_url.png)

    <span data-ttu-id="3d0a8-157">а.</span><span class="sxs-lookup"><span data-stu-id="3d0a8-157">a.</span></span> <span data-ttu-id="3d0a8-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<yourblackoardlearnserver>.blackboardlearn.com/Shibboleth.sso/Login`</span><span class="sxs-lookup"><span data-stu-id="3d0a8-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<yourblackoardlearnserver>.blackboardlearn.com/Shibboleth.sso/Login`</span></span>

    <span data-ttu-id="3d0a8-159">b.</span><span class="sxs-lookup"><span data-stu-id="3d0a8-159">b.</span></span> <span data-ttu-id="3d0a8-160">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<yourblackoardlearnserver>.blackboardlearn.com/shibboleth-sp`</span><span class="sxs-lookup"><span data-stu-id="3d0a8-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<yourblackoardlearnserver>.blackboardlearn.com/shibboleth-sp`</span></span>

    <span data-ttu-id="3d0a8-161">c.</span><span class="sxs-lookup"><span data-stu-id="3d0a8-161">c.</span></span> <span data-ttu-id="3d0a8-162">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате: `https://<yourblackoardlearnserver>.blackboardlearn.com/Shibboleth.sso/SAML2/POST`.</span><span class="sxs-lookup"><span data-stu-id="3d0a8-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://<yourblackoardlearnserver>.blackboardlearn.com/Shibboleth.sso/SAML2/POST`</span></span>
 
    > [!NOTE] 
    > <span data-ttu-id="3d0a8-163">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="3d0a8-163">These values are not real.</span></span> <span data-ttu-id="3d0a8-164">Замените их фактическими значениями идентификатора, URL-адреса ответа и URL-адреса входа.</span><span class="sxs-lookup"><span data-stu-id="3d0a8-164">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="3d0a8-165">Чтобы получить эти значения, обратитесь к [группе поддержки Blackboard Learn — Shibboleth](https://www.blackboard.com/forms/contact-us_form.aspx).</span><span class="sxs-lookup"><span data-stu-id="3d0a8-165">Contact [Blackboard Learn - Shibboleth Client support team](https://www.blackboard.com/forms/contact-us_form.aspx) to get these values.</span></span> 

4. <span data-ttu-id="3d0a8-166">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="3d0a8-166">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_certificate.png) 

5. <span data-ttu-id="3d0a8-168">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="3d0a8-168">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="3d0a8-170">В разделе **Конфигурация Blackboard Learn — Shibboleth** щелкните **Настроить Blackboard Learn — Shibboleth**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="3d0a8-170">On the **Blackboard Learn - Shibboleth Configuration** section, click **Configure Blackboard Learn - Shibboleth** to open **Configure sign-on** window.</span></span> <span data-ttu-id="3d0a8-171">Скопируйте **URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML**  из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="3d0a8-171">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_configure.png) 

7. <span data-ttu-id="3d0a8-173">Чтобы настроить единый вход на стороне **Blackboard Learn — Shibboleth**, нужно отправить скачанный **XML-файл метаданных**, **URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML** [группе поддержки Blackboard Learn — Shibboleth](https://www.blackboard.com/forms/contact-us_form.aspx).</span><span class="sxs-lookup"><span data-stu-id="3d0a8-173">To configure single sign-on on **Blackboard Learn - Shibboleth** side, you need to send the downloaded **Metadata XML** and **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Blackboard Learn - Shibboleth support team](https://www.blackboard.com/forms/contact-us_form.aspx).</span></span>

> [!TIP]
> <span data-ttu-id="3d0a8-174">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="3d0a8-174">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3d0a8-175">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="3d0a8-175">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3d0a8-176">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="3d0a8-176">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3d0a8-177">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="3d0a8-177">Creating an Azure AD test user</span></span>
<span data-ttu-id="3d0a8-178">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3d0a8-178">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="3d0a8-180">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="3d0a8-180">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3d0a8-181">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3d0a8-181">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3d0a8-183">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="3d0a8-183">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3d0a8-185">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="3d0a8-185">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3d0a8-187">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="3d0a8-187">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3d0a8-189">а.</span><span class="sxs-lookup"><span data-stu-id="3d0a8-189">a.</span></span> <span data-ttu-id="3d0a8-190">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3d0a8-190">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3d0a8-191">b.</span><span class="sxs-lookup"><span data-stu-id="3d0a8-191">b.</span></span> <span data-ttu-id="3d0a8-192">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="3d0a8-192">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3d0a8-193">c.</span><span class="sxs-lookup"><span data-stu-id="3d0a8-193">c.</span></span> <span data-ttu-id="3d0a8-194">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="3d0a8-194">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="3d0a8-195">d.</span><span class="sxs-lookup"><span data-stu-id="3d0a8-195">d.</span></span> <span data-ttu-id="3d0a8-196">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="3d0a8-196">Click **Create**.</span></span>
 
### <a name="creating-a-blackboard-learn---shibboleth-test-user"></a><span data-ttu-id="3d0a8-197">Создание тестового пользователя Blackboard Learn — Shibboleth</span><span class="sxs-lookup"><span data-stu-id="3d0a8-197">Creating a Blackboard Learn - Shibboleth test user</span></span>

<span data-ttu-id="3d0a8-198">В этом разделе описано, как создать пользователя Britta Simon в приложении Blackboard Learn — Shibboleth.</span><span class="sxs-lookup"><span data-stu-id="3d0a8-198">In this section, you create a user called Britta Simon in Blackboard Learn - Shibboleth.</span></span> <span data-ttu-id="3d0a8-199">Обратитесь к [группе поддержки Blackboard Learn — Shibboleth](https://www.blackboard.com/forms/contact-us_form.aspx), чтобы добавить пользователей на платформу Blackboard Learn — Shibboleth.</span><span class="sxs-lookup"><span data-stu-id="3d0a8-199">Work with your [Blackboard Learn - Shibboleth support team](https://www.blackboard.com/forms/contact-us_form.aspx) to add the users in the Blackboard Learn - Shibboleth platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="3d0a8-200">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="3d0a8-200">Assigning the Azure AD test user</span></span>

<span data-ttu-id="3d0a8-201">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к Blackboard Learn — Shibboleth.</span><span class="sxs-lookup"><span data-stu-id="3d0a8-201">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Blackboard Learn - Shibboleth.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="3d0a8-203">**Чтобы назначить пользователя Britta Simon в Blackboard Learn — Shibboleth, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="3d0a8-203">**To assign Britta Simon to Blackboard Learn - Shibboleth, perform the following steps:**</span></span>

1. <span data-ttu-id="3d0a8-204">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="3d0a8-204">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="3d0a8-206">В списке приложений выберите **Blackboard Learn — Shibboleth**.</span><span class="sxs-lookup"><span data-stu-id="3d0a8-206">In the applications list, select **Blackboard Learn - Shibboleth**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_blackboardlearn-shibboleth_app.png) 

3. <span data-ttu-id="3d0a8-208">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="3d0a8-208">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="3d0a8-210">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="3d0a8-210">Click **Add** button.</span></span> <span data-ttu-id="3d0a8-211">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="3d0a8-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="3d0a8-213">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="3d0a8-213">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3d0a8-214">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="3d0a8-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3d0a8-215">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="3d0a8-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3d0a8-216">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="3d0a8-216">Testing single sign-on</span></span>

<span data-ttu-id="3d0a8-217">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="3d0a8-217">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="3d0a8-218">Щелкнув плитку Blackboard Learn — Shibboleth на панели доступа, вы автоматически войдете в приложение Blackboard Learn — Shibboleth.</span><span class="sxs-lookup"><span data-stu-id="3d0a8-218">When you click the Blackboard Learn - Shibboleth tile in the Access Panel, you should get automatically signed-on to your Blackboard Learn - Shibboleth application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3d0a8-219">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="3d0a8-219">Additional resources</span></span>

* [<span data-ttu-id="3d0a8-220">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3d0a8-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3d0a8-221">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3d0a8-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-blackboard-learn-shibboleth-tutorial/tutorial_general_203.png

