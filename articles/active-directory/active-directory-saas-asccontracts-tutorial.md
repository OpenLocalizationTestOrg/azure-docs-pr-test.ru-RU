---
title: "Руководство по интеграции Azure Active Directory с ASC Contracts | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в приложении ASC Contracts."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f7f54202-1581-4e55-a97e-02633ff9382d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/21/2017
ms.author: jeedes
ms.openlocfilehash: 87ea3cc55f9683e7d5b9912a87d675575cea0347
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-asc-contracts"></a><span data-ttu-id="3dba0-103">Руководство по интеграции Azure Active Directory с ASC Contracts</span><span class="sxs-lookup"><span data-stu-id="3dba0-103">Tutorial: Azure Active Directory integration with ASC Contracts</span></span>

<span data-ttu-id="3dba0-104">В этом руководстве описано, как интегрировать ASC Contracts с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3dba0-104">In this tutorial, you learn how to integrate ASC Contracts with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3dba0-105">Интеграция Azure AD с приложением ASC Contracts обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="3dba0-105">Integrating ASC Contracts with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3dba0-106">С помощью Azure AD вы можете контролировать доступ к ASC Contracts.</span><span class="sxs-lookup"><span data-stu-id="3dba0-106">You can control in Azure AD who has access to ASC Contracts</span></span>
- <span data-ttu-id="3dba0-107">Вы можете включить автоматический вход пользователей в ASC Contracts (единый вход) с использованием учетных записей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3dba0-107">You can enable your users to automatically get signed-on to ASC Contracts (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3dba0-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="3dba0-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="3dba0-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3dba0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3dba0-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="3dba0-110">Prerequisites</span></span>

<span data-ttu-id="3dba0-111">Чтобы настроить интеграцию Azure AD с ASC Contracts, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="3dba0-111">To configure Azure AD integration with ASC Contracts, you need the following items:</span></span>

- <span data-ttu-id="3dba0-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="3dba0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3dba0-113">подписка ASC Contracts с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="3dba0-113">An ASC Contracts single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3dba0-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="3dba0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3dba0-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="3dba0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3dba0-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="3dba0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3dba0-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3dba0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3dba0-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="3dba0-118">Scenario description</span></span>
<span data-ttu-id="3dba0-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="3dba0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3dba0-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="3dba0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3dba0-121">Добавление ASC Contracts из коллекции</span><span class="sxs-lookup"><span data-stu-id="3dba0-121">Adding ASC Contracts from the gallery</span></span>
2. <span data-ttu-id="3dba0-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="3dba0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-asc-contracts-from-the-gallery"></a><span data-ttu-id="3dba0-123">Добавление ASC Contracts из коллекции</span><span class="sxs-lookup"><span data-stu-id="3dba0-123">Adding ASC Contracts from the gallery</span></span>
<span data-ttu-id="3dba0-124">Чтобы настроить интеграцию ASC Contracts с Azure AD, необходимо добавить ASC Contracts из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="3dba0-124">To configure the integration of ASC Contracts into Azure AD, you need to add ASC Contracts from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3dba0-125">**Чтобы добавить ASC Contracts из коллекции, выполните следующее.**</span><span class="sxs-lookup"><span data-stu-id="3dba0-125">**To add ASC Contracts from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3dba0-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3dba0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3dba0-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="3dba0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3dba0-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="3dba0-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="3dba0-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="3dba0-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="3dba0-133">В поле поиска введите **ASC Contracts**.</span><span class="sxs-lookup"><span data-stu-id="3dba0-133">In the search box, type **ASC Contracts**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_search.png)

5. <span data-ttu-id="3dba0-135">На панели результатов выберите **ASC Contracts** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="3dba0-135">In the results panel, select **ASC Contracts**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3dba0-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="3dba0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3dba0-138">В этом разделе описана настройка и проверка единого входа Azure AD в ASC Contracts с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3dba0-138">In this section, you configure and test Azure AD single sign-on with ASC Contracts based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="3dba0-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в ASC Contracts соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3dba0-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ASC Contracts is to a user in Azure AD.</span></span> <span data-ttu-id="3dba0-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в ASC Contracts.</span><span class="sxs-lookup"><span data-stu-id="3dba0-140">In other words, a link relationship between an Azure AD user and the related user in ASC Contracts needs to be established.</span></span>

