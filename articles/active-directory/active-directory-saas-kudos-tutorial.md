---
title: "Учебник. Интеграция Azure Active Directory с Kudos | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и Kudos."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 39c47ce6-4944-47ba-8f53-3afa95398034
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.openlocfilehash: 353798fcfd4ad7ce017fc2fddf4110715db3ace2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kudos"></a><span data-ttu-id="177cf-103">Руководство. Интеграция Azure Active Directory с Kudos</span><span class="sxs-lookup"><span data-stu-id="177cf-103">Tutorial: Azure Active Directory integration with Kudos</span></span>

<span data-ttu-id="177cf-104">В этом руководстве описано, как интегрировать Kudos с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="177cf-104">In this tutorial, you learn how to integrate Kudos with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="177cf-105">Интеграция Kudos с Azure AD обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="177cf-105">Integrating Kudos with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="177cf-106">С помощью Azure AD вы можете контролировать доступ к Kudos.</span><span class="sxs-lookup"><span data-stu-id="177cf-106">You can control in Azure AD who has access to Kudos</span></span>
- <span data-ttu-id="177cf-107">Вы можете включить автоматический вход пользователей в Kudos (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="177cf-107">You can enable your users to automatically get signed-on to Kudos (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="177cf-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="177cf-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="177cf-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="177cf-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="177cf-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="177cf-110">Prerequisites</span></span>

<span data-ttu-id="177cf-111">Чтобы настроить интеграцию Azure AD с Kudos, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="177cf-111">To configure Azure AD integration with Kudos, you need the following items:</span></span>

- <span data-ttu-id="177cf-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="177cf-112">An Azure AD subscription</span></span>
- <span data-ttu-id="177cf-113">подписка Kudos с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="177cf-113">A Kudos single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="177cf-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="177cf-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="177cf-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="177cf-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="177cf-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="177cf-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="177cf-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="177cf-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="177cf-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="177cf-118">Scenario description</span></span>
<span data-ttu-id="177cf-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="177cf-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="177cf-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="177cf-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="177cf-121">Добавление Kudos из коллекции</span><span class="sxs-lookup"><span data-stu-id="177cf-121">Adding Kudos from the gallery</span></span>
2. <span data-ttu-id="177cf-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="177cf-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kudos-from-the-gallery"></a><span data-ttu-id="177cf-123">Добавление Kudos из коллекции</span><span class="sxs-lookup"><span data-stu-id="177cf-123">Adding Kudos from the gallery</span></span>
<span data-ttu-id="177cf-124">Чтобы настроить интеграцию Kudos с Azure AD, необходимо добавить Kudos из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="177cf-124">To configure the integration of Kudos into Azure AD, you need to add Kudos from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="177cf-125">**Чтобы добавить Kudos из коллекции, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="177cf-125">**To add Kudos from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="177cf-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="177cf-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="177cf-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="177cf-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="177cf-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="177cf-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="177cf-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="177cf-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="177cf-133">В поле поиска введите **Kudos**.</span><span class="sxs-lookup"><span data-stu-id="177cf-133">In the search box, type **Kudos**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_search.png)

5. <span data-ttu-id="177cf-135">На панели результатов выберите **Kudos** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="177cf-135">In the results panel, select **Kudos**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="177cf-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="177cf-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="177cf-138">В этом разделе описана настройка и проверка единого входа Azure AD в Kudos для тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="177cf-138">In this section, you configure and test Azure AD single sign-on with Kudos based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="177cf-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Kudos соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="177cf-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Kudos is to a user in Azure AD.</span></span> <span data-ttu-id="177cf-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Kudos.</span><span class="sxs-lookup"><span data-stu-id="177cf-140">In other words, a link relationship between an Azure AD user and the related user in Kudos needs to be established.</span></span>

<span data-ttu-id="177cf-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Kudos.</span><span class="sxs-lookup"><span data-stu-id="177cf-141">In Kudos, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="177cf-142">Чтобы настроить и проверить единый вход в Azure AD в Kudos, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="177cf-142">To configure and test Azure AD single sign-on with Kudos, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="177cf-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="177cf-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="177cf-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="177cf-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="177cf-145">**[Создание тестового пользователя Kudos](#creating-a-kudos-test-user)** требуется для создания в Kudos пользователя Britta Simon, связанного с представлением этого же пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="177cf-145">**[Creating a Kudos test user](#creating-a-kudos-test-user)** - to have a counterpart of Britta Simon in Kudos that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="177cf-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="177cf-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="177cf-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="177cf-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="177cf-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="177cf-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="177cf-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Kudos.</span><span class="sxs-lookup"><span data-stu-id="177cf-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Kudos application.</span></span>

<span data-ttu-id="177cf-150">**Чтобы настроить единый вход Azure AD в Kudos, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="177cf-150">**To configure Azure AD single sign-on with Kudos, perform the following steps:**</span></span>

1. <span data-ttu-id="177cf-151">На портале Azure на странице интеграции с приложением **Kudos** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="177cf-151">In the Azure portal, on the **Kudos** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="177cf-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="177cf-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_samlbase.png)

