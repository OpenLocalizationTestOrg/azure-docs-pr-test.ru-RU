---
title: "Учебник. Интеграция Azure Active Directory с Directions on Microsoft | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory с Directions on Microsoft."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e0c8986f-2acd-418d-a306-437abc44b640
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: f9c068c71eb00a4c779c91c8ee0f0dc9d6ba85ae
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-directions-on-microsoft"></a><span data-ttu-id="982a0-103">Руководство. Интеграция Azure Active Directory с Directions on Microsoft</span><span class="sxs-lookup"><span data-stu-id="982a0-103">Tutorial: Azure Active Directory integration with Directions on Microsoft</span></span>

<span data-ttu-id="982a0-104">В этом руководстве описано, как интегрировать Directions on Microsoft с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="982a0-104">In this tutorial, you learn how to integrate Directions on Microsoft with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="982a0-105">Интеграция Azure AD с Directions on Microsoft обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="982a0-105">Integrating Directions on Microsoft with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="982a0-106">С помощью Azure AD вы можете контролировать доступ к Directions on Microsoft.</span><span class="sxs-lookup"><span data-stu-id="982a0-106">You can control in Azure AD who has access to Directions on Microsoft</span></span>
- <span data-ttu-id="982a0-107">Вы можете включить автоматический вход пользователей в Directions on Microsoft (единый вход) с использованием учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="982a0-107">You can enable your users to automatically get signed-on to Directions on Microsoft (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="982a0-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="982a0-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="982a0-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="982a0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="982a0-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="982a0-110">Prerequisites</span></span>

<span data-ttu-id="982a0-111">Чтобы настроить интеграцию Azure AD с Directions on Microsoft, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="982a0-111">To configure Azure AD integration with Directions on Microsoft, you need the following items:</span></span>

- <span data-ttu-id="982a0-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="982a0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="982a0-113">подписка Directions on Microsoft с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="982a0-113">A Directions on Microsoft single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="982a0-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="982a0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="982a0-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="982a0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="982a0-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="982a0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="982a0-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="982a0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="982a0-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="982a0-118">Scenario description</span></span>
<span data-ttu-id="982a0-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="982a0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="982a0-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="982a0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="982a0-121">Добавление Directions on Microsoft из коллекции</span><span class="sxs-lookup"><span data-stu-id="982a0-121">Adding Directions on Microsoft from the gallery</span></span>
2. <span data-ttu-id="982a0-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="982a0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-directions-on-microsoft-from-the-gallery"></a><span data-ttu-id="982a0-123">Добавление Directions on Microsoft из коллекции</span><span class="sxs-lookup"><span data-stu-id="982a0-123">Adding Directions on Microsoft from the gallery</span></span>
<span data-ttu-id="982a0-124">Чтобы настроить интеграцию Directions on Microsoft с Azure AD, необходимо добавить Directions on Microsoft из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="982a0-124">To configure the integration of Directions on Microsoft into Azure AD, you need to add Directions on Microsoft from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="982a0-125">**Чтобы добавить Directions on Microsoft из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="982a0-125">**To add Directions on Microsoft from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="982a0-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="982a0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="982a0-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="982a0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="982a0-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="982a0-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="982a0-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="982a0-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="982a0-133">В поле поиска введите **Directions on Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="982a0-133">In the search box, type **Directions on Microsoft**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_search.png)

5. <span data-ttu-id="982a0-135">В области результатов выберите **Directions on Microsoft** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="982a0-135">In the results panel, select **Directions on Microsoft**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="982a0-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="982a0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="982a0-138">В этом разделе описывается настройка и проверка единого входа Azure AD в Directions on Microsoft с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="982a0-138">In this section, you configure and test Azure AD single sign-on with Directions on Microsoft based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="982a0-139">Чтобы единый вход работал, Azure AD необходимо знать, какой пользователь в Directions on Microsoft соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="982a0-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Directions on Microsoft is to a user in Azure AD.</span></span> <span data-ttu-id="982a0-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Directions on Microsoft.</span><span class="sxs-lookup"><span data-stu-id="982a0-140">In other words, a link relationship between an Azure AD user and the related user in Directions on Microsoft needs to be established.</span></span>

