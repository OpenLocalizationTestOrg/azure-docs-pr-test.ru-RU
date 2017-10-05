---
title: "Руководство по интеграции Azure Active Directory с BambooHR | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и BambooHR."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f826b5d2-9c64-47df-bbbf-0adf9eb0fa71
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: jeedes
ms.openlocfilehash: 06bf91b0e598fd3d8e644378efdb753611ee1ebc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bamboohr"></a><span data-ttu-id="8b86b-103">Руководство по интеграции Azure Active Directory с BambooHR</span><span class="sxs-lookup"><span data-stu-id="8b86b-103">Tutorial: Azure Active Directory integration with BambooHR</span></span>

<span data-ttu-id="8b86b-104">В этом руководстве описано, как интегрировать BambooHR с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8b86b-104">In this tutorial, you learn how to integrate BambooHR with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8b86b-105">Интеграция Azure AD с приложением BambooHR обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="8b86b-105">Integrating BambooHR with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8b86b-106">С помощью Azure AD вы можете контролировать доступ к BambooHR.</span><span class="sxs-lookup"><span data-stu-id="8b86b-106">You can control in Azure AD who has access to BambooHR</span></span>
- <span data-ttu-id="8b86b-107">Вы можете включить автоматический вход пользователей в BambooHR (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8b86b-107">You can enable your users to automatically get signed-on to BambooHR (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8b86b-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="8b86b-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="8b86b-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8b86b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8b86b-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="8b86b-110">Prerequisites</span></span>

<span data-ttu-id="8b86b-111">Чтобы настроить интеграцию Azure AD с BambooHR, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="8b86b-111">To configure Azure AD integration with BambooHR, you need the following items:</span></span>

- <span data-ttu-id="8b86b-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="8b86b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8b86b-113">подписка BambooHR с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="8b86b-113">A BambooHR single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8b86b-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="8b86b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8b86b-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="8b86b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8b86b-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="8b86b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8b86b-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8b86b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8b86b-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="8b86b-118">Scenario description</span></span>
<span data-ttu-id="8b86b-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="8b86b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8b86b-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="8b86b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8b86b-121">Добавление BambooHR из коллекции</span><span class="sxs-lookup"><span data-stu-id="8b86b-121">Adding BambooHR from the gallery</span></span>
2. <span data-ttu-id="8b86b-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="8b86b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bamboohr-from-the-gallery"></a><span data-ttu-id="8b86b-123">Добавление BambooHR из коллекции</span><span class="sxs-lookup"><span data-stu-id="8b86b-123">Adding BambooHR from the gallery</span></span>
<span data-ttu-id="8b86b-124">Чтобы настроить интеграцию BambooHR с Azure AD, необходимо добавить BambooHR из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="8b86b-124">To configure the integration of BambooHR into Azure AD, you need to add BambooHR from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8b86b-125">**Чтобы добавить BambooHR из коллекции, сделайте следующее.**</span><span class="sxs-lookup"><span data-stu-id="8b86b-125">**To add BambooHR from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8b86b-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8b86b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8b86b-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="8b86b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8b86b-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="8b86b-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="8b86b-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="8b86b-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="8b86b-133">В поле поиска введите **BambooHR**.</span><span class="sxs-lookup"><span data-stu-id="8b86b-133">In the search box, type **BambooHR**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_search.png)

5. <span data-ttu-id="8b86b-135">На панели результатов выберите **BambooHR** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="8b86b-135">In the results panel, select **BambooHR**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8b86b-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="8b86b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="8b86b-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложение BambooHR с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8b86b-138">In this section, you configure and test Azure AD single sign-on with BambooHR based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8b86b-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в BambooHR соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8b86b-139">For single sign-on to work, Azure AD needs to know what the counterpart user in BambooHR is to a user in Azure AD.</span></span> <span data-ttu-id="8b86b-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в BambooHR.</span><span class="sxs-lookup"><span data-stu-id="8b86b-140">In other words, a link relationship between an Azure AD user and the related user in BambooHR needs to be established.</span></span>

<span data-ttu-id="8b86b-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в BambooHR.</span><span class="sxs-lookup"><span data-stu-id="8b86b-141">In BambooHR, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="8b86b-142">Чтобы настроить и проверить единый вход Azure AD в BambooHR, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="8b86b-142">To configure and test Azure AD single sign-on with BambooHR, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8b86b-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="8b86b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="8b86b-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8b86b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="8b86b-145">**[Создание тестового пользователя BambooHR](#creating-a-bamboohr-test-user)** нужно для того, чтобы в BambooHR также существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8b86b-145">**[Creating a BambooHR test user](#creating-a-bamboohr-test-user)** - to have a counterpart of Britta Simon in BambooHR that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="8b86b-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8b86b-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="8b86b-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="8b86b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8b86b-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="8b86b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8b86b-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении BambooHR.</span><span class="sxs-lookup"><span data-stu-id="8b86b-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your BambooHR application.</span></span>

<span data-ttu-id="8b86b-150">**Чтобы настроить единый вход Azure AD в BambooHR, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="8b86b-150">**To configure Azure AD single sign-on with BambooHR, perform the following steps:**</span></span>

1. <span data-ttu-id="8b86b-151">На портале Azure на странице интеграции с приложением **BambooHR** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="8b86b-151">In the Azure portal, on the **BambooHR** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="8b86b-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="8b86b-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_samlbase.png)

3. <span data-ttu-id="8b86b-155">В разделе **Домены и URL-адреса приложения BambooHR** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="8b86b-155">On the **BambooHR Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_url.png)

    <span data-ttu-id="8b86b-157">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<company>.bamboohr.com`</span><span class="sxs-lookup"><span data-stu-id="8b86b-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company>.bamboohr.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="8b86b-158">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="8b86b-158">This value is not real.</span></span> <span data-ttu-id="8b86b-159">Вместо него необходимо указать фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="8b86b-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="8b86b-160">Для получения этого значения обратитесь к [группе поддержки BambooHR](https://www.bamboohr.com/contact.php).</span><span class="sxs-lookup"><span data-stu-id="8b86b-160">Contact [BambooHR Client support team](https://www.bamboohr.com/contact.php) to get this value.</span></span> 
 
4. <span data-ttu-id="8b86b-161">В разделе **Сертификат для подписи токена SAML** щелкните **Certificate (Base64)** (Сертификат (Base64)), а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="8b86b-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_certificate.png) 

5. <span data-ttu-id="8b86b-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="8b86b-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8b86b-165">В разделе **Конфигурация BambooHR** щелкните **Настроить BambooHR**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="8b86b-165">On the **BambooHR Configuration** section, click **Configure BambooHR** to open **Configure sign-on** window.</span></span> <span data-ttu-id="8b86b-166">Скопируйте **URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="8b86b-166">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_configure.png) 

6. <span data-ttu-id="8b86b-168">В другом окне веб-браузера войдите на свой корпоративный веб-сайт BambooHR в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="8b86b-168">In a different web browser window, log into your BambooHR company site as an administrator.</span></span>

7. <span data-ttu-id="8b86b-169">На домашней странице выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="8b86b-169">On the homepage, perform the following steps:</span></span>
   
    <span data-ttu-id="8b86b-170">![Единый вход](./media/active-directory-saas-bamboo-hr-tutorial/ic796691.png "Единый вход")</span><span class="sxs-lookup"><span data-stu-id="8b86b-170">![Single Sign-On](./media/active-directory-saas-bamboo-hr-tutorial/ic796691.png "Single Sign-On")</span></span>   

    <span data-ttu-id="8b86b-171">а.</span><span class="sxs-lookup"><span data-stu-id="8b86b-171">a.</span></span> <span data-ttu-id="8b86b-172">Нажмите **Приложения**.</span><span class="sxs-lookup"><span data-stu-id="8b86b-172">Click **Apps**.</span></span>
   
    <span data-ttu-id="8b86b-173">b.</span><span class="sxs-lookup"><span data-stu-id="8b86b-173">b.</span></span> <span data-ttu-id="8b86b-174">В меню приложений в левой части окна нажмите **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="8b86b-174">In the apps menu on the left, click **Single Sign-On**.</span></span>
   
    <span data-ttu-id="8b86b-175">c.</span><span class="sxs-lookup"><span data-stu-id="8b86b-175">c.</span></span> <span data-ttu-id="8b86b-176">Нажмите **Единый вход SAML**.</span><span class="sxs-lookup"><span data-stu-id="8b86b-176">Click **SAML Single Sign-On**.</span></span>

8. <span data-ttu-id="8b86b-177">В разделе **Единый вход SAML** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="8b86b-177">In the **SAML Single Sign-On** section, perform the following steps:</span></span>
   
    <span data-ttu-id="8b86b-178">![Единый вход SAML](./media/active-directory-saas-bamboo-hr-tutorial/ic796692.png "Единый вход SAML")</span><span class="sxs-lookup"><span data-stu-id="8b86b-178">![SAML Single Sign-On](./media/active-directory-saas-bamboo-hr-tutorial/ic796692.png "SAML Single Sign-On")</span></span>
   
    <span data-ttu-id="8b86b-179">а.</span><span class="sxs-lookup"><span data-stu-id="8b86b-179">a.</span></span> <span data-ttu-id="8b86b-180">Вставьте значение **URL-адрес службы единого входа SAML** в текстовое поле **SSO Login Url** (URL-адрес единого входа).</span><span class="sxs-lookup"><span data-stu-id="8b86b-180">Paste the **SAML Single Sign-On Service URL** value into the **SSO Login Url** textbox.</span></span>
      
    <span data-ttu-id="8b86b-181">b.</span><span class="sxs-lookup"><span data-stu-id="8b86b-181">b.</span></span> <span data-ttu-id="8b86b-182">Откройте в Блокноте сертификат в кодировке Base-64, скачанный с портала Azure, скопируйте его содержимое в буфер обмена, а затем вставьте его в текстовое поле **X.509 Certificate** (Сертификат X.509).</span><span class="sxs-lookup"><span data-stu-id="8b86b-182">Open base-64 encoded certificate downloaded from Azure portal in notepad, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox</span></span>
   
    <span data-ttu-id="8b86b-183">c.</span><span class="sxs-lookup"><span data-stu-id="8b86b-183">c.</span></span> <span data-ttu-id="8b86b-184">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="8b86b-184">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="8b86b-185">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="8b86b-185">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="8b86b-186">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="8b86b-186">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="8b86b-187">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="8b86b-187">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8b86b-188">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="8b86b-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="8b86b-189">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8b86b-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="8b86b-191">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="8b86b-191">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8b86b-192">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8b86b-192">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bamboo-hr-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8b86b-194">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="8b86b-194">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bamboo-hr-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8b86b-196">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="8b86b-196">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bamboo-hr-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8b86b-198">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="8b86b-198">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-bamboo-hr-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8b86b-200">а.</span><span class="sxs-lookup"><span data-stu-id="8b86b-200">a.</span></span> <span data-ttu-id="8b86b-201">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8b86b-201">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8b86b-202">b.</span><span class="sxs-lookup"><span data-stu-id="8b86b-202">b.</span></span> <span data-ttu-id="8b86b-203">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8b86b-203">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8b86b-204">c.</span><span class="sxs-lookup"><span data-stu-id="8b86b-204">c.</span></span> <span data-ttu-id="8b86b-205">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="8b86b-205">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="8b86b-206">d.</span><span class="sxs-lookup"><span data-stu-id="8b86b-206">d.</span></span> <span data-ttu-id="8b86b-207">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="8b86b-207">Click **Create**.</span></span>
 
### <a name="creating-a-bamboohr-test-user"></a><span data-ttu-id="8b86b-208">Создание тестового пользователя BambooHR</span><span class="sxs-lookup"><span data-stu-id="8b86b-208">Creating a BambooHR test user</span></span>

<span data-ttu-id="8b86b-209">Чтобы пользователи Azure AD могли выполнять вход в BambooHR, они должны быть подготовлены в BambooHR.</span><span class="sxs-lookup"><span data-stu-id="8b86b-209">To enable Azure AD users to log in to BambooHR, they must be provisioned into BambooHR.</span></span>  

<span data-ttu-id="8b86b-210">В случае с BambooHR подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="8b86b-210">In the case of BambooHR, provisioning is a manual task.</span></span>

<span data-ttu-id="8b86b-211">**Чтобы подготовить учетную запись пользователя, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="8b86b-211">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="8b86b-212">Войдите на свой веб-сайт **BambooHR** в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="8b86b-212">Log in to your **BambooHR** site as administrator.</span></span>

2. <span data-ttu-id="8b86b-213">На панели инструментов в верхней части экрана нажмите **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="8b86b-213">In the toolbar on the top, click **Settings**.</span></span>
   
    <span data-ttu-id="8b86b-214">![Параметр](./media/active-directory-saas-bamboo-hr-tutorial/ic796694.png "Параметр")</span><span class="sxs-lookup"><span data-stu-id="8b86b-214">![Setting](./media/active-directory-saas-bamboo-hr-tutorial/ic796694.png "Setting")</span></span>

3. <span data-ttu-id="8b86b-215">Нажмите **Обзор**.</span><span class="sxs-lookup"><span data-stu-id="8b86b-215">Click **Overview**.</span></span>

4. <span data-ttu-id="8b86b-216">На панели навигации в левой части экрана последовательно выберите параметры **Безопасность \> Пользователи**.</span><span class="sxs-lookup"><span data-stu-id="8b86b-216">In the left navigation pane, go to **Security \> Users**.</span></span>

5. <span data-ttu-id="8b86b-217">Введите имя пользователя, пароль и адрес электронной почты для действующей учетной записи AAD, которую вы хотите подготовить, в соответствующие текстовые поля.</span><span class="sxs-lookup"><span data-stu-id="8b86b-217">Type the user name, password, and email address of a valid AAD account you want to provision into the related textboxes.</span></span>

6. <span data-ttu-id="8b86b-218">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="8b86b-218">Click **Save**.</span></span>
        
>[!NOTE]
><span data-ttu-id="8b86b-219">Вы можете использовать любые другие средства создания учетной записи пользователя BambooHR или API, предоставляемые BambooHR для подготовки учетных записей пользователя AAD.</span><span class="sxs-lookup"><span data-stu-id="8b86b-219">You can use any other BambooHR user account creation tools or APIs provided by BambooHR to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="8b86b-220">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="8b86b-220">Assigning the Azure AD test user</span></span>

<span data-ttu-id="8b86b-221">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к BambooHR.</span><span class="sxs-lookup"><span data-stu-id="8b86b-221">In this section, you enable Britta Simon to use Azure single sign-on by granting access to BambooHR.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="8b86b-223">**Чтобы назначить пользователя Britta Simon в BambooHR, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="8b86b-223">**To assign Britta Simon to BambooHR, perform the following steps:**</span></span>

1. <span data-ttu-id="8b86b-224">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="8b86b-224">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="8b86b-226">Из списка приложений выберите **BambooHR**.</span><span class="sxs-lookup"><span data-stu-id="8b86b-226">In the applications list, select **BambooHR**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_app.png) 

3. <span data-ttu-id="8b86b-228">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="8b86b-228">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="8b86b-230">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="8b86b-230">Click **Add** button.</span></span> <span data-ttu-id="8b86b-231">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="8b86b-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="8b86b-233">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="8b86b-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="8b86b-234">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="8b86b-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8b86b-235">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="8b86b-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8b86b-236">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="8b86b-236">Testing single sign-on</span></span>

<span data-ttu-id="8b86b-237">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="8b86b-237">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="8b86b-238">Щелкнув элемент "BambooHR" на панели доступа, вы автоматически войдете в приложение BambooHR.</span><span class="sxs-lookup"><span data-stu-id="8b86b-238">When you click the BambooHR tile in the Access Panel, you should get automatically signed-on to your BambooHR application.</span></span>
<span data-ttu-id="8b86b-239">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8b86b-239">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="8b86b-240">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="8b86b-240">Additional resources</span></span>

* [<span data-ttu-id="8b86b-241">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8b86b-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8b86b-242">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8b86b-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_203.png

