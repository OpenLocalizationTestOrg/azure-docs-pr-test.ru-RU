---
title: "Руководство по интеграции Azure Active Directory с RightAnswers | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в приложении RightAnswers."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7f09e25a-a716-41e1-8ca3-fd00e3d1b8cc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: e5985831598a0e5b1277d2c6cd02b03c919aad4d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rightanswers"></a><span data-ttu-id="824dd-103">Учебник. Интеграция Azure Active Directory с RightAnswers</span><span class="sxs-lookup"><span data-stu-id="824dd-103">Tutorial: Azure Active Directory integration with RightAnswers</span></span>

<span data-ttu-id="824dd-104">В этом учебнике описано, как интегрировать приложение RightAnswers с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="824dd-104">In this tutorial, you learn how to integrate RightAnswers with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="824dd-105">Интеграция Azure AD с приложением RightAnswers обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="824dd-105">Integrating RightAnswers with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="824dd-106">С помощью Azure AD можно управлять доступом к RightAnswers.</span><span class="sxs-lookup"><span data-stu-id="824dd-106">You can control in Azure AD who has access to RightAnswers</span></span>
- <span data-ttu-id="824dd-107">Вы можете включить автоматический вход пользователей в RightAnswers (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="824dd-107">You can enable your users to automatically get signed-on to RightAnswers (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="824dd-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="824dd-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="824dd-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="824dd-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="824dd-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="824dd-110">Prerequisites</span></span>

<span data-ttu-id="824dd-111">Чтобы настроить интеграцию Azure AD с RightAnswers, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="824dd-111">To configure Azure AD integration with RightAnswers, you need the following items:</span></span>

- <span data-ttu-id="824dd-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="824dd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="824dd-113">подписка RightAnswers с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="824dd-113">A RightAnswers single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="824dd-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="824dd-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="824dd-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="824dd-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="824dd-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="824dd-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="824dd-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="824dd-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="824dd-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="824dd-118">Scenario description</span></span>
<span data-ttu-id="824dd-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="824dd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="824dd-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="824dd-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="824dd-121">Добавление RightAnswers из коллекции</span><span class="sxs-lookup"><span data-stu-id="824dd-121">Adding RightAnswers from the gallery</span></span>
2. <span data-ttu-id="824dd-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="824dd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-rightanswers-from-the-gallery"></a><span data-ttu-id="824dd-123">Добавление RightAnswers из коллекции</span><span class="sxs-lookup"><span data-stu-id="824dd-123">Adding RightAnswers from the gallery</span></span>
<span data-ttu-id="824dd-124">Чтобы настроить интеграцию RightAnswers с Azure AD, необходимо добавить RightAnswers из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="824dd-124">To configure the integration of RightAnswers into Azure AD, you need to add RightAnswers from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="824dd-125">**Чтобы добавить RightAnswers из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="824dd-125">**To add RightAnswers from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="824dd-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="824dd-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="824dd-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="824dd-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="824dd-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="824dd-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="824dd-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="824dd-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="824dd-133">В поле поиска введите **RightAnswers**.</span><span class="sxs-lookup"><span data-stu-id="824dd-133">In the search box, type **RightAnswers**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-rightanswers-tutorial/tutorial_rightanswers_search.png)

5. <span data-ttu-id="824dd-135">На панели результатов выберите **RightAnswers** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="824dd-135">In the results panel, select **RightAnswers**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-rightanswers-tutorial/tutorial_rightanswers_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="824dd-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="824dd-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="824dd-138">В этом разделе описана настройка и проверка единого входа Azure AD в RightAnswers с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="824dd-138">In this section, you configure and test Azure AD single sign-on with RightAnswers based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="824dd-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в RightAnswers соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="824dd-139">For single sign-on to work, Azure AD needs to know what the counterpart user in RightAnswers is to a user in Azure AD.</span></span> <span data-ttu-id="824dd-140">Иными словами, необходимо установить связь между пользователям Azure AD и соответствующим пользователем в RightAnswers.</span><span class="sxs-lookup"><span data-stu-id="824dd-140">In other words, a link relationship between an Azure AD user and the related user in RightAnswers needs to be established.</span></span>

<span data-ttu-id="824dd-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в RightAnswers.</span><span class="sxs-lookup"><span data-stu-id="824dd-141">In RightAnswers, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="824dd-142">Чтобы настроить и проверить единый вход Azure AD в RightAnswers, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="824dd-142">To configure and test Azure AD single sign-on with RightAnswers, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="824dd-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="824dd-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="824dd-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="824dd-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="824dd-145">**[Создание тестового пользователя RightAnswers](#creating-a-rightanswers-test-user)** требуется для создания в RightAnswers пользователя Britta Simon, связанного с представлением этого же пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="824dd-145">**[Creating a RightAnswers test user](#creating-a-rightanswers-test-user)** - to have a counterpart of Britta Simon in RightAnswers that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="824dd-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="824dd-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="824dd-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="824dd-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="824dd-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="824dd-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="824dd-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении RightAnswers.</span><span class="sxs-lookup"><span data-stu-id="824dd-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your RightAnswers application.</span></span>

<span data-ttu-id="824dd-150">**Чтобы настроить единый вход Azure AD в RightAnswers, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="824dd-150">**To configure Azure AD single sign-on with RightAnswers, perform the following steps:**</span></span>

1. <span data-ttu-id="824dd-151">На портале Azure на странице интеграции с приложением **RightAnswers** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="824dd-151">In the Azure portal, on the **RightAnswers** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="824dd-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="824dd-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-rightanswers-tutorial/tutorial_rightanswers_samlbase.png)

