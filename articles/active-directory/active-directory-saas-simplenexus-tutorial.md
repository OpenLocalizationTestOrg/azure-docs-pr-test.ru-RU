---
title: "Руководство по интеграции Azure Active Directory с SimpleNexus | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в приложении SimpleNexus."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 89821a05-88e2-4579-b144-0123b2b9cb95
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: bddd82b986039cf67827cb407f500edb2000964b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-simplenexus"></a><span data-ttu-id="82993-103">Учебник. Интеграция Azure Active Directory с SimpleNexus</span><span class="sxs-lookup"><span data-stu-id="82993-103">Tutorial: Azure Active Directory integration with SimpleNexus</span></span>

<span data-ttu-id="82993-104">В этом руководстве описано, как интегрировать SimpleNexus с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="82993-104">In this tutorial, you learn how to integrate SimpleNexus with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="82993-105">Интеграция Azure AD с приложением SimpleNexus обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="82993-105">Integrating SimpleNexus with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="82993-106">С помощью Azure AD вы можете контролировать доступ к SimpleNexus.</span><span class="sxs-lookup"><span data-stu-id="82993-106">You can control in Azure AD who has access to SimpleNexus</span></span>
- <span data-ttu-id="82993-107">Вы можете включить автоматический вход пользователей в SimpleNexus (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="82993-107">You can enable your users to automatically get signed-on to SimpleNexus (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="82993-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="82993-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="82993-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="82993-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="82993-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="82993-110">Prerequisites</span></span>

<span data-ttu-id="82993-111">Чтобы настроить интеграцию Azure AD с SimpleNexus, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="82993-111">To configure Azure AD integration with SimpleNexus, you need the following items:</span></span>

- <span data-ttu-id="82993-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="82993-112">An Azure AD subscription</span></span>
- <span data-ttu-id="82993-113">подписка SimpleNexus с активированной функцией единого входа.</span><span class="sxs-lookup"><span data-stu-id="82993-113">A SimpleNexus single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="82993-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="82993-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="82993-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="82993-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="82993-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="82993-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="82993-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="82993-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="82993-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="82993-118">Scenario description</span></span>
<span data-ttu-id="82993-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="82993-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="82993-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="82993-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="82993-121">Добавление SimpleNexus из коллекции.</span><span class="sxs-lookup"><span data-stu-id="82993-121">Adding SimpleNexus from the gallery</span></span>
2. <span data-ttu-id="82993-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="82993-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-simplenexus-from-the-gallery"></a><span data-ttu-id="82993-123">Добавление SimpleNexus из коллекции</span><span class="sxs-lookup"><span data-stu-id="82993-123">Adding SimpleNexus from the gallery</span></span>
<span data-ttu-id="82993-124">Чтобы настроить интеграцию SimpleNexus с Azure AD, необходимо добавить SimpleNexus из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="82993-124">To configure the integration of SimpleNexus into Azure AD, you need to add SimpleNexus from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="82993-125">**Чтобы добавить SimpleNexus из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="82993-125">**To add SimpleNexus from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="82993-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="82993-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="82993-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="82993-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="82993-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="82993-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="82993-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="82993-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="82993-133">В поле поиска введите **SimpleNexus**.</span><span class="sxs-lookup"><span data-stu-id="82993-133">In the search box, type **SimpleNexus**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-simplenexus-tutorial/tutorial_simplenexus_search.png)

5. <span data-ttu-id="82993-135">На панели результатов выберите **SimpleNexus** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="82993-135">In the results panel, select **SimpleNexus**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-simplenexus-tutorial/tutorial_simplenexus_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="82993-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="82993-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="82993-138">В этом разделе описана настройка и проверка единого входа Azure AD в SimpleNexus с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="82993-138">In this section, you configure and test Azure AD single sign-on with SimpleNexus based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="82993-139">Чтобы единый вход работал, Azure AD необходима информация о том, какой пользователь в SimpleNexus соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="82993-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SimpleNexus is to a user in Azure AD.</span></span> <span data-ttu-id="82993-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в SimpleNexus.</span><span class="sxs-lookup"><span data-stu-id="82993-140">In other words, a link relationship between an Azure AD user and the related user in SimpleNexus needs to be established.</span></span>

<span data-ttu-id="82993-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в SimpleNexus.</span><span class="sxs-lookup"><span data-stu-id="82993-141">In SimpleNexus, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="82993-142">Чтобы настроить и проверить единый вход Azure AD в SimpleNexus, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="82993-142">To configure and test Azure AD single sign-on with SimpleNexus, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="82993-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="82993-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="82993-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="82993-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="82993-145">**[Создание тестового пользователя SimpleNexus](#creating-a-simplenexus-test-user)** требуется для того, чтобы в SimpleNexus существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="82993-145">**[Creating a SimpleNexus test user](#creating-a-simplenexus-test-user)** - to have a counterpart of Britta Simon in SimpleNexus that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="82993-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="82993-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="82993-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="82993-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="82993-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="82993-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="82993-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении SimpleNexus.</span><span class="sxs-lookup"><span data-stu-id="82993-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SimpleNexus application.</span></span>

<span data-ttu-id="82993-150">**Чтобы настроить единый вход Azure AD в SimpleNexus, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="82993-150">**To configure Azure AD single sign-on with SimpleNexus, perform the following steps:**</span></span>

1. <span data-ttu-id="82993-151">На портале Azure на странице интеграции с приложением **SimpleNexus** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="82993-151">In the Azure portal, on the **SimpleNexus** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="82993-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="82993-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-simplenexus-tutorial/tutorial_simplenexus_samlbase.png)

