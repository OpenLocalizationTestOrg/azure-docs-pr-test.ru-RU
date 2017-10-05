---
title: "Руководство по интеграции Azure Active Directory с приложением \"Люди\" | Документация Майкрософт"
description: "Сведения о настройке единого входа Azure Active Directory в приложение \"Люди\"."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7c9b6202-11dd-4bb6-a679-8fb0a7a0ef4e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: caa287a2ed8774965ef722685e4e950336e5e0ea
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-people"></a><span data-ttu-id="41db8-103">Руководство. Интеграция Azure Active Directory с приложением "Люди"</span><span class="sxs-lookup"><span data-stu-id="41db8-103">Tutorial: Azure Active Directory integration with People</span></span>

<span data-ttu-id="41db8-104">В этом руководстве описано, как интегрировать People с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="41db8-104">In this tutorial, you learn how to integrate People with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="41db8-105">Интеграция Azure AD с приложением "Люди" обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="41db8-105">Integrating People with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="41db8-106">С помощью Azure AD вы можете контролировать доступ к приложению "Люди".</span><span class="sxs-lookup"><span data-stu-id="41db8-106">You can control in Azure AD who has access to People</span></span>
- <span data-ttu-id="41db8-107">Вы можете включить автоматический вход пользователей в "Люди" (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="41db8-107">You can enable your users to automatically get signed-on to People (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="41db8-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="41db8-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="41db8-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="41db8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="41db8-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="41db8-110">Prerequisites</span></span>

<span data-ttu-id="41db8-111">Чтобы настроить интеграцию Azure AD с приложением "Люди", вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="41db8-111">To configure Azure AD integration with People, you need the following items:</span></span>

- <span data-ttu-id="41db8-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="41db8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="41db8-113">подписка People с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="41db8-113">A People single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="41db8-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="41db8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="41db8-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="41db8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="41db8-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="41db8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="41db8-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="41db8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="41db8-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="41db8-118">Scenario description</span></span>
<span data-ttu-id="41db8-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="41db8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="41db8-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="41db8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="41db8-121">Добавление приложения "Люди" из коллекции.</span><span class="sxs-lookup"><span data-stu-id="41db8-121">Adding People from the gallery</span></span>
2. <span data-ttu-id="41db8-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="41db8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-people-from-the-gallery"></a><span data-ttu-id="41db8-123">Добавление приложения "Люди" из коллекции.</span><span class="sxs-lookup"><span data-stu-id="41db8-123">Adding People from the gallery</span></span>
<span data-ttu-id="41db8-124">Чтобы настроить интеграцию приложения "Люди" с Azure AD, необходимо добавить это приложение из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="41db8-124">To configure the integration of People into Azure AD, you need to add People from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="41db8-125">**Чтобы добавить приложение "Люди" из коллекции, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="41db8-125">**To add People from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="41db8-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="41db8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="41db8-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="41db8-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="41db8-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="41db8-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="41db8-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="41db8-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="41db8-133">В поле поиска введите **Люди**.</span><span class="sxs-lookup"><span data-stu-id="41db8-133">In the search box, type **People**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-people-tutorial/tutorial_people_search.png)

5. <span data-ttu-id="41db8-135">На панели результатов выберите **People** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="41db8-135">In the results panel, select **People**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-people-tutorial/tutorial_people_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="41db8-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="41db8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="41db8-138">В этом разделе описана настройка и проверка единого входа Azure AD в People с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="41db8-138">In this section, you configure and test Azure AD single sign-on with People based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="41db8-139">Чтобы единый вход работал, Azure AD необходимо знать, какой пользователь в People соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="41db8-139">For single sign-on to work, Azure AD needs to know what the counterpart user in People is to a user in Azure AD.</span></span> <span data-ttu-id="41db8-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в People.</span><span class="sxs-lookup"><span data-stu-id="41db8-140">In other words, a link relationship between an Azure AD user and the related user in People needs to be established.</span></span>

<span data-ttu-id="41db8-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в People.</span><span class="sxs-lookup"><span data-stu-id="41db8-141">In People, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="41db8-142">Чтобы настроить и проверить единый вход Azure AD в приложение "Люди", вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="41db8-142">To configure and test Azure AD single sign-on with People, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="41db8-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="41db8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="41db8-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="41db8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="41db8-145">**[Создание тестового пользователя приложения People](#creating-a-people-test-user)** требуется для создания пользователя Britta Simon в приложении People, связанного с соответствующим представлением в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="41db8-145">**[Creating a People test user](#creating-a-people-test-user)** - to have a counterpart of Britta Simon in People that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="41db8-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="41db8-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="41db8-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="41db8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="41db8-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="41db8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="41db8-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в People.</span><span class="sxs-lookup"><span data-stu-id="41db8-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your People application.</span></span>

<span data-ttu-id="41db8-150">**Чтобы настроить единый вход Azure AD в приложение "Люди", сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="41db8-150">**To configure Azure AD single sign-on with People, perform the following steps:**</span></span>

1. <span data-ttu-id="41db8-151">На портале Azure на странице интеграции с приложением **People** выберите **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="41db8-151">In the Azure portal, on the **People** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="41db8-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="41db8-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-people-tutorial/tutorial_people_samlbase.png)

