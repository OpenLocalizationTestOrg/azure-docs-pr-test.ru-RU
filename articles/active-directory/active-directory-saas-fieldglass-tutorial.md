---
title: "Руководство по интеграции Azure Active Directory с Fieldglass | Документация Майкрософт"
description: "Сведения о настройке единого входа Azure Active Directory в Fieldglass."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2510195f-d5b1-4684-b3da-283fb8619df2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: 18926dd88b19cd672f11ae05f18e354e79a6b397
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-fieldglass"></a><span data-ttu-id="5c12c-103">Руководство по интеграции Azure Active Directory с Fieldglass</span><span class="sxs-lookup"><span data-stu-id="5c12c-103">Tutorial: Azure Active Directory integration with Fieldglass</span></span>

<span data-ttu-id="5c12c-104">В этом учебнике описано, как интегрировать приложение Fieldglass с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5c12c-104">In this tutorial, you learn how to integrate Fieldglass with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5c12c-105">Интеграция Azure AD с приложением Fieldglass обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="5c12c-105">Integrating Fieldglass with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5c12c-106">С помощью Azure AD вы можете контролировать доступ к Fieldglass.</span><span class="sxs-lookup"><span data-stu-id="5c12c-106">You can control in Azure AD who has access to Fieldglass</span></span>
- <span data-ttu-id="5c12c-107">Вы можете включить автоматический вход пользователей в Fieldglass (единый вход) с применением учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5c12c-107">You can enable your users to automatically get signed-on to Fieldglass (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5c12c-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="5c12c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="5c12c-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5c12c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5c12c-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="5c12c-110">Prerequisites</span></span>

<span data-ttu-id="5c12c-111">Чтобы настроить интеграцию Azure AD с Fieldglass, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="5c12c-111">To configure Azure AD integration with Fieldglass, you need the following items:</span></span>

- <span data-ttu-id="5c12c-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="5c12c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5c12c-113">подписка на Fieldglass с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="5c12c-113">A Fieldglass single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5c12c-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="5c12c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5c12c-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="5c12c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5c12c-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="5c12c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5c12c-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5c12c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5c12c-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="5c12c-118">Scenario description</span></span>
<span data-ttu-id="5c12c-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="5c12c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5c12c-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="5c12c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5c12c-121">Добавление Fieldglass из коллекции.</span><span class="sxs-lookup"><span data-stu-id="5c12c-121">Adding Fieldglass from the gallery</span></span>
2. <span data-ttu-id="5c12c-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="5c12c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-fieldglass-from-the-gallery"></a><span data-ttu-id="5c12c-123">Добавление Fieldglass из коллекции</span><span class="sxs-lookup"><span data-stu-id="5c12c-123">Adding Fieldglass from the gallery</span></span>
<span data-ttu-id="5c12c-124">Чтобы настроить интеграцию Fieldglass с Azure AD, необходимо добавить Fieldglass из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="5c12c-124">To configure the integration of Fieldglass into Azure AD, you need to add Fieldglass from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5c12c-125">**Чтобы добавить Fieldglass из коллекции, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="5c12c-125">**To add Fieldglass from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5c12c-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5c12c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5c12c-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="5c12c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5c12c-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="5c12c-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="5c12c-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="5c12c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="5c12c-133">В поле поиска введите **Fieldglass**.</span><span class="sxs-lookup"><span data-stu-id="5c12c-133">In the search box, type **Fieldglass**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-fieldglass-tutorial/tutorial_fieldglass_search.png)

5. <span data-ttu-id="5c12c-135">На панели результатов выберите **Fieldglass** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="5c12c-135">In the results panel, select **Fieldglass**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-fieldglass-tutorial/tutorial_fieldglass_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5c12c-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="5c12c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5c12c-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложение Fieldglass для тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5c12c-138">In this section, you configure and test Azure AD single sign-on with Fieldglass based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="5c12c-139">Для настройки единого входа Azure AD необходимо знать, какой пользователь в Fieldglass соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5c12c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Fieldglass is to a user in Azure AD.</span></span> <span data-ttu-id="5c12c-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Fieldglass.</span><span class="sxs-lookup"><span data-stu-id="5c12c-140">In other words, a link relationship between an Azure AD user and the related user in Fieldglass needs to be established.</span></span>

