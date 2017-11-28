---
title: "Руководство. Интеграция Azure Active Directory с Convercent | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в Convercent."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f9c9d290-0e13-490b-b559-0be772d6a690
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: jeedes
ms.openlocfilehash: 7af33cae7448a212734d327570b5082d0278fa0d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-convercent"></a><span data-ttu-id="c22ab-103">Руководство. Интеграция Azure Active Directory с Convercent</span><span class="sxs-lookup"><span data-stu-id="c22ab-103">Tutorial: Azure Active Directory integration with Convercent</span></span>

<span data-ttu-id="c22ab-104">В этом руководстве описано, как интегрировать Convercent с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c22ab-104">In this tutorial, you learn how to integrate Convercent with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="c22ab-105">Интеграция Convercent с Azure AD обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="c22ab-105">Integrating Convercent with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="c22ab-106">С помощью Azure AD вы можете контролировать доступ к Convercent.</span><span class="sxs-lookup"><span data-stu-id="c22ab-106">You can control in Azure AD who has access to Convercent</span></span>
- <span data-ttu-id="c22ab-107">Вы можете включить автоматический вход пользователей в Convercent (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c22ab-107">You can enable your users to automatically get signed-on to Convercent (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="c22ab-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="c22ab-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="c22ab-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="c22ab-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c22ab-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c22ab-110">Prerequisites</span></span>

<span data-ttu-id="c22ab-111">Чтобы настроить интеграцию Azure AD с Convercent, вам потребуется следующее:</span><span class="sxs-lookup"><span data-stu-id="c22ab-111">To configure Azure AD integration with Convercent, you need the following items:</span></span>

- <span data-ttu-id="c22ab-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="c22ab-112">An Azure AD subscription</span></span>
- <span data-ttu-id="c22ab-113">подписка Convercent с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="c22ab-113">A Convercent single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="c22ab-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="c22ab-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="c22ab-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="c22ab-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="c22ab-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="c22ab-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="c22ab-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c22ab-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="c22ab-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="c22ab-118">Scenario description</span></span>
<span data-ttu-id="c22ab-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="c22ab-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="c22ab-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="c22ab-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="c22ab-121">Добавление Convercent из коллекции</span><span class="sxs-lookup"><span data-stu-id="c22ab-121">Adding Convercent from the gallery</span></span>
2. <span data-ttu-id="c22ab-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="c22ab-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-convercent-from-the-gallery"></a><span data-ttu-id="c22ab-123">Добавление Convercent из коллекции</span><span class="sxs-lookup"><span data-stu-id="c22ab-123">Adding Convercent from the gallery</span></span>
<span data-ttu-id="c22ab-124">Чтобы настроить интеграцию Convercent с Azure AD, необходимо добавить Convercent из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="c22ab-124">To configure the integration of Convercent into Azure AD, you need to add Convercent from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="c22ab-125">**Чтобы добавить Convercent из коллекции, выполните следующее.**</span><span class="sxs-lookup"><span data-stu-id="c22ab-125">**To add Convercent from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="c22ab-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c22ab-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="c22ab-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="c22ab-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="c22ab-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="c22ab-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="c22ab-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="c22ab-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="c22ab-133">В поле поиска введите **Convercent**.</span><span class="sxs-lookup"><span data-stu-id="c22ab-133">In the search box, type **Convercent**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_search.png)

5. <span data-ttu-id="c22ab-135">На панели результатов выберите **Convercent** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="c22ab-135">In the results panel, select **Convercent**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="c22ab-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="c22ab-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="c22ab-138">В этом разделе описана настройка и проверка единого входа Azure AD в Convercent с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c22ab-138">In this section, you configure and test Azure AD single sign-on with Convercent based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="c22ab-139">Чтобы единый вход работал, Azure AD необходимо знать, какой пользователь в Convercent соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c22ab-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Convercent is to a user in Azure AD.</span></span> <span data-ttu-id="c22ab-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Convercent.</span><span class="sxs-lookup"><span data-stu-id="c22ab-140">In other words, a link relationship between an Azure AD user and the related user in Convercent needs to be established.</span></span>

<span data-ttu-id="c22ab-141">Чтобы установить эту связь, следует назначить **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Convercent.</span><span class="sxs-lookup"><span data-stu-id="c22ab-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Convercent.</span></span>

<span data-ttu-id="c22ab-142">Чтобы настроить и проверить единый вход в Azure AD в Convercent, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="c22ab-142">To configure and test Azure AD single sign-on with Convercent, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="c22ab-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="c22ab-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="c22ab-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c22ab-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="c22ab-145">**[Создание тестового пользователя Convercent](#creating-a-convercent-test-user)** требуется для создания в Convercent пользователя Britta Simon, связанного с соответствующим пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c22ab-145">**[Creating a Convercent test user](#creating-a-convercent-test-user)** - to have a counterpart of Britta Simon in Convercent that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="c22ab-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c22ab-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="c22ab-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="c22ab-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="c22ab-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="c22ab-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="c22ab-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Convercent.</span><span class="sxs-lookup"><span data-stu-id="c22ab-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Convercent application.</span></span>

<span data-ttu-id="c22ab-150">**Чтобы настроить единый вход Azure AD в Convercent, выполните следующее.**</span><span class="sxs-lookup"><span data-stu-id="c22ab-150">**To configure Azure AD single sign-on with Convercent, perform the following steps:**</span></span>

1. <span data-ttu-id="c22ab-151">На портале Azure на странице интеграции с приложением **Convercent** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="c22ab-151">In the Azure portal, on the **Convercent** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="c22ab-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="c22ab-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_samlbase.png)

3. <span data-ttu-id="c22ab-155">Если вы хотите настроить приложение в **режиме, инициированном поставщиком удостоверений**, то в разделе **Домены и URL-адреса приложения Convercent** выполните следующее действие:</span><span class="sxs-lookup"><span data-stu-id="c22ab-155">On the **Convercent Domain and URLs** section, If you wish to configure the application in **IDP initiated mode**, perform the following step:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_url.png)

    <span data-ttu-id="c22ab-157">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<instancename>.convercent.com/`</span><span class="sxs-lookup"><span data-stu-id="c22ab-157">In the **Identifier** textbox, type a URL using the following pattern: `https://<instancename>.convercent.com/`</span></span>
 
