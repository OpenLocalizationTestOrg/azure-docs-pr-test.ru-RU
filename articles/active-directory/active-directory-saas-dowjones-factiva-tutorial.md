---
title: "Руководство по интеграции Azure Active Directory с Dow Jones Factiva | Документация Майкрософт"
description: "Сведения о настройке единого входа между Azure Active Directory и Dow Jones Factiva."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b36e97e8-37a6-4096-a894-530427ee1331
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/11/2017
ms.author: jeedes
ms.openlocfilehash: dab48c24ff25fd68df1ee540bb8f0929e7e81bcb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-dow-jones-factiva"></a><span data-ttu-id="bfb90-103">Руководство по интеграции Azure Active Directory с Dow Jones Factiva</span><span class="sxs-lookup"><span data-stu-id="bfb90-103">Tutorial: Azure Active Directory integration with Dow Jones Factiva</span></span>

<span data-ttu-id="bfb90-104">В этом руководстве описано, как интегрировать Dow Jones Factiva с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bfb90-104">In this tutorial, you learn how to integrate Dow Jones Factiva with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bfb90-105">Интеграция Azure AD с приложением Dow Jones Factiva обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="bfb90-105">Integrating Dow Jones Factiva with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="bfb90-106">С помощью Azure AD вы можете контролировать доступ к Dow Jones Factiva.</span><span class="sxs-lookup"><span data-stu-id="bfb90-106">You can control in Azure AD who has access to Dow Jones Factiva</span></span>
- <span data-ttu-id="bfb90-107">Вы можете включить автоматический вход пользователей в Dow Jones Factiva (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bfb90-107">You can enable your users to automatically get signed-on to Dow Jones Factiva (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bfb90-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="bfb90-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="bfb90-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bfb90-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bfb90-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="bfb90-110">Prerequisites</span></span>

<span data-ttu-id="bfb90-111">Чтобы настроить интеграцию Azure AD с Dow Jones Factiva, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="bfb90-111">To configure Azure AD integration with Dow Jones Factiva, you need the following items:</span></span>

- <span data-ttu-id="bfb90-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="bfb90-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bfb90-113">подписка на Dow Jones Factiva с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="bfb90-113">A Dow Jones Factiva single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bfb90-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="bfb90-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bfb90-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="bfb90-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bfb90-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="bfb90-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bfb90-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bfb90-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bfb90-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="bfb90-118">Scenario description</span></span>
<span data-ttu-id="bfb90-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="bfb90-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bfb90-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="bfb90-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bfb90-121">Добавление Dow Jones Factiva из коллекции.</span><span class="sxs-lookup"><span data-stu-id="bfb90-121">Adding Dow Jones Factiva from the gallery</span></span>
2. <span data-ttu-id="bfb90-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="bfb90-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-dow-jones-factiva-from-the-gallery"></a><span data-ttu-id="bfb90-123">Добавление Dow Jones Factiva из коллекции</span><span class="sxs-lookup"><span data-stu-id="bfb90-123">Adding Dow Jones Factiva from the gallery</span></span>
<span data-ttu-id="bfb90-124">Чтобы настроить интеграцию Dow Jones Factiva с Azure AD, необходимо добавить Dow Jones Factiva из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="bfb90-124">To configure the integration of Dow Jones Factiva into Azure AD, you need to add Dow Jones Factiva from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="bfb90-125">**Чтобы добавить Dow Jones Factiva из коллекции, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="bfb90-125">**To add Dow Jones Factiva from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="bfb90-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="bfb90-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="bfb90-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="bfb90-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="bfb90-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="bfb90-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="bfb90-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="bfb90-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="bfb90-133">В поле поиска введите **Dow Jones Factiva**.</span><span class="sxs-lookup"><span data-stu-id="bfb90-133">In the search box, type **Dow Jones Factiva**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_dowjonesfactiva_search.png)

