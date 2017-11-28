---
title: "Руководство по интеграции Azure Active Directory с Optimizely | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и Optimizely."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 28ef03e1-9aad-4301-af97-d94e853edc74
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 4d6f6da6bace09fbd6ab105530a1162653675c99
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-optimizely"></a><span data-ttu-id="7bd36-103">Учебник. Интеграция Azure Active Directory с Optimizely</span><span class="sxs-lookup"><span data-stu-id="7bd36-103">Tutorial: Azure Active Directory integration with Optimizely</span></span>

<span data-ttu-id="7bd36-104">В этом учебнике описано, как интегрировать Optimizely с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="7bd36-104">In this tutorial, you learn how to integrate Optimizely with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="7bd36-105">Интеграция Azure AD с приложением Optimizely обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="7bd36-105">Integrating Optimizely with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="7bd36-106">С помощью Azure AD вы можете контролировать доступ к Optimizely.</span><span class="sxs-lookup"><span data-stu-id="7bd36-106">You can control in Azure AD who has access to Optimizely</span></span>
- <span data-ttu-id="7bd36-107">Вы можете включить автоматический вход пользователей в Optimizely (единый вход) с использованием их учетных записей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7bd36-107">You can enable your users to automatically get signed-on to Optimizely (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="7bd36-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="7bd36-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="7bd36-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="7bd36-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7bd36-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="7bd36-110">Prerequisites</span></span>

<span data-ttu-id="7bd36-111">Чтобы настроить интеграцию Azure AD с Optimizely, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="7bd36-111">To configure Azure AD integration with Optimizely, you need the following items:</span></span>

- <span data-ttu-id="7bd36-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="7bd36-112">An Azure AD subscription</span></span>
- <span data-ttu-id="7bd36-113">подписка Optimizely с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="7bd36-113">An Optimizely single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="7bd36-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="7bd36-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="7bd36-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="7bd36-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="7bd36-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="7bd36-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="7bd36-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7bd36-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="7bd36-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="7bd36-118">Scenario description</span></span>
<span data-ttu-id="7bd36-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="7bd36-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="7bd36-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="7bd36-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="7bd36-121">Добавление Optimizely из коллекции</span><span class="sxs-lookup"><span data-stu-id="7bd36-121">Adding Optimizely from the gallery</span></span>
2. <span data-ttu-id="7bd36-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="7bd36-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-optimizely-from-the-gallery"></a><span data-ttu-id="7bd36-123">Добавление Optimizely из коллекции</span><span class="sxs-lookup"><span data-stu-id="7bd36-123">Adding Optimizely from the gallery</span></span>
<span data-ttu-id="7bd36-124">Чтобы настроить интеграцию Optimizely с Azure AD, необходимо добавить Optimizely из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="7bd36-124">To configure the integration of Optimizely into Azure AD, you need to add Optimizely from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="7bd36-125">**Чтобы добавить Optimizely из коллекции, выполните следующие действия**</span><span class="sxs-lookup"><span data-stu-id="7bd36-125">**To add Optimizely from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="7bd36-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7bd36-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="7bd36-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="7bd36-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="7bd36-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="7bd36-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="7bd36-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="7bd36-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="7bd36-133">В поле поиска введите **Optimizely**.</span><span class="sxs-lookup"><span data-stu-id="7bd36-133">In the search box, type **Optimizely**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_search.png)

5. <span data-ttu-id="7bd36-135">На панели результатов выберите **Optimizely** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="7bd36-135">In the results panel, select **Optimizely**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="7bd36-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="7bd36-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="7bd36-138">В этом разделе описана настройка и проверка единого входа Azure AD в Optimizely с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7bd36-138">In this section, you configure and test Azure AD single sign-on with Optimizely based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="7bd36-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Optimizely соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7bd36-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Optimizely is to a user in Azure AD.</span></span> <span data-ttu-id="7bd36-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем Optimizely.</span><span class="sxs-lookup"><span data-stu-id="7bd36-140">In other words, a link relationship between an Azure AD user and the related user in Optimizely needs to be established.</span></span>

