---
title: "Учебник. Интеграция Azure Active Directory с Cornerstone OnDemand | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и Cornerstone OnDemand."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f57c5fef-49b0-4591-91ef-fc0de6d654ab
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: 8bb32588579a0d40b9ae7e0f823c6daab21c856e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-cornerstone-ondemand"></a><span data-ttu-id="23ebb-103">Руководство. Интеграция Azure Active Directory с Cornerstone OnDemand</span><span class="sxs-lookup"><span data-stu-id="23ebb-103">Tutorial: Azure Active Directory integration with Cornerstone OnDemand</span></span>

<span data-ttu-id="23ebb-104">В этом руководстве описано, как интегрировать Cornerstone OnDemand с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="23ebb-104">In this tutorial, you learn how to integrate Cornerstone OnDemand with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="23ebb-105">Интеграция Cornerstone OnDemand с Azure AD обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="23ebb-105">Integrating Cornerstone OnDemand with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="23ebb-106">С помощью Azure AD вы можете контролировать доступ к Cornerstone OnDemand</span><span class="sxs-lookup"><span data-stu-id="23ebb-106">You can control in Azure AD who has access to Cornerstone OnDemand</span></span>
- <span data-ttu-id="23ebb-107">Вы можете включить автоматический вход пользователей в Cornerstone OnDemand (единый вход) с учетной записью Azure AD</span><span class="sxs-lookup"><span data-stu-id="23ebb-107">You can enable your users to automatically get signed-on to Cornerstone OnDemand (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="23ebb-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="23ebb-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="23ebb-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="23ebb-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="23ebb-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="23ebb-110">Prerequisites</span></span>

<span data-ttu-id="23ebb-111">Чтобы настроить интеграцию Azure AD с Cornerstone OnDemand, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="23ebb-111">To configure Azure AD integration with Cornerstone OnDemand, you need the following items:</span></span>

- <span data-ttu-id="23ebb-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="23ebb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="23ebb-113">подписка Cornerstone OnDemand с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="23ebb-113">A Cornerstone OnDemand single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="23ebb-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="23ebb-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="23ebb-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="23ebb-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="23ebb-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="23ebb-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="23ebb-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="23ebb-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="23ebb-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="23ebb-118">Scenario description</span></span>
<span data-ttu-id="23ebb-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="23ebb-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="23ebb-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="23ebb-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="23ebb-121">Добавление Cornerstone OnDemand из коллекции</span><span class="sxs-lookup"><span data-stu-id="23ebb-121">Adding Cornerstone OnDemand from the gallery</span></span>
2. <span data-ttu-id="23ebb-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="23ebb-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-cornerstone-ondemand-from-the-gallery"></a><span data-ttu-id="23ebb-123">Добавление Cornerstone OnDemand из коллекции</span><span class="sxs-lookup"><span data-stu-id="23ebb-123">Adding Cornerstone OnDemand from the gallery</span></span>
<span data-ttu-id="23ebb-124">Чтобы настроить интеграцию Cornerstone OnDemand с Azure AD, необходимо добавить это приложение из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="23ebb-124">To configure the integration of Cornerstone OnDemand into Azure AD, you need to add Cornerstone OnDemand from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="23ebb-125">**Чтобы добавить Cornerstone OnDemand из коллекции, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="23ebb-125">**To add Cornerstone OnDemand from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="23ebb-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="23ebb-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="23ebb-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="23ebb-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="23ebb-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="23ebb-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="23ebb-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="23ebb-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="23ebb-133">В поле поиска введите **Cornerstone OnDemand**.</span><span class="sxs-lookup"><span data-stu-id="23ebb-133">In the search box, type **Cornerstone OnDemand**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_search.png)

5. <span data-ttu-id="23ebb-135">В области результатов выберите **Cornerstone OnDemand** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="23ebb-135">In the results panel, select **Cornerstone OnDemand**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="23ebb-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="23ebb-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="23ebb-138">В этом разделе описана настройка и проверка единого входа Azure AD в Cornerstone OnDemand для тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="23ebb-138">In this section, you configure and test Azure AD single sign-on with Cornerstone OnDemand based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="23ebb-139">Для работы единого входа Azure AD необходимо знать, какой пользователь в Cornerstone OnDemand соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="23ebb-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Cornerstone OnDemand is to a user in Azure AD.</span></span> <span data-ttu-id="23ebb-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Cornerstone OnDemand.</span><span class="sxs-lookup"><span data-stu-id="23ebb-140">In other words, a link relationship between an Azure AD user and the related user in Cornerstone OnDemand needs to be established.</span></span>

