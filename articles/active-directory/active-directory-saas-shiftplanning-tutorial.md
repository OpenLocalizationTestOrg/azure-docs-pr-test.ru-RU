---
title: "Учебник. Интеграция Azure Active Directory с Humanity | Документы Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и Humanity."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 6aa771e9-31c6-48d1-8dde-024bebc06943
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: jeedes
ms.openlocfilehash: 327cc1e3d0836e79376e0a3cd5a4422a967f5943
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-humanity"></a><span data-ttu-id="74513-103">Учебник. Интеграция Azure Active Directory с Humanity</span><span class="sxs-lookup"><span data-stu-id="74513-103">Tutorial: Azure Active Directory integration with Humanity</span></span>

<span data-ttu-id="74513-104">В этом учебнике описано, как интегрировать Humanity с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="74513-104">In this tutorial, you learn how to integrate Humanity with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="74513-105">Интеграция Azure AD с приложением Humanity обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="74513-105">Integrating Humanity with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="74513-106">С помощью Azure AD можно управлять доступом к Humanity.</span><span class="sxs-lookup"><span data-stu-id="74513-106">You can control in Azure AD who has access to Humanity</span></span>
- <span data-ttu-id="74513-107">Вы можете включить автоматический вход пользователей в Humanity (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="74513-107">You can enable your users to automatically get signed-on to Humanity (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="74513-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="74513-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="74513-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="74513-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="74513-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="74513-110">Prerequisites</span></span>

<span data-ttu-id="74513-111">Чтобы настроить интеграцию Azure AD с Humanity, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="74513-111">To configure Azure AD integration with Humanity, you need the following items:</span></span>

- <span data-ttu-id="74513-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="74513-112">An Azure AD subscription</span></span>
- <span data-ttu-id="74513-113">подписка Humanity с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="74513-113">A Humanity single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="74513-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="74513-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="74513-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="74513-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="74513-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="74513-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="74513-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="74513-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="74513-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="74513-118">Scenario description</span></span>
<span data-ttu-id="74513-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="74513-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="74513-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="74513-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="74513-121">Добавление Humanity из коллекции</span><span class="sxs-lookup"><span data-stu-id="74513-121">Adding Humanity from the gallery</span></span>
2. <span data-ttu-id="74513-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="74513-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-humanity-from-the-gallery"></a><span data-ttu-id="74513-123">Добавление Humanity из коллекции</span><span class="sxs-lookup"><span data-stu-id="74513-123">Adding Humanity from the gallery</span></span>
<span data-ttu-id="74513-124">Чтобы настроить интеграцию Humanity с Azure AD, необходимо добавить Humanity из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="74513-124">To configure the integration of Humanity into Azure AD, you need to add Humanity from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="74513-125">**Чтобы добавить Humanity из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="74513-125">**To add Humanity from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="74513-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="74513-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="74513-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="74513-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="74513-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="74513-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="74513-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="74513-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="74513-133">В поле поиска введите **Humanity**.</span><span class="sxs-lookup"><span data-stu-id="74513-133">In the search box, type **Humanity**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_search.png)

5. <span data-ttu-id="74513-135">На панели результатов выберите **Humanity** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="74513-135">In the results panel, select **Humanity**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="74513-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="74513-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="74513-138">В этом разделе описана настройка и проверка единого входа Azure AD в Humanity с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="74513-138">In this section, you configure and test Azure AD single sign-on with Humanity based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="74513-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Humanity соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="74513-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Humanity is to a user in Azure AD.</span></span> <span data-ttu-id="74513-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Humanity.</span><span class="sxs-lookup"><span data-stu-id="74513-140">In other words, a link relationship between an Azure AD user and the related user in Humanity needs to be established.</span></span>

<span data-ttu-id="74513-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Humanity.</span><span class="sxs-lookup"><span data-stu-id="74513-141">In Humanity, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="74513-142">Чтобы настроить и проверить единый вход Azure AD в Humanity, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="74513-142">To configure and test Azure AD single sign-on with Humanity, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="74513-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="74513-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="74513-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="74513-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="74513-145">**[Создание тестового пользователя Humanity](#creating-a-humanity-test-user)** требуется для создания в Humanity пользователя Britta Simon, связанного с представлением этого пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="74513-145">**[Creating a Humanity test user](#creating-a-humanity-test-user)** - to have a counterpart of Britta Simon in Humanity that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="74513-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="74513-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="74513-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="74513-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="74513-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="74513-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="74513-149">В этом разделе описано, как включить единый вход Azure AD на новом портале Azure и настроить его в приложении Humanity.</span><span class="sxs-lookup"><span data-stu-id="74513-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Humanity application.</span></span>

<span data-ttu-id="74513-150">**Чтобы настроить единый вход Azure AD в Humanity, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="74513-150">**To configure Azure AD single sign-on with Humanity, perform the following steps:**</span></span>

1. <span data-ttu-id="74513-151">На портале Azure на странице интеграции с приложением **Humanity** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="74513-151">In the Azure portal, on the **Humanity** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="74513-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="74513-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_samlbase.png)

