---
title: "Учебник. Интеграция Azure Active Directory с Freshservice | Документы Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в Freshservice."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3dd22b1f-445d-45c6-8eda-30207eb9a1a8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: d32775fa91d3a49da1ef55e57d1d38990fa09346
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-freshservice"></a><span data-ttu-id="e8331-103">Учебник. Интеграция Azure Active Directory с FreshService</span><span class="sxs-lookup"><span data-stu-id="e8331-103">Tutorial: Azure Active Directory integration with Freshservice</span></span>

<span data-ttu-id="e8331-104">В этом учебнике описано, как интегрировать Freshservice с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e8331-104">In this tutorial, you learn how to integrate Freshservice with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e8331-105">Интеграция Azure AD с приложением Freshservice обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="e8331-105">Integrating Freshservice with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e8331-106">С помощью Azure AD вы можете контролировать доступ к Freshservice.</span><span class="sxs-lookup"><span data-stu-id="e8331-106">You can control in Azure AD who has access to Freshservice</span></span>
- <span data-ttu-id="e8331-107">Вы можете включить автоматический вход пользователей в Freshservice (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e8331-107">You can enable your users to automatically get signed-on to Freshservice (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e8331-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="e8331-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e8331-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e8331-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e8331-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="e8331-110">Prerequisites</span></span>

<span data-ttu-id="e8331-111">Чтобы настроить интеграцию Azure AD с Freshservice, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="e8331-111">To configure Azure AD integration with Freshservice, you need the following items:</span></span>

- <span data-ttu-id="e8331-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="e8331-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e8331-113">подписка Freshservice с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="e8331-113">A Freshservice single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e8331-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="e8331-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e8331-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="e8331-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e8331-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="e8331-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e8331-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e8331-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e8331-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="e8331-118">Scenario description</span></span>
<span data-ttu-id="e8331-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="e8331-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e8331-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="e8331-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e8331-121">Добавление Freshservice из коллекции</span><span class="sxs-lookup"><span data-stu-id="e8331-121">Adding Freshservice from the gallery</span></span>
2. <span data-ttu-id="e8331-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="e8331-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-freshservice-from-the-gallery"></a><span data-ttu-id="e8331-123">Добавление Freshservice из коллекции</span><span class="sxs-lookup"><span data-stu-id="e8331-123">Adding Freshservice from the gallery</span></span>
<span data-ttu-id="e8331-124">Чтобы настроить интеграцию Freshservice с Azure AD, необходимо добавить Freshservice из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="e8331-124">To configure the integration of Freshservice into Azure AD, you need to add Freshservice from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e8331-125">**Чтобы добавить Freshservice из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="e8331-125">**To add Freshservice from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e8331-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e8331-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e8331-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="e8331-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e8331-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="e8331-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="e8331-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="e8331-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="e8331-133">В поле поиска введите **Freshservice**.</span><span class="sxs-lookup"><span data-stu-id="e8331-133">In the search box, type **Freshservice**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_search.png)

5. <span data-ttu-id="e8331-135">На панели результатов выберите **Freshservice** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="e8331-135">In the results panel, select **Freshservice**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e8331-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="e8331-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e8331-138">В этом разделе описана настройка и проверка единого входа Azure AD во Freshservice с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e8331-138">In this section, you configure and test Azure AD single sign-on with Freshservice based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="e8331-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь во Freshservice соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e8331-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Freshservice is to a user in Azure AD.</span></span> <span data-ttu-id="e8331-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем во Freshservice.</span><span class="sxs-lookup"><span data-stu-id="e8331-140">In other words, a link relationship between an Azure AD user and the related user in Freshservice needs to be established.</span></span>

<span data-ttu-id="e8331-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** во Freshservice.</span><span class="sxs-lookup"><span data-stu-id="e8331-141">In Freshservice, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="e8331-142">Чтобы настроить и проверить единый вход Azure AD во Freshservice, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="e8331-142">To configure and test Azure AD single sign-on with Freshservice, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e8331-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="e8331-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e8331-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e8331-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e8331-145">**[Создание тестового пользователя Freshservice](#creating-a-freshservice-test-user)** требуется для создания в Freshservice пользователя Britta Simon, связанного с представлением этого пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e8331-145">**[Creating a Freshservice test user](#creating-a-freshservice-test-user)** - to have a counterpart of Britta Simon in Freshservice that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e8331-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e8331-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e8331-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="e8331-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e8331-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="e8331-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e8331-149">В данном разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Freshservice.</span><span class="sxs-lookup"><span data-stu-id="e8331-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Freshservice application.</span></span>

<span data-ttu-id="e8331-150">**Чтобы настроить единый вход Azure AD во Freshservice, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="e8331-150">**To configure Azure AD single sign-on with Freshservice, perform the following steps:**</span></span>

1. <span data-ttu-id="e8331-151">На портале Azure на странице интеграции с приложением **Freshservice** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="e8331-151">In the Azure portal, on the **Freshservice** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="e8331-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="e8331-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_samlbase.png)

3. <span data-ttu-id="e8331-155">В разделе **Домены и URL-адреса приложения Freshservice** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="e8331-155">On the **Freshservice Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_url.png)

    <span data-ttu-id="e8331-157">а.</span><span class="sxs-lookup"><span data-stu-id="e8331-157">a.</span></span> <span data-ttu-id="e8331-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<democompany>.freshservice.com`</span><span class="sxs-lookup"><span data-stu-id="e8331-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<democompany>.freshservice.com`</span></span>

    <span data-ttu-id="e8331-159">b.</span><span class="sxs-lookup"><span data-stu-id="e8331-159">b.</span></span> <span data-ttu-id="e8331-160">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<democompany>.freshservice.com`</span><span class="sxs-lookup"><span data-stu-id="e8331-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<democompany>.freshservice.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e8331-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="e8331-161">These values are not real.</span></span> <span data-ttu-id="e8331-162">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="e8331-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="e8331-163">Чтобы получить их, обратитесь в [службу поддержки клиентов Freshservice](https://support.freshservice.com/).</span><span class="sxs-lookup"><span data-stu-id="e8331-163">Contact [Freshservice Client support team](https://support.freshservice.com/) to get these values.</span></span> 
 
4. <span data-ttu-id="e8331-164">В разделе **Сертификат подписи SAML** скопируйте значение **отпечатка** сертификата.</span><span class="sxs-lookup"><span data-stu-id="e8331-164">On the **SAML Signing Certificate** section, copy **THUMBPRINT** value of certificate.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_certificate.png) 

