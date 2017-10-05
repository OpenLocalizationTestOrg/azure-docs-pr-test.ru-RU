---
title: "Учебник по интеграции Azure Active Directory с Kiteworks | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в Kiteworks."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f7984aaf-ab1f-4a85-9646-a9523f5275d9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jeedes
ms.openlocfilehash: 2fd9b346cb6d838069ef94ee9c2a8d113f22779c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kiteworks"></a><span data-ttu-id="dc073-103">Руководство по интеграции Azure Active Directory с Kiteworks</span><span class="sxs-lookup"><span data-stu-id="dc073-103">Tutorial: Azure Active Directory integration with Kiteworks</span></span>

<span data-ttu-id="dc073-104">В этом руководстве описывается, как интегрировать приложение Kiteworks с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="dc073-104">In this tutorial, you learn how to integrate Kiteworks with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="dc073-105">Интеграция Azure AD с приложением Kiteworks обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="dc073-105">Integrating Kiteworks with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="dc073-106">С помощью Azure AD вы можете контролировать доступ к Kiteworks.</span><span class="sxs-lookup"><span data-stu-id="dc073-106">You can control in Azure AD who has access to Kiteworks</span></span>
- <span data-ttu-id="dc073-107">Вы можете включить автоматический вход пользователей в Kiteworks (единый вход) с использованием учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dc073-107">You can enable your users to automatically get signed-on to Kiteworks (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="dc073-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="dc073-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="dc073-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="dc073-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dc073-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="dc073-110">Prerequisites</span></span>

<span data-ttu-id="dc073-111">Чтобы настроить интеграцию Azure AD с Kiteworks, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="dc073-111">To configure Azure AD integration with Kiteworks, you need the following items:</span></span>

- <span data-ttu-id="dc073-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="dc073-112">An Azure AD subscription</span></span>
- <span data-ttu-id="dc073-113">подписка Kiteworks с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="dc073-113">A Kiteworks single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="dc073-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="dc073-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="dc073-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="dc073-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="dc073-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="dc073-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="dc073-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="dc073-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="dc073-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="dc073-118">Scenario description</span></span>
<span data-ttu-id="dc073-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="dc073-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="dc073-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="dc073-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="dc073-121">Добавление Kiteworks из коллекции</span><span class="sxs-lookup"><span data-stu-id="dc073-121">Adding Kiteworks from the gallery</span></span>
2. <span data-ttu-id="dc073-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="dc073-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kiteworks-from-the-gallery"></a><span data-ttu-id="dc073-123">Добавление Kiteworks из коллекции</span><span class="sxs-lookup"><span data-stu-id="dc073-123">Adding Kiteworks from the gallery</span></span>
<span data-ttu-id="dc073-124">Чтобы настроить интеграцию Kiteworks с Azure AD, необходимо добавить Kiteworks из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="dc073-124">To configure the integration of Kiteworks into Azure AD, you need to add Kiteworks from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="dc073-125">**Чтобы добавить Kiteworks из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="dc073-125">**To add Kiteworks from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="dc073-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="dc073-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="dc073-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="dc073-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="dc073-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="dc073-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="dc073-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="dc073-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="dc073-133">В поле поиска введите **Kiteworks**.</span><span class="sxs-lookup"><span data-stu-id="dc073-133">In the search box, type **Kiteworks**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_search.png)

5. <span data-ttu-id="dc073-135">На панели результатов выберите **Kiteworks** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="dc073-135">In the results panel, select **Kiteworks**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="dc073-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="dc073-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="dc073-138">В этом разделе описана настройка и проверка единого входа Azure AD в Kiteworks с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dc073-138">In this section, you configure and test Azure AD single sign-on with Kiteworks based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="dc073-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Kiteworks соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dc073-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Kiteworks is to a user in Azure AD.</span></span> <span data-ttu-id="dc073-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Kiteworks.</span><span class="sxs-lookup"><span data-stu-id="dc073-140">In other words, a link relationship between an Azure AD user and the related user in Kiteworks needs to be established.</span></span>

<span data-ttu-id="dc073-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Kiteworks.</span><span class="sxs-lookup"><span data-stu-id="dc073-141">In Kiteworks, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="dc073-142">Чтобы настроить и проверить единый вход Azure AD в Kiteworks, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="dc073-142">To configure and test Azure AD single sign-on with Kiteworks, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="dc073-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="dc073-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="dc073-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dc073-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="dc073-145">**[Создание тестового пользователя Kiteworks](#creating-a-kiteworks-test-user)** требуется для создания пользователя Britta Simon в Kiteworks, связанного с представлением этого же пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dc073-145">**[Creating a Kiteworks test user](#creating-a-kiteworks-test-user)** - to have a counterpart of Britta Simon in Kiteworks that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="dc073-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dc073-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="dc073-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="dc073-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="dc073-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="dc073-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="dc073-149">В этом разделе описано, как включить единый вход Azure AD на новом портале Azure и настроить его в приложении Kiteworks.</span><span class="sxs-lookup"><span data-stu-id="dc073-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Kiteworks application.</span></span>

<span data-ttu-id="dc073-150">**Чтобы настроить единый вход Azure AD в Kiteworks, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="dc073-150">**To configure Azure AD single sign-on with Kiteworks, perform the following steps:**</span></span>

1. <span data-ttu-id="dc073-151">На портале Azure на странице интеграции с приложением **Kiteworks** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="dc073-151">In the Azure portal, on the **Kiteworks** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="dc073-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="dc073-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_samlbase.png)

