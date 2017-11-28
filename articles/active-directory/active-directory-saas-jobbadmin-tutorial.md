---
title: "Руководство по интеграции Azure Active Directory с Jobbadmin | Документы Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в приложении Jobbadmin."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c5208b0d-66a3-49ed-9aad-70d21f54aee0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: 848a6d6d0f072bc3f697ff57756714fc45e7dcc4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jobbadmin"></a><span data-ttu-id="05e97-103">Руководство по интеграции Azure Active Directory с Jobbadmin</span><span class="sxs-lookup"><span data-stu-id="05e97-103">Tutorial: Azure Active Directory integration with Jobbadmin</span></span>

<span data-ttu-id="05e97-104">В этом руководстве описано, как интегрировать Jobbadmin с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="05e97-104">In this tutorial, you learn how to integrate Jobbadmin with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="05e97-105">Интеграция Azure AD с приложением Jobbadmin обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="05e97-105">Integrating Jobbadmin with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="05e97-106">С помощью Azure AD вы можете контролировать доступ к Jobbadmin.</span><span class="sxs-lookup"><span data-stu-id="05e97-106">You can control in Azure AD who has access to Jobbadmin</span></span>
- <span data-ttu-id="05e97-107">Вы можете включить автоматический вход пользователей в Jobbadmin (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="05e97-107">You can enable your users to automatically get signed-on to Jobbadmin (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="05e97-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="05e97-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="05e97-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="05e97-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="05e97-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="05e97-110">Prerequisites</span></span>

<span data-ttu-id="05e97-111">Чтобы настроить интеграцию Azure AD с Jobbadmin, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="05e97-111">To configure Azure AD integration with Jobbadmin, you need the following items:</span></span>

- <span data-ttu-id="05e97-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="05e97-112">An Azure AD subscription</span></span>
- <span data-ttu-id="05e97-113">подписка на Jobbadmin с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="05e97-113">A Jobbadmin single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="05e97-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="05e97-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="05e97-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="05e97-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="05e97-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="05e97-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="05e97-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="05e97-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="05e97-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="05e97-118">Scenario description</span></span>
<span data-ttu-id="05e97-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="05e97-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="05e97-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="05e97-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="05e97-121">Добавление Jobbadmin из коллекции</span><span class="sxs-lookup"><span data-stu-id="05e97-121">Adding Jobbadmin from the gallery</span></span>
2. <span data-ttu-id="05e97-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="05e97-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jobbadmin-from-the-gallery"></a><span data-ttu-id="05e97-123">Добавление Jobbadmin из коллекции</span><span class="sxs-lookup"><span data-stu-id="05e97-123">Adding Jobbadmin from the gallery</span></span>
<span data-ttu-id="05e97-124">Чтобы настроить интеграцию Jobbadmin с Azure AD, необходимо добавить Jobbadmin из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="05e97-124">To configure the integration of Jobbadmin into Azure AD, you need to add Jobbadmin from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="05e97-125">**Чтобы добавить Jobbadmin из коллекции, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="05e97-125">**To add Jobbadmin from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="05e97-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="05e97-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="05e97-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="05e97-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="05e97-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="05e97-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="05e97-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="05e97-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="05e97-133">В поле поиска введите **Jobbadmin**.</span><span class="sxs-lookup"><span data-stu-id="05e97-133">In the search box, type **Jobbadmin**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jobbadmin-tutorial/tutorial_jobbadmin_search.png)

5. <span data-ttu-id="05e97-135">На панели результатов выберите **Jobbadmin** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="05e97-135">In the results panel, select **Jobbadmin**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jobbadmin-tutorial/tutorial_jobbadmin_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="05e97-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="05e97-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="05e97-138">В этом разделе описана настройка и проверка единого входа Azure AD в Jobbadmin с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="05e97-138">In this section, you configure and test Azure AD single sign-on with Jobbadmin based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="05e97-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Jobbadmin соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="05e97-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Jobbadmin is to a user in Azure AD.</span></span> <span data-ttu-id="05e97-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Jobbadmin.</span><span class="sxs-lookup"><span data-stu-id="05e97-140">In other words, a link relationship between an Azure AD user and the related user in Jobbadmin needs to be established.</span></span>

<span data-ttu-id="05e97-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Jobbadmin.</span><span class="sxs-lookup"><span data-stu-id="05e97-141">In Jobbadmin, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="05e97-142">Чтобы настроить и проверить единый вход Azure AD в Jobbadmin, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="05e97-142">To configure and test Azure AD single sign-on with Jobbadmin, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="05e97-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="05e97-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="05e97-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="05e97-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="05e97-145">**[Создание тестового пользователя Jobbadmin](#creating-a-jobbadmin-test-user)** требуется для создания в Jobbadmin пользователя Britta Simon, связанного с представлением этого пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="05e97-145">**[Creating a Jobbadmin test user](#creating-a-jobbadmin-test-user)** - to have a counterpart of Britta Simon in Jobbadmin that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="05e97-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="05e97-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="05e97-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="05e97-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="05e97-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="05e97-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="05e97-149">В этом разделе описано, как включить единый вход Azure AD на новом портале Azure и настроить его в приложении Jobbadmin.</span><span class="sxs-lookup"><span data-stu-id="05e97-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Jobbadmin application.</span></span>

<span data-ttu-id="05e97-150">**Чтобы настроить единый вход Azure AD в Jobbadmin, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="05e97-150">**To configure Azure AD single sign-on with Jobbadmin, perform the following steps:**</span></span>

1. <span data-ttu-id="05e97-151">На портале Azure на странице интеграции с приложением **Jobbadmin** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="05e97-151">In the Azure portal, on the **Jobbadmin** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="05e97-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="05e97-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-jobbadmin-tutorial/tutorial_jobbadmin_samlbase.png)

