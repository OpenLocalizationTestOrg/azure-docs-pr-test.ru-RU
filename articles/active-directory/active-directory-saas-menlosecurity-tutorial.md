---
title: "Руководство по интеграции Azure Active Directory с Menlo Security | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в Menlo Security."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9e63fe6b-0ad0-405d-9e41-6a1a40a41df8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: jeedes
ms.openlocfilehash: 75366abafa551d21630b0edddb65db23b9ea9d42
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-menlo-security"></a><span data-ttu-id="881a6-103">Руководство по интеграции Azure Active Directory с Menlo Security</span><span class="sxs-lookup"><span data-stu-id="881a6-103">Tutorial: Azure Active Directory integration with Menlo Security</span></span>

<span data-ttu-id="881a6-104">В этом руководстве описано, как интегрировать Menlo Security с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="881a6-104">In this tutorial, you learn how to integrate Menlo Security with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="881a6-105">Интеграция Menlo Security с Azure AD имеет следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="881a6-105">Integrating Menlo Security with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="881a6-106">С помощью Azure AD вы можете контролировать, у кого есть доступ к приложению Menlo Security.</span><span class="sxs-lookup"><span data-stu-id="881a6-106">You can control in Azure AD who has access to Menlo Security</span></span>
- <span data-ttu-id="881a6-107">Вы можете включить автоматический вход пользователей в Menlo Security (единый вход) с помощью учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="881a6-107">You can enable your users to automatically get signed-on to Menlo Security (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="881a6-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="881a6-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="881a6-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в статье</span><span class="sxs-lookup"><span data-stu-id="881a6-109">If you want to know more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="881a6-110">[Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="881a6-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="881a6-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="881a6-111">Prerequisites</span></span>

<span data-ttu-id="881a6-112">Чтобы настроить интеграцию Azure AD с приложением Menlo Security, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="881a6-112">To configure Azure AD integration with Menlo Security, you need the following items:</span></span>

- <span data-ttu-id="881a6-113">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="881a6-113">An Azure AD subscription</span></span>
- <span data-ttu-id="881a6-114">подписка Menlo Security с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="881a6-114">A Menlo Security single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="881a6-115">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="881a6-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="881a6-116">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="881a6-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="881a6-117">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="881a6-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="881a6-118">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="881a6-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="881a6-119">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="881a6-119">Scenario description</span></span>
<span data-ttu-id="881a6-120">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="881a6-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="881a6-121">Сценарий, описанный в этом руководстве, состоит из двух стандартных блоков.</span><span class="sxs-lookup"><span data-stu-id="881a6-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="881a6-122">Добавление Menlo Security из коллекции</span><span class="sxs-lookup"><span data-stu-id="881a6-122">Adding Menlo Security from the gallery</span></span>
2. <span data-ttu-id="881a6-123">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="881a6-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-menlo-security-from-the-gallery"></a><span data-ttu-id="881a6-124">Добавление Menlo Security из коллекции</span><span class="sxs-lookup"><span data-stu-id="881a6-124">Adding Menlo Security from the gallery</span></span>
<span data-ttu-id="881a6-125">Чтобы настроить интеграцию приложения Menlo Security с Azure AD, вам нужно добавить это приложение из коллекции в свой список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="881a6-125">To configure the integration of Menlo Security into Azure AD, you need to add Menlo Security from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="881a6-126">**Добавление приложения Menlo Security из коллекции**</span><span class="sxs-lookup"><span data-stu-id="881a6-126">**To add Menlo Security from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="881a6-127">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="881a6-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="881a6-129">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="881a6-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="881a6-130">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="881a6-130">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="881a6-132">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="881a6-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="881a6-134">В поле поиска введите **Menlo Security**.</span><span class="sxs-lookup"><span data-stu-id="881a6-134">In the search box, type **Menlo Security**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_search.png)

5. <span data-ttu-id="881a6-136">На панели результатов выберите **Menlo Security** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="881a6-136">In the results panel, select **Menlo Security**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="881a6-138">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="881a6-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="881a6-139">В этом разделе описана настройка и проверка единого входа Azure AD в Menlo Security с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="881a6-139">In this section, you configure and test Azure AD single sign-on with Menlo Security based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="881a6-140">Для работы единого входа службе Azure AD нужно знать, какой пользователь в Menlo Security соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="881a6-140">For single sign-on to work, Azure AD needs to know what the counterpart user in Menlo Security is to a user in Azure AD.</span></span> <span data-ttu-id="881a6-141">Иными словами, нужно установить связь между пользователем Azure AD и соответствующим пользователем вMenlo Security.</span><span class="sxs-lookup"><span data-stu-id="881a6-141">In other words, a link relationship between an Azure AD user and the related user in Menlo Security needs to be established.</span></span>

<span data-ttu-id="881a6-142">Чтобы установить эту связь, следует назначить **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Menlo Security.</span><span class="sxs-lookup"><span data-stu-id="881a6-142">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Menlo Security.</span></span>

<span data-ttu-id="881a6-143">Чтобы настроить и проверить единый вход Azure AD в Menlo Security, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="881a6-143">To configure and test Azure AD single sign-on with Menlo Security, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="881a6-144">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="881a6-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="881a6-145">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="881a6-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="881a6-146">**[Создание тестового пользователя Menlo Security](#creating-a-menlo-security-test-user)** требуется для создания пользователя Britta Simon в Menlo Security, связанного с соответствующим представлением в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="881a6-146">**[Creating a Menlo Security test user](#creating-a-menlo-security-test-user)** - to have a counterpart of Britta Simon in Menlo Security that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="881a6-147">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход Azure AD.</span><span class="sxs-lookup"><span data-stu-id="881a6-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="881a6-148">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="881a6-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="881a6-149">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="881a6-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="881a6-150">В этом разделе мы включим на портале Azure единый вход Azure AD и настроим его в приложении Menlo Security.</span><span class="sxs-lookup"><span data-stu-id="881a6-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Menlo Security application.</span></span>

<span data-ttu-id="881a6-151">**Настройка единого входа Azure AD в Menlo Security**</span><span class="sxs-lookup"><span data-stu-id="881a6-151">**To configure Azure AD single sign-on with Menlo Security, perform the following steps:**</span></span>

1. <span data-ttu-id="881a6-152">На портале Azure на странице интеграции с приложением **Menlo Security** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="881a6-152">In the Azure portal, on the **Menlo Security** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="881a6-154">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="881a6-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_samlbase.png)

3. <span data-ttu-id="881a6-156">В разделе **Домены и URL-адреса приложения Menlo Security** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="881a6-156">On the **Menlo Security Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_url.png)

    <span data-ttu-id="881a6-158">а.</span><span class="sxs-lookup"><span data-stu-id="881a6-158">a.</span></span> <span data-ttu-id="881a6-159">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<subdomain>.menlosecurity.com/account/login`</span><span class="sxs-lookup"><span data-stu-id="881a6-159">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.menlosecurity.com/account/login`</span></span>

    <span data-ttu-id="881a6-160">b.</span><span class="sxs-lookup"><span data-stu-id="881a6-160">b.</span></span> <span data-ttu-id="881a6-161">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<subdomain>.menlosecurity.com/safeview-auth-server/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="881a6-161">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.menlosecurity.com/safeview-auth-server/saml/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="881a6-162">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="881a6-162">These values are not the real.</span></span> <span data-ttu-id="881a6-163">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="881a6-163">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="881a6-164">Чтобы получить эти значения, обратитесь в [службу поддержки клиентов Menlo Security](https://www.menlosecurity.com/menlo-contact).</span><span class="sxs-lookup"><span data-stu-id="881a6-164">Contact [Menlo Security Client support team](https://www.menlosecurity.com/menlo-contact) to get these values.</span></span> 
 
4. <span data-ttu-id="881a6-165">В разделе **Сертификат подписи SAML** щелкните **Сертификат (Base64)**, а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="881a6-165">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the Certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_certificate.png) 

5. <span data-ttu-id="881a6-167">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="881a6-167">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="881a6-169">В разделе **Настройка Menlo Security** щелкните **Настроить Menlo Security**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="881a6-169">On the **Menlo Security Configuration** section, click **Configure Menlo Security** to open **Configure sign-on** window.</span></span> <span data-ttu-id="881a6-170">Скопируйте **идентификатор сущности SAML** и **URL-адрес службы единого входа SAML** из раздела **Quick Reference** (Краткий справочник).</span><span class="sxs-lookup"><span data-stu-id="881a6-170">Copy the **SAML Entity ID**, and **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_configure.png) 

