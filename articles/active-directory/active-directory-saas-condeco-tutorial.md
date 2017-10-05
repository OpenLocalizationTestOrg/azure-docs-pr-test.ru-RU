---
title: "Учебник. Интеграция Azure Active Directory с Condeco | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в Condeco."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 4601c17d-ad93-4865-8885-b378c4bbe82b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: eab1d25abc2fccdeffdf2706269bfd078eb5a09f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-condeco"></a><span data-ttu-id="32a9d-103">Учебник. Интеграция Azure Active Directory с Concur</span><span class="sxs-lookup"><span data-stu-id="32a9d-103">Tutorial: Azure Active Directory integration with Condeco</span></span>

<span data-ttu-id="32a9d-104">В этом руководстве описано, как интегрировать Condeco с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="32a9d-104">In this tutorial, you learn how to integrate Condeco with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="32a9d-105">Интеграция Azure AD с приложением Condeco обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="32a9d-105">Integrating Condeco with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="32a9d-106">С помощью Azure AD вы можете контролировать доступ к Condeco.</span><span class="sxs-lookup"><span data-stu-id="32a9d-106">You can control in Azure AD who has access to Condeco</span></span>
- <span data-ttu-id="32a9d-107">Вы можете включить автоматический вход пользователей в Condeco (единый вход) с использованием их учетных записей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="32a9d-107">You can enable your users to automatically get signed-on to Condeco (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="32a9d-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="32a9d-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="32a9d-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="32a9d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="32a9d-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="32a9d-110">Prerequisites</span></span>

<span data-ttu-id="32a9d-111">Чтобы настроить интеграцию Azure AD с Condeco, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="32a9d-111">To configure Azure AD integration with Condeco, you need the following items:</span></span>

- <span data-ttu-id="32a9d-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="32a9d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="32a9d-113">подписка с поддержкой единого входа Condeco.</span><span class="sxs-lookup"><span data-stu-id="32a9d-113">A Condeco single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="32a9d-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="32a9d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="32a9d-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="32a9d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="32a9d-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="32a9d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="32a9d-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="32a9d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="32a9d-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="32a9d-118">Scenario description</span></span>
<span data-ttu-id="32a9d-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="32a9d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="32a9d-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="32a9d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="32a9d-121">Добавление Condeco из коллекции</span><span class="sxs-lookup"><span data-stu-id="32a9d-121">Adding Condeco from the gallery</span></span>
2. <span data-ttu-id="32a9d-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="32a9d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-condeco-from-the-gallery"></a><span data-ttu-id="32a9d-123">Добавление Condeco из коллекции</span><span class="sxs-lookup"><span data-stu-id="32a9d-123">Adding Condeco from the gallery</span></span>
<span data-ttu-id="32a9d-124">Чтобы настроить интеграцию Condeco с Azure AD, необходимо добавить Condeco из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="32a9d-124">To configure the integration of Condeco into Azure AD, you need to add Condeco from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="32a9d-125">**Чтобы добавить Condeco из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="32a9d-125">**To add Condeco from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="32a9d-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="32a9d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="32a9d-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="32a9d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="32a9d-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="32a9d-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="32a9d-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="32a9d-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="32a9d-133">В поле поиска введите **Condeco**.</span><span class="sxs-lookup"><span data-stu-id="32a9d-133">In the search box, type **Condeco**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-condeco-tutorial/tutorial_condeco_search.png)

5. <span data-ttu-id="32a9d-135">На панели результатов выберите **Condeco** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="32a9d-135">In the results panel, select **Condeco**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-condeco-tutorial/tutorial_condeco_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="32a9d-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="32a9d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="32a9d-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложение Condeco для тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="32a9d-138">In this section, you configure and test Azure AD single sign-on with Condeco based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="32a9d-139">Для работы единого входа Azure AD необходимо знать, какому пользователю в Azure AD соответствует пользователь в Condeco.</span><span class="sxs-lookup"><span data-stu-id="32a9d-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Condeco is to a user in Azure AD.</span></span> <span data-ttu-id="32a9d-140">Иными словами, необходимо установить связь между пользователям Azure AD и соответствующим пользователем в Condeco.</span><span class="sxs-lookup"><span data-stu-id="32a9d-140">In other words, a link relationship between an Azure AD user and the related user in Condeco needs to be established.</span></span>

