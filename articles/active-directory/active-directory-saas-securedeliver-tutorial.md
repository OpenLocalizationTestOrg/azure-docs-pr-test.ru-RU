---
title: "Руководство по интеграции Azure Active Directory с SECURE DELIVER | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в SECURE DELIVER."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: fccd5668-fe6f-4e6d-a9ce-ba4f321c33d1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: f6e5b1e34893f6b8fe14e238e24086bb47d009a5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-secure-deliver"></a><span data-ttu-id="12950-103">Руководство. Интеграция Azure Active Directory с SECURE DELIVER</span><span class="sxs-lookup"><span data-stu-id="12950-103">Tutorial: Azure Active Directory integration with SECURE DELIVER</span></span>

<span data-ttu-id="12950-104">В этом руководстве описано, как интегрировать SECURE DELIVER с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="12950-104">In this tutorial, you learn how to integrate SECURE DELIVER with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="12950-105">Интеграция SECURE DELIVER с Azure AD имеет следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="12950-105">Integrating SECURE DELIVER with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="12950-106">С помощью Azure AD вы можете управлять доступом к SECURE DELIVER.</span><span class="sxs-lookup"><span data-stu-id="12950-106">You can control in Azure AD who has access to SECURE DELIVER</span></span>
- <span data-ttu-id="12950-107">Вы можете включить автоматический вход пользователей в SECURE DELIVER (единый вход) с использованием учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="12950-107">You can enable your users to automatically get signed-on to SECURE DELIVER (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="12950-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="12950-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="12950-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="12950-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="12950-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="12950-110">Prerequisites</span></span>

<span data-ttu-id="12950-111">Чтобы настроить интеграцию Azure AD с SECURE DELIVER, вам потребуется следующее.</span><span class="sxs-lookup"><span data-stu-id="12950-111">To configure Azure AD integration with SECURE DELIVER, you need the following items:</span></span>

- <span data-ttu-id="12950-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="12950-112">An Azure AD subscription</span></span>
- <span data-ttu-id="12950-113">подписка SECURE DELIVER с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="12950-113">A SECURE DELIVER single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="12950-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="12950-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="12950-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="12950-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="12950-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="12950-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="12950-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="12950-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="12950-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="12950-118">Scenario description</span></span>
<span data-ttu-id="12950-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="12950-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="12950-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="12950-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="12950-121">Добавление SECURE DELIVER из коллекции</span><span class="sxs-lookup"><span data-stu-id="12950-121">Adding SECURE DELIVER from the gallery</span></span>
2. <span data-ttu-id="12950-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="12950-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-secure-deliver-from-the-gallery"></a><span data-ttu-id="12950-123">Добавление SECURE DELIVER из коллекции</span><span class="sxs-lookup"><span data-stu-id="12950-123">Adding SECURE DELIVER from the gallery</span></span>
<span data-ttu-id="12950-124">Чтобы настроить интеграцию SECURE DELIVER с Azure AD, необходимо добавить SECURE DELIVER из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="12950-124">To configure the integration of SECURE DELIVER into Azure AD, you need to add SECURE DELIVER from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="12950-125">**Чтобы добавить SECURE DELIVER из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="12950-125">**To add SECURE DELIVER from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="12950-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="12950-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="12950-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="12950-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="12950-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="12950-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="12950-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="12950-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="12950-133">В поле поиска введите **SECURE DELIVER**.</span><span class="sxs-lookup"><span data-stu-id="12950-133">In the search box, type **SECURE DELIVER**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-securedeliver-tutorial/tutorial_securedeliver_search.png)

5. <span data-ttu-id="12950-135">На панели результатов выберите **SECURE DELIVER** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="12950-135">In the results panel, select **SECURE DELIVER**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-securedeliver-tutorial/tutorial_securedeliver_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="12950-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="12950-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="12950-138">В этом разделе описана настройка и проверка единого входа Azure AD в SECURE DELIVER с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="12950-138">In this section, you configure and test Azure AD single sign-on with SECURE DELIVER based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="12950-139">Чтобы единый вход работал, Azure AD необходима информация о том, какой пользователь в SECURE DELIVER соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="12950-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SECURE DELIVER is to a user in Azure AD.</span></span> <span data-ttu-id="12950-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в SECURE DELIVER.</span><span class="sxs-lookup"><span data-stu-id="12950-140">In other words, a link relationship between an Azure AD user and the related user in SECURE DELIVER needs to be established.</span></span>

