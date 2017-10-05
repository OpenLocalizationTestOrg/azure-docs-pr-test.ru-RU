---
title: "Руководство по интеграции Azure Active Directory с платформой 23 Video | Документация Майкрософт"
description: "Узнайте, как настроить единый вход для Azure Active Directory и платформы 23 Video."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5e73dd1d-3995-4a73-b9cf-1b2318d49cb3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: jeedes
ms.openlocfilehash: ffcd665506c21e25c84367af5b6a3afb8e319af7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-23-video"></a><span data-ttu-id="00902-103">Руководство по интеграции Azure Active Directory с платформой 23 Video</span><span class="sxs-lookup"><span data-stu-id="00902-103">Tutorial: Azure Active Directory integration with 23 Video</span></span>

<span data-ttu-id="00902-104">В этом руководстве объясняется, как интегрировать приложение 23 Video с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="00902-104">In this tutorial, you learn how to integrate 23 Video with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="00902-105">Интеграция Azure AD с приложением 23 Video обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="00902-105">Integrating 23 Video with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="00902-106">С помощью Azure AD вы можете контролировать, у кого есть доступ к приложению 23 Video.</span><span class="sxs-lookup"><span data-stu-id="00902-106">You can control in Azure AD who has access to 23 Video</span></span>
- <span data-ttu-id="00902-107">Вы можете включить автоматический вход пользователей в 23 Video (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="00902-107">You can enable your users to automatically get signed-on to 23 Video (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="00902-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="00902-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="00902-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="00902-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="00902-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="00902-110">Prerequisites</span></span>

<span data-ttu-id="00902-111">Чтобы настроить интеграцию Azure AD с 23 Video, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="00902-111">To configure Azure AD integration with 23 Video, you need the following items:</span></span>

- <span data-ttu-id="00902-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="00902-112">An Azure AD subscription</span></span>
- <span data-ttu-id="00902-113">подписка на 23 Video с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="00902-113">A 23 Video single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="00902-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="00902-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="00902-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="00902-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="00902-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="00902-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="00902-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="00902-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="00902-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="00902-118">Scenario description</span></span>
<span data-ttu-id="00902-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="00902-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="00902-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="00902-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="00902-121">Добавление 23 Video из коллекции.</span><span class="sxs-lookup"><span data-stu-id="00902-121">Adding 23 Video from the gallery</span></span>
2. <span data-ttu-id="00902-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="00902-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-23-video-from-the-gallery"></a><span data-ttu-id="00902-123">Добавление 23 Video из коллекции.</span><span class="sxs-lookup"><span data-stu-id="00902-123">Adding 23 Video from the gallery</span></span>
<span data-ttu-id="00902-124">Чтобы настроить интеграцию приложения 23 Video с Azure AD, вам нужно добавить это приложение из коллекции в свой список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="00902-124">To configure the integration of 23 Video into Azure AD, you need to add 23 Video from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="00902-125">**Добавление приложения 23 Video из коллекции**</span><span class="sxs-lookup"><span data-stu-id="00902-125">**To add 23 Video from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="00902-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="00902-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="00902-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="00902-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="00902-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="00902-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="00902-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="00902-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="00902-133">В поле поиска введите **23 Video**.</span><span class="sxs-lookup"><span data-stu-id="00902-133">In the search box, type **23 Video**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-23video-tutorial/tutorial_23video_search.png)

5. <span data-ttu-id="00902-135">В области результатов выберите **23 Video** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="00902-135">In the results panel, select **23 Video**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-23video-tutorial/tutorial_23video_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="00902-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="00902-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="00902-138">В этом разделе мы настроим и проверим единый вход Azure AD в приложении 23 Video с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="00902-138">In this section, you configure and test Azure AD single sign-on with 23 Video based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="00902-139">Для работы единого входа службе Azure AD нужно знать, какой пользователь в 23 Video соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="00902-139">For single sign-on to work, Azure AD needs to know what the counterpart user in 23 Video is to a user in Azure AD.</span></span> <span data-ttu-id="00902-140">Иными словами, нужно установить связь между пользователем Azure AD и соответствующим пользователем в 23 Video.</span><span class="sxs-lookup"><span data-stu-id="00902-140">In other words, a link relationship between an Azure AD user and the related user in 23 Video needs to be established.</span></span>

<span data-ttu-id="00902-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в 23 Video.</span><span class="sxs-lookup"><span data-stu-id="00902-141">In 23 Video, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="00902-142">Чтобы настроить и проверить единый вход Azure AD в 23 Video, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="00902-142">To configure and test Azure AD single sign-on with 23 Video, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="00902-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы позволить пользователям использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="00902-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="00902-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="00902-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="00902-145">**[Создание тестового пользователя 23 Video](#creating-a-23-video-test-user)** требуется для создания в 23 Video пользователя Britta Simon, связанного с представлением этого же пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="00902-145">**[Creating a 23 Video test user](#creating-a-23-video-test-user)** - to have a counterpart of Britta Simon in 23 Video that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="00902-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="00902-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="00902-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="00902-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="00902-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="00902-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="00902-149">В этом разделе мы включим на портале Azure единый вход Azure AD и настроим его в приложении 23 Video.</span><span class="sxs-lookup"><span data-stu-id="00902-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your 23 Video application.</span></span>

<span data-ttu-id="00902-150">**Настройка единого входа Azure AD в 23 Video**</span><span class="sxs-lookup"><span data-stu-id="00902-150">**To configure Azure AD single sign-on with 23 Video, perform the following steps:**</span></span>

1. <span data-ttu-id="00902-151">На портале Azure на странице интеграции с приложением **23 Video** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="00902-151">In the Azure portal, on the **23 Video** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="00902-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="00902-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-23video-tutorial/tutorial_23video_samlbase.png)

