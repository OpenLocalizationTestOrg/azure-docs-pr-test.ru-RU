---
title: "Руководство по интеграции Azure Active Directory с Abintegro | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в приложении Abintegro."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 99287e1f-4189-494a-97c8-e1c03d047fd3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: jeedes
ms.openlocfilehash: a2a3c1a7a338ee1cb35dd08176ad3bb5f3cdc319
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-abintegro"></a><span data-ttu-id="44f46-103">Руководство. Интеграция Azure Active Directory с Abintegro</span><span class="sxs-lookup"><span data-stu-id="44f46-103">Tutorial: Azure Active Directory integration with Abintegro</span></span>

<span data-ttu-id="44f46-104">В этом руководстве объясняется, как интегрировать Abintegro с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="44f46-104">In this tutorial, you learn how to integrate Abintegro with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="44f46-105">Интеграция Azure AD с приложением Abintegro обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="44f46-105">Integrating Abintegro with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="44f46-106">С помощью Azure AD вы можете контролировать, у кого есть доступ к приложению Abintegro.</span><span class="sxs-lookup"><span data-stu-id="44f46-106">You can control in Azure AD who has access to Abintegro</span></span>
- <span data-ttu-id="44f46-107">Вы можете включить автоматический вход пользователей в Abintegro (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="44f46-107">You can enable your users to automatically get signed-on to Abintegro (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="44f46-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="44f46-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="44f46-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="44f46-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="44f46-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="44f46-110">Prerequisites</span></span>

<span data-ttu-id="44f46-111">Чтобы настроить интеграцию Azure AD с Abintegro, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="44f46-111">To configure Azure AD integration with Abintegro, you need the following items:</span></span>

- <span data-ttu-id="44f46-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="44f46-112">An Azure AD subscription</span></span>
- <span data-ttu-id="44f46-113">подписка Abintegro с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="44f46-113">An Abintegro single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="44f46-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="44f46-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="44f46-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="44f46-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="44f46-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="44f46-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="44f46-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="44f46-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="44f46-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="44f46-118">Scenario description</span></span>
<span data-ttu-id="44f46-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="44f46-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="44f46-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="44f46-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="44f46-121">Добавление Abintegro из коллекции</span><span class="sxs-lookup"><span data-stu-id="44f46-121">Adding Abintegro from the gallery</span></span>
2. <span data-ttu-id="44f46-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="44f46-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-abintegro-from-the-gallery"></a><span data-ttu-id="44f46-123">Добавление Abintegro из коллекции</span><span class="sxs-lookup"><span data-stu-id="44f46-123">Adding Abintegro from the gallery</span></span>
<span data-ttu-id="44f46-124">Чтобы настроить интеграцию приложения Abintegro с Azure AD, вам нужно добавить это приложение из коллекции в свой список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="44f46-124">To configure the integration of Abintegro into Azure AD, you need to add Abintegro from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="44f46-125">**Добавление приложения Abintegro из коллекции**</span><span class="sxs-lookup"><span data-stu-id="44f46-125">**To add Abintegro from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="44f46-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="44f46-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="44f46-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="44f46-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="44f46-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="44f46-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="44f46-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="44f46-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="44f46-133">В поле поиска введите **Abintegro**.</span><span class="sxs-lookup"><span data-stu-id="44f46-133">In the search box, type **Abintegro**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-abintegro-tutorial/tutorial_abintegro_search.png)

5. <span data-ttu-id="44f46-135">В области результатов выберите **Abintegro** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="44f46-135">In the results panel, select **Abintegro**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-abintegro-tutorial/tutorial_abintegro_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="44f46-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="44f46-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="44f46-138">В этом разделе мы настроим и проверим единый вход Azure AD в Abintegro с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="44f46-138">In this section, you configure and test Azure AD single sign-on with Abintegro based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="44f46-139">Для работы единого входа службе Azure AD нужно знать, какому пользователю в Azure AD соответствует пользователь в Abintegro.</span><span class="sxs-lookup"><span data-stu-id="44f46-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Abintegro is to a user in Azure AD.</span></span> <span data-ttu-id="44f46-140">Иными словами, нужно установить связь между пользователем Azure AD и соответствующим пользователем в Abintegro.</span><span class="sxs-lookup"><span data-stu-id="44f46-140">In other words, a link relationship between an Azure AD user and the related user in Abintegro needs to be established.</span></span>

<span data-ttu-id="44f46-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Abintegro.</span><span class="sxs-lookup"><span data-stu-id="44f46-141">In Abintegro, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="44f46-142">Чтобы настроить и проверить единый вход Azure AD в Abintegro, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="44f46-142">To configure and test Azure AD single sign-on with Abintegro, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="44f46-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="44f46-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="44f46-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="44f46-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="44f46-145">**[Создание тестового пользователя Abintegro](#creating-an-abintegro-test-user)** требуется для создания в Abintegro пользователя Britta Simon, связанного с представлением этого же пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="44f46-145">**[Creating an Abintegro test user](#creating-an-abintegro-test-user)** - to have a counterpart of Britta Simon in Abintegro that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="44f46-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="44f46-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="44f46-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="44f46-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="44f46-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="44f46-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="44f46-149">В этом разделе мы включим на портале Azure единый вход Azure AD и настроим его в приложении Abintegro.</span><span class="sxs-lookup"><span data-stu-id="44f46-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Abintegro application.</span></span>

<span data-ttu-id="44f46-150">**Настройка единого входа Azure AD в Abintegro**</span><span class="sxs-lookup"><span data-stu-id="44f46-150">**To configure Azure AD single sign-on with Abintegro, perform the following steps:**</span></span>

1. <span data-ttu-id="44f46-151">На портале Azure на странице интеграции с приложением **Abintegro** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="44f46-151">In the Azure portal, on the **Abintegro** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="44f46-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="44f46-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-abintegro-tutorial/tutorial_abintegro_samlbase.png)

