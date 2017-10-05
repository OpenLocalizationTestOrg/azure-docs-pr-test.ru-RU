---
title: "Руководство. Интеграция Azure Active Directory с Alcumus Info Exchange | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в Alcumus Info Exchange."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d26034b8-f0d5-4f65-aa56-0fc168ceec8c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2017
ms.author: jeedes
ms.openlocfilehash: 1f67682111de0bea1b18fd97d739492661ebbfd9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-alcumus-info-exchange"></a><span data-ttu-id="a7d42-103">Учебник. Интеграция Azure Active Directory с Alcumus Info Exchange</span><span class="sxs-lookup"><span data-stu-id="a7d42-103">Tutorial: Azure Active Directory integration with Alcumus Info Exchange</span></span>

<span data-ttu-id="a7d42-104">В этом руководстве описано, как интегрировать Alcumus Info Exchange с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a7d42-104">In this tutorial, you learn how to integrate Alcumus Info Exchange with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a7d42-105">Интеграция приложения Alcumus Info Exchange с Azure AD обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="a7d42-105">Integrating Alcumus Info Exchange with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a7d42-106">С помощью Azure AD вы можете контролировать доступ к Alcumus Info Exchange.</span><span class="sxs-lookup"><span data-stu-id="a7d42-106">You can control in Azure AD who has access to Alcumus Info Exchange</span></span>
- <span data-ttu-id="a7d42-107">Вы можете включить автоматический вход пользователей в Alcumus Info Exchange (единый вход) с использованием учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a7d42-107">You can enable your users to automatically get signed-on to Alcumus Info Exchange (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a7d42-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="a7d42-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a7d42-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a7d42-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a7d42-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a7d42-110">Prerequisites</span></span>

<span data-ttu-id="a7d42-111">Чтобы настроить интеграцию Azure AD с Alcumus Info Exchange, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="a7d42-111">To configure Azure AD integration with Alcumus Info Exchange, you need the following items:</span></span>

- <span data-ttu-id="a7d42-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="a7d42-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a7d42-113">подписка Alcumus Info Exchange с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="a7d42-113">An Alcumus Info Exchange single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a7d42-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="a7d42-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a7d42-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="a7d42-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a7d42-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="a7d42-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a7d42-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a7d42-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a7d42-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="a7d42-118">Scenario description</span></span>
<span data-ttu-id="a7d42-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="a7d42-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a7d42-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="a7d42-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a7d42-121">Добавление Alcumus Info Exchange из коллекции</span><span class="sxs-lookup"><span data-stu-id="a7d42-121">Adding Alcumus Info Exchange from the gallery</span></span>
2. <span data-ttu-id="a7d42-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="a7d42-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-alcumus-info-exchange-from-the-gallery"></a><span data-ttu-id="a7d42-123">Добавление Alcumus Info Exchange из коллекции</span><span class="sxs-lookup"><span data-stu-id="a7d42-123">Adding Alcumus Info Exchange from the gallery</span></span>
<span data-ttu-id="a7d42-124">Чтобы настроить интеграцию Alcumus Info Exchange с Azure AD, вам нужно добавить Alcumus Info Exchange из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="a7d42-124">To configure the integration of Alcumus Info Exchange into Azure AD, you need to add Alcumus Info Exchange from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a7d42-125">**Чтобы добавить Alcumus Info Exchange из коллекции, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="a7d42-125">**To add Alcumus Info Exchange from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a7d42-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a7d42-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a7d42-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="a7d42-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a7d42-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="a7d42-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="a7d42-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="a7d42-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="a7d42-133">В поле поиска введите **Alcumus Info Exchange**.</span><span class="sxs-lookup"><span data-stu-id="a7d42-133">In the search box, type **Alcumus Info Exchange**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-alcumus-info-tutorial/tutorial_alcumusinfoexchange_search.png)

5. <span data-ttu-id="a7d42-135">В области результатов выберите **Alcumus Info Exchange** и щелкните **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="a7d42-135">In the results panel, select **Alcumus Info Exchange**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-alcumus-info-tutorial/tutorial_alcumusinfoexchange_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a7d42-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="a7d42-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a7d42-138">В этом разделе описана настройка и проверка единого входа Azure AD в Alcumus Info Exchange с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a7d42-138">In this section, you configure and test Azure AD single sign-on with Alcumus Info Exchange based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a7d42-139">Для использования единого входа в Azure AD необходимо знать, какой пользователь в Alcumus Info Exchange соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a7d42-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Alcumus Info Exchange is to a user in Azure AD.</span></span> <span data-ttu-id="a7d42-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Alcumus Info Exchange.</span><span class="sxs-lookup"><span data-stu-id="a7d42-140">In other words, a link relationship between an Azure AD user and the related user in Alcumus Info Exchange needs to be established.</span></span>

