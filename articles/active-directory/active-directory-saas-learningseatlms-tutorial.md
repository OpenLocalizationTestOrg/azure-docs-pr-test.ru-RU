---
title: "Руководство по интеграции Azure Active Directory с Learning Seat LMS | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и Learning Seat LMS."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: bb056fcf-4135-478e-85b1-5015d1f07b85
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: jeedes
ms.openlocfilehash: 877e0288fdd1f590acf064c204aff0741539b112
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-learning-seat-lms"></a><span data-ttu-id="0a0f9-103">Руководство по интеграции Azure Active Directory с Learning Seat LMS</span><span class="sxs-lookup"><span data-stu-id="0a0f9-103">Tutorial: Azure Active Directory integration with Learning Seat LMS</span></span>

<span data-ttu-id="0a0f9-104">В этом руководстве описано, как интегрировать Azure Active Directory (Azure AD) с приложением Learning Seat LMS.</span><span class="sxs-lookup"><span data-stu-id="0a0f9-104">In this tutorial, you learn how to integrate Learning Seat LMS with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0a0f9-105">Интеграция Learning Seat LMS с Azure AD обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="0a0f9-105">Integrating Learning Seat LMS with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="0a0f9-106">С помощью Azure AD вы можете контролировать доступ к Learning Seat LMS.</span><span class="sxs-lookup"><span data-stu-id="0a0f9-106">You can control in Azure AD who has access to Learning Seat LMS</span></span>
- <span data-ttu-id="0a0f9-107">Вы можете включить автоматический вход пользователей в Learning Seat LMS (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0a0f9-107">You can enable your users to automatically get signed-on to Learning Seat LMS (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0a0f9-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="0a0f9-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="0a0f9-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в статье</span><span class="sxs-lookup"><span data-stu-id="0a0f9-109">If you want to know more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="0a0f9-110">[Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0a0f9-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0a0f9-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="0a0f9-111">Prerequisites</span></span>

<span data-ttu-id="0a0f9-112">Чтобы настроить интеграцию Azure AD с Learning Seat LMS, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="0a0f9-112">To configure Azure AD integration with Learning Seat LMS, you need the following items:</span></span>

- <span data-ttu-id="0a0f9-113">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="0a0f9-113">An Azure AD subscription</span></span>
- <span data-ttu-id="0a0f9-114">подписка на Learning Seat LMS с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="0a0f9-114">A Learning Seat LMS single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0a0f9-115">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="0a0f9-115">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0a0f9-116">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="0a0f9-116">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0a0f9-117">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="0a0f9-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="0a0f9-118">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0a0f9-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0a0f9-119">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="0a0f9-119">Scenario description</span></span>
<span data-ttu-id="0a0f9-120">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="0a0f9-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0a0f9-121">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="0a0f9-121">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0a0f9-122">Добавление Learning Seat LMS из коллекции.</span><span class="sxs-lookup"><span data-stu-id="0a0f9-122">Adding Learning Seat LMS from the gallery</span></span>
2. <span data-ttu-id="0a0f9-123">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="0a0f9-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-learning-seat-lms-from-the-gallery"></a><span data-ttu-id="0a0f9-124">Добавление Learning Seat LMS из коллекции</span><span class="sxs-lookup"><span data-stu-id="0a0f9-124">Adding Learning Seat LMS from the gallery</span></span>
<span data-ttu-id="0a0f9-125">Чтобы настроить интеграцию Learning Seat LMS с Azure AD, необходимо добавить Learning Seat LMS из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="0a0f9-125">To configure the integration of Learning Seat LMS into Azure AD, you need to add Learning Seat LMS from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="0a0f9-126">**Чтобы добавить Learning Seat LMS из коллекции, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="0a0f9-126">**To add Learning Seat LMS from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="0a0f9-127">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0a0f9-127">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0a0f9-129">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="0a0f9-129">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="0a0f9-130">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="0a0f9-130">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="0a0f9-132">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="0a0f9-132">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="0a0f9-134">В поле поиска введите **Learning Seat LMS**.</span><span class="sxs-lookup"><span data-stu-id="0a0f9-134">In the search box, type **Learning Seat LMS**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_search.png)

5. <span data-ttu-id="0a0f9-136">На панели результатов выберите **Learning Seat LMS** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="0a0f9-136">In the results panel, select **Learning Seat LMS**, and then click **Add** button to add the application.</span></span>


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0a0f9-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="0a0f9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0a0f9-138">В этом разделе описаны настройка и проверка единого входа Azure AD в Learning Seat LMS с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0a0f9-138">In this section, you configure and test Azure AD single sign-on with Learning Seat LMS based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="0a0f9-139">Чтобы единый вход работал, Azure AD необходимо знать, какой пользователь в Learning Seat LMS соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0a0f9-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Learning Seat LMS is to a user in Azure AD.</span></span> <span data-ttu-id="0a0f9-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Learning Seat LMS.</span><span class="sxs-lookup"><span data-stu-id="0a0f9-140">In other words, a link relationship between an Azure AD user and the related user in Learning Seat LMS needs to be established.</span></span>

