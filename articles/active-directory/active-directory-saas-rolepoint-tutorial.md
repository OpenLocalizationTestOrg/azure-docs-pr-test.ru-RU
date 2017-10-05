---
title: "Руководство по интеграции Azure Active Directory с RolePoint | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и RolePoint."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 68d37f40-15da-45f5-a9e1-d53f78e786d1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/27/2017
ms.author: jeedes
ms.openlocfilehash: fcde562484f4401e9f936614b9978f839f4aa290
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-rolepoint"></a><span data-ttu-id="97195-103">Руководство по интеграции Azure Active Directory с RolePoint</span><span class="sxs-lookup"><span data-stu-id="97195-103">Tutorial: Azure Active Directory integration with RolePoint</span></span>

<span data-ttu-id="97195-104">В этом руководстве описано, как интегрировать RolePoint с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="97195-104">In this tutorial, you learn how to integrate RolePoint with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="97195-105">Интеграция Azure AD с приложением RolePoint дает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="97195-105">Integrating RolePoint with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="97195-106">С помощью Azure AD вы можете контролировать доступ к RolePoint.</span><span class="sxs-lookup"><span data-stu-id="97195-106">You can control in Azure AD who has access to RolePoint</span></span>
- <span data-ttu-id="97195-107">Вы можете включить автоматический вход пользователей в RolePoint (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="97195-107">You can enable your users to automatically get signed-on to RolePoint (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="97195-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="97195-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="97195-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="97195-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="97195-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="97195-110">Prerequisites</span></span>

<span data-ttu-id="97195-111">Чтобы настроить интеграцию Azure AD с приложением RolePoint, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="97195-111">To configure Azure AD integration with RolePoint, you need the following items:</span></span>

- <span data-ttu-id="97195-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="97195-112">An Azure AD subscription</span></span>
- <span data-ttu-id="97195-113">подписка RolePoint с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="97195-113">A RolePoint single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="97195-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="97195-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="97195-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="97195-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="97195-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="97195-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="97195-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="97195-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="97195-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="97195-118">Scenario description</span></span>
<span data-ttu-id="97195-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="97195-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="97195-120">Сценарий, описанный в этом руководстве, состоит из двух стандартных блоков.</span><span class="sxs-lookup"><span data-stu-id="97195-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="97195-121">Добавление RolePoint из коллекции</span><span class="sxs-lookup"><span data-stu-id="97195-121">Adding RolePoint from the gallery</span></span>
2. <span data-ttu-id="97195-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="97195-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-rolepoint-from-the-gallery"></a><span data-ttu-id="97195-123">Добавление RolePoint из коллекции</span><span class="sxs-lookup"><span data-stu-id="97195-123">Adding RolePoint from the gallery</span></span>
<span data-ttu-id="97195-124">Чтобы настроить интеграцию RolePoint с Azure AD, необходимо добавить RolePoint из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="97195-124">To configure the integration of RolePoint into Azure AD, you need to add RolePoint from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="97195-125">**Чтобы добавить RolePoint из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="97195-125">**To add RolePoint from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="97195-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="97195-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="97195-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="97195-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="97195-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="97195-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="97195-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="97195-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="97195-133">В поле поиска введите **RolePoint**.</span><span class="sxs-lookup"><span data-stu-id="97195-133">In the search box, type **RolePoint**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_search.png)

5. <span data-ttu-id="97195-135">На панели результатов выберите **RolePoint** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="97195-135">In the results panel, select **RolePoint**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="97195-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="97195-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="97195-138">В этом разделе мы выполним настройку и проверку единого входа Azure AD в RolePoint с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="97195-138">In this section, you configure and test Azure AD single sign-on with RolePoint based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="97195-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в RolePoint соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="97195-139">For single sign-on to work, Azure AD needs to know what the counterpart user in RolePoint is to a user in Azure AD.</span></span> <span data-ttu-id="97195-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в RolePoint.</span><span class="sxs-lookup"><span data-stu-id="97195-140">In other words, a link relationship between an Azure AD user and the related user in RolePoint needs to be established.</span></span>

<span data-ttu-id="97195-141">Чтобы установить эту связь, следует назначить **имя пользователя** в Azure AD в качестве значения **имени пользователя** в RolePoint.</span><span class="sxs-lookup"><span data-stu-id="97195-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in RolePoint.</span></span>

<span data-ttu-id="97195-142">Чтобы настроить и проверить единый вход Azure AD в RolePoint, выполните следующие стандартные действия.</span><span class="sxs-lookup"><span data-stu-id="97195-142">To configure and test Azure AD single sign-on with RolePoint, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="97195-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="97195-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="97195-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="97195-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="97195-145">**[Создание тестового пользователя RolePoint](#creating-a-rolepoint-test-user)** — требуется для создания в RolePoint копии пользователя Britta Simon, связанной с соответствующим представлением пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="97195-145">**[Creating a RolePoint test user](#creating-a-rolepoint-test-user)** - to have a counterpart of Britta Simon in RolePoint that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="97195-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="97195-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="97195-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="97195-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="97195-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="97195-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="97195-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении RolePoint.</span><span class="sxs-lookup"><span data-stu-id="97195-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your RolePoint application.</span></span>

<span data-ttu-id="97195-150">**Чтобы настроить единый вход Azure AD в RolePoint, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="97195-150">**To configure Azure AD single sign-on with RolePoint, perform the following steps:**</span></span>

1. <span data-ttu-id="97195-151">На портале Azure на странице интеграции с приложением **RolePoint** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="97195-151">In the Azure portal, on the **RolePoint** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="97195-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="97195-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_samlbase.png)

3. <span data-ttu-id="97195-155">В разделе **Домены и URL-адреса приложения RolePoint** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="97195-155">On the **RolePoint Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_url.png)

    <span data-ttu-id="97195-157">а.</span><span class="sxs-lookup"><span data-stu-id="97195-157">a.</span></span> <span data-ttu-id="97195-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<subdomain>.rolepoint.com/login`</span><span class="sxs-lookup"><span data-stu-id="97195-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.rolepoint.com/login`</span></span>
    
    <span data-ttu-id="97195-159">b.</span><span class="sxs-lookup"><span data-stu-id="97195-159">b.</span></span> <span data-ttu-id="97195-160">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://app.rolepoint.com/<instancename>`</span><span class="sxs-lookup"><span data-stu-id="97195-160">In the **Identifier** textbox, type a URL using the following pattern: `https://app.rolepoint.com/<instancename>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="97195-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="97195-161">These values are not the real.</span></span> <span data-ttu-id="97195-162">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="97195-162">Update these values with the actual Sign-on URL and Identifier.</span></span> <span data-ttu-id="97195-163">Мы рекомендуем использовать уникальное значение строки в идентификаторе. Чтобы получить это значение, обратитесь в [службу поддержки RolePoint](mailto:info@rolepoint.com).</span><span class="sxs-lookup"><span data-stu-id="97195-163">Here we suggest you to use the unique value of string in the Identifier.Contact [RolePoint support team](mailto:info@rolepoint.com) to get the value.</span></span> 
 
4. <span data-ttu-id="97195-164">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="97195-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_certificate.png) 

5. <span data-ttu-id="97195-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="97195-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-rolepoint-tutorial/tutorial_general_400.png)


6. <span data-ttu-id="97195-168">Чтобы настроить единый вход на стороне **RolePoint**, отправьте скачанный **XML-файл метаданных** в [службу поддержки RolePoint](mailto:info@rolepoint.com).</span><span class="sxs-lookup"><span data-stu-id="97195-168">To configure single sign-on on **RolePoint** side, you need to send the downloaded **Metadata XML** to [RolePoint support team](mailto:info@rolepoint.com).</span></span>

> [!TIP]
> <span data-ttu-id="97195-169">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="97195-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="97195-170">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="97195-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="97195-171">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="97195-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="97195-172">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="97195-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="97195-173">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="97195-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="97195-175">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="97195-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="97195-176">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="97195-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-rolepoint-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="97195-178">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="97195-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-rolepoint-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="97195-180">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="97195-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-rolepoint-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="97195-182">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="97195-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-rolepoint-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="97195-184">а.</span><span class="sxs-lookup"><span data-stu-id="97195-184">a.</span></span> <span data-ttu-id="97195-185">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="97195-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="97195-186">b.</span><span class="sxs-lookup"><span data-stu-id="97195-186">b.</span></span> <span data-ttu-id="97195-187">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="97195-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="97195-188">c.</span><span class="sxs-lookup"><span data-stu-id="97195-188">c.</span></span> <span data-ttu-id="97195-189">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="97195-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="97195-190">d.</span><span class="sxs-lookup"><span data-stu-id="97195-190">d.</span></span> <span data-ttu-id="97195-191">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="97195-191">Click **Create**.</span></span>
 
### <a name="creating-a-rolepoint-test-user"></a><span data-ttu-id="97195-192">Создание тестового пользователя RolePoint</span><span class="sxs-lookup"><span data-stu-id="97195-192">Creating a RolePoint test user</span></span>

<span data-ttu-id="97195-193">В этом разделе описано, как создать пользователя Britta Simon в приложении RolePoint.</span><span class="sxs-lookup"><span data-stu-id="97195-193">In this section, you create a user called Britta Simon in RolePoint.</span></span> <span data-ttu-id="97195-194">Обратитесь к [службу поддержки RolePoint](mailto:info@rolepoint.com), чтобы добавить пользователей на платформу RolePoint.</span><span class="sxs-lookup"><span data-stu-id="97195-194">Work with [RolePoint support team](mailto:info@rolepoint.com) to add the users in the RolePoint platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="97195-195">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="97195-195">Assigning the Azure AD test user</span></span>

<span data-ttu-id="97195-196">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив доступ к RolePoint.</span><span class="sxs-lookup"><span data-stu-id="97195-196">In this section, you enable Britta Simon to use Azure single sign-on by granting access to RolePoint.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="97195-198">**Чтобы назначить пользователя Britta Simon в RolePoint, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="97195-198">**To assign Britta Simon to RolePoint, perform the following steps:**</span></span>

1. <span data-ttu-id="97195-199">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="97195-199">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="97195-201">В списке приложений выберите **RolePoint**.</span><span class="sxs-lookup"><span data-stu-id="97195-201">In the applications list, select **RolePoint**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-rolepoint-tutorial/tutorial_rolepoint_app.png) 

3. <span data-ttu-id="97195-203">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="97195-203">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="97195-205">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="97195-205">Click **Add** button.</span></span> <span data-ttu-id="97195-206">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="97195-206">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="97195-208">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="97195-208">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="97195-209">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="97195-209">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="97195-210">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="97195-210">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="97195-211">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="97195-211">Testing single sign-on</span></span>

<span data-ttu-id="97195-212">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="97195-212">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="97195-213">Щелкнув элемент RolePoint на панели доступа, вы автоматически войдете в приложение RolePoint.</span><span class="sxs-lookup"><span data-stu-id="97195-213">When you click the RolePoint tile in the Access Panel, you should get automatically signed-on to your RolePoint application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="97195-214">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="97195-214">Additional resources</span></span>

* [<span data-ttu-id="97195-215">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="97195-215">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="97195-216">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="97195-216">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-rolepoint-tutorial/tutorial_general_203.png