<span data-ttu-id="23ebb-141">Чтобы установить эту связь, укажите **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Cornerstone OnDemand.</span><span class="sxs-lookup"><span data-stu-id="23ebb-141">In Cornerstone OnDemand, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="23ebb-142">Чтобы настроить и проверить единый вход Azure AD в Cornerstone OnDemand, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="23ebb-142">To configure and test Azure AD single sign-on with Cornerstone OnDemand, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="23ebb-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="23ebb-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="23ebb-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="23ebb-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="23ebb-145">**[Создание тестового пользователя Cornerstone OnDemand](#creating-a-cornerstone-ondemand-test-user)** требуется для создания в Cornerstone OnDemand пользователя Britta Simon, связанного с представлением этого пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="23ebb-145">**[Creating a Cornerstone OnDemand test user](#creating-a-cornerstone-ondemand-test-user)** - to have a counterpart of Britta Simon in Cornerstone OnDemand that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="23ebb-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="23ebb-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="23ebb-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="23ebb-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="23ebb-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="23ebb-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="23ebb-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Cornerstone OnDemand.</span><span class="sxs-lookup"><span data-stu-id="23ebb-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Cornerstone OnDemand application.</span></span>

<span data-ttu-id="23ebb-150">**Чтобы настроить единый вход Azure AD в Cornerstone OnDemand, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="23ebb-150">**To configure Azure AD single sign-on with Cornerstone OnDemand, perform the following steps:**</span></span>

1. <span data-ttu-id="23ebb-151">На портале Azure на странице интеграции с приложением **Cornerstone OnDemand** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="23ebb-151">In the Azure portal, on the **Cornerstone OnDemand** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="23ebb-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="23ebb-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_samlbase.png)

