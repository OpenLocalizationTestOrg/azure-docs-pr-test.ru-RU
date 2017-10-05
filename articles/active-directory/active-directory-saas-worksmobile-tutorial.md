---
title: "Руководство. Интеграция Azure Active Directory с WORKS MOBILE | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в WORKS MOBILE."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 725f32fd-d0ad-49c7-b137-1cc246bf85d7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 139a1968a59424eae278de3e7fa227ad340a1eb8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-works-mobile"></a><span data-ttu-id="e4265-103">Руководство. Интеграция Azure Active Directory с WORKS MOBILE</span><span class="sxs-lookup"><span data-stu-id="e4265-103">Tutorial: Azure Active Directory integration with WORKS MOBILE</span></span>

<span data-ttu-id="e4265-104">В этом руководстве описано, как интегрировать WORKS MOBILE с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e4265-104">In this tutorial, you learn how to integrate WORKS MOBILE with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e4265-105">Интеграция WORKS MOBILE с Azure AD обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="e4265-105">Integrating WORKS MOBILE with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e4265-106">С помощью Azure AD вы можете контролировать доступ к WORKS MOBILE.</span><span class="sxs-lookup"><span data-stu-id="e4265-106">You can control in Azure AD who has access to WORKS MOBILE</span></span>
- <span data-ttu-id="e4265-107">Вы можете настроить автоматический вход пользователей в WORKS MOBILE (единый вход) под учетными записями Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e4265-107">You can enable your users to automatically get signed-on to WORKS MOBILE (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e4265-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="e4265-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e4265-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в статье [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e4265-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e4265-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="e4265-110">Prerequisites</span></span>

<span data-ttu-id="e4265-111">Чтобы настроить интеграцию Azure AD с WORKS MOBILE, вам потребуются:</span><span class="sxs-lookup"><span data-stu-id="e4265-111">To configure Azure AD integration with WORKS MOBILE, you need the following items:</span></span>

- <span data-ttu-id="e4265-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="e4265-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e4265-113">подписка WORKS MOBILE с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="e4265-113">A WORKS MOBILE single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e4265-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="e4265-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e4265-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="e4265-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e4265-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="e4265-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e4265-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e4265-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e4265-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="e4265-118">Scenario description</span></span>
<span data-ttu-id="e4265-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="e4265-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e4265-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="e4265-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e4265-121">Добавление WORKS MOBILE из коллекции</span><span class="sxs-lookup"><span data-stu-id="e4265-121">Adding WORKS MOBILE from the gallery</span></span>
2. <span data-ttu-id="e4265-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="e4265-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-works-mobile-from-the-gallery"></a><span data-ttu-id="e4265-123">Добавление WORKS MOBILE из коллекции</span><span class="sxs-lookup"><span data-stu-id="e4265-123">Adding WORKS MOBILE from the gallery</span></span>
<span data-ttu-id="e4265-124">Чтобы настроить интеграцию WORKS MOBILE с Azure AD, необходимо добавить WORKS MOBILE из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="e4265-124">To configure the integration of WORKS MOBILE into Azure AD, you need to add WORKS MOBILE from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e4265-125">**Чтобы добавить WORKS MOBILE из коллекции, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="e4265-125">**To add WORKS MOBILE from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e4265-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e4265-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e4265-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="e4265-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e4265-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="e4265-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="e4265-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="e4265-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="e4265-133">В поле поиска введите **WORKS MOBILE**.</span><span class="sxs-lookup"><span data-stu-id="e4265-133">In the search box, type **WORKS MOBILE**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_search.png)

5. <span data-ttu-id="e4265-135">На панели результатов выберите **WORKS MOBILE** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="e4265-135">In the results panel, select **WORKS MOBILE**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e4265-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="e4265-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e4265-138">В этом разделе описывается настройка и проверка единого входа Azure AD в WORKS MOBILE с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e4265-138">In this section, you configure and test Azure AD single sign-on with WORKS MOBILE based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e4265-139">Чтобы настроить единый вход, Azure AD необходимо знать, какой пользователь в WORKS MOBILE соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e4265-139">For single sign-on to work, Azure AD needs to know what the counterpart user in WORKS MOBILE is to a user in Azure AD.</span></span> <span data-ttu-id="e4265-140">Другими словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в WORKS MOBILE.</span><span class="sxs-lookup"><span data-stu-id="e4265-140">In other words, a link relationship between an Azure AD user and the related user in WORKS MOBILE needs to be established.</span></span>

<span data-ttu-id="e4265-141">Чтобы установить эту связь, следует назначить **имя пользователя** в Azure AD в качестве значения параметра **Имя пользователя** в WORKS MOBILE.</span><span class="sxs-lookup"><span data-stu-id="e4265-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in WORKS MOBILE.</span></span>

<span data-ttu-id="e4265-142">Чтобы настроить и проверить единый вход Azure AD в WORKS MOBILE, потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="e4265-142">To configure and test Azure AD single sign-on with WORKS MOBILE, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e4265-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="e4265-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e4265-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e4265-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e4265-145">**[Создание тестового пользователя WORKS MOBILE](#creating-a-works-mobile-test-user)** — требуется для создания в WORKS MOBILE копии пользователя Britta Simon, связанной с представлением этого пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e4265-145">**[Creating a WORKS MOBILE test user](#creating-a-works-mobile-test-user)** - to have a counterpart of Britta Simon in WORKS MOBILE that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e4265-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e4265-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e4265-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="e4265-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e4265-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="e4265-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e4265-149">В данном разделе описывается, как включить единый вход Azure AD на портале Azure и настроить единый вход в приложении WORKS MOBILE.</span><span class="sxs-lookup"><span data-stu-id="e4265-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your WORKS MOBILE application.</span></span>

<span data-ttu-id="e4265-150">**Чтобы настроить единый вход Azure AD в WORKS MOBILE, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="e4265-150">**To configure Azure AD single sign-on with WORKS MOBILE, perform the following steps:**</span></span>

1. <span data-ttu-id="e4265-151">На портале Azure на странице интеграции с приложением **WORKS MOBILE** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="e4265-151">In the Azure portal, on the **WORKS MOBILE** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="e4265-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="e4265-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_samlbase.png)

3. <span data-ttu-id="e4265-155">В разделе **Домены и URL-адреса приложения WORKS MOBILE** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="e4265-155">On the **WORKS MOBILE Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_url.png)

    <span data-ttu-id="e4265-157">а.</span><span class="sxs-lookup"><span data-stu-id="e4265-157">a.</span></span> <span data-ttu-id="e4265-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<subdomain>.worksmobile.com/jp/myservice`</span><span class="sxs-lookup"><span data-stu-id="e4265-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.worksmobile.com/jp/myservice`</span></span>

    <span data-ttu-id="e4265-159">b.</span><span class="sxs-lookup"><span data-stu-id="e4265-159">b.</span></span> <span data-ttu-id="e4265-160">В текстовом поле **Идентификатор** введите значение `worksmobile.com`.</span><span class="sxs-lookup"><span data-stu-id="e4265-160">In the **Identifier** textbox, type the value as `worksmobile.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e4265-161">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="e4265-161">This value is not real.</span></span> <span data-ttu-id="e4265-162">Вместо него необходимо указать фактический URL-адрес для входа.</span><span class="sxs-lookup"><span data-stu-id="e4265-162">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="e4265-163">Чтобы получить это значение, обратитесь в [службу поддержки клиентов WORKS MOBILE](mailto:dl_ssoinfo@worksmobile.com).</span><span class="sxs-lookup"><span data-stu-id="e4265-163">Contact [WORKS MOBILE Client support team](mailto:dl_ssoinfo@worksmobile.com) to get this value.</span></span> 
 