3. <span data-ttu-id="824dd-155">В разделе **Домен и URL-адреса приложения RightAnswers** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="824dd-155">On the **RightAnswers Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-rightanswers-tutorial/tutorial_rightanswers_url.png)

    <span data-ttu-id="824dd-157">а.</span><span class="sxs-lookup"><span data-stu-id="824dd-157">a.</span></span> <span data-ttu-id="824dd-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<subdomain>.rightanswers.com/portal/ss/`</span><span class="sxs-lookup"><span data-stu-id="824dd-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.rightanswers.com/portal/ss/`</span></span>

    <span data-ttu-id="824dd-159">b.</span><span class="sxs-lookup"><span data-stu-id="824dd-159">b.</span></span> <span data-ttu-id="824dd-160">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<subdomain>.rightanswers.com:<identifier>/portal`</span><span class="sxs-lookup"><span data-stu-id="824dd-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.rightanswers.com:<identifier>/portal`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="824dd-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="824dd-161">These values are not real.</span></span> <span data-ttu-id="824dd-162">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="824dd-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="824dd-163">Чтобы получить эти значения, обратитесь в [службу поддержки клиентов RightAnswers](https://www.rightanswers.com/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="824dd-163">Contact [RightAnswers Client support team](https://www.rightanswers.com/contact-us/) to get these values.</span></span> 
 
4. <span data-ttu-id="824dd-164">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="824dd-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-rightanswers-tutorial/tutorial_rightanswers_certificate.png) 