3. <span data-ttu-id="05e97-155">В разделе **Домены и URL-адреса приложения Jobbadmin** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="05e97-155">On the **Jobbadmin Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-jobbadmin-tutorial/tutorial_jobbadmin_url.png)

    <span data-ttu-id="05e97-157">а.</span><span class="sxs-lookup"><span data-stu-id="05e97-157">a.</span></span> <span data-ttu-id="05e97-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<instancename>.jobbnorge.no/auth/saml2/login.ashx`</span><span class="sxs-lookup"><span data-stu-id="05e97-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<instancename>.jobbnorge.no/auth/saml2/login.ashx`</span></span>

    <span data-ttu-id="05e97-159">b.</span><span class="sxs-lookup"><span data-stu-id="05e97-159">b.</span></span> <span data-ttu-id="05e97-160">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<instancename>.jobnorge.no`</span><span class="sxs-lookup"><span data-stu-id="05e97-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<instancename>.jobnorge.no`</span></span>

    <span data-ttu-id="05e97-161">c.</span><span class="sxs-lookup"><span data-stu-id="05e97-161">c.</span></span> <span data-ttu-id="05e97-162">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате: `https://<instancename>.jobbnorge.no/auth/saml2/login.ashx`.</span><span class="sxs-lookup"><span data-stu-id="05e97-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://<instancename>.jobbnorge.no/auth/saml2/login.ashx`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="05e97-163">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="05e97-163">These values are not real.</span></span> <span data-ttu-id="05e97-164">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="05e97-164">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="05e97-165">Чтобы получить их, обратитесь в [службу поддержки клиентов Jobbadmin](https://www.jobbnorge.no/om-oss/kontakt-oss).</span><span class="sxs-lookup"><span data-stu-id="05e97-165">Contact [Jobbadmin Client support team](https://www.jobbnorge.no/om-oss/kontakt-oss) to get these values.</span></span> 
 


4. <span data-ttu-id="05e97-166">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="05e97-166">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-jobbadmin-tutorial/tutorial_jobbadmin_certificate.png) 

