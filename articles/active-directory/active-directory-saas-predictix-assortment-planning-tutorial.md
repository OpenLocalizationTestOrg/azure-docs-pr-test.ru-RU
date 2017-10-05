---
title: "Руководство по интеграции Azure Active Directory с Predictix Assortment Planning | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и Predictix Assortment Planning."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 37e686ff-f8e5-40b1-9d7e-f64b076917b7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: cc7ad4aa5260276e26406b6b79c039372e5ee69f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="tutorial-azure-active-directory-integration-with-predictix-assortment-planning"></a><span data-ttu-id="03708-103">Руководство. Интеграция Azure Active Directory с Predictix Assortment Planning</span><span class="sxs-lookup"><span data-stu-id="03708-103">Tutorial: Azure Active Directory integration with Predictix Assortment Planning</span></span>

<span data-ttu-id="03708-104">В этом руководстве описано, как интегрировать Predictix Assortment Planning с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="03708-104">In this tutorial, you learn how to integrate Predictix Assortment Planning with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="03708-105">Интеграция Azure AD с Predictix Assortment Planning дает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="03708-105">Integrating Predictix Assortment Planning with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="03708-106">С помощью Azure AD вы можете контролировать доступ к Predictix Assortment Planning.</span><span class="sxs-lookup"><span data-stu-id="03708-106">You can control in Azure AD who has access to Predictix Assortment Planning.</span></span>
- <span data-ttu-id="03708-107">Вы можете включить автоматический вход пользователей в Predictix Assortment Planning (единый вход) с использованием учетных записей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="03708-107">You can enable your users to automatically get signed-on to Predictix Assortment Planning (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="03708-108">Вы можете управлять учетными записями централизованно — на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="03708-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="03708-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="03708-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="03708-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="03708-110">Prerequisites</span></span>

<span data-ttu-id="03708-111">Чтобы настроить интеграцию Azure AD с Predictix Assortment Planning, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="03708-111">To configure Azure AD integration with Predictix Assortment Planning, you need the following items:</span></span>

- <span data-ttu-id="03708-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="03708-112">An Azure AD subscription</span></span>
- <span data-ttu-id="03708-113">подписка на Predictix Assortment Planning с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="03708-113">A Predictix Assortment Planning single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="03708-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="03708-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="03708-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="03708-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="03708-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="03708-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="03708-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="03708-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="03708-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="03708-118">Scenario description</span></span>
<span data-ttu-id="03708-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="03708-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="03708-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="03708-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="03708-121">Добавление Predictix Assortment Planning из коллекции</span><span class="sxs-lookup"><span data-stu-id="03708-121">Adding Predictix Assortment Planning from the gallery</span></span>
2. <span data-ttu-id="03708-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="03708-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-predictix-assortment-planning-from-the-gallery"></a><span data-ttu-id="03708-123">Добавление Predictix Assortment Planning из коллекции</span><span class="sxs-lookup"><span data-stu-id="03708-123">Adding Predictix Assortment Planning from the gallery</span></span>
<span data-ttu-id="03708-124">Чтобы настроить интеграцию Predictix Assortment Planning с Azure AD, необходимо добавить приложение Predictix Assortment Planning из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="03708-124">To configure the integration of Predictix Assortment Planning into Azure AD, you need to add Predictix Assortment Planning from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="03708-125">**Чтобы добавить Predictix Assortment Planning из коллекции, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="03708-125">**To add Predictix Assortment Planning from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="03708-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="03708-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка "Azure Active Directory"][1]

2. <span data-ttu-id="03708-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="03708-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="03708-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="03708-129">Then go to **All applications**.</span></span>

    ![Колонка "Корпоративные приложения"][2]
    
3. <span data-ttu-id="03708-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="03708-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Кнопка "Новое приложение"][3]

