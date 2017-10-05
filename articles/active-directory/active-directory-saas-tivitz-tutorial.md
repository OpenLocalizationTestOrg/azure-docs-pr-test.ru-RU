---
title: "Руководство по интеграции Azure Active Directory с TiViTz | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и TiViTz."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b97ed88f-7888-4185-be22-41d1f62cbbf1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jeedes
ms.openlocfilehash: b1b27918bb5fcff1d19f4711ea70fe46a5697933
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-tivitz"></a><span data-ttu-id="3affe-103">Руководство по интеграции Azure Active Directory с TiViTz</span><span class="sxs-lookup"><span data-stu-id="3affe-103">Tutorial: Azure Active Directory integration with TiViTz</span></span>

<span data-ttu-id="3affe-104">В этом руководстве описано, как интегрировать приложение TiViTz с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3affe-104">In this tutorial, you learn how to integrate TiViTz with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3affe-105">Интеграция Azure AD с приложением TiViTz обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="3affe-105">Integrating TiViTz with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3affe-106">С помощью Azure AD вы можете контролировать доступ к TiViTz.</span><span class="sxs-lookup"><span data-stu-id="3affe-106">You can control in Azure AD who has access to TiViTz</span></span>
- <span data-ttu-id="3affe-107">Вы можете включить автоматический вход пользователей в TiViTz (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3affe-107">You can enable your users to automatically get signed-on to TiViTz (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3affe-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="3affe-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="3affe-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3affe-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3affe-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="3affe-110">Prerequisites</span></span>

<span data-ttu-id="3affe-111">Чтобы настроить интеграцию Azure AD с TiViTz, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="3affe-111">To configure Azure AD integration with TiViTz, you need the following items:</span></span>

- <span data-ttu-id="3affe-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="3affe-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3affe-113">подписка TiViTz с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="3affe-113">A TiViTz single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3affe-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="3affe-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3affe-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="3affe-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3affe-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="3affe-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3affe-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3affe-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3affe-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="3affe-118">Scenario description</span></span>
<span data-ttu-id="3affe-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="3affe-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3affe-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="3affe-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3affe-121">Добавление TiViTz из коллекции</span><span class="sxs-lookup"><span data-stu-id="3affe-121">Adding TiViTz from the gallery</span></span>
2. <span data-ttu-id="3affe-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="3affe-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-tivitz-from-the-gallery"></a><span data-ttu-id="3affe-123">Добавление TiViTz из коллекции</span><span class="sxs-lookup"><span data-stu-id="3affe-123">Adding TiViTz from the gallery</span></span>
<span data-ttu-id="3affe-124">Чтобы настроить интеграцию TiViTz с Azure AD, необходимо добавить это приложение из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="3affe-124">To configure the integration of TiViTz into Azure AD, you need to add TiViTz from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3affe-125">**Чтобы добавить TiViTz из коллекции, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="3affe-125">**To add TiViTz from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3affe-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3affe-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3affe-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="3affe-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3affe-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="3affe-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="3affe-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="3affe-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="3affe-133">В поле поиска введите **TiViTz**.</span><span class="sxs-lookup"><span data-stu-id="3affe-133">In the search box, type **TiViTz**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-tivitz-tutorial/tutorial_tivitz_search.png)

5. <span data-ttu-id="3affe-135">На панели результатов выберите **TiViTz** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="3affe-135">In the results panel, select **TiViTz**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-tivitz-tutorial/tutorial_tivitz_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3affe-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="3affe-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3affe-138">В этом разделе описана настройка и проверка единого входа Azure AD в TiViTz с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3affe-138">In this section, you configure and test Azure AD single sign-on with TiViTz based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3affe-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в TiViTz соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3affe-139">For single sign-on to work, Azure AD needs to know what the counterpart user in TiViTz is to a user in Azure AD.</span></span> <span data-ttu-id="3affe-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в TiViTz.</span><span class="sxs-lookup"><span data-stu-id="3affe-140">In other words, a link relationship between an Azure AD user and the related user in TiViTz needs to be established.</span></span>

<span data-ttu-id="3affe-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в TiViTz.</span><span class="sxs-lookup"><span data-stu-id="3affe-141">In TiViTz, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="3affe-142">Чтобы настроить и проверить единый вход Azure AD в TiViTz, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="3affe-142">To configure and test Azure AD single sign-on with TiViTz, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3affe-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="3affe-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3affe-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3affe-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3affe-145">**[Создание тестового пользователя TiViTz](#creating-a-tivitz-test-user)** требуется для того, чтобы в TiViTz существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3affe-145">**[Creating a TiViTz test user](#creating-a-tivitz-test-user)** - to have a counterpart of Britta Simon in TiViTz that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="3affe-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3affe-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3affe-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="3affe-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3affe-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="3affe-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3affe-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении TiViTz.</span><span class="sxs-lookup"><span data-stu-id="3affe-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your TiViTz application.</span></span>

<span data-ttu-id="3affe-150">**Чтобы настроить единый вход Azure AD в TiViTz, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="3affe-150">**To configure Azure AD single sign-on with TiViTz, perform the following steps:**</span></span>

1. <span data-ttu-id="3affe-151">На портале Azure на странице интеграции с приложением **TiViTz** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="3affe-151">In the Azure portal, on the **TiViTz** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="3affe-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="3affe-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-tivitz-tutorial/tutorial_tivitz_samlbase.png)

3. <span data-ttu-id="3affe-155">В разделе **Домены и URL-адреса приложения TiViTz** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="3affe-155">On the **TiViTz Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-tivitz-tutorial/tutorial_tivitz_url.png)

    <span data-ttu-id="3affe-157">а.</span><span class="sxs-lookup"><span data-stu-id="3affe-157">a.</span></span> <span data-ttu-id="3affe-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<companyname>.o365.tivitz.com/`</span><span class="sxs-lookup"><span data-stu-id="3affe-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.o365.tivitz.com/`</span></span>

    <span data-ttu-id="3affe-159">b.</span><span class="sxs-lookup"><span data-stu-id="3affe-159">b.</span></span> <span data-ttu-id="3affe-160">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<companyname>.o365.tivitz.com/`</span><span class="sxs-lookup"><span data-stu-id="3affe-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.o365.tivitz.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="3affe-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="3affe-161">These values are not real.</span></span> <span data-ttu-id="3affe-162">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="3affe-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="3affe-163">Чтобы получить эти значения, обратитесь к [группе поддержки клиентов TiViTz](mailto:info@tivitz.com).</span><span class="sxs-lookup"><span data-stu-id="3affe-163">Contact [TiViTz Client support team](mailto:info@tivitz.com) to get these values.</span></span> 