3. <span data-ttu-id="82993-155">В разделе **Домены и URL-адреса приложения SimpleNexus** сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="82993-155">On the **SimpleNexus Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-simplenexus-tutorial/tutorial_simplenexus_url.png)

    <span data-ttu-id="82993-157">а.</span><span class="sxs-lookup"><span data-stu-id="82993-157">a.</span></span> <span data-ttu-id="82993-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://simplenexus.com/<companyname>_login`</span><span class="sxs-lookup"><span data-stu-id="82993-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://simplenexus.com/<companyname>_login`</span></span>

    <span data-ttu-id="82993-159">b.</span><span class="sxs-lookup"><span data-stu-id="82993-159">b.</span></span> <span data-ttu-id="82993-160">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://simplenexus.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="82993-160">In the **Identifier** textbox, type a URL using the following pattern: `https://simplenexus.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="82993-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="82993-161">These values are not real.</span></span> <span data-ttu-id="82993-162">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="82993-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="82993-163">Чтобы получить эти значения, обратитесь к [группе поддержки клиентов SimpleNexus](https://simplenexus.com/site/contact).</span><span class="sxs-lookup"><span data-stu-id="82993-163">Contact [SimpleNexus Client support team](https://simplenexus.com/site/contact) to get these values.</span></span> 
 
4. <span data-ttu-id="82993-164">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="82993-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-simplenexus-tutorial/tutorial_simplenexus_certificate.png) 