4. <span data-ttu-id="03708-133">В поле поиска введите **Predictix Assortment Planning**, выберите **Predictix Assortment Planning** на панели результатов и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="03708-133">In the search box, type **Predictix Assortment Planning**, select **Predictix Assortment Planning** from result panel then click **Add** button to add the application.</span></span>

    ![Predictix Assortment Planning в списке результатов поиска](./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_predictixassortmentplanning_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="03708-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="03708-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="03708-136">В этом разделе описана настройка и проверка единого входа Azure AD в Predictix Assortment Planning с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="03708-136">In this section, you configure and test Azure AD single sign-on with Predictix Assortment Planning based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="03708-137">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Predictix Assortment Planning соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="03708-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Predictix Assortment Planning is to a user in Azure AD.</span></span> <span data-ttu-id="03708-138">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Predictix Assortment Planning.</span><span class="sxs-lookup"><span data-stu-id="03708-138">In other words, a link relationship between an Azure AD user and the related user in Predictix Assortment Planning needs to be established.</span></span>

<span data-ttu-id="03708-139">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Predictix Assortment Planning.</span><span class="sxs-lookup"><span data-stu-id="03708-139">In Predictix Assortment Planning, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="03708-140">Чтобы настроить и проверить единый вход Azure AD в Predictix Assortment Planning, выполните следующие стандартные действия.</span><span class="sxs-lookup"><span data-stu-id="03708-140">To configure and test Azure AD single sign-on with Predictix Assortment Planning, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="03708-141">**[Настройка единого входа Azure AD](#configure-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="03708-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="03708-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="03708-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="03708-143">**[Создание тестового пользователя Predictix Assortment Planning](#create-a-predictix-assortment-planning-test-user)** требуется для создания в Predictix Assortment Planning пользователя Britta Simon, связанного с соответствующим представлением в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="03708-143">**[Create a Predictix Assortment Planning test user](#create-a-predictix-assortment-planning-test-user)** - to have a counterpart of Britta Simon in Predictix Assortment Planning that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="03708-144">**[Назначение тестового пользователя Azure AD](#assign-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход Azure AD.</span><span class="sxs-lookup"><span data-stu-id="03708-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="03708-145">**[Проверка единого входа](#test-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="03708-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="03708-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="03708-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="03708-147">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Predictix Assortment Planning.</span><span class="sxs-lookup"><span data-stu-id="03708-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Predictix Assortment Planning application.</span></span>

<span data-ttu-id="03708-148">**Чтобы настроить единый вход Azure AD в Predictix Assortment Planning, выполните указанные ниже действия.**</span><span class="sxs-lookup"><span data-stu-id="03708-148">**To configure Azure AD single sign-on with Predictix Assortment Planning, perform the following steps:**</span></span>

1. <span data-ttu-id="03708-149">На портале Azure на странице интеграции с приложением **Predictix Assortment Planning** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="03708-149">In the Azure portal, on the **Predictix Assortment Planning** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="03708-151">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="03708-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_predictixassortmentplanning_samlbase.png)

3. <span data-ttu-id="03708-153">В разделе **Домены и URL-адреса приложения Predictix Assortment Planning** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="03708-153">On the **Predictix Assortment Planning Domain and URLs** section, perform the following steps:</span></span>

    ![Сведения о домене и URL-адресах единого входа для приложения Predictix Assortment Planning](./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_predictixassortmentplanning_url.png)

    <span data-ttu-id="03708-155">а.</span><span class="sxs-lookup"><span data-stu-id="03708-155">a.</span></span> <span data-ttu-id="03708-156">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="03708-156">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|--|
    | `https://<sub-domain>.ap.predictix.com/sso/request`|
    | `https://<sub-domain>.dev.ap.predictix.com/`|

    <span data-ttu-id="03708-157">b.</span><span class="sxs-lookup"><span data-stu-id="03708-157">b.</span></span> <span data-ttu-id="03708-158">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="03708-158">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|--|
    | `https://<sub-domain>.ap.predictix.com`|
    | `https://<sub-domain>.dev.ap.predictix.com`|
    
    > [!NOTE] 
    > <span data-ttu-id="03708-159">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="03708-159">These values are not real.</span></span> <span data-ttu-id="03708-160">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="03708-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="03708-161">Чтобы получить эти значения, обратитесь в [службу поддержки клиентов Predictix Assortment Planning](http://www.infor.com/support).</span><span class="sxs-lookup"><span data-stu-id="03708-161">Contact [Predictix Assortment Planning Client support team](http://www.infor.com/support) to get these values.</span></span> 
 


4. <span data-ttu-id="03708-162">В разделе **Сертификат подписи SAML** щелкните **Сертификат (Base64)**, а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="03708-162">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Ссылка для скачивания сертификата](./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_predictixassortmentplanning_certificate.png) 

5. <span data-ttu-id="03708-164">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="03708-164">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="03708-166">В разделе **Конфигурация Predictix Assortment Planning** щелкните **Настроить Predictix Assortment Planning**, чтобы открыть окно **Настройка входа**.</span><span class="sxs-lookup"><span data-stu-id="03708-166">On the **Predictix Assortment Planning Configuration** section, click **Configure Predictix Assortment Planning** to open **Configure sign-on** window.</span></span> <span data-ttu-id="03708-167">Скопируйте **URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="03708-167">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка Predictix Assortment Planning](./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_predictixassortmentplanning_configure.png) 

