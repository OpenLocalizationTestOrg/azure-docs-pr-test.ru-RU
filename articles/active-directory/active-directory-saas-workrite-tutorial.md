---
title: "Руководство по интеграции Azure Active Directory с Workrite | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и Workrite."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 2a5c2956-a011-4d5c-877b-80679b6587b5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: 4358c4c621634c17cbbd7fa1c72f12746b8e4a2a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workrite"></a><span data-ttu-id="402b7-103">Руководство. Интеграция Azure Active Directory с Workrite</span><span class="sxs-lookup"><span data-stu-id="402b7-103">Tutorial: Azure Active Directory integration with Workrite</span></span>

<span data-ttu-id="402b7-104">В этом руководстве описано, как интегрировать Workrite с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="402b7-104">In this tutorial, you learn how to integrate Workrite with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="402b7-105">Интеграция Workrite с Azure AD обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="402b7-105">Integrating Workrite with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="402b7-106">С помощью Azure AD вы можете контролировать доступ к Workrite.</span><span class="sxs-lookup"><span data-stu-id="402b7-106">You can control in Azure AD who has access to Workrite.</span></span>
- <span data-ttu-id="402b7-107">Вы можете включить автоматический вход пользователей в Workrite (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="402b7-107">You can enable your users to automatically get signed-on to Workrite (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="402b7-108">Вы можете управлять учетными записями централизованно — на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="402b7-108">You can manage your accounts in one central location - the Azure portal.</span></span>

<span data-ttu-id="402b7-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="402b7-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="402b7-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="402b7-110">Prerequisites</span></span>

<span data-ttu-id="402b7-111">Чтобы настроить интеграцию Azure AD с Workrite, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="402b7-111">To configure Azure AD integration with Workrite, you need the following items:</span></span>

- <span data-ttu-id="402b7-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="402b7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="402b7-113">подписка Workrite с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="402b7-113">A Workrite single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="402b7-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="402b7-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="402b7-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="402b7-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="402b7-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="402b7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="402b7-117">Если у вас нет пробной среды Azure AD, вы можете [получить пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="402b7-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="402b7-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="402b7-118">Scenario description</span></span>
<span data-ttu-id="402b7-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="402b7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="402b7-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="402b7-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="402b7-121">Добавление Workrite из коллекции</span><span class="sxs-lookup"><span data-stu-id="402b7-121">Adding Workrite from the gallery</span></span>
2. <span data-ttu-id="402b7-122">Настройка и проверка единого входа в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="402b7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-workrite-from-the-gallery"></a><span data-ttu-id="402b7-123">Добавление Workrite из коллекции</span><span class="sxs-lookup"><span data-stu-id="402b7-123">Adding Workrite from the gallery</span></span>
<span data-ttu-id="402b7-124">Чтобы настроить интеграцию Workrite с Azure AD, необходимо добавить Workrite из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="402b7-124">To configure the integration of Workrite into Azure AD, you need to add Workrite from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="402b7-125">**Чтобы добавить Workrite из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="402b7-125">**To add Workrite from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="402b7-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="402b7-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Кнопка "Azure Active Directory"][1]

2. <span data-ttu-id="402b7-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="402b7-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="402b7-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="402b7-129">Then go to **All applications**.</span></span>

    ![Колонка "Корпоративные приложения"][2]
    
3. <span data-ttu-id="402b7-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="402b7-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Кнопка "Новое приложение"][3]

4. <span data-ttu-id="402b7-133">В поле поиска введите **Workrite**, выберите **Workrite** на панели результатов и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="402b7-133">In the search box, type **Workrite**, select **Workrite** from result panel then click **Add** button to add the application.</span></span>

    ![Workrite в списке результатов](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="402b7-135">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="402b7-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="402b7-136">В этом разделе описана настройка и проверка единого входа Azure AD в Workrite с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="402b7-136">In this section, you configure and test Azure AD single sign-on with Workrite based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="402b7-137">Чтобы единый вход работал, Azure AD необходима информация о том, какой пользователь в Workrite соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="402b7-137">For single sign-on to work, Azure AD needs to know what the counterpart user in Workrite is to a user in Azure AD.</span></span> <span data-ttu-id="402b7-138">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Workrite.</span><span class="sxs-lookup"><span data-stu-id="402b7-138">In other words, a link relationship between an Azure AD user and the related user in Workrite needs to be established.</span></span>

<span data-ttu-id="402b7-139">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Workrite.</span><span class="sxs-lookup"><span data-stu-id="402b7-139">In Workrite, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="402b7-140">Чтобы настроить и проверить единый вход Azure AD в Workrite, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="402b7-140">To configure and test Azure AD single sign-on with Workrite, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="402b7-141">**[Настройка единого входа Azure AD](#configure-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="402b7-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="402b7-142">**[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="402b7-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="402b7-143">**[Создание тестового пользователя Workrite](#create-a-workrite-test-user)** требуется для того, чтобы в Workrite существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="402b7-143">**[Create a Workrite test user](#create-a-workrite-test-user)** - to have a counterpart of Britta Simon in Workrite that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="402b7-144">**[Назначение тестового пользователя Azure AD](#assign-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход Azure AD.</span><span class="sxs-lookup"><span data-stu-id="402b7-144">**[Assign the Azure AD test user](#assign-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="402b7-145">**[Проверка единого входа](#test-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="402b7-145">**[Test single sign-on](#test-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="402b7-146">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="402b7-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="402b7-147">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Workrite.</span><span class="sxs-lookup"><span data-stu-id="402b7-147">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Workrite application.</span></span>

<span data-ttu-id="402b7-148">**Чтобы настроить единый вход Azure AD в Workrite, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="402b7-148">**To configure Azure AD single sign-on with Workrite, perform the following steps:**</span></span>

1. <span data-ttu-id="402b7-149">На портале Azure на странице интеграции с приложением **Workrite** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="402b7-149">In the Azure portal, on the **Workrite** application integration page, click **Single sign-on**.</span></span>

    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="402b7-151">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="402b7-151">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_samlbase.png)

3. <span data-ttu-id="402b7-153">В разделе **Домены и URL-адреса приложения Workrite** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="402b7-153">On the **Workrite Domain and URLs** section, perform the following steps:</span></span>

    ![Сведения о домене и URL-адресах единого входа приложения Workrite](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_url.png)

    <span data-ttu-id="402b7-155">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://app.workrite.co.uk/securelogin/samlgateway.aspx?id=<uniqueid>`</span><span class="sxs-lookup"><span data-stu-id="402b7-155">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://app.workrite.co.uk/securelogin/samlgateway.aspx?id=<uniqueid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="402b7-156">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="402b7-156">This value is not real.</span></span> <span data-ttu-id="402b7-157">Вместо него необходимо указать фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="402b7-157">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="402b7-158">Для получения этого значения обратитесь к [группе поддержки клиентов Workrite](mailto:support@workrite.co.uk).</span><span class="sxs-lookup"><span data-stu-id="402b7-158">Contact [Workrite Client support team](mailto:support@workrite.co.uk) to get this value.</span></span>

4. <span data-ttu-id="402b7-159">В разделе **Сертификат подписи SAML** щелкните **Сертификат (Base64)**, а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="402b7-159">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Ссылка для скачивания сертификата](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_certificate.png) 

5. <span data-ttu-id="402b7-161">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="402b7-161">Click **Save** button.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-workrite-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="402b7-163">В разделе **Конфигурация Workrite** щелкните **Настроить Workrite**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="402b7-163">On the **Workrite Configuration** section, click **Configure Workrite** to open **Configure sign-on** window.</span></span> <span data-ttu-id="402b7-164">Скопируйте **URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML**  из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="402b7-164">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Конфигурация Workrite](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_configure.png) 