5. <span data-ttu-id="bfb90-135">На панели результатов выберите **Dow Jones Factiva** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="bfb90-135">In the results panel, select **Dow Jones Factiva**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_dowjonesfactiva_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bfb90-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="bfb90-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bfb90-138">В этом разделе описана настройка и проверка единого входа Azure AD в Dow Jones Factiva с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bfb90-138">In this section, you configure and test Azure AD single sign-on with Dow Jones Factiva based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="bfb90-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Dow Jones Factiva соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bfb90-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Dow Jones Factiva is to a user in Azure AD.</span></span> <span data-ttu-id="bfb90-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Dow Jones Factiva.</span><span class="sxs-lookup"><span data-stu-id="bfb90-140">In other words, a link relationship between an Azure AD user and the related user in Dow Jones Factiva needs to be established.</span></span>

<span data-ttu-id="bfb90-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Dow Jones Factiva.</span><span class="sxs-lookup"><span data-stu-id="bfb90-141">In Dow Jones Factiva, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="bfb90-142">Чтобы настроить и проверить единый вход Azure AD в Dow Jones Factiva, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="bfb90-142">To configure and test Azure AD single sign-on with Dow Jones Factiva, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="bfb90-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="bfb90-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="bfb90-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bfb90-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bfb90-145">**[Создание тестового пользователя Dow Jones Factiva](#creating-a-dow-jones-factiva-test-user)** требуется для создания в Dow Jones Factiva пользователя Britta Simon, связанного с представлением этого же пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bfb90-145">**[Creating a Dow Jones Factiva test user](#creating-a-dow-jones-factiva-test-user)** - to have a counterpart of Britta Simon in Dow Jones Factiva that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="bfb90-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bfb90-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bfb90-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="bfb90-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bfb90-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="bfb90-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bfb90-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Dow Jones Factiva.</span><span class="sxs-lookup"><span data-stu-id="bfb90-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Dow Jones Factiva application.</span></span>

<span data-ttu-id="bfb90-150">**Чтобы настроить единый вход Azure AD в Dow Jones Factiva, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="bfb90-150">**To configure Azure AD single sign-on with Dow Jones Factiva, perform the following steps:**</span></span>

1. <span data-ttu-id="bfb90-151">На портале Azure на странице интеграции с приложением **Dow Jones Factiva** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="bfb90-151">In the Azure portal, on the **Dow Jones Factiva** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="bfb90-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="bfb90-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_dowjonesfactiva_samlbase.png)

3. <span data-ttu-id="bfb90-155">В разделе **Домены и URL-адреса приложения Dow Jones Factiva** не нужно выполнять никаких действий, так как приложение предварительно интегрировано с Azure.</span><span class="sxs-lookup"><span data-stu-id="bfb90-155">On the **Dow Jones Factiva Domain and URLs** section, the user does not have to perform any steps as the app is already pre-integrated with Azure.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_dowjonesfactiva_url.png)

4. <span data-ttu-id="bfb90-157">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="bfb90-157">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_dowjonesfactiva_certificate.png) 