3. <span data-ttu-id="74513-155">В разделе **Домены и URL-адреса приложения Humanity** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="74513-155">On the **Humanity Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_url.png)

    <span data-ttu-id="74513-157">а.</span><span class="sxs-lookup"><span data-stu-id="74513-157">a.</span></span> <span data-ttu-id="74513-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://company.humanity.com/includes/saml/`</span><span class="sxs-lookup"><span data-stu-id="74513-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://company.humanity.com/includes/saml/`</span></span>

    <span data-ttu-id="74513-159">b.</span><span class="sxs-lookup"><span data-stu-id="74513-159">b.</span></span> <span data-ttu-id="74513-160">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://company.humanity.com/app/`</span><span class="sxs-lookup"><span data-stu-id="74513-160">In the **Identifier** textbox, type a URL using the following pattern: `https://company.humanity.com/app/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="74513-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="74513-161">These values are not real.</span></span> <span data-ttu-id="74513-162">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="74513-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="74513-163">Чтобы получить их, обратитесь в [службу поддержки клиентов Humanity](https://www.humanity.com/support/).</span><span class="sxs-lookup"><span data-stu-id="74513-163">Contact [Humanity Client support team](https://www.humanity.com/support/) to get these values.</span></span> 
 
4. <span data-ttu-id="74513-164">В разделе **Сертификат для подписи токена SAML** щелкните **Certificate (Base64)** (Сертификат (Base64)), а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="74513-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_certificate.png) 

5. <span data-ttu-id="74513-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="74513-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="74513-168">В разделе **Настройка Humanity** щелкните **Настроить Humanity**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="74513-168">On the **Humanity Configuration** section, click **Configure Humanity** to open **Configure sign-on** window.</span></span> <span data-ttu-id="74513-169">Скопируйте **URL-адрес службы единого входа SAML и URL-адрес выхода** из раздела **Краткий справочник.**</span><span class="sxs-lookup"><span data-stu-id="74513-169">Copy the **SAML Single Sign-On Service URL, and Sign-Out URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_configure.png) 

7. <span data-ttu-id="74513-171">В другом окне веб-браузера войдите на свой корпоративный веб-сайт **Humanity** в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="74513-171">In a different web browser window, log in to your **Humanity** company site as an administrator.</span></span>

8. <span data-ttu-id="74513-172">В верхнем меню щелкните **Администратор**.</span><span class="sxs-lookup"><span data-stu-id="74513-172">In the menu on the top, click **Admin**.</span></span>
   
    <span data-ttu-id="74513-173">![Администратор](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "Администратор")</span><span class="sxs-lookup"><span data-stu-id="74513-173">![Admin](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "Admin")</span></span>

9. <span data-ttu-id="74513-174">В разделе **Integration** (Интеграция) щелкните **Single Sign-On** (Единый вход).</span><span class="sxs-lookup"><span data-stu-id="74513-174">Under **Integration**, click **Single Sign-On**.</span></span>
   
    <span data-ttu-id="74513-175">![Единый вход](./media/active-directory-saas-shiftplanning-tutorial/iC786620.png "Единый вход")</span><span class="sxs-lookup"><span data-stu-id="74513-175">![Single Sign-On](./media/active-directory-saas-shiftplanning-tutorial/iC786620.png "Single Sign-On")</span></span>

