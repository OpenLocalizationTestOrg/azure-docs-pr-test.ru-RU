---
title: "Руководство по интеграции Azure Active Directory с MobileXpense | Документы Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в приложении MobileXpense."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e649fc4e-3e15-4948-b977-00bfe9f7db13
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/25/2017
ms.author: jeedes
ms.openlocfilehash: 030a1fc9f36d6fcfa607552d85ce232e36eaa64b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-mobilexpense"></a><span data-ttu-id="6d97f-103">Руководство. Интеграция Azure Active Directory с MobileXpense</span><span class="sxs-lookup"><span data-stu-id="6d97f-103">Tutorial: Azure Active Directory integration with MobileXpense</span></span>

<span data-ttu-id="6d97f-104">В этом руководстве описано, как интегрировать MobileXpense с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6d97f-104">In this tutorial, you learn how to integrate MobileXpense with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6d97f-105">Интеграция Azure AD с MobileXpense обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="6d97f-105">Integrating MobileXpense with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6d97f-106">С помощью Azure AD вы можете контролировать доступ к MobileXpense</span><span class="sxs-lookup"><span data-stu-id="6d97f-106">You can control in Azure AD who has access to MobileXpense</span></span>
- <span data-ttu-id="6d97f-107">Вы можете включить автоматический вход пользователей в MobileXpense (единый вход) с учетной записью Azure AD</span><span class="sxs-lookup"><span data-stu-id="6d97f-107">You can enable your users to automatically get signed-on to MobileXpense (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6d97f-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="6d97f-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="6d97f-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6d97f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6d97f-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="6d97f-110">Prerequisites</span></span>

<span data-ttu-id="6d97f-111">Чтобы настроить интеграцию Azure AD с MobileXpense, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="6d97f-111">To configure Azure AD integration with MobileXpense, you need the following items:</span></span>

- <span data-ttu-id="6d97f-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="6d97f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6d97f-113">подписка на MobileXpense с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="6d97f-113">A MobileXpense single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6d97f-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="6d97f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6d97f-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="6d97f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6d97f-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="6d97f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6d97f-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6d97f-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6d97f-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="6d97f-118">Scenario description</span></span>
<span data-ttu-id="6d97f-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="6d97f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6d97f-120">Сценарий, описанный в этом руководстве, состоит из двух стандартных блоков.</span><span class="sxs-lookup"><span data-stu-id="6d97f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6d97f-121">Добавление MobileXpense из коллекции</span><span class="sxs-lookup"><span data-stu-id="6d97f-121">Adding MobileXpense from the gallery</span></span>
2. <span data-ttu-id="6d97f-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="6d97f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-mobilexpense-from-the-gallery"></a><span data-ttu-id="6d97f-123">Добавление MobileXpense из коллекции</span><span class="sxs-lookup"><span data-stu-id="6d97f-123">Adding MobileXpense from the gallery</span></span>
<span data-ttu-id="6d97f-124">Чтобы настроить интеграцию MobileXpense с Azure AD, необходимо добавить MobileXpense из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="6d97f-124">To configure the integration of MobileXpense into Azure AD, you need to add MobileXpense from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6d97f-125">**Чтобы добавить MobileXpense из коллекции, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="6d97f-125">**To add MobileXpense from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6d97f-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6d97f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6d97f-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="6d97f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6d97f-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="6d97f-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="6d97f-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="6d97f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="6d97f-133">В поле поиска введите **MobileXpense**.</span><span class="sxs-lookup"><span data-stu-id="6d97f-133">In the search box, type **MobileXpense**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mobilexpense-tutorial/tutorial_mobilexpense_search.png)

5. <span data-ttu-id="6d97f-135">На панели результатов выберите **MobileXpense** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="6d97f-135">In the results panel, select **MobileXpense**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mobilexpense-tutorial/tutorial_mobilexpense_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6d97f-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="6d97f-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6d97f-138">В этом разделе описано, как настроить и проверить единый вход Azure AD в MobileXpense с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6d97f-138">In this section, you configure and test Azure AD single sign-on with MobileXpense based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="6d97f-139">Для настройки единого входа в Azure AD необходимо знать, какой пользователь в MobileXpense соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6d97f-139">For single sign-on to work, Azure AD needs to know what the counterpart user in MobileXpense is to a user in Azure AD.</span></span> <span data-ttu-id="6d97f-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в MobileXpense.</span><span class="sxs-lookup"><span data-stu-id="6d97f-140">In other words, a link relationship between an Azure AD user and the related user in MobileXpense needs to be established.</span></span>

<span data-ttu-id="6d97f-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в MobileXpense.</span><span class="sxs-lookup"><span data-stu-id="6d97f-141">In MobileXpense, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="6d97f-142">Чтобы настроить и проверить единый вход Azure AD в MobileXpense, необходимо выполнить следующие стандартные действия:</span><span class="sxs-lookup"><span data-stu-id="6d97f-142">To configure and test Azure AD single sign-on with MobileXpense, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6d97f-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="6d97f-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6d97f-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6d97f-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6d97f-145">**[Создание тестового пользователя MobileXpense](#creating-a-mobilexpense-test-user)** требуется для создания в MobileXpense пользователя Britta Simon, связанного с представлением этого пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6d97f-145">**[Creating a MobileXpense test user](#creating-a-mobilexpense-test-user)** - to have a counterpart of Britta Simon in MobileXpense that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="6d97f-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6d97f-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6d97f-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="6d97f-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6d97f-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="6d97f-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6d97f-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и как настроить его в приложении MobileXpense.</span><span class="sxs-lookup"><span data-stu-id="6d97f-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your MobileXpense application.</span></span>

<span data-ttu-id="6d97f-150">**Чтобы настроить единый вход Azure AD в MobileXpense, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="6d97f-150">**To configure Azure AD single sign-on with MobileXpense, perform the following steps:**</span></span>

1. <span data-ttu-id="6d97f-151">На портале Azure на странице интеграции с приложением **MobileXpense** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="6d97f-151">In the Azure portal, on the **MobileXpense** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="6d97f-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="6d97f-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-mobilexpense-tutorial/tutorial_mobilexpense_samlbase.png)

3. <span data-ttu-id="6d97f-155">Если вы хотите настроить приложение в **режиме, инициированном поставщиком удостоверений**, то в разделе **Домены и URL-адреса приложения MobileXpense** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="6d97f-155">On the **MobileXpense Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-mobilexpense-tutorial/tutorial_mobilexpense_url11.png)

    <span data-ttu-id="6d97f-157">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате: `https://<sub domain>.mobilexpense.com/SSO/SAML20/SAML/AssertionConsumerService.aspx`.</span><span class="sxs-lookup"><span data-stu-id="6d97f-157">In the **Reply URL** textbox, type a URL using the following pattern: `https://<sub domain>.mobilexpense.com/SSO/SAML20/SAML/AssertionConsumerService.aspx`</span></span>

