---
title: "Руководство по интеграции Azure Active Directory с BC in the Cloud | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в BC in the Cloud."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 7dc40d2c-6349-40cb-b304-b098bd03a66c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/1/2017
ms.author: jeedes
ms.openlocfilehash: ebc95d600eca1027331cd92cfe481d0c3ee833a5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bc-in-the-cloud"></a><span data-ttu-id="dcd83-103">Руководство по интеграции Azure Active Directory с BC in the Cloud</span><span class="sxs-lookup"><span data-stu-id="dcd83-103">Tutorial: Azure Active Directory integration with BC in the Cloud</span></span>

<span data-ttu-id="dcd83-104">В этом руководстве описано, как интегрировать BC in the Cloud с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="dcd83-104">In this tutorial, you learn how to integrate BC in the Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="dcd83-105">Интеграция Azure AD с BC in the Cloud обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="dcd83-105">Integrating BC in the Cloud with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="dcd83-106">С помощью Azure AD вы можете контролировать доступ к BC in the Cloud.</span><span class="sxs-lookup"><span data-stu-id="dcd83-106">You can control in Azure AD who has access to BC in the Cloud</span></span>
- <span data-ttu-id="dcd83-107">Вы можете включить автоматический вход пользователей в BC in the Cloud (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dcd83-107">You can enable your users to automatically get signed-on to BC in the Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="dcd83-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="dcd83-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="dcd83-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="dcd83-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dcd83-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="dcd83-110">Prerequisites</span></span>

<span data-ttu-id="dcd83-111">Чтобы настроить интеграцию Azure AD с приложением BC in the Cloud, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="dcd83-111">To configure Azure AD integration with BC in the Cloud, you need the following items:</span></span>

- <span data-ttu-id="dcd83-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="dcd83-112">An Azure AD subscription</span></span>
- <span data-ttu-id="dcd83-113">подписка BC in the Cloud с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="dcd83-113">A BC in the Cloud single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="dcd83-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="dcd83-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="dcd83-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="dcd83-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="dcd83-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="dcd83-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="dcd83-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="dcd83-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="dcd83-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="dcd83-118">Scenario description</span></span>
<span data-ttu-id="dcd83-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="dcd83-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="dcd83-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="dcd83-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="dcd83-121">Добавление BC in the Cloud из коллекции</span><span class="sxs-lookup"><span data-stu-id="dcd83-121">Adding BC in the Cloud from the gallery</span></span>
2. <span data-ttu-id="dcd83-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="dcd83-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bc-in-the-cloud-from-the-gallery"></a><span data-ttu-id="dcd83-123">Добавление BC in the Cloud из коллекции</span><span class="sxs-lookup"><span data-stu-id="dcd83-123">Adding BC in the Cloud from the gallery</span></span>
<span data-ttu-id="dcd83-124">Чтобы настроить интеграцию BC in the Cloud с Azure AD, необходимо добавить BC in the Cloud из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="dcd83-124">To configure the integration of BC in the Cloud into Azure AD, you need to add BC in the Cloud from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="dcd83-125">**Чтобы добавить BC in the Cloud из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="dcd83-125">**To add BC in the Cloud from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="dcd83-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="dcd83-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="dcd83-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="dcd83-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="dcd83-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="dcd83-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="dcd83-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="dcd83-131">To add new application, click **Add** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="dcd83-133">В поле поиска введите **BC in the Cloud**.</span><span class="sxs-lookup"><span data-stu-id="dcd83-133">In the search box, type **BC in the Cloud**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_search.png)

5. <span data-ttu-id="dcd83-135">На панели результатов выберите **BC in the Cloud** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="dcd83-135">In the results panel, select **BC in the Cloud**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="dcd83-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="dcd83-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="dcd83-138">В этом разделе описана настройка и проверка единого входа Azure AD в BC in the Cloud с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dcd83-138">In this section, you configure and test Azure AD single sign-on with BC in the Cloud based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="dcd83-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в BC in the Cloud соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dcd83-139">For single sign-on to work, Azure AD needs to know what the counterpart user in BC in the Cloud is to a user in Azure AD.</span></span> <span data-ttu-id="dcd83-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в BC in the Cloud.</span><span class="sxs-lookup"><span data-stu-id="dcd83-140">In other words, a link relationship between an Azure AD user and the related user in BC in the Cloud needs to be established.</span></span>

<span data-ttu-id="dcd83-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в BC in the Cloud.</span><span class="sxs-lookup"><span data-stu-id="dcd83-141">In BC in the Cloud, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="dcd83-142">Чтобы настроить и проверить единый вход Azure AD в BC in the Cloud, выполните действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="dcd83-142">To configure and test Azure AD single sign-on with BC in the Cloud, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="dcd83-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="dcd83-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="dcd83-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dcd83-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="dcd83-145">**[Создание тестового пользователя BC in the Cloud](#creating-a-bc-in-the-cloud-test-user)** нужно для того, чтобы в BC in the Cloud также существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dcd83-145">**[Creating a BC in the Cloud test user](#creating-a-bc-in-the-cloud-test-user)** - to have a counterpart of Britta Simon in BC in the Cloud that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="dcd83-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dcd83-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="dcd83-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="dcd83-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="dcd83-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="dcd83-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="dcd83-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении BC in the Cloud.</span><span class="sxs-lookup"><span data-stu-id="dcd83-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your BC in the Cloud application.</span></span>

<span data-ttu-id="dcd83-150">**Чтобы настроить единый вход Azure AD в BC in the Cloud, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="dcd83-150">**To configure Azure AD single sign-on with BC in the Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="dcd83-151">На портале Azure на странице интеграции с приложением **BC in the Cloud** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="dcd83-151">In the Azure portal, on the **BC in the Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="dcd83-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="dcd83-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_samlbase.png)

3. <span data-ttu-id="dcd83-155">В разделе **Домены и URL-адреса приложения BC in the Cloud** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="dcd83-155">On the **BC in the Cloud Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_url.png)

    <span data-ttu-id="dcd83-157">а.</span><span class="sxs-lookup"><span data-stu-id="dcd83-157">a.</span></span> <span data-ttu-id="dcd83-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://app.bcinthecloud.com/router/loginSaml/<customerid>`</span><span class="sxs-lookup"><span data-stu-id="dcd83-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://app.bcinthecloud.com/router/loginSaml/<customerid>`</span></span>

    <span data-ttu-id="dcd83-159">b.</span><span class="sxs-lookup"><span data-stu-id="dcd83-159">b.</span></span> <span data-ttu-id="dcd83-160">В текстовом поле **Идентификатор** введите URL-адрес в формате `https://app.bcinthecloud.com`.</span><span class="sxs-lookup"><span data-stu-id="dcd83-160">In the **Identifier** textbox, type a URL as: `https://app.bcinthecloud.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="dcd83-161">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="dcd83-161">This value is not real.</span></span> <span data-ttu-id="dcd83-162">Вместо него необходимо указать фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="dcd83-162">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="dcd83-163">Для получения этого значения обратитесь к [группе поддержки BC in the Cloud](https://www.bcinthecloud.com/supportcenter/).</span><span class="sxs-lookup"><span data-stu-id="dcd83-163">Contact [BC in the Cloud Client support team](https://www.bcinthecloud.com/supportcenter/) to get this value.</span></span> 
 
4. <span data-ttu-id="dcd83-164">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="dcd83-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_certificate.png) 

5. <span data-ttu-id="dcd83-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="dcd83-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="dcd83-168">Чтобы настроить единый вход на стороне **BC in the Cloud**, отправьте скачанный **XML-файл метаданных** [группе поддержки BC in the Cloud](https://www.bcinthecloud.com/supportcenter/).</span><span class="sxs-lookup"><span data-stu-id="dcd83-168">To configure single sign-on on **BC in the Cloud** side, you need to send the downloaded **Metadata XML** to [BC in the Cloud support team](https://www.bcinthecloud.com/supportcenter/).</span></span>

> [!TIP]
> <span data-ttu-id="dcd83-169">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="dcd83-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="dcd83-170">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="dcd83-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="dcd83-171">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="dcd83-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="dcd83-172">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="dcd83-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="dcd83-173">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dcd83-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="dcd83-175">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="dcd83-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="dcd83-176">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="dcd83-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bcinthecloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="dcd83-178">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="dcd83-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bcinthecloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="dcd83-180">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="dcd83-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bcinthecloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="dcd83-182">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="dcd83-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bcinthecloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="dcd83-184">а.</span><span class="sxs-lookup"><span data-stu-id="dcd83-184">a.</span></span> <span data-ttu-id="dcd83-185">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="dcd83-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="dcd83-186">b.</span><span class="sxs-lookup"><span data-stu-id="dcd83-186">b.</span></span> <span data-ttu-id="dcd83-187">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="dcd83-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="dcd83-188">c.</span><span class="sxs-lookup"><span data-stu-id="dcd83-188">c.</span></span> <span data-ttu-id="dcd83-189">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="dcd83-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="dcd83-190">d.</span><span class="sxs-lookup"><span data-stu-id="dcd83-190">d.</span></span> <span data-ttu-id="dcd83-191">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="dcd83-191">Click **Create**.</span></span>
 
### <a name="creating-a-bc-in-the-cloud-test-user"></a><span data-ttu-id="dcd83-192">Создание тестового пользователя BC in the Cloud</span><span class="sxs-lookup"><span data-stu-id="dcd83-192">Creating a BC in the Cloud test user</span></span>

<span data-ttu-id="dcd83-193">В этом разделе описано, как создать пользователя Britta Simon в приложении BC in the Cloud.</span><span class="sxs-lookup"><span data-stu-id="dcd83-193">In this section, you create a user called Britta Simon in BC in the Cloud.</span></span> <span data-ttu-id="dcd83-194">Обратитесь к [группе поддержки BC in the Cloud](https://www.bcinthecloud.com/supportcenter/) для добавления пользователей в приложение BC in the Cloud.</span><span class="sxs-lookup"><span data-stu-id="dcd83-194">Work with [BC in the Cloud Client support team](https://www.bcinthecloud.com/supportcenter/) to add the users in the BC in the Cloud application.</span></span> <span data-ttu-id="dcd83-195">Перед использованием единого входа необходимо создать и активировать пользователей.</span><span class="sxs-lookup"><span data-stu-id="dcd83-195">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="dcd83-196">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="dcd83-196">Assigning the Azure AD test user</span></span>

<span data-ttu-id="dcd83-197">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к BC in the Cloud.</span><span class="sxs-lookup"><span data-stu-id="dcd83-197">In this section, you enable Britta Simon to use Azure single sign-on by granting access to BC in the Cloud.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="dcd83-199">**Чтобы назначить пользователя Britta Simon в BC in the Cloud, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="dcd83-199">**To assign Britta Simon to BC in the Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="dcd83-200">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="dcd83-200">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="dcd83-202">В списке приложений выберите **BC in the Cloud**.</span><span class="sxs-lookup"><span data-stu-id="dcd83-202">In the applications list, select **BC in the Cloud**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-bcinthecloud-tutorial/tutorial_bcinthecloud_app.png) 

3. <span data-ttu-id="dcd83-204">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="dcd83-204">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="dcd83-206">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="dcd83-206">Click **Add** button.</span></span> <span data-ttu-id="dcd83-207">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="dcd83-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="dcd83-209">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="dcd83-209">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="dcd83-210">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="dcd83-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="dcd83-211">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="dcd83-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="dcd83-212">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="dcd83-212">Testing single sign-on</span></span>

<span data-ttu-id="dcd83-213">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="dcd83-213">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

 <span data-ttu-id="dcd83-214">Щелкнув элемент "BC in the Cloud" на панели доступа, вы автоматически войдете в приложение BC in the Cloud.</span><span class="sxs-lookup"><span data-stu-id="dcd83-214">When you click the BC in the Cloud tile in the Access Panel, you should get automatically signed-on to your BC in the Cloud application.</span></span> <span data-ttu-id="dcd83-215">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="dcd83-215">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="dcd83-216">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="dcd83-216">Additional resources</span></span>

* [<span data-ttu-id="dcd83-217">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dcd83-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="dcd83-218">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="dcd83-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bcinthecloud-tutorial/tutorial_general_203.png