<span data-ttu-id="3dba0-141">Чтобы установить эту связь, следует назначить **имя пользователя** в Azure AD в качестве значения **имени пользователя** в ASC Contracts.</span><span class="sxs-lookup"><span data-stu-id="3dba0-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ASC Contracts.</span></span>

<span data-ttu-id="3dba0-142">Чтобы настроить и проверить единый вход Azure AD в ASC Contracts, требуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="3dba0-142">To configure and test Azure AD single sign-on with ASC Contracts, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3dba0-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="3dba0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3dba0-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3dba0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3dba0-145">**[Создание тестового пользователя ASC Contracts](#creating-an-asc-contracts-test-user)** требуется для создания в ASC Contracts пользователя Britta Simon, связанного с соответствующим пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3dba0-145">**[Creating an ASC Contracts test user](#creating-an-asc-contracts-test-user)** - to have a counterpart of Britta Simon in ASC Contracts that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="3dba0-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3dba0-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3dba0-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="3dba0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3dba0-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="3dba0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3dba0-149">В этом разделе описано, как включить единый вход Azure AD на новом портале Azure и настроить его в приложении ASC Contracts.</span><span class="sxs-lookup"><span data-stu-id="3dba0-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ASC Contracts application.</span></span>

<span data-ttu-id="3dba0-150">**Чтобы настроить единый вход Azure AD в ASC Contracts, выполните следующее.**</span><span class="sxs-lookup"><span data-stu-id="3dba0-150">**To configure Azure AD single sign-on with ASC Contracts, perform the following steps:**</span></span>

1. <span data-ttu-id="3dba0-151">На портале Azure на странице интеграции с приложением **ASC Contracts** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="3dba0-151">In the Azure portal, on the **ASC Contracts** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="3dba0-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="3dba0-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_samlbase.png)

3. <span data-ttu-id="3dba0-155">В разделе **Домены и URL-адреса приложения ASC Contracts** сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="3dba0-155">On the **ASC Contracts Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_url.png)

    <span data-ttu-id="3dba0-157">а.</span><span class="sxs-lookup"><span data-stu-id="3dba0-157">a.</span></span> <span data-ttu-id="3dba0-158">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<subdomain>.asccontracts.com/shibboleth`</span><span class="sxs-lookup"><span data-stu-id="3dba0-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.asccontracts.com/shibboleth`</span></span>

    <span data-ttu-id="3dba0-159">b.</span><span class="sxs-lookup"><span data-stu-id="3dba0-159">b.</span></span> <span data-ttu-id="3dba0-160">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате: `https://<subdomain>.asccontracts.com/shibboleth.sso/login`.</span><span class="sxs-lookup"><span data-stu-id="3dba0-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.asccontracts.com/shibboleth.sso/login`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3dba0-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="3dba0-161">These values are not real.</span></span> <span data-ttu-id="3dba0-162">Измените их на фактические значения идентификатора и URL-адреса ответа.</span><span class="sxs-lookup"><span data-stu-id="3dba0-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="3dba0-163">Обратитесь к группе поддержки ASC Networks Inc. (ASC) по номеру **(613) 599-61-78**, чтобы получить эти значения.</span><span class="sxs-lookup"><span data-stu-id="3dba0-163">Contact ASC Networks Inc. (ASC) team at **613.599.6178** to get these values.</span></span>

4. <span data-ttu-id="3dba0-164">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="3dba0-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_certificate.png) 