10. <span data-ttu-id="74513-176">В разделе **Единый вход** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="74513-176">In the **Single Sign-On** section, perform the following steps:</span></span>
   
    <span data-ttu-id="74513-177">![Единый вход](./media/active-directory-saas-shiftplanning-tutorial/iC786905.png "Единый вход")</span><span class="sxs-lookup"><span data-stu-id="74513-177">![Single Sign-On](./media/active-directory-saas-shiftplanning-tutorial/iC786905.png "Single Sign-On")</span></span>
   
    <span data-ttu-id="74513-178">а.</span><span class="sxs-lookup"><span data-stu-id="74513-178">a.</span></span> <span data-ttu-id="74513-179">Установите флажок **SAML включен**.</span><span class="sxs-lookup"><span data-stu-id="74513-179">Select **SAML Enabled**.</span></span>

    <span data-ttu-id="74513-180">b.</span><span class="sxs-lookup"><span data-stu-id="74513-180">b.</span></span> <span data-ttu-id="74513-181">Установите флажок **Allow Password Login** (Разрешить вход с паролем).</span><span class="sxs-lookup"><span data-stu-id="74513-181">Select **Allow Password Login**.</span></span>

    <span data-ttu-id="74513-182">c.</span><span class="sxs-lookup"><span data-stu-id="74513-182">c.</span></span> <span data-ttu-id="74513-183">Вставьте **URL-адрес службы единого входа SAML** в текстовое поле **URL-адрес издателя SAML**.</span><span class="sxs-lookup"><span data-stu-id="74513-183">Paste the **SAML Single Sign-On Service URL** value into the **SAML Issuer URL** textbox.</span></span>

    <span data-ttu-id="74513-184">г)</span><span class="sxs-lookup"><span data-stu-id="74513-184">d.</span></span> <span data-ttu-id="74513-185">Вставьте значение **URL-адреса выхода** в текстовое поле **URL-адрес удаленного выхода**.</span><span class="sxs-lookup"><span data-stu-id="74513-185">Paste the **Sign-Out URL** value into the **Remote Logout URL** textbox.</span></span>
   
    <span data-ttu-id="74513-186">д.</span><span class="sxs-lookup"><span data-stu-id="74513-186">e.</span></span> <span data-ttu-id="74513-187">Откройте сертификат в кодировке Base-64 в Блокноте, скопируйте его содержимое в буфер обмена, а затем вставьте его в текстовое поле **Сертификат X.509** .</span><span class="sxs-lookup"><span data-stu-id="74513-187">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox.</span></span>

11. <span data-ttu-id="74513-188">Нажмите кнопку **Сохранить параметры**.</span><span class="sxs-lookup"><span data-stu-id="74513-188">Click **Save Settings**.</span></span>

> [!TIP]
> <span data-ttu-id="74513-189">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="74513-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="74513-190">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="74513-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="74513-191">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="74513-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="74513-192">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="74513-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="74513-193">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="74513-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="74513-195">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="74513-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="74513-196">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="74513-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="74513-198">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="74513-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="74513-200">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="74513-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="74513-202">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="74513-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-shiftplanning-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="74513-204">а.</span><span class="sxs-lookup"><span data-stu-id="74513-204">a.</span></span> <span data-ttu-id="74513-205">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="74513-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="74513-206">b.</span><span class="sxs-lookup"><span data-stu-id="74513-206">b.</span></span> <span data-ttu-id="74513-207">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="74513-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="74513-208">c.</span><span class="sxs-lookup"><span data-stu-id="74513-208">c.</span></span> <span data-ttu-id="74513-209">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="74513-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="74513-210">d.</span><span class="sxs-lookup"><span data-stu-id="74513-210">d.</span></span> <span data-ttu-id="74513-211">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="74513-211">Click **Create**.</span></span>
 
### <a name="creating-a-humanity-test-user"></a><span data-ttu-id="74513-212">Создание тестового пользователя Humanity</span><span class="sxs-lookup"><span data-stu-id="74513-212">Creating a Humanity test user</span></span>

<span data-ttu-id="74513-213">Чтобы пользователи Azure AD могли выполнять вход в Humanity, они должны быть подготовлены в Humanity.</span><span class="sxs-lookup"><span data-stu-id="74513-213">In order to enable Azure AD users to log in to Humanity, they must be provisioned into Humanity.</span></span> <span data-ttu-id="74513-214">В случае с Humanity подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="74513-214">In the case of Humanity, provisioning is a manual task.</span></span>

<span data-ttu-id="74513-215">**Чтобы подготовить учетную запись пользователя, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="74513-215">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="74513-216">Войдите на веб-сайт **Humanity** вашей компании в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="74513-216">Log in to your **Humanity** company site as an administrator.</span></span>

2. <span data-ttu-id="74513-217">Щелкните **Администратор**.</span><span class="sxs-lookup"><span data-stu-id="74513-217">Click **Admin**.</span></span>
   
    <span data-ttu-id="74513-218">![Администратор](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "Администратор")</span><span class="sxs-lookup"><span data-stu-id="74513-218">![Admin](./media/active-directory-saas-shiftplanning-tutorial/iC786619.png "Admin")</span></span>

