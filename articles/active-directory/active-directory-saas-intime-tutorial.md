---
title: "Руководство по интеграции Azure Active Directory с InTime | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в InTime."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d4e2c6e1-ae5d-4d2c-8ffc-1b24534d376a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: jeedes
ms.openlocfilehash: 4bb22c92ad7f6963be6ca15073f7f01da99ba2bb
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-intime"></a><span data-ttu-id="3901b-103">Руководство по интеграции Azure Active Directory с InTime</span><span class="sxs-lookup"><span data-stu-id="3901b-103">Tutorial: Azure Active Directory integration with InTime</span></span>

<span data-ttu-id="3901b-104">В этом руководстве описано, как интегрировать InTime с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3901b-104">In this tutorial, you learn how to integrate InTime with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3901b-105">Интеграция Azure AD с приложением InTime обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="3901b-105">Integrating InTime with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3901b-106">С помощью Azure AD вы можете контролировать доступ к InTime.</span><span class="sxs-lookup"><span data-stu-id="3901b-106">You can control in Azure AD who has access to InTime.</span></span>
- <span data-ttu-id="3901b-107">Вы можете включить автоматический вход пользователей в InTime (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3901b-107">You can enable your users to automatically get signed-on to InTime (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="3901b-108">Вы можете управлять учетными записями централизованно — на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="3901b-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="3901b-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3901b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3901b-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="3901b-110">Prerequisites</span></span>

<span data-ttu-id="3901b-111">Чтобы настроить интеграцию Azure AD с InTime, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="3901b-111">To configure Azure AD integration with InTime, you need the following items:</span></span>

- <span data-ttu-id="3901b-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="3901b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3901b-113">подписка InTime с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="3901b-113">A InTime single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3901b-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="3901b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3901b-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="3901b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3901b-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="3901b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3901b-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3901b-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3901b-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="3901b-118">Scenario description</span></span>
<span data-ttu-id="3901b-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="3901b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3901b-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="3901b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3901b-121">Добавление InTime из коллекции.</span><span class="sxs-lookup"><span data-stu-id="3901b-121">Adding InTime from the gallery</span></span>
2. <span data-ttu-id="3901b-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="3901b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-intime-from-the-gallery"></a><span data-ttu-id="3901b-123">Добавление InTime из коллекции</span><span class="sxs-lookup"><span data-stu-id="3901b-123">Adding InTime from the gallery</span></span>
<span data-ttu-id="3901b-124">Чтобы настроить интеграцию InTime с Azure AD, необходимо добавить InTime из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="3901b-124">To configure the integration of InTime into Azure AD, you need to add InTime from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3901b-125">**Чтобы добавить InTime из коллекции, сделайте следующее.**</span><span class="sxs-lookup"><span data-stu-id="3901b-125">**To add InTime from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3901b-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3901b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка "Azure Active Directory"][1]

2. <span data-ttu-id="3901b-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="3901b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3901b-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="3901b-129">Then go to **All applications**.</span></span>

    ![Колонка "Корпоративные приложения"][2]
    
3. <span data-ttu-id="3901b-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="3901b-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Кнопка "Новое приложение"][3]