5. <span data-ttu-id="3dba0-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="3dba0-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-asccontracts-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3dba0-168">Для настройки единого входа на стороне **ASC Contracts** обратитесь в службу поддержки ASC Networks Inc. (ASC) по номеру **(613) 599-61-78** и предоставьте скачанный **XML-файл метаданных**.</span><span class="sxs-lookup"><span data-stu-id="3dba0-168">To configure single sign-on on **ASC Contracts** side, call ASC Networks Inc. (ASC) support at **613.599.6178** and provide them with the downloaded **Metadata XML**.</span></span> <span data-ttu-id="3dba0-169">Это позволит службе поддержки правильно настроить подключение единого входа SAML для приложения на обоих сторонах.</span><span class="sxs-lookup"><span data-stu-id="3dba0-169">They set this application up to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="3dba0-170">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="3dba0-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3dba0-171">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="3dba0-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3dba0-172">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="3dba0-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3dba0-173">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="3dba0-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="3dba0-174">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3dba0-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="3dba0-176">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="3dba0-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3dba0-177">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3dba0-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-asccontracts-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3dba0-179">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="3dba0-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-asccontracts-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3dba0-181">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="3dba0-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-asccontracts-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3dba0-183">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="3dba0-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-asccontracts-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3dba0-185">а.</span><span class="sxs-lookup"><span data-stu-id="3dba0-185">a.</span></span> <span data-ttu-id="3dba0-186">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3dba0-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3dba0-187">b.</span><span class="sxs-lookup"><span data-stu-id="3dba0-187">b.</span></span> <span data-ttu-id="3dba0-188">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="3dba0-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3dba0-189">c.</span><span class="sxs-lookup"><span data-stu-id="3dba0-189">c.</span></span> <span data-ttu-id="3dba0-190">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="3dba0-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="3dba0-191">d.</span><span class="sxs-lookup"><span data-stu-id="3dba0-191">d.</span></span> <span data-ttu-id="3dba0-192">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="3dba0-192">Click **Create**.</span></span>
 
### <a name="creating-an-asc-contracts-test-user"></a><span data-ttu-id="3dba0-193">Создание тестового пользователя ASC Contracts</span><span class="sxs-lookup"><span data-stu-id="3dba0-193">Creating an ASC Contracts test user</span></span>

<span data-ttu-id="3dba0-194">Обратитесь в службу поддержки ASC Networks Inc. (ASC) по номеру **(613) 599-61-78**, чтобы добавить пользователей на платформу ASC Contracts.</span><span class="sxs-lookup"><span data-stu-id="3dba0-194">Work with ASC Networks Inc. (ASC) support team at **613.599.6178** to get the users added in the ASC Contracts platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="3dba0-195">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="3dba0-195">Assigning the Azure AD test user</span></span>

<span data-ttu-id="3dba0-196">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к ASC Contracts.</span><span class="sxs-lookup"><span data-stu-id="3dba0-196">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ASC Contracts.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="3dba0-198">**Чтобы назначить пользователя Britta Simon приложению ASC Contracts, сделайте следующее.**</span><span class="sxs-lookup"><span data-stu-id="3dba0-198">**To assign Britta Simon to ASC Contracts, perform the following steps:**</span></span>

1. <span data-ttu-id="3dba0-199">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="3dba0-199">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="3dba0-201">Из списка приложений выберите **ASC Contracts**.</span><span class="sxs-lookup"><span data-stu-id="3dba0-201">In the applications list, select **ASC Contracts**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-asccontracts-tutorial/tutorial_asccontracts_app.png) 

3. <span data-ttu-id="3dba0-203">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="3dba0-203">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="3dba0-205">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="3dba0-205">Click **Add** button.</span></span> <span data-ttu-id="3dba0-206">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="3dba0-206">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="3dba0-208">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="3dba0-208">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3dba0-209">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="3dba0-209">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3dba0-210">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="3dba0-210">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3dba0-211">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="3dba0-211">Testing single sign-on</span></span>

<span data-ttu-id="3dba0-212">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="3dba0-212">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="3dba0-213">Щелкнув элемент ASC Contracts на панели доступа, вы автоматически войдете в приложение ASC Contracts.</span><span class="sxs-lookup"><span data-stu-id="3dba0-213">When you click the ASC Contracts tile in the Access Panel, you should get automatically signed-on to your ASC Contracts application.</span></span> <span data-ttu-id="3dba0-214">Дополнительные сведения о панели доступа см. в статье</span><span class="sxs-lookup"><span data-stu-id="3dba0-214">For more information about the Access Panel, see.</span></span> <span data-ttu-id="3dba0-215">[Общие сведения о панели доступа](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="3dba0-215">[Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3dba0-216">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="3dba0-216">Additional resources</span></span>

* [<span data-ttu-id="3dba0-217">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3dba0-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3dba0-218">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3dba0-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-asccontracts-tutorial/tutorial_general_203.png

