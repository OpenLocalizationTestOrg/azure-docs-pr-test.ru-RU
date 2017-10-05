---
title: "Руководство. Интеграция Azure Active Directory с HappyFox | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и HappyFox."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8204ee77-f64b-4fac-b64a-25ea534feac0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: jeedes
ms.openlocfilehash: 8b5ad750d7849e4037ed7ee93c48b5645c68e799
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-happyfox"></a><span data-ttu-id="51b41-103">Руководство. Интеграция Azure Active Directory с HappyFox</span><span class="sxs-lookup"><span data-stu-id="51b41-103">Tutorial: Azure Active Directory integration with HappyFox</span></span>

<span data-ttu-id="51b41-104">В этом руководстве описано, как интегрировать HappyFox с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="51b41-104">In this tutorial, you learn how to integrate HappyFox with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="51b41-105">Интеграция приложения HappyFox с Azure AD обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="51b41-105">Integrating HappyFox with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="51b41-106">С помощью Azure AD вы можете контролировать, у кого есть доступ к приложению HappyFox.</span><span class="sxs-lookup"><span data-stu-id="51b41-106">You can control in Azure AD who has access to HappyFox</span></span>
- <span data-ttu-id="51b41-107">Вы можете включить автоматический вход пользователей в HappyFox (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="51b41-107">You can enable your users to automatically get signed-on to HappyFox (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="51b41-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="51b41-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="51b41-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="51b41-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="51b41-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="51b41-110">Prerequisites</span></span>

<span data-ttu-id="51b41-111">Чтобы настроить интеграцию Azure AD с HappyFox, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="51b41-111">To configure Azure AD integration with HappyFox, you need the following items:</span></span>

- <span data-ttu-id="51b41-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="51b41-112">An Azure AD subscription</span></span>
- <span data-ttu-id="51b41-113">подписка HappyFox с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="51b41-113">A HappyFox single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="51b41-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="51b41-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="51b41-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="51b41-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="51b41-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="51b41-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="51b41-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="51b41-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="51b41-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="51b41-118">Scenario description</span></span>
<span data-ttu-id="51b41-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="51b41-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="51b41-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="51b41-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="51b41-121">Добавление HappyFox из коллекции.</span><span class="sxs-lookup"><span data-stu-id="51b41-121">Adding HappyFox from the gallery</span></span>
2. <span data-ttu-id="51b41-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="51b41-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-happyfox-from-the-gallery"></a><span data-ttu-id="51b41-123">Добавление HappyFox из коллекции</span><span class="sxs-lookup"><span data-stu-id="51b41-123">Adding HappyFox from the gallery</span></span>
<span data-ttu-id="51b41-124">Чтобы настроить интеграцию приложения HappyFox с Azure AD, вам нужно добавить это приложение из коллекции в свой список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="51b41-124">To configure the integration of HappyFox into Azure AD, you need to add HappyFox from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="51b41-125">**Добавление приложения HappyFox из коллекции**</span><span class="sxs-lookup"><span data-stu-id="51b41-125">**To add HappyFox from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="51b41-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="51b41-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="51b41-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="51b41-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="51b41-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="51b41-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="51b41-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="51b41-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="51b41-133">В поле поиска введите **HappyFox**.</span><span class="sxs-lookup"><span data-stu-id="51b41-133">In the search box, type **HappyFox**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_search.png)

5. <span data-ttu-id="51b41-135">На панели результатов выберите **HappyFox** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="51b41-135">In the results panel, select **HappyFox**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="51b41-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="51b41-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="51b41-138">В этом разделе описана настройка и проверка единого входа Azure AD в HappyFox с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="51b41-138">In this section, you configure and test Azure AD single sign-on with HappyFox based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="51b41-139">Для работы единого входа службе Azure AD нужно знать, какой пользователь в HappyFox соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="51b41-139">For single sign-on to work, Azure AD needs to know what the counterpart user in HappyFox is to a user in Azure AD.</span></span> <span data-ttu-id="51b41-140">Иными словами, нужно установить связь между пользователем Azure AD и соответствующим пользователем в HappyFox.</span><span class="sxs-lookup"><span data-stu-id="51b41-140">In other words, a link relationship between an Azure AD user and the related user in HappyFox needs to be established.</span></span>

<span data-ttu-id="51b41-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в HappyFox.</span><span class="sxs-lookup"><span data-stu-id="51b41-141">In HappyFox, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="51b41-142">Чтобы настроить и проверить единый вход Azure AD в HappyFox, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="51b41-142">To configure and test Azure AD single sign-on with HappyFox, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="51b41-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="51b41-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="51b41-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="51b41-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="51b41-145">**[Создание тестового пользователя HappyFox](#creating-a-happyfox-test-user)** требуется для создания в HappyFox пользователя Britta Simon, связанного с представлением этого пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="51b41-145">**[Creating a HappyFox test user](#creating-a-happyfox-test-user)** - to have a counterpart of Britta Simon in HappyFox that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="51b41-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="51b41-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="51b41-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="51b41-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="51b41-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="51b41-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="51b41-149">В этом разделе мы включим на портале Azure единый вход Azure AD и настроим его в приложении HappyFox.</span><span class="sxs-lookup"><span data-stu-id="51b41-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your HappyFox application.</span></span>

<span data-ttu-id="51b41-150">**Настройка единого входа Azure AD в HappyFox**</span><span class="sxs-lookup"><span data-stu-id="51b41-150">**To configure Azure AD single sign-on with HappyFox, perform the following steps:**</span></span>

1. <span data-ttu-id="51b41-151">На портале Azure на странице интеграции с приложением **HappyFox** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="51b41-151">In the Azure portal, on the **HappyFox** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="51b41-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="51b41-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_samlbase.png)