3. <span data-ttu-id="44f46-155">В разделе **Домены и URL-адреса приложения Abintegro** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="44f46-155">On the **Abintegro Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-abintegro-tutorial/tutorial_abintegro_url.png)

    <span data-ttu-id="44f46-157">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://dev.abintegro.com/Shibboleth.sso/Login?entityID=<Issuer>&target=https://dev.abintegro.com/secure/`</span><span class="sxs-lookup"><span data-stu-id="44f46-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://dev.abintegro.com/Shibboleth.sso/Login?entityID=<Issuer>&target=https://dev.abintegro.com/secure/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="44f46-158">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="44f46-158">This value is not real.</span></span> <span data-ttu-id="44f46-159">Вместо него необходимо указать фактический URL-адрес для входа.</span><span class="sxs-lookup"><span data-stu-id="44f46-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="44f46-160">Для получения этого значения обратитесь в [службу поддержки клиентов Abintegro](mailto:support@abintegro.com).</span><span class="sxs-lookup"><span data-stu-id="44f46-160">Contact [Abintegro Client support team](mailto:support@abintegro.com) to get this value.</span></span> 
 
4. <span data-ttu-id="44f46-161">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="44f46-161">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-abintegro-tutorial/tutorial_abintegro_certificate.png) 

5. <span data-ttu-id="44f46-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="44f46-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-abintegro-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="44f46-165">Чтобы настроить единый вход на стороне **Abintegro**, отправьте в **службу поддержки Abintegro** скачанный [XML-файл метаданных](mailto:support@abintegro.com).</span><span class="sxs-lookup"><span data-stu-id="44f46-165">To configure single sign-on on **Abintegro** side, you need to send the downloaded **Metadata XML** to [Abintegro support team](mailto:support@abintegro.com).</span></span> <span data-ttu-id="44f46-166">Специалисты службы поддержки правильно настроят подключение единого входа SAML на обеих сторонах подключения.</span><span class="sxs-lookup"><span data-stu-id="44f46-166">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="44f46-167">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="44f46-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="44f46-168">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="44f46-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="44f46-169">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="44f46-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="44f46-170">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="44f46-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="44f46-171">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="44f46-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="44f46-173">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="44f46-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="44f46-174">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="44f46-174">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-abintegro-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="44f46-176">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="44f46-176">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-abintegro-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="44f46-178">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="44f46-178">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-abintegro-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="44f46-180">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="44f46-180">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-abintegro-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="44f46-182">а.</span><span class="sxs-lookup"><span data-stu-id="44f46-182">a.</span></span> <span data-ttu-id="44f46-183">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="44f46-183">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="44f46-184">b.</span><span class="sxs-lookup"><span data-stu-id="44f46-184">b.</span></span> <span data-ttu-id="44f46-185">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="44f46-185">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="44f46-186">c.</span><span class="sxs-lookup"><span data-stu-id="44f46-186">c.</span></span> <span data-ttu-id="44f46-187">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="44f46-187">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="44f46-188">d.</span><span class="sxs-lookup"><span data-stu-id="44f46-188">d.</span></span> <span data-ttu-id="44f46-189">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="44f46-189">Click **Create**.</span></span>
 
