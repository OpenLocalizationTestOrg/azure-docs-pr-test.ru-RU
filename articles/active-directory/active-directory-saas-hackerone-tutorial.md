---
title: "Руководство по интеграции Azure Active Directory с HackerOne | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в HackerOne."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 229d1efb-b6a5-4df8-9839-5d551487db4e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 657d8d4c98b7b133698a5cda0aa675da7f68c464
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hackerone"></a><span data-ttu-id="a9548-103">Учебник. Интеграция Azure Active Directory с HackerOn</span><span class="sxs-lookup"><span data-stu-id="a9548-103">Tutorial: Azure Active Directory integration with HackerOne</span></span>

<span data-ttu-id="a9548-104">В данном руководстве описано, как интегрировать Azure Active Directory (Azure AD) с приложением HackerOne.</span><span class="sxs-lookup"><span data-stu-id="a9548-104">In this tutorial, you learn how to integrate HackerOne with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a9548-105">Интеграция HackerOn с Azure AD дает приведенные далее преимущества:</span><span class="sxs-lookup"><span data-stu-id="a9548-105">Integrating HackerOne with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a9548-106">С помощью Azure AD вы можете контролировать доступ к HackerOn.</span><span class="sxs-lookup"><span data-stu-id="a9548-106">You can control in Azure AD who has access to HackerOne</span></span>
- <span data-ttu-id="a9548-107">Вы можете включить автоматический вход пользователей в HackerOn (единый вход) под учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a9548-107">You can enable your users to automatically get signed-on to HackerOne (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a9548-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="a9548-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a9548-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a9548-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a9548-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a9548-110">Prerequisites</span></span>

<span data-ttu-id="a9548-111">Чтобы настроить интеграцию Azure AD с HackerOn, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="a9548-111">To configure Azure AD integration with HackerOne, you need the following items:</span></span>

- <span data-ttu-id="a9548-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="a9548-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a9548-113">подписка с поддержкой единого входа HackerOne.</span><span class="sxs-lookup"><span data-stu-id="a9548-113">A HackerOne single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a9548-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="a9548-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a9548-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="a9548-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a9548-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="a9548-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a9548-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a9548-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a9548-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="a9548-118">Scenario description</span></span>
<span data-ttu-id="a9548-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="a9548-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a9548-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="a9548-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a9548-121">Добавление HackerOne из коллекции</span><span class="sxs-lookup"><span data-stu-id="a9548-121">Adding HackerOne from the gallery</span></span>
2. <span data-ttu-id="a9548-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="a9548-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-hackerone-from-the-gallery"></a><span data-ttu-id="a9548-123">Добавление HackerOne из коллекции</span><span class="sxs-lookup"><span data-stu-id="a9548-123">Adding HackerOne from the gallery</span></span>
<span data-ttu-id="a9548-124">Чтобы настроить интеграцию HackerOne с Azure AD, необходимо добавить HackerOne из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="a9548-124">To configure the integration of HackerOne into Azure AD, you need to add HackerOne from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a9548-125">**Чтобы добавить HackerOn из коллекции, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="a9548-125">**To add HackerOne from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a9548-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a9548-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a9548-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="a9548-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a9548-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="a9548-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="a9548-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="a9548-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="a9548-133">В поле поиска введите **HackerOne**.</span><span class="sxs-lookup"><span data-stu-id="a9548-133">In the search box, type **HackerOne**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_search.png)

5. <span data-ttu-id="a9548-135">На панели результатов выберите **HackerOne** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="a9548-135">In the results panel, select **HackerOne**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a9548-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="a9548-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="a9548-138">В этом разделе описана настройка и проверка единого входа Azure AD в HackerOne с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a9548-138">In this section, you configure and test Azure AD single sign-on with HackerOne based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a9548-139">Чтобы единый вход работал, Azure AD необходимо знать, какой пользователь в HackerOne соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a9548-139">For single sign-on to work, Azure AD needs to know what the counterpart user in HackerOne is to a user in Azure AD.</span></span> <span data-ttu-id="a9548-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в HackerOne.</span><span class="sxs-lookup"><span data-stu-id="a9548-140">In other words, a link relationship between an Azure AD user and the related user in HackerOne needs to be established.</span></span>