3. <span data-ttu-id="51b41-155">В разделе **Домены и URL-адреса приложения HappyFox** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="51b41-155">On the **HappyFox Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_url.png)

    <span data-ttu-id="51b41-157">а.</span><span class="sxs-lookup"><span data-stu-id="51b41-157">a.</span></span> <span data-ttu-id="51b41-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<subdomain>.happyfox.com/`</span><span class="sxs-lookup"><span data-stu-id="51b41-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.happyfox.com/`</span></span>

    <span data-ttu-id="51b41-159">b.</span><span class="sxs-lookup"><span data-stu-id="51b41-159">b.</span></span> <span data-ttu-id="51b41-160">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<subdomain>.happyfox.com/saml/metadata/`</span><span class="sxs-lookup"><span data-stu-id="51b41-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.happyfox.com/saml/metadata/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="51b41-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="51b41-161">These values are not real.</span></span> <span data-ttu-id="51b41-162">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="51b41-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="51b41-163">Чтобы получить их, обратитесь в [службу поддержки клиентов HappyFox](https://support.happyfox.com/home).</span><span class="sxs-lookup"><span data-stu-id="51b41-163">Contact [HappyFox Client support team](https://support.happyfox.com/home) to get these values.</span></span> 
 
4. <span data-ttu-id="51b41-164">В разделе **Сертификат подписи SAML** щелкните **Сертификат (Base64)**, а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="51b41-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the Certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_certificate.png) 

5. <span data-ttu-id="51b41-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="51b41-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-happyfox-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="51b41-168">В разделе **Конфигурация HappyFox** щелкните **Настроить HappyFox**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="51b41-168">On the **HappyFox Configuration** section, click **Configure HappyFox** to open **Configure sign-on** window.</span></span> <span data-ttu-id="51b41-169">Скопируйте **URL-адрес службы единого входа SAML** из раздела **Quick Reference** (Краткий справочник).</span><span class="sxs-lookup"><span data-stu-id="51b41-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_configure.png) 

7. <span data-ttu-id="51b41-171">Войдите на портал HappyFox для сотрудников, перейдите к разделу **Manage** (Управление) и щелкните вкладку **Integrations** (Интеграция).</span><span class="sxs-lookup"><span data-stu-id="51b41-171">Sign on to your HappyFox staff portal and navigate to **Manage**, Click on **Integrations** tab.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-happyfox-tutorial/header.png) 

8. <span data-ttu-id="51b41-173">На вкладке Integrations (Интеграция) щелкните **Configure** (Настройка) в разделе **SAML Integration** (Интеграция SAML), чтобы открыть параметры единого входа.</span><span class="sxs-lookup"><span data-stu-id="51b41-173">In the Integrations tab, Click **Configure** under **SAML Integration** to open the Single Sign On Settings.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-happyfox-tutorial/configure.png) 

9. <span data-ttu-id="51b41-175">В разделе конфигурации SAML вставьте **URL-адрес службы единого входа SAML**, скопированный на портале Azure, в текстовое поле **SSO Target URL** (Целевой URL-адрес единого входа).</span><span class="sxs-lookup"><span data-stu-id="51b41-175">Inside SAML configuration section, paste the **SAML Single Sign-On Service URL** that you have copied from Azure portal into **SSO Target URL** textbox.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-happyfox-tutorial/targeturl.png)

10. <span data-ttu-id="51b41-177">Откройте в Блокноте сертификат, загруженный с портала Azure, и вставьте его содержимое в раздел **IdP Signature** (Подпись поставщика удостоверений).</span><span class="sxs-lookup"><span data-stu-id="51b41-177">Open the certificate downloaded from Azure portal in notepad and paste its content in **IdP Signature** section.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-happyfox-tutorial/cert.png)

