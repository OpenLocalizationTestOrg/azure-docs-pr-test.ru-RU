---
title: "Руководство по интеграции Azure Active Directory с Asset Bank | Документация Майкрософт"
description: "Узнайте, как настроить единый вход для Azure Active Directory и Asset Bank."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3006ad6e-8831-41cd-94aa-7e7ae770ce7b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 17bc0082e3721b50269cb4b17884c0e4a4cbcb5d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-asset-bank"></a><span data-ttu-id="a8cda-103">Учебник. Интеграция Azure Active Directory с Asset Bank</span><span class="sxs-lookup"><span data-stu-id="a8cda-103">Tutorial: Azure Active Directory integration with Asset Bank</span></span>

<span data-ttu-id="a8cda-104">В этом руководстве описано, как интегрировать Asset Bank с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a8cda-104">In this tutorial, you learn how to integrate Asset Bank with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a8cda-105">Интеграция Asset Bank с Azure AD дает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="a8cda-105">Integrating Asset Bank with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a8cda-106">С помощью Azure AD вы можете контролировать доступ к Asset Bank.</span><span class="sxs-lookup"><span data-stu-id="a8cda-106">You can control in Azure AD who has access to Asset Bank</span></span>
- <span data-ttu-id="a8cda-107">Вы можете включить автоматический вход пользователей в Asset Bank (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a8cda-107">You can enable your users to automatically get signed-on to Asset Bank (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a8cda-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="a8cda-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a8cda-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a8cda-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a8cda-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a8cda-110">Prerequisites</span></span>

<span data-ttu-id="a8cda-111">Чтобы настроить интеграцию Azure AD с Asset Bank, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="a8cda-111">To configure Azure AD integration with Asset Bank, you need the following items:</span></span>

- <span data-ttu-id="a8cda-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="a8cda-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a8cda-113">подписка Asset Bank с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="a8cda-113">An Asset Bank single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a8cda-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="a8cda-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a8cda-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="a8cda-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a8cda-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="a8cda-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a8cda-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a8cda-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a8cda-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="a8cda-118">Scenario description</span></span>
<span data-ttu-id="a8cda-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="a8cda-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a8cda-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="a8cda-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a8cda-121">Добавление Asset Bank из коллекции</span><span class="sxs-lookup"><span data-stu-id="a8cda-121">Adding Asset Bank from the gallery</span></span>
2. <span data-ttu-id="a8cda-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="a8cda-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-asset-bank-from-the-gallery"></a><span data-ttu-id="a8cda-123">Добавление Asset Bank из коллекции</span><span class="sxs-lookup"><span data-stu-id="a8cda-123">Adding Asset Bank from the gallery</span></span>
<span data-ttu-id="a8cda-124">Чтобы настроить интеграцию Asset Bank с Azure AD, необходимо добавить Asset Bank из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="a8cda-124">To configure the integration of Asset Bank into Azure AD, you need to add Asset Bank from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a8cda-125">**Чтобы добавить Asset Bank из коллекции, выполните следующее.**</span><span class="sxs-lookup"><span data-stu-id="a8cda-125">**To add Asset Bank from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a8cda-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a8cda-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a8cda-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="a8cda-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a8cda-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="a8cda-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="a8cda-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="a8cda-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="a8cda-133">В поле поиска введите **Asset Bank**.</span><span class="sxs-lookup"><span data-stu-id="a8cda-133">In the search box, type **Asset Bank**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-assetbank-tutorial/tutorial_assetbank_search.png)

5. <span data-ttu-id="a8cda-135">На панели результатов выберите **Asset Bank** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="a8cda-135">In the results panel, select **Asset Bank**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-assetbank-tutorial/tutorial_assetbank_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a8cda-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="a8cda-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a8cda-138">В этом разделе описана настройка и проверка единого входа Azure AD в Asset Bank с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a8cda-138">In this section, you configure and test Azure AD single sign-on with Asset Bank based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a8cda-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Asset Bank соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a8cda-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Asset Bank is to a user in Azure AD.</span></span> <span data-ttu-id="a8cda-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Asset Bank.</span><span class="sxs-lookup"><span data-stu-id="a8cda-140">In other words, a link relationship between an Azure AD user and the related user in Asset Bank needs to be established.</span></span>

<span data-ttu-id="a8cda-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Asset Bank.</span><span class="sxs-lookup"><span data-stu-id="a8cda-141">In Asset Bank, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a8cda-142">Чтобы настроить и проверить единый вход Azure AD в Asset Bank, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="a8cda-142">To configure and test Azure AD single sign-on with Asset Bank, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a8cda-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="a8cda-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a8cda-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a8cda-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a8cda-145">**[Создание тестового пользователя Asset Bank](#creating-an-asset-bank-test-user)** нужно для того, чтобы в Asset Bank также существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a8cda-145">**[Creating an Asset Bank test user](#creating-an-asset-bank-test-user)** - to have a counterpart of Britta Simon in Asset Bank that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a8cda-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a8cda-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a8cda-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="a8cda-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a8cda-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="a8cda-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a8cda-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Asset Bank.</span><span class="sxs-lookup"><span data-stu-id="a8cda-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Asset Bank application.</span></span>

<span data-ttu-id="a8cda-150">**Чтобы настроить единый вход Azure AD в Asset Bank, выполните следующее.**</span><span class="sxs-lookup"><span data-stu-id="a8cda-150">**To configure Azure AD single sign-on with Asset Bank, perform the following steps:**</span></span>

1. <span data-ttu-id="a8cda-151">На портале Azure на странице интеграции с приложением **Asset Bank** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="a8cda-151">In the Azure portal, on the **Asset Bank** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="a8cda-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="a8cda-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-assetbank-tutorial/tutorial_assetbank_samlbase.png)

3. <span data-ttu-id="a8cda-155">В разделе **Домены и URL-адреса приложения Asset Bank** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="a8cda-155">On the **Asset Bank Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-assetbank-tutorial/tutorial_assetbank_url.png)

    <span data-ttu-id="a8cda-157">а.</span><span class="sxs-lookup"><span data-stu-id="a8cda-157">a.</span></span> <span data-ttu-id="a8cda-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<companyname>.assetbank-server.com`</span><span class="sxs-lookup"><span data-stu-id="a8cda-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.assetbank-server.com`</span></span>

    <span data-ttu-id="a8cda-159">b.</span><span class="sxs-lookup"><span data-stu-id="a8cda-159">b.</span></span> <span data-ttu-id="a8cda-160">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<companyname>.assetbank-server.com/shibboleth`</span><span class="sxs-lookup"><span data-stu-id="a8cda-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.assetbank-server.com/shibboleth`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a8cda-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="a8cda-161">These values are not real.</span></span> <span data-ttu-id="a8cda-162">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="a8cda-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="a8cda-163">Чтобы получить эти значения, обратитесь к [группе поддержки Asset Bank](mailto:support@assetbank.co.uk).</span><span class="sxs-lookup"><span data-stu-id="a8cda-163">Contact [Asset Bank Client support team](mailto:support@assetbank.co.uk) to get these values.</span></span> 
 