3. <span data-ttu-id="74513-219">Щелкните **Персонал**.</span><span class="sxs-lookup"><span data-stu-id="74513-219">Click **Staff**.</span></span>
   
    <span data-ttu-id="74513-220">![Персонал](./media/active-directory-saas-shiftplanning-tutorial/ic786623.png "Персонал")</span><span class="sxs-lookup"><span data-stu-id="74513-220">![Staff](./media/active-directory-saas-shiftplanning-tutorial/ic786623.png "Staff")</span></span>

4. <span data-ttu-id="74513-221">В разделе **Действия** щелкните **Добавление сотрудников**.</span><span class="sxs-lookup"><span data-stu-id="74513-221">Under **Actions**, click **Add Employees**.</span></span>
   
    <span data-ttu-id="74513-222">![Добавить сотрудников](./media/active-directory-saas-shiftplanning-tutorial/iC786624.png "Добавить сотрудников")</span><span class="sxs-lookup"><span data-stu-id="74513-222">![Add Employees](./media/active-directory-saas-shiftplanning-tutorial/iC786624.png "Add Employees")</span></span>

5. <span data-ttu-id="74513-223">В разделе **Добавление сотрудников** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="74513-223">In the **Add Employees** section, perform the following steps:</span></span>
   
    <span data-ttu-id="74513-224">![Сохранить сотрудников](./media/active-directory-saas-shiftplanning-tutorial/iC786625.png "Сохранить сотрудников")</span><span class="sxs-lookup"><span data-stu-id="74513-224">![Save Employees](./media/active-directory-saas-shiftplanning-tutorial/iC786625.png "Save Employees")</span></span>
   
    <span data-ttu-id="74513-225">а.</span><span class="sxs-lookup"><span data-stu-id="74513-225">a.</span></span> <span data-ttu-id="74513-226">Заполните текстовые поля **Имя**, **Фамилия** и **Email** (Электронная почта) данными действующей учетной записи AAD, которую необходимо подготовить.</span><span class="sxs-lookup"><span data-stu-id="74513-226">Type the **First Name**, **Last Name**, and **Email** of a valid AAD account you want to provision into the related textboxes.</span></span>

    <span data-ttu-id="74513-227">b.</span><span class="sxs-lookup"><span data-stu-id="74513-227">b.</span></span> <span data-ttu-id="74513-228">Щелкните **Сохранить сотрудников**.</span><span class="sxs-lookup"><span data-stu-id="74513-228">Click **Save Employees**.</span></span>

>[!NOTE]
><span data-ttu-id="74513-229">Вы можете использовать любые другие средства создания учетной записи пользователя Humanity или API, предоставляемые Humanity для подготовки учетных записей пользователей AAD.</span><span class="sxs-lookup"><span data-stu-id="74513-229">You can use any other Humanity user account creation tools or APIs provided by Humanity to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="74513-230">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="74513-230">Assigning the Azure AD test user</span></span>

<span data-ttu-id="74513-231">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure путем предоставления доступа к Humanity.</span><span class="sxs-lookup"><span data-stu-id="74513-231">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Humanity.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="74513-233">**Чтобы назначить пользователя Britta Simon в Humanity, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="74513-233">**To assign Britta Simon to Humanity, perform the following steps:**</span></span>

1. <span data-ttu-id="74513-234">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="74513-234">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="74513-236">В списке приложений выберите **Humanity**.</span><span class="sxs-lookup"><span data-stu-id="74513-236">In the applications list, select **Humanity**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-shiftplanning-tutorial/tutorial_humanity_app.png) 

3. <span data-ttu-id="74513-238">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="74513-238">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="74513-240">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="74513-240">Click **Add** button.</span></span> <span data-ttu-id="74513-241">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="74513-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="74513-243">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="74513-243">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="74513-244">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="74513-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="74513-245">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="74513-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="74513-246">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="74513-246">Testing single sign-on</span></span>

<span data-ttu-id="74513-247">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="74513-247">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="74513-248">Щелкнув плитку Humanity на панели доступа, вы автоматически войдете в приложение Humanity.</span><span class="sxs-lookup"><span data-stu-id="74513-248">When you click the Humanity tile in the Access Panel, you should get automatically signed-on to your Humanity application.</span></span>
<span data-ttu-id="74513-249">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="74513-249">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="74513-250">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="74513-250">Additional resources</span></span>

* [<span data-ttu-id="74513-251">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="74513-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="74513-252">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="74513-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-shiftplanning-tutorial/tutorial_general_203.png