3. <span data-ttu-id="dc073-155">В разделе **Домен и URL-адреса приложения Kiteworks** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="dc073-155">On the **Kiteworks Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_url.png)

    <span data-ttu-id="dc073-157">а.</span><span class="sxs-lookup"><span data-stu-id="dc073-157">a.</span></span> <span data-ttu-id="dc073-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<subdomain>.kiteworks.com`</span><span class="sxs-lookup"><span data-stu-id="dc073-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.kiteworks.com`</span></span>

    <span data-ttu-id="dc073-159">b.</span><span class="sxs-lookup"><span data-stu-id="dc073-159">b.</span></span> <span data-ttu-id="dc073-160">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<subdomain>.kiteworks.com/sp/module.php/saml/sp/saml2-acs.php/sp-sso`</span><span class="sxs-lookup"><span data-stu-id="dc073-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.kiteworks.com/sp/module.php/saml/sp/saml2-acs.php/sp-sso`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="dc073-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="dc073-161">These values are not real.</span></span> <span data-ttu-id="dc073-162">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="dc073-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="dc073-163">Чтобы получить эти значения, обратитесь в [службу поддержки клиентов Kiteworks](http://accellion.com/support).</span><span class="sxs-lookup"><span data-stu-id="dc073-163">Contact [Kiteworks Client support team](http://accellion.com/support) to get these values.</span></span> 
 
4. <span data-ttu-id="dc073-164">В разделе **Сертификат для подписи токена SAML** щелкните **Certificate (Base64)** (Сертификат (Base64)), а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="dc073-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_certificate.png) 

5. <span data-ttu-id="dc073-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="dc073-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kiteworks-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="dc073-168">В разделе **Настройка Kiteworks** щелкните **Настроить Kiteworks**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="dc073-168">On the **Kiteworks Configuration** section, click **Configure Kiteworks** to open **Configure sign-on** window.</span></span> <span data-ttu-id="dc073-169">Скопируйте **URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML**  из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="dc073-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_configure.png) 

7. <span data-ttu-id="dc073-171">Войдите на корпоративный сайт Kiteworks с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="dc073-171">Sign on to your Kiteworks company site as an administrator.</span></span>

8. <span data-ttu-id="dc073-172">На панели инструментов в верхней части экрана нажмите **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="dc073-172">In the toolbar on the top, click **Settings**.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_06.png) 

9. <span data-ttu-id="dc073-174">В разделе **Authentication and Authorization** (Проверка подлинности и авторизация) щелкните **SSO Setup** (Настройка единого входа).</span><span class="sxs-lookup"><span data-stu-id="dc073-174">In the **Authentication and Authorization** section, click **SSO Setup**.</span></span> 
   
    ![Настройка единого входа](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_07.png)
 