7. <span data-ttu-id="881a6-172">Чтобы настроить единый вход в приложении **Menlo Security**, войдите на соответствующий сайт **Menlo Security** в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="881a6-172">To configure single sign-on on **Menlo Security** side, login to the **Menlo Security** website as an administrator.</span></span>

8. <span data-ttu-id="881a6-173">В разделе **Параметры** выберите **Проверка подлинности** и выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="881a6-173">Under **Settings** go to **Authentication** and perform following actions:</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-menlosecurity-tutorial/menlo_user_setup.png)

    <span data-ttu-id="881a6-175">а.</span><span class="sxs-lookup"><span data-stu-id="881a6-175">a.</span></span> <span data-ttu-id="881a6-176">Установите флажок **Enable user authentication using SAML** (Включить проверку подлинности пользователя с помощью SAML).</span><span class="sxs-lookup"><span data-stu-id="881a6-176">Tick the checkbox **Enable user authentication using SAML**.</span></span>

    <span data-ttu-id="881a6-177">b.</span><span class="sxs-lookup"><span data-stu-id="881a6-177">b.</span></span> <span data-ttu-id="881a6-178">Задайте для параметра **Allow External Access** (Разрешить внешний доступ) значение **Да**.</span><span class="sxs-lookup"><span data-stu-id="881a6-178">Select **Allow External Access** to **Yes**.</span></span>

    <span data-ttu-id="881a6-179">c.</span><span class="sxs-lookup"><span data-stu-id="881a6-179">c.</span></span> <span data-ttu-id="881a6-180">В разделе **SAML Provider** (Поставщик SAML) выберите **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="881a6-180">Under **SAML Provider**, select **Azure Active Directory**.</span></span>

    <span data-ttu-id="881a6-181">г)</span><span class="sxs-lookup"><span data-stu-id="881a6-181">d.</span></span> <span data-ttu-id="881a6-182">**SAML 2.0 Endpoint** (Конечная точка SAML 2.0). Вставьте **URL-адрес службы единого входа SAML**, скопированный на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="881a6-182">**SAML 2.0 Endpoint** : Paste the **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="881a6-183">д.</span><span class="sxs-lookup"><span data-stu-id="881a6-183">e.</span></span> <span data-ttu-id="881a6-184">**Service Identifier (Issuer)** (Идентификатор службы (издатель)). Вставьте **идентификатор сущности SAML**, скопированный на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="881a6-184">**Service Identifier (Issuer)** : Paste the **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="881a6-185">f.</span><span class="sxs-lookup"><span data-stu-id="881a6-185">f.</span></span> <span data-ttu-id="881a6-186">**Сертификат X.509**. Откройте **сертификат (Base64)**, скачанный на портале Azure, в Блокноте и вставьте его в это поле.</span><span class="sxs-lookup"><span data-stu-id="881a6-186">**X.509 Certificate** : Open the **Certificate (Base64)** downloaded from the Azure Portal in notepad and paste it in this box.</span></span>

    <span data-ttu-id="881a6-187">g.</span><span class="sxs-lookup"><span data-stu-id="881a6-187">g.</span></span> <span data-ttu-id="881a6-188">Нажмите кнопку **Сохранить** , чтобы сохранить параметры.</span><span class="sxs-lookup"><span data-stu-id="881a6-188">Click **Save** to save the settings.</span></span>