<span data-ttu-id="a7d42-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Alcumus Info Exchange.</span><span class="sxs-lookup"><span data-stu-id="a7d42-141">In Alcumus Info Exchange, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a7d42-142">Чтобы настроить и проверить единый вход Azure AD в Alcumus Info Exchange, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="a7d42-142">To configure and test Azure AD single sign-on with Alcumus Info Exchange, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a7d42-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="a7d42-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a7d42-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a7d42-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a7d42-145">**[Создание тестового пользователя Alcumus Info Exchange](#creating-an-alcumus-info-exchange-test-user)** нужно для того, чтобы в Alcumus Info Exchange также существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a7d42-145">**[Creating an Alcumus Info Exchange test user](#creating-an-alcumus-info-exchange-test-user)** - to have a counterpart of Britta Simon in Alcumus Info Exchange that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a7d42-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a7d42-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a7d42-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="a7d42-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a7d42-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="a7d42-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a7d42-149">В данном разделе описано, как включить единый вход в Azure AD на портале управления Azure и настроить его в приложении Alcumus Info Exchange.</span><span class="sxs-lookup"><span data-stu-id="a7d42-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Alcumus Info Exchange application.</span></span>

<span data-ttu-id="a7d42-150">**Чтобы настроить единый вход Azure AD в Alcumus Info Exchange, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="a7d42-150">**To configure Azure AD single sign-on with Alcumus Info Exchange, perform the following steps:**</span></span>

1. <span data-ttu-id="a7d42-151">На портале Azure на странице интеграции с приложением **Alcumus Info Exchange** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="a7d42-151">In the Azure portal, on the **Alcumus Info Exchange** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="a7d42-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="a7d42-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-alcumus-info-tutorial/tutorial_alcumusinfoexchange_samlbase.png)

3. <span data-ttu-id="a7d42-155">В разделе **Домены и URL-адреса приложения Alcumus Info Exchange** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="a7d42-155">On the **Alcumus Info Exchange Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-alcumus-info-tutorial/tutorial_alcumusinfoexchange_url.png)

    <span data-ttu-id="a7d42-157">а.</span><span class="sxs-lookup"><span data-stu-id="a7d42-157">a.</span></span> <span data-ttu-id="a7d42-158">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<subdomain>.info-exchange.com`</span><span class="sxs-lookup"><span data-stu-id="a7d42-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.info-exchange.com`</span></span>

    <span data-ttu-id="a7d42-159">b.</span><span class="sxs-lookup"><span data-stu-id="a7d42-159">b.</span></span> <span data-ttu-id="a7d42-160">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате: `https://<subdomain>.info-exchange.com/Auth/`.</span><span class="sxs-lookup"><span data-stu-id="a7d42-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.info-exchange.com/Auth/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a7d42-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="a7d42-161">These values are not real.</span></span> <span data-ttu-id="a7d42-162">Измените их на фактические значения идентификатора и URL-адреса ответа.</span><span class="sxs-lookup"><span data-stu-id="a7d42-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="a7d42-163">Обратитесь к [группе поддержки Alcumus Info Exchange](mailto:helpdesk@alcumusgroup.com), чтобы получить эти значения.</span><span class="sxs-lookup"><span data-stu-id="a7d42-163">Contact [Alcumus Info Exchange support team](mailto:helpdesk@alcumusgroup.com) to get these values.</span></span>
 
4. <span data-ttu-id="a7d42-164">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="a7d42-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-alcumus-info-tutorial/tutorial_alcumusinfoexchange_certificate.png) 

5. <span data-ttu-id="a7d42-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="a7d42-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-alcumus-info-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a7d42-168">Чтобы настроить единый вход на стороне **Alcumus Info Exchange**, отправьте скачанный **XML-файл метаданных** [группе поддержки Alcumus Info Exchange](mailto:helpdesk@alcumusgroup.com).</span><span class="sxs-lookup"><span data-stu-id="a7d42-168">To configure single sign-on on **Alcumus Info Exchange** side, you need to send the downloaded **Metadata XML** to [Alcumus Info Exchange support team](mailto:helpdesk@alcumusgroup.com).</span></span>

