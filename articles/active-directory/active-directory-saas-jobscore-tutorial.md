---
title: "Руководство по интеграции Azure Active Directory с JobScore | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и JobScore."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 30f51b32-e55c-4c66-96e8-50a2f9c2194a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: f6ed2d362f7b027bfdc38ba2fdaa03948ff5632c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jobscore"></a><span data-ttu-id="60733-103">Руководство по интеграции Azure Active Directory с JobScore</span><span class="sxs-lookup"><span data-stu-id="60733-103">Tutorial: Azure Active Directory integration with JobScore</span></span>

<span data-ttu-id="60733-104">В этом руководстве описано, как интегрировать JobScore с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="60733-104">In this tutorial, you learn how to integrate JobScore with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="60733-105">Интеграция Azure AD с JobScore обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="60733-105">Integrating JobScore with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="60733-106">С помощью Azure AD вы можете контролировать доступ к JobScore.</span><span class="sxs-lookup"><span data-stu-id="60733-106">You can control in Azure AD who has access to JobScore</span></span>
- <span data-ttu-id="60733-107">Вы можете включить автоматический вход пользователей в JobScore (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="60733-107">You can enable your users to automatically get signed-on to JobScore (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="60733-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="60733-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="60733-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="60733-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="60733-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="60733-110">Prerequisites</span></span>

<span data-ttu-id="60733-111">Чтобы настроить интеграцию Azure AD с JobScore, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="60733-111">To configure Azure AD integration with JobScore, you need the following items:</span></span>

- <span data-ttu-id="60733-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="60733-112">An Azure AD subscription</span></span>
- <span data-ttu-id="60733-113">подписка JobScore с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="60733-113">A JobScore single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="60733-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="60733-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="60733-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="60733-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="60733-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="60733-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="60733-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="60733-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="60733-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="60733-118">Scenario description</span></span>
<span data-ttu-id="60733-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="60733-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="60733-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="60733-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="60733-121">Добавление JobScore из коллекции</span><span class="sxs-lookup"><span data-stu-id="60733-121">Adding JobScore from the gallery</span></span>
2. <span data-ttu-id="60733-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="60733-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jobscore-from-the-gallery"></a><span data-ttu-id="60733-123">Добавление JobScore из коллекции</span><span class="sxs-lookup"><span data-stu-id="60733-123">Adding JobScore from the gallery</span></span>
<span data-ttu-id="60733-124">Чтобы настроить интеграцию JobScore с Azure AD, необходимо добавить JobScore из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="60733-124">To configure the integration of JobScore into Azure AD, you need to add JobScore from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="60733-125">**Чтобы добавить JobScore из коллекции, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="60733-125">**To add JobScore from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="60733-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="60733-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="60733-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="60733-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="60733-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="60733-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="60733-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="60733-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="60733-133">В поле поиска введите **JobScore**.</span><span class="sxs-lookup"><span data-stu-id="60733-133">In the search box, type **JobScore**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jobscore-tutorial/tutorial_jobscore_search.png)

5. <span data-ttu-id="60733-135">На панели результатов выберите **JobScore** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="60733-135">In the results panel, select **JobScore**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jobscore-tutorial/tutorial_jobscore_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="60733-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="60733-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="60733-138">В этом разделе описана настройка и проверка единого входа Azure AD в JobScore с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="60733-138">In this section, you configure and test Azure AD single sign-on with JobScore based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="60733-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в JobScore соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="60733-139">For single sign-on to work, Azure AD needs to know what the counterpart user in JobScore is to a user in Azure AD.</span></span> <span data-ttu-id="60733-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в JobScore.</span><span class="sxs-lookup"><span data-stu-id="60733-140">In other words, a link relationship between an Azure AD user and the related user in JobScore needs to be established.</span></span>

<span data-ttu-id="60733-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в JobScore.</span><span class="sxs-lookup"><span data-stu-id="60733-141">In JobScore, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="60733-142">Чтобы настроить и проверить единый вход Azure AD в JobScore, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="60733-142">To configure and test Azure AD single sign-on with JobScore, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="60733-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="60733-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="60733-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="60733-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="60733-145">**[Создание тестового пользователя JobScore](#creating-a-jobscore-test-user)** требуется для создания пользователя Britta Simon в JobScore, связанного с соответствующим представлением в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="60733-145">**[Creating a JobScore test user](#creating-a-jobscore-test-user)** - to have a counterpart of Britta Simon in JobScore that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="60733-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="60733-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="60733-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="60733-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="60733-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="60733-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="60733-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении JobScore.</span><span class="sxs-lookup"><span data-stu-id="60733-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your JobScore application.</span></span>

<span data-ttu-id="60733-150">**Чтобы настроить единый вход Azure AD в JobScore, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="60733-150">**To configure Azure AD single sign-on with JobScore, perform the following steps:**</span></span>

1. <span data-ttu-id="60733-151">На портале Azure на странице интеграции с приложением **JobScore** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="60733-151">In the Azure portal, on the **JobScore** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="60733-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="60733-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-jobscore-tutorial/tutorial_jobscore_samlbase.png)

