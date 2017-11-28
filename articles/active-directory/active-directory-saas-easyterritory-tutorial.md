---
title: "Руководство. Интеграция Azure Active Directory с EasyTerritory | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и EasyTerritory."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: d29b362d-e986-4f67-8ff2-e158e49353aa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: jeedes
ms.openlocfilehash: 46f99496397e2ed39b1d9410453dac7983ced612
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-easyterritory"></a><span data-ttu-id="becbe-103">Руководство. Интеграция Azure Active Directory с EasyTerritory</span><span class="sxs-lookup"><span data-stu-id="becbe-103">Tutorial: Azure Active Directory integration with EasyTerritory</span></span>

<span data-ttu-id="becbe-104">В этом руководстве описано, как интегрировать EasyTerritory с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="becbe-104">In this tutorial, you learn how to integrate EasyTerritory with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="becbe-105">Интеграция Azure AD с приложением EasyTerritory обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="becbe-105">Integrating EasyTerritory with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="becbe-106">С помощью Azure AD вы можете контролировать доступ к EasyTerritory.</span><span class="sxs-lookup"><span data-stu-id="becbe-106">You can control in Azure AD who has access to EasyTerritory.</span></span>
- <span data-ttu-id="becbe-107">Вы можете включить автоматический вход пользователей в EasyTerritory (единый вход) с использованием учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="becbe-107">You can enable your users to automatically get signed-on to EasyTerritory (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="becbe-108">Вы можете управлять учетными записями централизованно — на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="becbe-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="becbe-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="becbe-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="becbe-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="becbe-110">Prerequisites</span></span>

<span data-ttu-id="becbe-111">Чтобы настроить интеграцию Azure AD с приложением EasyTerritory, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="becbe-111">To configure Azure AD integration with EasyTerritory, you need the following items:</span></span>

- <span data-ttu-id="becbe-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="becbe-112">An Azure AD subscription</span></span>
- <span data-ttu-id="becbe-113">подписка EasyTerritory с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="becbe-113">A EasyTerritory single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="becbe-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="becbe-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="becbe-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="becbe-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="becbe-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="becbe-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="becbe-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="becbe-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="becbe-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="becbe-118">Scenario description</span></span>
<span data-ttu-id="becbe-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="becbe-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="becbe-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="becbe-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="becbe-121">Добавление приложения EasyTerritory из коллекции</span><span class="sxs-lookup"><span data-stu-id="becbe-121">Adding EasyTerritory from the gallery</span></span>
2. <span data-ttu-id="becbe-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="becbe-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-easyterritory-from-the-gallery"></a><span data-ttu-id="becbe-123">Добавление приложения EasyTerritory из коллекции</span><span class="sxs-lookup"><span data-stu-id="becbe-123">Adding EasyTerritory from the gallery</span></span>
<span data-ttu-id="becbe-124">Чтобы настроить интеграцию EasyTerritory с Azure AD, необходимо добавить EasyTerritory из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="becbe-124">To configure the integration of EasyTerritory into Azure AD, you need to add EasyTerritory from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="becbe-125">**Чтобы добавить EasyTerritory из коллекции, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="becbe-125">**To add EasyTerritory from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="becbe-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="becbe-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка "Azure Active Directory"][1]

2. <span data-ttu-id="becbe-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="becbe-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="becbe-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="becbe-129">Then go to **All applications**.</span></span>

    ![Колонка "Корпоративные приложения"][2]
    
3. <span data-ttu-id="becbe-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="becbe-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Кнопка "Новое приложение"][3]