<span data-ttu-id="a9548-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в HackerOne.</span><span class="sxs-lookup"><span data-stu-id="a9548-141">In HackerOne, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a9548-142">Чтобы настроить и проверить единый вход Azure AD в HackerOne, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="a9548-142">To configure and test Azure AD single sign-on with HackerOne, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a9548-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="a9548-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a9548-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a9548-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a9548-145">**[Создание тестового пользователя HackerOne](#creating-a-hackerone-test-user)** требуется для создания пользователя Britta Simon в HackerOne, связанного с соответствующим представлением в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a9548-145">**[Creating a HackerOne test user](#creating-a-hackerone-test-user)** - to have a counterpart of Britta Simon in HackerOne that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a9548-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a9548-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a9548-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="a9548-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a9548-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="a9548-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a9548-149">В данном разделе описано, как включить единый вход Azure AD на портале управления Azure и настроить его в приложении HackerOne.</span><span class="sxs-lookup"><span data-stu-id="a9548-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your HackerOne application.</span></span>

<span data-ttu-id="a9548-150">**Чтобы настроить единый вход Azure AD в HackerOne, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="a9548-150">**To configure Azure AD single sign-on with HackerOne, perform the following steps:**</span></span>

1. <span data-ttu-id="a9548-151">На портале Azure на странице интеграции с приложением **HackerOne** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="a9548-151">In the Azure portal, on the **HackerOne** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="a9548-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="a9548-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_samlbase.png)

3. <span data-ttu-id="a9548-155">Для **URL-адреса службы единого входа и идентификатора HackerOne** введите следующие значения:</span><span class="sxs-lookup"><span data-stu-id="a9548-155">On the **HackerOne Single sign-on URL and Identifier** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_url.png)

    <span data-ttu-id="a9548-157">а.</span><span class="sxs-lookup"><span data-stu-id="a9548-157">a.</span></span> <span data-ttu-id="a9548-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://hackerone.com/<company name>/authentication`</span><span class="sxs-lookup"><span data-stu-id="a9548-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://hackerone.com/<company name>/authentication`</span></span>

    <span data-ttu-id="a9548-159">b.</span><span class="sxs-lookup"><span data-stu-id="a9548-159">b.</span></span> <span data-ttu-id="a9548-160">В текстовом поле **Идентификатор** введите URL-адрес в формате:`https://hackerone.com/users/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="a9548-160">In the **Identifier** textbox, type a URL as:  `https://hackerone.com/users/saml/metadata`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="a9548-161">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="a9548-161">This value is not real.</span></span> <span data-ttu-id="a9548-162">Вместо него необходимо указать фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="a9548-162">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="a9548-163">Чтобы получить его, обратитесь в [службу поддержки HackerOne](mailto:support@hackerone.com).</span><span class="sxs-lookup"><span data-stu-id="a9548-163">Contact [HackerOne support team](mailto:support@hackerone.com) to get this value.</span></span> 
 
4. <span data-ttu-id="a9548-164">В разделе **Сертификат для подписи токена SAML** щелкните **Certificate (Base64)** (Сертификат (Base64)), а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="a9548-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_certificate.png) 

5. <span data-ttu-id="a9548-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="a9548-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-hackerone-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a9548-168">В разделе **Настройка HackerOne** щелкните **Настроить HackerOne**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="a9548-168">On the **HackerOne Configuration** section, click **Configure HackerOne** to open **Configure sign-on** window.</span></span> <span data-ttu-id="a9548-169">Скопируйте **URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="a9548-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_configure.png) 

