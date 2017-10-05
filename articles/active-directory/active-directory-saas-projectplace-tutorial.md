---
title: "Руководство по интеграции Azure Active Directory с Projectplace | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в приложении Projectplace."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 298059ca-b652-4577-916a-c31393d53d7a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: bb9dd10c887cb0e42e544066d9b0dcfa554e10ce
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-projectplace"></a><span data-ttu-id="5f5df-103">Учебник. Интеграция Azure Active Directory с Projectplace</span><span class="sxs-lookup"><span data-stu-id="5f5df-103">Tutorial: Azure Active Directory integration with Projectplace</span></span>

<span data-ttu-id="5f5df-104">В данном руководстве описано, как интегрировать Projectplace с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5f5df-104">In this tutorial, you learn how to integrate Projectplace with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5f5df-105">Интеграция Azure AD с приложением Projectplace обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="5f5df-105">Integrating Projectplace with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5f5df-106">С помощью Azure AD вы можете контролировать доступ к Projectplace.</span><span class="sxs-lookup"><span data-stu-id="5f5df-106">You can control in Azure AD who has access to Projectplace</span></span>
- <span data-ttu-id="5f5df-107">Вы можете включить автоматический вход для пользователей в Projectplace (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5f5df-107">You can enable your users to automatically get signed-on to Projectplace (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5f5df-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="5f5df-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="5f5df-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5f5df-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5f5df-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="5f5df-110">Prerequisites</span></span>

<span data-ttu-id="5f5df-111">Чтобы настроить интеграцию Azure AD с Projectplace, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="5f5df-111">To configure Azure AD integration with Projectplace, you need the following items:</span></span>

- <span data-ttu-id="5f5df-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="5f5df-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5f5df-113">подписка Projectplace с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="5f5df-113">A Projectplace single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5f5df-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="5f5df-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5f5df-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="5f5df-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5f5df-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="5f5df-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5f5df-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5f5df-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5f5df-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="5f5df-118">Scenario description</span></span>
<span data-ttu-id="5f5df-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="5f5df-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5f5df-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="5f5df-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5f5df-121">Добавление Projectplace из коллекции.</span><span class="sxs-lookup"><span data-stu-id="5f5df-121">Adding Projectplace from the gallery</span></span>
2. <span data-ttu-id="5f5df-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="5f5df-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-projectplace-from-the-gallery"></a><span data-ttu-id="5f5df-123">Добавление Projectplace из коллекции</span><span class="sxs-lookup"><span data-stu-id="5f5df-123">Adding Projectplace from the gallery</span></span>
<span data-ttu-id="5f5df-124">Чтобы настроить интеграцию Projectplace с Azure AD, необходимо добавить Projectplace из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="5f5df-124">To configure the integration of Projectplace into Azure AD, you need to add Projectplace from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5f5df-125">**Чтобы добавить Projectplace из коллекции, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="5f5df-125">**To add Projectplace from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5f5df-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5f5df-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5f5df-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="5f5df-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5f5df-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="5f5df-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="5f5df-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="5f5df-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="5f5df-133">В поле поиска введите **Projectplace**.</span><span class="sxs-lookup"><span data-stu-id="5f5df-133">In the search box, type **Projectplace**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_search.png)

5. <span data-ttu-id="5f5df-135">На панели результатов выберите **Projectplace** и щелкните **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="5f5df-135">In the results panel, select **Projectplace**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5f5df-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="5f5df-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5f5df-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложение Projectplace с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5f5df-138">In this section, you configure and test Azure AD single sign-on with Projectplace based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5f5df-139">Чтобы единый вход работал, Azure AD необходимо знать, какой пользователь в Projectplace соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5f5df-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Projectplace is to a user in Azure AD.</span></span> <span data-ttu-id="5f5df-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Projectplace.</span><span class="sxs-lookup"><span data-stu-id="5f5df-140">In other words, a link relationship between an Azure AD user and the related user in Projectplace needs to be established.</span></span>

<span data-ttu-id="5f5df-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Projectplace.</span><span class="sxs-lookup"><span data-stu-id="5f5df-141">In Projectplace, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="5f5df-142">Чтобы настроить и проверить единый вход Azure AD в Projectplace, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="5f5df-142">To configure and test Azure AD single sign-on with Projectplace, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5f5df-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="5f5df-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5f5df-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5f5df-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5f5df-145">**[Создание тестового пользователя Projectplace](#creating-a-projectplace-test-user)** требуется для создания в Projectplace пользователя Britta Simon, связанного с представлением этого пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5f5df-145">**[Creating a Projectplace test user](#creating-a-projectplace-test-user)** - to have a counterpart of Britta Simon in Projectplace that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="5f5df-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5f5df-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5f5df-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="5f5df-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5f5df-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="5f5df-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5f5df-149">В данном разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Projectplace.</span><span class="sxs-lookup"><span data-stu-id="5f5df-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Projectplace application.</span></span>

<span data-ttu-id="5f5df-150">**Чтобы настроить единый вход Azure AD в Projectplace, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="5f5df-150">**To configure Azure AD single sign-on with Projectplace, perform the following steps:**</span></span>

1. <span data-ttu-id="5f5df-151">На портале Azure на странице интеграции с приложением **Projectplace** выберите **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="5f5df-151">In the Azure portal, on the **Projectplace** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="5f5df-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="5f5df-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_samlbase.png)

3. <span data-ttu-id="5f5df-155">В разделе **Домены и URL-адреса приложения Projectplace** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="5f5df-155">On the **Projectplace Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_url.png)

    <span data-ttu-id="5f5df-157">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<company>.projectplace.com`</span><span class="sxs-lookup"><span data-stu-id="5f5df-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company>.projectplace.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="5f5df-158">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="5f5df-158">This value is not real.</span></span> <span data-ttu-id="5f5df-159">Вместо него необходимо указать фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="5f5df-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="5f5df-160">Для получения этого значения обратитесь в [службу поддержки клиентов Projectplace](https://success.planview.com/Projectplace/Support).</span><span class="sxs-lookup"><span data-stu-id="5f5df-160">Contact [Projectplace Client support team](https://success.planview.com/Projectplace/Support) to get this value.</span></span> 
 
4. <span data-ttu-id="5f5df-161">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="5f5df-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_certificate.png) 

5. <span data-ttu-id="5f5df-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="5f5df-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-projectplace-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="5f5df-165">Чтобы настроить единый вход на стороне **Projectplace**, отправьте скачанный **XML-файл метаданных** в [службу поддержки Projectplace](https://success.planview.com/Projectplace/Support).</span><span class="sxs-lookup"><span data-stu-id="5f5df-165">To configure single sign-on on **Projectplace** side, you need to send the downloaded **Metadata XML** to [Projectplace support team](https://success.planview.com/Projectplace/Support).</span></span> <span data-ttu-id="5f5df-166">Специалисты службы поддержки настроят подключение единого входа SAML на обеих сторонах.</span><span class="sxs-lookup"><span data-stu-id="5f5df-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

>[!NOTE]
><span data-ttu-id="5f5df-167">Настройку единого входа должна выполнять [служба поддержки Projectplace](https://success.planview.com/Projectplace/Support).</span><span class="sxs-lookup"><span data-stu-id="5f5df-167">The single sign-on configuration has to be performed by the [Projectplace support team](https://success.planview.com/Projectplace/Support).</span></span> <span data-ttu-id="5f5df-168">Сразу же после завершения настройки вы получите уведомление.</span><span class="sxs-lookup"><span data-stu-id="5f5df-168">You will get a notification as soon as the configuration has been completed.</span></span>

> [!TIP]
> <span data-ttu-id="5f5df-169">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="5f5df-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="5f5df-170">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="5f5df-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="5f5df-171">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="5f5df-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5f5df-172">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="5f5df-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="5f5df-173">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5f5df-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="5f5df-175">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="5f5df-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5f5df-176">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5f5df-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-projectplace-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5f5df-178">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="5f5df-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-projectplace-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5f5df-180">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="5f5df-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-projectplace-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5f5df-182">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="5f5df-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-projectplace-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5f5df-184">а.</span><span class="sxs-lookup"><span data-stu-id="5f5df-184">a.</span></span> <span data-ttu-id="5f5df-185">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5f5df-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5f5df-186">b.</span><span class="sxs-lookup"><span data-stu-id="5f5df-186">b.</span></span> <span data-ttu-id="5f5df-187">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5f5df-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5f5df-188">c.</span><span class="sxs-lookup"><span data-stu-id="5f5df-188">c.</span></span> <span data-ttu-id="5f5df-189">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="5f5df-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="5f5df-190">d.</span><span class="sxs-lookup"><span data-stu-id="5f5df-190">d.</span></span> <span data-ttu-id="5f5df-191">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="5f5df-191">Click **Create**.</span></span>
 
### <a name="creating-a-projectplace-test-user"></a><span data-ttu-id="5f5df-192">Создание тестового пользователя Projectplace</span><span class="sxs-lookup"><span data-stu-id="5f5df-192">Creating a Projectplace test user</span></span>

<span data-ttu-id="5f5df-193">Чтобы пользователи Azure AD могли выполнять вход в Projectplace, они должны быть подготовлены для Projectplace.</span><span class="sxs-lookup"><span data-stu-id="5f5df-193">In order to enable Azure AD users to log into Projectplace, they must be provisioned into Projectplace.</span></span> <span data-ttu-id="5f5df-194">В случае с Projectplace подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="5f5df-194">In the case of Projectplace, provisioning is a manual task.</span></span>

<span data-ttu-id="5f5df-195">**Чтобы подготовить учетную запись пользователя, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="5f5df-195">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="5f5df-196">Выполните вход на сайт **Projectplace** компании в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="5f5df-196">Log in to your **Projectplace** company site as an administrator.</span></span>

2. <span data-ttu-id="5f5df-197">Перейдите к разделу **People** (Люди) и щелкните **Members** (Участники).</span><span class="sxs-lookup"><span data-stu-id="5f5df-197">Go to **People**, and then click **Members**.</span></span>
   
    <span data-ttu-id="5f5df-198">![Люди](./media/active-directory-saas-projectplace-tutorial/ic790228.png "Люди")</span><span class="sxs-lookup"><span data-stu-id="5f5df-198">![People](./media/active-directory-saas-projectplace-tutorial/ic790228.png "People")</span></span>

3. <span data-ttu-id="5f5df-199">Щелкните **Добавить участника**.</span><span class="sxs-lookup"><span data-stu-id="5f5df-199">Click **Add Member**.</span></span>
   
    <span data-ttu-id="5f5df-200">![Добавление участников](./media/active-directory-saas-projectplace-tutorial/ic790232.png "Добавление участников")</span><span class="sxs-lookup"><span data-stu-id="5f5df-200">![Add Members](./media/active-directory-saas-projectplace-tutorial/ic790232.png "Add Members")</span></span>

4. <span data-ttu-id="5f5df-201">В разделе **Добавление участника** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="5f5df-201">In the **Add Member** section, perform the following steps:</span></span>
   
    <span data-ttu-id="5f5df-202">![Новые участники](./media/active-directory-saas-projectplace-tutorial/ic790233.png "Новые участники")</span><span class="sxs-lookup"><span data-stu-id="5f5df-202">![New Members](./media/active-directory-saas-projectplace-tutorial/ic790233.png "New Members")</span></span>
   
    <span data-ttu-id="5f5df-203">а.</span><span class="sxs-lookup"><span data-stu-id="5f5df-203">a.</span></span> <span data-ttu-id="5f5df-204">В разделе **Новые участники** введите электронный адрес действующей учетной записи AAD, которую вы хотите подготовить, в соответствующее текстовое поле.</span><span class="sxs-lookup"><span data-stu-id="5f5df-204">In the **New Members** textbox, type the email address of a valid AAD account you want to provision into the related textboxes.</span></span>
   
    <span data-ttu-id="5f5df-205">b.</span><span class="sxs-lookup"><span data-stu-id="5f5df-205">b.</span></span> <span data-ttu-id="5f5df-206">Нажмите кнопку **Отправить**.</span><span class="sxs-lookup"><span data-stu-id="5f5df-206">Click **Send**.</span></span>

   <span data-ttu-id="5f5df-207">Владельцу учетной записи Azure Active Directory будет отправлено электронное сообщение со ссылкой для подтверждения учетной записи перед ее активацией.</span><span class="sxs-lookup"><span data-stu-id="5f5df-207">An email including a link to confirm the account before it becomes active is sent to the Azure Active Directory account holder.</span></span>

>[!NOTE]
><span data-ttu-id="5f5df-208">Вы можете использовать любые другие инструменты создания учетных записей пользователя Projectplace или API, предоставляемые Projectplace для подготовки учетных записей пользователя AAD.</span><span class="sxs-lookup"><span data-stu-id="5f5df-208">You can use any other Projectplace user account creation tools or APIs provided by Projectplace to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="5f5df-209">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="5f5df-209">Assigning the Azure AD test user</span></span>

<span data-ttu-id="5f5df-210">В данном разделе описано, как предоставить пользователю Britta Simon доступ к Projectplace, чтобы он мог использовать единый вход Azure.</span><span class="sxs-lookup"><span data-stu-id="5f5df-210">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Projectplace.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="5f5df-212">**Чтобы назначить пользователя Britta Simon в Projectplace, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="5f5df-212">**To assign Britta Simon to Projectplace, perform the following steps:**</span></span>

1. <span data-ttu-id="5f5df-213">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="5f5df-213">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="5f5df-215">В списке приложений выберите **Projectplace**.</span><span class="sxs-lookup"><span data-stu-id="5f5df-215">In the applications list, select **Projectplace**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-projectplace-tutorial/tutorial_projectplace_app.png) 

3. <span data-ttu-id="5f5df-217">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="5f5df-217">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="5f5df-219">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="5f5df-219">Click **Add** button.</span></span> <span data-ttu-id="5f5df-220">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="5f5df-220">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="5f5df-222">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="5f5df-222">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5f5df-223">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="5f5df-223">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5f5df-224">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="5f5df-224">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5f5df-225">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="5f5df-225">Testing single sign-on</span></span>

<span data-ttu-id="5f5df-226">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="5f5df-226">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="5f5df-227">Щелкнув элемент Projectplace на панели доступа, вы автоматически войдете в приложение Projectplace.</span><span class="sxs-lookup"><span data-stu-id="5f5df-227">When you click the Projectplace tile in the Access Panel, you should get automatically signed-on to your Projectplace application.</span></span>
<span data-ttu-id="5f5df-228">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5f5df-228">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5f5df-229">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="5f5df-229">Additional resources</span></span>

* [<span data-ttu-id="5f5df-230">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5f5df-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5f5df-231">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5f5df-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-projectplace-tutorial/tutorial_general_203.png