> [!TIP]
> <span data-ttu-id="881a6-189">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="881a6-189">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="881a6-190">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="881a6-190">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="881a6-191">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="881a6-191">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="881a6-192">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="881a6-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="881a6-193">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="881a6-193">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="881a6-195">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="881a6-195">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="881a6-196">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="881a6-196">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="881a6-198">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="881a6-198">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="881a6-200">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="881a6-200">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="881a6-202">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="881a6-202">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="881a6-204">а.</span><span class="sxs-lookup"><span data-stu-id="881a6-204">a.</span></span> <span data-ttu-id="881a6-205">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="881a6-205">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="881a6-206">b.</span><span class="sxs-lookup"><span data-stu-id="881a6-206">b.</span></span> <span data-ttu-id="881a6-207">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="881a6-207">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="881a6-208">c.</span><span class="sxs-lookup"><span data-stu-id="881a6-208">c.</span></span> <span data-ttu-id="881a6-209">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="881a6-209">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="881a6-210">d.</span><span class="sxs-lookup"><span data-stu-id="881a6-210">d.</span></span> <span data-ttu-id="881a6-211">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="881a6-211">Click **Create**.</span></span>
 
### <a name="creating-a-menlo-security-test-user"></a><span data-ttu-id="881a6-212">Создание тестового пользователя Menlo Security</span><span class="sxs-lookup"><span data-stu-id="881a6-212">Creating a Menlo Security test user</span></span>
 