4. <span data-ttu-id="becbe-133">В поле поиска введите **EasyTerritory**, выберите **EasyTerritory** на панели результатов и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="becbe-133">In the search box, type **EasyTerritory**, select **EasyTerritory** from result panel then click **Add** button to add the application.</span></span>

    ![EasyTerritory в списке результатов](./media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="becbe-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="becbe-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="becbe-136">В этом разделе описана настройка и проверка единого входа Azure AD в EasyTerritory с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="becbe-136">In this section, you configure and test Azure AD single sign-on with EasyTerritory based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="becbe-137">Чтобы настроить единый вход Azure AD, необходимо знать, какой пользователь в EasyTerritory соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="becbe-137">For single sign-on to work, Azure AD needs to know what the counterpart user in EasyTerritory is to a user in Azure AD.</span></span> <span data-ttu-id="becbe-138">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в EasyTerritory.</span><span class="sxs-lookup"><span data-stu-id="becbe-138">In other words, a link relationship between an Azure AD user and the related user in EasyTerritory needs to be established.</span></span>

<span data-ttu-id="becbe-139">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в EasyTerritory.</span><span class="sxs-lookup"><span data-stu-id="becbe-139">In EasyTerritory, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="becbe-140">Чтобы настроить и проверить единый вход Azure AD в EasyTerritory, необходимо выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="becbe-140">To configure and test Azure AD single sign-on with EasyTerritory, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="becbe-141">**[Настройка единого входа Azure AD](#configure-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="becbe-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="becbe-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="becbe-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="becbe-143">**[Создание тестового пользователя EasyTerritory](#create-a-easyterritory-test-user)** требуется для того, чтобы в EasyTerritory существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="becbe-143">**[Create a EasyTerritory test user](#create-a-easyterritory-test-user)** - to have a counterpart of Britta Simon in EasyTerritory that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="becbe-144">**[Назначение тестового пользователя Azure AD](#assign-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход Azure AD.</span><span class="sxs-lookup"><span data-stu-id="becbe-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="becbe-145">**[Проверка единого входа](#test-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="becbe-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="becbe-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="becbe-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="becbe-147">В этом разделе мы включим на портале Azure единый вход Azure AD и настроим его в приложении EasyTerritory.</span><span class="sxs-lookup"><span data-stu-id="becbe-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your EasyTerritory application.</span></span>

<span data-ttu-id="becbe-148">**Чтобы настроить единый вход Azure AD в EasyTerritory, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="becbe-148">**To configure Azure AD single sign-on with EasyTerritory, perform the following steps:**</span></span>

1. <span data-ttu-id="becbe-149">На портале Azure на странице интеграции с приложением **EasyTerritory** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="becbe-149">In the Azure portal, on the **EasyTerritory** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="becbe-151">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="becbe-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_samlbase.png)

3. <span data-ttu-id="becbe-153">Если вы хотите настроить приложение в режиме, инициированном поставщиком удостоверений, в разделе **Домены и URL-адреса приложения EasyTerritory** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="becbe-153">On the **EasyTerritory Domain and URLs** section, perform the following steps if you wish to configure the application in IDP initiated mode:</span></span>

    ![Сведения о домене и URL-адресах единого входа для приложения EasyTerritory](./media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_url.png)

    <span data-ttu-id="becbe-155">а.</span><span class="sxs-lookup"><span data-stu-id="becbe-155">a.</span></span> <span data-ttu-id="becbe-156">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://apps.easyterritory.com/<tenant id>/dev/`</span><span class="sxs-lookup"><span data-stu-id="becbe-156">In the **Identifier** textbox, type a URL using the following pattern: `https://apps.easyterritory.com/<tenant id>/dev/`</span></span>

    <span data-ttu-id="becbe-157">b.</span><span class="sxs-lookup"><span data-stu-id="becbe-157">b.</span></span> <span data-ttu-id="becbe-158">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате: `https://apps.easyterritory.com/<tenant id>/dev/authservices/acs`.</span><span class="sxs-lookup"><span data-stu-id="becbe-158">In the **Reply URL** textbox, type a URL using the following pattern: `https://apps.easyterritory.com/<tenant id>/dev/authservices/acs`</span></span>

4. <span data-ttu-id="becbe-159">Установите флажок **Показать дополнительные параметры URL-адресов**, и выполните следующее действие, если хотите настроить приложение для работы в режиме, инициируемом **поставщиком услуг**:</span><span class="sxs-lookup"><span data-stu-id="becbe-159">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Сведения о домене и URL-адресах единого входа для приложения EasyTerritory](./media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_url1.png)

    <span data-ttu-id="becbe-161">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<company name>.easyterritory.com/`</span><span class="sxs-lookup"><span data-stu-id="becbe-161">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company name>.easyterritory.com/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="becbe-162">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="becbe-162">These values are not real.</span></span> <span data-ttu-id="becbe-163">Замените их фактическими значениями идентификатора, URL-адреса ответа и URL-адреса входа.</span><span class="sxs-lookup"><span data-stu-id="becbe-163">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="becbe-164">Чтобы получить их, обратитесь в [службу поддержки клиентов EasyTerritory](mailto:sales@easyterritory.com).</span><span class="sxs-lookup"><span data-stu-id="becbe-164">Contact [EasyTerritory Client support team](mailto:sales@easyterritory.com) to get these values.</span></span> 

5. <span data-ttu-id="becbe-165">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="becbe-165">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Ссылка для скачивания сертификата](./media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_certificate.png) 

6. <span data-ttu-id="becbe-167">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="becbe-167">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-easyterritory-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="becbe-169">Чтобы настроить единый вход на стороне **EasyTerritory**, отправьте в [службу поддержки EasyTerritory](mailto:sales@easyterritory.com) скачанный **XML-файл метаданных**.</span><span class="sxs-lookup"><span data-stu-id="becbe-169">To configure single sign-on on **EasyTerritory** side, you need to send the downloaded **Metadata XML** to [EasyTerritory support team](mailto:sales@easyterritory.com).</span></span> <span data-ttu-id="becbe-170">Специалисты службы поддержки настроят подключение единого входа SAML на обеих сторонах.</span><span class="sxs-lookup"><span data-stu-id="becbe-170">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="becbe-171">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="becbe-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="becbe-172">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="becbe-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="becbe-173">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="becbe-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="becbe-174">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="becbe-174">Create an Azure AD test user</span></span>

<span data-ttu-id="becbe-175">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="becbe-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="becbe-177">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="becbe-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="becbe-178">На портале Azure в области слева нажмите кнопку **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="becbe-178">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Кнопка "Azure Active Directory"](./media/active-directory-saas-easyterritory-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="becbe-180">Чтобы открыть список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="becbe-180">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Ссылки "Пользователи и группы" и "Все пользователи"](./media/active-directory-saas-easyterritory-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="becbe-182">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна **Все пользователи** щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="becbe-182">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Кнопка "Добавить"](./media/active-directory-saas-easyterritory-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="becbe-184">В диалоговом окне **Пользователь** сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="becbe-184">In the **User** dialog box, perform the following steps:</span></span>

    ![Диалоговое окно "Пользователь"](./media/active-directory-saas-easyterritory-tutorial/create_aaduser_04.png)

    <span data-ttu-id="becbe-186">а.</span><span class="sxs-lookup"><span data-stu-id="becbe-186">a.</span></span> <span data-ttu-id="becbe-187">В поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="becbe-187">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="becbe-188">b.</span><span class="sxs-lookup"><span data-stu-id="becbe-188">b.</span></span> <span data-ttu-id="becbe-189">В поле **Имя пользователя** введите адрес электронной почты для пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="becbe-189">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="becbe-190">c.</span><span class="sxs-lookup"><span data-stu-id="becbe-190">c.</span></span> <span data-ttu-id="becbe-191">Установите флажок **Показать пароль** и запишите значение, которое отображается в поле **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="becbe-191">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="becbe-192">г)</span><span class="sxs-lookup"><span data-stu-id="becbe-192">d.</span></span> <span data-ttu-id="becbe-193">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="becbe-193">Click **Create**.</span></span>
 
### <a name="create-a-easyterritory-test-user"></a><span data-ttu-id="becbe-194">Создание тестового пользователя в EasyTerritory</span><span class="sxs-lookup"><span data-stu-id="becbe-194">Create a EasyTerritory test user</span></span>

<span data-ttu-id="becbe-195">В этом разделе описано, как создать пользователя Britta Simon в приложении EasyTerritory.</span><span class="sxs-lookup"><span data-stu-id="becbe-195">In this section, you create a user called Britta Simon in EasyTerritory.</span></span> <span data-ttu-id="becbe-196">Обратитесь в [службу поддержки EasyTerritory](mailto:sales@easyterritory.com), чтобы добавить пользователей на платформу EasyTerritory.</span><span class="sxs-lookup"><span data-stu-id="becbe-196">Please work with [EasyTerritory support team](mailto:sales@easyterritory.com) to add the users in the EasyTerritory platform.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="becbe-197">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="becbe-197">Assign the Azure AD test user</span></span>

<span data-ttu-id="becbe-198">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure путем предоставления доступа к EasyTerritory.</span><span class="sxs-lookup"><span data-stu-id="becbe-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to EasyTerritory.</span></span>

![Назначение роли пользователя][200] 

<span data-ttu-id="becbe-200">**Чтобы назначить пользователя Britta Simon в EasyTerritory, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="becbe-200">**To assign Britta Simon to EasyTerritory, perform the following steps:**</span></span>

1. <span data-ttu-id="becbe-201">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="becbe-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="becbe-203">В списке приложений выберите **EasyTerritory**.</span><span class="sxs-lookup"><span data-stu-id="becbe-203">In the applications list, select **EasyTerritory**.</span></span>

    ![Ссылка на EasyTerritory в списке "Приложения"](./media/active-directory-saas-easyterritory-tutorial/tutorial_easyterritory_app.png)  

3. <span data-ttu-id="becbe-205">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="becbe-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Ссылка "Пользователи и группы"][202]

4. <span data-ttu-id="becbe-207">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="becbe-207">Click **Add** button.</span></span> <span data-ttu-id="becbe-208">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="becbe-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Область "Добавление назначения"][203]

5. <span data-ttu-id="becbe-210">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="becbe-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="becbe-211">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="becbe-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="becbe-212">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="becbe-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="becbe-213">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="becbe-213">Test single sign-on</span></span>

<span data-ttu-id="becbe-214">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="becbe-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="becbe-215">Щелкнув элемент EasyTerritory на панели доступа, вы автоматически войдете в приложение EasyTerritory.</span><span class="sxs-lookup"><span data-stu-id="becbe-215">When you click the EasyTerritory tile in the Access Panel, you should get automatically signed-on to your EasyTerritory application.</span></span>
<span data-ttu-id="becbe-216">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="becbe-216">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="becbe-217">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="becbe-217">Additional resources</span></span>

* [<span data-ttu-id="becbe-218">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="becbe-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="becbe-219">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="becbe-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)




<!--Image references-->

[1]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-easyterritory-tutorial/tutorial_general_203.png

