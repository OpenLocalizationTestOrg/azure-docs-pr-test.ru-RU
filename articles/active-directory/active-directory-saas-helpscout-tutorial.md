---
title: "Учебник. Интеграция Azure Active Directory с Help Scout | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в приложении Help Scout."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 0aad9910-0bc1-4394-9f73-267cf39973ab
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: jeedes
ms.openlocfilehash: 84cee39c28a0f7e6b9878441e504131795673020
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-help-scout"></a><span data-ttu-id="3bd5d-103">Учебник. Интеграция Azure Active Directory с Help Scout</span><span class="sxs-lookup"><span data-stu-id="3bd5d-103">Tutorial: Azure Active Directory integration with Help Scout</span></span>

<span data-ttu-id="3bd5d-104">В этом учебнике описано, как интегрировать Help Scout с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3bd5d-104">In this tutorial, you learn how to integrate Help Scout with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3bd5d-105">Интеграция Azure AD с Help Scout обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="3bd5d-105">You get the following benefits from integrating Help Scout with Azure AD:</span></span>

- <span data-ttu-id="3bd5d-106">С помощью Azure AD вы можете контролировать доступ к Help Scout.</span><span class="sxs-lookup"><span data-stu-id="3bd5d-106">In Azure AD, you can control who has access to Help Scout.</span></span>
- <span data-ttu-id="3bd5d-107">Вы можете включить автоматический вход пользователей в Help Scout с помощью единого входа и учетной записи пользователя Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3bd5d-107">You can automatically sign in your users to Help Scout by using single sign-on and a user's Azure AD account.</span></span>
- <span data-ttu-id="3bd5d-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="3bd5d-108">You can manage your accounts in one, central location, the Azure portal.</span></span>