4. <span data-ttu-id="3901b-133">В поле поиска введите **InTime**, выберите **InTime** на панели результатов и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="3901b-133">In the search box, type **InTime**, select **InTime** from result panel then click **Add** button to add the application.</span></span>

    ![InTime в списке результатов](./media/active-directory-saas-intime-tutorial/tutorial_intime_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="3901b-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="3901b-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="3901b-136">В этом разделе описана настройка и проверка единого входа Azure AD в приложение InTime с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3901b-136">In this section, you configure and test Azure AD single sign-on with InTime based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3901b-137">Для работы единого входа в Azure AD необходимо знать, какой пользователь в InTime соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3901b-137">For single sign-on to work, Azure AD needs to know what the counterpart user in InTime is to a user in Azure AD.</span></span> <span data-ttu-id="3901b-138">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в InTime.</span><span class="sxs-lookup"><span data-stu-id="3901b-138">In other words, a link relationship between an Azure AD user and the related user in InTime needs to be established.</span></span>

<span data-ttu-id="3901b-139">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в InTime.</span><span class="sxs-lookup"><span data-stu-id="3901b-139">In InTime, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="3901b-140">Чтобы настроить и проверить единый вход Azure AD в InTime, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="3901b-140">To configure and test Azure AD single sign-on with InTime, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3901b-141">**[Настройка единого входа Azure AD](#configure-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="3901b-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3901b-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3901b-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3901b-143">**[Создание тестового пользователя InTime](#create-a-intime-test-user)** требуется для того, чтобы в InTime существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3901b-143">**[Create a InTime test user](#create-a-intime-test-user)** - to have a counterpart of Britta Simon in InTime that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="3901b-144">**[Назначение тестового пользователя Azure AD](#assign-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3901b-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3901b-145">**[Проверка единого входа](#test-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="3901b-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="3901b-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="3901b-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="3901b-147">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении InTime.</span><span class="sxs-lookup"><span data-stu-id="3901b-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your InTime application.</span></span>

<span data-ttu-id="3901b-148">**Чтобы настроить единый вход Azure AD в InTime, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="3901b-148">**To configure Azure AD single sign-on with InTime, perform the following steps:**</span></span>

1. <span data-ttu-id="3901b-149">На портале Azure на странице интеграции с приложением **InTime** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="3901b-149">In the Azure portal, on the **InTime** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="3901b-151">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="3901b-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-intime-tutorial/tutorial_intime_samlbase.png)

3. <span data-ttu-id="3901b-153">В разделе **Домены и URL-адреса приложения InTime** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="3901b-153">On the **InTime Domain and URLs** section, perform the following steps:</span></span>

    ![Сведения о домене и URL-адресах единого входа приложения InTime](./media/active-directory-saas-intime-tutorial/tutorial_intime_url.png)

    <span data-ttu-id="3901b-155">а.</span><span class="sxs-lookup"><span data-stu-id="3901b-155">a.</span></span> <span data-ttu-id="3901b-156">В текстовом поле **URL-адрес для входа** введите URL-адрес: `https://intime6.intimesoft.com/mytime/login/login.xhtml`</span><span class="sxs-lookup"><span data-stu-id="3901b-156">In the **Sign-on URL** textbox, type the URL: `https://intime6.intimesoft.com/mytime/login/login.xhtml`</span></span>

    <span data-ttu-id="3901b-157">b.</span><span class="sxs-lookup"><span data-stu-id="3901b-157">b.</span></span> <span data-ttu-id="3901b-158">В текстовом поле **Идентификатор** введите URL-адрес: `https://auth.intimesoft.com/auth/realms/master`</span><span class="sxs-lookup"><span data-stu-id="3901b-158">In the **Identifier** textbox, type the URL: `https://auth.intimesoft.com/auth/realms/master`</span></span>

4. <span data-ttu-id="3901b-159">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="3901b-159">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Ссылка для скачивания сертификата](./media/active-directory-saas-intime-tutorial/tutorial_intime_certificate.png) 

5. <span data-ttu-id="3901b-161">Приложение InTime ожидает утверждения SAML в определенном формате, который требует добавить настраиваемые сопоставления атрибутов в вашу конфигурацию атрибутов токена SAML.</span><span class="sxs-lookup"><span data-stu-id="3901b-161">Your InTime application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token attributes configuration.</span></span> <span data-ttu-id="3901b-162">На следующем снимке экрана приведен пример.</span><span class="sxs-lookup"><span data-stu-id="3901b-162">The following screenshot shows an example for this.</span></span> <span data-ttu-id="3901b-163">По умолчанию **идентификатор пользователя** имеет значение **user.userprincipalname**, но для InTime требуется сопоставить это значение с адресом электронной почты пользователя.</span><span class="sxs-lookup"><span data-stu-id="3901b-163">The default value of **User Identifier** is **user.userprincipalname** but InTime expects this to be mapped with the user's email address.</span></span> <span data-ttu-id="3901b-164">Для этого можно использовать атрибут **user.mail** из списка или соответствующее значение атрибута, основанное на конфигурации организации.</span><span class="sxs-lookup"><span data-stu-id="3901b-164">For that you can use **user.mail** attribute from the list or use the appropriate attribute value based on your organization configuration</span></span> 

    ![Настройка атрибута](./media/active-directory-saas-intime-tutorial/tutorial_intime_attribute.png)

6. <span data-ttu-id="3901b-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="3901b-166">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-intime-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="3901b-168">В разделе **Конфигурация InTime** щелкните **Настроить InTime**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="3901b-168">On the **InTime Configuration** section, click **Configure InTime** to open **Configure sign-on** window.</span></span> <span data-ttu-id="3901b-169">Скопируйте **URL-адрес выхода и URL-адрес службы единого входа SAML** из раздела **Quick Reference** (Краткий справочник).</span><span class="sxs-lookup"><span data-stu-id="3901b-169">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Конфигурация InTime](./media/active-directory-saas-intime-tutorial/tutorial_intime_configure.png) 

8. <span data-ttu-id="3901b-171">Чтобы настроить единый вход на стороне **InTime**, нужно передать скачанный **XML-файл метаданных**, а также **URL-адрес выхода и URL-адрес службы единого входа SAML** [группе поддержки InTime](mailto:hdollard@intimesoft.com).</span><span class="sxs-lookup"><span data-stu-id="3901b-171">To configure single sign-on on **InTime** side, you need to send the downloaded **Metadata XML**, **Sign-Out URL, and SAML Single Sign-On Service URL** to [InTime support team](mailto:hdollard@intimesoft.com).</span></span> <span data-ttu-id="3901b-172">Специалисты службы поддержки настроят подключение единого входа SAML на обеих сторонах.</span><span class="sxs-lookup"><span data-stu-id="3901b-172">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="3901b-173">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="3901b-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3901b-174">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="3901b-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3901b-175">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="3901b-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="3901b-176">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="3901b-176">Create an Azure AD test user</span></span>

<span data-ttu-id="3901b-177">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3901b-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="3901b-179">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="3901b-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3901b-180">На портале Azure в области слева нажмите кнопку **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3901b-180">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Кнопка "Azure Active Directory"](./media/active-directory-saas-intime-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="3901b-182">Чтобы открыть список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="3901b-182">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Ссылки "Пользователи и группы" и "Все пользователи"](./media/active-directory-saas-intime-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="3901b-184">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна **Все пользователи** щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="3901b-184">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Кнопка "Добавить"](./media/active-directory-saas-intime-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="3901b-186">В диалоговом окне **Пользователь** сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="3901b-186">In the **User** dialog box, perform the following steps:</span></span>

    ![Диалоговое окно "Пользователь"](./media/active-directory-saas-intime-tutorial/create_aaduser_04.png)

    <span data-ttu-id="3901b-188">а.</span><span class="sxs-lookup"><span data-stu-id="3901b-188">a.</span></span> <span data-ttu-id="3901b-189">В поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3901b-189">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3901b-190">b.</span><span class="sxs-lookup"><span data-stu-id="3901b-190">b.</span></span> <span data-ttu-id="3901b-191">В поле **Имя пользователя** введите адрес электронной почты для пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3901b-191">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="3901b-192">c.</span><span class="sxs-lookup"><span data-stu-id="3901b-192">c.</span></span> <span data-ttu-id="3901b-193">Установите флажок **Показать пароль** и запишите значение, которое отображается в поле **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="3901b-193">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="3901b-194">г)</span><span class="sxs-lookup"><span data-stu-id="3901b-194">d.</span></span> <span data-ttu-id="3901b-195">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="3901b-195">Click **Create**.</span></span>
 
### <a name="create-a-intime-test-user"></a><span data-ttu-id="3901b-196">Создание тестового пользователя InTime</span><span class="sxs-lookup"><span data-stu-id="3901b-196">Create a InTime test user</span></span>

<span data-ttu-id="3901b-197">В этом разделе описано, как создать пользователя Britta Simon в приложении InTime.</span><span class="sxs-lookup"><span data-stu-id="3901b-197">In this section, you create a user called Britta Simon in InTime.</span></span> <span data-ttu-id="3901b-198">Обратитесь к [группе поддержки InTime](mailto:hdollard@intimesoft.com), чтобы добавить пользователей на платформу InTime.</span><span class="sxs-lookup"><span data-stu-id="3901b-198">Work with [InTime support team](mailto:hdollard@intimesoft.com) to add the users in the InTime platform.</span></span> <span data-ttu-id="3901b-199">Перед использованием единого входа необходимо создать и активировать пользователей.</span><span class="sxs-lookup"><span data-stu-id="3901b-199">Users must be created and activated before you use single sign-on.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="3901b-200">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="3901b-200">Assign the Azure AD test user</span></span>

<span data-ttu-id="3901b-201">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к InTime.</span><span class="sxs-lookup"><span data-stu-id="3901b-201">In this section, you enable Britta Simon to use Azure single sign-on by granting access to InTime.</span></span>

![Назначение роли пользователя][200] 

<span data-ttu-id="3901b-203">**Чтобы назначить пользователя Britta Simon в InTime, сделайте следующее.**</span><span class="sxs-lookup"><span data-stu-id="3901b-203">**To assign Britta Simon to InTime, perform the following steps:**</span></span>

1. <span data-ttu-id="3901b-204">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="3901b-204">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="3901b-206">Из списка приложений выберите **InTime**.</span><span class="sxs-lookup"><span data-stu-id="3901b-206">In the applications list, select **InTime**.</span></span>

    ![Ссылка на InTime в списке "Приложения"](./media/active-directory-saas-intime-tutorial/tutorial_intime_app.png)  

3. <span data-ttu-id="3901b-208">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="3901b-208">In the menu on the left, click **Users and groups**.</span></span>

    ![Ссылка "Пользователи и группы"][202]

4. <span data-ttu-id="3901b-210">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="3901b-210">Click **Add** button.</span></span> <span data-ttu-id="3901b-211">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="3901b-211">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Область "Добавление назначения"][203]