4. <span data-ttu-id="6d97f-158">Установите флажок **Показать дополнительные параметры URL-адресов**, если хотите настроить приложение для работы в режиме, инициируемом **поставщиком услуг**:</span><span class="sxs-lookup"><span data-stu-id="6d97f-158">Check **Show advanced URL settings**, If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-mobilexpense-tutorial/tutorial_mobilexpense_url22.png)

<span data-ttu-id="6d97f-160">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<sub domain>.mobilexpense.com/<customername>`</span><span class="sxs-lookup"><span data-stu-id="6d97f-160">In the **Sign-on URL** textbox, type a URL using the following pattern:: `https://<sub domain>.mobilexpense.com/<customername>`</span></span>

> [!NOTE] 
> <span data-ttu-id="6d97f-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="6d97f-161">These values are not real.</span></span> <span data-ttu-id="6d97f-162">Измените их на фактические значения URL-адреса ответа и URL-адреса входа.</span><span class="sxs-lookup"><span data-stu-id="6d97f-162">Update these values with the actual Reply URL and Sign-On URL.</span></span> <span data-ttu-id="6d97f-163">Чтобы получить их, обратитесь в [службу поддержки клиентов MobileXpense](http://www.mobilexpense.net/contact).</span><span class="sxs-lookup"><span data-stu-id="6d97f-163">Contact [MobileXpense Client support team](http://www.mobilexpense.net/contact) to get these values.</span></span> 

5. <span data-ttu-id="6d97f-164">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="6d97f-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-mobilexpense-tutorial/tutorial_mobilexpense_certificate.png) 