10. <span data-ttu-id="dc073-176">На странице настройки единого входа выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="dc073-176">On the SSO Setup page, perform the following steps:</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_09.png)   

    <span data-ttu-id="dc073-178">а.</span><span class="sxs-lookup"><span data-stu-id="dc073-178">a.</span></span> <span data-ttu-id="dc073-179">Установите флажок **Проверка подлинности с помощью единого входа**.</span><span class="sxs-lookup"><span data-stu-id="dc073-179">Select **Authenticate via SSO**.</span></span>

    <span data-ttu-id="dc073-180">b.</span><span class="sxs-lookup"><span data-stu-id="dc073-180">b.</span></span> <span data-ttu-id="dc073-181">Выберите **Initiate AuthnRequest**(Инициировать запрос на проверку подлинности).</span><span class="sxs-lookup"><span data-stu-id="dc073-181">Select **Initiate AuthnRequest**.</span></span>

    <span data-ttu-id="dc073-182">c.</span><span class="sxs-lookup"><span data-stu-id="dc073-182">c.</span></span> <span data-ttu-id="dc073-183">В текстовое поле **Идентификатор сущности IDP** вставьте значение **идентификатора сущности SAML**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="dc073-183">In the **IDP Entity ID** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="dc073-184">г)</span><span class="sxs-lookup"><span data-stu-id="dc073-184">d.</span></span> <span data-ttu-id="dc073-185">В текстовое поле **URL-адрес службы единого входа** вставьте значение **URL-адреса службы единого входа SAML**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="dc073-185">In the **Single Sign-On Service URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="dc073-186">д.</span><span class="sxs-lookup"><span data-stu-id="dc073-186">e.</span></span> <span data-ttu-id="dc073-187">В текстовом поле **URL-адрес службы единого выхода** вставьте значение **URL-адреса выхода**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="dc073-187">In the **Single Logout Service URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="dc073-188">Е.</span><span class="sxs-lookup"><span data-stu-id="dc073-188">f.</span></span> <span data-ttu-id="dc073-189">Откройте загруженный сертификат в блокноте, скопируйте его содержимое в буфер обмена, а затем вставьте его в текстовое поле **Сертификат открытого ключа RSA** .</span><span class="sxs-lookup"><span data-stu-id="dc073-189">Open your downloaded certificate in Notepad, copy the content, and then paste it into the **RSA Public Key Certificate** textbox.</span></span>
 
    <span data-ttu-id="dc073-190">g.</span><span class="sxs-lookup"><span data-stu-id="dc073-190">g.</span></span> <span data-ttu-id="dc073-191">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="dc073-191">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="dc073-192">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="dc073-192">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="dc073-193">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="dc073-193">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="dc073-194">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="dc073-194">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="dc073-195">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="dc073-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="dc073-196">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dc073-196">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="dc073-198">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="dc073-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="dc073-199">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="dc073-199">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kiteworks-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="dc073-201">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="dc073-201">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kiteworks-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="dc073-203">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="dc073-203">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kiteworks-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="dc073-205">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="dc073-205">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kiteworks-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="dc073-207">а.</span><span class="sxs-lookup"><span data-stu-id="dc073-207">a.</span></span> <span data-ttu-id="dc073-208">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="dc073-208">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="dc073-209">b.</span><span class="sxs-lookup"><span data-stu-id="dc073-209">b.</span></span> <span data-ttu-id="dc073-210">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="dc073-210">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="dc073-211">c.</span><span class="sxs-lookup"><span data-stu-id="dc073-211">c.</span></span> <span data-ttu-id="dc073-212">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="dc073-212">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="dc073-213">d.</span><span class="sxs-lookup"><span data-stu-id="dc073-213">d.</span></span> <span data-ttu-id="dc073-214">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="dc073-214">Click **Create**.</span></span>
 
### <a name="creating-a-kiteworks-test-user"></a><span data-ttu-id="dc073-215">Создание тестового пользователя Kiteworks</span><span class="sxs-lookup"><span data-stu-id="dc073-215">Creating a Kiteworks test user</span></span>

<span data-ttu-id="dc073-216">Цель этого раздела — создать пользователя с именем Britta Simon в Kiteworks.</span><span class="sxs-lookup"><span data-stu-id="dc073-216">The objective of this section is to create a user called Britta Simon in Kiteworks.</span></span>

<span data-ttu-id="dc073-217">Приложение Kiteworks поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="dc073-217">Kiteworks supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="dc073-218">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="dc073-218">There is no action item for you in this section.</span></span> <span data-ttu-id="dc073-219">Новый пользователь будет создан при попытке получить доступ к приложению Kiteworks (если он еще не создан).</span><span class="sxs-lookup"><span data-stu-id="dc073-219">A new user is created during an attempt to access Kitewors if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="dc073-220">Если вам нужно вручную создать пользователя, необходимо обратиться в [службу поддержки Kiteworks](http://accellion.com/support).</span><span class="sxs-lookup"><span data-stu-id="dc073-220">If you need to create a user manually, you need to contact the [Kiteworks support team](http://accellion.com/support).</span></span>
 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="dc073-221">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="dc073-221">Assigning the Azure AD test user</span></span>

<span data-ttu-id="dc073-222">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к Kiteworks.</span><span class="sxs-lookup"><span data-stu-id="dc073-222">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Kiteworks.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="dc073-224">**Чтобы назначить пользователя Britta Simon в Kiteworks, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="dc073-224">**To assign Britta Simon to Kiteworks, perform the following steps:**</span></span>

1. <span data-ttu-id="dc073-225">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="dc073-225">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="dc073-227">В списке приложений выберите **Kiteworks**.</span><span class="sxs-lookup"><span data-stu-id="dc073-227">In the applications list, select **Kiteworks**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kiteworks-tutorial/tutorial_kiteworks_app.png) 

3. <span data-ttu-id="dc073-229">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="dc073-229">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="dc073-231">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="dc073-231">Click **Add** button.</span></span> <span data-ttu-id="dc073-232">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="dc073-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="dc073-234">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="dc073-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="dc073-235">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="dc073-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="dc073-236">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="dc073-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="dc073-237">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="dc073-237">Testing single sign-on</span></span>

<span data-ttu-id="dc073-238">Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="dc073-238">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="dc073-239">Щелкнув элемент Kiteworks на панели доступа, вы автоматически войдете в приложение Kiteworks.</span><span class="sxs-lookup"><span data-stu-id="dc073-239">When you click the Kiteworks tile in the Access Panel, you should get automatically signed-on to your Kiteworks application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="dc073-240">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="dc073-240">Additional resources</span></span>

* [<span data-ttu-id="dc073-241">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dc073-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="dc073-242">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="dc073-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kiteworks-tutorial/tutorial_general_203.png