4. <span data-ttu-id="e4265-164">В разделе **Сертификат подписи SAML** щелкните **Сертификат (необработанный)**, а затем сохраните файл сертификата на компьютер.</span><span class="sxs-lookup"><span data-stu-id="e4265-164">On the **SAML Signing Certificate** section, click **Certificate(Raw)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_certificate.png) 

5. <span data-ttu-id="e4265-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="e4265-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-worksmobile-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e4265-168">В разделе **Настройка WORKS MOBILE** щелкните **Настроить WORKS MOBILE**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="e4265-168">On the **WORKS MOBILE Configuration** section, click **Configure WORKS MOBILE** to open **Configure sign-on** window.</span></span> <span data-ttu-id="e4265-169">Скопируйте **URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML**  из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="e4265-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_configure.png) 

7. <span data-ttu-id="e4265-171">Чтобы настроить единый вход для своего приложения, обратитесь в [службу поддержки WORKS MOBILE](mailto:dl_ssoinfo@worksmobile.com) и предоставьте следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="e4265-171">To get SSO configured for your application, contact [WORKS MOBILE support team](mailto:dl_ssoinfo@worksmobile.com) and provide them with the following information:</span></span> 

    <span data-ttu-id="e4265-172">• скачанный **файл сертификата**;</span><span class="sxs-lookup"><span data-stu-id="e4265-172">• The downloaded **Certificate file**</span></span>

    <span data-ttu-id="e4265-173">• **URL-адрес службы единого входа SAML**;</span><span class="sxs-lookup"><span data-stu-id="e4265-173">• The **SAML Single Sign-On Service URL**</span></span>

    <span data-ttu-id="e4265-174">• **идентификатор сущности SAML**;</span><span class="sxs-lookup"><span data-stu-id="e4265-174">• The **SAML Entity ID**</span></span>

    <span data-ttu-id="e4265-175">• **URL-адрес выхода**.</span><span class="sxs-lookup"><span data-stu-id="e4265-175">• The **Sign-Out URL**</span></span>

