---
title: "Руководство по интеграции Azure Active Directory с Aravo | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и Aravo."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 224939d8-2c9c-4561-968d-62722f5ab5ed
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: 2b6da25a22463619180f635954660e6efeef62ce
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-aravo"></a><span data-ttu-id="48caa-103">Руководство. Интеграция Azure Active Directory с Aravo</span><span class="sxs-lookup"><span data-stu-id="48caa-103">Tutorial: Azure Active Directory integration with Aravo</span></span>

<span data-ttu-id="48caa-104">В этом руководстве описано, как интегрировать Aravo с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="48caa-104">In this tutorial, you learn how to integrate Aravo with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="48caa-105">Интеграция Azure AD с приложением Aravo обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="48caa-105">Integrating Aravo with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="48caa-106">С помощью Azure AD вы можете контролировать доступ к Aravo.</span><span class="sxs-lookup"><span data-stu-id="48caa-106">You can control in Azure AD who has access to Aravo</span></span>
- <span data-ttu-id="48caa-107">Вы можете включить автоматический вход пользователей в Aravo (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="48caa-107">You can enable your users to automatically get signed-on to Aravo (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="48caa-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="48caa-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="48caa-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="48caa-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="48caa-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="48caa-110">Prerequisites</span></span>

<span data-ttu-id="48caa-111">Чтобы настроить интеграцию Azure AD с Aravo, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="48caa-111">To configure Azure AD integration with Aravo, you need the following items:</span></span>

- <span data-ttu-id="48caa-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="48caa-112">An Azure AD subscription</span></span>
- <span data-ttu-id="48caa-113">подписка Aravo с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="48caa-113">An Aravo single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="48caa-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="48caa-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="48caa-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="48caa-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="48caa-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="48caa-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="48caa-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="48caa-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="48caa-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="48caa-118">Scenario description</span></span>
<span data-ttu-id="48caa-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="48caa-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="48caa-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="48caa-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="48caa-121">Добавление Aravo из коллекции.</span><span class="sxs-lookup"><span data-stu-id="48caa-121">Adding Aravo from the gallery</span></span>
2. <span data-ttu-id="48caa-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="48caa-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-aravo-from-the-gallery"></a><span data-ttu-id="48caa-123">Добавление Aravo из коллекции.</span><span class="sxs-lookup"><span data-stu-id="48caa-123">Adding Aravo from the gallery</span></span>
<span data-ttu-id="48caa-124">Чтобы настроить интеграцию Aravo с Azure AD, необходимо добавить Aravo из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="48caa-124">To configure the integration of Aravo into Azure AD, you need to add Aravo from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="48caa-125">**Чтобы добавить Aravo из коллекции, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="48caa-125">**To add Aravo from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="48caa-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="48caa-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="48caa-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="48caa-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="48caa-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="48caa-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="48caa-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="48caa-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="48caa-133">В поле поиска введите **Aravo**.</span><span class="sxs-lookup"><span data-stu-id="48caa-133">In the search box, type **Aravo**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-aravo-tutorial/tutorial_aravo_search.png)

5. <span data-ttu-id="48caa-135">На панели результатов выберите **Aravo** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="48caa-135">In the results panel, select **Aravo**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-aravo-tutorial/tutorial_aravo_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="48caa-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="48caa-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="48caa-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложение Aravo с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="48caa-138">In this section, you configure and test Azure AD single sign-on with Aravo based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="48caa-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Aravo соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="48caa-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Aravo is to a user in Azure AD.</span></span> <span data-ttu-id="48caa-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Aravo.</span><span class="sxs-lookup"><span data-stu-id="48caa-140">In other words, a link relationship between an Azure AD user and the related user in Aravo needs to be established.</span></span>

<span data-ttu-id="48caa-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Aravo.</span><span class="sxs-lookup"><span data-stu-id="48caa-141">In Aravo, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="48caa-142">Чтобы настроить и проверить единый вход Azure AD в Aravo, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="48caa-142">To configure and test Azure AD single sign-on with Aravo, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="48caa-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="48caa-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="48caa-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="48caa-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="48caa-145">**[Создание тестового пользователя Aravo](#creating-an-aravo-test-user)** нужно для того, чтобы в Aravo также существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="48caa-145">**[Creating an Aravo test user](#creating-an-aravo-test-user)** - to have a counterpart of Britta Simon in Aravo that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="48caa-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="48caa-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="48caa-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="48caa-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="48caa-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="48caa-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="48caa-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Aravo.</span><span class="sxs-lookup"><span data-stu-id="48caa-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Aravo application.</span></span>

<span data-ttu-id="48caa-150">**Чтобы настроить единый вход Azure AD в Aravo, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="48caa-150">**To configure Azure AD single sign-on with Aravo, perform the following steps:**</span></span>

1. <span data-ttu-id="48caa-151">На портале Azure на странице интеграции с приложением **Aravo** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="48caa-151">In the Azure portal, on the **Aravo** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="48caa-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="48caa-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-aravo-tutorial/tutorial_aravo_samlbase.png)

3. <span data-ttu-id="48caa-155">В разделе **Домены и URL-адреса приложения Aravo** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="48caa-155">On the **Aravo Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-aravo-tutorial/tutorial_aravo_url.png)

    <span data-ttu-id="48caa-157">а.</span><span class="sxs-lookup"><span data-stu-id="48caa-157">a.</span></span> <span data-ttu-id="48caa-158">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<companyname>.aravo.com`</span><span class="sxs-lookup"><span data-stu-id="48caa-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.aravo.com`</span></span>

    <span data-ttu-id="48caa-159">b.</span><span class="sxs-lookup"><span data-stu-id="48caa-159">b.</span></span> <span data-ttu-id="48caa-160">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате: `https://<companyname>.aravo.com/aems/login.do`.</span><span class="sxs-lookup"><span data-stu-id="48caa-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.aravo.com/aems/login.do`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="48caa-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="48caa-161">These values are not real.</span></span> <span data-ttu-id="48caa-162">Измените их на фактические значения идентификатора и URL-адреса ответа.</span><span class="sxs-lookup"><span data-stu-id="48caa-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="48caa-163">Чтобы получить эти значения, обратитесь к [группе поддержки Aravo](http://www.aravo.com/about-us/contact/).</span><span class="sxs-lookup"><span data-stu-id="48caa-163">Contact [Aravo support team](http://www.aravo.com/about-us/contact/) to get these values.</span></span>
 