<span data-ttu-id="7bd36-141">Чтобы установить эту связь, следует назначить **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Optimizely.</span><span class="sxs-lookup"><span data-stu-id="7bd36-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Optimizely.</span></span>

<span data-ttu-id="7bd36-142">Чтобы настроить и проверить единый вход Azure AD в Optimizely, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="7bd36-142">To configure and test Azure AD single sign-on with Optimizely, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="7bd36-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="7bd36-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="7bd36-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7bd36-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="7bd36-145">**[Создание тестового пользователя Optimizely](#creating-an-optimizely-test-user)** требуется для создания в Optimizely пользователя Britta Simon, связанного с представлением этого же пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7bd36-145">**[Creating an Optimizely test user](#creating-an-optimizely-test-user)** - to have a counterpart of Britta Simon in Optimizely that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="7bd36-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7bd36-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="7bd36-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="7bd36-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="7bd36-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="7bd36-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="7bd36-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Optimizely.</span><span class="sxs-lookup"><span data-stu-id="7bd36-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Optimizely application.</span></span>

<span data-ttu-id="7bd36-150">**Чтобы настроить единый вход Azure AD в Optimizely, выполните следующие действия**</span><span class="sxs-lookup"><span data-stu-id="7bd36-150">**To configure Azure AD single sign-on with Optimizely, perform the following steps:**</span></span>

1. <span data-ttu-id="7bd36-151">На портале Azure на странице интеграции с приложением **Optimizely** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="7bd36-151">In the Azure portal, on the **Optimizely** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="7bd36-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="7bd36-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_samlbase.png)

3. <span data-ttu-id="7bd36-155">В разделе **Домен и URL-адреса приложения Optimizely** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="7bd36-155">On the **Optimizely Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_url.png)

    <span data-ttu-id="7bd36-157">а.</span><span class="sxs-lookup"><span data-stu-id="7bd36-157">a.</span></span> <span data-ttu-id="7bd36-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://app.optimizely.net/<instance name>`</span><span class="sxs-lookup"><span data-stu-id="7bd36-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://app.optimizely.net/<instance name>`</span></span>

    <span data-ttu-id="7bd36-159">b.</span><span class="sxs-lookup"><span data-stu-id="7bd36-159">b.</span></span> <span data-ttu-id="7bd36-160">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `urn:auth0:optimizely:contoso`</span><span class="sxs-lookup"><span data-stu-id="7bd36-160">In the **Identifier** textbox, type a URL using the following pattern:  `urn:auth0:optimizely:contoso`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7bd36-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="7bd36-161">These values are not the real.</span></span> <span data-ttu-id="7bd36-162">Их необходимо заменить на фактический URL-адрес ответа и идентификатор, что описывается далее в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="7bd36-162">You will update the value with the actual Sign-on URL and Identifier, which is explained later in the tutorial.</span></span> 

4. <span data-ttu-id="7bd36-163">В разделе **Сертификат подписи SAML** щелкните **Сертификат (Base64)**, а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="7bd36-163">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_certificate.png) 

5. <span data-ttu-id="7bd36-165">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="7bd36-165">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-optimizely-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="7bd36-167">В разделе **Настройка Optimizely** щелкните **Настроить Optimizely**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="7bd36-167">On the **Optimizely Configuration** section, click **Configure Optimizely** to open **Configure sign-on** window.</span></span> <span data-ttu-id="7bd36-168">Скопируйте **URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="7bd36-168">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_configure.png) 

7. <span data-ttu-id="7bd36-170">Чтобы настроить единый вход на стороне приложения **Optimizely**, обратитесь к менеджеру по технической поддержке Optimizely и предоставьте скачанный **сертификат (Base64)** и **URL-адрес службы единого входа SAML**.</span><span class="sxs-lookup"><span data-stu-id="7bd36-170">To configure single sign-on on **Optimizely** side, contact your Optimizely Account Manager and provide the downloaded **Certificate (Base64)**, and **SAML Single Sign-On Service URL**.</span></span> 