> [!TIP]
> <span data-ttu-id="e4265-176">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="e4265-176">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e4265-177">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="e4265-177">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e4265-178">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="e4265-178">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e4265-179">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="e4265-179">Creating an Azure AD test user</span></span>
<span data-ttu-id="e4265-180">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e4265-180">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="e4265-182">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="e4265-182">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e4265-183">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e4265-183">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-worksmobile-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e4265-185">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="e4265-185">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-worksmobile-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e4265-187">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="e4265-187">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-worksmobile-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e4265-189">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="e4265-189">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-worksmobile-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e4265-191">а.</span><span class="sxs-lookup"><span data-stu-id="e4265-191">a.</span></span> <span data-ttu-id="e4265-192">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e4265-192">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e4265-193">b.</span><span class="sxs-lookup"><span data-stu-id="e4265-193">b.</span></span> <span data-ttu-id="e4265-194">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e4265-194">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e4265-195">c.</span><span class="sxs-lookup"><span data-stu-id="e4265-195">c.</span></span> <span data-ttu-id="e4265-196">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="e4265-196">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e4265-197">d.</span><span class="sxs-lookup"><span data-stu-id="e4265-197">d.</span></span> <span data-ttu-id="e4265-198">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="e4265-198">Click **Create**.</span></span>
 
### <a name="creating-a-works-mobile-test-user"></a><span data-ttu-id="e4265-199">Создание тестового пользователя WORKS MOBILE</span><span class="sxs-lookup"><span data-stu-id="e4265-199">Creating a WORKS MOBILE test user</span></span>

 <span data-ttu-id="e4265-200">В этом разделе описано, как создать пользователя Britta Simon в приложении WORKS MOBILE.</span><span class="sxs-lookup"><span data-stu-id="e4265-200">In this section, you create a user called Britta Simon in WORKS MOBILE.</span></span> <span data-ttu-id="e4265-201">Обратитесь в [службу поддержки WORKS MOBILE](mailto:dl_ssoinfo@worksmobile.com), чтобы добавить пользователей на платформу WORKS MOBILE.</span><span class="sxs-lookup"><span data-stu-id="e4265-201">Please work with [WORKS MOBILE support team](mailto:dl_ssoinfo@worksmobile.com) to add the users in the WORKS MOBILE platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e4265-202">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="e4265-202">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e4265-203">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив ему доступ к WORKS MOBILE.</span><span class="sxs-lookup"><span data-stu-id="e4265-203">In this section, you enable Britta Simon to use Azure single sign-on by granting access to WORKS MOBILE.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="e4265-205">**Чтобы назначить пользователя Britta Simon в WORKS MOBILE, выполните следующие действия**.</span><span class="sxs-lookup"><span data-stu-id="e4265-205">**To assign Britta Simon to WORKS MOBILE, perform the following steps:**</span></span>

1. <span data-ttu-id="e4265-206">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="e4265-206">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="e4265-208">В списке приложений выберите **WORKS MOBILE**.</span><span class="sxs-lookup"><span data-stu-id="e4265-208">In the applications list, select **WORKS MOBILE**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-worksmobile-tutorial/tutorial_worksmobile_app.png) 

3. <span data-ttu-id="e4265-210">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="e4265-210">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="e4265-212">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="e4265-212">Click **Add** button.</span></span> <span data-ttu-id="e4265-213">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="e4265-213">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="e4265-215">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="e4265-215">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e4265-216">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="e4265-216">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e4265-217">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="e4265-217">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e4265-218">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="e4265-218">Testing single sign-on</span></span>

<span data-ttu-id="e4265-219">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="e4265-219">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="e4265-220">Щелкнув элемент WORKS MOBILE на панели доступа, вы автоматически войдете в приложение WORKS MOBILE.</span><span class="sxs-lookup"><span data-stu-id="e4265-220">When you click the WORKS MOBILE tile in the Access Panel, you should get automatically signed-on to your WORKS MOBILE application.</span></span>
<span data-ttu-id="e4265-221">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="e4265-221">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="e4265-222">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="e4265-222">Additional resources</span></span>

* [<span data-ttu-id="e4265-223">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e4265-223">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e4265-224">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e4265-224">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-worksmobile-tutorial/tutorial_general_203.png