4. <span data-ttu-id="3affe-164">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="3affe-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-tivitz-tutorial/tutorial_tivitz_certificate.png) 

5. <span data-ttu-id="3affe-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="3affe-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-tivitz-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="3affe-168">Чтобы настроить единый вход на стороне **TiViTz**, отправьте [группе поддержки TiViTz](mailto:info@tivitz.com) скачанный **XML-файл метаданных**.</span><span class="sxs-lookup"><span data-stu-id="3affe-168">To configure single sign-on on **TiViTz** side, you need to send the downloaded **Metadata XML** to [TiViTz support team](mailto:info@tivitz.com).</span></span>

> [!TIP]
> <span data-ttu-id="3affe-169">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="3affe-169">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3affe-170">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="3affe-170">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3affe-171">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="3affe-171">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3affe-172">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="3affe-172">Creating an Azure AD test user</span></span>
<span data-ttu-id="3affe-173">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3affe-173">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="3affe-175">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="3affe-175">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3affe-176">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3affe-176">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-tivitz-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3affe-178">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="3affe-178">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-tivitz-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3affe-180">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="3affe-180">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-tivitz-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3affe-182">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="3affe-182">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-tivitz-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3affe-184">а.</span><span class="sxs-lookup"><span data-stu-id="3affe-184">a.</span></span> <span data-ttu-id="3affe-185">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3affe-185">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3affe-186">b.</span><span class="sxs-lookup"><span data-stu-id="3affe-186">b.</span></span> <span data-ttu-id="3affe-187">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="3affe-187">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3affe-188">c.</span><span class="sxs-lookup"><span data-stu-id="3affe-188">c.</span></span> <span data-ttu-id="3affe-189">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="3affe-189">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="3affe-190">d.</span><span class="sxs-lookup"><span data-stu-id="3affe-190">d.</span></span> <span data-ttu-id="3affe-191">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="3affe-191">Click **Create**.</span></span>
 