<span data-ttu-id="12950-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в SECURE DELIVER.</span><span class="sxs-lookup"><span data-stu-id="12950-141">In SECURE DELIVER, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="12950-142">Чтобы настроить и проверить единый вход Azure AD в SECURE DELIVER, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="12950-142">To configure and test Azure AD single sign-on with SECURE DELIVER, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="12950-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="12950-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="12950-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="12950-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="12950-145">**[Создание тестового пользователя SECURE DELIVER](#creating-a-secure-deliver-test-user)** требуется для того, чтобы в SECURE DELIVER существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="12950-145">**[Creating a SECURE DELIVER test user](#creating-a-secure-deliver-test-user)** - to have a counterpart of Britta Simon in SECURE DELIVER that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="12950-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="12950-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="12950-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="12950-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="12950-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="12950-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="12950-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении SECURE DELIVER.</span><span class="sxs-lookup"><span data-stu-id="12950-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SECURE DELIVER application.</span></span>

<span data-ttu-id="12950-150">**Чтобы настроить единый вход Azure AD в SECURE DELIVER, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="12950-150">**To configure Azure AD single sign-on with SECURE DELIVER, perform the following steps:**</span></span>

1. <span data-ttu-id="12950-151">На портале Azure на странице интеграции с приложением **SECURE DELIVER** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="12950-151">In the Azure portal, on the **SECURE DELIVER** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="12950-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="12950-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-securedeliver-tutorial/tutorial_securedeliver_samlbase.png)

3. <span data-ttu-id="12950-155">В разделе **Домены и URL-адреса приложения SECURE DELIVER** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="12950-155">On the **SECURE DELIVER Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-securedeliver-tutorial/tutorial_securedeliver_url.png)

    <span data-ttu-id="12950-157">а.</span><span class="sxs-lookup"><span data-stu-id="12950-157">a.</span></span> <span data-ttu-id="12950-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<companyname>.i-securedeliver.jp/sd/<tenantname>/jsf/login/sso`</span><span class="sxs-lookup"><span data-stu-id="12950-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.i-securedeliver.jp/sd/<tenantname>/jsf/login/sso`</span></span>

    <span data-ttu-id="12950-159">b.</span><span class="sxs-lookup"><span data-stu-id="12950-159">b.</span></span> <span data-ttu-id="12950-160">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<companyname>.i-securedeliver.jp/sd/<tenantname>/postResponse`</span><span class="sxs-lookup"><span data-stu-id="12950-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.i-securedeliver.jp/sd/<tenantname>/postResponse`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="12950-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="12950-161">These values are not real.</span></span> <span data-ttu-id="12950-162">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="12950-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="12950-163">Чтобы получить эти значения, обратитесь к [группе поддержки клиентов SECURE DELIVER](mailto:iw-sd-support@fujifilm.com).</span><span class="sxs-lookup"><span data-stu-id="12950-163">Contact [SECURE DELIVER Client support team](mailto:iw-sd-support@fujifilm.com) to get these values.</span></span> 
 
4. <span data-ttu-id="12950-164">В разделе **Сертификат для подписи токена SAML** щелкните **Certificate (Base64)** (Сертификат (Base64)), а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="12950-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-securedeliver-tutorial/tutorial_securedeliver_certificate.png) 

5. <span data-ttu-id="12950-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="12950-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-securedeliver-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="12950-168">В разделе **Настройка SECURE DELIVER** щелкните **Настроить SECURE DELIVER**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="12950-168">On the **SECURE DELIVER Configuration** section, click **Configure SECURE DELIVER** to open **Configure sign-on** window.</span></span> <span data-ttu-id="12950-169">Скопируйте **URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML**  из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="12950-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-securedeliver-tutorial/tutorial_securedeliver_configure.png) 