<span data-ttu-id="32a9d-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Condeco.</span><span class="sxs-lookup"><span data-stu-id="32a9d-141">In Condeco, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="32a9d-142">Чтобы настроить и проверить единый вход Azure AD в Condeco, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="32a9d-142">To configure and test Azure AD single sign-on with Condeco, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="32a9d-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="32a9d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="32a9d-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="32a9d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="32a9d-145">**[Создание тестового пользователя Condeco](#creating-a-condeco-test-user)** требуется для создания пользователя Britta Simon в Condeco, связанного с представлением этого пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="32a9d-145">**[Creating a Condeco test user](#creating-a-condeco-test-user)** - to have a counterpart of Britta Simon in Condeco that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="32a9d-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="32a9d-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="32a9d-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="32a9d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="32a9d-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="32a9d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="32a9d-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Condeco.</span><span class="sxs-lookup"><span data-stu-id="32a9d-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Condeco application.</span></span>

<span data-ttu-id="32a9d-150">**Чтобы настроить единый вход Azure AD в Condeco, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="32a9d-150">**To configure Azure AD single sign-on with Condeco, perform the following steps:**</span></span>

1. <span data-ttu-id="32a9d-151">На портале Azure на странице интеграции с приложением **Condeco** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="32a9d-151">In the Azure portal, on the **Condeco** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="32a9d-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="32a9d-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-condeco-tutorial/tutorial_condeco_samlbase.png)