7. <span data-ttu-id="402b7-166">Чтобы настроить единый вход на стороне **Workrite**, нужно отправить скачанный **сертификат в кодировке Base64, URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML** [группе поддержки Workrite](mailto:support@workrite.co.uk).</span><span class="sxs-lookup"><span data-stu-id="402b7-166">To configure single sign-on on **Workrite** side, you need to send the downloaded **Certificate(Base64), Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** to [Workrite support team](mailto:support@workrite.co.uk).</span></span>

> [!TIP]
> <span data-ttu-id="402b7-167">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="402b7-167">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="402b7-168">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="402b7-168">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="402b7-169">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="402b7-169">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="402b7-170">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="402b7-170">Create an Azure AD test user</span></span>

<span data-ttu-id="402b7-171">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="402b7-171">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

   ![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="402b7-173">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="402b7-173">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="402b7-174">На портале Azure в области слева нажмите кнопку **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="402b7-174">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Кнопка "Azure Active Directory"](./media/active-directory-saas-workrite-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="402b7-176">Чтобы открыть список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="402b7-176">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>

    ![Ссылки "Пользователи и группы" и "Все пользователи"](./media/active-directory-saas-workrite-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="402b7-178">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна **Все пользователи** щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="402b7-178">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>

    ![Кнопка "Добавить"](./media/active-directory-saas-workrite-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="402b7-180">В диалоговом окне **Пользователь** сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="402b7-180">In the **User** dialog box, perform the following steps:</span></span>

    ![Диалоговое окно "Пользователь"](./media/active-directory-saas-workrite-tutorial/create_aaduser_04.png)

    <span data-ttu-id="402b7-182">а.</span><span class="sxs-lookup"><span data-stu-id="402b7-182">a.</span></span> <span data-ttu-id="402b7-183">В поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="402b7-183">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="402b7-184">b.</span><span class="sxs-lookup"><span data-stu-id="402b7-184">b.</span></span> <span data-ttu-id="402b7-185">В поле **Имя пользователя** введите адрес электронной почты для пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="402b7-185">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="402b7-186">c.</span><span class="sxs-lookup"><span data-stu-id="402b7-186">c.</span></span> <span data-ttu-id="402b7-187">Установите флажок **Показать пароль** и запишите значение, которое отображается в поле **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="402b7-187">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="402b7-188">г)</span><span class="sxs-lookup"><span data-stu-id="402b7-188">d.</span></span> <span data-ttu-id="402b7-189">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="402b7-189">Click **Create**.</span></span>
 
### <a name="create-a-workrite-test-user"></a><span data-ttu-id="402b7-190">Создание тестового пользователя Workrite</span><span class="sxs-lookup"><span data-stu-id="402b7-190">Create a Workrite test user</span></span>

<span data-ttu-id="402b7-191">Цель этого раздела — создать пользователя с именем Britta Simon в Workrite.</span><span class="sxs-lookup"><span data-stu-id="402b7-191">The objective of this section is to create a user called Britta Simon in Workrite.</span></span>

<span data-ttu-id="402b7-192">**Чтобы создать пользователя с именем Britta Simon в Workrite, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="402b7-192">**To create a user called Britta Simon in Workrite, perform the following steps:**</span></span>

1. <span data-ttu-id="402b7-193">Выполните вход на сайт компании Workrite в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="402b7-193">Sign on to your workrite company site as administrator.</span></span>

2. <span data-ttu-id="402b7-194">В области навигации щелкните **Администратор**.</span><span class="sxs-lookup"><span data-stu-id="402b7-194">In the navigation pane, click **Admin**.</span></span>
   
    ![Элемент управления "Admin" (Администратор)][400]

3. <span data-ttu-id="402b7-196">Перейдите в раздел быстрых ссылок и щелкните **Create a User** (Создать пользователя).</span><span class="sxs-lookup"><span data-stu-id="402b7-196">Go to Quick Links, and then click **Create a User**.</span></span>
   
    ![Раздел "Create a User" (Создание пользователя)][401]

4. <span data-ttu-id="402b7-198">В диалоговом окне **Создание пользователя** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="402b7-198">On the **Create User** dialog, perform the following steps:</span></span>
   
    ![Диалоговое окно"Create a User" (Создание пользователя)][402]
    
    <span data-ttu-id="402b7-200">а.</span><span class="sxs-lookup"><span data-stu-id="402b7-200">a.</span></span> <span data-ttu-id="402b7-201">В текстовом поле **Email** (Электронная почта) введите адрес электронной почты пользователя, например Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="402b7-201">In the **Email** textbox, type the email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="402b7-202">b.</span><span class="sxs-lookup"><span data-stu-id="402b7-202">b.</span></span> <span data-ttu-id="402b7-203">В текстовое поле **First Name** (Имя) введите имя пользователя, например Britta.</span><span class="sxs-lookup"><span data-stu-id="402b7-203">In the **First Name** textbox, type the firstname of user like Britta.</span></span>

    <span data-ttu-id="402b7-204">c.</span><span class="sxs-lookup"><span data-stu-id="402b7-204">c.</span></span> <span data-ttu-id="402b7-205">В текстовое поле **Last Name** (Фамилия) введите фамилию пользователя, например Simon.</span><span class="sxs-lookup"><span data-stu-id="402b7-205">In the **Surname** textbox, type the surname of user like Simon.</span></span>
    
    <span data-ttu-id="402b7-206">г)</span><span class="sxs-lookup"><span data-stu-id="402b7-206">d.</span></span> <span data-ttu-id="402b7-207">Выберите значение **Client Administrator** (Администратор клиента) в поле **Choose Role** (Выберите роль).</span><span class="sxs-lookup"><span data-stu-id="402b7-207">Select **Client Administrator** as **Choose Role**.</span></span>
    
    <span data-ttu-id="402b7-208">д.</span><span class="sxs-lookup"><span data-stu-id="402b7-208">e.</span></span> <span data-ttu-id="402b7-209">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="402b7-209">Click **Save**.</span></span>   

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="402b7-210">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="402b7-210">Assign the Azure AD test user</span></span>

<span data-ttu-id="402b7-211">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к Workrite.</span><span class="sxs-lookup"><span data-stu-id="402b7-211">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Workrite.</span></span>

![Назначение роли пользователя][200] 

<span data-ttu-id="402b7-213">**Чтобы назначить пользователя Britta Simon в Workrite, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="402b7-213">**To assign Britta Simon to Workrite, perform the following steps:**</span></span>

1. <span data-ttu-id="402b7-214">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="402b7-214">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="402b7-216">В списке приложений выберите **Workrite**.</span><span class="sxs-lookup"><span data-stu-id="402b7-216">In the applications list, select **Workrite**.</span></span>

    ![Ссылка на Workrite в списке "Приложения"](./media/active-directory-saas-workrite-tutorial/tutorial_workrite_app.png)  

3. <span data-ttu-id="402b7-218">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="402b7-218">In the menu on the left, click **Users and groups**.</span></span>

    ![Ссылка "Пользователи и группы"][202]

4. <span data-ttu-id="402b7-220">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="402b7-220">Click **Add** button.</span></span> <span data-ttu-id="402b7-221">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="402b7-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Область "Добавление назначения"][203]

5. <span data-ttu-id="402b7-223">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="402b7-223">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="402b7-224">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="402b7-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="402b7-225">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="402b7-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="402b7-226">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="402b7-226">Test single sign-on</span></span>

<span data-ttu-id="402b7-227">Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="402b7-227">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="402b7-228">Щелкнув плитку Workrite на панели доступа, вы автоматически войдете в приложение Workrite.</span><span class="sxs-lookup"><span data-stu-id="402b7-228">When you click the Workrite tile in the Access Panel, you should get automatically signed-on to your Workrite application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="402b7-229">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="402b7-229">Additional resources</span></span>

* [<span data-ttu-id="402b7-230">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="402b7-230">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="402b7-231">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="402b7-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-workrite-tutorial/tutorial_general_203.png
[400]: ./media/active-directory-saas-workrite-tutorial/tutorial_workrite_400.png
[401]: ./media/active-directory-saas-workrite-tutorial/tutorial_workrite_401.png
[402]: ./media/active-directory-saas-workrite-tutorial/tutorial_workrite_402.png