<span data-ttu-id="982a0-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Directions on Microsoft.</span><span class="sxs-lookup"><span data-stu-id="982a0-141">In Directions on Microsoft, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="982a0-142">Чтобы настроить и проверить единый вход Microsoft Azure AD в Directions on Microsoft, выполните следующие стандартные действия.</span><span class="sxs-lookup"><span data-stu-id="982a0-142">To configure and test Azure AD single sign-on with Directions on Microsoft, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="982a0-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="982a0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="982a0-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="982a0-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="982a0-145">**[Создание тестового пользователя Directions on Microsoft](#creating-a-directions-on-microsoft-test-user)** требуется для создания в Directions on Microsoft пользователя Britta Simon, связанного с представлением этого же пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="982a0-145">**[Creating a Directions on Microsoft test user](#creating-a-directions-on-microsoft-test-user)** - to have a counterpart of Britta Simon in Directions on Microsoft that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="982a0-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="982a0-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="982a0-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="982a0-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="982a0-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="982a0-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="982a0-149">В данном разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Directions on Microsoft.</span><span class="sxs-lookup"><span data-stu-id="982a0-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Directions on Microsoft application.</span></span>

<span data-ttu-id="982a0-150">**Чтобы настроить единый вход Azure AD в Directions on Microsoft, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="982a0-150">**To configure Azure AD single sign-on with Directions on Microsoft, perform the following steps:**</span></span>

1. <span data-ttu-id="982a0-151">На портале Azure на странице интеграции с приложением **Directions on Microsoft** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="982a0-151">In the Azure portal, on the **Directions on Microsoft** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="982a0-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="982a0-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_samlbase.png)