3. <span data-ttu-id="23ebb-155">В разделе **Домены и URL-адреса Cornerstone OnDemand** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="23ebb-155">On the **Cornerstone OnDemand Domain and URLs** section, perform the following step:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_url.png)

    <span data-ttu-id="23ebb-157">а.</span><span class="sxs-lookup"><span data-stu-id="23ebb-157">a.</span></span> <span data-ttu-id="23ebb-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<company>.csod.com`</span><span class="sxs-lookup"><span data-stu-id="23ebb-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<company>.csod.com`</span></span>

    <span data-ttu-id="23ebb-159">b.</span><span class="sxs-lookup"><span data-stu-id="23ebb-159">b.</span></span> <span data-ttu-id="23ebb-160">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<company>.csod.com`</span><span class="sxs-lookup"><span data-stu-id="23ebb-160">In **Identifier** textbox, type a URL using the following pattern: `https://<company>.csod.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="23ebb-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="23ebb-161">These values are not real.</span></span> <span data-ttu-id="23ebb-162">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="23ebb-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="23ebb-163">Чтобы получить эти значения, обратитесь в [службу поддержки клиентов Cornerstone OnDemand](mailTo:moreinfo@csod.com).</span><span class="sxs-lookup"><span data-stu-id="23ebb-163">Contact [Cornerstone OnDemand Client support team](mailTo:moreinfo@csod.com) to get these values.</span></span> 
 
4. <span data-ttu-id="23ebb-164">В разделе **Сертификат подписи SAML** щелкните **Сертификат (Base64)**, а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="23ebb-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_certificate.png) 

5. <span data-ttu-id="23ebb-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="23ebb-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="23ebb-168">В разделе **Настройка Cornerstone OnDemand** щелкните **Настроить Cornerstone OnDemand**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="23ebb-168">On the **Cornerstone OnDemand Configuration** section, click **Configure Cornerstone OnDemand** to open **Configure sign-on** window.</span></span> <span data-ttu-id="23ebb-169">Скопируйте **URL-адрес выхода и URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="23ebb-169">Copy the **Sign-Out URL and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_configure.png) 

7. <span data-ttu-id="23ebb-171">Чтобы настроить единый вход на стороне **Cornerstone OnDemand**, нужно отправить скачанный **Сертификат**, **URL-адрес выхода** и **URL-адрес службы единого входа SAML** в [службу поддержки Cornerstone OnDemand](mailTo:moreinfo@csod.com).</span><span class="sxs-lookup"><span data-stu-id="23ebb-171">To configure single sign-on on **Cornerstone OnDemand** side, you need to send the downloaded **Certificate**, **Sign-Out URL** and **SAML Single Sign-On Service URL**  to [Cornerstone OnDemand support team](mailTo:moreinfo@csod.com).</span></span> <span data-ttu-id="23ebb-172">Специалисты службы поддержки настроят подключение единого входа SAML на обеих сторонах подключения.</span><span class="sxs-lookup"><span data-stu-id="23ebb-172">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="23ebb-173">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="23ebb-173">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="23ebb-174">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="23ebb-174">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="23ebb-175">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="23ebb-175">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="23ebb-176">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="23ebb-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="23ebb-177">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="23ebb-177">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="23ebb-179">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="23ebb-179">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="23ebb-180">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="23ebb-180">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cornerstone-ondemand-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="23ebb-182">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="23ebb-182">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cornerstone-ondemand-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="23ebb-184">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="23ebb-184">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cornerstone-ondemand-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="23ebb-186">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="23ebb-186">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-cornerstone-ondemand-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="23ebb-188">а.</span><span class="sxs-lookup"><span data-stu-id="23ebb-188">a.</span></span> <span data-ttu-id="23ebb-189">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="23ebb-189">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="23ebb-190">b.</span><span class="sxs-lookup"><span data-stu-id="23ebb-190">b.</span></span> <span data-ttu-id="23ebb-191">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="23ebb-191">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="23ebb-192">c.</span><span class="sxs-lookup"><span data-stu-id="23ebb-192">c.</span></span> <span data-ttu-id="23ebb-193">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="23ebb-193">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="23ebb-194">d.</span><span class="sxs-lookup"><span data-stu-id="23ebb-194">d.</span></span> <span data-ttu-id="23ebb-195">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="23ebb-195">Click **Create**.</span></span>
 
### <a name="creating-a-cornerstone-ondemand-test-user"></a><span data-ttu-id="23ebb-196">Создание тестового пользователя Cornerstone OnDemand</span><span class="sxs-lookup"><span data-stu-id="23ebb-196">Creating a Cornerstone OnDemand test user</span></span>

<span data-ttu-id="23ebb-197">Чтобы пользователи Azure AD могли выполнять вход в Cornerstone OnDemand, они должны быть подготовлены для работы с Cornerstone OnDemand.</span><span class="sxs-lookup"><span data-stu-id="23ebb-197">In order to enable Azure AD users to log into Cornerstone OnDemand, they must be provisioned into Cornerstone OnDemand.</span></span> <span data-ttu-id="23ebb-198">В случае с Cornerstone OnDemand подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="23ebb-198">In the case of Cornerstone OnDemand, provisioning is a manual task.</span></span>

<span data-ttu-id="23ebb-199">Чтобы настроить подготовку пользователей, отправьте сведения о пользователе Azure AD, которого необходимо подготовить (например, имя, адрес электронной почты), в [службу поддержки Cornerstone OnDemand](mailTo:moreinfo@csod.com).</span><span class="sxs-lookup"><span data-stu-id="23ebb-199">To configure user provisioning, send the information (e.g.: Name, Email) about the Azure AD user you want to provision to the [Cornerstone OnDemand support team](mailTo:moreinfo@csod.com).</span></span>

>[!NOTE]
><span data-ttu-id="23ebb-200">Вы можете использовать любые другие средства создания учетной записи пользователя Cornerstone OnDemand или API, предоставляемые Cornerstone OnDemand, для подготовки учетных записей пользователей AAD.</span><span class="sxs-lookup"><span data-stu-id="23ebb-200">You can use any other Cornerstone OnDemand user account creation tools or APIs provided by Cornerstone OnDemand to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="23ebb-201">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="23ebb-201">Assigning the Azure AD test user</span></span>

<span data-ttu-id="23ebb-202">В этом разделе описано, как включить единый вход Azure для пользователя Britta Simon, предоставив этому пользователю доступ к Cornerstone OnDemand.</span><span class="sxs-lookup"><span data-stu-id="23ebb-202">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Cornerstone OnDemand.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="23ebb-204">**Чтобы назначить пользователя Britta Simon для приложения Cornerstone OnDemand, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="23ebb-204">**To assign Britta Simon to Cornerstone OnDemand, perform the following steps:**</span></span>

1. <span data-ttu-id="23ebb-205">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="23ebb-205">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="23ebb-207">В списке приложений выберите **Cornerstone OnDemand**.</span><span class="sxs-lookup"><span data-stu-id="23ebb-207">In the applications list, select **Cornerstone OnDemand**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_cornerstoneondemand_app.png) 

3. <span data-ttu-id="23ebb-209">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="23ebb-209">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="23ebb-211">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="23ebb-211">Click **Add** button.</span></span> <span data-ttu-id="23ebb-212">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="23ebb-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="23ebb-214">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="23ebb-214">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="23ebb-215">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="23ebb-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="23ebb-216">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="23ebb-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="23ebb-217">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="23ebb-217">Testing single sign-on</span></span>

<span data-ttu-id="23ebb-218">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="23ebb-218">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="23ebb-219">Щелкнув элемент Cornerstone OnDemand на панели доступа, вы автоматически войдете в приложение Cornerstone OnDemand.</span><span class="sxs-lookup"><span data-stu-id="23ebb-219">When you click the Cornerstone OnDemand tile in the Access Panel, you should get automatically signed-on to your Cornerstone OnDemand application.</span></span>
<span data-ttu-id="23ebb-220">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="23ebb-220">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="23ebb-221">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="23ebb-221">Additional resources</span></span>

* [<span data-ttu-id="23ebb-222">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="23ebb-222">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="23ebb-223">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="23ebb-223">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-cornerstone-ondemand-tutorial/tutorial_general_203.png

