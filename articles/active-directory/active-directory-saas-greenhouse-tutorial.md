---
title: "Учебник. Интеграция Azure Active Directory с Greenhouse | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и Greenhouse."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 78ec1766-4f79-4f16-9a66-d5584c4b6151
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: d3aba4aab8ded8749db2bf8197f57a6763008c60
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-greenhouse"></a><span data-ttu-id="d3e1f-103">Руководство. Интеграция Azure Active Directory с Greenhouse</span><span class="sxs-lookup"><span data-stu-id="d3e1f-103">Tutorial: Azure Active Directory integration with Greenhouse</span></span>

<span data-ttu-id="d3e1f-104">В этом руководстве описано, как интегрировать Greenhouse с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d3e1f-104">In this tutorial, you learn how to integrate Greenhouse with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="d3e1f-105">Интеграция Azure AD с приложением Greenhouse обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="d3e1f-105">Integrating Greenhouse with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="d3e1f-106">С помощью Azure AD вы можете контролировать доступ к Greenhouse.</span><span class="sxs-lookup"><span data-stu-id="d3e1f-106">You can control in Azure AD who has access to Greenhouse.</span></span>
- <span data-ttu-id="d3e1f-107">Вы можете включить автоматический вход пользователей в Greenhouse (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d3e1f-107">You can enable your users to automatically get signed-on to Greenhouse (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="d3e1f-108">Вы можете управлять учетными записями централизованно — на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="d3e1f-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="d3e1f-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="d3e1f-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d3e1f-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="d3e1f-110">Prerequisites</span></span>

<span data-ttu-id="d3e1f-111">Чтобы настроить интеграцию Azure AD с приложением Greenhouse, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="d3e1f-111">To configure Azure AD integration with Greenhouse, you need the following items:</span></span>

- <span data-ttu-id="d3e1f-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="d3e1f-112">An Azure AD subscription</span></span>
- <span data-ttu-id="d3e1f-113">подписка с поддержкой единого входа Greenhouse.</span><span class="sxs-lookup"><span data-stu-id="d3e1f-113">A Greenhouse single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="d3e1f-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="d3e1f-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="d3e1f-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="d3e1f-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="d3e1f-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="d3e1f-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="d3e1f-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d3e1f-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="d3e1f-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="d3e1f-118">Scenario description</span></span>
<span data-ttu-id="d3e1f-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="d3e1f-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="d3e1f-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="d3e1f-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="d3e1f-121">Добавление Greenhouse из коллекции</span><span class="sxs-lookup"><span data-stu-id="d3e1f-121">Adding Greenhouse from the gallery</span></span>
2. <span data-ttu-id="d3e1f-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="d3e1f-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-greenhouse-from-the-gallery"></a><span data-ttu-id="d3e1f-123">Добавление Greenhouse из коллекции</span><span class="sxs-lookup"><span data-stu-id="d3e1f-123">Adding Greenhouse from the gallery</span></span>
<span data-ttu-id="d3e1f-124">Чтобы настроить интеграцию Greenhouse с Azure AD, необходимо добавить Greenhouse из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="d3e1f-124">To configure the integration of Greenhouse into Azure AD, you need to add Greenhouse from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="d3e1f-125">**Чтобы добавить Greenhouse из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="d3e1f-125">**To add Greenhouse from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="d3e1f-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d3e1f-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка "Azure Active Directory"][1]

2. <span data-ttu-id="d3e1f-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="d3e1f-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="d3e1f-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="d3e1f-129">Then go to **All applications**.</span></span>

    ![Колонка "Корпоративные приложения"][2]
    
3. <span data-ttu-id="d3e1f-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="d3e1f-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Кнопка "Новое приложение"][3]