4. <span data-ttu-id="48caa-164">В разделе **Сертификат для подписи токена SAML** щелкните **Certificate (Base64)** (Сертификат (Base64)), а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="48caa-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-aravo-tutorial/tutorial_aravo_certificate.png) 

5. <span data-ttu-id="48caa-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="48caa-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-aravo-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="48caa-168">В разделе **Конфигурация Aravo** щелкните **Настроить Aravo**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="48caa-168">On the **Aravo Configuration** section, click **Configure Aravo** to open **Configure sign-on** window.</span></span> <span data-ttu-id="48caa-169">Скопируйте **URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML**  из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="48caa-169">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-aravo-tutorial/tutorial_aravo_configure.png) 

7. <span data-ttu-id="48caa-171">Чтобы настроить единый вход на стороне **Aravo**, нужно отправить скачанный **сертификат (Base64)**, **URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML** [группе поддержки Aravo](http://www.aravo.com/about-us/contact/).</span><span class="sxs-lookup"><span data-stu-id="48caa-171">To configure single sign-on on **Aravo** side, you need to send the downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Aravo support team](http://www.aravo.com/about-us/contact/).</span></span> 


> [!TIP]
> <span data-ttu-id="48caa-172">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="48caa-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="48caa-173">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="48caa-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="48caa-174">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="48caa-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="48caa-175">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="48caa-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="48caa-176">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="48caa-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="48caa-178">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="48caa-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="48caa-179">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="48caa-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-aravo-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="48caa-181">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="48caa-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-aravo-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="48caa-183">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="48caa-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-aravo-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="48caa-185">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="48caa-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-aravo-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="48caa-187">а.</span><span class="sxs-lookup"><span data-stu-id="48caa-187">a.</span></span> <span data-ttu-id="48caa-188">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="48caa-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="48caa-189">b.</span><span class="sxs-lookup"><span data-stu-id="48caa-189">b.</span></span> <span data-ttu-id="48caa-190">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="48caa-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="48caa-191">c.</span><span class="sxs-lookup"><span data-stu-id="48caa-191">c.</span></span> <span data-ttu-id="48caa-192">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="48caa-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="48caa-193">d.</span><span class="sxs-lookup"><span data-stu-id="48caa-193">d.</span></span> <span data-ttu-id="48caa-194">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="48caa-194">Click **Create**.</span></span>
 
### <a name="creating-an-aravo-test-user"></a><span data-ttu-id="48caa-195">Создание тестового пользователя Aravo</span><span class="sxs-lookup"><span data-stu-id="48caa-195">Creating an Aravo test user</span></span>

<span data-ttu-id="48caa-196">Цель этого раздела — создать пользователя с именем Britta Simon в приложении Aravo.</span><span class="sxs-lookup"><span data-stu-id="48caa-196">The objective of this section is to create a user called Britta Simon in Aravo.</span></span> <span data-ttu-id="48caa-197">Обратитесь к [группе поддержки Aravo](http://www.aravo.com/about-us/contact/), чтобы добавить пользователей в учетную запись Aravo.</span><span class="sxs-lookup"><span data-stu-id="48caa-197">Work with [Aravo support team](http://www.aravo.com/about-us/contact/) to add the users in the Aravo account.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="48caa-198">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="48caa-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="48caa-199">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к Aravo.</span><span class="sxs-lookup"><span data-stu-id="48caa-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Aravo.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="48caa-201">**Чтобы назначить пользователя Britta Simon в Aravo, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="48caa-201">**To assign Britta Simon to Aravo, perform the following steps:**</span></span>

1. <span data-ttu-id="48caa-202">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="48caa-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="48caa-204">В списке приложений выберите **Aravo**.</span><span class="sxs-lookup"><span data-stu-id="48caa-204">In the applications list, select **Aravo**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-aravo-tutorial/tutorial_aravo_app.png) 

3. <span data-ttu-id="48caa-206">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="48caa-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="48caa-208">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="48caa-208">Click **Add** button.</span></span> <span data-ttu-id="48caa-209">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="48caa-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="48caa-211">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="48caa-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="48caa-212">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="48caa-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="48caa-213">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="48caa-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="48caa-214">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="48caa-214">Testing single sign-on</span></span>

<span data-ttu-id="48caa-215">Цель этого раздела — проверить конфигурацию единого входа Microsoft Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="48caa-215">The objective of this section is to test your Microsoft Azure AD Single Sign-On configuration using the Access Panel.</span></span>

<span data-ttu-id="48caa-216">Щелкнув элемент Aravo на панели доступа, вы автоматически войдете в приложение Aravo.</span><span class="sxs-lookup"><span data-stu-id="48caa-216">When you click the Aravo tile in the Access Panel, you should get automatically signed-on to your Aravo application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="48caa-217">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="48caa-217">Additional resources</span></span>

* [<span data-ttu-id="48caa-218">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="48caa-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="48caa-219">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="48caa-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-aravo-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-aravo-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-aravo-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-aravo-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-aravo-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-aravo-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-aravo-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-aravo-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-aravo-tutorial/tutorial_general_203.png