### <a name="creating-a-tivitz-test-user"></a><span data-ttu-id="3affe-192">Создание тестового пользователя TiViTz</span><span class="sxs-lookup"><span data-stu-id="3affe-192">Creating a TiViTz test user</span></span>

<span data-ttu-id="3affe-193">Цель этого раздела — создать пользователя с именем Britta Simon в приложении TiViTz.</span><span class="sxs-lookup"><span data-stu-id="3affe-193">The objective of this section is to create a user called Britta Simon in TiViTz.</span></span> <span data-ttu-id="3affe-194">Приложение TiViTz поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="3affe-194">TiViTz supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="3affe-195">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="3affe-195">There is no action item for you in this section.</span></span> <span data-ttu-id="3affe-196">Пользователь будет создан при попытке получить доступ к приложению TiViTz (если он еще не создан).</span><span class="sxs-lookup"><span data-stu-id="3affe-196">A new user is created during an attempt to access TiViTz if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="3affe-197">Чтобы создать пользователя вручную, обратитесь в [службу поддержки TiViTz](mailto:info@tivitz.com).</span><span class="sxs-lookup"><span data-stu-id="3affe-197">If you need to create an user manually, you need to contact [TiViTz support team](mailto:info@tivitz.com).</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="3affe-198">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="3affe-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="3affe-199">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к TiViTz.</span><span class="sxs-lookup"><span data-stu-id="3affe-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to TiViTz.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="3affe-201">**Чтобы назначить пользователя Britta Simon в TiViTz, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="3affe-201">**To assign Britta Simon to TiViTz, perform the following steps:**</span></span>

1. <span data-ttu-id="3affe-202">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="3affe-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="3affe-204">В списке приложений выберите **TiViTz**.</span><span class="sxs-lookup"><span data-stu-id="3affe-204">In the applications list, select **TiViTz**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-tivitz-tutorial/tutorial_tivitz_app.png) 

3. <span data-ttu-id="3affe-206">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="3affe-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="3affe-208">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="3affe-208">Click **Add** button.</span></span> <span data-ttu-id="3affe-209">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="3affe-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="3affe-211">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="3affe-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3affe-212">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="3affe-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3affe-213">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="3affe-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3affe-214">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="3affe-214">Testing single sign-on</span></span>

<span data-ttu-id="3affe-215">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="3affe-215">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="3affe-216">Щелкнув элемент TiViTz на панели доступа, вы автоматически войдете в приложение TiViTz.</span><span class="sxs-lookup"><span data-stu-id="3affe-216">When you click the TiViTz tile in the Access Panel, you should get automatically signed-on to your TiViTz application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3affe-217">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="3affe-217">Additional resources</span></span>

* [<span data-ttu-id="3affe-218">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3affe-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3affe-219">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3affe-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-tivitz-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-tivitz-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-tivitz-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-tivitz-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-tivitz-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-tivitz-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-tivitz-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-tivitz-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-tivitz-tutorial/tutorial_general_203.png

