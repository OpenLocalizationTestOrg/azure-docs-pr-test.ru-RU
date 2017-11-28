---
title: "Руководство по интеграции Azure Active Directory с Ariba | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в Ariba."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 45a8364c-55d1-4dc7-b079-9eb2a701842d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/02/2017
ms.author: jeedes
ms.openlocfilehash: 214367847055ba38ee03a28d0afdcc58f68333cc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ariba"></a><span data-ttu-id="b6997-103">Руководство. Интеграция Azure Active Directory с Ariba</span><span class="sxs-lookup"><span data-stu-id="b6997-103">Tutorial: Azure Active Directory integration with Ariba</span></span>

<span data-ttu-id="b6997-104">В этом руководстве описано, как интегрировать Ariba с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b6997-104">In this tutorial, you learn how to integrate Ariba with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b6997-105">Интеграция Azure AD с приложением Ariba обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="b6997-105">Integrating Ariba with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b6997-106">С помощью Azure AD вы можете контролировать доступ к Ariba.</span><span class="sxs-lookup"><span data-stu-id="b6997-106">You can control in Azure AD who has access to Ariba</span></span>
- <span data-ttu-id="b6997-107">Вы можете включить автоматический вход пользователей в Ariba (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b6997-107">You can enable your users to automatically get signed-on to Ariba (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b6997-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="b6997-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b6997-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b6997-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b6997-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b6997-110">Prerequisites</span></span>

<span data-ttu-id="b6997-111">Чтобы настроить интеграцию Azure AD с Ariba, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="b6997-111">To configure Azure AD integration with Ariba, you need the following items:</span></span>

- <span data-ttu-id="b6997-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="b6997-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b6997-113">подписка Ariba с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="b6997-113">An Ariba single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b6997-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="b6997-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b6997-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="b6997-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b6997-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="b6997-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b6997-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b6997-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b6997-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="b6997-118">Scenario description</span></span>
<span data-ttu-id="b6997-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="b6997-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b6997-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="b6997-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b6997-121">Добавление Ariba из коллекции</span><span class="sxs-lookup"><span data-stu-id="b6997-121">Adding Ariba from the gallery</span></span>
2. <span data-ttu-id="b6997-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b6997-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ariba-from-the-gallery"></a><span data-ttu-id="b6997-123">Добавление Ariba из коллекции</span><span class="sxs-lookup"><span data-stu-id="b6997-123">Adding Ariba from the gallery</span></span>
<span data-ttu-id="b6997-124">Чтобы настроить интеграцию Ariba с Azure AD, необходимо добавить Ariba из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="b6997-124">To configure the integration of Ariba into Azure AD, you need to add Ariba from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b6997-125">**Чтобы добавить Ariba из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="b6997-125">**To add Ariba from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b6997-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b6997-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b6997-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="b6997-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b6997-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="b6997-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="b6997-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="b6997-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="b6997-133">В поле поиска введите **Ariba**.</span><span class="sxs-lookup"><span data-stu-id="b6997-133">In the search box, type **Ariba**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_search.png)

5. <span data-ttu-id="b6997-135">На панели результатов выберите **Ariba** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="b6997-135">In the results panel, select **Ariba**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b6997-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b6997-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b6997-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложение Ariba с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b6997-138">In this section, you configure and test Azure AD single sign-on with Ariba based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b6997-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Ariba соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b6997-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Ariba is to a user in Azure AD.</span></span> <span data-ttu-id="b6997-140">То есть необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Ariba.</span><span class="sxs-lookup"><span data-stu-id="b6997-140">In other words, a link relationship between an Azure AD user and the related user in Ariba needs to be established.</span></span>

<span data-ttu-id="b6997-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Ariba.</span><span class="sxs-lookup"><span data-stu-id="b6997-141">In Ariba, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="b6997-142">Чтобы настроить и проверить единый вход Azure AD в Ariba, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="b6997-142">To configure and test Azure AD single sign-on with Ariba, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b6997-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="b6997-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b6997-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b6997-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b6997-145">**[Создание тестового пользователя Ariba](#creating-an-ariba-test-user)** нужно для того, чтобы в Ariba также существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b6997-145">**[Creating an Ariba test user](#creating-an-ariba-test-user)** - to have a counterpart of Britta Simon in Ariba that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b6997-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b6997-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b6997-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="b6997-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b6997-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b6997-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b6997-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Ariba.</span><span class="sxs-lookup"><span data-stu-id="b6997-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Ariba application.</span></span>

<span data-ttu-id="b6997-150">**Чтобы настроить единый вход Azure AD в Ariba, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="b6997-150">**To configure Azure AD single sign-on with Ariba, perform the following steps:**</span></span>

1. <span data-ttu-id="b6997-151">На портале Azure на странице интеграции с приложением **Ariba** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="b6997-151">In the Azure portal, on the **Ariba** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="b6997-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="b6997-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_samlbase.png)

3. <span data-ttu-id="b6997-155">В разделе **Домены и URL-адреса приложения Ariba** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="b6997-155">On the **Ariba Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_url.png)

    <span data-ttu-id="b6997-157">а.</span><span class="sxs-lookup"><span data-stu-id="b6997-157">a.</span></span> <span data-ttu-id="b6997-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<subdomain>.sourcing.ariba.com` или `https://<subdomain>.supplier.ariba.com`.</span><span class="sxs-lookup"><span data-stu-id="b6997-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.sourcing.ariba.com` or `https://<subdomain>.supplier.ariba.com`</span></span>

    <span data-ttu-id="b6997-159">b.</span><span class="sxs-lookup"><span data-stu-id="b6997-159">b.</span></span> <span data-ttu-id="b6997-160">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `http://<subdomain>.procurement-2.ariba.com`</span><span class="sxs-lookup"><span data-stu-id="b6997-160">In the **Identifier** textbox, type a URL using the following pattern: `http://<subdomain>.procurement-2.ariba.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b6997-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="b6997-161">These values are not real.</span></span> <span data-ttu-id="b6997-162">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="b6997-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="b6997-163">Мы рекомендуем использовать уникальное значение строки идентификатора.</span><span class="sxs-lookup"><span data-stu-id="b6997-163">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="b6997-164">Чтобы получить эти значения, обратитесь к группе поддержки Ariba по номеру **1-866-218-2155**.</span><span class="sxs-lookup"><span data-stu-id="b6997-164">Contact Ariba Client support team at **1-866-218-2155** to get these values.</span></span> 
 

4. <span data-ttu-id="b6997-165">В разделе **Сертификат для подписи токена SAML** щелкните **Сертификат (Base64)**, а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="b6997-165">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate  file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_certificate.png) 

5. <span data-ttu-id="b6997-167">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="b6997-167">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-ariba-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b6997-169">Чтобы настроить единый вход для приложения, позвоните в группу поддержки Ariba по номеру **1-866-218-2155**. Вы получите дальнейшие указания по тому, как предоставить скачанный файл **сертификата (Base64)**.</span><span class="sxs-lookup"><span data-stu-id="b6997-169">To get SSO configured for your application, call Ariba support team on **1-866-218-2155** and they'll assist you further on how to provide them the downloaded **Certificate (Base64)** file.</span></span>  
 
> [!TIP]
> <span data-ttu-id="b6997-170">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="b6997-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b6997-171">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="b6997-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b6997-172">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="b6997-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b6997-173">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="b6997-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="b6997-174">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b6997-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="b6997-176">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="b6997-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b6997-177">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b6997-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ariba-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b6997-179">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="b6997-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ariba-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b6997-181">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="b6997-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ariba-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b6997-183">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="b6997-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ariba-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b6997-185">а.</span><span class="sxs-lookup"><span data-stu-id="b6997-185">a.</span></span> <span data-ttu-id="b6997-186">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b6997-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b6997-187">b.</span><span class="sxs-lookup"><span data-stu-id="b6997-187">b.</span></span> <span data-ttu-id="b6997-188">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b6997-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b6997-189">c.</span><span class="sxs-lookup"><span data-stu-id="b6997-189">c.</span></span> <span data-ttu-id="b6997-190">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="b6997-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b6997-191">d.</span><span class="sxs-lookup"><span data-stu-id="b6997-191">d.</span></span> <span data-ttu-id="b6997-192">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="b6997-192">Click **Create**.</span></span>
 
### <a name="creating-an-ariba-test-user"></a><span data-ttu-id="b6997-193">Создание тестового пользователя Ariba</span><span class="sxs-lookup"><span data-stu-id="b6997-193">Creating an Ariba test user</span></span>

<span data-ttu-id="b6997-194">Цель этого раздела — создать пользователя с именем Britta Simon в приложении Ariba.</span><span class="sxs-lookup"><span data-stu-id="b6997-194">The objective of this section is to create a user called Britta Simon in Ariba.</span></span> <span data-ttu-id="b6997-195">Обратитесь к группе поддержки Ariba по номеру **1-866-218-2155**, чтобы добавить пользователей в систему Ariba.</span><span class="sxs-lookup"><span data-stu-id="b6997-195">Work with Ariba support team at **1-866-218-2155** to add the users in the Ariba system.</span></span> 

 >[!NOTE]
 ><span data-ttu-id="b6997-196">Чтобы создать пользователя вручную, необходимо обратиться к группе поддержки Ariba по номеру **1-866-218-2155**.</span><span class="sxs-lookup"><span data-stu-id="b6997-196">If you need to create a user manually, you need to contact the Ariba support team at **1-866-218-2155**.</span></span>
 >  

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b6997-197">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="b6997-197">Assigning the Azure AD test user</span></span>

<span data-ttu-id="b6997-198">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к Ariba.</span><span class="sxs-lookup"><span data-stu-id="b6997-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Ariba.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="b6997-200">**Чтобы назначить пользователя Britta Simon в Ariba, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="b6997-200">**To assign Britta Simon to Ariba, perform the following steps:**</span></span>

1. <span data-ttu-id="b6997-201">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="b6997-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="b6997-203">В списке приложений выберите **Ariba**.</span><span class="sxs-lookup"><span data-stu-id="b6997-203">In the applications list, select **Ariba**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_app.png) 

3. <span data-ttu-id="b6997-205">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="b6997-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="b6997-207">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="b6997-207">Click **Add** button.</span></span> <span data-ttu-id="b6997-208">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="b6997-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="b6997-210">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="b6997-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b6997-211">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="b6997-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b6997-212">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="b6997-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b6997-213">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="b6997-213">Testing single sign-on</span></span>
<span data-ttu-id="b6997-214">Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="b6997-214">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="b6997-215">Щелкнув плитку Ariba на панели доступа, вы автоматически войдете в приложение Ariba.</span><span class="sxs-lookup"><span data-stu-id="b6997-215">When you click the Ariba tile in the Access Panel, you should get automatically signed-on to your Ariba application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="b6997-216">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="b6997-216">Additional resources</span></span>

* [<span data-ttu-id="b6997-217">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b6997-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b6997-218">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b6997-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_203.png

