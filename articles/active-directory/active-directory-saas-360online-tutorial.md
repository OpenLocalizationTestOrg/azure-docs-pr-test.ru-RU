---
title: "Руководство по интеграции Azure Active Directory с 360 Online | Документация Майкрософт"
description: "Сведения о настройке единого входа между Azure Active Directory и 360 Online."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: cda8eba6-843f-4a09-8c55-0aaf6e593d75
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: 629c7db04b0f9c880da6dfa8eac7fe14ecd8a215
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-360-online"></a><span data-ttu-id="8ec91-103">Руководство по интеграции Azure Active Directory с 360 Online</span><span class="sxs-lookup"><span data-stu-id="8ec91-103">Tutorial: Azure Active Directory integration with 360 Online</span></span>

<span data-ttu-id="8ec91-104">В этом руководстве объясняется, как интегрировать приложение 360 Online со службой Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8ec91-104">In this tutorial, you learn how to integrate 360 Online with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8ec91-105">Интеграция 360 Online с Azure AD обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="8ec91-105">Integrating 360 Online with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8ec91-106">С помощью Azure AD вы можете контролировать, у кого есть доступ к приложению 360 Online.</span><span class="sxs-lookup"><span data-stu-id="8ec91-106">You can control in Azure AD who has access to 360 Online</span></span>
- <span data-ttu-id="8ec91-107">Вы можете включить автоматический вход пользователей в 360 Online (единый вход) под учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8ec91-107">You can enable your users to automatically get signed-on to 360 Online (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8ec91-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="8ec91-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="8ec91-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8ec91-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8ec91-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="8ec91-110">Prerequisites</span></span>

<span data-ttu-id="8ec91-111">Чтобы настроить интеграцию Azure AD с 360 Online, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="8ec91-111">To configure Azure AD integration with 360 Online, you need the following items:</span></span>

- <span data-ttu-id="8ec91-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="8ec91-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8ec91-113">подписка 360 Online с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="8ec91-113">A 360 Online single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8ec91-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="8ec91-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8ec91-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="8ec91-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8ec91-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="8ec91-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8ec91-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8ec91-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8ec91-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="8ec91-118">Scenario description</span></span>
<span data-ttu-id="8ec91-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="8ec91-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8ec91-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="8ec91-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8ec91-121">Добавление 360 Online из коллекции.</span><span class="sxs-lookup"><span data-stu-id="8ec91-121">Adding 360 Online from the gallery</span></span>
2. <span data-ttu-id="8ec91-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ec91-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-360-online-from-the-gallery"></a><span data-ttu-id="8ec91-123">Добавление 360 Online из коллекции</span><span class="sxs-lookup"><span data-stu-id="8ec91-123">Adding 360 Online from the gallery</span></span>
<span data-ttu-id="8ec91-124">Чтобы настроить интеграцию приложения 360 Online с Azure AD, вам нужно добавить это приложение из коллекции в свой список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="8ec91-124">To configure the integration of 360 Online into Azure AD, you need to add 360 Online from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8ec91-125">**Добавление приложения 360 Online из коллекции**</span><span class="sxs-lookup"><span data-stu-id="8ec91-125">**To add 360 Online from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8ec91-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8ec91-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8ec91-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="8ec91-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8ec91-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="8ec91-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="8ec91-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="8ec91-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="8ec91-133">В поле поиска введите **360 Online**.</span><span class="sxs-lookup"><span data-stu-id="8ec91-133">In the search box, type **360 Online**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-360online-tutorial/tutorial_360online_search.png)