### <a name="creating-an-abintegro-test-user"></a><span data-ttu-id="44f46-190">Создание тестового пользователя Abintegro</span><span class="sxs-lookup"><span data-stu-id="44f46-190">Creating an Abintegro test user</span></span>

<span data-ttu-id="44f46-191">Элемент действия для настройки подготовки пользователей в Abintegro отсутствует.</span><span class="sxs-lookup"><span data-stu-id="44f46-191">There is no action item for you to configure user provisioning to Abintegro.</span></span> <span data-ttu-id="44f46-192">Когда назначенный пользователь пытается войти в Abintegro с помощью панели доступа, Abintegro проверяет, существует ли данный пользователь.</span><span class="sxs-lookup"><span data-stu-id="44f46-192">When an assigned user tries to log into Abintegro using the access panel, Abintegro checks whether the user exists.</span></span>
  
<span data-ttu-id="44f46-193">Если учетная запись пользователя отсутствует, Abintegro автоматически создает ее.</span><span class="sxs-lookup"><span data-stu-id="44f46-193">If there is no user account available yet, it is automatically created by Abintegro.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="44f46-194">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="44f46-194">Assigning the Azure AD test user</span></span>

<span data-ttu-id="44f46-195">В этом разделе мы разрешим пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к Abintegro.</span><span class="sxs-lookup"><span data-stu-id="44f46-195">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Abintegro.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="44f46-197">**Назначение пользователя Britta Simon приложению Abintegro**</span><span class="sxs-lookup"><span data-stu-id="44f46-197">**To assign Britta Simon to Abintegro, perform the following steps:**</span></span>

1. <span data-ttu-id="44f46-198">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="44f46-198">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="44f46-200">В списке приложений выберите **Abintegro**.</span><span class="sxs-lookup"><span data-stu-id="44f46-200">In the applications list, select **Abintegro**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-abintegro-tutorial/tutorial_abintegro_app.png) 

3. <span data-ttu-id="44f46-202">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="44f46-202">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="44f46-204">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="44f46-204">Click **Add** button.</span></span> <span data-ttu-id="44f46-205">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="44f46-205">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="44f46-207">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="44f46-207">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="44f46-208">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="44f46-208">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="44f46-209">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="44f46-209">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="44f46-210">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="44f46-210">Testing single sign-on</span></span>

<span data-ttu-id="44f46-211">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="44f46-211">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="44f46-212">Когда вы нажмете плитку Abintegro на панели доступа, должна появиться страница входа в приложение Abintegro.</span><span class="sxs-lookup"><span data-stu-id="44f46-212">When you click the Abintegro tile in the Access Panel, you should get login page of Abintegro application.</span></span>
<span data-ttu-id="44f46-213">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="44f46-213">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="44f46-214">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="44f46-214">Additional resources</span></span>

* [<span data-ttu-id="44f46-215">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="44f46-215">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="44f46-216">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="44f46-216">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-abintegro-tutorial/tutorial_general_203.png