5. <span data-ttu-id="82993-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="82993-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-simplenexus-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="82993-168">Чтобы настроить единый вход на стороне **SimpleNexus**, отправьте скачанный **XML-файл метаданных** [группе поддержки SimpleNexus](https://simplenexus.com/site/contact).</span><span class="sxs-lookup"><span data-stu-id="82993-168">To configure single sign-on on **SimpleNexus** side, you need to send the downloaded **Metadata XML** to [SimpleNexus support team](https://simplenexus.com/site/contact).</span></span> <span data-ttu-id="82993-169">Специалисты службы поддержки настроят подключение единого входа SAML на обеих сторонах.</span><span class="sxs-lookup"><span data-stu-id="82993-169">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="82993-170">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="82993-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="82993-171">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="82993-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="82993-172">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="82993-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="82993-173">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="82993-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="82993-174">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="82993-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="82993-176">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="82993-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="82993-177">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="82993-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-simplenexus-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="82993-179">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="82993-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-simplenexus-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="82993-181">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="82993-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-simplenexus-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="82993-183">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="82993-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-simplenexus-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="82993-185">а.</span><span class="sxs-lookup"><span data-stu-id="82993-185">a.</span></span> <span data-ttu-id="82993-186">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="82993-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="82993-187">b.</span><span class="sxs-lookup"><span data-stu-id="82993-187">b.</span></span> <span data-ttu-id="82993-188">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="82993-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="82993-189">c.</span><span class="sxs-lookup"><span data-stu-id="82993-189">c.</span></span> <span data-ttu-id="82993-190">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="82993-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="82993-191">d.</span><span class="sxs-lookup"><span data-stu-id="82993-191">d.</span></span> <span data-ttu-id="82993-192">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="82993-192">Click **Create**.</span></span>
 
### <a name="creating-a-simplenexus-test-user"></a><span data-ttu-id="82993-193">Создание тестового пользователя SimpleNexus</span><span class="sxs-lookup"><span data-stu-id="82993-193">Creating a SimpleNexus test user</span></span>

<span data-ttu-id="82993-194">Чтобы пользователи Azure AD могли выполнять вход в SimpleNexus, они должны быть подготовлены в SimpleNexus.</span><span class="sxs-lookup"><span data-stu-id="82993-194">In order to enable Azure AD users to log in to SimpleNexus, they must be provisioned into SimpleNexus.</span></span>

<span data-ttu-id="82993-195">В случае SimpleNexus подготовка выполняется вручную администратором клиента.</span><span class="sxs-lookup"><span data-stu-id="82993-195">In the case of SimpleNexus, provisioning is a manual task performed by the tenant administrator.</span></span>

>[!NOTE]
><span data-ttu-id="82993-196">Вы можете использовать любые другие инструменты создания учетных записей пользователей SimpleNexus или API, предоставляемые SimpleNexus для подготовки учетных записей пользователей AAD.</span><span class="sxs-lookup"><span data-stu-id="82993-196">You can use any other SimpleNexus user account creation tools or APIs provided by SimpleNexus to provision AAD user accounts.</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="82993-197">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="82993-197">Assigning the Azure AD test user</span></span>

<span data-ttu-id="82993-198">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к SimpleNexus.</span><span class="sxs-lookup"><span data-stu-id="82993-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SimpleNexus.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="82993-200">**Чтобы назначить пользователя Britta Simon в SimpleNexus, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="82993-200">**To assign Britta Simon to SimpleNexus, perform the following steps:**</span></span>

1. <span data-ttu-id="82993-201">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="82993-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="82993-203">Из списка приложений выберите **SimpleNexus**.</span><span class="sxs-lookup"><span data-stu-id="82993-203">In the applications list, select **SimpleNexus**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-simplenexus-tutorial/tutorial_simplenexus_app.png) 

3. <span data-ttu-id="82993-205">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="82993-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="82993-207">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="82993-207">Click **Add** button.</span></span> <span data-ttu-id="82993-208">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="82993-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="82993-210">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="82993-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="82993-211">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="82993-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="82993-212">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="82993-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="82993-213">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="82993-213">Testing single sign-on</span></span>

<span data-ttu-id="82993-214">Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="82993-214">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="82993-215">Щелкнув элемент "SimpleNexus" на панели доступа, вы автоматически войдете в приложение SimpleNexus.</span><span class="sxs-lookup"><span data-stu-id="82993-215">When you click the SimpleNexus tile in the Access Panel, you should get automatically signed-on to your SimpleNexus application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="82993-216">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="82993-216">Additional resources</span></span>

* [<span data-ttu-id="82993-217">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="82993-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="82993-218">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="82993-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-simplenexus-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-simplenexus-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-simplenexus-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-simplenexus-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-simplenexus-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-simplenexus-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-simplenexus-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-simplenexus-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-simplenexus-tutorial/tutorial_general_203.png