5. <span data-ttu-id="05e97-168">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="05e97-168">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="05e97-170">Чтобы настроить единый вход на стороне **Jobbadmin**, отправьте скачанный **XML-файл метаданных** в [службу поддержки Jobbadmin](https://www.jobbnorge.no/om-oss/kontakt-oss).</span><span class="sxs-lookup"><span data-stu-id="05e97-170">To configure single sign-on on **Jobbadmin** side, you need to send the downloaded **Metadata XML** to [Jobbadmin support team](https://www.jobbnorge.no/om-oss/kontakt-oss).</span></span> <span data-ttu-id="05e97-171">Специалисты службы поддержки настроят подключение единого входа SAML на обеих сторонах подключения.</span><span class="sxs-lookup"><span data-stu-id="05e97-171">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="05e97-172">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="05e97-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="05e97-173">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="05e97-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="05e97-174">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="05e97-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="05e97-175">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="05e97-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="05e97-176">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="05e97-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="05e97-178">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="05e97-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="05e97-179">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="05e97-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jobbadmin-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="05e97-181">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="05e97-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jobbadmin-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="05e97-183">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="05e97-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jobbadmin-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="05e97-185">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="05e97-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jobbadmin-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="05e97-187">а.</span><span class="sxs-lookup"><span data-stu-id="05e97-187">a.</span></span> <span data-ttu-id="05e97-188">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="05e97-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="05e97-189">b.</span><span class="sxs-lookup"><span data-stu-id="05e97-189">b.</span></span> <span data-ttu-id="05e97-190">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="05e97-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="05e97-191">c.</span><span class="sxs-lookup"><span data-stu-id="05e97-191">c.</span></span> <span data-ttu-id="05e97-192">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="05e97-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="05e97-193">d.</span><span class="sxs-lookup"><span data-stu-id="05e97-193">d.</span></span> <span data-ttu-id="05e97-194">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="05e97-194">Click **Create**.</span></span>
 
### <a name="creating-a-jobbadmin-test-user"></a><span data-ttu-id="05e97-195">Создание тестового пользователя Jobbadmin</span><span class="sxs-lookup"><span data-stu-id="05e97-195">Creating a Jobbadmin test user</span></span>

<span data-ttu-id="05e97-196">Чтобы пользователи Azure AD могли выполнять вход в Jobbadmin, они должны быть подготовлены для Jobbadmin.</span><span class="sxs-lookup"><span data-stu-id="05e97-196">To enable Azure AD users to log in to Jobbadmin, they must be provisioned into Jobbadmin.</span></span>
 
<span data-ttu-id="05e97-197">Обратитесь в [службу поддержки Jobbadmin](https://www.jobbnorge.no/om-oss/kontakt-oss), чтобы добавить пользователей на их стороне.</span><span class="sxs-lookup"><span data-stu-id="05e97-197">Please contact [Jobbadmin support team](https://www.jobbnorge.no/om-oss/kontakt-oss) to get the users added on their side.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="05e97-198">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="05e97-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="05e97-199">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure путем предоставления доступа к Jobbadmin.</span><span class="sxs-lookup"><span data-stu-id="05e97-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Jobbadmin.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="05e97-201">**Чтобы назначить пользователя Britta Simon в Jobbadmin, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="05e97-201">**To assign Britta Simon to Jobbadmin, perform the following steps:**</span></span>

1. <span data-ttu-id="05e97-202">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="05e97-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="05e97-204">В списке приложений выберите **Jobbadmin**.</span><span class="sxs-lookup"><span data-stu-id="05e97-204">In the applications list, select **Jobbadmin**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-jobbadmin-tutorial/tutorial_jobbadmin_app.png) 

3. <span data-ttu-id="05e97-206">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="05e97-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="05e97-208">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="05e97-208">Click **Add** button.</span></span> <span data-ttu-id="05e97-209">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="05e97-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="05e97-211">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="05e97-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="05e97-212">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="05e97-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="05e97-213">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="05e97-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="05e97-214">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="05e97-214">Testing single sign-on</span></span>

<span data-ttu-id="05e97-215">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="05e97-215">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="05e97-216">Когда вы нажмете значок Jobbadmin на панели доступа, должна появиться страница входа в приложение Jobbadmin.</span><span class="sxs-lookup"><span data-stu-id="05e97-216">When you click the Jobbadmin tile in the Access Panel, you should get login page of Jobbadmin application.</span></span>
<span data-ttu-id="05e97-217">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="05e97-217">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="05e97-218">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="05e97-218">Additional resources</span></span>

* [<span data-ttu-id="05e97-219">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="05e97-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="05e97-220">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="05e97-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jobbadmin-tutorial/tutorial_general_203.png

