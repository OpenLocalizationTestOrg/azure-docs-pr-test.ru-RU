---
title: "Руководство. Интеграция Azure Active Directory с AppBlade | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в приложении AppBlade."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3360d7aa-6518-4f99-88bd-b7f7258183e8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 7820a70b34b6d25ba81b17c472159d08904335d1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-appblade"></a><span data-ttu-id="629bb-103">Руководство. Интеграция Azure Active Directory с AppBlade</span><span class="sxs-lookup"><span data-stu-id="629bb-103">Tutorial: Azure Active Directory integration with AppBlade</span></span>

<span data-ttu-id="629bb-104">В этом руководстве описано, как интегрировать AppBlade с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="629bb-104">In this tutorial, you learn how to integrate AppBlade with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="629bb-105">Интеграция AppBlade с Azure AD обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="629bb-105">Integrating AppBlade with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="629bb-106">С помощью Azure AD вы можете контролировать доступ к приложению AppBlade.</span><span class="sxs-lookup"><span data-stu-id="629bb-106">You can control in Azure AD who has access to AppBlade</span></span>
- <span data-ttu-id="629bb-107">Вы можете включить автоматический вход пользователей в AppBlade (единый вход) под учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="629bb-107">You can enable your users to automatically get signed-on to AppBlade (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="629bb-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="629bb-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="629bb-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="629bb-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="629bb-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="629bb-110">Prerequisites</span></span>

<span data-ttu-id="629bb-111">Чтобы настроить интеграцию Azure AD с AppBlade, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="629bb-111">To configure Azure AD integration with AppBlade, you need the following items:</span></span>

- <span data-ttu-id="629bb-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="629bb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="629bb-113">подписка AppBlade с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="629bb-113">An AppBlade single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="629bb-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="629bb-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="629bb-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="629bb-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="629bb-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="629bb-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="629bb-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="629bb-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="629bb-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="629bb-118">Scenario description</span></span>
<span data-ttu-id="629bb-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="629bb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="629bb-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="629bb-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="629bb-121">Добавление AppBlade из коллекции</span><span class="sxs-lookup"><span data-stu-id="629bb-121">Adding AppBlade from the gallery</span></span>
2. <span data-ttu-id="629bb-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="629bb-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-appblade-from-the-gallery"></a><span data-ttu-id="629bb-123">Добавление AppBlade из коллекции</span><span class="sxs-lookup"><span data-stu-id="629bb-123">Adding AppBlade from the gallery</span></span>
<span data-ttu-id="629bb-124">Чтобы настроить интеграцию AppBlade с Azure AD, необходимо добавить AppBlade из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="629bb-124">To configure the integration of AppBlade into Azure AD, you need to add AppBlade from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="629bb-125">**Чтобы добавить AppBlade из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="629bb-125">**To add AppBlade from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="629bb-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="629bb-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="629bb-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="629bb-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="629bb-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="629bb-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="629bb-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="629bb-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="629bb-133">В поле поиска введите **AppBlade**.</span><span class="sxs-lookup"><span data-stu-id="629bb-133">In the search box, type **AppBlade**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_search.png)

5. <span data-ttu-id="629bb-135">На панели результатов выберите **AppBlade** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="629bb-135">In the results panel, select **AppBlade**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="629bb-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="629bb-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="629bb-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложение AppBlade с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="629bb-138">In this section, you configure and test Azure AD single sign-on with AppBlade based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="629bb-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в AppBlade соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="629bb-139">For single sign-on to work, Azure AD needs to know what the counterpart user in AppBlade is to a user in Azure AD.</span></span> <span data-ttu-id="629bb-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в AppBlade.</span><span class="sxs-lookup"><span data-stu-id="629bb-140">In other words, a link relationship between an Azure AD user and the related user in AppBlade needs to be established.</span></span>

<span data-ttu-id="629bb-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в AppBlade.</span><span class="sxs-lookup"><span data-stu-id="629bb-141">In AppBlade, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="629bb-142">Чтобы настроить и проверить единый вход Azure AD в AppBlade, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="629bb-142">To configure and test Azure AD single sign-on with AppBlade, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="629bb-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="629bb-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="629bb-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="629bb-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="629bb-145">**[Создание тестового пользователя AppBlade](#creating-an-appblade-test-user)** нужно для того, чтобы в AppBlade также существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="629bb-145">**[Creating an AppBlade test user](#creating-an-appblade-test-user)** - to have a counterpart of Britta Simon in AppBlade that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="629bb-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="629bb-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="629bb-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="629bb-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="629bb-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="629bb-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="629bb-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении AppBlade.</span><span class="sxs-lookup"><span data-stu-id="629bb-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your AppBlade application.</span></span>