<span data-ttu-id="5c12c-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Fieldglass.</span><span class="sxs-lookup"><span data-stu-id="5c12c-141">In Fieldglass, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="5c12c-142">Чтобы настроить и проверить единый вход Azure AD в Fieldglass, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="5c12c-142">To configure and test Azure AD single sign-on with Fieldglass, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5c12c-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="5c12c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5c12c-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5c12c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5c12c-145">**[Создание тестового пользователя Fieldglass](#creating-a-fieldglass-test-user)** требуется для создания пользователя Britta Simon в Fieldglass, связанного с представлением этого пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5c12c-145">**[Creating a Fieldglass test user](#creating-a-fieldglass-test-user)** - to have a counterpart of Britta Simon in Fieldglass that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="5c12c-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5c12c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5c12c-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="5c12c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5c12c-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="5c12c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5c12c-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Fieldglass.</span><span class="sxs-lookup"><span data-stu-id="5c12c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Fieldglass application.</span></span>

<span data-ttu-id="5c12c-150">**Чтобы настроить единый вход Azure AD в Fieldglass, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="5c12c-150">**To configure Azure AD single sign-on with Fieldglass, perform the following steps:**</span></span>

1. <span data-ttu-id="5c12c-151">На портале Azure на странице интеграции с приложением **Fieldglass** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="5c12c-151">In the Azure portal, on the **Fieldglass** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="5c12c-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="5c12c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-fieldglass-tutorial/tutorial_fieldglass_samlbase.png)