3. <span data-ttu-id="177cf-155">В разделе **Домены и URL-адреса Kudos** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="177cf-155">On the **Kudos Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_url.png)

    <span data-ttu-id="177cf-157">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<company>.kudosnow.com`</span><span class="sxs-lookup"><span data-stu-id="177cf-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company>.kudosnow.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="177cf-158">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="177cf-158">This value is not real.</span></span> <span data-ttu-id="177cf-159">Вместо него необходимо указать фактический URL-адрес для входа.</span><span class="sxs-lookup"><span data-stu-id="177cf-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="177cf-160">Для получения данного значения обратитесь в [службу поддержки клиентов Kudos](http://success.kudosnow.com/home).</span><span class="sxs-lookup"><span data-stu-id="177cf-160">Contact [Kudos Client support team](http://success.kudosnow.com/home) to get this value.</span></span> 
 
4. <span data-ttu-id="177cf-161">В разделе **Сертификат подписи SAML** щелкните **Сертификат (Base64)**, а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="177cf-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_certificate.png) 

5. <span data-ttu-id="177cf-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="177cf-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kudos-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="177cf-165">В разделе **Настройка Kudos** щелкните **Настроить Kudos**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="177cf-165">On the **Kudos Configuration** section, click **Configure Kudos** to open **Configure sign-on** window.</span></span> <span data-ttu-id="177cf-166">Скопируйте **URL-адрес выхода и URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="177cf-166">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_configure.png) 

7. <span data-ttu-id="177cf-168">В другом окне веб-браузера войдите на ваш корпоративный веб-сайт Kudos в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="177cf-168">In a different web browser window, log into your Kudos company site as an administrator.</span></span>

8. <span data-ttu-id="177cf-169">В верхнем меню нажмите пункт **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="177cf-169">In the menu on the top, click **Settings**.</span></span>
   
    <span data-ttu-id="177cf-170">![Параметры](./media/active-directory-saas-kudos-tutorial/ic787806.png "Параметры")</span><span class="sxs-lookup"><span data-stu-id="177cf-170">![Settings](./media/active-directory-saas-kudos-tutorial/ic787806.png "Settings")</span></span>

9. <span data-ttu-id="177cf-171">Выберите пункты **Integrations \> SSO** (Интеграции > Единый вход).</span><span class="sxs-lookup"><span data-stu-id="177cf-171">Click **Integrations \> SSO**.</span></span>

10. <span data-ttu-id="177cf-172">В разделе **Единый вход** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="177cf-172">In the **SSO** section, perform the following steps:</span></span>
   
    <span data-ttu-id="177cf-173">![SSO](./media/active-directory-saas-kudos-tutorial/ic787807.png "SSO")</span><span class="sxs-lookup"><span data-stu-id="177cf-173">![SSO](./media/active-directory-saas-kudos-tutorial/ic787807.png "SSO")</span></span>
   
    <span data-ttu-id="177cf-174">а.</span><span class="sxs-lookup"><span data-stu-id="177cf-174">a.</span></span> <span data-ttu-id="177cf-175">В текстовое поле **URL-адрес входа** вставьте значение **URL-адреса службы единого входа SAML**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="177cf-175">In **Sign on URL** textbox, paste the value of  **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="177cf-176">b.</span><span class="sxs-lookup"><span data-stu-id="177cf-176">b.</span></span> <span data-ttu-id="177cf-177">Откройте сертификат в кодировке Base-64 в Блокноте, скопируйте его содержимое в буфер обмена, а затем вставьте его в текстовое поле **Сертификат X.509** .</span><span class="sxs-lookup"><span data-stu-id="177cf-177">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **X.509 certificate** textbox</span></span>
   
    <span data-ttu-id="177cf-178">c.</span><span class="sxs-lookup"><span data-stu-id="177cf-178">c.</span></span> <span data-ttu-id="177cf-179">В текстовое поле **URL-адрес выхода** вставьте значение **URL-адреса выхода**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="177cf-179">In **Logout To URL**, paste the value of  **Sign-Out URL** which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="177cf-180">г)</span><span class="sxs-lookup"><span data-stu-id="177cf-180">d.</span></span> <span data-ttu-id="177cf-181">В текстовом поле **URL-адрес Kudos** введите название своей компании.</span><span class="sxs-lookup"><span data-stu-id="177cf-181">In the **Your Kudos URL** textbox, type your company name.</span></span>
   
    <span data-ttu-id="177cf-182">д.</span><span class="sxs-lookup"><span data-stu-id="177cf-182">e.</span></span> <span data-ttu-id="177cf-183">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="177cf-183">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="177cf-184">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="177cf-184">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="177cf-185">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="177cf-185">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="177cf-186">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="177cf-186">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="177cf-187">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="177cf-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="177cf-188">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="177cf-188">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="177cf-190">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="177cf-190">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="177cf-191">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="177cf-191">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kudos-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="177cf-193">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="177cf-193">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kudos-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="177cf-195">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="177cf-195">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kudos-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="177cf-197">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="177cf-197">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kudos-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="177cf-199">а.</span><span class="sxs-lookup"><span data-stu-id="177cf-199">a.</span></span> <span data-ttu-id="177cf-200">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="177cf-200">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="177cf-201">b.</span><span class="sxs-lookup"><span data-stu-id="177cf-201">b.</span></span> <span data-ttu-id="177cf-202">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="177cf-202">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="177cf-203">c.</span><span class="sxs-lookup"><span data-stu-id="177cf-203">c.</span></span> <span data-ttu-id="177cf-204">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="177cf-204">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="177cf-205">d.</span><span class="sxs-lookup"><span data-stu-id="177cf-205">d.</span></span> <span data-ttu-id="177cf-206">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="177cf-206">Click **Create**.</span></span>
 
### <a name="creating-a-kudos-test-user"></a><span data-ttu-id="177cf-207">Создание тестового пользователя Kudos</span><span class="sxs-lookup"><span data-stu-id="177cf-207">Creating a Kudos test user</span></span>

<span data-ttu-id="177cf-208">Чтобы разрешить пользователям Azure AD вход в Kudos, они должны быть подготовлены для Kudos.</span><span class="sxs-lookup"><span data-stu-id="177cf-208">In order to enable Azure AD users to log into Kudos, they must be provisioned into Kudos.</span></span> 

<span data-ttu-id="177cf-209">В случае с Kudos подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="177cf-209">In the case of Kudos, provisioning is a manual task.</span></span>

<span data-ttu-id="177cf-210">**Чтобы подготовить учетную запись пользователя, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="177cf-210">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="177cf-211">Выполните вход на веб-сайт **Kudos** компании в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="177cf-211">Log in to your **Kudos** company site as administrator.</span></span>

2. <span data-ttu-id="177cf-212">В верхнем меню нажмите пункт **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="177cf-212">In the menu on the top, click **Settings**.</span></span>
   
   <span data-ttu-id="177cf-213">![Параметры](./media/active-directory-saas-kudos-tutorial/ic787806.png "Параметры")</span><span class="sxs-lookup"><span data-stu-id="177cf-213">![Settings](./media/active-directory-saas-kudos-tutorial/ic787806.png "Settings")</span></span>

3. <span data-ttu-id="177cf-214">Выберите **Администратор пользователей**.</span><span class="sxs-lookup"><span data-stu-id="177cf-214">Click **User Admin**.</span></span>

4. <span data-ttu-id="177cf-215">Откройте вкладку **Пользователи** и щелкните **Добавить пользователя**.</span><span class="sxs-lookup"><span data-stu-id="177cf-215">Click the **Users** tab, and then click **Add a User**.</span></span>
   
   <span data-ttu-id="177cf-216">![User Admin](./media/active-directory-saas-kudos-tutorial/ic787809.png "User Admin") (Администратор пользователей)</span><span class="sxs-lookup"><span data-stu-id="177cf-216">![User Admin](./media/active-directory-saas-kudos-tutorial/ic787809.png "User Admin")</span></span>

5. <span data-ttu-id="177cf-217">В разделе **Добавление пользователя** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="177cf-217">In the **Add a User** section, perform the following steps:</span></span>
   
    <span data-ttu-id="177cf-218">![Добавление пользователя](./media/active-directory-saas-kudos-tutorial/ic787810.png "Добавление пользователя")</span><span class="sxs-lookup"><span data-stu-id="177cf-218">![Add a User](./media/active-directory-saas-kudos-tutorial/ic787810.png "Add a User")</span></span>
   
    <span data-ttu-id="177cf-219">а.</span><span class="sxs-lookup"><span data-stu-id="177cf-219">a.</span></span> <span data-ttu-id="177cf-220">В соответствующие текстовые поля введите атрибуты **First Name** (Имя), **Last Name** (Фамилия), **Email** (Адрес электронной почты) и другие данные действующей учетной записи Azure Active Directory, которую вы хотите подготовить.</span><span class="sxs-lookup"><span data-stu-id="177cf-220">Type the **First Name**, **Last Name**, **Email** and other details of a valid Azure Active Directory account you want to provision into the related textboxes.</span></span>
   
    <span data-ttu-id="177cf-221">b.</span><span class="sxs-lookup"><span data-stu-id="177cf-221">b.</span></span> <span data-ttu-id="177cf-222">Щелкните **Создать пользователя**.</span><span class="sxs-lookup"><span data-stu-id="177cf-222">Click **Create User**.</span></span>

>[!NOTE]
><span data-ttu-id="177cf-223">Вы можете использовать любые другие средства создания учетной записи пользователя Kudos или API, предоставляемые Kudos для подготовки учетных записей пользователя AAD.</span><span class="sxs-lookup"><span data-stu-id="177cf-223">You can use any other Kudos user account creation tools or APIs provided by Kudos to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="177cf-224">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="177cf-224">Assigning the Azure AD test user</span></span>

<span data-ttu-id="177cf-225">В этом разделе описано, как включить единый вход Azure для пользователя Britta Simon и предоставить этому пользователю доступ к Kudos.</span><span class="sxs-lookup"><span data-stu-id="177cf-225">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Kudos.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="177cf-227">**Чтобы назначить пользователя Britta Simon в Kudos, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="177cf-227">**To assign Britta Simon to Kudos, perform the following steps:**</span></span>

1. <span data-ttu-id="177cf-228">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="177cf-228">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="177cf-230">В списке приложений выберите **Kudos**.</span><span class="sxs-lookup"><span data-stu-id="177cf-230">In the applications list, select **Kudos**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kudos-tutorial/tutorial_kudos_app.png) 

3. <span data-ttu-id="177cf-232">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="177cf-232">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="177cf-234">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="177cf-234">Click **Add** button.</span></span> <span data-ttu-id="177cf-235">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="177cf-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="177cf-237">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="177cf-237">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="177cf-238">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="177cf-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="177cf-239">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="177cf-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="177cf-240">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="177cf-240">Testing single sign-on</span></span>

<span data-ttu-id="177cf-241">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="177cf-241">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="177cf-242">Щелкнув элемент Kudos на панели доступа, вы автоматически войдете в приложение Kudos.</span><span class="sxs-lookup"><span data-stu-id="177cf-242">When you click the Kudos tile in the Access Panel, you should get automatically signed-on to your Kudos application.</span></span> <span data-ttu-id="177cf-243">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="177cf-243">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="177cf-244">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="177cf-244">Additional resources</span></span>

* [<span data-ttu-id="177cf-245">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="177cf-245">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="177cf-246">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="177cf-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kudos-tutorial/tutorial_general_203.png