<span data-ttu-id="3bd5d-109">Дополнительные сведения об интеграции приложений SaaS с Azure AD см. в статье [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3bd5d-109">To learn more about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3bd5d-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="3bd5d-110">Prerequisites</span></span>

<span data-ttu-id="3bd5d-111">Чтобы настроить интеграцию Azure AD с Help Scout, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="3bd5d-111">To set up Azure AD integration with Help Scout, you need the following items:</span></span>

- <span data-ttu-id="3bd5d-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="3bd5d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3bd5d-113">подписка Help Scout с включенным единым входом.</span><span class="sxs-lookup"><span data-stu-id="3bd5d-113">A Help Scout subscription, with single sign-on turned on</span></span> 

> [!NOTE]
> <span data-ttu-id="3bd5d-114">Мы не рекомендуем использовать рабочую среду для проверки действий, выполняемых в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="3bd5d-114">If you test the steps in this tutorial, we recommend that you don't test them in a production environment.</span></span>

<span data-ttu-id="3bd5d-115">Для проверки действий в этом руководстве соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="3bd5d-115">Recommendations for testing the steps in this tutorial:</span></span>

- <span data-ttu-id="3bd5d-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="3bd5d-116">Do not use your production environment, unless it's necessary.</span></span>
- <span data-ttu-id="3bd5d-117">Если у вас нет пробной среды Azure AD, вы можете [получить бесплатную пробную версию на один месяц](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3bd5d-117">If you don't have an Azure AD trial environment, you can [get a one-month free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3bd5d-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="3bd5d-118">Scenario description</span></span>
<span data-ttu-id="3bd5d-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="3bd5d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> 

<span data-ttu-id="3bd5d-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="3bd5d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3bd5d-121">Добавление Help Scout из галереи.</span><span class="sxs-lookup"><span data-stu-id="3bd5d-121">Add Help Scout from the gallery.</span></span>
2. <span data-ttu-id="3bd5d-122">Настройка и проверка единого входа Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3bd5d-122">Set up and test Azure AD single sign-on.</span></span>

## <a name="add-help-scout-from-the-gallery"></a><span data-ttu-id="3bd5d-123">Добавление Help Scout из галереи</span><span class="sxs-lookup"><span data-stu-id="3bd5d-123">Add Help Scout from the gallery</span></span>
<span data-ttu-id="3bd5d-124">Чтобы настроить интеграцию Help Scout с Azure AD, в галерее необходимо добавить Help Scout в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="3bd5d-124">To set up the integration of Help Scout with Azure AD, in the gallery, add Help Scout to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3bd5d-125">Чтобы добавить Help Scout из галереи, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="3bd5d-125">To add Help Scout from the gallery:</span></span>

1. <span data-ttu-id="3bd5d-126">На [портале Azure](https://portal.azure.com) в меню слева щелкните **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3bd5d-126">In the [Azure portal](https://portal.azure.com), in the left menu, select **Azure Active Directory**.</span></span> 

    ![Кнопка "Azure Active Directory"][1]

2. <span data-ttu-id="3bd5d-128">Перейдите в колонку **Корпоративные приложения** и выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="3bd5d-128">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![Страница "Корпоративные приложения"][2]
    
3. <span data-ttu-id="3bd5d-130">Чтобы добавить новое приложение, выберите **Новое приложение**.</span><span class="sxs-lookup"><span data-stu-id="3bd5d-130">To add a new application, select **New application**.</span></span>

    ![Кнопка "Новое приложение"][3]

4. <span data-ttu-id="3bd5d-132">В поле поиска введите **Help Scout**.</span><span class="sxs-lookup"><span data-stu-id="3bd5d-132">In the search box, enter **Help Scout**.</span></span> <span data-ttu-id="3bd5d-133">В результатах поиска выберите **Help Scout**, а затем щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="3bd5d-133">In the search results, select **Help Scout**, and then select **Add**.</span></span>

    ![Help Scout в списке результатов](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_addfromgallery.png)

## <a name="set-up-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="3bd5d-135">Настройка и проверка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="3bd5d-135">Set up and test Azure AD single sign-on</span></span>

<span data-ttu-id="3bd5d-136">В этом разделе описана настройка и проверка единого входа Azure AD в Help Scout с использованием тестового имени пользователя *Britta Simon*.</span><span class="sxs-lookup"><span data-stu-id="3bd5d-136">In this section, you set up and test Azure AD single sign-on with Help Scout based on a test user named *Britta Simon*.</span></span>

<span data-ttu-id="3bd5d-137">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Azure AD соответствует пользователю в Help Scout.</span><span class="sxs-lookup"><span data-stu-id="3bd5d-137">For single sign-on to work, Azure AD needs to know the Azure AD counterpart user in Help Scout.</span></span> <span data-ttu-id="3bd5d-138">Необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Help Scout.</span><span class="sxs-lookup"><span data-stu-id="3bd5d-138">A link relationship between an Azure AD user and the related user in Help Scout must be established.</span></span>

<span data-ttu-id="3bd5d-139">Для этого назначьте **имя пользователя** Azure AD в качестве значения **имени пользователя** в Help Scout.</span><span class="sxs-lookup"><span data-stu-id="3bd5d-139">To establish the link relationship, in Help Scout, for **Username**, assign the value of the **user name** in Azure AD.</span></span>

<span data-ttu-id="3bd5d-140">Чтобы настроить и проверить единый вход Azure Active Directory в Help Scout, вам потребуется выполнить следующие действия:</span><span class="sxs-lookup"><span data-stu-id="3bd5d-140">To configure and test Azure AD single sign-on with Help Scout, complete the following tasks:</span></span>

1. <span data-ttu-id="3bd5d-141">[Настройка единого входа Azure AD](#set-up-azure-ad-single-sign-on)</span><span class="sxs-lookup"><span data-stu-id="3bd5d-141">[Set up Azure AD single sign-on](#set-up-azure-ad-single-sign-on).</span></span> <span data-ttu-id="3bd5d-142">необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="3bd5d-142">Sets up a user to use this feature.</span></span>
2. <span data-ttu-id="3bd5d-143">[Создание тестового пользователя Azure AD](#create-an-azure-ad-test-user)</span><span class="sxs-lookup"><span data-stu-id="3bd5d-143">[Create an Azure AD test user](#create-an-azure-ad-test-user).</span></span> <span data-ttu-id="3bd5d-144">требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3bd5d-144">Tests Azure AD single sign-on with the user Britta Simon.</span></span>
3. <span data-ttu-id="3bd5d-145">[Создание тестового пользователя Help Scout](#create-a-help-scout-test-user)</span><span class="sxs-lookup"><span data-stu-id="3bd5d-145">[Create a Help Scout test user](#create-a-help-scout-test-user).</span></span> <span data-ttu-id="3bd5d-146">требуется, чтобы в Help Scout существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3bd5d-146">Creates a counterpart of Britta Simon in Help Scout that is linked to the Azure AD representation of the user.</span></span>
4. <span data-ttu-id="3bd5d-147">[Назначение тестового пользователя Azure AD](#assign-the-azure-ad-test-user)</span><span class="sxs-lookup"><span data-stu-id="3bd5d-147">[Assign the Azure AD test user](#assign-the-azure-ad-test-user).</span></span> <span data-ttu-id="3bd5d-148">позволяет пользователю Britta Simon использовать единый вход Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3bd5d-148">Sets up Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3bd5d-149">[Проверка единого входа](#test-single-sign-on)</span><span class="sxs-lookup"><span data-stu-id="3bd5d-149">[Test single sign-on](#test-single-sign-on).</span></span> <span data-ttu-id="3bd5d-150">необходима, чтобы убедиться, что конфигурация работает правильно.</span><span class="sxs-lookup"><span data-stu-id="3bd5d-150">Verifies that the configuration works.</span></span>

### <a name="set-up-azure-ad-single-sign-on"></a><span data-ttu-id="3bd5d-151">Настройка единого входа Azure AD</span><span class="sxs-lookup"><span data-stu-id="3bd5d-151">Set up Azure AD single sign-on</span></span>

<span data-ttu-id="3bd5d-152">В этом разделе вы включите единый вход Azure AD на портале Azure,</span><span class="sxs-lookup"><span data-stu-id="3bd5d-152">In this section, you set up Azure AD single sign-on in the Azure portal.</span></span> <span data-ttu-id="3bd5d-153">а затем настроите его в приложении Help Scout.</span><span class="sxs-lookup"><span data-stu-id="3bd5d-153">Then, you set up single sign-on in your Help Scout application.</span></span>

<span data-ttu-id="3bd5d-154">Чтобы настроить единый вход Azure AD в Help Scout, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="3bd5d-154">To set up Azure AD single sign-on with Help Scout:</span></span>

1. <span data-ttu-id="3bd5d-155">На портале Azure на странице интеграции с приложением **Help Scout** выберите **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="3bd5d-155">In the Azure portal, on the **Help Scout** application integration page, select **Single sign-on**.</span></span>
 
    ![Ссылка "Настройка единого входа"][4]

2. <span data-ttu-id="3bd5d-157">На странице **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**.</span><span class="sxs-lookup"><span data-stu-id="3bd5d-157">On the **Single sign-on** page, for **Mode**, select **SAML-based Sign-on**.</span></span>
 
    ![Диалоговое окно "Единый вход"](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_samlbase.png)

3. <span data-ttu-id="3bd5d-159">Если вы хотите настроить приложение в режиме, инициированном поставщиком удостоверений, в разделе **Домены и URL-адреса приложения Help Scout** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="3bd5d-159">Under **Help Scout Domain and URLs**, if you want to set up the application in IDP-initiated mode, complete the following steps:</span></span>

    1. <span data-ttu-id="3bd5d-160">В поле **Идентификатор** введите URL-адрес в следующем формате: `urn:auth0:helpscout:<instancename>`.</span><span class="sxs-lookup"><span data-stu-id="3bd5d-160">In the **Identifier** box, enter a URL that has the following pattern: `urn:auth0:helpscout:<instancename>`</span></span>

    2. <span data-ttu-id="3bd5d-161">В поле **URL-адрес ответа** введите URL-адрес в следующем формате: `https://helpscout.auth0.com/login/callback?connection=<instancename>`.</span><span class="sxs-lookup"><span data-stu-id="3bd5d-161">In the **Reply URL** box, enter a URL that has the following pattern: `https://helpscout.auth0.com/login/callback?connection=<instancename>`</span></span>

    ![Сведения о домене и URL-адресах единого входа приложения Help Scout](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_url.png)

4. <span data-ttu-id="3bd5d-163">Если вы хотите настроить приложение в режиме, инициируемом поставщиком услуг, установите флажок **Показать дополнительные настройки URL-адресов** и сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="3bd5d-163">If you want to set up the application in SP-initiated mode, select the **Show advanced URL settings** check box, and then do the following:</span></span>

    * <span data-ttu-id="3bd5d-164">В поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://secure.helpscout.net/members/login/`.</span><span class="sxs-lookup"><span data-stu-id="3bd5d-164">In the **Sign on URL** box, enter a URL that has the following format: `https://secure.helpscout.net/members/login/`</span></span>

    ![Сведения о домене и URL-адресах единого входа приложения Help Scout](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_url1.png)
 
    > [!NOTE] 
    > <span data-ttu-id="3bd5d-166">Значения этих URL-адресов приведены только в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="3bd5d-166">The values in these URLs are for demonstration only.</span></span> <span data-ttu-id="3bd5d-167">Измените их на фактические значения идентификатора и URL-адреса ответа.</span><span class="sxs-lookup"><span data-stu-id="3bd5d-167">Update the values with the actual identifier URL and reply URL.</span></span> <span data-ttu-id="3bd5d-168">Чтобы получить их, обратитесь в [службу поддержки клиентов Help Scout](mailto:help@helpscout.com).</span><span class="sxs-lookup"><span data-stu-id="3bd5d-168">To get these values, contact [Help Scout support team](mailto:help@helpscout.com).</span></span> 

5. <span data-ttu-id="3bd5d-169">В разделе **Сертификат подписи SAML** щелкните **XML метаданных** и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="3bd5d-169">Under **SAML Signing Certificate**, select **Metadata XML**, and then save the metadata file on your computer.</span></span>

    ![Ссылка для скачивания сертификата](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_certificate.png) 

6. <span data-ttu-id="3bd5d-171">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="3bd5d-171">Select **Save**.</span></span>

    ![Кнопка "Сохранить" в окне настройки единого входа](./media/active-directory-saas-helpscout-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="3bd5d-173">Чтобы настроить единый вход на стороне Help Scout, отправьте скачанный XML-файл метаданных в [службу поддержки Help Scout](mailto:help@helpscout.com).</span><span class="sxs-lookup"><span data-stu-id="3bd5d-173">To set up single sign-on on the Help Scout side, send the downloaded metadata XML file to the [Help Scout support team](mailto:help@helpscout.com).</span></span> <span data-ttu-id="3bd5d-174">Специалисты службы поддержки Help Scout используют этот параметр для правильной настройки подключения единого входа SAML с обеих сторон.</span><span class="sxs-lookup"><span data-stu-id="3bd5d-174">The Help Scout support team applies this setting so that the SAML single sign-on connection is set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="3bd5d-175">Краткую версию этих инструкций можно также прочесть на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="3bd5d-175">You can read a concise version of these instructions in the [Azure portal](https://portal.azure.com), while you are setting up your app!</span></span> <span data-ttu-id="3bd5d-176">После добавления этого приложения из раздела **Active Directory** > **Корпоративные приложения** выберите вкладку **Единый вход**. Откройте встроенную документацию в разделе **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="3bd5d-176">After you add the app by selecting **Active Directory** > **Enterprise Applications**, select the **Single Sign-On** tab. You can access the embedded documentation in the **Configuration** section, at the bottom of the page.</span></span> <span data-ttu-id="3bd5d-177">Чтобы узнать больше, ознакомьтесь со [встроенной документацией по Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="3bd5d-177">For more information, see [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="3bd5d-178">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="3bd5d-178">Create an Azure AD test user</span></span>

<span data-ttu-id="3bd5d-179">В этом разделе описано, как на портале Azure создать тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3bd5d-179">In this section, in the Azure portal, you create a test user named Britta Simon.</span></span>

![Создание тестового пользователя Azure AD][100]

<span data-ttu-id="3bd5d-181">Чтобы создать тестового пользователя в Azure AD, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="3bd5d-181">To create a test user in Azure AD:</span></span>

1. <span data-ttu-id="3bd5d-182">На портале Azure в меню слева щелкните **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3bd5d-182">In the Azure portal, in the left menu, select **Azure Active Directory**.</span></span>

    ![Кнопка "Azure Active Directory"](./media/active-directory-saas-helpscout-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="3bd5d-184">Чтобы открыть список пользователей, выберите **Пользователи и группы**, а затем — **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="3bd5d-184">To display the list of users, select **Users and groups**, and then select **All users**.</span></span>

    ![Выбор элементов "Пользователи и группы" и "Все пользователи"](./media/active-directory-saas-helpscout-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="3bd5d-186">Чтобы открыть диалоговое окно **Пользователь**, в верхней части страницы **Все пользователи** щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="3bd5d-186">To open the **User** dialog box, at the top of the **All Users** page, select **Add**.</span></span>

    ![Кнопка "Добавить"](./media/active-directory-saas-helpscout-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="3bd5d-188">В диалоговом окне **Пользователь** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="3bd5d-188">In the **User** dialog box, complete the following steps:</span></span>

    1. <span data-ttu-id="3bd5d-189">В поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3bd5d-189">In the **Name** box, enter **BrittaSimon**.</span></span>

    2. <span data-ttu-id="3bd5d-190">В поле **Имя пользователя** введите адрес электронной почты пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3bd5d-190">In the **User name** box, enter the email address of user Britta Simon.</span></span>

    3. <span data-ttu-id="3bd5d-191">Установите флажок **Показать пароль** и запишите значение, которое отображается в поле **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="3bd5d-191">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    4. <span data-ttu-id="3bd5d-192">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="3bd5d-192">Select **Create**.</span></span>

        ![Диалоговое окно "Пользователь"](./media/active-directory-saas-helpscout-tutorial/create_aaduser_04.png)

 
### <a name="create-a-help-scout-test-user"></a><span data-ttu-id="3bd5d-194">Создание тестового пользователя Help Scout</span><span class="sxs-lookup"><span data-stu-id="3bd5d-194">Create a Help Scout test user</span></span>

<span data-ttu-id="3bd5d-195">Цель этого раздела — создать пользователя с именем Britta Simon в Help Scout.</span><span class="sxs-lookup"><span data-stu-id="3bd5d-195">The object of this section is to create a user named Britta Simon in Help Scout.</span></span> <span data-ttu-id="3bd5d-196">Help Scout поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="3bd5d-196">Help Scout supports just-in-time (JIT) provisioning, which is turned on by default.</span></span>

<span data-ttu-id="3bd5d-197">В этом разделе не нужно ничего делать.</span><span class="sxs-lookup"><span data-stu-id="3bd5d-197">In this section, there's no action or task to complete.</span></span> <span data-ttu-id="3bd5d-198">Если пользователь еще не существует в Help Scout, он создается при попытке доступа к приложению Help Scout.</span><span class="sxs-lookup"><span data-stu-id="3bd5d-198">If a user doesn't already exist in Help Scout, a new one is created when you attempt to access Help Scout.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="3bd5d-199">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="3bd5d-199">Assign the Azure AD test user</span></span>

<span data-ttu-id="3bd5d-200">Здесь описано, как разрешить пользователю Britta Simon использовать единый вход Azure AD, предоставив доступ учетным записям пользователя к Help Scout.</span><span class="sxs-lookup"><span data-stu-id="3bd5d-200">In this section, you allow the user Britta Simon to use Azure AD single sign-on by granting the user account access to Help Scout.</span></span>

![Назначение роли пользователя][200] 

<span data-ttu-id="3bd5d-202">Чтобы назначить пользователя Britta Simon в Help Scout, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="3bd5d-202">To assign Britta Simon to Help Scout:</span></span>

1. <span data-ttu-id="3bd5d-203">На портале Azure откройте представление приложений и перейдите к представлению каталога.</span><span class="sxs-lookup"><span data-stu-id="3bd5d-203">In the Azure portal, open the applications view, and then go to the directory view.</span></span> <span data-ttu-id="3bd5d-204">Перейдите в колонку **Корпоративные приложения** и выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="3bd5d-204">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="3bd5d-206">В списке приложений выберите **Help Scout**.</span><span class="sxs-lookup"><span data-stu-id="3bd5d-206">In the applications list, select **Help Scout**.</span></span>

    ![Ссылка на Help Scout в списке "Приложения"](./media/active-directory-saas-helpscout-tutorial/tutorial_helpscout_app.png)  

3. <span data-ttu-id="3bd5d-208">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="3bd5d-208">In the left menu, select **Users and groups**.</span></span>

    ![Ссылка "Пользователи и группы"][202]

4. <span data-ttu-id="3bd5d-210">Выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="3bd5d-210">Select **Add**.</span></span> <span data-ttu-id="3bd5d-211">Затем на странице **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="3bd5d-211">Then, on the **Add Assignment** page, select **Users and groups**.</span></span>

    ![Область "Добавление назначения"][203]

5. <span data-ttu-id="3bd5d-213">На странице **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="3bd5d-213">On the **Users and groups** page, in the list of users, select **Britta Simon**.</span></span>

6. <span data-ttu-id="3bd5d-214">На странице **Пользователи и группы** щелкните **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="3bd5d-214">On the **Users and groups** page, select **Select**.</span></span>

7. <span data-ttu-id="3bd5d-215">На странице **Добавление назначения** выберите **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="3bd5d-215">On the **Add Assignment** page, select **Assign**.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="3bd5d-216">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="3bd5d-216">Test single sign-on</span></span>

<span data-ttu-id="3bd5d-217">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="3bd5d-217">In this section, you test your Azure AD single sign-on configuration by using the access panel.</span></span>

<span data-ttu-id="3bd5d-218">Выбрав плитку Help Scout на панели доступа, вы должны автоматически войти в приложение Help Scout.</span><span class="sxs-lookup"><span data-stu-id="3bd5d-218">When you select the Help Scout tile in the access panel, you should be automatically signed in to your Help Scout application.</span></span>

<span data-ttu-id="3bd5d-219">Дополнительные сведения о панели доступа см. в статье [Что такое панель доступа?](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3bd5d-219">For more information about the access panel, see [Introduction to the access panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="3bd5d-220">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="3bd5d-220">Additional resources</span></span>

* [<span data-ttu-id="3bd5d-221">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3bd5d-221">List of tutorials on how to integrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3bd5d-222">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3bd5d-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-helpscout-tutorial/tutorial_general_203.png