7. <span data-ttu-id="03708-169">Чтобы настроить единый вход на стороне **Predictix Assortment Planning**, нужно передать скачанный **сертификат (Base64)**, **идентификатор сущности SAML**, **URL-адрес службы единого входа SAML** и **URL-адрес выхода** в [службу поддержки Predictix Assortment Planning](http://www.infor.com/support).</span><span class="sxs-lookup"><span data-stu-id="03708-169">To configure single sign-on on **Predictix Assortment Planning** side, you need to send the downloaded **Certificate(Base64)**, **SAML Entity ID**, **SAML Single Sign-On Service URL**, and **Sign-Out URL**  to [Predictix Assortment Planning support team](http://www.infor.com/support).</span></span> <span data-ttu-id="03708-170">Специалисты службы поддержки настроят подключение единого входа SAML на обеих сторонах.</span><span class="sxs-lookup"><span data-stu-id="03708-170">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="03708-171">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="03708-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="03708-172">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="03708-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="03708-173">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="03708-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="03708-174">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="03708-174">Create an Azure AD test user</span></span>

<span data-ttu-id="03708-175">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="03708-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="03708-177">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="03708-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="03708-178">На портале Azure в области слева нажмите кнопку **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="03708-178">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Кнопка "Azure Active Directory"](./media/active-directory-saas-predictix-assortment-planning-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="03708-180">Чтобы открыть список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="03708-180">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Ссылки "Пользователи и группы" и "Все пользователи"](./media/active-directory-saas-predictix-assortment-planning-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="03708-182">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна **Все пользователи** щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="03708-182">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Кнопка "Добавить"](./media/active-directory-saas-predictix-assortment-planning-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="03708-184">В диалоговом окне **Пользователь** сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="03708-184">In the **User** dialog box, perform the following steps:</span></span>

    ![Диалоговое окно "Пользователь"](./media/active-directory-saas-predictix-assortment-planning-tutorial/create_aaduser_04.png)

    <span data-ttu-id="03708-186">а.</span><span class="sxs-lookup"><span data-stu-id="03708-186">a.</span></span> <span data-ttu-id="03708-187">В поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="03708-187">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="03708-188">b.</span><span class="sxs-lookup"><span data-stu-id="03708-188">b.</span></span> <span data-ttu-id="03708-189">В поле **Имя пользователя** введите адрес электронной почты для пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="03708-189">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="03708-190">c.</span><span class="sxs-lookup"><span data-stu-id="03708-190">c.</span></span> <span data-ttu-id="03708-191">Установите флажок **Показать пароль** и запишите значение, которое отображается в поле **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="03708-191">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="03708-192">г)</span><span class="sxs-lookup"><span data-stu-id="03708-192">d.</span></span> <span data-ttu-id="03708-193">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="03708-193">Click **Create**.</span></span>
 