7. <span data-ttu-id="a9548-171">Войдите в клиент HackerOne как администратор.</span><span class="sxs-lookup"><span data-stu-id="a9548-171">Sign On to your HackerOne tenant as an administrator.</span></span>

8. <span data-ttu-id="a9548-172">В верхнем меню щелкните **Settings** (Параметры).</span><span class="sxs-lookup"><span data-stu-id="a9548-172">In the menu on the top, click the "**Settings**."</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_001.png) 

9. <span data-ttu-id="a9548-174">Перейдите к разделу **Authentication** (Аутентификация) и щелкните **Add SAML settings** (Добавить параметры SAML).</span><span class="sxs-lookup"><span data-stu-id="a9548-174">Navigate to "**Authentication**" and click "**Add SAML settings**."</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_003.png) 

10. <span data-ttu-id="a9548-176">В диалоговом окне **SAML Settings** (Параметры SAML) выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="a9548-176">On the **SAML Settings** dialog, perform the following steps:</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_004.png) 

    <span data-ttu-id="a9548-178">а.</span><span class="sxs-lookup"><span data-stu-id="a9548-178">a.</span></span> <span data-ttu-id="a9548-179">Введите имя зарегистрированного домена в поле **Email Domain** (Домен электронной почты).</span><span class="sxs-lookup"><span data-stu-id="a9548-179">In the **Email Domain** textbox, type a registered domain.</span></span>

    <span data-ttu-id="a9548-180">b.</span><span class="sxs-lookup"><span data-stu-id="a9548-180">b.</span></span> <span data-ttu-id="a9548-181">В текстовое поле **URL-адрес для единого входа** вставьте значение **URL-адреса службы единого входа SAML**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="a9548-181">In  **Single Sign On URL** textboxes, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="a9548-182">c.</span><span class="sxs-lookup"><span data-stu-id="a9548-182">c.</span></span> <span data-ttu-id="a9548-183">Откройте в блокноте **сертификат**, скачанный на портале Azure, скопируйте его содержимое в буфер обмена, а затем вставьте его в текстовое поле **Сертификат X.509**.</span><span class="sxs-lookup"><span data-stu-id="a9548-183">Open your **Certificate file** in notepad downloaded from Azure portal, copy the content of it into your clipboard, and then paste it to the **X509 Certificate**  textbox.</span></span>
    
    <span data-ttu-id="a9548-184">г)</span><span class="sxs-lookup"><span data-stu-id="a9548-184">d.</span></span> <span data-ttu-id="a9548-185">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="a9548-185">Click **Save**.</span></span>

11. <span data-ttu-id="a9548-186">В диалоговом окне "Authentication Settings" (Параметры аутентификации) выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="a9548-186">On the Authentication Settings dialog, perform the following steps:</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_005.png) 

    <span data-ttu-id="a9548-188">а.</span><span class="sxs-lookup"><span data-stu-id="a9548-188">a.</span></span> <span data-ttu-id="a9548-189">Щелкните **Run test**(Выполнить проверку).</span><span class="sxs-lookup"><span data-stu-id="a9548-189">Click **Run test**.</span></span>

    <span data-ttu-id="a9548-190">b.</span><span class="sxs-lookup"><span data-stu-id="a9548-190">b.</span></span> <span data-ttu-id="a9548-191">Если поле **Status** (Состояние) имеет значение **Last test status: created** (Состояние при последней проверке: создан), обратитесь в [службу поддержки HackerOne](mailto:support@hackerone.com), чтобы запросить проверку своей конфигурации.</span><span class="sxs-lookup"><span data-stu-id="a9548-191">If the value of the **Status** field equals **Last test status: created**, contact your [HackerOne support team](mailto:support@hackerone.com) to request a review of your configuration.</span></span>