5. <span data-ttu-id="e8331-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="e8331-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-freshservice-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e8331-168">В разделе **Конфигурация Freshservice** щелкните **Настроить Freshservice**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="e8331-168">On the **Freshservice Configuration** section, click **Configure Freshservice** to open **Configure sign-on** window.</span></span> <span data-ttu-id="e8331-169">Скопируйте **URL-адрес выхода и URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="e8331-169">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_configure.png) 

7. <span data-ttu-id="e8331-171">В другом окне веб-браузера войдите на свой корпоративный веб-сайт Freshservice в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="e8331-171">In a different web browser window, log in to your Freshservice company site as an administrator.</span></span>

8. <span data-ttu-id="e8331-172">В верхнем меню щелкните **Администратор**.</span><span class="sxs-lookup"><span data-stu-id="e8331-172">In the menu on the top, click **Admin**.</span></span>
   
    <span data-ttu-id="e8331-173">![Администратор](./media/active-directory-saas-freshservice-tutorial/ic790814.png "Администратор")</span><span class="sxs-lookup"><span data-stu-id="e8331-173">![Admin](./media/active-directory-saas-freshservice-tutorial/ic790814.png "Admin")</span></span>

9. <span data-ttu-id="e8331-174">В области **Customer Portal** (Клиентский портал) выберите **Security** (Безопасность).</span><span class="sxs-lookup"><span data-stu-id="e8331-174">In the **Customer Portal**, click **Security**.</span></span>
   
    <span data-ttu-id="e8331-175">![Безопасность](./media/active-directory-saas-freshservice-tutorial/ic790815.png "Безопасность")</span><span class="sxs-lookup"><span data-stu-id="e8331-175">![Security](./media/active-directory-saas-freshservice-tutorial/ic790815.png "Security")</span></span>