3. <span data-ttu-id="41db8-155">В разделе **Домены и URL-адреса приложения People** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="41db8-155">On the **People Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-people-tutorial/tutorial_people_url.png)

    <span data-ttu-id="41db8-157">а.</span><span class="sxs-lookup"><span data-stu-id="41db8-157">a.</span></span> <span data-ttu-id="41db8-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<company name>.peoplehr.com/`</span><span class="sxs-lookup"><span data-stu-id="41db8-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.peoplehr.com/`</span></span>

    <span data-ttu-id="41db8-159">b.</span><span class="sxs-lookup"><span data-stu-id="41db8-159">b.</span></span> <span data-ttu-id="41db8-160">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://www.peoplehr.com`</span><span class="sxs-lookup"><span data-stu-id="41db8-160">In the **Identifier** textbox, type a URL using the following pattern: `https://www.peoplehr.com`</span></span>

    <span data-ttu-id="41db8-161">c.</span><span class="sxs-lookup"><span data-stu-id="41db8-161">c.</span></span> <span data-ttu-id="41db8-162">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате: `https://<company name>.peoplehr.net/Pages/Saml/ConsumeAzureAD.aspx`.</span><span class="sxs-lookup"><span data-stu-id="41db8-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://<company name>.peoplehr.net/Pages/Saml/ConsumeAzureAD.aspx`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="41db8-163">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="41db8-163">These values are not real.</span></span> <span data-ttu-id="41db8-164">Замените их фактическими значениями идентификатора, URL-адреса ответа и URL-адреса входа.</span><span class="sxs-lookup"><span data-stu-id="41db8-164">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="41db8-165">Чтобы получить эти значения, обратитесь в [службу поддержки People](mailto:customerservices@peoplehr.com).</span><span class="sxs-lookup"><span data-stu-id="41db8-165">Contact [People Client support team](mailto:customerservices@peoplehr.com) to get these values.</span></span>

5. <span data-ttu-id="41db8-166">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="41db8-166">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-people-tutorial/tutorial_people_certificate.png) 

6. <span data-ttu-id="41db8-168">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="41db8-168">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-people-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="41db8-170">Чтобы настроить для приложения единый вход, нужно войти в клиент приложения "Люди" с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="41db8-170">To get SSO configured for your application, you need to sign-on to your People tenant as an administrator.</span></span>
   
8. <span data-ttu-id="41db8-171">В меню слева выберите **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="41db8-171">In the menu on the left side, click **Settings**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-people-tutorial/tutorial_people_001.png)

9. <span data-ttu-id="41db8-173">Нажмите **Компания**.</span><span class="sxs-lookup"><span data-stu-id="41db8-173">Click **Company**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-people-tutorial/tutorial_people_002.png)

10. <span data-ttu-id="41db8-175">Чтобы отправить скачанный файл метаданных, в разделе **Upload 'Single Sign On' SAML meta-data file** (Отправить файл метаданных SAML для единого входа) нажмите кнопку **Browse** (Обзор).</span><span class="sxs-lookup"><span data-stu-id="41db8-175">On the **Upload 'Single Sign On' SAML meta-data file**, click **Browse** to upload the downloaded metadata file.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-people-tutorial/tutorial_people_003.png)