11. <span data-ttu-id="51b41-179">Нажмите кнопку **Save Settings** (Сохранить параметры).</span><span class="sxs-lookup"><span data-stu-id="51b41-179">Click **Save Settings** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-happyfox-tutorial/savesettings.png)

> [!TIP]
> <span data-ttu-id="51b41-181">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="51b41-181">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="51b41-182">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="51b41-182">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="51b41-183">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="51b41-183">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="51b41-184">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="51b41-184">Creating an Azure AD test user</span></span>
<span data-ttu-id="51b41-185">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="51b41-185">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="51b41-187">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="51b41-187">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="51b41-188">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="51b41-188">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-happyfox-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="51b41-190">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="51b41-190">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-happyfox-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="51b41-192">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="51b41-192">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-happyfox-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="51b41-194">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="51b41-194">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-happyfox-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="51b41-196">а.</span><span class="sxs-lookup"><span data-stu-id="51b41-196">a.</span></span> <span data-ttu-id="51b41-197">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="51b41-197">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="51b41-198">b.</span><span class="sxs-lookup"><span data-stu-id="51b41-198">b.</span></span> <span data-ttu-id="51b41-199">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="51b41-199">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="51b41-200">c.</span><span class="sxs-lookup"><span data-stu-id="51b41-200">c.</span></span> <span data-ttu-id="51b41-201">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="51b41-201">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="51b41-202">d.</span><span class="sxs-lookup"><span data-stu-id="51b41-202">d.</span></span> <span data-ttu-id="51b41-203">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="51b41-203">Click **Create**.</span></span>
 
### <a name="creating-a-happyfox-test-user"></a><span data-ttu-id="51b41-204">Создание тестового пользователя HappyFox</span><span class="sxs-lookup"><span data-stu-id="51b41-204">Creating a HappyFox test user</span></span>

<span data-ttu-id="51b41-205">Приложение поддерживает JIT-подготовку пользователей, поэтому после проверки подлинности пользователи будут созданы в приложении автоматически.</span><span class="sxs-lookup"><span data-stu-id="51b41-205">Application supports Just in time user provisioning and after authentication users are created in the application automatically.</span></span>
        
### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="51b41-206">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="51b41-206">Assigning the Azure AD test user</span></span>

<span data-ttu-id="51b41-207">В этом разделе мы разрешим пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к HappyFox.</span><span class="sxs-lookup"><span data-stu-id="51b41-207">In this section, you enable Britta Simon to use Azure single sign-on by granting access to HappyFox.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="51b41-209">**Назначение пользователя Britta Simon приложению HappyFox**</span><span class="sxs-lookup"><span data-stu-id="51b41-209">**To assign Britta Simon to HappyFox, perform the following steps:**</span></span>

1. <span data-ttu-id="51b41-210">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="51b41-210">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="51b41-212">В списке приложений выберите **HappyFox**.</span><span class="sxs-lookup"><span data-stu-id="51b41-212">In the applications list, select **HappyFox**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-happyfox-tutorial/tutorial_happyfox_app.png) 

3. <span data-ttu-id="51b41-214">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="51b41-214">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="51b41-216">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="51b41-216">Click **Add** button.</span></span> <span data-ttu-id="51b41-217">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="51b41-217">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="51b41-219">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="51b41-219">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="51b41-220">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="51b41-220">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="51b41-221">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="51b41-221">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="51b41-222">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="51b41-222">Testing single sign-on</span></span>

<span data-ttu-id="51b41-223">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="51b41-223">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

1. <span data-ttu-id="51b41-224">Когда вы нажмете плитку HappyFox на панели доступа, должна появиться страница входа в приложение HappyFox.</span><span class="sxs-lookup"><span data-stu-id="51b41-224">When you click the HappyFox tile in the Access Panel, you should get login page of HappyFox application.</span></span> <span data-ttu-id="51b41-225">На этой странице входа вы увидите кнопку **SAML**.</span><span class="sxs-lookup"><span data-stu-id="51b41-225">You should see the **‘SAML’** button on the sign-in page.</span></span>

    ![Подключаемый модуль](./media/active-directory-saas-happyfox-tutorial/saml.png) 

2. <span data-ttu-id="51b41-227">Нажмите кнопку **SAML**, чтобы войти в HappyFox с помощью учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="51b41-227">Click the **‘SAML’** button to log in to HappyFox using your Azure AD account.</span></span>

<span data-ttu-id="51b41-228">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="51b41-228">For more information about the Access Panel, see [introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="51b41-229">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="51b41-229">Additional resources</span></span>

* [<span data-ttu-id="51b41-230">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="51b41-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="51b41-231">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="51b41-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-happyfox-tutorial/tutorial_general_203.png