<span data-ttu-id="881a6-213">В этом разделе описано, как создать пользователя Britta Simon в приложении Menlo Security.</span><span class="sxs-lookup"><span data-stu-id="881a6-213">In this section, you create a user called Britta Simon in Menlo Security.</span></span> <span data-ttu-id="881a6-214">Обратитесь в [службу поддержки клиентов Menlo Security](https://www.menlosecurity.com/menlo-contact), чтобы добавить пользователей на платформу Menlo Security.</span><span class="sxs-lookup"><span data-stu-id="881a6-214">Work with [Menlo Security Client support team](https://www.menlosecurity.com/menlo-contact) to add the users in the Menlo Security platform.</span></span> <span data-ttu-id="881a6-215">Перед использованием единого входа необходимо создать и активировать пользователей.</span><span class="sxs-lookup"><span data-stu-id="881a6-215">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="881a6-216">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="881a6-216">Assigning the Azure AD test user</span></span>

<span data-ttu-id="881a6-217">В этом разделе мы разрешим пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к Menlo Security.</span><span class="sxs-lookup"><span data-stu-id="881a6-217">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Menlo Security.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="881a6-219">**Назначение пользователя Britta Simon приложению Menlo Security**</span><span class="sxs-lookup"><span data-stu-id="881a6-219">**To assign Britta Simon to Menlo Security, perform the following steps:**</span></span>

1. <span data-ttu-id="881a6-220">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="881a6-220">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="881a6-222">В списке приложений выберите **Menlo Security**.</span><span class="sxs-lookup"><span data-stu-id="881a6-222">In the applications list, select **Menlo Security**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_app.png) 

3. <span data-ttu-id="881a6-224">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="881a6-224">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="881a6-226">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="881a6-226">Click **Add** button.</span></span> <span data-ttu-id="881a6-227">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="881a6-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="881a6-229">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="881a6-229">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="881a6-230">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="881a6-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="881a6-231">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="881a6-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="881a6-232">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="881a6-232">Testing single sign-on</span></span>

<span data-ttu-id="881a6-233">В этом разделе описано, как проверить конфигурацию единого входа Azure AD.</span><span class="sxs-lookup"><span data-stu-id="881a6-233">In this section, you test your Azure AD single sign-on configuration.</span></span>

<span data-ttu-id="881a6-234">Откройте браузер в режиме инкогнито или InPrivate, чтобы начать новый сеанс аутентификации.</span><span class="sxs-lookup"><span data-stu-id="881a6-234">Open a browser window in an "InPrivate" or "Incognito" mode to trigger a new authentication.</span></span>  <span data-ttu-id="881a6-235">В Internet Explorer нажмите клавиши CTRL+SHIFT+P.</span><span class="sxs-lookup"><span data-stu-id="881a6-235">In Internet Explorer, use Ctrl+Shift+P.</span></span>  <span data-ttu-id="881a6-236">В Chrome нажмите клавиши CTRL+SHIFT+N.</span><span class="sxs-lookup"><span data-stu-id="881a6-236">In Chrome, use Ctrl+Shift+N.</span></span>  <span data-ttu-id="881a6-237">В режиме конфиденциального просмотра перейдите к защищенному ресурсу и войдите в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="881a6-237">In the private browsing window, browse to a protected resource and perform an Azure AD login.</span></span>  <span data-ttu-id="881a6-238">После успешного входа нужный сайт откроется в отдельном сеансе.</span><span class="sxs-lookup"><span data-stu-id="881a6-238">Upon successful login, you will be taken to the requested site in an isolation session.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="881a6-239">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="881a6-239">Additional resources</span></span>

* [<span data-ttu-id="881a6-240">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="881a6-240">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="881a6-241">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="881a6-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_203.png