7. <span data-ttu-id="12950-171">Чтобы настроить единый вход на стороне **SECURE DELIVER**, нужно отправить скачанный **сертификат в кодировке Base64**, **URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML** [группе поддержки SECURE DELIVER](mailto:iw-sd-support@fujifilm.com).</span><span class="sxs-lookup"><span data-stu-id="12950-171">To configure single sign-on on **SECURE DELIVER** side, you need to send the downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [SECURE DELIVER support team](mailto:iw-sd-support@fujifilm.com).</span></span> <span data-ttu-id="12950-172">Специалисты службы поддержки настроят подключение единого входа SAML на обеих сторонах.</span><span class="sxs-lookup"><span data-stu-id="12950-172">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="12950-173">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="12950-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="12950-174">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="12950-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="12950-175">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="12950-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="12950-176">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="12950-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="12950-177">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="12950-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="12950-179">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="12950-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="12950-180">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="12950-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-securedeliver-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="12950-182">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="12950-182">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-securedeliver-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="12950-184">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="12950-184">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-securedeliver-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="12950-186">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="12950-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-securedeliver-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="12950-188">а.</span><span class="sxs-lookup"><span data-stu-id="12950-188">a.</span></span> <span data-ttu-id="12950-189">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="12950-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="12950-190">b.</span><span class="sxs-lookup"><span data-stu-id="12950-190">b.</span></span> <span data-ttu-id="12950-191">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="12950-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="12950-192">c.</span><span class="sxs-lookup"><span data-stu-id="12950-192">c.</span></span> <span data-ttu-id="12950-193">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="12950-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="12950-194">d.</span><span class="sxs-lookup"><span data-stu-id="12950-194">d.</span></span> <span data-ttu-id="12950-195">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="12950-195">Click **Create**.</span></span>
 
### <a name="creating-a-secure-deliver-test-user"></a><span data-ttu-id="12950-196">Создание тестового пользователя в SECURE DELIVER</span><span class="sxs-lookup"><span data-stu-id="12950-196">Creating a SECURE DELIVER test user</span></span>

<span data-ttu-id="12950-197">Цель этого раздела — создать в приложении SECURE DELIVER пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="12950-197">The objective of this section is to create a user called Britta Simon in SECURE DELIVER.</span></span> <span data-ttu-id="12950-198">Обратитесь к [группе поддержки SECURE DELIVER](mailto:iw-sd-support@fujifilm.com), чтобы добавить пользователей в учетную запись SECURE DELIVER.</span><span class="sxs-lookup"><span data-stu-id="12950-198">Work with [SECURE DELIVER support team](mailto:iw-sd-support@fujifilm.com) to add the users in the SECURE DELIVER account.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="12950-199">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="12950-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="12950-200">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к SECURE DELIVER.</span><span class="sxs-lookup"><span data-stu-id="12950-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SECURE DELIVER.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="12950-202">**Чтобы назначить пользователя Britta Simon приложению SECURE DELIVER, сделайте следующее.**</span><span class="sxs-lookup"><span data-stu-id="12950-202">**To assign Britta Simon to SECURE DELIVER, perform the following steps:**</span></span>

1. <span data-ttu-id="12950-203">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="12950-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="12950-205">В списке приложений выберите **SECURE DELIVER**.</span><span class="sxs-lookup"><span data-stu-id="12950-205">In the applications list, select **SECURE DELIVER**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-securedeliver-tutorial/tutorial_securedeliver_app.png) 

3. <span data-ttu-id="12950-207">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="12950-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="12950-209">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="12950-209">Click **Add** button.</span></span> <span data-ttu-id="12950-210">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="12950-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="12950-212">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="12950-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="12950-213">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="12950-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="12950-214">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="12950-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="12950-215">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="12950-215">Testing single sign-on</span></span>

<span data-ttu-id="12950-216">Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="12950-216">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="12950-217">Щелкнув плитку SECURE DELIVER на панели доступа, вы автоматически войдете в приложение SECURE DELIVER.</span><span class="sxs-lookup"><span data-stu-id="12950-217">When you click the SECURE DELIVER tile in the Access Panel, you should get automatically signed-on to your SECURE DELIVER application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="12950-218">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="12950-218">Additional resources</span></span>

* [<span data-ttu-id="12950-219">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="12950-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="12950-220">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="12950-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-securedeliver-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-securedeliver-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-securedeliver-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-securedeliver-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-securedeliver-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-securedeliver-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-securedeliver-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-securedeliver-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-securedeliver-tutorial/tutorial_general_203.png