5. <span data-ttu-id="3901b-213">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="3901b-213">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3901b-214">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="3901b-214">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3901b-215">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="3901b-215">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="3901b-216">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="3901b-216">Test single sign-on</span></span>

<span data-ttu-id="3901b-217">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="3901b-217">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="3901b-218">Если щелкнуть элемент "InTime" на панели доступа, должна появиться страница входа в приложение InTime.</span><span class="sxs-lookup"><span data-stu-id="3901b-218">When you click the InTime tile in the Access Panel, you should get the login page of your InTime application.</span></span> <span data-ttu-id="3901b-219">Нажмите кнопку **Login** (Вход), после чего в списке кнопок отобразится несколько IdP.</span><span class="sxs-lookup"><span data-stu-id="3901b-219">Click the **Login** button, then a series of IdPs will be displayed on a list of buttons.</span></span> <span data-ttu-id="3901b-220">Нажмите кнопку с **именем IdP**, предоставленным [группой поддержки InTime](mailto:hdollard@intimesoft.com), чтобы войти в приложение InTime.</span><span class="sxs-lookup"><span data-stu-id="3901b-220">click **IDP name** given by [InTime support team](mailto:hdollard@intimesoft.com) to login into your InTime application.</span></span> <span data-ttu-id="3901b-221">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3901b-221">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="3901b-222">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="3901b-222">Additional resources</span></span>

* [<span data-ttu-id="3901b-223">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3901b-223">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3901b-224">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3901b-224">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-intime-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-intime-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-intime-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-intime-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-intime-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-intime-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-intime-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-intime-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-intime-tutorial/tutorial_general_203.png

