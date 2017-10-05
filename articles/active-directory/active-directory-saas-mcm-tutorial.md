---
title: "Руководство по интеграции Azure Active Directory с MCM | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и MCM."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7f00799d-e3e9-4ba9-ae4a-fbca843ac5db
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: jeedes
ms.openlocfilehash: cbbb0f54b7954c0ec7326fb62bb427155527cc84
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mcm"></a><span data-ttu-id="c9be0-103">Руководство. Интеграция Azure Active Directory с МСМ</span><span class="sxs-lookup"><span data-stu-id="c9be0-103">Tutorial: Azure Active Directory integration with MCM</span></span>

<span data-ttu-id="c9be0-104">В этом руководстве описано, как интегрировать MCM с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c9be0-104">In this tutorial, you learn how to integrate MCM with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c9be0-105">Интеграция Azure AD с приложением MCM обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="c9be0-105">Integrating MCM with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c9be0-106">С помощью Azure AD вы можете контролировать доступ к MCM.</span><span class="sxs-lookup"><span data-stu-id="c9be0-106">You can control in Azure AD who has access to MCM</span></span>
- <span data-ttu-id="c9be0-107">Вы можете включить автоматический вход пользователей в MCM (единый вход) с использованием учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c9be0-107">You can enable your users to automatically get signed-on to MCM (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c9be0-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="c9be0-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c9be0-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c9be0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c9be0-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c9be0-110">Prerequisites</span></span>

<span data-ttu-id="c9be0-111">Чтобы настроить интеграцию Azure AD с MCM, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="c9be0-111">To configure Azure AD integration with MCM, you need the following items:</span></span>

- <span data-ttu-id="c9be0-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="c9be0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c9be0-113">подписка на MCM с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="c9be0-113">A MCM single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c9be0-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="c9be0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c9be0-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="c9be0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c9be0-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="c9be0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c9be0-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c9be0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c9be0-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="c9be0-118">Scenario description</span></span>
<span data-ttu-id="c9be0-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="c9be0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c9be0-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="c9be0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c9be0-121">Добавление MCM из коллекции</span><span class="sxs-lookup"><span data-stu-id="c9be0-121">Adding MCM from the gallery</span></span>
2. <span data-ttu-id="c9be0-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="c9be0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mcm-from-the-gallery"></a><span data-ttu-id="c9be0-123">Добавление MCM из коллекции</span><span class="sxs-lookup"><span data-stu-id="c9be0-123">Adding MCM from the gallery</span></span>
<span data-ttu-id="c9be0-124">Чтобы настроить интеграцию MCM с Azure AD, необходимо добавить MCM из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="c9be0-124">To configure the integration of MCM into Azure AD, you need to add MCM from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c9be0-125">**Чтобы добавить MCM из коллекции, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="c9be0-125">**To add MCM from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c9be0-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c9be0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c9be0-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="c9be0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c9be0-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="c9be0-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="c9be0-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="c9be0-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="c9be0-133">В поле поиска введите **MCM**.</span><span class="sxs-lookup"><span data-stu-id="c9be0-133">In the search box, type **MCM**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mcm-tutorial/tutorial_mcm_search.png)

5. <span data-ttu-id="c9be0-135">На панели результатов выберите **MCM** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="c9be0-135">In the results panel, select **MCM**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mcm-tutorial/tutorial_mcm_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c9be0-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="c9be0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c9be0-138">В этом разделе описаны настройка и проверка единого входа Azure AD в приложение MCM с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c9be0-138">In this section, you configure and test Azure AD single sign-on with MCM based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="c9be0-139">Чтобы единый вход работал, Azure AD необходимо знать, какой пользователь в MCM соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c9be0-139">For single sign-on to work, Azure AD needs to know what the counterpart user in MCM is to a user in Azure AD.</span></span> <span data-ttu-id="c9be0-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в MCM.</span><span class="sxs-lookup"><span data-stu-id="c9be0-140">In other words, a link relationship between an Azure AD user and the related user in MCM needs to be established.</span></span>