<span data-ttu-id="629bb-150">**Чтобы настроить единый вход Azure AD в AppBlade, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="629bb-150">**To configure Azure AD single sign-on with AppBlade, perform the following steps:**</span></span>

1. <span data-ttu-id="629bb-151">На портале Azure на странице интеграции с приложением **AppBlade** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="629bb-151">In the Azure portal, on the **AppBlade** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="629bb-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="629bb-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_samlbase.png)

3. <span data-ttu-id="629bb-155">В разделе **Домены и URL-адреса приложения AppBlade** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="629bb-155">On the **AppBlade Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_url.png)

    <span data-ttu-id="629bb-157">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<companyname>.appblade.com/saml/<tenantid>`</span><span class="sxs-lookup"><span data-stu-id="629bb-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.appblade.com/saml/<tenantid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="629bb-158">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="629bb-158">This value is not real.</span></span> <span data-ttu-id="629bb-159">Вместо него необходимо указать фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="629bb-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="629bb-160">Чтобы получить это значение, обратитесь к [группе поддержки AppBlade](mailto:support@appblade.com).</span><span class="sxs-lookup"><span data-stu-id="629bb-160">Contact [AppBlade Client support team](mailto:support@appblade.com) to get the value.</span></span> 
 
4. <span data-ttu-id="629bb-161">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="629bb-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_certificate.png) 

5. <span data-ttu-id="629bb-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="629bb-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-appblade-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="629bb-165">Чтобы настроить единый вход на стороне **AppBlade**, отправьте [группе поддержки AppBlade](mailto:support@appblade.com) скачанный **XML-файл метаданных**.</span><span class="sxs-lookup"><span data-stu-id="629bb-165">To configure single sign-on on **AppBlade** side, you need to send the downloaded **Metadata XML** to [AppBlade support team](mailto:support@appblade.com).</span></span> <span data-ttu-id="629bb-166">Кроме того, попросите их настроить для параметра **SSO Issuer URL** (URL-адрес единого входа издателя) значение `https://appblade.com/saml`.</span><span class="sxs-lookup"><span data-stu-id="629bb-166">Also, please ask them to configure the **SSO Issuer URL** as `https://appblade.com/saml`.</span></span> <span data-ttu-id="629bb-167">Без этого параметра единый вход работать не будет.</span><span class="sxs-lookup"><span data-stu-id="629bb-167">This setting is required for single sign-on to work.</span></span>


> [!TIP]
> <span data-ttu-id="629bb-168">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="629bb-168">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="629bb-169">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="629bb-169">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="629bb-170">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="629bb-170">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="629bb-171">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="629bb-171">Creating an Azure AD test user</span></span>
<span data-ttu-id="629bb-172">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="629bb-172">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="629bb-174">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="629bb-174">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="629bb-175">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="629bb-175">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-appblade-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="629bb-177">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="629bb-177">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-appblade-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="629bb-179">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="629bb-179">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-appblade-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="629bb-181">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="629bb-181">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-appblade-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="629bb-183">а.</span><span class="sxs-lookup"><span data-stu-id="629bb-183">a.</span></span> <span data-ttu-id="629bb-184">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="629bb-184">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="629bb-185">b.</span><span class="sxs-lookup"><span data-stu-id="629bb-185">b.</span></span> <span data-ttu-id="629bb-186">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="629bb-186">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="629bb-187">c.</span><span class="sxs-lookup"><span data-stu-id="629bb-187">c.</span></span> <span data-ttu-id="629bb-188">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="629bb-188">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="629bb-189">d.</span><span class="sxs-lookup"><span data-stu-id="629bb-189">d.</span></span> <span data-ttu-id="629bb-190">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="629bb-190">Click **Create**.</span></span>
 
### <a name="creating-an-appblade-test-user"></a><span data-ttu-id="629bb-191">Создание тестового пользователя AppBlade</span><span class="sxs-lookup"><span data-stu-id="629bb-191">Creating an AppBlade test user</span></span>

