---
title: "Руководство по интеграции Azure Active Directory с Rightscale | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и Rightscale."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3a8d376d-95fb-4dd7-832a-4fdd4dd7c87c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 222c4414a9f736a3589b4cdd0ed934696f6c31ef
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rightscale"></a><span data-ttu-id="3da2e-103">Руководство по интеграции Azure Active Directory с Rightscale</span><span class="sxs-lookup"><span data-stu-id="3da2e-103">Tutorial: Azure Active Directory integration with Rightscale</span></span>

<span data-ttu-id="3da2e-104">В этом руководстве описано, как интегрировать Rightscale с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3da2e-104">In this tutorial, you learn how to integrate Rightscale with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3da2e-105">Интеграция Rightscale с Azure AD обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="3da2e-105">Integrating Rightscale with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3da2e-106">С помощью Azure AD вы можете контролировать доступ к Rightscale.</span><span class="sxs-lookup"><span data-stu-id="3da2e-106">You can control in Azure AD who has access to Rightscale</span></span>
- <span data-ttu-id="3da2e-107">Вы можете включить автоматический вход пользователей в Rightscale (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3da2e-107">You can enable your users to automatically get signed-on to Rightscale (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3da2e-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="3da2e-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="3da2e-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3da2e-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3da2e-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="3da2e-110">Prerequisites</span></span>

<span data-ttu-id="3da2e-111">Чтобы настроить интеграцию Azure AD с приложением Rightscale, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="3da2e-111">To configure Azure AD integration with Rightscale, you need the following items:</span></span>

- <span data-ttu-id="3da2e-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="3da2e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3da2e-113">подписка Rightscale с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="3da2e-113">A Rightscale single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3da2e-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="3da2e-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3da2e-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="3da2e-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3da2e-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="3da2e-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3da2e-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3da2e-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3da2e-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="3da2e-118">Scenario description</span></span>
<span data-ttu-id="3da2e-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="3da2e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3da2e-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="3da2e-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3da2e-121">Добавление Rightscale из коллекции.</span><span class="sxs-lookup"><span data-stu-id="3da2e-121">Adding Rightscale from the gallery</span></span>
2. <span data-ttu-id="3da2e-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="3da2e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-rightscale-from-the-gallery"></a><span data-ttu-id="3da2e-123">Добавление Rightscale из коллекции</span><span class="sxs-lookup"><span data-stu-id="3da2e-123">Adding Rightscale from the gallery</span></span>
<span data-ttu-id="3da2e-124">Чтобы настроить интеграцию Rightscale с Azure AD, необходимо добавить Rightscale из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="3da2e-124">To configure the integration of Rightscale into Azure AD, you need to add Rightscale from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3da2e-125">**Чтобы добавить Rightscale из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="3da2e-125">**To add Rightscale from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3da2e-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3da2e-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3da2e-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="3da2e-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3da2e-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="3da2e-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="3da2e-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="3da2e-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="3da2e-133">В поле поиска введите **Rightscale**.</span><span class="sxs-lookup"><span data-stu-id="3da2e-133">In the search box, type **Rightscale**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_search.png)

5. <span data-ttu-id="3da2e-135">На панели результатов выберите **Rightscale** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="3da2e-135">In the results panel, select **Rightscale**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3da2e-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="3da2e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3da2e-138">В этом разделе описана настройка и проверка единого входа Azure AD в Rightscale с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3da2e-138">In this section, you configure and test Azure AD single sign-on with Rightscale based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3da2e-139">Чтобы единый вход работал, Azure AD необходима информация о том, какой пользователь в Rightscale соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3da2e-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Rightscale is to a user in Azure AD.</span></span> <span data-ttu-id="3da2e-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Rightscale.</span><span class="sxs-lookup"><span data-stu-id="3da2e-140">In other words, a link relationship between an Azure AD user and the related user in Rightscale needs to be established.</span></span>

<span data-ttu-id="3da2e-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Rightscale.</span><span class="sxs-lookup"><span data-stu-id="3da2e-141">In Rightscale, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="3da2e-142">Чтобы настроить и проверить единый вход Azure AD в Rightscale, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="3da2e-142">To configure and test Azure AD single sign-on with Rightscale, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3da2e-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="3da2e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3da2e-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3da2e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3da2e-145">**[Создание тестового пользователя Rightscale](#creating-a-rightscale-test-user)** требуется для того, чтобы в Rightscale существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3da2e-145">**[Creating a Rightscale test user](#creating-a-rightscale-test-user)** - to have a counterpart of Britta Simon in Rightscale that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="3da2e-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3da2e-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3da2e-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="3da2e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3da2e-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="3da2e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3da2e-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Rightscale.</span><span class="sxs-lookup"><span data-stu-id="3da2e-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Rightscale application.</span></span>

<span data-ttu-id="3da2e-150">**Чтобы настроить единый вход Azure AD в Rightscale, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="3da2e-150">**To configure Azure AD single sign-on with Rightscale, perform the following steps:**</span></span>

1. <span data-ttu-id="3da2e-151">На портале Azure на странице интеграции с приложением **Rightscale** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="3da2e-151">In the Azure portal, on the **Rightscale** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="3da2e-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="3da2e-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_samlbase.png)

3. <span data-ttu-id="3da2e-155">Если вы хотите настроить приложение в **режиме, инициируемом IdP**, то в разделе **Домены и URL-адреса приложения Rightscale** не нужно ничего делать, так как это приложение уже предварительно интегрировано в Azure.</span><span class="sxs-lookup"><span data-stu-id="3da2e-155">On the **Rightscale Domain and URLs** section, if you wish to configure the application in **IDP initiated mode** you do not have to perform any steps as the app is already pre-integrated with Azure.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_url.png)