### <a name="create-a-predictix-assortment-planning-test-user"></a><span data-ttu-id="03708-194">Создание тестового пользователя Predictix Assortment Planning</span><span class="sxs-lookup"><span data-stu-id="03708-194">Create a Predictix Assortment Planning test user</span></span>

<span data-ttu-id="03708-195">В этом разделе описано, как создать пользователя Britta Simon в приложении Predictix Assortment Planning.</span><span class="sxs-lookup"><span data-stu-id="03708-195">In this section, you create a user called Britta Simon in Predictix Assortment Planning.</span></span> <span data-ttu-id="03708-196">Чтобы добавить пользователей на платформу Predictix Assortment Planning, обратитесь в [службу поддержки Predictix Assortment Planning](http://www.infor.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="03708-196">Please work with [Predictix Assortment Planning support team](http://www.infor.com/contact/) to add the users in the Predictix Assortment Planning platform.</span></span>
 > [!NOTE]
 > <span data-ttu-id="03708-197">Владелец учетной записи Azure Active Directory получит по электронной почте сообщение со ссылкой для активации учетной записи.</span><span class="sxs-lookup"><span data-stu-id="03708-197">The Azure Active Directory account holder receives an email and follows a link to confirm their account before it becomes active.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="03708-198">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="03708-198">Assign the Azure AD test user</span></span>

<span data-ttu-id="03708-199">В этом разделе описано, как позволить пользователю Britta Simon использовать единый вход Azure, предоставив пользователю доступ к Predictix Assortment Planning.</span><span class="sxs-lookup"><span data-stu-id="03708-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Predictix Assortment Planning.</span></span>

![Назначение роли пользователя][200] 

<span data-ttu-id="03708-201">**Чтобы назначить пользователя Britta Simon приложению Predictix Assortment Planning, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="03708-201">**To assign Britta Simon to Predictix Assortment Planning, perform the following steps:**</span></span>

1. <span data-ttu-id="03708-202">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="03708-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="03708-204">В списке приложений выберите **Predictix Assortment Planning**.</span><span class="sxs-lookup"><span data-stu-id="03708-204">In the applications list, select **Predictix Assortment Planning**.</span></span>

    ![В списке приложений выберите ссылку "Predictix Assortment Planning".](./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_predictixassortmentplanning_app.png)  

3. <span data-ttu-id="03708-206">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="03708-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Ссылка "Пользователи и группы"][202]

4. <span data-ttu-id="03708-208">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="03708-208">Click **Add** button.</span></span> <span data-ttu-id="03708-209">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="03708-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Область "Добавление назначения"][203]

5. <span data-ttu-id="03708-211">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="03708-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="03708-212">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="03708-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="03708-213">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="03708-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="03708-214">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="03708-214">Test single sign-on</span></span>

<span data-ttu-id="03708-215">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="03708-215">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="03708-216">Щелкнув элемент Predictix Assortment Planning на панели доступа, вы автоматически войдете в приложение Predictix Assortment Planning.</span><span class="sxs-lookup"><span data-stu-id="03708-216">When you click the Predictix Assortment Planning tile in the Access Panel, you should get automatically signed-on to your Predictix Assortment Planning application.</span></span>
<span data-ttu-id="03708-217">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="03708-217">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="03708-218">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="03708-218">Additional resources</span></span>

* [<span data-ttu-id="03708-219">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="03708-219">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="03708-220">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="03708-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-predictix-assortment-planning-tutorial/tutorial_general_203.png