5. <span data-ttu-id="bfb90-159">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="bfb90-159">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="bfb90-161">Чтобы настроить единый вход на стороне **Dow Jones Factiva**, отправьте скачанный **XML-файл метаданных** в [службу поддержки Dow Jones Factiva](https://www.dowjones.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="bfb90-161">To configure single sign-on on **Dow Jones Factiva** side, you need to send the downloaded **Metadata XML** to [Dow Jones Factiva support team](https://www.dowjones.com/contact/).</span></span> <span data-ttu-id="bfb90-162">Специалисты службы поддержки настроят подключение единого входа SAML на обеих сторонах подключения.</span><span class="sxs-lookup"><span data-stu-id="bfb90-162">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="bfb90-163">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="bfb90-163">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="bfb90-164">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="bfb90-164">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="bfb90-165">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="bfb90-165">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bfb90-166">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="bfb90-166">Creating an Azure AD test user</span></span>
<span data-ttu-id="bfb90-167">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bfb90-167">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="bfb90-169">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="bfb90-169">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="bfb90-170">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="bfb90-170">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-dowjones-factiva-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bfb90-172">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="bfb90-172">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-dowjones-factiva-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bfb90-174">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="bfb90-174">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-dowjones-factiva-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bfb90-176">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="bfb90-176">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-dowjones-factiva-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bfb90-178">а.</span><span class="sxs-lookup"><span data-stu-id="bfb90-178">a.</span></span> <span data-ttu-id="bfb90-179">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bfb90-179">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bfb90-180">b.</span><span class="sxs-lookup"><span data-stu-id="bfb90-180">b.</span></span> <span data-ttu-id="bfb90-181">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="bfb90-181">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bfb90-182">c.</span><span class="sxs-lookup"><span data-stu-id="bfb90-182">c.</span></span> <span data-ttu-id="bfb90-183">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="bfb90-183">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="bfb90-184">d.</span><span class="sxs-lookup"><span data-stu-id="bfb90-184">d.</span></span> <span data-ttu-id="bfb90-185">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="bfb90-185">Click **Create**.</span></span>
 
### <a name="creating-a-dow-jones-factiva-test-user"></a><span data-ttu-id="bfb90-186">Создание тестового пользователя Dow Jones Factiva</span><span class="sxs-lookup"><span data-stu-id="bfb90-186">Creating a Dow Jones Factiva test user</span></span>

<span data-ttu-id="bfb90-187">В этом разделе описано, как создать пользователя Britta Simon в приложении Dow Jones Factiva.</span><span class="sxs-lookup"><span data-stu-id="bfb90-187">In this section, you create a user called Britta Simon in Dow Jones Factiva.</span></span> <span data-ttu-id="bfb90-188">Обратитесь в [службу поддержки Dow Jones Factiva](https://www.dowjones.com/contact/), чтобы добавить пользователей на платформу Dow Jones Factiva.</span><span class="sxs-lookup"><span data-stu-id="bfb90-188">Please work with Dow [Jones Factiva support team](https://www.dowjones.com/contact/) to add the users in the Dow Jones Factiva platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="bfb90-189">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="bfb90-189">Assigning the Azure AD test user</span></span>

<span data-ttu-id="bfb90-190">В этом разделе описано, как позволить пользователю Britta Simon использовать единый вход Azure, предоставив ему доступ к Dow Jones Factiva.</span><span class="sxs-lookup"><span data-stu-id="bfb90-190">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Dow Jones Factiva.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="bfb90-192">**Чтобы назначить пользователя Britta Simon в Dow Jones Factiva, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="bfb90-192">**To assign Britta Simon to Dow Jones Factiva, perform the following steps:**</span></span>

1. <span data-ttu-id="bfb90-193">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="bfb90-193">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="bfb90-195">В списке приложений выберите **Dow Jones Factiva**.</span><span class="sxs-lookup"><span data-stu-id="bfb90-195">In the applications list, select **Dow Jones Factiva**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_dowjonesfactiva_app.png) 

3. <span data-ttu-id="bfb90-197">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="bfb90-197">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="bfb90-199">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="bfb90-199">Click **Add** button.</span></span> <span data-ttu-id="bfb90-200">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="bfb90-200">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="bfb90-202">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="bfb90-202">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="bfb90-203">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="bfb90-203">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bfb90-204">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="bfb90-204">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="bfb90-205">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="bfb90-205">Testing single sign-on</span></span>

<span data-ttu-id="bfb90-206">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="bfb90-206">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="bfb90-207">Щелкнув плитку Dow Jones Factiva на панели доступа, вы автоматически войдете в приложение Dow Jones Factiva.</span><span class="sxs-lookup"><span data-stu-id="bfb90-207">When you click the Dow Jones Factiva tile in the Access Panel, you should get automatically signed-on to your Dow Jones Factiva application.</span></span>
<span data-ttu-id="bfb90-208">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="bfb90-208">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="bfb90-209">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="bfb90-209">Additional resources</span></span>

* [<span data-ttu-id="bfb90-210">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bfb90-210">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bfb90-211">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="bfb90-211">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-dowjones-factiva-tutorial/tutorial_general_203.png

