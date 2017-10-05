---
title: "Руководство по интеграции Azure Active Directory с Reward Gateway | Документация Майкрософт"
description: "Узнайте, как настроить единый вход для Azure Active Directory и Reward Gateway."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 34336386-998a-4d47-ab55-721d97708e5e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: b1a468caa22159ad603dbec1ef530e7e0e24f96d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-reward-gateway"></a><span data-ttu-id="960fd-103">Учебник. Интеграция Azure Active Directory с Reward Gateway</span><span class="sxs-lookup"><span data-stu-id="960fd-103">Tutorial: Azure Active Directory integration with Reward Gateway</span></span>

<span data-ttu-id="960fd-104">В этом учебнике описано, как интегрировать Reward Gateway с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="960fd-104">In this tutorial, you learn how to integrate Reward Gateway with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="960fd-105">Интеграция Reward Gateway с Azure AD обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="960fd-105">Integrating Reward Gateway with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="960fd-106">С помощью Azure AD вы можете контролировать доступ к Reward Gateway.</span><span class="sxs-lookup"><span data-stu-id="960fd-106">You can control in Azure AD who has access to Reward Gateway</span></span>
- <span data-ttu-id="960fd-107">Вы можете включить автоматический вход пользователей в Reward Gateway (единый вход) с помощью их учетных записей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="960fd-107">You can enable your users to automatically get signed-on to Reward Gateway (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="960fd-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="960fd-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="960fd-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="960fd-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="960fd-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="960fd-110">Prerequisites</span></span>

<span data-ttu-id="960fd-111">Чтобы настроить интеграцию Azure AD с Reward Gateway, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="960fd-111">To configure Azure AD integration with Reward Gateway, you need the following items:</span></span>

- <span data-ttu-id="960fd-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="960fd-112">An Azure AD subscription</span></span>
- <span data-ttu-id="960fd-113">подписка Reward Gateway с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="960fd-113">A Reward Gateway single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="960fd-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="960fd-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="960fd-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="960fd-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="960fd-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="960fd-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="960fd-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="960fd-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="960fd-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="960fd-118">Scenario description</span></span>
<span data-ttu-id="960fd-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="960fd-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="960fd-120">Сценарий, описанный в этом руководстве, состоит из двух стандартных блоков.</span><span class="sxs-lookup"><span data-stu-id="960fd-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="960fd-121">Добавление Reward Gateway из коллекции.</span><span class="sxs-lookup"><span data-stu-id="960fd-121">Adding Reward Gateway from the gallery</span></span>
2. <span data-ttu-id="960fd-122">Настройка и проверка единого входа в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="960fd-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-reward-gateway-from-the-gallery"></a><span data-ttu-id="960fd-123">Добавление Reward Gateway из коллекции</span><span class="sxs-lookup"><span data-stu-id="960fd-123">Adding Reward Gateway from the gallery</span></span>
<span data-ttu-id="960fd-124">Чтобы настроить интеграцию Reward Gateway с Azure AD, необходимо добавить Reward Gateway из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="960fd-124">To configure the integration of Reward Gateway into Azure AD, you need to add Reward Gateway from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="960fd-125">**Чтобы добавить Reward Gateway из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="960fd-125">**To add Reward Gateway from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="960fd-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="960fd-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="960fd-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="960fd-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="960fd-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="960fd-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="960fd-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="960fd-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="960fd-133">В поле поиска введите **Reward Gateway**.</span><span class="sxs-lookup"><span data-stu-id="960fd-133">In the search box, type **Reward Gateway**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-reward-gateway-tutorial/tutorial_rewardgateway_search.png)

5. <span data-ttu-id="960fd-135">На панели результатов выберите **Reward Gateway** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="960fd-135">In the results panel, select **Reward Gateway**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-reward-gateway-tutorial/tutorial_rewardgateway_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="960fd-137">Настройка и проверка единого входа в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="960fd-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="960fd-138">В этом разделе описана настройка и проверка единого входа Azure AD в Reward Gateway с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="960fd-138">In this section, you configure and test Azure AD single sign-on with Reward Gateway based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="960fd-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Reward Gateway соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="960fd-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Reward Gateway is to a user in Azure AD.</span></span> <span data-ttu-id="960fd-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Reward Gateway.</span><span class="sxs-lookup"><span data-stu-id="960fd-140">In other words, a link relationship between an Azure AD user and the related user in Reward Gateway needs to be established.</span></span>