<span data-ttu-id="0a0f9-141">Чтобы установить эту связь, следует назначить **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Learning Seat LMS.</span><span class="sxs-lookup"><span data-stu-id="0a0f9-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Learning Seat LMS.</span></span>

<span data-ttu-id="0a0f9-142">Чтобы настроить и проверить единый вход Azure AD в Learning Seat LMS, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="0a0f9-142">To configure and test Azure AD single sign-on with Learning Seat LMS, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="0a0f9-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="0a0f9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="0a0f9-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0a0f9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0a0f9-145">**[Создание тестового пользователя Learning Seat LMS](#creating-a-learnconnect-test-user)** требуется для создания в Learning Seat LMS пользователя Britta Simon, связанного с соответствующим представлением в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0a0f9-145">**[Creating a Learning Seat LMS test user](#creating-a-learnconnect-test-user)** - to have a counterpart of Britta Simon in Learning Seat LMS that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="0a0f9-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0a0f9-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0a0f9-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="0a0f9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0a0f9-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="0a0f9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0a0f9-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Learning Seat LMS.</span><span class="sxs-lookup"><span data-stu-id="0a0f9-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Learning Seat LMS application.</span></span>

<span data-ttu-id="0a0f9-150">**Чтобы настроить единый вход Azure AD в Learning Seat LMS, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="0a0f9-150">**To configure Azure AD single sign-on with Learning Seat LMS, perform the following steps:**</span></span>

1. <span data-ttu-id="0a0f9-151">На портале Azure на странице интеграции с приложением **Learning Seat LMS** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="0a0f9-151">In the Azure portal, on the **Learning Seat LMS** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="0a0f9-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="0a0f9-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_samlbase.png)

3. <span data-ttu-id="0a0f9-155">Если вы хотите настроить приложение в режиме, инициированном **поставщиком удостоверений**, то в разделе **Домены и URL-адреса приложения Learning Seat LMS** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="0a0f9-155">On the **Learning Seat LMS Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_url.png)

    <span data-ttu-id="0a0f9-157">а.</span><span class="sxs-lookup"><span data-stu-id="0a0f9-157">a.</span></span> <span data-ttu-id="0a0f9-158">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<subdomain>.learningseatlms.com`</span><span class="sxs-lookup"><span data-stu-id="0a0f9-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.learningseatlms.com`</span></span>

    <span data-ttu-id="0a0f9-159">b.</span><span class="sxs-lookup"><span data-stu-id="0a0f9-159">b.</span></span> <span data-ttu-id="0a0f9-160">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате: `https://<subdomain>.learningseatlms.com/Account/AssertionConsumerService`.</span><span class="sxs-lookup"><span data-stu-id="0a0f9-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<subdomain>.learningseatlms.com/Account/AssertionConsumerService`</span></span>

4. <span data-ttu-id="0a0f9-161">Установите флажок **Показать дополнительные параметры URL-адресов**, если вы хотите настроить приложение для работы в режиме, инициируемом **поставщиком услуг**.</span><span class="sxs-lookup"><span data-stu-id="0a0f9-161">Check **Show advanced URL settings**, if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_url2.png)

    <span data-ttu-id="0a0f9-163">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<subdomain>.learningseatlms.com`</span><span class="sxs-lookup"><span data-stu-id="0a0f9-163">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.learningseatlms.com`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="0a0f9-164">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="0a0f9-164">These values are not the real values.</span></span> <span data-ttu-id="0a0f9-165">Замените их на фактические значения идентификатора, URL-адреса ответа и URL-адреса входа.</span><span class="sxs-lookup"><span data-stu-id="0a0f9-165">Update these values with the actual Identifier, Reply URL and Sign-On URL.</span></span> <span data-ttu-id="0a0f9-166">Чтобы получить эти значения, обратитесь в [службу поддержки Learning Seat](http://help.learningseatlms.com/help).</span><span class="sxs-lookup"><span data-stu-id="0a0f9-166">Contact [Learning Seat support team](http://help.learningseatlms.com/help) to get these values.</span></span> 

5. <span data-ttu-id="0a0f9-167">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="0a0f9-167">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_certificate.png) 