5. <span data-ttu-id="8ec91-135">В области результатов выберите **360 Online** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="8ec91-135">In the results panel, select **360 Online**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-360online-tutorial/tutorial_360online_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8ec91-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ec91-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8ec91-138">В этом разделе мы настроим и проверим единый вход Azure AD в приложении 360 Online с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8ec91-138">In this section, you configure and test Azure AD single sign-on with 360 Online based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8ec91-139">Для работы единого входа службе Azure AD нужно знать, какой пользователь в 360 Online соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8ec91-139">For single sign-on to work, Azure AD needs to know what the counterpart user in 360 Online is to a user in Azure AD.</span></span> <span data-ttu-id="8ec91-140">Иными словами, нужно установить связь между пользователем Azure AD и соответствующим пользователем в360 Online.</span><span class="sxs-lookup"><span data-stu-id="8ec91-140">In other words, a link relationship between an Azure AD user and the related user in 360 Online needs to be established.</span></span>

<span data-ttu-id="8ec91-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в 360 Online.</span><span class="sxs-lookup"><span data-stu-id="8ec91-141">In 360 Online, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="8ec91-142">Чтобы настроить и проверить единый вход Azure AD в 360 Online, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="8ec91-142">To configure and test Azure AD single sign-on with 360 Online, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8ec91-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="8ec91-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8ec91-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8ec91-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8ec91-145">**[Создание тестового пользователя 360 Online](#creating-a-360-online-test-user)** требуется для создания пользователя Britta Simon в 360 Online, связанного с представлением этого же пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8ec91-145">**[Creating a 360 Online test user](#creating-a-360-online-test-user)** - to have a counterpart of Britta Simon in 360 Online that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="8ec91-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8ec91-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8ec91-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="8ec91-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8ec91-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ec91-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8ec91-149">В этом разделе мы включим на портале Azure единый вход Azure AD и настроим его в приложении 360 Online.</span><span class="sxs-lookup"><span data-stu-id="8ec91-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your 360 Online application.</span></span>

<span data-ttu-id="8ec91-150">**Настройка единого входа Azure AD в 360 Online**</span><span class="sxs-lookup"><span data-stu-id="8ec91-150">**To configure Azure AD single sign-on with 360 Online, perform the following steps:**</span></span>

1. <span data-ttu-id="8ec91-151">На портале Azure на странице интеграции с приложением **360 Online** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="8ec91-151">In the Azure portal, on the **360 Online** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="8ec91-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="8ec91-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-360online-tutorial/tutorial_360online_samlbase.png)