4. <span data-ttu-id="3da2e-157">В разделе **Домены и URL-адреса приложения Rightscale** выполните приведенные ниже действия, если вы хотите настроить приложение в **режиме, инициируемом поставщиком услуг**.</span><span class="sxs-lookup"><span data-stu-id="3da2e-157">On the **Rightscale Domain and URLs** section, if you wish to configure the application in **SP initiated mode**, perform the following steps:</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_url1.png)

    <span data-ttu-id="3da2e-159">а.</span><span class="sxs-lookup"><span data-stu-id="3da2e-159">a.</span></span> <span data-ttu-id="3da2e-160">Установите флажок **Показать дополнительные параметры URL-адресов**.</span><span class="sxs-lookup"><span data-stu-id="3da2e-160">Click on the **Show advanced URL settings**.</span></span>

    <span data-ttu-id="3da2e-161">b.</span><span class="sxs-lookup"><span data-stu-id="3da2e-161">b.</span></span> <span data-ttu-id="3da2e-162">В текстовое поле **URL-адрес для входа** введите URL-адрес `https://login.rightscale.com/`.</span><span class="sxs-lookup"><span data-stu-id="3da2e-162">In the **Sign On URL** textbox, type the URL: `https://login.rightscale.com/`</span></span>

5. <span data-ttu-id="3da2e-163">В разделе **Сертификат для подписи токена SAML** щелкните **Certificate (Base64)** (Сертификат (Base64)), а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="3da2e-163">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_certificate.png) 