10. <span data-ttu-id="e8331-176">В разделе **Security** (Безопасность) выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="e8331-176">In the **Security** section, perform the following steps:</span></span>
   
    <span data-ttu-id="e8331-177">![Единый вход](./media/active-directory-saas-freshservice-tutorial/ic790816.png "Единый вход")</span><span class="sxs-lookup"><span data-stu-id="e8331-177">![Single Sign On](./media/active-directory-saas-freshservice-tutorial/ic790816.png "Single Sign On")</span></span>
   
    <span data-ttu-id="e8331-178">а.</span><span class="sxs-lookup"><span data-stu-id="e8331-178">a.</span></span> <span data-ttu-id="e8331-179">Включите **единый вход**.</span><span class="sxs-lookup"><span data-stu-id="e8331-179">Switch **Single Sign On**.</span></span>

    <span data-ttu-id="e8331-180">b.</span><span class="sxs-lookup"><span data-stu-id="e8331-180">b.</span></span> <span data-ttu-id="e8331-181">Выберите **Единый вход SAML**.</span><span class="sxs-lookup"><span data-stu-id="e8331-181">Select **SAML SSO**.</span></span>

    <span data-ttu-id="e8331-182">c.</span><span class="sxs-lookup"><span data-stu-id="e8331-182">c.</span></span> <span data-ttu-id="e8331-183">В текстовое поле **URL-адрес входа SAML** вставьте значение **URL-адреса службы единого входа SAML**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="e8331-183">In the **SAML Login URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="e8331-184">г)</span><span class="sxs-lookup"><span data-stu-id="e8331-184">d.</span></span> <span data-ttu-id="e8331-185">В текстовое поле **URL-адрес выхода SAML** вставьте значение **URL-адреса выхода**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="e8331-185">In the **Logout URL** textbox, paste the value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="e8331-186">д.</span><span class="sxs-lookup"><span data-stu-id="e8331-186">e.</span></span> <span data-ttu-id="e8331-187">В текстовое поле **Отпечаток сертификата безопасности** вставьте значение **ОТПЕЧАТОК** сертификата, которое вы скопировали на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="e8331-187">In **Security Certificate Fingerprint** textbox, paste the **THUMBPRINT** value of certificate which you have copied from Azure portal.</span></span>

    <span data-ttu-id="e8331-188">Е.</span><span class="sxs-lookup"><span data-stu-id="e8331-188">f.</span></span> <span data-ttu-id="e8331-189">Нажмите кнопку **Сохранить**</span><span class="sxs-lookup"><span data-stu-id="e8331-189">Click **Save**</span></span>
   
> [!TIP]
> <span data-ttu-id="e8331-190">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="e8331-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e8331-191">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="e8331-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e8331-192">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="e8331-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e8331-193">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="e8331-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="e8331-194">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e8331-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="e8331-196">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="e8331-196">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e8331-197">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e8331-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-freshservice-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e8331-199">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="e8331-199">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-freshservice-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e8331-201">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="e8331-201">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-freshservice-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e8331-203">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="e8331-203">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-freshservice-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e8331-205">а.</span><span class="sxs-lookup"><span data-stu-id="e8331-205">a.</span></span> <span data-ttu-id="e8331-206">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e8331-206">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e8331-207">b.</span><span class="sxs-lookup"><span data-stu-id="e8331-207">b.</span></span> <span data-ttu-id="e8331-208">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e8331-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e8331-209">c.</span><span class="sxs-lookup"><span data-stu-id="e8331-209">c.</span></span> <span data-ttu-id="e8331-210">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="e8331-210">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e8331-211">d.</span><span class="sxs-lookup"><span data-stu-id="e8331-211">d.</span></span> <span data-ttu-id="e8331-212">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="e8331-212">Click **Create**.</span></span>
 
### <a name="creating-a-freshservice-test-user"></a><span data-ttu-id="e8331-213">Создание тестового пользователя Freshservice</span><span class="sxs-lookup"><span data-stu-id="e8331-213">Creating a Freshservice test user</span></span>

<span data-ttu-id="e8331-214">Чтобы пользователи Azure AD могли выполнять вход во Freshservice, они должны быть подготовлены для Freshservice.</span><span class="sxs-lookup"><span data-stu-id="e8331-214">To enable Azure AD users to log in to FreshService, they must be provisioned into FreshService.</span></span> <span data-ttu-id="e8331-215">В случае с FreshService подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="e8331-215">In the case of FreshService, provisioning is a manual task.</span></span>

<span data-ttu-id="e8331-216">**Чтобы подготовить учетную запись пользователя, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="e8331-216">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="e8331-217">Выполните вход на корпоративный сайт **FreshService** в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="e8331-217">Log in to your **FreshService** company site as an administrator.</span></span>

2. <span data-ttu-id="e8331-218">В верхнем меню щелкните **Администратор**.</span><span class="sxs-lookup"><span data-stu-id="e8331-218">In the menu on the top, click **Admin**.</span></span>
   
    <span data-ttu-id="e8331-219">![Администратор](./media/active-directory-saas-freshservice-tutorial/ic790814.png "Администратор")</span><span class="sxs-lookup"><span data-stu-id="e8331-219">![Admin](./media/active-directory-saas-freshservice-tutorial/ic790814.png "Admin")</span></span>