8. <span data-ttu-id="7bd36-171">В ответ на ваше электронное сообщение Optimizely предоставит URL-адрес входа (для единого входа, инициируемого поставщиком услуг) и идентификатор (идентификатор сущности поставщика службы).</span><span class="sxs-lookup"><span data-stu-id="7bd36-171">In response to your email, Optimizely provides you with the Sign On URL (SP-initiated SSO) and the Identifier (Service Provider Entity ID) values.</span></span>

    <span data-ttu-id="7bd36-172">а.</span><span class="sxs-lookup"><span data-stu-id="7bd36-172">a.</span></span> <span data-ttu-id="7bd36-173">Скопируйте **инициируемый SP URL-адрес единого входа**, предоставленный приложением Optimizely, и вставьте его в текстовое поле **URL-адрес входа** в разделе **Домен и URL-адреса приложения Optimizely** на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="7bd36-173">Copy the **SP-initiated SSO URL** provided by Optimizely, and paste into the **Sign On URL** textbox in **Optimizely Domain and URLs** section on Azure portal</span></span> 

    <span data-ttu-id="7bd36-174">b.</span><span class="sxs-lookup"><span data-stu-id="7bd36-174">b.</span></span> <span data-ttu-id="7bd36-175">Скопируйте **идентификатор сущности поставщика службы**, предоставленный приложением Optimizely, и вставьте его в текстовое поле **Идентификатор** в разделе **Домен и URL-адреса приложения Optimizely** на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="7bd36-175">Copy the **Service Provider Entity ID** provided by Optimizely, and paste into the **Identifier** textbox in **Optimizely Domain and URLs** section on Azure portal</span></span> 

9. <span data-ttu-id="7bd36-176">В отдельном окне браузера войдите в приложение Optimizely.</span><span class="sxs-lookup"><span data-stu-id="7bd36-176">In a different browser window, sign-on to your Optimizely application.</span></span>

10. <span data-ttu-id="7bd36-177">Щелкните имя своей учетной записи в верхнем правом углу, затем щелкните **Account Settings**(Параметры учетной записи).</span><span class="sxs-lookup"><span data-stu-id="7bd36-177">Click you account name in the top right corner and then **Account Settings**.</span></span>
   
    ![единого входа Azure AD](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_09.png)

11. <span data-ttu-id="7bd36-179">На вкладке "Account" (Учетная запись) установите флажок **Enable SSO** (Включить единый вход) в области Single Sign On (Единый вход) раздела **Overview** (Общие сведения).</span><span class="sxs-lookup"><span data-stu-id="7bd36-179">In the Account tab, check the box **Enable SSO** under Single Sign On in the **Overview** section.</span></span>
   
    ![единого входа Azure AD](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_10.png)
    
12. <span data-ttu-id="7bd36-181">Нажмите кнопку **Сохранить**</span><span class="sxs-lookup"><span data-stu-id="7bd36-181">Click **Save**</span></span>

> [!TIP]
> <span data-ttu-id="7bd36-182">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="7bd36-182">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="7bd36-183">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="7bd36-183">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="7bd36-184">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="7bd36-184">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="7bd36-185">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="7bd36-185">Creating an Azure AD test user</span></span>
<span data-ttu-id="7bd36-186">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7bd36-186">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="7bd36-188">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="7bd36-188">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="7bd36-189">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7bd36-189">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-optimizely-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="7bd36-191">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="7bd36-191">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-optimizely-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="7bd36-193">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="7bd36-193">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-optimizely-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="7bd36-195">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="7bd36-195">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-optimizely-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="7bd36-197">а.</span><span class="sxs-lookup"><span data-stu-id="7bd36-197">a.</span></span> <span data-ttu-id="7bd36-198">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="7bd36-198">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="7bd36-199">b.</span><span class="sxs-lookup"><span data-stu-id="7bd36-199">b.</span></span> <span data-ttu-id="7bd36-200">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="7bd36-200">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="7bd36-201">c.</span><span class="sxs-lookup"><span data-stu-id="7bd36-201">c.</span></span> <span data-ttu-id="7bd36-202">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="7bd36-202">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="7bd36-203">d.</span><span class="sxs-lookup"><span data-stu-id="7bd36-203">d.</span></span> <span data-ttu-id="7bd36-204">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="7bd36-204">Click **Create**.</span></span>
 
