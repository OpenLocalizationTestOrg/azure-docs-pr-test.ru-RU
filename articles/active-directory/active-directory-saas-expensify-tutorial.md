---
title: "Учебник. Интеграция Azure Active Directory с Expensify | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в приложении Expensify."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1e761484-7a2f-4321-91f4-6d5d0b69344e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/12/2017
ms.author: jeedes
ms.openlocfilehash: e45576fd92706881121469ccd82150b3d48059cd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-expensify"></a><span data-ttu-id="692bb-103">Руководство. Интеграция Azure Active Directory с Expensify</span><span class="sxs-lookup"><span data-stu-id="692bb-103">Tutorial: Azure Active Directory integration with Expensify</span></span>

<span data-ttu-id="692bb-104">В этом руководстве описано, как интегрировать Expensify с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="692bb-104">In this tutorial, you learn how to integrate Expensify with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="692bb-105">Интеграция Expensify с Azure AD дает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="692bb-105">Integrating Expensify with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="692bb-106">С помощью Azure AD вы можете контролировать доступ к Expensify.</span><span class="sxs-lookup"><span data-stu-id="692bb-106">You can control in Azure AD who has access to Expensify</span></span>
- <span data-ttu-id="692bb-107">Вы можете включить автоматический вход пользователей в Expensify (единый вход) с помощью их учетных записей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="692bb-107">You can enable your users to automatically get signed-on to Expensify (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="692bb-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="692bb-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="692bb-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="692bb-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="692bb-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="692bb-110">Prerequisites</span></span>

<span data-ttu-id="692bb-111">Чтобы настроить интеграцию Azure AD с Expensify, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="692bb-111">To configure Azure AD integration with Expensify, you need the following items:</span></span>

- <span data-ttu-id="692bb-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="692bb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="692bb-113">подписка с поддержкой единого входа Expensify.</span><span class="sxs-lookup"><span data-stu-id="692bb-113">An Expensify single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="692bb-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="692bb-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="692bb-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="692bb-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="692bb-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="692bb-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="692bb-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="692bb-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="692bb-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="692bb-118">Scenario description</span></span>
<span data-ttu-id="692bb-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="692bb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="692bb-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="692bb-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="692bb-121">Добавление Expensify из коллекции</span><span class="sxs-lookup"><span data-stu-id="692bb-121">Adding Expensify from the gallery</span></span>
2. <span data-ttu-id="692bb-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="692bb-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-expensify-from-the-gallery"></a><span data-ttu-id="692bb-123">Добавление Expensify из коллекции</span><span class="sxs-lookup"><span data-stu-id="692bb-123">Adding Expensify from the gallery</span></span>
<span data-ttu-id="692bb-124">Чтобы настроить интеграцию Expensify с Azure AD, необходимо добавить это приложение из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="692bb-124">To configure the integration of Expensify into Azure AD, you need to add Expensify from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="692bb-125">**Чтобы добавить Expensify из коллекции, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="692bb-125">**To add Expensify from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="692bb-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="692bb-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="692bb-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="692bb-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="692bb-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="692bb-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="692bb-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="692bb-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="692bb-133">В поле поиска введите **Expensify**.</span><span class="sxs-lookup"><span data-stu-id="692bb-133">In the search box, type **Expensify**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_search.png)

5. <span data-ttu-id="692bb-135">На панели результатов выберите **Expensify** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="692bb-135">In the results panel, select **Expensify**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="692bb-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="692bb-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="692bb-138">В этом разделе описана настройка и проверка единого входа Azure AD в Expensify с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="692bb-138">In this section, you configure and test Azure AD single sign-on with Expensify based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="692bb-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Expensify соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="692bb-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Expensify is to a user in Azure AD.</span></span> <span data-ttu-id="692bb-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Expensify.</span><span class="sxs-lookup"><span data-stu-id="692bb-140">In other words, a link relationship between an Azure AD user and the related user in Expensify needs to be established.</span></span>

<span data-ttu-id="692bb-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Expensify.</span><span class="sxs-lookup"><span data-stu-id="692bb-141">In Expensify, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="692bb-142">Чтобы настроить и проверить единый вход Azure AD в Expensify, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="692bb-142">To configure and test Azure AD single sign-on with Expensify, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="692bb-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="692bb-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="692bb-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="692bb-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="692bb-145">**[Создание тестового пользователя Expensify](#creating-an-expensify-test-user)** требуется для создания в Expensify пользователя Britta Simon, связанного с представлением этого же пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="692bb-145">**[Creating an Expensify test user](#creating-an-expensify-test-user)** - to have a counterpart of Britta Simon in Expensify that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="692bb-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="692bb-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="692bb-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="692bb-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="692bb-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="692bb-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="692bb-149">В данном разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Expensify.</span><span class="sxs-lookup"><span data-stu-id="692bb-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Expensify application.</span></span>