3. <span data-ttu-id="32a9d-155">В разделе **Домены и URL-адреса Condeco** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="32a9d-155">On the **Condeco Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-condeco-tutorial/tutorial_condeco_url.png)

    <span data-ttu-id="32a9d-157">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<companyname>.condecosoftware.com`</span><span class="sxs-lookup"><span data-stu-id="32a9d-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.condecosoftware.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="32a9d-158">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="32a9d-158">This value is not real.</span></span> <span data-ttu-id="32a9d-159">Вместо него необходимо указать фактический URL-адрес для входа.</span><span class="sxs-lookup"><span data-stu-id="32a9d-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="32a9d-160">Для получения этого значения обратитесь в [службу поддержки клиентов Condeco](mailTo:supportna@condecosoftware.com).</span><span class="sxs-lookup"><span data-stu-id="32a9d-160">Contact [Condeco Client support team](mailTo:supportna@condecosoftware.com) to get this value.</span></span> 
 
4. <span data-ttu-id="32a9d-161">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="32a9d-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-condeco-tutorial/tutorial_condeco_certificate.png) 

5. <span data-ttu-id="32a9d-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="32a9d-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-condeco-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="32a9d-165">Чтобы настроить единый вход на стороне **Condeco**, отправьте скачанный **XML-файл метаданных** в [службу поддержки Condeco](mailTo:supportna@condecosoftware.com).</span><span class="sxs-lookup"><span data-stu-id="32a9d-165">To configure single sign-on on **Condeco** side, you need to send the downloaded **Metadata XML** to [Condeco support team](mailTo:supportna@condecosoftware.com).</span></span> <span data-ttu-id="32a9d-166">Специалисты службы поддержки настроят подключение единого входа SAML на обеих сторонах подключения.</span><span class="sxs-lookup"><span data-stu-id="32a9d-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="32a9d-167">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="32a9d-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="32a9d-168">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="32a9d-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="32a9d-169">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="32a9d-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="32a9d-170">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="32a9d-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="32a9d-171">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="32a9d-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="32a9d-173">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="32a9d-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="32a9d-174">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="32a9d-174">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-condeco-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="32a9d-176">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="32a9d-176">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-condeco-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="32a9d-178">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="32a9d-178">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-condeco-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="32a9d-180">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="32a9d-180">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-condeco-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="32a9d-182">а.</span><span class="sxs-lookup"><span data-stu-id="32a9d-182">a.</span></span> <span data-ttu-id="32a9d-183">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="32a9d-183">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="32a9d-184">b.</span><span class="sxs-lookup"><span data-stu-id="32a9d-184">b.</span></span> <span data-ttu-id="32a9d-185">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="32a9d-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="32a9d-186">c.</span><span class="sxs-lookup"><span data-stu-id="32a9d-186">c.</span></span> <span data-ttu-id="32a9d-187">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="32a9d-187">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="32a9d-188">d.</span><span class="sxs-lookup"><span data-stu-id="32a9d-188">d.</span></span> <span data-ttu-id="32a9d-189">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="32a9d-189">Click **Create**.</span></span>
 
### <a name="creating-a-condeco-test-user"></a><span data-ttu-id="32a9d-190">Создание тестового пользователя Condeco</span><span class="sxs-lookup"><span data-stu-id="32a9d-190">Creating a Condeco test user</span></span>

<span data-ttu-id="32a9d-191">Цель этого раздела — создать пользователя с именем Britta Simon в Condeco.</span><span class="sxs-lookup"><span data-stu-id="32a9d-191">The objective of this section is to create a user called Britta Simon in Condeco.</span></span> <span data-ttu-id="32a9d-192">Приложение Condeco поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="32a9d-192">Condeco supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="32a9d-193">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="32a9d-193">There is no action item for you in this section.</span></span> <span data-ttu-id="32a9d-194">Новый пользователь будет создан при попытке получить доступ к приложению Condeco (если он еще не создан).</span><span class="sxs-lookup"><span data-stu-id="32a9d-194">A new user is created during an attempt to access Condeco if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="32a9d-195">Если необходимо создать пользователя вручную, обратитесь в [службу поддержки Condeco](mailTo:supportna@condecosoftware.com).</span><span class="sxs-lookup"><span data-stu-id="32a9d-195">If you need to create a user manually, you need to contact the [Condeco support team](mailTo:supportna@condecosoftware.com).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="32a9d-196">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="32a9d-196">Assigning the Azure AD test user</span></span>

<span data-ttu-id="32a9d-197">В этом разделе описано, как включить единый вход Azure для пользователя Britta Simon, предоставив этому пользователю доступ к Condeco.</span><span class="sxs-lookup"><span data-stu-id="32a9d-197">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Condeco.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="32a9d-199">**Чтобы назначить пользователя Britta Simon в Condeco, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="32a9d-199">**To assign Britta Simon to Condeco, perform the following steps:**</span></span>

1. <span data-ttu-id="32a9d-200">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="32a9d-200">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="32a9d-202">В списке приложений выберите **Condeco**.</span><span class="sxs-lookup"><span data-stu-id="32a9d-202">In the applications list, select **Condeco**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-condeco-tutorial/tutorial_condeco_app.png) 

3. <span data-ttu-id="32a9d-204">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="32a9d-204">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="32a9d-206">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="32a9d-206">Click **Add** button.</span></span> <span data-ttu-id="32a9d-207">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="32a9d-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="32a9d-209">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="32a9d-209">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="32a9d-210">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="32a9d-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="32a9d-211">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="32a9d-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="32a9d-212">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="32a9d-212">Testing single sign-on</span></span>

<span data-ttu-id="32a9d-213">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="32a9d-213">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="32a9d-214">Щелкнув плитку Condeco на панели доступа, вы автоматически войдете в приложение Condeco.</span><span class="sxs-lookup"><span data-stu-id="32a9d-214">When you click the Condeco tile in the Access Panel, you should get automatically signed-on to your Condeco application.</span></span>
<span data-ttu-id="32a9d-215">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="32a9d-215">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="32a9d-216">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="32a9d-216">Additional resources</span></span>

* [<span data-ttu-id="32a9d-217">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="32a9d-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="32a9d-218">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="32a9d-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-condeco-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-condeco-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-condeco-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-condeco-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-condeco-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-condeco-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-condeco-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-condeco-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-condeco-tutorial/tutorial_general_203.png