3. <span data-ttu-id="5c12c-155">В разделе **Домены и URL-адреса Fieldglass** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="5c12c-155">On the **Fieldglass Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-fieldglass-tutorial/tutorial_fieldglass_url.png)

    <span data-ttu-id="5c12c-157">а.</span><span class="sxs-lookup"><span data-stu-id="5c12c-157">a.</span></span> <span data-ttu-id="5c12c-158">В текстовом поле **Идентификатор** введите URL-адрес `https://www.fieldglass.com` или URL-адрес в следующем формате: `https://<company name>.fgvms.com`</span><span class="sxs-lookup"><span data-stu-id="5c12c-158">In the **Identifier** textbox, type a URL as  `https://www.fieldglass.com` or follow the pattern:  `https://<company name>.fgvms.com`</span></span>

    <span data-ttu-id="5c12c-159">b.</span><span class="sxs-lookup"><span data-stu-id="5c12c-159">b.</span></span> <span data-ttu-id="5c12c-160">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="5c12c-160">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://www.fieldglass.net/<company name>`|
    | `https://<company name>.fgvms.com/<company name>`|

    > [!NOTE] 
    > <span data-ttu-id="5c12c-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="5c12c-161">These values are not real.</span></span> <span data-ttu-id="5c12c-162">Измените их на фактические значения идентификатора и URL-адреса ответа.</span><span class="sxs-lookup"><span data-stu-id="5c12c-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="5c12c-163">Чтобы получить эти значения, обратитесь в [службу поддержки Fieldglass](http://www.fieldglass.com/solutions/support).</span><span class="sxs-lookup"><span data-stu-id="5c12c-163">Contact [Fieldglass support team](http://www.fieldglass.com/solutions/support) to get these values.</span></span>
 
4. <span data-ttu-id="5c12c-164">В разделе **Сертификат подписи SAML** щелкните **Сертификат (Base64)**, а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="5c12c-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-fieldglass-tutorial/tutorial_fieldglass_certificate.png) 

5. <span data-ttu-id="5c12c-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="5c12c-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-fieldglass-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5c12c-168">В разделе **Настройка Fieldglass** щелкните **Настроить Fieldglass**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="5c12c-168">On the **Fieldglass Configuration** section, click **Configure Fieldglass** to open **Configure sign-on** window.</span></span> <span data-ttu-id="5c12c-169">Скопируйте **URL-адрес выхода и идентификатор сущности SAM** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="5c12c-169">Copy the **Sign-Out URL and SAML Entity ID** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-fieldglass-tutorial/tutorial_fieldglass_configure.png) 

7. <span data-ttu-id="5c12c-171">Для настройки единого входа на стороне **Fieldglass** необходимо отправить загруженный **сертификат (Base64)**, а также **URL-адрес выхода и идентификатор сущности SAML** в [службу поддержки Fieldglass](http://www.fieldglass.com/solutions/support).</span><span class="sxs-lookup"><span data-stu-id="5c12c-171">To configure single sign-on on **Fieldglass** side, you need to send the downloaded **Certificate(Base64)** and **Sign-Out URL, SAML Entity ID** to [Fieldglass support team](http://www.fieldglass.com/solutions/support).</span></span> <span data-ttu-id="5c12c-172">Специалисты службы поддержки настроят подключение единого входа SAML на обеих сторонах подключения.</span><span class="sxs-lookup"><span data-stu-id="5c12c-172">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="5c12c-173">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="5c12c-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="5c12c-174">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="5c12c-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="5c12c-175">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="5c12c-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5c12c-176">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="5c12c-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="5c12c-177">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5c12c-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="5c12c-179">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="5c12c-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5c12c-180">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5c12c-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-fieldglass-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5c12c-182">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="5c12c-182">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-fieldglass-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5c12c-184">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="5c12c-184">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-fieldglass-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5c12c-186">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="5c12c-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-fieldglass-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5c12c-188">а.</span><span class="sxs-lookup"><span data-stu-id="5c12c-188">a.</span></span> <span data-ttu-id="5c12c-189">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5c12c-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5c12c-190">b.</span><span class="sxs-lookup"><span data-stu-id="5c12c-190">b.</span></span> <span data-ttu-id="5c12c-191">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5c12c-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5c12c-192">c.</span><span class="sxs-lookup"><span data-stu-id="5c12c-192">c.</span></span> <span data-ttu-id="5c12c-193">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="5c12c-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="5c12c-194">d.</span><span class="sxs-lookup"><span data-stu-id="5c12c-194">d.</span></span> <span data-ttu-id="5c12c-195">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="5c12c-195">Click **Create**.</span></span>
 
### <a name="creating-a-fieldglass-test-user"></a><span data-ttu-id="5c12c-196">Создание тестового пользователя Fieldglass</span><span class="sxs-lookup"><span data-stu-id="5c12c-196">Creating a Fieldglass test user</span></span>

<span data-ttu-id="5c12c-197">Цель этого раздела — создать пользователя с именем Britta Simon в FieldGlass.</span><span class="sxs-lookup"><span data-stu-id="5c12c-197">The objective of this section is to create a user called Britta Simon in FieldGlass.</span></span> <span data-ttu-id="5c12c-198">Обратитесь в [службу поддержки FieldGlass](http://www.fieldglass.com/solutions/support), чтобы добавить пользователей в учетную запись FieldGlass.</span><span class="sxs-lookup"><span data-stu-id="5c12c-198">Please work with your [Fieldglass support team](http://www.fieldglass.com/solutions/support) to add the users in the Fieldglass account.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="5c12c-199">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="5c12c-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="5c12c-200">В этом разделе описано, как включить единый вход Azure для пользователя Britta Simon, предоставив этому пользователю доступ к Fieldglass.</span><span class="sxs-lookup"><span data-stu-id="5c12c-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Fieldglass.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="5c12c-202">**Чтобы назначить пользователя Britta Simon в Fieldglass, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="5c12c-202">**To assign Britta Simon to Fieldglass, perform the following steps:**</span></span>

1. <span data-ttu-id="5c12c-203">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="5c12c-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="5c12c-205">В списке приложений выберите **Fieldglass**.</span><span class="sxs-lookup"><span data-stu-id="5c12c-205">In the applications list, select **Fieldglass**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-fieldglass-tutorial/tutorial_fieldglass_app.png) 

3. <span data-ttu-id="5c12c-207">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="5c12c-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="5c12c-209">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="5c12c-209">Click **Add** button.</span></span> <span data-ttu-id="5c12c-210">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="5c12c-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="5c12c-212">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="5c12c-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5c12c-213">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="5c12c-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5c12c-214">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="5c12c-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5c12c-215">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="5c12c-215">Testing single sign-on</span></span>

<span data-ttu-id="5c12c-216">Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="5c12c-216">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="5c12c-217">Щелкнув плитку Fieldglass на панели доступа, вы автоматически войдете в приложение Fieldglass.</span><span class="sxs-lookup"><span data-stu-id="5c12c-217">When you click the Fieldglass tile in the Access Panel, you should get automatically signed-on to your Fieldglass application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5c12c-218">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="5c12c-218">Additional resources</span></span>

* [<span data-ttu-id="5c12c-219">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5c12c-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5c12c-220">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5c12c-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-fieldglass-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-fieldglass-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-fieldglass-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-fieldglass-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-fieldglass-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-fieldglass-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-fieldglass-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-fieldglass-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-fieldglass-tutorial/tutorial_general_203.png

