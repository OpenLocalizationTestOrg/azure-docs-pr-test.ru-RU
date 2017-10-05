---
title: "Руководство по интеграции Azure Active Directory с Panorama9 | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в приложении Panorama9."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5e28d7fa-03be-49f3-96c8-b567f1257d44
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: 934c0743464fd32398071aa3d07f7af76fdf7e3b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-panorama9"></a><span data-ttu-id="01f8b-103">Учебник. Интеграция Azure Active Directory с Panorama9</span><span class="sxs-lookup"><span data-stu-id="01f8b-103">Tutorial: Azure Active Directory integration with Panorama9</span></span>

<span data-ttu-id="01f8b-104">В этом руководстве описано, как интегрировать Panorama9 с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="01f8b-104">In this tutorial, you learn how to integrate Panorama9 with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="01f8b-105">Интеграция Azure AD с приложением Panorama9 обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="01f8b-105">Integrating Panorama9 with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="01f8b-106">С помощью Azure AD вы можете контролировать доступ к Panorama9.</span><span class="sxs-lookup"><span data-stu-id="01f8b-106">You can control in Azure AD who has access to Panorama9</span></span>
- <span data-ttu-id="01f8b-107">Вы можете включить автоматический вход пользователей в Panorama9 (единый вход) с использованием учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="01f8b-107">You can enable your users to automatically get signed-on to Panorama9 (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="01f8b-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="01f8b-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="01f8b-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="01f8b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="01f8b-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="01f8b-110">Prerequisites</span></span>

<span data-ttu-id="01f8b-111">Чтобы настроить интеграцию Azure AD с Panorama9, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="01f8b-111">To configure Azure AD integration with Panorama9, you need the following items:</span></span>

- <span data-ttu-id="01f8b-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="01f8b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="01f8b-113">Подписка с поддержкой единого входа Panorama9.</span><span class="sxs-lookup"><span data-stu-id="01f8b-113">A Panorama9 single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="01f8b-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="01f8b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="01f8b-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="01f8b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="01f8b-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="01f8b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="01f8b-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="01f8b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="01f8b-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="01f8b-118">Scenario description</span></span>
<span data-ttu-id="01f8b-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="01f8b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="01f8b-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="01f8b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="01f8b-121">Добавление Panorama9 из коллекции.</span><span class="sxs-lookup"><span data-stu-id="01f8b-121">Adding Panorama9 from the gallery</span></span>
2. <span data-ttu-id="01f8b-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="01f8b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-panorama9-from-the-gallery"></a><span data-ttu-id="01f8b-123">Добавление Panorama9 из коллекции</span><span class="sxs-lookup"><span data-stu-id="01f8b-123">Adding Panorama9 from the gallery</span></span>
<span data-ttu-id="01f8b-124">Чтобы настроить интеграцию Panorama9 с Azure AD, необходимо добавить Panorama9 из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="01f8b-124">To configure the integration of Panorama9 into Azure AD, you need to add Panorama9 from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="01f8b-125">**Чтобы добавить Panorama9 из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="01f8b-125">**To add Panorama9 from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="01f8b-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="01f8b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="01f8b-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="01f8b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="01f8b-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="01f8b-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="01f8b-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="01f8b-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="01f8b-133">В поле поиска введите **Panorama9**.</span><span class="sxs-lookup"><span data-stu-id="01f8b-133">In the search box, type **Panorama9**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_search.png)

5. <span data-ttu-id="01f8b-135">На панели результатов выберите **Panorama9** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="01f8b-135">In the results panel, select **Panorama9**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="01f8b-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="01f8b-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="01f8b-138">В этом разделе описана настройка и проверка единого входа Azure AD в Panorama9 с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="01f8b-138">In this section, you configure and test Azure AD single sign-on with Panorama9 based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="01f8b-139">Чтобы единый вход работал, Azure AD необходима информация о том, какой пользователь в Panorama9 соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="01f8b-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Panorama9 is to a user in Azure AD.</span></span> <span data-ttu-id="01f8b-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Panorama9.</span><span class="sxs-lookup"><span data-stu-id="01f8b-140">In other words, a link relationship between an Azure AD user and the related user in Panorama9 needs to be established.</span></span>