4. <span data-ttu-id="a8cda-164">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="a8cda-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-assetbank-tutorial/tutorial_assetbank_certificate.png) 

5. <span data-ttu-id="a8cda-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="a8cda-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-assetbank-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a8cda-168">Чтобы настроить единый вход на стороне **Asset Bank**, отправьте скачанный **XML-файл метаданных** [группе поддержки Asset Bank](mailto:support@assetbank.co.uk).</span><span class="sxs-lookup"><span data-stu-id="a8cda-168">To configure single sign-on on **Asset Bank** side, you need to send the downloaded **Metadata XML** to [Asset Bank support team](mailto:support@assetbank.co.uk).</span></span> 


> [!TIP]
> <span data-ttu-id="a8cda-169">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="a8cda-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a8cda-170">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="a8cda-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a8cda-171">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="a8cda-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a8cda-172">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="a8cda-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="a8cda-173">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a8cda-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="a8cda-175">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="a8cda-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a8cda-176">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a8cda-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-assetbank-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a8cda-178">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="a8cda-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-assetbank-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a8cda-180">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="a8cda-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-assetbank-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a8cda-182">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="a8cda-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-assetbank-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a8cda-184">а.</span><span class="sxs-lookup"><span data-stu-id="a8cda-184">a.</span></span> <span data-ttu-id="a8cda-185">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a8cda-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a8cda-186">b.</span><span class="sxs-lookup"><span data-stu-id="a8cda-186">b.</span></span> <span data-ttu-id="a8cda-187">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a8cda-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a8cda-188">c.</span><span class="sxs-lookup"><span data-stu-id="a8cda-188">c.</span></span> <span data-ttu-id="a8cda-189">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="a8cda-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a8cda-190">d.</span><span class="sxs-lookup"><span data-stu-id="a8cda-190">d.</span></span> <span data-ttu-id="a8cda-191">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="a8cda-191">Click **Create**.</span></span>
 