> [!TIP]
> <span data-ttu-id="a9548-192">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="a9548-192">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a9548-193">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="a9548-193">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a9548-194">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="a9548-194">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a9548-195">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="a9548-195">Creating an Azure AD test user</span></span>
<span data-ttu-id="a9548-196">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a9548-196">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="a9548-198">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="a9548-198">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a9548-199">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a9548-199">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-hackerone-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a9548-201">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="a9548-201">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-hackerone-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a9548-203">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="a9548-203">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-hackerone-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a9548-205">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="a9548-205">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-hackerone-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a9548-207">а.</span><span class="sxs-lookup"><span data-stu-id="a9548-207">a.</span></span> <span data-ttu-id="a9548-208">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a9548-208">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a9548-209">b.</span><span class="sxs-lookup"><span data-stu-id="a9548-209">b.</span></span> <span data-ttu-id="a9548-210">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a9548-210">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a9548-211">c.</span><span class="sxs-lookup"><span data-stu-id="a9548-211">c.</span></span> <span data-ttu-id="a9548-212">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="a9548-212">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a9548-213">d.</span><span class="sxs-lookup"><span data-stu-id="a9548-213">d.</span></span> <span data-ttu-id="a9548-214">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="a9548-214">Click **Create**.</span></span>
 
### <a name="creating-a-hackerone-test-user"></a><span data-ttu-id="a9548-215">Создание тестового пользователя HackerOne</span><span class="sxs-lookup"><span data-stu-id="a9548-215">Creating a HackerOne test user</span></span>

<span data-ttu-id="a9548-216">Затем нужно создать пользователя Britta Simon в приложении HackerOne.</span><span class="sxs-lookup"><span data-stu-id="a9548-216">Next, you create a user called Britta Simon in HackerOne.</span></span> <span data-ttu-id="a9548-217">Приложение HackerOne поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="a9548-217">HackerOne supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="a9548-218">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="a9548-218">There is no action item for you in this section.</span></span> <span data-ttu-id="a9548-219">Новый пользователь, если он еще не существует, создается при доступе к HackerOne.</span><span class="sxs-lookup"><span data-stu-id="a9548-219">When you access HackerOne, a new user is created if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="a9548-220">Если вам нужно вручную создать пользователя, необходимо обратиться в службу поддержки HackerOne.</span><span class="sxs-lookup"><span data-stu-id="a9548-220">If you need to create a user manually, you need to contact the Certify support team.</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a9548-221">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="a9548-221">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a9548-222">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure путем предоставления доступа к HackerOne.</span><span class="sxs-lookup"><span data-stu-id="a9548-222">In this section, you enable Britta Simon to use Azure single sign-on by granting access to HackerOne.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="a9548-224">**Чтобы назначить пользователя Britta Simon в HackerOne, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="a9548-224">**To assign Britta Simon to HackerOne, perform the following steps:**</span></span>

1. <span data-ttu-id="a9548-225">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="a9548-225">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="a9548-227">В списке приложений выберите **HackerOne**.</span><span class="sxs-lookup"><span data-stu-id="a9548-227">In the applications list, select **HackerOne**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-hackerone-tutorial/tutorial_hackerone_app.png) 

3. <span data-ttu-id="a9548-229">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="a9548-229">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="a9548-231">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="a9548-231">Click **Add** button.</span></span> <span data-ttu-id="a9548-232">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="a9548-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="a9548-234">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="a9548-234">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a9548-235">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="a9548-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a9548-236">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="a9548-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a9548-237">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="a9548-237">Testing single sign-on</span></span>

<span data-ttu-id="a9548-238">И, наконец, нужно проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="a9548-238">Finally, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>  

<span data-ttu-id="a9548-239">Щелкнув плитку HackerOne на панели доступа, вы автоматически войдете в приложение HackerOne.</span><span class="sxs-lookup"><span data-stu-id="a9548-239">When you click the HackerOne tile in the Access Panel, you should get automatically signed-on to your HackerOne application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a9548-240">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="a9548-240">Additional resources</span></span>

* [<span data-ttu-id="a9548-241">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a9548-241">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a9548-242">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a9548-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hackerone-tutorial/tutorial_general_203.png