<span data-ttu-id="01f8b-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Panorama9.</span><span class="sxs-lookup"><span data-stu-id="01f8b-141">In Panorama9, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="01f8b-142">Чтобы настроить и проверить единый вход Azure AD в Panorama9, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="01f8b-142">To configure and test Azure AD single sign-on with Panorama9, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="01f8b-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="01f8b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="01f8b-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="01f8b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="01f8b-145">**[Создание тестового пользователя Panorama9](#creating-a-panorama9-test-user)** требуется для того, чтобы в Panorama9 существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="01f8b-145">**[Creating a Panorama9 test user](#creating-a-panorama9-test-user)** - to have a counterpart of Britta Simon in Panorama9 that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="01f8b-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="01f8b-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="01f8b-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="01f8b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="01f8b-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="01f8b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="01f8b-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Panorama9.</span><span class="sxs-lookup"><span data-stu-id="01f8b-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Panorama9 application.</span></span>

<span data-ttu-id="01f8b-150">**Чтобы настроить единый вход Azure AD в Panorama9, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="01f8b-150">**To configure Azure AD single sign-on with Panorama9, perform the following steps:**</span></span>

1. <span data-ttu-id="01f8b-151">На портале Azure на странице интеграции с приложением **Panorama9** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="01f8b-151">In the Azure portal, on the **Panorama9** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="01f8b-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="01f8b-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_samlbase.png)