### <a name="creating-an-asset-bank-test-user"></a><span data-ttu-id="a8cda-192">Создание тестового пользователя Asset Bank</span><span class="sxs-lookup"><span data-stu-id="a8cda-192">Creating an Asset Bank test user</span></span>

<span data-ttu-id="a8cda-193">Цель этого раздела — создать пользователя Britta Simon в Asset Bank.</span><span class="sxs-lookup"><span data-stu-id="a8cda-193">The objective of this section is to create a user called Britta Simon in Asset Bank.</span></span> <span data-ttu-id="a8cda-194">Приложение Asset Bank поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="a8cda-194">Asset Bank supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="a8cda-195">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="a8cda-195">There is no action item for you in this section.</span></span> <span data-ttu-id="a8cda-196">Пользователь будет создан при попытке получить доступ к Asset Bank (если он еще не создан).</span><span class="sxs-lookup"><span data-stu-id="a8cda-196">A new user is created during an attempt to access Asset Bank if it doesn't exist yet.</span></span> 

>[!NOTE]
><span data-ttu-id="a8cda-197">Чтобы создать пользователя вручную, обратитесь к [группе поддержки Asset Bank](mailto:support@assetbank.co.uk).</span><span class="sxs-lookup"><span data-stu-id="a8cda-197">If you need to create a user manually, you need to contact the [Asset Bank support team](mailto:support@assetbank.co.uk).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a8cda-198">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="a8cda-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a8cda-199">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к Asset Bank.</span><span class="sxs-lookup"><span data-stu-id="a8cda-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Asset Bank.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="a8cda-201">**Чтобы назначить пользователя Britta Simon в Asset Bank, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="a8cda-201">**To assign Britta Simon to Asset Bank, perform the following steps:**</span></span>

1. <span data-ttu-id="a8cda-202">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="a8cda-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="a8cda-204">Из списка приложений выберите **Asset Bank**.</span><span class="sxs-lookup"><span data-stu-id="a8cda-204">In the applications list, select **Asset Bank**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-assetbank-tutorial/tutorial_assetbank_app.png) 

3. <span data-ttu-id="a8cda-206">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="a8cda-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="a8cda-208">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="a8cda-208">Click **Add** button.</span></span> <span data-ttu-id="a8cda-209">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="a8cda-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="a8cda-211">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="a8cda-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a8cda-212">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="a8cda-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a8cda-213">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="a8cda-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a8cda-214">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="a8cda-214">Testing single sign-on</span></span>

<span data-ttu-id="a8cda-215">Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="a8cda-215">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="a8cda-216">Щелкнув элемент "Asset Bank" на панели доступа, вы автоматически войдете в приложение Asset Bank.</span><span class="sxs-lookup"><span data-stu-id="a8cda-216">When you click the Asset Bank tile in the Access Panel, you should get automatically signed-on to your Asset Bank application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="a8cda-217">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="a8cda-217">Additional resources</span></span>

* [<span data-ttu-id="a8cda-218">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a8cda-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a8cda-219">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a8cda-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-assetbank-tutorial/tutorial_general_203.png