3. <span data-ttu-id="60733-155">В разделе **Домены и URL-адреса приложения JobScore** выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="60733-155">On the **JobScore Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-jobscore-tutorial/tutorial_jobscore_url.png)

    <span data-ttu-id="60733-157">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://hire.jobscore.com/auth/adfs/<company name>`</span><span class="sxs-lookup"><span data-stu-id="60733-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://hire.jobscore.com/auth/adfs/<company name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="60733-158">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="60733-158">This value is not real.</span></span> <span data-ttu-id="60733-159">Вместо него необходимо указать фактический URL-адрес для входа.</span><span class="sxs-lookup"><span data-stu-id="60733-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="60733-160">Чтобы получить это значение, обратитесь в [службу поддержки клиентов JobScore](mailto:support@jobscore.com).</span><span class="sxs-lookup"><span data-stu-id="60733-160">Contact [JobScore Client support team](mailto:support@jobscore.com) to get this value.</span></span> 
 
4. <span data-ttu-id="60733-161">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="60733-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-jobscore-tutorial/tutorial_jobscore_certificate.png) 

5. <span data-ttu-id="60733-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="60733-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-jobscore-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="60733-165">Чтобы настроить единый вход на стороне **JobScore**, отправьте в [службу поддержки JobScore](mailto:support@jobscore.com) скачанный **XML-файл метаданных**.</span><span class="sxs-lookup"><span data-stu-id="60733-165">To configure single sign-on on **JobScore** side, you need to send the downloaded **Metadata XML** to [JobScore support team](mailto:support@jobscore.com).</span></span> 

> [!TIP]
> <span data-ttu-id="60733-166">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="60733-166">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="60733-167">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="60733-167">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="60733-168">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="60733-168">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="60733-169">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="60733-169">Creating an Azure AD test user</span></span>
<span data-ttu-id="60733-170">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="60733-170">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="60733-172">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="60733-172">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="60733-173">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="60733-173">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jobscore-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="60733-175">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="60733-175">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jobscore-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="60733-177">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="60733-177">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jobscore-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="60733-179">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="60733-179">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jobscore-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="60733-181">а.</span><span class="sxs-lookup"><span data-stu-id="60733-181">a.</span></span> <span data-ttu-id="60733-182">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="60733-182">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="60733-183">b.</span><span class="sxs-lookup"><span data-stu-id="60733-183">b.</span></span> <span data-ttu-id="60733-184">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="60733-184">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="60733-185">c.</span><span class="sxs-lookup"><span data-stu-id="60733-185">c.</span></span> <span data-ttu-id="60733-186">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="60733-186">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="60733-187">d.</span><span class="sxs-lookup"><span data-stu-id="60733-187">d.</span></span> <span data-ttu-id="60733-188">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="60733-188">Click **Create**.</span></span>
 
### <a name="creating-a-jobscore-test-user"></a><span data-ttu-id="60733-189">Создание тестового пользователя JobScore</span><span class="sxs-lookup"><span data-stu-id="60733-189">Creating a JobScore test user</span></span>

<span data-ttu-id="60733-190">В этом разделе описано, как создать пользователя Britta Simon в приложении JobScore.</span><span class="sxs-lookup"><span data-stu-id="60733-190">In this section, you create a user called Britta Simon in JobScore.</span></span> <span data-ttu-id="60733-191">Обратитесь в [службу поддержки JobScore](mailto:support@jobscore.com), чтобы добавить пользователей на платформу JobScore.</span><span class="sxs-lookup"><span data-stu-id="60733-191">Work with [JobScore support team](mailto:support@jobscore.com) to add the users in the JobScore platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="60733-192">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="60733-192">Assigning the Azure AD test user</span></span>

<span data-ttu-id="60733-193">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure путем предоставления доступа к JobScore.</span><span class="sxs-lookup"><span data-stu-id="60733-193">In this section, you enable Britta Simon to use Azure single sign-on by granting access to JobScore.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="60733-195">**Чтобы назначить пользователя Britta Simon в JobScore, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="60733-195">**To assign Britta Simon to JobScore, perform the following steps:**</span></span>

1. <span data-ttu-id="60733-196">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="60733-196">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="60733-198">В списке приложений выберите **JobScore**.</span><span class="sxs-lookup"><span data-stu-id="60733-198">In the applications list, select **JobScore**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-jobscore-tutorial/tutorial_jobscore_app.png) 

3. <span data-ttu-id="60733-200">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="60733-200">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="60733-202">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="60733-202">Click **Add** button.</span></span> <span data-ttu-id="60733-203">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="60733-203">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="60733-205">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="60733-205">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="60733-206">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="60733-206">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="60733-207">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="60733-207">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="60733-208">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="60733-208">Testing single sign-on</span></span>

<span data-ttu-id="60733-209">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="60733-209">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="60733-210">Щелкнув элемент JobScore на панели доступа, вы автоматически войдете в приложение JobScore.</span><span class="sxs-lookup"><span data-stu-id="60733-210">When you click the JobScore tile in the Access Panel, you should get automatically signed-on to your JobScore application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="60733-211">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="60733-211">Additional resources</span></span>

* [<span data-ttu-id="60733-212">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="60733-212">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="60733-213">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="60733-213">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jobscore-tutorial/tutorial_general_203.png