<span data-ttu-id="c9be0-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в MCM.</span><span class="sxs-lookup"><span data-stu-id="c9be0-141">In MCM, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="c9be0-142">Чтобы настроить и проверить единый вход Azure AD в MCM, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="c9be0-142">To configure and test Azure AD single sign-on with MCM, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c9be0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="c9be0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c9be0-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c9be0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c9be0-145">**[Создание тестового пользователя MCM](#creating-a-mcm-test-user)** требуется для создания в MCM пользователя Britta Simon, связанного с представлением этого же пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c9be0-145">**[Creating a MCM test user](#creating-a-mcm-test-user)** - to have a counterpart of Britta Simon in MCM that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c9be0-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c9be0-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c9be0-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="c9be0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c9be0-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="c9be0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c9be0-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении MCM.</span><span class="sxs-lookup"><span data-stu-id="c9be0-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your MCM application.</span></span>

<span data-ttu-id="c9be0-150">**Чтобы настроить единый вход Azure AD в MCM, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="c9be0-150">**To configure Azure AD single sign-on with MCM, perform the following steps:**</span></span>

1. <span data-ttu-id="c9be0-151">На портале Azure на странице интеграции с приложением **MCM** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="c9be0-151">In the Azure portal, on the **MCM** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="c9be0-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="c9be0-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-mcm-tutorial/tutorial_mcm_samlbase.png)

3. <span data-ttu-id="c9be0-155">В разделе **Домены и URL-адреса приложения MCM** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="c9be0-155">On the **MCM Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-mcm-tutorial/tutorial_mcm_url.png)

    <span data-ttu-id="c9be0-157">а.</span><span class="sxs-lookup"><span data-stu-id="c9be0-157">a.</span></span> <span data-ttu-id="c9be0-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://myaba.co.uk/client-access/<companyname>/saml.php`</span><span class="sxs-lookup"><span data-stu-id="c9be0-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://myaba.co.uk/client-access/<companyname>/saml.php`</span></span>

    <span data-ttu-id="c9be0-159">b.</span><span class="sxs-lookup"><span data-stu-id="c9be0-159">b.</span></span> <span data-ttu-id="c9be0-160">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://myaba.co.uk/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="c9be0-160">In the **Identifier** textbox, type a URL using the following pattern: `https://myaba.co.uk/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c9be0-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="c9be0-161">These values are not real.</span></span> <span data-ttu-id="c9be0-162">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="c9be0-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="c9be0-163">Чтобы получить их, обратитесь в [службу поддержки клиентов MCM](http://mcmtechnology.com/support/).</span><span class="sxs-lookup"><span data-stu-id="c9be0-163">Contact [MCM Client support team](http://mcmtechnology.com/support/) to get these values.</span></span> 
 
4. <span data-ttu-id="c9be0-164">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="c9be0-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-mcm-tutorial/tutorial_mcm_certificate.png) 

5. <span data-ttu-id="c9be0-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="c9be0-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-mcm-tutorial/tutorial_general_400.png) 