3. <span data-ttu-id="982a0-155">В разделе **Домены и URL-адреса приложения Directions on Microsoft** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="982a0-155">On the **Directions on Microsoft Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_url.png)

    <span data-ttu-id="982a0-157">а.</span><span class="sxs-lookup"><span data-stu-id="982a0-157">a.</span></span> <span data-ttu-id="982a0-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="982a0-158">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span>
    |  |
    | --- |
    | `https://www.directionsonmicrosoft.com/user/login` |
    | `https://<subdomain>.devcloud.acquia-sites.com/<companyname>` |

    <span data-ttu-id="982a0-159">b.</span><span class="sxs-lookup"><span data-stu-id="982a0-159">b.</span></span> <span data-ttu-id="982a0-160">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="982a0-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    |  |
    | --- |
    | `https://rhelmdirectionsonmicrosoftcomtest.devcloud.acquia-sites.com/simplesaml/<companyname>` |
    | `https://www.directionsonmicrosoft.com/simplesaml/<companyname>` |

    > [!NOTE] 
    > <span data-ttu-id="982a0-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="982a0-161">These values are not real.</span></span> <span data-ttu-id="982a0-162">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="982a0-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="982a0-163">Чтобы получить эти значения, обратитесь в [службу поддержки клиентов Directions on Microsoft](mailto:service@DirectionsOnMicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="982a0-163">Contact [Directions on Microsoft Client support team](mailto:service@DirectionsOnMicrosoft.com) to get these values.</span></span> 
 
4. <span data-ttu-id="982a0-164">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="982a0-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_certificate.png) 

5. <span data-ttu-id="982a0-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="982a0-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="982a0-168">Чтобы настроить единый вход на стороне **Directions on Microsoft**, отправьте в [службу поддержки Directions on Microsoft](mailto:service@DirectionsOnMicrosoft.com) скачанный **XML-файл метаданных**.</span><span class="sxs-lookup"><span data-stu-id="982a0-168">To configure single sign-on on **Directions on Microsoft** side, you need to send the downloaded **Metadata XML** to [Directions on Microsoft support team](mailto:service@DirectionsOnMicrosoft.com).</span></span> <span data-ttu-id="982a0-169">Чтобы позволить службе поддержки Directions on Microsoft найти ваше членство федеративного веб-сайта, включите в сообщение электронной почты сведения о своей организации.</span><span class="sxs-lookup"><span data-stu-id="982a0-169">To enable the Directions on Microsoft support team to locate your federated site membership, include your company information in your email.</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="982a0-170">Единый вход Directions on Microsoft должна включить [служба поддержки клиентов Directions on Microsoft](mailto:service@DirectionsOnMicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="982a0-170">Single sign-on for Directions on Microsoft needs to be enabled by the [Directions on Microsoft Client support team](mailto:service@DirectionsOnMicrosoft.com).</span></span> <span data-ttu-id="982a0-171">Вы получите уведомление, когда такой единый вход будет включен.</span><span class="sxs-lookup"><span data-stu-id="982a0-171">You will receive a notification when single sign-on has been enabled.</span></span>

> [!TIP]
> <span data-ttu-id="982a0-172">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="982a0-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="982a0-173">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="982a0-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="982a0-174">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="982a0-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="982a0-175">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="982a0-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="982a0-176">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="982a0-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="982a0-178">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="982a0-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="982a0-179">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="982a0-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-directions-microsoft-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="982a0-181">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="982a0-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-directions-microsoft-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="982a0-183">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="982a0-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-directions-microsoft-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="982a0-185">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="982a0-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-directions-microsoft-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="982a0-187">а.</span><span class="sxs-lookup"><span data-stu-id="982a0-187">a.</span></span> <span data-ttu-id="982a0-188">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="982a0-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="982a0-189">b.</span><span class="sxs-lookup"><span data-stu-id="982a0-189">b.</span></span> <span data-ttu-id="982a0-190">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="982a0-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="982a0-191">c.</span><span class="sxs-lookup"><span data-stu-id="982a0-191">c.</span></span> <span data-ttu-id="982a0-192">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="982a0-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="982a0-193">d.</span><span class="sxs-lookup"><span data-stu-id="982a0-193">d.</span></span> <span data-ttu-id="982a0-194">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="982a0-194">Click **Create**.</span></span>
 
### <a name="creating-a-directions-on-microsoft-test-user"></a><span data-ttu-id="982a0-195">Создание тестового пользователя Directions on Microsoft</span><span class="sxs-lookup"><span data-stu-id="982a0-195">Creating a Directions on Microsoft test user</span></span>

<span data-ttu-id="982a0-196">Элемент действия для настройки подготовки пользователей в Directions on Microsoft отсутствует.</span><span class="sxs-lookup"><span data-stu-id="982a0-196">There is no action item for you to configure user provisioning to Directions on Microsoft.</span></span>  

<span data-ttu-id="982a0-197">Когда назначенный пользователь пытается войти в Directions on Microsoft с помощью панели доступа, Directions on Microsoft проверяет, существует ли данный пользователь.</span><span class="sxs-lookup"><span data-stu-id="982a0-197">When an assigned user tries to log in to Directions on Microsoft using the access panel, Directions on Microsoft checks whether the user exists.</span></span> <span data-ttu-id="982a0-198">Если учетная запись пользователя отсутствует, Directions on Microsoft автоматически создает ее.</span><span class="sxs-lookup"><span data-stu-id="982a0-198">If there is no user account available yet, it is automatically created by Directions on Microsoft.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="982a0-199">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="982a0-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="982a0-200">В этом разделе описано, как позволить пользователю Britta Simon использовать единый вход Azure, предоставив ему доступ к Directions on Microsoft.</span><span class="sxs-lookup"><span data-stu-id="982a0-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Directions on Microsoft.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="982a0-202">**Чтобы назначить пользователя Britta Simon в Directions on Microsoft, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="982a0-202">**To assign Britta Simon to Directions on Microsoft, perform the following steps:**</span></span>

1. <span data-ttu-id="982a0-203">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="982a0-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="982a0-205">В списке приложений выберите **Directions on Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="982a0-205">In the applications list, select **Directions on Microsoft**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-directions-microsoft-tutorial/tutorial_directionsonmicrosoft_app.png) 

3. <span data-ttu-id="982a0-207">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="982a0-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="982a0-209">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="982a0-209">Click **Add** button.</span></span> <span data-ttu-id="982a0-210">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="982a0-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="982a0-212">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="982a0-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="982a0-213">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="982a0-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="982a0-214">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="982a0-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="982a0-215">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="982a0-215">Testing single sign-on</span></span>

<span data-ttu-id="982a0-216">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="982a0-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>
 
<span data-ttu-id="982a0-217">Щелкнув элемент Directions on Microsoft на панели доступа, вы автоматически войдете в приложение Directions on Microsoft.</span><span class="sxs-lookup"><span data-stu-id="982a0-217">When you click the Directions on Microsoft tile in the Access Panel, you should get automatically signed-on to your Directions on Microsoft application.</span></span>

<span data-ttu-id="982a0-218">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="982a0-218">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="982a0-219">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="982a0-219">Additional resources</span></span>

* [<span data-ttu-id="982a0-220">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="982a0-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="982a0-221">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="982a0-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-directions-microsoft-tutorial/tutorial_general_203.png