6. <span data-ttu-id="3da2e-165">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="3da2e-165">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-rightscale-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="3da2e-167">В разделе **Конфигурация Rightscale** щелкните **Настроить Rightscale**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="3da2e-167">On the **Rightscale Configuration** section, click **Configure Rightscale** to open **Configure sign-on** window.</span></span> <span data-ttu-id="3da2e-168">Скопируйте **идентификатор сущности SAML и URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="3da2e-168">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    <span data-ttu-id="3da2e-169">![Настройка единого входа](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_configure.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="3da2e-169">![Configure Single Sign-On](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_configure.png) 
<CS></span></span>
8. <span data-ttu-id="3da2e-170">Чтобы настроить для приложения единый вход, нужно войти в клиент приложения RightScale с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="3da2e-170">To get SSO configured for your application, you need to sign-on to your RightScale tenant as an administrator.</span></span>

    <span data-ttu-id="3da2e-171">а.</span><span class="sxs-lookup"><span data-stu-id="3da2e-171">a.</span></span> <span data-ttu-id="3da2e-172">В меню в верхней части откройте вкладку **Параметры** и выберите **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="3da2e-172">In the menu on the top, click the **Settings** tab and select **Single Sign-On**.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_001.png) 

    <span data-ttu-id="3da2e-174">b.</span><span class="sxs-lookup"><span data-stu-id="3da2e-174">b.</span></span> <span data-ttu-id="3da2e-175">Нажмите кнопку **Новый** и добавьте свои поставщики удостоверений SAML в области **Your SAML Identity Providers** (Ваши поставщики удостоверений SAML).</span><span class="sxs-lookup"><span data-stu-id="3da2e-175">Click the "**new**" button to add **Your SAML Identity Providers**.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_002.png) 
 
    <span data-ttu-id="3da2e-177">В.</span><span class="sxs-lookup"><span data-stu-id="3da2e-177">c.</span></span> <span data-ttu-id="3da2e-178">В текстовом поле **Отображаемое имя** введите название своей компании.</span><span class="sxs-lookup"><span data-stu-id="3da2e-178">In the textbox of **Display Name**, input your company name.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_003.png)
 
    <span data-ttu-id="3da2e-180">d.</span><span class="sxs-lookup"><span data-stu-id="3da2e-180">d.</span></span> <span data-ttu-id="3da2e-181">Выберите **Allow RightScale-initiated SSO using a discovery hint** (Разрешить единый вход, инициированный RightScale, с использованием подсказки обнаружения) и в приведенном ниже текстовом поле введите **имя домена**.</span><span class="sxs-lookup"><span data-stu-id="3da2e-181">Select **Allow RightScale-initiated SSO using a discovery hint** and input your **domain name** in the below textbox.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_004.png)

    <span data-ttu-id="3da2e-183">д.</span><span class="sxs-lookup"><span data-stu-id="3da2e-183">e.</span></span> <span data-ttu-id="3da2e-184">В текстовое поле **SAML SSO Endpoint** (Конечная точка единого входа SAML) в Rightscale вставьте значение **SAML Single Sign-On Service URL** (URL-адрес службы единого входа SAML), скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="3da2e-184">Paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal into **SAML SSO Endpoint** in RightScale.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_006.png)

    <span data-ttu-id="3da2e-186">f.</span><span class="sxs-lookup"><span data-stu-id="3da2e-186">f.</span></span> <span data-ttu-id="3da2e-187">В текстовое поле **SAML EntityID** (Идентификатор сущности SAML) в Rightscale вставьте значение **SAML Entity ID** (Идентификатор сущности SAML), скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="3da2e-187">Paste the value of **SAML Entity ID** which you have copied from Azure portal into **SAML EntityID** in RightScale.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_008.png)

    <span data-ttu-id="3da2e-189">g.</span><span class="sxs-lookup"><span data-stu-id="3da2e-189">g.</span></span> <span data-ttu-id="3da2e-190">Нажмите кнопку **Browse** (Обзор), чтобы передать сертификат, скачанный с портала Azure.</span><span class="sxs-lookup"><span data-stu-id="3da2e-190">Click **Browser** button to upload the certificate which you downloaded from Azure portal.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_009.png)

    <span data-ttu-id="3da2e-192">h.</span><span class="sxs-lookup"><span data-stu-id="3da2e-192">h.</span></span> <span data-ttu-id="3da2e-193">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="3da2e-193">Click **Save**.</span></span>