6. <span data-ttu-id="c9be0-168">Чтобы настроить единый вход на стороне **MCM**, отправьте в [службу поддержки MCM](http://mcmtechnology.com/support/) скачанный **XML-файл метаданных**.</span><span class="sxs-lookup"><span data-stu-id="c9be0-168">To configure single sign-on on **MCM** side, you need to send the downloaded **Metadata XML** to [MCM support team](http://mcmtechnology.com/support/).</span></span> <span data-ttu-id="c9be0-169">Специалисты службы поддержки настроят подключение единого входа SAML на обеих сторонах.</span><span class="sxs-lookup"><span data-stu-id="c9be0-169">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="c9be0-170">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="c9be0-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c9be0-171">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="c9be0-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c9be0-172">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="c9be0-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c9be0-173">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="c9be0-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="c9be0-174">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c9be0-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="c9be0-176">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="c9be0-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c9be0-177">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c9be0-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mcm-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c9be0-179">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="c9be0-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mcm-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c9be0-181">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="c9be0-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mcm-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c9be0-183">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="c9be0-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mcm-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c9be0-185">а.</span><span class="sxs-lookup"><span data-stu-id="c9be0-185">a.</span></span> <span data-ttu-id="c9be0-186">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c9be0-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c9be0-187">b.</span><span class="sxs-lookup"><span data-stu-id="c9be0-187">b.</span></span> <span data-ttu-id="c9be0-188">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c9be0-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c9be0-189">c.</span><span class="sxs-lookup"><span data-stu-id="c9be0-189">c.</span></span> <span data-ttu-id="c9be0-190">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="c9be0-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c9be0-191">d.</span><span class="sxs-lookup"><span data-stu-id="c9be0-191">d.</span></span> <span data-ttu-id="c9be0-192">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="c9be0-192">Click **Create**.</span></span>
 
### <a name="creating-a-mcm-test-user"></a><span data-ttu-id="c9be0-193">Создание тестового пользователя MCM</span><span class="sxs-lookup"><span data-stu-id="c9be0-193">Creating a MCM test user</span></span>

<span data-ttu-id="c9be0-194">В этом разделе описано, как создать пользователя Britta Simon в приложении MCM.</span><span class="sxs-lookup"><span data-stu-id="c9be0-194">In this section, you create a user called Britta Simon in MCM.</span></span> <span data-ttu-id="c9be0-195">Обратитесь в [службу поддержки MCM](http://mcmtechnology.com/support/), чтобы добавить пользователей в платформу MCM.</span><span class="sxs-lookup"><span data-stu-id="c9be0-195">Work with [MCM support team](http://mcmtechnology.com/support/) to add the users in the MCM platform.</span></span>

> [!NOTE]
> <span data-ttu-id="c9be0-196">Вы можете использовать любые другие средства создания учетной записи пользователя MCM или API, предоставляемые MCM для подготовки учетных записей пользователя AAD.</span><span class="sxs-lookup"><span data-stu-id="c9be0-196">You can use any other MCM user account creation tools or APIs provided by MCM to provision AAD user accounts.</span></span>


### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c9be0-197">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="c9be0-197">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c9be0-198">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure путем предоставления доступа к MCM.</span><span class="sxs-lookup"><span data-stu-id="c9be0-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to MCM.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="c9be0-200">**Чтобы назначить пользователя Britta Simon в MCM, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="c9be0-200">**To assign Britta Simon to MCM, perform the following steps:**</span></span>

1. <span data-ttu-id="c9be0-201">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="c9be0-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="c9be0-203">В списке приложений выберите **MCM**.</span><span class="sxs-lookup"><span data-stu-id="c9be0-203">In the applications list, select **MCM**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-mcm-tutorial/tutorial_mcm_app.png) 

3. <span data-ttu-id="c9be0-205">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="c9be0-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="c9be0-207">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="c9be0-207">Click **Add** button.</span></span> <span data-ttu-id="c9be0-208">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="c9be0-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="c9be0-210">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="c9be0-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c9be0-211">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="c9be0-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c9be0-212">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="c9be0-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c9be0-213">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="c9be0-213">Testing single sign-on</span></span>

<span data-ttu-id="c9be0-214">Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="c9be0-214">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c9be0-215">Щелкнув плитку MCM на панели доступа, вы автоматически войдете в приложение MCM.</span><span class="sxs-lookup"><span data-stu-id="c9be0-215">When you click the MCM tile in the Access Panel, you should get automatically signed-on to your MCM application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="c9be0-216">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="c9be0-216">Additional resources</span></span>

* [<span data-ttu-id="c9be0-217">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c9be0-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c9be0-218">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c9be0-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-mcm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mcm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mcm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mcm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mcm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mcm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mcm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mcm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mcm-tutorial/tutorial_general_203.png