### <a name="creating-an-optimizely-test-user"></a><span data-ttu-id="7bd36-205">Создание тестового пользователя Optimizely</span><span class="sxs-lookup"><span data-stu-id="7bd36-205">Creating an Optimizely test user</span></span>

<span data-ttu-id="7bd36-206">В этом разделе описано, как создать пользователя Britta Simon в приложении Optimizely.</span><span class="sxs-lookup"><span data-stu-id="7bd36-206">In this section, you create a user called Britta Simon in Optimizely.</span></span>

1. <span data-ttu-id="7bd36-207">На домашней странице выберите вкладку **Collaborators** (Сотрудники).</span><span class="sxs-lookup"><span data-stu-id="7bd36-207">On the home page, select **Collaborators** tab.</span></span>

2. <span data-ttu-id="7bd36-208">Чтобы добавить в проект нового сотрудника, щелкните **New Collaborator** (Создать сотрудника).</span><span class="sxs-lookup"><span data-stu-id="7bd36-208">To add new collaborator to the project, click **New Collaborator**.</span></span>
   
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-optimizely-tutorial/create_aaduser_10.png)

3. <span data-ttu-id="7bd36-210">Введите электронный адрес и назначьте роль.</span><span class="sxs-lookup"><span data-stu-id="7bd36-210">Fill in the email address and assign them a role.</span></span> <span data-ttu-id="7bd36-211">Нажмите кнопку **Пригласить**.</span><span class="sxs-lookup"><span data-stu-id="7bd36-211">Click **Invite**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-optimizely-tutorial/create_aaduser_11.png)

4. <span data-ttu-id="7bd36-213">Он получит приглашение по электронной почте.</span><span class="sxs-lookup"><span data-stu-id="7bd36-213">They receive an email invite.</span></span> <span data-ttu-id="7bd36-214">Этот электронный адрес будет использоваться для входа в приложение Optimizely.</span><span class="sxs-lookup"><span data-stu-id="7bd36-214">Using the email address, they have to log in to Optimizely.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="7bd36-215">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="7bd36-215">Assigning the Azure AD test user</span></span>

<span data-ttu-id="7bd36-216">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure путем предоставления доступа к Optimizely.</span><span class="sxs-lookup"><span data-stu-id="7bd36-216">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Optimizely.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="7bd36-218">**Чтобы назначить пользователя Britta Simon в Optimizely, выполните следующие действия**</span><span class="sxs-lookup"><span data-stu-id="7bd36-218">**To assign Britta Simon to Optimizely, perform the following steps:**</span></span>

1. <span data-ttu-id="7bd36-219">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="7bd36-219">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="7bd36-221">Из списка приложений выберите **Optimizely**.</span><span class="sxs-lookup"><span data-stu-id="7bd36-221">In the applications list, select **Optimizely**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-optimizely-tutorial/tutorial_optimizely_app.png) 

3. <span data-ttu-id="7bd36-223">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="7bd36-223">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="7bd36-225">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="7bd36-225">Click **Add** button.</span></span> <span data-ttu-id="7bd36-226">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="7bd36-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="7bd36-228">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="7bd36-228">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="7bd36-229">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="7bd36-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="7bd36-230">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="7bd36-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="7bd36-231">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="7bd36-231">Testing single sign-on</span></span>

<span data-ttu-id="7bd36-232">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="7bd36-232">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="7bd36-233">Щелкнув элемент "Optimizely" на панели доступа, вы автоматически войдете в приложение Optimizely.</span><span class="sxs-lookup"><span data-stu-id="7bd36-233">When you click the Optimizely tile in the Access Panel, you should get automatically signed-on to your Optimizely application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="7bd36-234">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="7bd36-234">Additional resources</span></span>

* [<span data-ttu-id="7bd36-235">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7bd36-235">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="7bd36-236">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="7bd36-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-optimizely-tutorial/tutorial_general_203.png