3. <span data-ttu-id="01f8b-155">В разделе **Домены и URL-адреса приложения Panorama9** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="01f8b-155">On the **Panorama9 Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_url.png)

    <span data-ttu-id="01f8b-157">а.</span><span class="sxs-lookup"><span data-stu-id="01f8b-157">a.</span></span> <span data-ttu-id="01f8b-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в формате `https://dashboard.panorama9.com/saml/access/3262`.</span><span class="sxs-lookup"><span data-stu-id="01f8b-158">In the **Sign-on URL** textbox, type a URL as: `https://dashboard.panorama9.com/saml/access/3262`</span></span>

    <span data-ttu-id="01f8b-159">b.</span><span class="sxs-lookup"><span data-stu-id="01f8b-159">b.</span></span> <span data-ttu-id="01f8b-160">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `http://www.panorama9.com/saml20/<tenant-name>`</span><span class="sxs-lookup"><span data-stu-id="01f8b-160">In the **Identifier** textbox, type a URL using the following pattern: `http://www.panorama9.com/saml20/<tenant-name>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="01f8b-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="01f8b-161">These values are not real.</span></span> <span data-ttu-id="01f8b-162">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="01f8b-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="01f8b-163">Чтобы получить эти значения, обратитесь к [группе поддержки клиентов Panorama9](https://support.panorama9.com).</span><span class="sxs-lookup"><span data-stu-id="01f8b-163">Contact [Panorama9 Client support team](https://support.panorama9.com) to get these values.</span></span> 
 
4. <span data-ttu-id="01f8b-164">В разделе **Сертификат подписи SAML** скопируйте значение **Отпечаток**.</span><span class="sxs-lookup"><span data-stu-id="01f8b-164">On the **SAML Signing Certificate** section, copy the **THUMBPRINT** value of certificate.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_certificate.png) 

5. <span data-ttu-id="01f8b-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="01f8b-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-panorama9-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="01f8b-168">В разделе **Конфигурация Panorama9** щелкните **Настроить Panorama9**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="01f8b-168">On the **Panorama9 Configuration** section, click **Configure Panorama9** to open **Configure sign-on** window.</span></span> <span data-ttu-id="01f8b-169">Скопируйте **URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="01f8b-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_configure.png) 

5. <span data-ttu-id="01f8b-171">В другом окне веб-браузера войдите на сайт Panorama9 своей компании в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="01f8b-171">In a different web browser window, log into your Panorama9 company site as an administrator.</span></span>

6. <span data-ttu-id="01f8b-172">На панели инструментов вверху щелкните **Manage** (Управление), затем щелкните **Extensions** (Расширения).</span><span class="sxs-lookup"><span data-stu-id="01f8b-172">In the toolbar on the top, click **Manage**, and then click **Extensions**.</span></span>
   
   <span data-ttu-id="01f8b-173">![Расширения](./media/active-directory-saas-panorama9-tutorial/ic790023.png "Расширения")</span><span class="sxs-lookup"><span data-stu-id="01f8b-173">![Extensions](./media/active-directory-saas-panorama9-tutorial/ic790023.png "Extensions")</span></span>
7. <span data-ttu-id="01f8b-174">В диалоговом окне **Extensions** (Расширения) щелкните **Single Sign-On** (Единый вход).</span><span class="sxs-lookup"><span data-stu-id="01f8b-174">On the **Extensions** dialog, click **Single Sign-On**.</span></span>
   
   <span data-ttu-id="01f8b-175">![Единый вход](./media/active-directory-saas-panorama9-tutorial/ic790024.png "Единый вход")</span><span class="sxs-lookup"><span data-stu-id="01f8b-175">![Single Sign-On](./media/active-directory-saas-panorama9-tutorial/ic790024.png "Single Sign-On")</span></span>
8. <span data-ttu-id="01f8b-176">В разделе **Параметры** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="01f8b-176">In the **Settings** section, perform the following steps:</span></span>
   
   <span data-ttu-id="01f8b-177">![Параметры](./media/active-directory-saas-panorama9-tutorial/ic790025.png "Параметры")</span><span class="sxs-lookup"><span data-stu-id="01f8b-177">![Settings](./media/active-directory-saas-panorama9-tutorial/ic790025.png "Settings")</span></span>
   
    <span data-ttu-id="01f8b-178">а.</span><span class="sxs-lookup"><span data-stu-id="01f8b-178">a.</span></span> <span data-ttu-id="01f8b-179">В текстовое поле **Identity provider URL** (URL-адрес поставщика удостоверений) вставьте значение **URL-адрес службы единого входа**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="01f8b-179">In **Identity provider URL** textbox, paste the value of **Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
   
    <span data-ttu-id="01f8b-180">b.</span><span class="sxs-lookup"><span data-stu-id="01f8b-180">b.</span></span> <span data-ttu-id="01f8b-181">В текстовое поле **Certificate fingerprint** (Отпечаток сертификата) вставьте значение **Отпечаток**, которое вы скопировали на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="01f8b-181">In **Certificate fingerprint** textbox, paste the **Thumbprint** value of certificate, which you have copied from Azure portal.</span></span>    
         
9. <span data-ttu-id="01f8b-182">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="01f8b-182">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="01f8b-183">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="01f8b-183">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="01f8b-184">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="01f8b-184">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="01f8b-185">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="01f8b-185">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="01f8b-186">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="01f8b-186">Creating an Azure AD test user</span></span>
<span data-ttu-id="01f8b-187">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="01f8b-187">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="01f8b-189">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="01f8b-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="01f8b-190">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="01f8b-190">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-panorama9-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="01f8b-192">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="01f8b-192">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-panorama9-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="01f8b-194">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="01f8b-194">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-panorama9-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="01f8b-196">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="01f8b-196">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-panorama9-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="01f8b-198">а.</span><span class="sxs-lookup"><span data-stu-id="01f8b-198">a.</span></span> <span data-ttu-id="01f8b-199">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="01f8b-199">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="01f8b-200">b.</span><span class="sxs-lookup"><span data-stu-id="01f8b-200">b.</span></span> <span data-ttu-id="01f8b-201">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="01f8b-201">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="01f8b-202">c.</span><span class="sxs-lookup"><span data-stu-id="01f8b-202">c.</span></span> <span data-ttu-id="01f8b-203">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="01f8b-203">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="01f8b-204">d.</span><span class="sxs-lookup"><span data-stu-id="01f8b-204">d.</span></span> <span data-ttu-id="01f8b-205">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="01f8b-205">Click **Create**.</span></span>
 
### <a name="creating-a-panorama9-test-user"></a><span data-ttu-id="01f8b-206">Создание тестового пользователя Panorama9</span><span class="sxs-lookup"><span data-stu-id="01f8b-206">Creating a Panorama9 test user</span></span>

<span data-ttu-id="01f8b-207">Чтобы пользователи Azure AD могли выполнять вход в Panorama9, они должны быть подготовлены для Panorama9.</span><span class="sxs-lookup"><span data-stu-id="01f8b-207">In order to enable Azure AD users to log into Panorama9, they must be provisioned into Panorama9.</span></span>  

<span data-ttu-id="01f8b-208">В случае с Panorama9 подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="01f8b-208">In the case of Panorama9, provisioning is a manual task.</span></span>

<span data-ttu-id="01f8b-209">**Чтобы настроить подготовку учетных записей пользователей, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="01f8b-209">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="01f8b-210">Выполните вход на сайт компании **Panorama9** в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="01f8b-210">Log in to your **Panorama9** company site as an administrator.</span></span>

2. <span data-ttu-id="01f8b-211">На панели инструментов вверху нажмите **Manage** (Управление), а затем **Users** (Пользователи).</span><span class="sxs-lookup"><span data-stu-id="01f8b-211">In the menu on the top, click **Manage**, and then click **Users**.</span></span>
   
  <span data-ttu-id="01f8b-212">![Пользователи](./media/active-directory-saas-panorama9-tutorial/ic790027.png "Пользователи")</span><span class="sxs-lookup"><span data-stu-id="01f8b-212">![Users](./media/active-directory-saas-panorama9-tutorial/ic790027.png "Users")</span></span>

3. <span data-ttu-id="01f8b-213">В разделе "Users" (Пользователи) щелкните **+**, чтобы добавить нового пользователя.</span><span class="sxs-lookup"><span data-stu-id="01f8b-213">In the Users section, Click **+** to add new user.</span></span>

 <span data-ttu-id="01f8b-214">![Пользователи](./media/active-directory-saas-panorama9-tutorial/ic790028.png "Пользователи")</span><span class="sxs-lookup"><span data-stu-id="01f8b-214">![Users](./media/active-directory-saas-panorama9-tutorial/ic790028.png "Users")</span></span>

4. <span data-ttu-id="01f8b-215">Перейдите в раздел "User data" (Данные пользователя) и в текстовое поле **Email** (Электронная почта) введите электронный адрес действительного пользователя Azure Active Directory, которого вы хотите подготовить.</span><span class="sxs-lookup"><span data-stu-id="01f8b-215">Go to the User data section, type the email address of a valid Azure Active Directory user you want to provision into the **Email** textbox.</span></span>

5. <span data-ttu-id="01f8b-216">Перейдите в раздел "Users" (Пользователи) и нажмите кнопку **Save** (Сохранить).</span><span class="sxs-lookup"><span data-stu-id="01f8b-216">Come to the Users section, Click **Save**.</span></span>
   
> [!NOTE]
    > <span data-ttu-id="01f8b-217">Владелец учетной записи Azure Active Directory получит по электронной почте сообщение со ссылкой для активации учетной записи.</span><span class="sxs-lookup"><span data-stu-id="01f8b-217">The Azure Active Directory account holder receives an email and follows a link to confirm their account before it becomes active.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="01f8b-218">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="01f8b-218">Assigning the Azure AD test user</span></span>

<span data-ttu-id="01f8b-219">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к Panorama9.</span><span class="sxs-lookup"><span data-stu-id="01f8b-219">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Panorama9.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="01f8b-221">**Чтобы назначить пользователя Britta Simon в Panorama9, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="01f8b-221">**To assign Britta Simon to Panorama9, perform the following steps:**</span></span>

1. <span data-ttu-id="01f8b-222">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="01f8b-222">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="01f8b-224">Из списка приложений выберите **Panorama9**.</span><span class="sxs-lookup"><span data-stu-id="01f8b-224">In the applications list, select **Panorama9**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-panorama9-tutorial/tutorial_panorama9_app.png) 

3. <span data-ttu-id="01f8b-226">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="01f8b-226">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="01f8b-228">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="01f8b-228">Click **Add** button.</span></span> <span data-ttu-id="01f8b-229">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="01f8b-229">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="01f8b-231">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="01f8b-231">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="01f8b-232">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="01f8b-232">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="01f8b-233">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="01f8b-233">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="01f8b-234">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="01f8b-234">Testing single sign-on</span></span>

<span data-ttu-id="01f8b-235">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="01f8b-235">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="01f8b-236">Щелкнув элемент "Panorama9" на панели доступа, вы автоматически войдете в приложение Panorama9.</span><span class="sxs-lookup"><span data-stu-id="01f8b-236">When you click the Panorama9 tile in the Access Panel, you should get automatically signed-on to Panorama9 application.</span></span>
<span data-ttu-id="01f8b-237">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="01f8b-237">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="01f8b-238">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="01f8b-238">Additional resources</span></span>

* [<span data-ttu-id="01f8b-239">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="01f8b-239">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="01f8b-240">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="01f8b-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-panorama9-tutorial/tutorial_general_203.png