4. <span data-ttu-id="c22ab-158">Если вы хотите настроить приложение в **режиме, инициированном поставщиком услуг**, то в разделе **Домены и URL-адреса приложения Convercent** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="c22ab-158">If you wish to configure the application in **SP initiated mode**, on the **Convercent Domain and URLs** section perform the following steps:</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_url1.png)

     <span data-ttu-id="c22ab-160">а.</span><span class="sxs-lookup"><span data-stu-id="c22ab-160">a.</span></span> <span data-ttu-id="c22ab-161">Щелкните **Показать дополнительные параметры URL-адресов**.</span><span class="sxs-lookup"><span data-stu-id="c22ab-161">Click **"Show advanced URL settings."**</span></span> 

     <span data-ttu-id="c22ab-162">b.</span><span class="sxs-lookup"><span data-stu-id="c22ab-162">b.</span></span> <span data-ttu-id="c22ab-163">В текстовом поле **URL-адрес для входа** введите значение в следующем формате: `https://<instancename>.convercent.com/`.</span><span class="sxs-lookup"><span data-stu-id="c22ab-163">In the **Sign On URL** textbox, type the value using the following pattern: `https://<instancename>.convercent.com/`</span></span>

     <span data-ttu-id="c22ab-164">c.</span><span class="sxs-lookup"><span data-stu-id="c22ab-164">c.</span></span> <span data-ttu-id="c22ab-165">В текстовое поле **Состояние ретранслятора** введите значение в следующем формате: `https://<instancename>.convercent.com/`.</span><span class="sxs-lookup"><span data-stu-id="c22ab-165">In the **Relay State** textbox, type the value using the following pattern: `https://<instancename>.convercent.com/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="c22ab-166">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="c22ab-166">These values are not the real values.</span></span> <span data-ttu-id="c22ab-167">Замените эти значения фактическим идентификатором, URL-адресом для входа и состоянием ретранслятора.</span><span class="sxs-lookup"><span data-stu-id="c22ab-167">Update these values with the actual Identifier, Sign On URL and Relay State.</span></span> <span data-ttu-id="c22ab-168">Чтобы получить их, обратитесь в [службу поддержки клиентов Convercent](http://support.convercent.com).</span><span class="sxs-lookup"><span data-stu-id="c22ab-168">Contact [Convercent Client support team](http://support.convercent.com) to get these values.</span></span>

5. <span data-ttu-id="c22ab-169">В разделе **Сертификат подписи SAML** щелкните **XML метаданных** и сохраните XML-файл на компьютере.</span><span class="sxs-lookup"><span data-stu-id="c22ab-169">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_certificate.png) 

6. <span data-ttu-id="c22ab-171">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="c22ab-171">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-convercent-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="c22ab-173">Чтобы настроить единый вход для своего приложения, обратитесь в [службу поддержки Convercent](mailto:support@convercent.com) и предоставьте скачанный **XML-файл метаданных**.</span><span class="sxs-lookup"><span data-stu-id="c22ab-173">To get SSO configured for your application, contact [Convercent support team](mailto:support@convercent.com) and provide them with the downloaded **Metadata XML**.</span></span>

> [!TIP]
> <span data-ttu-id="c22ab-174">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="c22ab-174">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="c22ab-175">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="c22ab-175">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="c22ab-176">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="c22ab-176">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="c22ab-177">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="c22ab-177">Creating an Azure AD test user</span></span>
<span data-ttu-id="c22ab-178">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="c22ab-178">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="c22ab-180">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="c22ab-180">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="c22ab-181">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c22ab-181">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-convercent-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="c22ab-183">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="c22ab-183">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-convercent-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="c22ab-185">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="c22ab-185">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-convercent-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="c22ab-187">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="c22ab-187">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-convercent-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="c22ab-189">а.</span><span class="sxs-lookup"><span data-stu-id="c22ab-189">a.</span></span> <span data-ttu-id="c22ab-190">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="c22ab-190">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="c22ab-191">b.</span><span class="sxs-lookup"><span data-stu-id="c22ab-191">b.</span></span> <span data-ttu-id="c22ab-192">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="c22ab-192">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="c22ab-193">c.</span><span class="sxs-lookup"><span data-stu-id="c22ab-193">c.</span></span> <span data-ttu-id="c22ab-194">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="c22ab-194">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="c22ab-195">d.</span><span class="sxs-lookup"><span data-stu-id="c22ab-195">d.</span></span> <span data-ttu-id="c22ab-196">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="c22ab-196">Click **Create**.</span></span>
 
### <a name="creating-a-convercent-test-user"></a><span data-ttu-id="c22ab-197">Создание тестового пользователя Convercent</span><span class="sxs-lookup"><span data-stu-id="c22ab-197">Creating a Convercent test user</span></span>

<span data-ttu-id="c22ab-198">Обратитесь к [группе поддержки Convercent](mailto:support@convercent.com), чтобы добавить пользователей на платформу Convercent.</span><span class="sxs-lookup"><span data-stu-id="c22ab-198">Work with [Convercent support team](mailto:support@convercent.com) to add the users in the Convercent platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="c22ab-199">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="c22ab-199">Assigning the Azure AD test user</span></span>

<span data-ttu-id="c22ab-200">В этом разделе описано, как позволить пользователю Britta Simon использовать единый вход Azure путем предоставления доступа к Convercent.</span><span class="sxs-lookup"><span data-stu-id="c22ab-200">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Convercent.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="c22ab-202">**Чтобы назначить пользователя Britta Simon в Convercent, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="c22ab-202">**To assign Britta Simon to Convercent, perform the following steps:**</span></span>

1. <span data-ttu-id="c22ab-203">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="c22ab-203">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="c22ab-205">Из списка приложений выберите **Convercent**.</span><span class="sxs-lookup"><span data-stu-id="c22ab-205">In the applications list, select **Convercent**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-convercent-tutorial/tutorial_convercent_app.png) 

3. <span data-ttu-id="c22ab-207">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="c22ab-207">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="c22ab-209">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="c22ab-209">Click **Add** button.</span></span> <span data-ttu-id="c22ab-210">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="c22ab-210">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="c22ab-212">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="c22ab-212">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="c22ab-213">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="c22ab-213">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="c22ab-214">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="c22ab-214">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="c22ab-215">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="c22ab-215">Testing single sign-on</span></span>

<span data-ttu-id="c22ab-216">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="c22ab-216">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="c22ab-217">Щелкнув элемент Convercent на панели доступа, вы автоматически войдете в приложение Convercent.</span><span class="sxs-lookup"><span data-stu-id="c22ab-217">When you click the Convercent tile in the Access Panel, you should get automatically signed-on to your Convercent application.</span></span>
<span data-ttu-id="c22ab-218">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c22ab-218">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="c22ab-219">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="c22ab-219">Additional resources</span></span>

* [<span data-ttu-id="c22ab-220">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c22ab-220">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="c22ab-221">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c22ab-221">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-convercent-tutorial/tutorial_general_203.png