<span data-ttu-id="692bb-150">**Чтобы настроить единый вход Azure AD в Expensify, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="692bb-150">**To configure Azure AD single sign-on with Expensify, perform the following steps:**</span></span>

1. <span data-ttu-id="692bb-151">На портале Azure на странице интеграции с приложением **Expensify** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="692bb-151">In the Azure portal, on the **Expensify** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="692bb-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="692bb-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_samlbase.png)

3. <span data-ttu-id="692bb-155">В разделе **Домены и URL-адреса приложения Expensify** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="692bb-155">On the **Expensify Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_url.png)

    <span data-ttu-id="692bb-157">а.</span><span class="sxs-lookup"><span data-stu-id="692bb-157">a.</span></span> <span data-ttu-id="692bb-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://www.expensify.com/authentication/saml/login`</span><span class="sxs-lookup"><span data-stu-id="692bb-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://www.expensify.com/authentication/saml/login`</span></span>

    <span data-ttu-id="692bb-159">b.</span><span class="sxs-lookup"><span data-stu-id="692bb-159">b.</span></span> <span data-ttu-id="692bb-160">В текстовом поле **URL-адрес идентификатора** введите URL-адрес в следующем формате: `https://www.<companyname>.expensify.com/`</span><span class="sxs-lookup"><span data-stu-id="692bb-160">In the **Identifier URL** textbox, type a URL using the following pattern: `https://www.<companyname>.expensify.com/`</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="692bb-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="692bb-161">These values are not real.</span></span> <span data-ttu-id="692bb-162">Замените эти значения фактическим URL-адресом для входа и URL-адресом идентификатора.</span><span class="sxs-lookup"><span data-stu-id="692bb-162">Update these values with the actual Sign-On URL and Identifier URL.</span></span> <span data-ttu-id="692bb-163">Чтобы получить их, обратитесь в [службу поддержки клиентов Expensify](mailto:help@expensify.com).</span><span class="sxs-lookup"><span data-stu-id="692bb-163">Contact [Expensify Client support team](mailto:help@expensify.com) to get these values.</span></span> 
 
4. <span data-ttu-id="692bb-164">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="692bb-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_certificate.png) 

5. <span data-ttu-id="692bb-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="692bb-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-expensify-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="692bb-168">Чтобы включить единый вход в Expensify, сначала необходимо включить в этом приложении **управление доменами**.</span><span class="sxs-lookup"><span data-stu-id="692bb-168">To enable SSO in Expensify, you first need to enable **Domain Control** in the application.</span></span> <span data-ttu-id="692bb-169">Это можно сделать, выполнив действия, указанные [здесь](http://help.expensify.com/domain-control).</span><span class="sxs-lookup"><span data-stu-id="692bb-169">You can enable Domain Control in the application through the steps listed [here](http://help.expensify.com/domain-control).</span></span> <span data-ttu-id="692bb-170">Для получения дополнительной поддержки обратитесь в [службу поддержки клиентов Expensify](mailto:help@expensify.com).</span><span class="sxs-lookup"><span data-stu-id="692bb-170">For additional support, work with [Expensify Client support team](mailto:help@expensify.com).</span></span> <span data-ttu-id="692bb-171">После включения управления доменами сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="692bb-171">Once you have Domain Control enabled, follow these steps:</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_51.png)
    
    <span data-ttu-id="692bb-173">а.</span><span class="sxs-lookup"><span data-stu-id="692bb-173">a.</span></span> <span data-ttu-id="692bb-174">Войдите в приложение Expensify.</span><span class="sxs-lookup"><span data-stu-id="692bb-174">Sign on to your Expensify application.</span></span>
    
    <span data-ttu-id="692bb-175">b.</span><span class="sxs-lookup"><span data-stu-id="692bb-175">b.</span></span> <span data-ttu-id="692bb-176">На панели инструментов в верхней части экрана нажмите **Администратор**.</span><span class="sxs-lookup"><span data-stu-id="692bb-176">In the toolbar on the top, click **Admin**.</span></span>
    
    <span data-ttu-id="692bb-177">c.</span><span class="sxs-lookup"><span data-stu-id="692bb-177">c.</span></span> <span data-ttu-id="692bb-178">На панели слева щелкните **Домен**.</span><span class="sxs-lookup"><span data-stu-id="692bb-178">In the left panel, click **Domain**.</span></span>
    
    <span data-ttu-id="692bb-179">г)</span><span class="sxs-lookup"><span data-stu-id="692bb-179">d.</span></span> <span data-ttu-id="692bb-180">Щелкните имя проверенного домена.</span><span class="sxs-lookup"><span data-stu-id="692bb-180">Click your verified domain name.</span></span>
    
    <span data-ttu-id="692bb-181">д.</span><span class="sxs-lookup"><span data-stu-id="692bb-181">e.</span></span> <span data-ttu-id="692bb-182">На панели слева щелкните **SAML**, а затем переведите переключатель в положение **Включено**.</span><span class="sxs-lookup"><span data-stu-id="692bb-182">In the left panel, click **SAML**, and then select **Enabled**.</span></span>
    
    <span data-ttu-id="692bb-183">Е.</span><span class="sxs-lookup"><span data-stu-id="692bb-183">f.</span></span> <span data-ttu-id="692bb-184">Откройте скачанные метаданные федерации из Azure AD в блокноте, скопируйте содержимое и вставьте его в текстовое поле **Метаданные поставщика удостоверений**.</span><span class="sxs-lookup"><span data-stu-id="692bb-184">Open the downloaded Federation Metadata from Azure AD in notepad, copy the content, and then paste it into the **Identity Provider Metadata** textbox.</span></span>