3. <span data-ttu-id="e8331-220">В разделе **User Management** (Управление пользователями) выберите **Requesters** (Инициаторы запроса).</span><span class="sxs-lookup"><span data-stu-id="e8331-220">In the **User Management** section, click **Requesters**.</span></span>
   
    <span data-ttu-id="e8331-221">![Инициатор запроса](./media/active-directory-saas-freshservice-tutorial/ic790818.png "Инициатор запроса")</span><span class="sxs-lookup"><span data-stu-id="e8331-221">![Requesters](./media/active-directory-saas-freshservice-tutorial/ic790818.png "Requesters")</span></span>

4. <span data-ttu-id="e8331-222">Нажмите **Новый инициатор запроса**.</span><span class="sxs-lookup"><span data-stu-id="e8331-222">Click **New Requester**.</span></span>
   
    <span data-ttu-id="e8331-223">![Создание инициаторов запроса](./media/active-directory-saas-freshservice-tutorial/ic790819.png "Создание инициаторов запроса")</span><span class="sxs-lookup"><span data-stu-id="e8331-223">![New Requesters](./media/active-directory-saas-freshservice-tutorial/ic790819.png "New Requesters")</span></span>

5. <span data-ttu-id="e8331-224">В разделе **Новый инициатор запроса** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="e8331-224">In the **New Requester** section, perform the following steps:</span></span>
   
    <span data-ttu-id="e8331-225">![Создание инициатора запроса](./media/active-directory-saas-freshservice-tutorial/ic790820.png "Создание инициатора запроса")</span><span class="sxs-lookup"><span data-stu-id="e8331-225">![New Requester](./media/active-directory-saas-freshservice-tutorial/ic790820.png "New Requester")</span></span>   

    <span data-ttu-id="e8331-226">а.</span><span class="sxs-lookup"><span data-stu-id="e8331-226">a.</span></span> <span data-ttu-id="e8331-227">В соответствующие текстовые поля введите атрибуты **First name** (Имя) и **Email** (Адрес электронной почты) действующей учетной записи Azure Active Directory, которую вы хотите подготовить.</span><span class="sxs-lookup"><span data-stu-id="e8331-227">Enter the **First Name** and **Email** attributes of a valid Azure Active Directory account you want to provision into the related textboxes.</span></span>

    <span data-ttu-id="e8331-228">b.</span><span class="sxs-lookup"><span data-stu-id="e8331-228">b.</span></span> <span data-ttu-id="e8331-229">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="e8331-229">Click **Save**.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="e8331-230">Владелец учетной записи Azure Active Directory получит электронное сообщение со ссылкой для подтверждения учетной записи перед ее активацией.</span><span class="sxs-lookup"><span data-stu-id="e8331-230">The Azure Active Directory account holder gets an email including a link to confirm the account before it becomes active</span></span>
    >  

>[!NOTE]
><span data-ttu-id="e8331-231">Вы можете использовать любые другие инструменты создания учетных записей пользователя FreshService или API, предоставляемые FreshService для подготовки учетных записей пользователя AAD.</span><span class="sxs-lookup"><span data-stu-id="e8331-231">You can use any other FreshService user account creation tools or APIs provided by FreshService to provision AAD user accounts.</span></span>
>  

![Назначение пользователя][200] 

<span data-ttu-id="e8331-233">**Чтобы назначить пользователя Britta Simon во Freshservice, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="e8331-233">**To assign Britta Simon to Freshservice, perform the following steps:**</span></span>

1. <span data-ttu-id="e8331-234">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="e8331-234">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="e8331-236">В списке приложений выберите **Freshservice**.</span><span class="sxs-lookup"><span data-stu-id="e8331-236">In the applications list, select **Freshservice**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-freshservice-tutorial/tutorial_freshservice_app.png) 

3. <span data-ttu-id="e8331-238">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="e8331-238">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="e8331-240">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="e8331-240">Click **Add** button.</span></span> <span data-ttu-id="e8331-241">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="e8331-241">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="e8331-243">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="e8331-243">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e8331-244">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="e8331-244">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e8331-245">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="e8331-245">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e8331-246">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="e8331-246">Testing single sign-on</span></span>

<span data-ttu-id="e8331-247">Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="e8331-247">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="e8331-248">Щелкнув плитку Freshservice на панели доступа, вы автоматически войдете в приложение Freshservice.</span><span class="sxs-lookup"><span data-stu-id="e8331-248">When you click the Freshservice tile in the Access Panel, you should get automatically signed-on to your Freshservice application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e8331-249">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="e8331-249">Additional resources</span></span>

* [<span data-ttu-id="e8331-250">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e8331-250">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e8331-251">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e8331-251">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-freshservice-tutorial/tutorial_general_203.png