<CE>
> [!TIP]
> <span data-ttu-id="3da2e-194">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="3da2e-194">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3da2e-195">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="3da2e-195">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3da2e-196">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="3da2e-196">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3da2e-197">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="3da2e-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="3da2e-198">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3da2e-198">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="3da2e-200">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="3da2e-200">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3da2e-201">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3da2e-201">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-rightscale-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3da2e-203">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="3da2e-203">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-rightscale-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3da2e-205">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="3da2e-205">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-rightscale-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3da2e-207">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="3da2e-207">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-rightscale-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3da2e-209">а.</span><span class="sxs-lookup"><span data-stu-id="3da2e-209">a.</span></span> <span data-ttu-id="3da2e-210">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3da2e-210">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3da2e-211">b.</span><span class="sxs-lookup"><span data-stu-id="3da2e-211">b.</span></span> <span data-ttu-id="3da2e-212">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="3da2e-212">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3da2e-213">c.</span><span class="sxs-lookup"><span data-stu-id="3da2e-213">c.</span></span> <span data-ttu-id="3da2e-214">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="3da2e-214">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="3da2e-215">d.</span><span class="sxs-lookup"><span data-stu-id="3da2e-215">d.</span></span> <span data-ttu-id="3da2e-216">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="3da2e-216">Click **Create**.</span></span>
 
### <a name="creating-a-rightscale-test-user"></a><span data-ttu-id="3da2e-217">Создание тестового пользователя Rightscale</span><span class="sxs-lookup"><span data-stu-id="3da2e-217">Creating a Rightscale test user</span></span>

<span data-ttu-id="3da2e-218">В этом разделе описано, как создать пользователя Britta Simon в приложении RightScale.</span><span class="sxs-lookup"><span data-stu-id="3da2e-218">In this section, you create a user called Britta Simon in RightScale.</span></span> <span data-ttu-id="3da2e-219">Обратитесь к [группе поддержки клиентов Rightscale](mailto:support@rightscale.com), чтобы добавить пользователей на платформу Rightscale.</span><span class="sxs-lookup"><span data-stu-id="3da2e-219">Work with [Rightscale Client support team](mailto:support@rightscale.com) to add the users in the RightScale platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="3da2e-220">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="3da2e-220">Assigning the Azure AD test user</span></span>

<span data-ttu-id="3da2e-221">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к Rightscale.</span><span class="sxs-lookup"><span data-stu-id="3da2e-221">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Rightscale.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="3da2e-223">**Чтобы назначить пользователя Britta Simon в Rightscale, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="3da2e-223">**To assign Britta Simon to Rightscale, perform the following steps:**</span></span>

1. <span data-ttu-id="3da2e-224">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="3da2e-224">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="3da2e-226">Из списка приложений выберите **Rightscale**.</span><span class="sxs-lookup"><span data-stu-id="3da2e-226">In the applications list, select **Rightscale**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-rightscale-tutorial/tutorial_rightscale_app.png) 

3. <span data-ttu-id="3da2e-228">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="3da2e-228">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="3da2e-230">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="3da2e-230">Click **Add** button.</span></span> <span data-ttu-id="3da2e-231">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="3da2e-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="3da2e-233">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="3da2e-233">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3da2e-234">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="3da2e-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3da2e-235">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="3da2e-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3da2e-236">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="3da2e-236">Testing single sign-on</span></span>

<span data-ttu-id="3da2e-237">Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="3da2e-237">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>  

<span data-ttu-id="3da2e-238">Щелкнув элемент RightScale на панели доступа, вы автоматически войдете в приложение RightScale.</span><span class="sxs-lookup"><span data-stu-id="3da2e-238">When you click the RightScale tile in the Access Panel, you should get automatically signed-on to your RightScale application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3da2e-239">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="3da2e-239">Additional resources</span></span>

* [<span data-ttu-id="3da2e-240">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3da2e-240">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3da2e-241">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3da2e-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rightscale-tutorial/tutorial_general_203.png

