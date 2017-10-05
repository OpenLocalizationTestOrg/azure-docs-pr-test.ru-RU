---
title: "Учебник. Интеграция Azure Active Directory с Concur | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и Concur."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1eee0a5d-24fa-4986-9aef-3c543cfe3296
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 0b44437b3dcf69dae3587529da7d12e7809b9f55
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-concur"></a><span data-ttu-id="fc1b5-103">Руководство. Интеграция Azure Active Directory с Concur</span><span class="sxs-lookup"><span data-stu-id="fc1b5-103">Tutorial: Azure Active Directory integration with Concur</span></span>

<span data-ttu-id="fc1b5-104">Цель данного руководства — показать, как интегрировать Concur с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="fc1b5-104">In this tutorial, you learn how to integrate Concur with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="fc1b5-105">Интеграция Azure AD с приложением Concur обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="fc1b5-105">Integrating Concur with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="fc1b5-106">С помощью Azure AD вы можете контролировать доступ к Concur.</span><span class="sxs-lookup"><span data-stu-id="fc1b5-106">You can control in Azure AD who has access to Concur</span></span>
- <span data-ttu-id="fc1b5-107">Вы можете включить автоматический вход пользователей в Concur (единый вход) с использованием учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fc1b5-107">You can enable your users to automatically get signed-on to Concur (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="fc1b5-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="fc1b5-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="fc1b5-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в статье [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="fc1b5-109">If you want to know more information about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fc1b5-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="fc1b5-110">Prerequisites</span></span>

<span data-ttu-id="fc1b5-111">Чтобы настроить интеграцию Azure AD с Concur, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="fc1b5-111">To configure Azure AD integration with Concur, you need the following items:</span></span>

- <span data-ttu-id="fc1b5-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="fc1b5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="fc1b5-113">подписка с поддержкой единого входа Concur.</span><span class="sxs-lookup"><span data-stu-id="fc1b5-113">A Concur single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="fc1b5-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="fc1b5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="fc1b5-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="fc1b5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="fc1b5-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="fc1b5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="fc1b5-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fc1b5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="fc1b5-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="fc1b5-118">Scenario description</span></span>
<span data-ttu-id="fc1b5-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="fc1b5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="fc1b5-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="fc1b5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="fc1b5-121">Добавление Concur из коллекции.</span><span class="sxs-lookup"><span data-stu-id="fc1b5-121">Adding Concur from the gallery</span></span>
2. <span data-ttu-id="fc1b5-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="fc1b5-122">Configuring and testing Azure AD single sign-on</span></span>

>[!NOTE]
><span data-ttu-id="fc1b5-123">Настройка подписки Concur для федеративного единого входа посредством SAML представляет собой отдельную задачу, для выполнения которой вам необходимо обратиться в [службу поддержки Concur](https://www.concur.co.in/contact).</span><span class="sxs-lookup"><span data-stu-id="fc1b5-123">The configuration of your Concur subscription for federated SSO via SAML is a separate task, which you must contact [Concur Client support team](https://www.concur.co.in/contact) to perform.</span></span> 

## <a name="adding-concur-from-the-gallery"></a><span data-ttu-id="fc1b5-124">Добавление Concur из коллекции</span><span class="sxs-lookup"><span data-stu-id="fc1b5-124">Adding Concur from the gallery</span></span>
<span data-ttu-id="fc1b5-125">Чтобы настроить интеграцию Concur с Azure AD, необходимо добавить Concur из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="fc1b5-125">To configure the integration of Concur into Azure AD, you need to add Concur from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="fc1b5-126">**Чтобы добавить Concur из коллекции, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="fc1b5-126">**To add Concur from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="fc1b5-127">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fc1b5-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="fc1b5-129">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="fc1b5-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="fc1b5-130">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="fc1b5-130">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="fc1b5-132">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="fc1b5-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="fc1b5-134">В поле поиска введите **Concur**.</span><span class="sxs-lookup"><span data-stu-id="fc1b5-134">In the search box, type **Concur**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-concur-tutorial/tutorial_concur_search.png)

5. <span data-ttu-id="fc1b5-136">На панели результатов выберите **Concur** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="fc1b5-136">In the results panel, select **Concur**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-concur-tutorial/tutorial_concur_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="fc1b5-138">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="fc1b5-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="fc1b5-139">В этом разделе описаны настройка и проверка единого входа Azure AD в Concur с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fc1b5-139">In this section, you configure and test Azure AD single sign-on with Concur based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="fc1b5-140">Чтобы единый вход работал, Azure AD необходимо знать, какой пользователь в Concur соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fc1b5-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Concur is to a user in Azure AD.</span></span> <span data-ttu-id="fc1b5-141">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Concur.</span><span class="sxs-lookup"><span data-stu-id="fc1b5-141">In other words, a link relationship between an Azure AD user and the related user in Concur needs to be established.</span></span>

<span data-ttu-id="fc1b5-142">Чтобы установить эту связь, следует назначить **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Concur.</span><span class="sxs-lookup"><span data-stu-id="fc1b5-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Concur.</span></span>

<span data-ttu-id="fc1b5-143">Чтобы настроить и проверить единый вход Azure AD в Concur, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="fc1b5-143">To configure and test Azure AD single sign-on with Concur, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="fc1b5-144">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="fc1b5-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="fc1b5-145">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fc1b5-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="fc1b5-146">**[Создание тестового пользователя Concur](#creating-a-concur-test-user)** требуется для создания пользователя Britta Simon в Concur, связанного с соответствующим пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fc1b5-146">**[Creating a Concur test user](#creating-a-concur-test-user)** - to have a counterpart of Britta Simon in Concur that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="fc1b5-147">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fc1b5-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="fc1b5-148">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="fc1b5-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="fc1b5-149">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="fc1b5-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="fc1b5-150">В этом разделе описано, как активировать единый вход Azure AD на портале Azure и настроить его в приложении Concur.</span><span class="sxs-lookup"><span data-stu-id="fc1b5-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Concur application.</span></span>

<span data-ttu-id="fc1b5-151">**Чтобы настроить единый вход Azure AD в Concur, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="fc1b5-151">**To configure Azure AD single sign-on with Concur, perform the following steps:**</span></span>

1. <span data-ttu-id="fc1b5-152">На портале Azure на странице интеграции с приложением **Concur** выберите **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="fc1b5-152">In the Azure portal, on the **Concur** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="fc1b5-154">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="fc1b5-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-concur-tutorial/tutorial_concur_samlbase.png)

3. <span data-ttu-id="fc1b5-156">В разделе **Домены и URL-адреса приложения Concur** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="fc1b5-156">On the **Concur Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-concur-tutorial/tutorial_concur_url.png)

    <span data-ttu-id="fc1b5-158">а.</span><span class="sxs-lookup"><span data-stu-id="fc1b5-158">a.</span></span> <span data-ttu-id="fc1b5-159">В текстовом поле **URL-адрес для входа** введите значение в следующем формате: `https://www.concursolutions.com/UI/SSO/<OrganizationId>`</span><span class="sxs-lookup"><span data-stu-id="fc1b5-159">In the **Sign on URL** textbox, type the value using the following pattern: `https://www.concursolutions.com/UI/SSO/<OrganizationId>`</span></span>

    <span data-ttu-id="fc1b5-160">b.</span><span class="sxs-lookup"><span data-stu-id="fc1b5-160">b.</span></span> <span data-ttu-id="fc1b5-161">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<customer-domain>.concursolutions.com`</span><span class="sxs-lookup"><span data-stu-id="fc1b5-161">In the **Identifier** textbox, type a URL using the following pattern: `https://<customer-domain>.concursolutions.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="fc1b5-162">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="fc1b5-162">These values are not the real.</span></span> <span data-ttu-id="fc1b5-163">Необходимо обновить эти значения действующим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="fc1b5-163">Update these values with the actual Sign on URL and Identifier.</span></span> <span data-ttu-id="fc1b5-164">Чтобы получить эти значения, обратитесь в [службу поддержки клиентов Concur](https://www.concur.co.in/contact).</span><span class="sxs-lookup"><span data-stu-id="fc1b5-164">Contact [Concur Client support team](https://www.concur.co.in/contact) to get these values.</span></span> 

4. <span data-ttu-id="fc1b5-165">В разделе **Сертификат подписи SAML** щелкните **XML метаданных** и сохраните XML-файл на компьютере.</span><span class="sxs-lookup"><span data-stu-id="fc1b5-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-concur-tutorial/tutorial_concur_certificate.png) 

5. <span data-ttu-id="fc1b5-167">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="fc1b5-167">Click **Save** button.</span></span>

    <span data-ttu-id="fc1b5-168">![Настройка единого входа](./media/active-directory-saas-concur-tutorial/tutorial_general_400.png)
<CS></span><span class="sxs-lookup"><span data-stu-id="fc1b5-168">![Configure Single Sign-On](./media/active-directory-saas-concur-tutorial/tutorial_general_400.png)
<CS></span></span>

6. <span data-ttu-id="fc1b5-169">Чтобы настроить единый вход на стороне **Concur**, отправьте в службу поддержки Concur скачанный **XML-файл метаданных**.</span><span class="sxs-lookup"><span data-stu-id="fc1b5-169">To configure single sign-on on **Concur** side, you need to send the downloaded **Metadata XML** to Concur support.</span></span> <span data-ttu-id="fc1b5-170">Специалисты службы поддержки настроят подключение единого входа SAML на обеих сторонах.</span><span class="sxs-lookup"><span data-stu-id="fc1b5-170">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

  >[!NOTE]
  ><span data-ttu-id="fc1b5-171">Настройка подписки Concur для федеративного единого входа посредством SAML представляет собой отдельную задачу, для выполнения которой вам необходимо обратиться в [службу поддержки Concur](https://www.concur.co.in/contact).</span><span class="sxs-lookup"><span data-stu-id="fc1b5-171">The configuration of your Concur subscription for federated SSO via SAML is a separate task, which you must contact [Concur Client support team](https://www.concur.co.in/contact) to perform.</span></span> 
  
<CE>

> [!TIP]
> <span data-ttu-id="fc1b5-172">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="fc1b5-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="fc1b5-173">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="fc1b5-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="fc1b5-174">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="fc1b5-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="fc1b5-175">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="fc1b5-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="fc1b5-176">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="fc1b5-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="fc1b5-178">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="fc1b5-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="fc1b5-179">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="fc1b5-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-concur-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="fc1b5-181">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="fc1b5-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-concur-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="fc1b5-183">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="fc1b5-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-concur-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="fc1b5-185">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="fc1b5-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-concur-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="fc1b5-187">а.</span><span class="sxs-lookup"><span data-stu-id="fc1b5-187">a.</span></span> <span data-ttu-id="fc1b5-188">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="fc1b5-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="fc1b5-189">b.</span><span class="sxs-lookup"><span data-stu-id="fc1b5-189">b.</span></span> <span data-ttu-id="fc1b5-190">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="fc1b5-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="fc1b5-191">c.</span><span class="sxs-lookup"><span data-stu-id="fc1b5-191">c.</span></span> <span data-ttu-id="fc1b5-192">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="fc1b5-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="fc1b5-193">d.</span><span class="sxs-lookup"><span data-stu-id="fc1b5-193">d.</span></span> <span data-ttu-id="fc1b5-194">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="fc1b5-194">Click **Create**.</span></span>
 
### <a name="creating-a-concur-test-user"></a><span data-ttu-id="fc1b5-195">Создание тестового пользователя Concur</span><span class="sxs-lookup"><span data-stu-id="fc1b5-195">Creating a Concur test user</span></span>

<span data-ttu-id="fc1b5-196">Приложение поддерживает JIT-подготовку пользователей, поэтому после проверки подлинности пользователи будут созданы в приложении автоматически.</span><span class="sxs-lookup"><span data-stu-id="fc1b5-196">Application supports the Just in time user provisioning and after authentication users are created in the application automatically.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="fc1b5-197">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="fc1b5-197">Assigning the Azure AD test user</span></span>

<span data-ttu-id="fc1b5-198">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure путем предоставления доступа к Concur.</span><span class="sxs-lookup"><span data-stu-id="fc1b5-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Concur.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="fc1b5-200">**Чтобы назначить пользователя Britta Simon в приложении Concur, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="fc1b5-200">**To assign Britta Simon to Concur, perform the following steps:**</span></span>

1. <span data-ttu-id="fc1b5-201">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="fc1b5-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="fc1b5-203">В списке приложений выберите **Concur**.</span><span class="sxs-lookup"><span data-stu-id="fc1b5-203">In the applications list, select **Concur**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-concur-tutorial/tutorial_concur_app.png) 

3. <span data-ttu-id="fc1b5-205">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="fc1b5-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="fc1b5-207">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="fc1b5-207">Click **Add** button.</span></span> <span data-ttu-id="fc1b5-208">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="fc1b5-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="fc1b5-210">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="fc1b5-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="fc1b5-211">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="fc1b5-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="fc1b5-212">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="fc1b5-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="fc1b5-213">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="fc1b5-213">Testing single sign-on</span></span>

<span data-ttu-id="fc1b5-214">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="fc1b5-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="fc1b5-215">Когда вы щелкните элемент Concur на панели доступа, должна появиться страница входа в приложение Concur.</span><span class="sxs-lookup"><span data-stu-id="fc1b5-215">When you click the Concur tile in the Access Panel, you should get login page of Concur application.</span></span>
<span data-ttu-id="fc1b5-216">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="fc1b5-216">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="fc1b5-217">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="fc1b5-217">Additional resources</span></span>

* [<span data-ttu-id="fc1b5-218">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fc1b5-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="fc1b5-219">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="fc1b5-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="fc1b5-220">Руководство по настройке Google Apps для автоматической подготовки пользователей</span><span class="sxs-lookup"><span data-stu-id="fc1b5-220">Configure User Provisioning</span></span>](active-directory-saas-concur-provisioning-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-concur-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-concur-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-concur-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-concur-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-concur-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-concur-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-concur-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-concur-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-concur-tutorial/tutorial_general_203.png