> [!TIP]
> <span data-ttu-id="a7d42-169">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="a7d42-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a7d42-170">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="a7d42-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a7d42-171">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="a7d42-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a7d42-172">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="a7d42-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="a7d42-173">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a7d42-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="a7d42-175">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="a7d42-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a7d42-176">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a7d42-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-alcumus-info-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a7d42-178">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="a7d42-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-alcumus-info-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a7d42-180">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="a7d42-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-alcumus-info-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a7d42-182">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="a7d42-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-alcumus-info-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a7d42-184">а.</span><span class="sxs-lookup"><span data-stu-id="a7d42-184">a.</span></span> <span data-ttu-id="a7d42-185">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a7d42-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a7d42-186">b.</span><span class="sxs-lookup"><span data-stu-id="a7d42-186">b.</span></span> <span data-ttu-id="a7d42-187">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a7d42-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a7d42-188">c.</span><span class="sxs-lookup"><span data-stu-id="a7d42-188">c.</span></span> <span data-ttu-id="a7d42-189">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="a7d42-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a7d42-190">d.</span><span class="sxs-lookup"><span data-stu-id="a7d42-190">d.</span></span> <span data-ttu-id="a7d42-191">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="a7d42-191">Click **Create**.</span></span>
 
### <a name="creating-an-alcumus-info-exchange-test-user"></a><span data-ttu-id="a7d42-192">Создание тестового пользователя Alcumus Info Exchange</span><span class="sxs-lookup"><span data-stu-id="a7d42-192">Creating an Alcumus Info Exchange test user</span></span>

<span data-ttu-id="a7d42-193">Цель этого раздела — создать пользователя с именем Britta Simon в Alcumus Info Exchange.</span><span class="sxs-lookup"><span data-stu-id="a7d42-193">The objective of this section is to create a user called Britta Simon in Alcumus Info Exchange.</span></span>

<span data-ttu-id="a7d42-194">Чтобы создать пользователя Britta Simon в Alcumus Info Exchange, обратитесь к [группе поддержки Alcumus Info Exchange](mailto:helpdesk@alcumusgroup.com).</span><span class="sxs-lookup"><span data-stu-id="a7d42-194">To create a user called Britta Simon in Alcumus Info Exchange, Contact the [Alcumus Info Exchange support team](mailto:helpdesk@alcumusgroup.com).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a7d42-195">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="a7d42-195">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a7d42-196">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к Alcumus Info Exchange.</span><span class="sxs-lookup"><span data-stu-id="a7d42-196">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Alcumus Info Exchange.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="a7d42-198">**Чтобы назначить Britta Simon в Alcumus Info Exchange, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="a7d42-198">**To assign Britta Simon to Alcumus Info Exchange, perform the following steps:**</span></span>

1. <span data-ttu-id="a7d42-199">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="a7d42-199">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="a7d42-201">В списке приложений выберите **Alcumus Info Exchange**.</span><span class="sxs-lookup"><span data-stu-id="a7d42-201">In the applications list, select **Alcumus Info Exchange**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-alcumus-info-tutorial/tutorial_alcumusinfoexchange_app.png) 

3. <span data-ttu-id="a7d42-203">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="a7d42-203">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="a7d42-205">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="a7d42-205">Click **Add** button.</span></span> <span data-ttu-id="a7d42-206">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="a7d42-206">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="a7d42-208">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="a7d42-208">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a7d42-209">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="a7d42-209">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a7d42-210">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="a7d42-210">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a7d42-211">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="a7d42-211">Testing single sign-on</span></span>

<span data-ttu-id="a7d42-212">Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="a7d42-212">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="a7d42-213">Щелкнув элемент Alcumus Info Exchange на панели доступа, вы автоматически войдете в приложение Alcumus Info Exchange.</span><span class="sxs-lookup"><span data-stu-id="a7d42-213">When you click the Alcumus Info Exchange tile in the Access Panel, you should get automatically signed-on to your Alcumus Info Exchange application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a7d42-214">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="a7d42-214">Additional resources</span></span>

* [<span data-ttu-id="a7d42-215">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a7d42-215">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a7d42-216">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a7d42-216">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-alcumus-info-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-alcumus-info-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-alcumus-info-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-alcumus-info-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-alcumus-info-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-alcumus-info-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-alcumus-info-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-alcumus-info-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-alcumus-info-tutorial/tutorial_general_203.png

