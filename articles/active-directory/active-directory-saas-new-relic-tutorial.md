---
title: "Руководство по интеграции Azure Active Directory с New Relic | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и New Relic."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3186b9a8-f4d8-45e2-ad82-6275f95e7aa6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: jeedes
ms.openlocfilehash: 605e85c23a849f70fcc0237361d7a891f716ca3a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-new-relic"></a><span data-ttu-id="b8c71-103">Учебник. Интеграция Azure Active Directory с New Relic</span><span class="sxs-lookup"><span data-stu-id="b8c71-103">Tutorial: Azure Active Directory integration with New Relic</span></span>

<span data-ttu-id="b8c71-104">В этом руководстве описано, как интегрировать New Relic с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b8c71-104">In this tutorial, you learn how to integrate New Relic with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b8c71-105">Интеграция Azure AD с приложением New Relic обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="b8c71-105">Integrating New Relic with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b8c71-106">С помощью Azure AD вы можете контролировать доступ к New Relic.</span><span class="sxs-lookup"><span data-stu-id="b8c71-106">You can control in Azure AD who has access to New Relic</span></span>
- <span data-ttu-id="b8c71-107">Вы можете включить автоматический вход пользователей в New Relic (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b8c71-107">You can enable your users to automatically get signed-on to New Relic (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b8c71-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="b8c71-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b8c71-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b8c71-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b8c71-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b8c71-110">Prerequisites</span></span>

<span data-ttu-id="b8c71-111">Чтобы настроить интеграцию Azure AD с New Relic, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="b8c71-111">To configure Azure AD integration with New Relic, you need the following items:</span></span>

- <span data-ttu-id="b8c71-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="b8c71-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b8c71-113">Подписка с поддержкой единого входа New Relic.</span><span class="sxs-lookup"><span data-stu-id="b8c71-113">A New Relic single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b8c71-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="b8c71-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b8c71-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="b8c71-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b8c71-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="b8c71-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b8c71-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b8c71-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b8c71-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="b8c71-118">Scenario description</span></span>
<span data-ttu-id="b8c71-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="b8c71-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b8c71-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="b8c71-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b8c71-121">Добавление New Relic из коллекции.</span><span class="sxs-lookup"><span data-stu-id="b8c71-121">Adding New Relic from the gallery</span></span>
2. <span data-ttu-id="b8c71-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b8c71-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-new-relic-from-the-gallery"></a><span data-ttu-id="b8c71-123">Добавление New Relic из коллекции</span><span class="sxs-lookup"><span data-stu-id="b8c71-123">Adding New Relic from the gallery</span></span>
<span data-ttu-id="b8c71-124">Чтобы настроить интеграцию New Relic с Azure AD, необходимо добавить New Relic из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="b8c71-124">To configure the integration of New Relic into Azure AD, you need to add New Relic from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b8c71-125">**Чтобы добавить New Relic из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="b8c71-125">**To add New Relic from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b8c71-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b8c71-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b8c71-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="b8c71-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b8c71-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="b8c71-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="b8c71-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="b8c71-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="b8c71-133">В поле поиска введите **New Relic**.</span><span class="sxs-lookup"><span data-stu-id="b8c71-133">In the search box, type **New Relic**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_search.png)

5. <span data-ttu-id="b8c71-135">На панели результатов выберите **New Relic** и щелкните **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="b8c71-135">In the results panel, select **New Relic**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b8c71-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b8c71-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b8c71-138">В этом разделе описаны настройка и проверка единого входа Azure AD в приложение New Relic с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b8c71-138">In this section, you configure and test Azure AD single sign-on with New Relic based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b8c71-139">Чтобы единый вход работал, Azure AD необходимо знать, какой пользователь в New Relic соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b8c71-139">For single sign-on to work, Azure AD needs to know what the counterpart user in New Relic is to a user in Azure AD.</span></span> <span data-ttu-id="b8c71-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в New Relic.</span><span class="sxs-lookup"><span data-stu-id="b8c71-140">In other words, a link relationship between an Azure AD user and the related user in New Relic needs to be established.</span></span>

<span data-ttu-id="b8c71-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в New Relic.</span><span class="sxs-lookup"><span data-stu-id="b8c71-141">In New Relic, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="b8c71-142">Чтобы настроить и проверить единый вход Azure AD в New Relic, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="b8c71-142">To configure and test Azure AD single sign-on with New Relic, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b8c71-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="b8c71-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b8c71-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b8c71-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b8c71-145">**[Создание тестового пользователя New Relic](#creating-a-new-relic-test-user)** требуется для создания в New Relic пользователя Britta Simon, связанного с представлением этого же пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b8c71-145">**[Creating a New Relic test user](#creating-a-new-relic-test-user)** - to have a counterpart of Britta Simon in New Relic that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b8c71-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b8c71-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b8c71-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="b8c71-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b8c71-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b8c71-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b8c71-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении New Relic.</span><span class="sxs-lookup"><span data-stu-id="b8c71-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your New Relic application.</span></span>

<span data-ttu-id="b8c71-150">**Чтобы настроить единый вход Azure AD в New Relic, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="b8c71-150">**To configure Azure AD single sign-on with New Relic, perform the following steps:**</span></span>

1. <span data-ttu-id="b8c71-151">На портале Azure на странице интеграции с приложением **New Relic** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="b8c71-151">In the Azure portal, on the **New Relic** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="b8c71-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="b8c71-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_samlbase.png)

3. <span data-ttu-id="b8c71-155">В разделе **Домены и URL-адреса приложения New Relic** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="b8c71-155">On the **New Relic Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_url.png)

    <span data-ttu-id="b8c71-157">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<subdomain>.newrelic.com`</span><span class="sxs-lookup"><span data-stu-id="b8c71-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.newrelic.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b8c71-158">Это значение приведено для примера.</span><span class="sxs-lookup"><span data-stu-id="b8c71-158">The value is not real.</span></span> <span data-ttu-id="b8c71-159">Вместо него необходимо указать фактический URL-адрес для входа.</span><span class="sxs-lookup"><span data-stu-id="b8c71-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="b8c71-160">Чтобы получить это значение, обратитесь в [службу поддержки клиентов New Relic](https://support.newrelic.com/).</span><span class="sxs-lookup"><span data-stu-id="b8c71-160">Contact [New Relic Client support team](https://support.newrelic.com/) to get the value.</span></span> 
 
4. <span data-ttu-id="b8c71-161">В разделе **Сертификат для подписи токена SAML** щелкните **Certificate (Base64)** (Сертификат (Base64)), а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="b8c71-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_certificate.png) 

5. <span data-ttu-id="b8c71-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="b8c71-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-new-relic-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b8c71-165">В разделе **Настройка New Relic** щелкните **Настроить New Relic**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="b8c71-165">On the **New Relic Configuration** section, click **Configure New Relic** to open **Configure sign-on** window.</span></span> <span data-ttu-id="b8c71-166">Скопируйте **URL-адрес выхода и URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="b8c71-166">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_configure.png) 

7. <span data-ttu-id="b8c71-168">В другом окне веб-браузера войдите на веб-сайт **New Relic** компании в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="b8c71-168">In a different web browser window, sign on to your **New Relic** company site as administrator.</span></span>

8. <span data-ttu-id="b8c71-169">В меню в верхней части страницы щелкните **Параметры учетной записи**.</span><span class="sxs-lookup"><span data-stu-id="b8c71-169">In the menu on the top, click **Account Settings**.</span></span>
   
    <span data-ttu-id="b8c71-170">![Параметры учетной записи](./media/active-directory-saas-new-relic-tutorial/ic797036.png "параметры учетной записи")</span><span class="sxs-lookup"><span data-stu-id="b8c71-170">![Account Settings](./media/active-directory-saas-new-relic-tutorial/ic797036.png "Account Settings")</span></span>

9. <span data-ttu-id="b8c71-171">Щелкните вкладку **Security and authentication** (Безопасность и аутентификация), а затем выберите вкладку **Single sign on** (Единый вход).</span><span class="sxs-lookup"><span data-stu-id="b8c71-171">Click the **Security and authentication** tab, and then click the **Single sign on** tab.</span></span>
   
    <span data-ttu-id="b8c71-172">![Единый вход](./media/active-directory-saas-new-relic-tutorial/ic797037.png "Единый вход")</span><span class="sxs-lookup"><span data-stu-id="b8c71-172">![Single Sign-On](./media/active-directory-saas-new-relic-tutorial/ic797037.png "Single Sign-On")</span></span>

10. <span data-ttu-id="b8c71-173">На диалоговой странице «Настройка SAML» выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="b8c71-173">On the SAML dialog page, perform the following steps:</span></span>
   
    <span data-ttu-id="b8c71-174">![SAML](./media/active-directory-saas-new-relic-tutorial/ic797038.png "SAML")</span><span class="sxs-lookup"><span data-stu-id="b8c71-174">![SAML](./media/active-directory-saas-new-relic-tutorial/ic797038.png "SAML")</span></span>
   
   <span data-ttu-id="b8c71-175">а.</span><span class="sxs-lookup"><span data-stu-id="b8c71-175">a.</span></span> <span data-ttu-id="b8c71-176">Щелкните **Выбор файла** , чтобы передать скачанный сертификат Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b8c71-176">Click **Choose File** to upload your downloaded Azure Active Directory certificate.</span></span>

   <span data-ttu-id="b8c71-177">b.</span><span class="sxs-lookup"><span data-stu-id="b8c71-177">b.</span></span> <span data-ttu-id="b8c71-178">В текстовое поле **URL-адрес удаленного входа** вставьте значение **URL-адрес службы единого входа SAML**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="b8c71-178">In the **Remote login URL** textbox,  paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
   <span data-ttu-id="b8c71-179">c.</span><span class="sxs-lookup"><span data-stu-id="b8c71-179">c.</span></span> <span data-ttu-id="b8c71-180">В текстовое поле **Logout landing URL** (URL-адрес целевой страницы выхода) вставьте значение **URL-адреса выхода**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="b8c71-180">In the **Logout landing URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

   <span data-ttu-id="b8c71-181">г)</span><span class="sxs-lookup"><span data-stu-id="b8c71-181">d.</span></span> <span data-ttu-id="b8c71-182">Щелкните **Сохранить изменения**.</span><span class="sxs-lookup"><span data-stu-id="b8c71-182">Click **Save my changes**.</span></span>

> [!TIP]
> <span data-ttu-id="b8c71-183">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="b8c71-183">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b8c71-184">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="b8c71-184">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b8c71-185">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="b8c71-185">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b8c71-186">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="b8c71-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="b8c71-187">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b8c71-187">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="b8c71-189">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="b8c71-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b8c71-190">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b8c71-190">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-new-relic-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b8c71-192">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="b8c71-192">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-new-relic-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b8c71-194">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="b8c71-194">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-new-relic-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b8c71-196">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="b8c71-196">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-new-relic-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b8c71-198">а.</span><span class="sxs-lookup"><span data-stu-id="b8c71-198">a.</span></span> <span data-ttu-id="b8c71-199">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b8c71-199">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b8c71-200">b.</span><span class="sxs-lookup"><span data-stu-id="b8c71-200">b.</span></span> <span data-ttu-id="b8c71-201">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b8c71-201">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b8c71-202">c.</span><span class="sxs-lookup"><span data-stu-id="b8c71-202">c.</span></span> <span data-ttu-id="b8c71-203">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="b8c71-203">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b8c71-204">d.</span><span class="sxs-lookup"><span data-stu-id="b8c71-204">d.</span></span> <span data-ttu-id="b8c71-205">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="b8c71-205">Click **Create**.</span></span>
 
### <a name="creating-a-new-relic-test-user"></a><span data-ttu-id="b8c71-206">Создание тестового пользователя New Relic</span><span class="sxs-lookup"><span data-stu-id="b8c71-206">Creating a New Relic test user</span></span>

<span data-ttu-id="b8c71-207">Чтобы пользователи Azure Active Directory могли входить New Relic, они должны быть подготовлены в New Relic.</span><span class="sxs-lookup"><span data-stu-id="b8c71-207">In order to enable Azure Active Directory users to log in to New Relic, they must be provisioned into New Relic.</span></span> <span data-ttu-id="b8c71-208">В случае New Relic подготовка пользователей осуществляется вручную.</span><span class="sxs-lookup"><span data-stu-id="b8c71-208">In the case of New Relic, provisioning is a manual task.</span></span>

<span data-ttu-id="b8c71-209">**Чтобы подготовить учетные записи пользователей для New Relic, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="b8c71-209">**To provision a user account to New Relic, perform the following steps:**</span></span>

1. <span data-ttu-id="b8c71-210">Выполните вход на веб-сайт **New Relic** компании в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="b8c71-210">Log in to your **New Relic** company site as administrator.</span></span>

2. <span data-ttu-id="b8c71-211">В меню в верхней части страницы щелкните **Параметры учетной записи**.</span><span class="sxs-lookup"><span data-stu-id="b8c71-211">In the menu on the top, click **Account Settings**.</span></span>
   
    <span data-ttu-id="b8c71-212">![Параметры учетной записи](./media/active-directory-saas-new-relic-tutorial/ic797040.png "параметры учетной записи")</span><span class="sxs-lookup"><span data-stu-id="b8c71-212">![Account Settings](./media/active-directory-saas-new-relic-tutorial/ic797040.png "Account Settings")</span></span>

3. <span data-ttu-id="b8c71-213">В области **Account** (Учетная запись) слева щелкните **Summary** (Сводка) и нажмите кнопку **Add user** (Добавить пользователя).</span><span class="sxs-lookup"><span data-stu-id="b8c71-213">In the **Account** pane on the left side, click **Summary**, and then click **Add user**.</span></span>
   
    <span data-ttu-id="b8c71-214">![Параметры учетной записи](./media/active-directory-saas-new-relic-tutorial/ic797041.png "параметры учетной записи")</span><span class="sxs-lookup"><span data-stu-id="b8c71-214">![Account Settings](./media/active-directory-saas-new-relic-tutorial/ic797041.png "Account Settings")</span></span>

4. <span data-ttu-id="b8c71-215">В диалоговом окне **Активные пользователи** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="b8c71-215">On the **Active users** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="b8c71-216">![Активные пользователи](./media/active-directory-saas-new-relic-tutorial/ic797042.png "Активные пользователи")</span><span class="sxs-lookup"><span data-stu-id="b8c71-216">![Active Users](./media/active-directory-saas-new-relic-tutorial/ic797042.png "Active Users")</span></span>
   
    <span data-ttu-id="b8c71-217">а.</span><span class="sxs-lookup"><span data-stu-id="b8c71-217">a.</span></span> <span data-ttu-id="b8c71-218">В текстовом поле **Электронная почта** введите электронный адрес действующего пользователя Azure Active Directory, которого вы хотите подготовить.</span><span class="sxs-lookup"><span data-stu-id="b8c71-218">In the **Email** textbox, type the email address of a valid Azure Active Directory user you want to provision.</span></span>

    <span data-ttu-id="b8c71-219">b.</span><span class="sxs-lookup"><span data-stu-id="b8c71-219">b.</span></span> <span data-ttu-id="b8c71-220">Для параметра **Role** (Роль) выберите значение **User** (Пользователь).</span><span class="sxs-lookup"><span data-stu-id="b8c71-220">As **Role** select **User**.</span></span>

    <span data-ttu-id="b8c71-221">c.</span><span class="sxs-lookup"><span data-stu-id="b8c71-221">c.</span></span> <span data-ttu-id="b8c71-222">Щелкните **Добавить этого пользователя**.</span><span class="sxs-lookup"><span data-stu-id="b8c71-222">Click **Add this user**.</span></span>

>[!NOTE]
><span data-ttu-id="b8c71-223">Вы можете использовать любые другие инструменты создания учетных записей пользователя New Relic или API, предоставляемые New Relic для подготовки учетных записей пользователя AAD.</span><span class="sxs-lookup"><span data-stu-id="b8c71-223">You can use any other New Relic user account creation tools or APIs provided by New Relic to provision AAD user accounts.</span></span>
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b8c71-224">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="b8c71-224">Assigning the Azure AD test user</span></span>

<span data-ttu-id="b8c71-225">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure путем предоставления доступа к New Relic.</span><span class="sxs-lookup"><span data-stu-id="b8c71-225">In this section, you enable Britta Simon to use Azure single sign-on by granting access to New Relic.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="b8c71-227">**Чтобы назначить пользователя Britta Simon в New Relic, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="b8c71-227">**To assign Britta Simon to New Relic, perform the following steps:**</span></span>

1. <span data-ttu-id="b8c71-228">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="b8c71-228">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="b8c71-230">В списке приложений выберите **New Relic**.</span><span class="sxs-lookup"><span data-stu-id="b8c71-230">In the applications list, select **New Relic**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-new-relic-tutorial/tutorial_newrelic_app.png) 

3. <span data-ttu-id="b8c71-232">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="b8c71-232">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="b8c71-234">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="b8c71-234">Click **Add** button.</span></span> <span data-ttu-id="b8c71-235">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="b8c71-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="b8c71-237">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="b8c71-237">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b8c71-238">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="b8c71-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b8c71-239">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="b8c71-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b8c71-240">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="b8c71-240">Testing single sign-on</span></span>

<span data-ttu-id="b8c71-241">Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="b8c71-241">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b8c71-242">Щелкнув элемент New Relic на панели доступа, вы автоматически войдете в приложение New Relic.</span><span class="sxs-lookup"><span data-stu-id="b8c71-242">When you click the New Relic tile in the Access Panel, you should get automatically signed-on to your New Relic application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b8c71-243">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="b8c71-243">Additional resources</span></span>

* [<span data-ttu-id="b8c71-244">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b8c71-244">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b8c71-245">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b8c71-245">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-new-relic-tutorial/tutorial_general_203.png