> [!TIP]
> <span data-ttu-id="41db8-177">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="41db8-177">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="41db8-178">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="41db8-178">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="41db8-179">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="41db8-179">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="41db8-180">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="41db8-180">Creating an Azure AD test user</span></span>
<span data-ttu-id="41db8-181">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="41db8-181">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="41db8-183">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="41db8-183">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="41db8-184">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="41db8-184">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-people-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="41db8-186">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="41db8-186">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-people-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="41db8-188">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="41db8-188">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-people-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="41db8-190">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="41db8-190">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-people-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="41db8-192">а.</span><span class="sxs-lookup"><span data-stu-id="41db8-192">a.</span></span> <span data-ttu-id="41db8-193">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="41db8-193">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="41db8-194">b.</span><span class="sxs-lookup"><span data-stu-id="41db8-194">b.</span></span> <span data-ttu-id="41db8-195">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="41db8-195">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="41db8-196">c.</span><span class="sxs-lookup"><span data-stu-id="41db8-196">c.</span></span> <span data-ttu-id="41db8-197">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="41db8-197">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="41db8-198">d.</span><span class="sxs-lookup"><span data-stu-id="41db8-198">d.</span></span> <span data-ttu-id="41db8-199">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="41db8-199">Click **Create**.</span></span>
 
### <a name="creating-a-people-test-user"></a><span data-ttu-id="41db8-200">Создание тестового пользователя приложения "Люди"</span><span class="sxs-lookup"><span data-stu-id="41db8-200">Creating a People test user</span></span>

<span data-ttu-id="41db8-201">В этом разделе описано, как создать пользователя Britta Simon в приложении People.</span><span class="sxs-lookup"><span data-stu-id="41db8-201">In this section, you create a user called Britta Simon in People.</span></span> <span data-ttu-id="41db8-202">Обратитесь в [службу поддержки клиентов People](mailto:customerservices@peoplehr.com), чтобы добавить пользователей на платформу People.</span><span class="sxs-lookup"><span data-stu-id="41db8-202">Work with [People Client support team](mailto:customerservices@peoplehr.com) to add the users in the People platform.</span></span> <span data-ttu-id="41db8-203">Перед использованием единого входа необходимо создать и активировать пользователей.</span><span class="sxs-lookup"><span data-stu-id="41db8-203">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="41db8-204">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="41db8-204">Assigning the Azure AD test user</span></span>

<span data-ttu-id="41db8-205">В этом разделе описано, как предоставить пользователю Britta Simon доступ к People, чтобы он мог использовать единый вход Azure.</span><span class="sxs-lookup"><span data-stu-id="41db8-205">In this section, you enable Britta Simon to use Azure single sign-on by granting access to People.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="41db8-207">**Чтобы назначить пользователя Britta Simon в приложении "Люди", сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="41db8-207">**To assign Britta Simon to People, perform the following steps:**</span></span>

1. <span data-ttu-id="41db8-208">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="41db8-208">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="41db8-210">В списке приложений выберите **Люди**.</span><span class="sxs-lookup"><span data-stu-id="41db8-210">In the applications list, select **People**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-people-tutorial/tutorial_people_app.png) 

3. <span data-ttu-id="41db8-212">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="41db8-212">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="41db8-214">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="41db8-214">Click **Add** button.</span></span> <span data-ttu-id="41db8-215">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="41db8-215">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="41db8-217">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="41db8-217">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="41db8-218">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="41db8-218">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="41db8-219">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="41db8-219">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="41db8-220">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="41db8-220">Testing single sign-on</span></span>

<span data-ttu-id="41db8-221">Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="41db8-221">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="41db8-222">Щелкнув элемент "Люди" на панели доступа, вы автоматически войдете в приложение "Люди".</span><span class="sxs-lookup"><span data-stu-id="41db8-222">When you click the People tile in the Access Panel, you should get automatically signed-on to your People application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="41db8-223">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="41db8-223">Additional resources</span></span>

* [<span data-ttu-id="41db8-224">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="41db8-224">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="41db8-225">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="41db8-225">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-people-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-people-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-people-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-people-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-people-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-people-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-people-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-people-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-people-tutorial/tutorial_general_203.png