> [!TIP]
> <span data-ttu-id="692bb-185">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="692bb-185">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="692bb-186">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="692bb-186">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="692bb-187">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="692bb-187">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="692bb-188">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="692bb-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="692bb-189">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="692bb-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="692bb-191">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="692bb-191">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="692bb-192">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="692bb-192">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-expensify-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="692bb-194">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="692bb-194">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-expensify-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="692bb-196">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="692bb-196">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-expensify-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="692bb-198">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="692bb-198">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-expensify-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="692bb-200">а.</span><span class="sxs-lookup"><span data-stu-id="692bb-200">a.</span></span> <span data-ttu-id="692bb-201">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="692bb-201">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="692bb-202">b.</span><span class="sxs-lookup"><span data-stu-id="692bb-202">b.</span></span> <span data-ttu-id="692bb-203">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="692bb-203">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="692bb-204">c.</span><span class="sxs-lookup"><span data-stu-id="692bb-204">c.</span></span> <span data-ttu-id="692bb-205">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="692bb-205">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="692bb-206">d.</span><span class="sxs-lookup"><span data-stu-id="692bb-206">d.</span></span> <span data-ttu-id="692bb-207">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="692bb-207">Click **Create**.</span></span>
 
### <a name="creating-an-expensify-test-user"></a><span data-ttu-id="692bb-208">Создание тестового пользователя Expensify</span><span class="sxs-lookup"><span data-stu-id="692bb-208">Creating an Expensify test user</span></span>

<span data-ttu-id="692bb-209">В этом разделе описано, как создать пользователя Britta Simon в приложении Expensify.</span><span class="sxs-lookup"><span data-stu-id="692bb-209">In this section, you create a user called Britta Simon in Expensify.</span></span> <span data-ttu-id="692bb-210">Обратитесь в [службу поддержки клиентов Expensify](mailto:help@expensify.com), чтобы добавить пользователей на платформу Expensify.</span><span class="sxs-lookup"><span data-stu-id="692bb-210">Work with [Expensify Client support team](mailto:help@expensify.com) to add the users in the Expensify platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="692bb-211">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="692bb-211">Assigning the Azure AD test user</span></span>

<span data-ttu-id="692bb-212">В этом разделе описано, как позволить пользователю Britta Simon использовать единый вход Azure, предоставив доступ к Expensify.</span><span class="sxs-lookup"><span data-stu-id="692bb-212">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Expensify.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="692bb-214">**Чтобы назначить пользователя Britta Simon в Expensify, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="692bb-214">**To assign Britta Simon to Expensify, perform the following steps:**</span></span>

1. <span data-ttu-id="692bb-215">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="692bb-215">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="692bb-217">В списке приложений выберите **Expensify**.</span><span class="sxs-lookup"><span data-stu-id="692bb-217">In the applications list, select **Expensify**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-expensify-tutorial/tutorial_expensify_app.png) 

3. <span data-ttu-id="692bb-219">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="692bb-219">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="692bb-221">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="692bb-221">Click **Add** button.</span></span> <span data-ttu-id="692bb-222">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="692bb-222">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="692bb-224">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="692bb-224">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="692bb-225">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="692bb-225">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="692bb-226">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="692bb-226">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="692bb-227">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="692bb-227">Testing single sign-on</span></span>

<span data-ttu-id="692bb-228">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="692bb-228">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>  

<span data-ttu-id="692bb-229">Щелкнув элемент Expensify на панели доступа, вы автоматически войдете в приложение Expensify.</span><span class="sxs-lookup"><span data-stu-id="692bb-229">When you click the Expensify tile in the Access Panel, you should get automatically signed-on to your Expensify application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="692bb-230">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="692bb-230">Additional resources</span></span>

* [<span data-ttu-id="692bb-231">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="692bb-231">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="692bb-232">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="692bb-232">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-expensify-tutorial/tutorial_general_203.png