3. <span data-ttu-id="8ec91-155">В разделе **Домены и URL-адреса приложения 360 Online** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="8ec91-155">On the **360 Online Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-360online-tutorial/tutorial_360online_url.png)

    <span data-ttu-id="8ec91-157">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<company name>.public360online.com`</span><span class="sxs-lookup"><span data-stu-id="8ec91-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.public360online.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8ec91-158">Это значение приведено для примера.</span><span class="sxs-lookup"><span data-stu-id="8ec91-158">The value is not real.</span></span> <span data-ttu-id="8ec91-159">Вместо него необходимо указать фактический URL-адрес для входа.</span><span class="sxs-lookup"><span data-stu-id="8ec91-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="8ec91-160">Чтобы получить это значение, обратитесь в [службу поддержки клиентов 360 Online](mailto:360online@software-innovation.com).</span><span class="sxs-lookup"><span data-stu-id="8ec91-160">Contact [360 Online Client support team](mailto:360online@software-innovation.com) to get the value.</span></span> 
 
4. <span data-ttu-id="8ec91-161">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="8ec91-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-360online-tutorial/tutorial_360online_certificate.png) 

5. <span data-ttu-id="8ec91-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="8ec91-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-360online-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8ec91-165">Чтобы настроить единый вход на стороне **360 Online**, отправьте в [службу поддержки 360 Online](mailto:360online@software-innovation.com) скачанный **XML-файл метаданных**.</span><span class="sxs-lookup"><span data-stu-id="8ec91-165">To configure single sign-on on **360 Online** side, you need to send the downloaded **Metadata XML** to [360 Online support team](mailto:360online@software-innovation.com).</span></span> 

> [!TIP]
> <span data-ttu-id="8ec91-166">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="8ec91-166">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="8ec91-167">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="8ec91-167">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="8ec91-168">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="8ec91-168">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8ec91-169">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ec91-169">Creating an Azure AD test user</span></span>
<span data-ttu-id="8ec91-170">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8ec91-170">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="8ec91-172">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="8ec91-172">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8ec91-173">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8ec91-173">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-360online-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8ec91-175">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="8ec91-175">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-360online-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8ec91-177">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="8ec91-177">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-360online-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8ec91-179">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="8ec91-179">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-360online-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8ec91-181">а.</span><span class="sxs-lookup"><span data-stu-id="8ec91-181">a.</span></span> <span data-ttu-id="8ec91-182">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8ec91-182">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8ec91-183">b.</span><span class="sxs-lookup"><span data-stu-id="8ec91-183">b.</span></span> <span data-ttu-id="8ec91-184">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8ec91-184">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8ec91-185">c.</span><span class="sxs-lookup"><span data-stu-id="8ec91-185">c.</span></span> <span data-ttu-id="8ec91-186">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="8ec91-186">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="8ec91-187">d.</span><span class="sxs-lookup"><span data-stu-id="8ec91-187">d.</span></span> <span data-ttu-id="8ec91-188">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="8ec91-188">Click **Create**.</span></span>
 
### <a name="creating-a-360-online-test-user"></a><span data-ttu-id="8ec91-189">Создание тестового пользователя 360 Online</span><span class="sxs-lookup"><span data-stu-id="8ec91-189">Creating a 360 Online test user</span></span>

<span data-ttu-id="8ec91-190">В этом разделе мы создадим пользователя Britta Simon в приложении 360 Online.</span><span class="sxs-lookup"><span data-stu-id="8ec91-190">In this section, you create a user called Britta Simon in 360 Online.</span></span> <span data-ttu-id="8ec91-191">Чтобы создать пользователя, необходимо обратиться в [службу поддержки 360 Online](mailto:360online@software-innovation.com).</span><span class="sxs-lookup"><span data-stu-id="8ec91-191">you need to contact [360 Online support team](mailto:360online@software-innovation.com).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="8ec91-192">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="8ec91-192">Assigning the Azure AD test user</span></span>

<span data-ttu-id="8ec91-193">В этом разделе мы разрешим пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к 360 Online.</span><span class="sxs-lookup"><span data-stu-id="8ec91-193">In this section, you enable Britta Simon to use Azure single sign-on by granting access to 360 Online.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="8ec91-195">**Назначение пользователя Britta Simon приложению 360 Online**</span><span class="sxs-lookup"><span data-stu-id="8ec91-195">**To assign Britta Simon to 360 Online, perform the following steps:**</span></span>

1. <span data-ttu-id="8ec91-196">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="8ec91-196">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="8ec91-198">В списке приложений выберите **360 Online**.</span><span class="sxs-lookup"><span data-stu-id="8ec91-198">In the applications list, select **360 Online**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-360online-tutorial/tutorial_360online_app.png) 

3. <span data-ttu-id="8ec91-200">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="8ec91-200">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="8ec91-202">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="8ec91-202">Click **Add** button.</span></span> <span data-ttu-id="8ec91-203">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="8ec91-203">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="8ec91-205">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="8ec91-205">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="8ec91-206">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="8ec91-206">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8ec91-207">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="8ec91-207">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8ec91-208">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="8ec91-208">Testing single sign-on</span></span>

<span data-ttu-id="8ec91-209">Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="8ec91-209">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="8ec91-210">Щелкнув плитку 360 Online на панели доступа, вы автоматически войдете в приложение 360 Online.</span><span class="sxs-lookup"><span data-stu-id="8ec91-210">When you click the 360 Online tile in the Access Panel, you should get automatically signed-on to your 360 Online application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="8ec91-211">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="8ec91-211">Additional resources</span></span>

* [<span data-ttu-id="8ec91-212">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8ec91-212">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8ec91-213">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8ec91-213">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-360online-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-360online-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-360online-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-360online-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-360online-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-360online-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-360online-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-360online-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-360online-tutorial/tutorial_general_203.png