6. <span data-ttu-id="6d97f-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="6d97f-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="6d97f-168">Чтобы настроить единый вход на стороне **MobileXpense**, отправьте скачанный **XML-файл метаданных** в [службу поддержки MobileXpense](http://www.mobilexpense.net/contact).</span><span class="sxs-lookup"><span data-stu-id="6d97f-168">To configure single sign-on on **MobileXpense** side, you need to send the downloaded **Metadata XML** to [MobileXpense support team](http://www.mobilexpense.net/contact).</span></span>

> [!TIP]
> <span data-ttu-id="6d97f-169">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="6d97f-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="6d97f-170">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="6d97f-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="6d97f-171">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="6d97f-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6d97f-172">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="6d97f-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="6d97f-173">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6d97f-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="6d97f-175">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="6d97f-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6d97f-176">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6d97f-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mobilexpense-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6d97f-178">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="6d97f-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mobilexpense-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6d97f-180">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="6d97f-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mobilexpense-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6d97f-182">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="6d97f-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-mobilexpense-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6d97f-184">а.</span><span class="sxs-lookup"><span data-stu-id="6d97f-184">a.</span></span> <span data-ttu-id="6d97f-185">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6d97f-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6d97f-186">b.</span><span class="sxs-lookup"><span data-stu-id="6d97f-186">b.</span></span> <span data-ttu-id="6d97f-187">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="6d97f-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6d97f-188">c.</span><span class="sxs-lookup"><span data-stu-id="6d97f-188">c.</span></span> <span data-ttu-id="6d97f-189">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="6d97f-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="6d97f-190">d.</span><span class="sxs-lookup"><span data-stu-id="6d97f-190">d.</span></span> <span data-ttu-id="6d97f-191">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="6d97f-191">Click **Create**.</span></span>
 
### <a name="creating-a-mobilexpense-test-user"></a><span data-ttu-id="6d97f-192">Создание тестового пользователя MobileXpense</span><span class="sxs-lookup"><span data-stu-id="6d97f-192">Creating a MobileXpense test user</span></span>

<span data-ttu-id="6d97f-193">В этом разделе описано, как создать пользователя Britta Simon в MobileXpense.</span><span class="sxs-lookup"><span data-stu-id="6d97f-193">In this section, you create a user called Britta Simon in MobileXpense.</span></span> <span data-ttu-id="6d97f-194">Чтобы добавить пользователей в MobileXpense, обратитесь в [службу поддержки клиентов MobileXpense](http://www.mobilexpense.net/contact).</span><span class="sxs-lookup"><span data-stu-id="6d97f-194">work with [MobileXpense support team](http://www.mobilexpense.net/contact) to add the users in the MobileXpense platform.</span></span> <span data-ttu-id="6d97f-195">Перед использованием единого входа необходимо создать и активировать пользователей.</span><span class="sxs-lookup"><span data-stu-id="6d97f-195">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="6d97f-196">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="6d97f-196">Assigning the Azure AD test user</span></span>

<span data-ttu-id="6d97f-197">В этом разделе описано, как настроить единый вход Azure для пользователя Britta Simon, предоставив этому пользователю доступ к MobileXpense.</span><span class="sxs-lookup"><span data-stu-id="6d97f-197">In this section, you enable Britta Simon to use Azure single sign-on by granting access to MobileXpense.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="6d97f-199">**Чтобы назначить пользователя Britta Simon для приложения MobileXpense, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="6d97f-199">**To assign Britta Simon to MobileXpense, perform the following steps:**</span></span>

1. <span data-ttu-id="6d97f-200">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="6d97f-200">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="6d97f-202">В списке приложений выберите **MobileXpense**.</span><span class="sxs-lookup"><span data-stu-id="6d97f-202">In the applications list, select **MobileXpense**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-mobilexpense-tutorial/tutorial_mobilexpense_app.png) 

3. <span data-ttu-id="6d97f-204">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="6d97f-204">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="6d97f-206">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="6d97f-206">Click **Add** button.</span></span> <span data-ttu-id="6d97f-207">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="6d97f-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="6d97f-209">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="6d97f-209">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="6d97f-210">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="6d97f-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6d97f-211">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="6d97f-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6d97f-212">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="6d97f-212">Testing single sign-on</span></span>

<span data-ttu-id="6d97f-213">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="6d97f-213">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="6d97f-214">Щелкнув элемент MobileXpense на панели доступа, вы автоматически войдете в приложение MobileXpense.</span><span class="sxs-lookup"><span data-stu-id="6d97f-214">When you click the MobileXpense tile in the Access Panel, you should get automatically signed-on to your MobileXpense application.</span></span>
<span data-ttu-id="6d97f-215">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="6d97f-215">For more information about the Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="6d97f-216">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="6d97f-216">Additional resources</span></span>

* [<span data-ttu-id="6d97f-217">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6d97f-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6d97f-218">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6d97f-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-mobilexpense-tutorial/tutorial_general_203.png