<span data-ttu-id="960fd-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Reward Gateway.</span><span class="sxs-lookup"><span data-stu-id="960fd-141">In Reward Gateway, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="960fd-142">Чтобы настроить и проверить единый вход Azure AD в Reward Gateway, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="960fd-142">To configure and test Azure AD single sign-on with Reward Gateway, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="960fd-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="960fd-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="960fd-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="960fd-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="960fd-145">**[Создание тестового пользователя Reward Gateway](#creating-a-reward-gateway-test-user)** требуется для создания в Reward Gateway пользователя Britta Simon, связанного с представлением этого же пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="960fd-145">**[Creating a Reward Gateway test user](#creating-a-reward-gateway-test-user)** - to have a counterpart of Britta Simon in Reward Gateway that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="960fd-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="960fd-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="960fd-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="960fd-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="960fd-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="960fd-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="960fd-149">В данном разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Reward Gateway.</span><span class="sxs-lookup"><span data-stu-id="960fd-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Reward Gateway application.</span></span>

<span data-ttu-id="960fd-150">**Чтобы настроить единый вход Azure AD в Reward Gateway, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="960fd-150">**To configure Azure AD single sign-on with Reward Gateway, perform the following steps:**</span></span>

1. <span data-ttu-id="960fd-151">На портале Azure на странице интеграции с приложением **Reward Gateway** выберите **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="960fd-151">In the Azure portal, on the **Reward Gateway** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="960fd-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="960fd-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-reward-gateway-tutorial/tutorial_rewardgateway_samlbase.png)

3. <span data-ttu-id="960fd-155">В разделе **Домены и URL-адреса приложения Reward Gateway** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="960fd-155">On the **Reward Gateway Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-reward-gateway-tutorial/tutorial_rewardgateway_url.png)

    <span data-ttu-id="960fd-157">а.</span><span class="sxs-lookup"><span data-stu-id="960fd-157">a.</span></span> <span data-ttu-id="960fd-158">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="960fd-158">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.rewardgateway.com` |
    | `https://<companyname>.rewardgateway.co.uk/` |
    | `https://<companyname>.rewardgateway.co.nz/` |
    | `https://<companyname>.rewardgateway.com.au/` |

    <span data-ttu-id="960fd-159">b.</span><span class="sxs-lookup"><span data-stu-id="960fd-159">b.</span></span> <span data-ttu-id="960fd-160">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="960fd-160">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    |  `https://<companyname>.rewardgateway.com/Authentication/EndLogin?idp=<Unique Id>` |
    | `https://<companyname>.rewardgateway.co.uk/Authentication/EndLogin?idp=<Unique Id>` |
    | `https://<companyname>.rewardgateway.co.nz/Authentication/EndLogin?idp=<Unique Id>` |
    | `https://<companyname>.rewardgateway.com.au/Authentication/EndLogin?idp=<Unique Id>` |

    > [!NOTE] 
    > <span data-ttu-id="960fd-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="960fd-161">These values are not real.</span></span> <span data-ttu-id="960fd-162">Измените их на фактические значения идентификатора и URL-адреса ответа.</span><span class="sxs-lookup"><span data-stu-id="960fd-162">Update these values with the actual Identifier and Reply URL.</span></span> <span data-ttu-id="960fd-163">Чтобы получить эти значения, обратитесь в [службу поддержки Reward Gateway](mailto:clientsupport@rewardgateway.com).</span><span class="sxs-lookup"><span data-stu-id="960fd-163">Contact [Reward Gateway support team](mailto:clientsupport@rewardgateway.com) to get these values.</span></span>
 
4. <span data-ttu-id="960fd-164">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="960fd-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-reward-gateway-tutorial/tutorial_rewardgateway_certificate.png) 