4. <span data-ttu-id="d3e1f-133">В поле поиска введите **Greenhouse**, выберите **Greenhouse** на панели результатов и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="d3e1f-133">In the search box, type **Greenhouse**, select **Greenhouse** from result panel then click **Add** button to add the application.</span></span>

    ![Greenhouse в списке результатов](./media/active-directory-saas-greenhouse-tutorial/tutorial_greenhouse_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="d3e1f-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="d3e1f-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="d3e1f-136">В этом разделе описана настройка и проверка единого входа Azure AD в приложение Greenhouse с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d3e1f-136">In this section, you configure and test Azure AD single sign-on with Greenhouse based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="d3e1f-137">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Greenhouse соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d3e1f-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Greenhouse is to a user in Azure AD.</span></span> <span data-ttu-id="d3e1f-138">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Greenhouse.</span><span class="sxs-lookup"><span data-stu-id="d3e1f-138">In other words, a link relationship between an Azure AD user and the related user in Greenhouse needs to be established.</span></span>

<span data-ttu-id="d3e1f-139">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Greenhouse.</span><span class="sxs-lookup"><span data-stu-id="d3e1f-139">In Greenhouse, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="d3e1f-140">Чтобы настроить и проверить единый вход Azure AD в Greenhouse, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="d3e1f-140">To configure and test Azure AD single sign-on with Greenhouse, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="d3e1f-141">**[Настройка единого входа Azure AD](#configure-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="d3e1f-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="d3e1f-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d3e1f-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="d3e1f-143">**[Создание тестового пользователя приложения Greenhouse](#create-a-greenhouse-test-user)** требуется для создания в Greenhouse пользователя Britta Simon, связанного с представлением пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d3e1f-143">**[Create a Greenhouse test user](#create-a-greenhouse-test-user)** - to have a counterpart of Britta Simon in Greenhouse that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="d3e1f-144">**[Назначение тестового пользователя Azure AD](#assign-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d3e1f-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="d3e1f-145">**[Проверка единого входа](#test-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="d3e1f-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="d3e1f-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="d3e1f-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="d3e1f-147">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Greenhouse.</span><span class="sxs-lookup"><span data-stu-id="d3e1f-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Greenhouse application.</span></span>

<span data-ttu-id="d3e1f-148">**Чтобы настроить единый вход Azure AD в Greenhouse, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="d3e1f-148">**To configure Azure AD single sign-on with Greenhouse, perform the following steps:**</span></span>

1. <span data-ttu-id="d3e1f-149">На портале Azure на странице интеграции с приложением **Greenhouse** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="d3e1f-149">In the Azure portal, on the **Greenhouse** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="d3e1f-151">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="d3e1f-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-greenhouse-tutorial/tutorial_greenhouse_samlbase.png)

3. <span data-ttu-id="d3e1f-153">В разделе **Домены и URL-адреса приложения Greenhouse** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="d3e1f-153">On the **Greenhouse Domain and URLs** section, perform the following steps:</span></span>

    ![Сведения о домене и URL-адресах единого входа приложения Greenhouse](./media/active-directory-saas-greenhouse-tutorial/tutorial_greenhouse_url.png)

    <span data-ttu-id="d3e1f-155">а.</span><span class="sxs-lookup"><span data-stu-id="d3e1f-155">a.</span></span> <span data-ttu-id="d3e1f-156">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<companyname>.greenhouse.io`</span><span class="sxs-lookup"><span data-stu-id="d3e1f-156">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.greenhouse.io`</span></span>

    <span data-ttu-id="d3e1f-157">b.</span><span class="sxs-lookup"><span data-stu-id="d3e1f-157">b.</span></span> <span data-ttu-id="d3e1f-158">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<companyname>.greenhouse.io`</span><span class="sxs-lookup"><span data-stu-id="d3e1f-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.greenhouse.io`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="d3e1f-159">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="d3e1f-159">These values are not real.</span></span> <span data-ttu-id="d3e1f-160">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="d3e1f-160">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="d3e1f-161">Чтобы получить эти значения, обратитесь к [группе поддержки Greenhouse](https://www.greenhouse.io/contact).</span><span class="sxs-lookup"><span data-stu-id="d3e1f-161">Contact [Greenhouse Client support team](https://www.greenhouse.io/contact) to get these values.</span></span> 
 


4. <span data-ttu-id="d3e1f-162">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="d3e1f-162">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Ссылка для скачивания сертификата](./media/active-directory-saas-greenhouse-tutorial/tutorial_greenhouse_certificate.png) 

5. <span data-ttu-id="d3e1f-164">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="d3e1f-164">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-greenhouse-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="d3e1f-166">Чтобы настроить единый вход на стороне **Greenhouse**, отправьте скачанный **XML-файл метаданных** в [службу поддержки Greenhouse](http://www.greenhouse.io/contact).</span><span class="sxs-lookup"><span data-stu-id="d3e1f-166">To configure single sign-on on **Greenhouse** side, you need to send the downloaded **Metadata XML** to [Greenhouse support team](http://www.greenhouse.io/contact).</span></span>

> [!TIP]
> <span data-ttu-id="d3e1f-167">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="d3e1f-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="d3e1f-168">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="d3e1f-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="d3e1f-169">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="d3e1f-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="d3e1f-170">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="d3e1f-170">Create an Azure AD test user</span></span>

<span data-ttu-id="d3e1f-171">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d3e1f-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="d3e1f-173">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="d3e1f-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="d3e1f-174">На портале Azure в области слева нажмите кнопку **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d3e1f-174">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Кнопка "Azure Active Directory"](./media/active-directory-saas-greenhouse-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="d3e1f-176">Чтобы открыть список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="d3e1f-176">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Ссылки "Пользователи и группы" и "Все пользователи"](./media/active-directory-saas-greenhouse-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="d3e1f-178">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна **Все пользователи** щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="d3e1f-178">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Кнопка "Добавить"](./media/active-directory-saas-greenhouse-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="d3e1f-180">В диалоговом окне **Пользователь** сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="d3e1f-180">In the **User** dialog box, perform the following steps:</span></span>

    ![Диалоговое окно "Пользователь"](./media/active-directory-saas-greenhouse-tutorial/create_aaduser_04.png)

    <span data-ttu-id="d3e1f-182">а.</span><span class="sxs-lookup"><span data-stu-id="d3e1f-182">a.</span></span> <span data-ttu-id="d3e1f-183">В поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="d3e1f-183">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="d3e1f-184">b.</span><span class="sxs-lookup"><span data-stu-id="d3e1f-184">b.</span></span> <span data-ttu-id="d3e1f-185">В поле **Имя пользователя** введите адрес электронной почты для пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="d3e1f-185">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="d3e1f-186">c.</span><span class="sxs-lookup"><span data-stu-id="d3e1f-186">c.</span></span> <span data-ttu-id="d3e1f-187">Установите флажок **Показать пароль** и запишите значение, которое отображается в поле **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="d3e1f-187">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="d3e1f-188">г)</span><span class="sxs-lookup"><span data-stu-id="d3e1f-188">d.</span></span> <span data-ttu-id="d3e1f-189">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="d3e1f-189">Click **Create**.</span></span>
 
### <a name="create-a-greenhouse-test-user"></a><span data-ttu-id="d3e1f-190">Создание тестового пользователя Greenhouse</span><span class="sxs-lookup"><span data-stu-id="d3e1f-190">Create a Greenhouse test user</span></span>

<span data-ttu-id="d3e1f-191">Чтобы пользователи Azure AD могли выполнять вход в Greenhouse, они должны быть подготовлены для Greenhouse.</span><span class="sxs-lookup"><span data-stu-id="d3e1f-191">In order to enable Azure AD users to log into Greenhouse, they must be provisioned into Greenhouse.</span></span> <span data-ttu-id="d3e1f-192">В случае с Greenhouse подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="d3e1f-192">In the case of Greenhouse, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="d3e1f-193">Вы можете использовать любые другие средства создания учетной записи пользователя Greenhouse или API, предоставляемые Greenhouse для подготовки учетных записей пользователя AAD.</span><span class="sxs-lookup"><span data-stu-id="d3e1f-193">You can use any other Greenhouse user account creation tools or APIs provided by Greenhouse to provision AAD user accounts.</span></span> 

<span data-ttu-id="d3e1f-194">**Чтобы подготовить учетные записи пользователей, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="d3e1f-194">**To provision a user accounts, perform the following steps:**</span></span>

1. <span data-ttu-id="d3e1f-195">Выполните вход на веб-сайт компании **Greenhouse** в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="d3e1f-195">Log in to your **Greenhouse** company site as an administrator.</span></span>

2. <span data-ttu-id="d3e1f-196">В меню вверху щелкните **Configure** (Настройка) и выберите **Users** (Пользователи).</span><span class="sxs-lookup"><span data-stu-id="d3e1f-196">In the menu on the top, click **Configure**, and then click **Users**.</span></span>
   
   <span data-ttu-id="d3e1f-197">![Пользователи](./media/active-directory-saas-greenhouse-tutorial/ic790791.png "Пользователи")</span><span class="sxs-lookup"><span data-stu-id="d3e1f-197">![Users](./media/active-directory-saas-greenhouse-tutorial/ic790791.png "Users")</span></span>

3. <span data-ttu-id="d3e1f-198">Нажмите кнопку **Новые пользователи**.</span><span class="sxs-lookup"><span data-stu-id="d3e1f-198">Click **New Users**.</span></span>
   
   <span data-ttu-id="d3e1f-199">![Новый пользователь](./media/active-directory-saas-greenhouse-tutorial/ic790792.png "Новый пользователь")</span><span class="sxs-lookup"><span data-stu-id="d3e1f-199">![New User](./media/active-directory-saas-greenhouse-tutorial/ic790792.png "New User")</span></span>

4. <span data-ttu-id="d3e1f-200">В разделе **Добавить нового пользователя** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="d3e1f-200">In the **Add New User** section, perform the following steps:</span></span>
   
   <span data-ttu-id="d3e1f-201">![Добавление нового пользователя](./media/active-directory-saas-greenhouse-tutorial/ic790793.png "Добавление нового пользователя")</span><span class="sxs-lookup"><span data-stu-id="d3e1f-201">![Add New User](./media/active-directory-saas-greenhouse-tutorial/ic790793.png "Add New User")</span></span>

   <span data-ttu-id="d3e1f-202">а.</span><span class="sxs-lookup"><span data-stu-id="d3e1f-202">a.</span></span> <span data-ttu-id="d3e1f-203">В текстовом поле **Введите адреса электронной почты пользователей** укажите адрес электронной почты действующей учетной записи Azure Active Directory, которую вы хотите подготовить.</span><span class="sxs-lookup"><span data-stu-id="d3e1f-203">In the **Enter user emails** textbox, type the email address of a valid Azure Active Directory account you want to provision.</span></span>

   <span data-ttu-id="d3e1f-204">b.</span><span class="sxs-lookup"><span data-stu-id="d3e1f-204">b.</span></span> <span data-ttu-id="d3e1f-205">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="d3e1f-205">Click **Save**.</span></span>    
   
      >[!NOTE]
      ><span data-ttu-id="d3e1f-206">Владельцы учетных записей Azure Active Directory получат электронное сообщение со ссылкой для подтверждения учетной записи перед ее активацией.</span><span class="sxs-lookup"><span data-stu-id="d3e1f-206">The Azure Active Directory account holders will receive an email including a link to confirm the account before it becomes active.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="d3e1f-207">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="d3e1f-207">Assign the Azure AD test user</span></span>

<span data-ttu-id="d3e1f-208">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure путем предоставления доступа к Greenhouse.</span><span class="sxs-lookup"><span data-stu-id="d3e1f-208">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Greenhouse.</span></span>

![Назначение роли пользователя][200] 

<span data-ttu-id="d3e1f-210">**Чтобы назначить пользователя Britta Simon в Greenhouse, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="d3e1f-210">**To assign Britta Simon to Greenhouse, perform the following steps:**</span></span>

1. <span data-ttu-id="d3e1f-211">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="d3e1f-211">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="d3e1f-213">В списке приложений выберите **Greenhouse**.</span><span class="sxs-lookup"><span data-stu-id="d3e1f-213">In the applications list, select **Greenhouse**.</span></span>

    ![Ссылка на Greenhouse в списке "Приложения"](./media/active-directory-saas-greenhouse-tutorial/tutorial_greenhouse_app.png)  

3. <span data-ttu-id="d3e1f-215">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="d3e1f-215">In the menu on the left, click **Users and groups**.</span></span>

    ![Ссылка "Пользователи и группы"][202]

4. <span data-ttu-id="d3e1f-217">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="d3e1f-217">Click **Add** button.</span></span> <span data-ttu-id="d3e1f-218">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="d3e1f-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Область "Добавление назначения"][203]

5. <span data-ttu-id="d3e1f-220">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="d3e1f-220">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="d3e1f-221">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="d3e1f-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="d3e1f-222">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="d3e1f-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="d3e1f-223">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="d3e1f-223">Test single sign-on</span></span>

<span data-ttu-id="d3e1f-224">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="d3e1f-224">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="d3e1f-225">Щелкнув элемент Greenhouse на панели доступа, вы автоматически войдете в приложение Greenhouse.</span><span class="sxs-lookup"><span data-stu-id="d3e1f-225">When you click the Greenhouse tile in the Access Panel, you should get automatically signed-on to your Greenhouse application.</span></span>
<span data-ttu-id="d3e1f-226">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="d3e1f-226">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d3e1f-227">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="d3e1f-227">Additional resources</span></span>

* [<span data-ttu-id="d3e1f-228">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d3e1f-228">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="d3e1f-229">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="d3e1f-229">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-greenhouse-tutorial/tutorial_general_203.png