6. <span data-ttu-id="0a0f9-169">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="0a0f9-169">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-learnconnect-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="0a0f9-171">Чтобы настроить единый вход на стороне **Learning Seat LMS**, отправьте в [службу поддержки Learning Seat](http://help.learningseatlms.com/help) скачанный **XML-файл метаданных**.</span><span class="sxs-lookup"><span data-stu-id="0a0f9-171">To configure single sign-on on **Learning Seat LMS** side, you need to send the downloaded **Metadata XML** to [Learning Seat support team](http://help.learningseatlms.com/help).</span></span>

> [!TIP]
> <span data-ttu-id="0a0f9-172">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="0a0f9-172">You can now read a concise version of these instructions inside the [Azure  portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="0a0f9-173">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="0a0f9-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="0a0f9-174">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD](https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="0a0f9-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation](https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0a0f9-175">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="0a0f9-175">Creating an Azure AD test user</span></span>

<span data-ttu-id="0a0f9-176">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0a0f9-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="0a0f9-178">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="0a0f9-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="0a0f9-179">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="0a0f9-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-learnconnect-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0a0f9-181">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="0a0f9-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-learnconnect-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0a0f9-183">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="0a0f9-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-learnconnect-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0a0f9-185">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="0a0f9-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-learnconnect-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0a0f9-187">а.</span><span class="sxs-lookup"><span data-stu-id="0a0f9-187">a.</span></span> <span data-ttu-id="0a0f9-188">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0a0f9-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0a0f9-189">b.</span><span class="sxs-lookup"><span data-stu-id="0a0f9-189">b.</span></span> <span data-ttu-id="0a0f9-190">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0a0f9-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0a0f9-191">c.</span><span class="sxs-lookup"><span data-stu-id="0a0f9-191">c.</span></span> <span data-ttu-id="0a0f9-192">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="0a0f9-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="0a0f9-193">d.</span><span class="sxs-lookup"><span data-stu-id="0a0f9-193">d.</span></span> <span data-ttu-id="0a0f9-194">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="0a0f9-194">Click **Create**.</span></span>
 
### <a name="creating-a-learning-seat-lms-test-user"></a><span data-ttu-id="0a0f9-195">Создание тестового пользователя Learning Seat LMS</span><span class="sxs-lookup"><span data-stu-id="0a0f9-195">Creating a Learning Seat LMS test user</span></span>

<span data-ttu-id="0a0f9-196">В этом разделе описано, как создать пользователя Britta Simon в приложении Learning Seat LMS.</span><span class="sxs-lookup"><span data-stu-id="0a0f9-196">In this section, you create a user called Britta Simon in Learning Seat LMS.</span></span> <span data-ttu-id="0a0f9-197">Обратитесь в [службу поддержки Learning Seat](http://help.learningseatlms.com/help), указав все необходимые сведения о пользователе, чтобы добавить пользователей в приложение Learning Seat LMS.</span><span class="sxs-lookup"><span data-stu-id="0a0f9-197">Contact [Learning Seat support team](http://help.learningseatlms.com/help) with all the user information to add the users in the Learning Seat LMS application.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="0a0f9-198">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="0a0f9-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="0a0f9-199">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив доступ к Learning Seat LMS.</span><span class="sxs-lookup"><span data-stu-id="0a0f9-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Learning Seat LMS.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="0a0f9-201">**Чтобы назначить пользователя Britta Simon в Learning Seat LMS, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="0a0f9-201">**To assign Britta Simon to Learning Seat LMS, perform the following steps:**</span></span>

1. <span data-ttu-id="0a0f9-202">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="0a0f9-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="0a0f9-204">В списке приложений выберите **Learning Seat LMS**.</span><span class="sxs-lookup"><span data-stu-id="0a0f9-204">In the applications list, select **Learning Seat LMS**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-learnconnect-tutorial/tutorial_learnconnect_app.png) 

3. <span data-ttu-id="0a0f9-206">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="0a0f9-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="0a0f9-208">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="0a0f9-208">Click **Add** button.</span></span> <span data-ttu-id="0a0f9-209">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="0a0f9-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="0a0f9-211">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="0a0f9-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="0a0f9-212">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="0a0f9-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0a0f9-213">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="0a0f9-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0a0f9-214">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="0a0f9-214">Testing single sign-on</span></span>

<span data-ttu-id="0a0f9-215">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="0a0f9-215">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span> 

<span data-ttu-id="0a0f9-216">Щелкнув элемент Learning Seat LMS на панели доступа, вы автоматически войдете в приложение Learning Seat LMS.</span><span class="sxs-lookup"><span data-stu-id="0a0f9-216">Click the Learning Seat LMS tile in the Access Panel, you will be automatically signed-on to your Learning Seat LMS application.</span></span> <span data-ttu-id="0a0f9-217">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="0a0f9-217">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0a0f9-218">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="0a0f9-218">Additional resources</span></span>

* [<span data-ttu-id="0a0f9-219">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0a0f9-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0a0f9-220">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0a0f9-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-learnconnect-tutorial/tutorial_general_203.png