<span data-ttu-id="629bb-192">Цель этого раздела — создать в приложении AppBlade пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="629bb-192">The objective of this section is to create a user called Britta Simon in AppBlade.</span></span> <span data-ttu-id="629bb-193">Приложение AppBlade поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="629bb-193">AppBlade supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="629bb-194">**Убедитесь, что ваше доменное имя настроено в AppBlade для подготовки пользователей. После этого будет работать только JIT-подготовка пользователей.**</span><span class="sxs-lookup"><span data-stu-id="629bb-194">**Make sure that your domain name is configured with AppBlade for user provisioning. After that only the just-in-time user provisioning works.**</span></span>

<span data-ttu-id="629bb-195">Если у пользователя есть адрес электронной почты в домене, настроенном приложением AppBlade для вашей учетной записи, такой пользователь автоматически станет участником этой учетной записи и получит указанный вами уровень разрешений: "Базовый" (базовый пользователь, который может только устанавливать приложения), "Участник команды" (пользователь, который может скачивать новые версии приложений и управлять проектами) или "Администратор" (все права администратора учетной записи).</span><span class="sxs-lookup"><span data-stu-id="629bb-195">If the user has an email address ending with the domain configured by AppBlade for your account, then the user will automatically join the account as a member with the permission level you specify, which is one of "Basic" (a basic user who can only install applications), "Team Member" (a user who can upload new app versions and manage projects), or "Administrator" (full admin privileges to the account).</span></span> <span data-ttu-id="629bb-196">Обычно выбирается базовый уровень, для повышения которого пользователю предоставляется имя входа администратора (в AppBlade имя входа администратора можно настроить заранее на основе адреса электронной почты или повысить уровень пользователя от имени клиента после того, как он выполнит вход).</span><span class="sxs-lookup"><span data-stu-id="629bb-196">Normally one would choose Basic and then promote users manually via an Admin login (AppBlade needs to configure either an email-based admin login in advance or promote a user on behalf of the customer after login).</span></span>

<span data-ttu-id="629bb-197">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="629bb-197">There is no action item for you in this section.</span></span> <span data-ttu-id="629bb-198">Пользователь будет создан при попытке получить доступ к AppBlade (если он еще не создан).</span><span class="sxs-lookup"><span data-stu-id="629bb-198">A new user is created during an attempt to access AppBlade if it doesn't exist yet.</span></span> 

> [!NOTE]
> <span data-ttu-id="629bb-199">Если вам нужно вручную создать пользователя, необходимо обратиться к [группе поддержки AppBlade](mailto:support@appblade.com).</span><span class="sxs-lookup"><span data-stu-id="629bb-199">If you need to create a user manually, you need to contact the [AppBlade support team](mailto:support@appblade.com).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="629bb-200">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="629bb-200">Assigning the Azure AD test user</span></span>

<span data-ttu-id="629bb-201">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к AppBlade.</span><span class="sxs-lookup"><span data-stu-id="629bb-201">In this section, you enable Britta Simon to use Azure single sign-on by granting access to AppBlade.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="629bb-203">**Чтобы назначить пользователя Britta Simon в AppBlade, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="629bb-203">**To assign Britta Simon to AppBlade, perform the following steps:**</span></span>

1. <span data-ttu-id="629bb-204">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="629bb-204">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="629bb-206">В списке приложений выберите **AppBlade**.</span><span class="sxs-lookup"><span data-stu-id="629bb-206">In the applications list, select **AppBlade**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-appblade-tutorial/tutorial_appblade_app.png) 

3. <span data-ttu-id="629bb-208">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="629bb-208">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="629bb-210">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="629bb-210">Click **Add** button.</span></span> <span data-ttu-id="629bb-211">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="629bb-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="629bb-213">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="629bb-213">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="629bb-214">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="629bb-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="629bb-215">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="629bb-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="629bb-216">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="629bb-216">Testing single sign-on</span></span>

<span data-ttu-id="629bb-217">Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="629bb-217">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="629bb-218">Щелкнув элемент AppBlade на панели доступа, вы автоматически войдете в приложение AppBlade.</span><span class="sxs-lookup"><span data-stu-id="629bb-218">When you click the AppBlade tile in the Access Panel, you should get automatically signed-on to your AppBlade application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="629bb-219">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="629bb-219">Additional resources</span></span>

* [<span data-ttu-id="629bb-220">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="629bb-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="629bb-221">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="629bb-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-appblade-tutorial/tutorial_general_203.png