3. <span data-ttu-id="00902-155">В разделе **Домены и URL-адреса приложения 23 Video** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="00902-155">On the **23 Video Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-23video-tutorial/tutorial_23video_url.png)

    <span data-ttu-id="00902-157">а.</span><span class="sxs-lookup"><span data-stu-id="00902-157">a.</span></span> <span data-ttu-id="00902-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<subdomain>.23video.com`</span><span class="sxs-lookup"><span data-stu-id="00902-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.23video.com`</span></span>

    <span data-ttu-id="00902-159">b.</span><span class="sxs-lookup"><span data-stu-id="00902-159">b.</span></span> <span data-ttu-id="00902-160">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://www.23video.com/saml/trust/<uniqueid>`</span><span class="sxs-lookup"><span data-stu-id="00902-160">In the **Identifier** textbox, type a URL using the following pattern: `https://www.23video.com/saml/trust/<uniqueid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="00902-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="00902-161">These values are not real.</span></span> <span data-ttu-id="00902-162">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="00902-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="00902-163">Чтобы получить эти значения, обратитесь в [службу поддержки клиентов 23 Video](mailto:support@23company.com).</span><span class="sxs-lookup"><span data-stu-id="00902-163">Contact [23 Video Client support team](mailto:support@23company.com) to get these values.</span></span> 
 
4. <span data-ttu-id="00902-164">В разделе **Сертификат для подписи токена SAML** щелкните **Certificate (Base64)** (Сертификат (Base64)), а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="00902-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-23video-tutorial/tutorial_23video_certificate.png) 

5. <span data-ttu-id="00902-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="00902-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-23video-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="00902-168">В разделе **Настройка 23 Video** щелкните **Настроить 23 Video**. Откроется окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="00902-168">On the **23 Video Configuration** section, click **Configure 23 Video** to open **Configure sign-on** window.</span></span> <span data-ttu-id="00902-169">Скопируйте **URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML**  из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="00902-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-23video-tutorial/tutorial_23video_configure.png) 

7. <span data-ttu-id="00902-171">Чтобы настроить единый вход на стороне **23 Video**, нужно отправить скачанный **сертификат (Base64)**, **URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML** в [службу поддержки 23 Video](mailto:support@23company.com).</span><span class="sxs-lookup"><span data-stu-id="00902-171">To configure single sign-on on **23 Video** side, you need to send the downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [23 Video support team](mailto:support@23company.com).</span></span> 


> [!TIP]
> <span data-ttu-id="00902-172">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="00902-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="00902-173">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="00902-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="00902-174">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="00902-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="00902-175">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="00902-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="00902-176">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="00902-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="00902-178">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="00902-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="00902-179">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="00902-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-23video-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="00902-181">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="00902-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-23video-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="00902-183">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="00902-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-23video-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="00902-185">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="00902-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-23video-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="00902-187">а.</span><span class="sxs-lookup"><span data-stu-id="00902-187">a.</span></span> <span data-ttu-id="00902-188">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="00902-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="00902-189">b.</span><span class="sxs-lookup"><span data-stu-id="00902-189">b.</span></span> <span data-ttu-id="00902-190">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="00902-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="00902-191">c.</span><span class="sxs-lookup"><span data-stu-id="00902-191">c.</span></span> <span data-ttu-id="00902-192">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="00902-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="00902-193">d.</span><span class="sxs-lookup"><span data-stu-id="00902-193">d.</span></span> <span data-ttu-id="00902-194">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="00902-194">Click **Create**.</span></span>
 
### <a name="creating-a-23-video-test-user"></a><span data-ttu-id="00902-195">Создание тестового пользователя 23 Video</span><span class="sxs-lookup"><span data-stu-id="00902-195">Creating a 23 Video test user</span></span>

<span data-ttu-id="00902-196">Цель этого раздела — создать в 23 Video пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="00902-196">The objective of this section is to create a user called Britta Simon in 23 Video.</span></span>

<span data-ttu-id="00902-197">**Чтобы создать в 23 Video пользователя с именем Britta Simon, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="00902-197">**To create a user called Britta Simon in 23 Video, perform the following steps:**</span></span>

1. <span data-ttu-id="00902-198">Войдите на сайт компании 23 Video от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="00902-198">Sign on to your 23 Video company site as administrator.</span></span>

2. <span data-ttu-id="00902-199">Перейдите в меню **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="00902-199">Go to **Settings**.</span></span>
 
3. <span data-ttu-id="00902-200">В разделе **Users** (Пользователи) щелкните **Configure** (Настройка).</span><span class="sxs-lookup"><span data-stu-id="00902-200">In **Users** section, click **Configure**.</span></span>
   
    ![Назначение пользователя][400]

4. <span data-ttu-id="00902-202">Щелкните **Add a new user**(Добавить нового пользователя).</span><span class="sxs-lookup"><span data-stu-id="00902-202">Click **Add a new user**.</span></span> 
   
    ![Назначение пользователя][401]

5. <span data-ttu-id="00902-204">В разделе **Invite someone to join this site** (Пригласить присоединиться к сайту) выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="00902-204">In the **Invite someone to join this site** section, perform the following steps:</span></span>
   
    ![Назначение пользователя][402]

    <span data-ttu-id="00902-206">а.</span><span class="sxs-lookup"><span data-stu-id="00902-206">a.</span></span> <span data-ttu-id="00902-207">В текстовом поле **E-mail addresses** (Адреса электронной почты) введите адрес электронной почты пользователя Britta Simon в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="00902-207">In the **E-mail addresses** textbox, type Britta Simon's email address in Azure AD.</span></span>  
 
    <span data-ttu-id="00902-208">b.</span><span class="sxs-lookup"><span data-stu-id="00902-208">b.</span></span> <span data-ttu-id="00902-209">Щелкните **Add the user**(Добавить пользователя).</span><span class="sxs-lookup"><span data-stu-id="00902-209">Click **Add the user**.</span></span>   

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="00902-210">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="00902-210">Assigning the Azure AD test user</span></span>

<span data-ttu-id="00902-211">В этом разделе мы разрешим пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к 23 Video.</span><span class="sxs-lookup"><span data-stu-id="00902-211">In this section, you enable Britta Simon to use Azure single sign-on by granting access to 23 Video.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="00902-213">**Назначение пользователя Britta Simon приложению 23 Video**</span><span class="sxs-lookup"><span data-stu-id="00902-213">**To assign Britta Simon to 23 Video, perform the following steps:**</span></span>

1. <span data-ttu-id="00902-214">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="00902-214">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="00902-216">В списке приложений выберите **23 Video**.</span><span class="sxs-lookup"><span data-stu-id="00902-216">In the applications list, select **23 Video**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-23video-tutorial/tutorial_23video_app.png) 

3. <span data-ttu-id="00902-218">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="00902-218">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="00902-220">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="00902-220">Click **Add** button.</span></span> <span data-ttu-id="00902-221">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="00902-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="00902-223">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="00902-223">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="00902-224">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="00902-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="00902-225">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="00902-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="00902-226">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="00902-226">Testing single sign-on</span></span>

<span data-ttu-id="00902-227">Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="00902-227">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="00902-228">Щелкнув плитку 23 Video на панели доступа, вы автоматически войдете в приложение 23 Video.</span><span class="sxs-lookup"><span data-stu-id="00902-228">When you click the 23 Video tile in the Access Panel, you should get automatically signed-on to your 23 Video application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="00902-229">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="00902-229">Additional resources</span></span>

* [<span data-ttu-id="00902-230">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="00902-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="00902-231">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="00902-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-23video-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-23video-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-23video-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-23video-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-23video-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-23video-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-23video-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-23video-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-23video-tutorial/tutorial_general_203.png

[400]: ./media/active-directory-saas-23video-tutorial/tutorial_23video_10.png
[401]: ./media/active-directory-saas-23video-tutorial/tutorial_23video_11.png
[402]: ./media/active-directory-saas-23video-tutorial/tutorial_23video_12.png