5. <span data-ttu-id="960fd-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="960fd-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="960fd-168">Чтобы настроить единый вход на стороне **Reward Gateway**, отправьте скачанный **XML-файл метаданных** в [службу поддержки Reward Gateway](mailto:clientsupport@rewardgateway.com).</span><span class="sxs-lookup"><span data-stu-id="960fd-168">To configure single sign-on on **Reward Gateway** side, you need to send the downloaded **Metadata XML** to [Reward Gateway support team](mailto:clientsupport@rewardgateway.com).</span></span> <span data-ttu-id="960fd-169">Специалисты службы поддержки настроят подключение единого входа SAML на обеих сторонах.</span><span class="sxs-lookup"><span data-stu-id="960fd-169">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="960fd-170">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="960fd-170">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="960fd-171">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="960fd-171">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="960fd-172">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="960fd-172">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="960fd-173">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="960fd-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="960fd-174">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="960fd-174">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="960fd-176">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="960fd-176">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="960fd-177">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="960fd-177">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-reward-gateway-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="960fd-179">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="960fd-179">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-reward-gateway-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="960fd-181">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="960fd-181">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-reward-gateway-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="960fd-183">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="960fd-183">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-reward-gateway-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="960fd-185">а.</span><span class="sxs-lookup"><span data-stu-id="960fd-185">a.</span></span> <span data-ttu-id="960fd-186">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="960fd-186">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="960fd-187">b.</span><span class="sxs-lookup"><span data-stu-id="960fd-187">b.</span></span> <span data-ttu-id="960fd-188">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="960fd-188">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="960fd-189">c.</span><span class="sxs-lookup"><span data-stu-id="960fd-189">c.</span></span> <span data-ttu-id="960fd-190">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="960fd-190">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="960fd-191">d.</span><span class="sxs-lookup"><span data-stu-id="960fd-191">d.</span></span> <span data-ttu-id="960fd-192">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="960fd-192">Click **Create**.</span></span>
 
### <a name="creating-a-reward-gateway-test-user"></a><span data-ttu-id="960fd-193">Создание тестового пользователя Reward Gateway</span><span class="sxs-lookup"><span data-stu-id="960fd-193">Creating a Reward Gateway test user</span></span>

<span data-ttu-id="960fd-194">В этом разделе описано, как создать пользователя Britta Simon в приложении Reward Gateway.</span><span class="sxs-lookup"><span data-stu-id="960fd-194">In this section, you create a user called Britta Simon in Reward Gateway.</span></span> <span data-ttu-id="960fd-195">Обратитесь в [службу поддержки](mailto:clientsupport@rewardgateway.com) Reward Gateway, чтобы добавить пользователей на платформу Reward Gateway.</span><span class="sxs-lookup"><span data-stu-id="960fd-195">Work with Reward Gateway [support team](mailto:clientsupport@rewardgateway.com) to add the users in the Reward Gateway platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="960fd-196">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="960fd-196">Assigning the Azure AD test user</span></span>

<span data-ttu-id="960fd-197">В этом разделе описано, как предоставить пользователю Britta Simon доступ к Reward Gateway, чтобы он мог использовать единый вход Azure.</span><span class="sxs-lookup"><span data-stu-id="960fd-197">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Reward Gateway.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="960fd-199">**Чтобы назначить пользователя Britta Simon в Reward Gateway, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="960fd-199">**To assign Britta Simon to Reward Gateway, perform the following steps:**</span></span>

1. <span data-ttu-id="960fd-200">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="960fd-200">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="960fd-202">В списке приложений выберите **Reward Gateway**.</span><span class="sxs-lookup"><span data-stu-id="960fd-202">In the applications list, select **Reward Gateway**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-reward-gateway-tutorial/tutorial_rewardgateway_app.png) 

3. <span data-ttu-id="960fd-204">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="960fd-204">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="960fd-206">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="960fd-206">Click **Add** button.</span></span> <span data-ttu-id="960fd-207">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="960fd-207">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="960fd-209">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="960fd-209">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="960fd-210">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="960fd-210">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="960fd-211">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="960fd-211">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="960fd-212">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="960fd-212">Testing single sign-on</span></span>

<span data-ttu-id="960fd-213">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="960fd-213">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="960fd-214">Щелкнув элемент Reward Gateway на панели доступа, вы автоматически войдете в приложение Reward Gateway.</span><span class="sxs-lookup"><span data-stu-id="960fd-214">When you click the Reward Gateway tile in the Access Panel, you should get automatically signed-on to your Reward Gateway application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="960fd-215">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="960fd-215">Additional resources</span></span>

* [<span data-ttu-id="960fd-216">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="960fd-216">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="960fd-217">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="960fd-217">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-reward-gateway-tutorial/tutorial_general_203.png