5. <span data-ttu-id="824dd-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="824dd-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-rightanswers-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="824dd-168">Чтобы настроить единый вход на стороне **RightAnswers**, отправьте скачанный **XML-файл метаданных** в [службу поддержки RightAnswers](https://www.rightanswers.com/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="824dd-168">To configure single sign-on on **RightAnswers** side, you need to send the downloaded **Metadata XML** to [RightAnswers support team](https://www.rightanswers.com/contact-us/).</span></span>

    >[!NOTE]
    ><span data-ttu-id="824dd-169">Настройка единого входа должна выполняться службой поддержки RightAnswers.</span><span class="sxs-lookup"><span data-stu-id="824dd-169">Your RightAnswers support team has to do the actual SSO configuration.</span></span>
    ><span data-ttu-id="824dd-170">Как только единый вход для вашей подписки будет включен, вы получите уведомление.</span><span class="sxs-lookup"><span data-stu-id="824dd-170">You will get a notification when SSO has been enabled for your subscription.</span></span>

> [!TIP]
> <span data-ttu-id="824dd-171">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="824dd-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="824dd-172">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="824dd-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="824dd-173">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="824dd-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="824dd-174">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="824dd-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="824dd-175">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="824dd-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="824dd-177">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="824dd-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="824dd-178">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="824dd-178">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-rightanswers-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="824dd-180">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="824dd-180">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-rightanswers-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="824dd-182">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="824dd-182">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-rightanswers-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="824dd-184">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="824dd-184">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-rightanswers-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="824dd-186">а.</span><span class="sxs-lookup"><span data-stu-id="824dd-186">a.</span></span> <span data-ttu-id="824dd-187">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="824dd-187">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="824dd-188">b.</span><span class="sxs-lookup"><span data-stu-id="824dd-188">b.</span></span> <span data-ttu-id="824dd-189">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="824dd-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="824dd-190">c.</span><span class="sxs-lookup"><span data-stu-id="824dd-190">c.</span></span> <span data-ttu-id="824dd-191">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="824dd-191">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="824dd-192">d.</span><span class="sxs-lookup"><span data-stu-id="824dd-192">d.</span></span> <span data-ttu-id="824dd-193">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="824dd-193">Click **Create**.</span></span>
 
### <a name="creating-a-rightanswers-test-user"></a><span data-ttu-id="824dd-194">Создание тестового пользователя RightAnswers</span><span class="sxs-lookup"><span data-stu-id="824dd-194">Creating a RightAnswers test user</span></span>

<span data-ttu-id="824dd-195">Чтобы пользователи Azure AD могли выполнять вход в RightAnswers, они должны быть подготовлены в RightAnswers.</span><span class="sxs-lookup"><span data-stu-id="824dd-195">To enable Azure AD users to log in to RightAnswers, they must be provisioned into RightAnswers.</span></span> <span data-ttu-id="824dd-196">В случае RightAnswers подготовка выполняется автоматически, так что вам не нужно ничего делать.</span><span class="sxs-lookup"><span data-stu-id="824dd-196">When RightAnswers, provisioning is an automated task so there is no action item for you.</span></span>

<span data-ttu-id="824dd-197">В случае необходимости пользователи создаются автоматически при первой попытке входа в систему.</span><span class="sxs-lookup"><span data-stu-id="824dd-197">Users are automatically created if necessary during the first single sign-on attempt.</span></span>

>[!NOTE]
><span data-ttu-id="824dd-198">Вы можете использовать любые другие инструменты создания учетных записей пользователя RightAnswers или API, предоставляемые RightAnswers для подготовки учетных записей пользователя AAD.</span><span class="sxs-lookup"><span data-stu-id="824dd-198">You can use any other RightAnswers user account creation tools or APIs provided by RightAnswers to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="824dd-199">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="824dd-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="824dd-200">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к RightAnswers.</span><span class="sxs-lookup"><span data-stu-id="824dd-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to RightAnswers.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="824dd-202">**Чтобы назначить пользователя Britta Simon приложению RightAnswers, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="824dd-202">**To assign Britta Simon to RightAnswers, perform the following steps:**</span></span>

1. <span data-ttu-id="824dd-203">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="824dd-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="824dd-205">В списке приложений выберите **RightAnswers**.</span><span class="sxs-lookup"><span data-stu-id="824dd-205">In the applications list, select **RightAnswers**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-rightanswers-tutorial/tutorial_rightanswers_app.png) 

3. <span data-ttu-id="824dd-207">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="824dd-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="824dd-209">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="824dd-209">Click **Add** button.</span></span> <span data-ttu-id="824dd-210">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="824dd-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="824dd-212">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="824dd-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="824dd-213">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="824dd-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="824dd-214">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="824dd-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="824dd-215">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="824dd-215">Testing single sign-on</span></span>

<span data-ttu-id="824dd-216">Если вы хотите проверить параметры единого входа, откройте панель доступа.</span><span class="sxs-lookup"><span data-stu-id="824dd-216">If you want to test your SSO settings, open the Access Panel.</span></span> <span data-ttu-id="824dd-217">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="824dd-217">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>
## <a name="additional-resources"></a><span data-ttu-id="824dd-218">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="824dd-218">Additional resources</span></span>

* [<span data-ttu-id="824dd-219">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="824dd-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="824dd-220">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="824dd-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-rightanswers-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rightanswers-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rightanswers-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rightanswers-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rightanswers-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rightanswers-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rightanswers-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rightanswers-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rightanswers-tutorial/tutorial_general_203.png

