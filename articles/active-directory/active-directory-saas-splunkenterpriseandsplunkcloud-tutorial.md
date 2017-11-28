---
title: "Руководство. Интеграция Azure Active Directory с приложениями Splunk Enterprise и Splunk Cloud | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в Splunk Enterprise и Splunk Cloud."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: b3e2b4a9-749c-4895-813d-db46f8dfdbf8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/02/2017
ms.author: jeedes
ms.openlocfilehash: 181d0f33245f0811c15c1e7945c797502ef71eba
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-splunk-enterprise-and-splunk-cloud"></a><span data-ttu-id="401f9-103">Руководство. Интеграция Azure Active Directory с приложениями Splunk Enterprise и Splunk Cloud</span><span class="sxs-lookup"><span data-stu-id="401f9-103">Tutorial: Azure Active Directory integration with Splunk Enterprise and Splunk Cloud</span></span>

<span data-ttu-id="401f9-104">В этом руководстве описано, как интегрировать Splunk Enterprise и Splunk Cloud с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="401f9-104">In this tutorial, you learn how to integrate Splunk Enterprise and Splunk Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="401f9-105">Интеграция Splunk Enterprise и Splunk Cloud с Azure AD обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="401f9-105">Integrating Splunk Enterprise and Splunk Cloud with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="401f9-106">С помощью Azure AD можно контролировать доступ к Splunk Enterprise и Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="401f9-106">You can control in Azure AD who has access to Splunk Enterprise and Splunk Cloud</span></span>
- <span data-ttu-id="401f9-107">Вы можете включить автоматический вход пользователей в Splunk Enterprise и Splunk Cloud (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="401f9-107">You can enable your users to automatically get signed-on to Splunk Enterprise and Splunk Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="401f9-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="401f9-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="401f9-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="401f9-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="401f9-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="401f9-110">Prerequisites</span></span>

<span data-ttu-id="401f9-111">Чтобы настроить интеграцию Azure AD с приложениями Splunk Enterprise и Splunk Cloud, вам потребуется следующее:</span><span class="sxs-lookup"><span data-stu-id="401f9-111">To configure Azure AD integration with Splunk Enterprise and Splunk Cloud, you need the following items:</span></span>

- <span data-ttu-id="401f9-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="401f9-112">An Azure AD subscription</span></span>
- <span data-ttu-id="401f9-113">подписка Splunk Enterprise и Splunk Cloud с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="401f9-113">A Splunk Enterprise and Splunk Cloud single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="401f9-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="401f9-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="401f9-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="401f9-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="401f9-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="401f9-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="401f9-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="401f9-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="401f9-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="401f9-118">Scenario description</span></span>
<span data-ttu-id="401f9-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="401f9-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="401f9-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="401f9-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="401f9-121">Добавление Splunk Enterprise и Splunk Cloud из коллекции.</span><span class="sxs-lookup"><span data-stu-id="401f9-121">Adding Splunk Enterprise and Splunk Cloud from the gallery</span></span>
2. <span data-ttu-id="401f9-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="401f9-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-splunk-enterprise-and-splunk-cloud-from-the-gallery"></a><span data-ttu-id="401f9-123">Добавление Splunk Enterprise и Splunk Cloud из коллекции</span><span class="sxs-lookup"><span data-stu-id="401f9-123">Adding Splunk Enterprise and Splunk Cloud from the gallery</span></span>
<span data-ttu-id="401f9-124">Чтобы настроить интеграцию Splunk Enterprise и Splunk Cloud с Azure AD, необходимо добавить Splunk Enterprise и Splunk Cloud из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="401f9-124">To configure the integration of Splunk Enterprise and Splunk Cloud into Azure AD, you need to add Splunk Enterprise and Splunk Cloud from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="401f9-125">**Чтобы добавить Splunk Enterprise и Splunk Cloud из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="401f9-125">**To add Splunk Enterprise and Splunk Cloud from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="401f9-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="401f9-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="401f9-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="401f9-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="401f9-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="401f9-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="401f9-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="401f9-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="401f9-133">В поле поиска введите **Splunk Enterprise и Splunk Cloud**.</span><span class="sxs-lookup"><span data-stu-id="401f9-133">In the search box, type **Splunk Enterprise and Splunk Cloud**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_splunkenterpriseandsplunkcloud_search.png)

5. <span data-ttu-id="401f9-135">В области результатов выберите **Splunk Enterprise и Splunk Cloud**, а затем нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="401f9-135">In the results panel, select **Splunk Enterprise and Splunk Cloud**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_splunkenterpriseandsplunkcloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="401f9-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="401f9-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="401f9-138">В этом разделе описывается настройка и проверка единого входа Azure AD в Splunk Enterprise и Splunk Cloud с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="401f9-138">In this section, you configure and test Azure AD single sign-on with Splunk Enterprise and Splunk Cloud based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="401f9-139">Для работы единого входа в Azure AD необходимо указать, какой пользователь в Splunk Enterprise и Splunk Cloud соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="401f9-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Splunk Enterprise and Splunk Cloud is to a user in Azure AD.</span></span> <span data-ttu-id="401f9-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Splunk Enterprise и Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="401f9-140">In other words, a link relationship between an Azure AD user and the related user in Splunk Enterprise and Splunk Cloud needs to be established.</span></span>

<span data-ttu-id="401f9-141">Чтобы установить эту связь, следует назначить **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Splunk Enterprise и Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="401f9-141">In Splunk Enterprise and Splunk Cloud, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="401f9-142">Чтобы настроить и проверить единый вход Azure AD в Splunk Enterprise и Splunk Cloud, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="401f9-142">To configure and test Azure AD single sign-on with Splunk Enterprise and Splunk Cloud, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="401f9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="401f9-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="401f9-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="401f9-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="401f9-145">**[Создание тестового пользователя Splunk Enterprise и Splunk Cloud](#creating-a-splunk-enterprise-and-splunk-cloud-test-user)** требуется для создания пользователя Britta Simon в Splunk Enterprise и Splunk Cloud, связанного с соответствующим представлением в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="401f9-145">**[Creating a Splunk Enterprise and Splunk Cloud test user](#creating-a-splunk-enterprise-and-splunk-cloud-test-user)** - to have a counterpart of Britta Simon in Splunk Enterprise and Splunk Cloud that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="401f9-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="401f9-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="401f9-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="401f9-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="401f9-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="401f9-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="401f9-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Splunk Enterprise и Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="401f9-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Splunk Enterprise and Splunk Cloud application.</span></span>

<span data-ttu-id="401f9-150">**Чтобы настроить единый вход Azure AD в Splunk Enterprise и Splunk Cloud, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="401f9-150">**To configure Azure AD single sign-on with Splunk Enterprise and Splunk Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="401f9-151">На портале Azure на странице интеграции с приложением **Splunk Enterprise и Splunk Cloud** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="401f9-151">In the Azure portal, on the **Splunk Enterprise and Splunk Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="401f9-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="401f9-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_splunkenterpriseandsplunkcloud_samlbase.png)

3. <span data-ttu-id="401f9-155">Если требуется настроить приложение в **режиме, инициированном поставщиком удостоверений**, то в разделе **Домен и URL-адреса Splunk Enterprise и Splunk Cloud** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="401f9-155">On the **Splunk Enterprise and Splunk Cloud Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_splunkenterpriseandsplunkcloud_url.png)

    <span data-ttu-id="401f9-157">а.</span><span class="sxs-lookup"><span data-stu-id="401f9-157">a.</span></span> <span data-ttu-id="401f9-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<splunkserverUrl>/en-US/app/launcher/home`</span><span class="sxs-lookup"><span data-stu-id="401f9-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<splunkserverUrl>/en-US/app/launcher/home`</span></span>
    
    <span data-ttu-id="401f9-159">b.</span><span class="sxs-lookup"><span data-stu-id="401f9-159">b.</span></span> <span data-ttu-id="401f9-160">В текстовом поле **Идентификатор** введите URL-адрес сервера Splunk Server.</span><span class="sxs-lookup"><span data-stu-id="401f9-160">In the **Identifier** textbox, type the URL of your Splunk Server.</span></span>

    <span data-ttu-id="401f9-161">c.</span><span class="sxs-lookup"><span data-stu-id="401f9-161">c.</span></span> <span data-ttu-id="401f9-162">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате: `https://<splunkserver>/saml/acs`.</span><span class="sxs-lookup"><span data-stu-id="401f9-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://<splunkserver>/saml/acs`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="401f9-163">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="401f9-163">These values are not real.</span></span> <span data-ttu-id="401f9-164">Замените их фактическими значениями идентификатора, URL-адреса ответа и URL-адреса входа.</span><span class="sxs-lookup"><span data-stu-id="401f9-164">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="401f9-165">Мы рекомендуем использовать уникальное значение строки идентификатора.</span><span class="sxs-lookup"><span data-stu-id="401f9-165">Here we suggest you to use the unique value of string in the Identifier.</span></span> <span data-ttu-id="401f9-166">Чтобы получить эти значения, обратитесь в [службу поддержки клиентов Splunk Enterprise и Splunk Cloud](https://www.splunk.com/content/splunkcom/en_us/about-us/contact.html#tabs/customer-support).</span><span class="sxs-lookup"><span data-stu-id="401f9-166">Contact [Splunk Enterprise and Splunk Cloud Client support team](https://www.splunk.com/content/splunkcom/en_us/about-us/contact.html#tabs/customer-support) to get these values.</span></span> 

4. <span data-ttu-id="401f9-167">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="401f9-167">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_splunkenterpriseandsplunkcloud_certificate.png) 

5. <span data-ttu-id="401f9-169">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="401f9-169">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="401f9-171">Для настройки единого входа на стороне **Splunk Enterprise и Splunk Cloud** необходимо отправить загруженные **метаданные в формате XML** в [службу поддержки Splunk Enterprise и Splunk Cloud](https://www.splunk.com/content/splunkcom/en_us/about-us/contact.html#tabs/customer-support).</span><span class="sxs-lookup"><span data-stu-id="401f9-171">To configure single sign-on on **Splunk Enterprise and Splunk Cloud** side, you need to send the downloaded **Metadata XML** to [Splunk Enterprise and Splunk Cloud support team](https://www.splunk.com/content/splunkcom/en_us/about-us/contact.html#tabs/customer-support).</span></span>

> [!TIP]
> <span data-ttu-id="401f9-172">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="401f9-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="401f9-173">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="401f9-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="401f9-174">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="401f9-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="401f9-175">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="401f9-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="401f9-176">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="401f9-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="401f9-178">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="401f9-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="401f9-179">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="401f9-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="401f9-181">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="401f9-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="401f9-183">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="401f9-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="401f9-185">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="401f9-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="401f9-187">а.</span><span class="sxs-lookup"><span data-stu-id="401f9-187">a.</span></span> <span data-ttu-id="401f9-188">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="401f9-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="401f9-189">b.</span><span class="sxs-lookup"><span data-stu-id="401f9-189">b.</span></span> <span data-ttu-id="401f9-190">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="401f9-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="401f9-191">c.</span><span class="sxs-lookup"><span data-stu-id="401f9-191">c.</span></span> <span data-ttu-id="401f9-192">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="401f9-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="401f9-193">d.</span><span class="sxs-lookup"><span data-stu-id="401f9-193">d.</span></span> <span data-ttu-id="401f9-194">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="401f9-194">Click **Create**.</span></span>
 
### <a name="creating-a-splunk-enterprise-and-splunk-cloud-test-user"></a><span data-ttu-id="401f9-195">Создание тестового пользователя Splunk Enterprise и Splunk Cloud</span><span class="sxs-lookup"><span data-stu-id="401f9-195">Creating a Splunk Enterprise and Splunk Cloud test user</span></span>

<span data-ttu-id="401f9-196">В этом разделе описано, как создать пользователя Britta Simon в Splunk Enterprise и Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="401f9-196">In this section, you create a user called Britta Simon in Splunk Enterprise and Splunk Cloud.</span></span> <span data-ttu-id="401f9-197">Чтобы добавить пользователей на платформу Splunk Enterprise и Splunk Cloud, обратитесь в [службу поддержки Splunk Enterprise и Splunk Cloud](https://www.splunk.com/content/splunkcom/en_us/about-us/contact.html#tabs/customer-support).</span><span class="sxs-lookup"><span data-stu-id="401f9-197">Work with  [Splunk Enterprise and Splunk Cloud support team](https://www.splunk.com/content/splunkcom/en_us/about-us/contact.html#tabs/customer-support) to add the users in the Splunk Enterprise and Splunk Cloud platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="401f9-198">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="401f9-198">Assigning the Azure AD test user</span></span>

<span data-ttu-id="401f9-199">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив ему доступ к Splunk Enterprise и Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="401f9-199">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Splunk Enterprise and Splunk Cloud.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="401f9-201">**Чтобы назначить Britta Simon в Splunk Enterprise и Splunk Cloud, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="401f9-201">**To assign Britta Simon to Splunk Enterprise and Splunk Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="401f9-202">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="401f9-202">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="401f9-204">В списке приложений выберите **Splunk Enterprise и Splunk Cloud**.</span><span class="sxs-lookup"><span data-stu-id="401f9-204">In the applications list, select **Splunk Enterprise and Splunk Cloud**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_splunkenterpriseandsplunkcloud_app.png) 

3. <span data-ttu-id="401f9-206">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="401f9-206">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="401f9-208">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="401f9-208">Click **Add** button.</span></span> <span data-ttu-id="401f9-209">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="401f9-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="401f9-211">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="401f9-211">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="401f9-212">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="401f9-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="401f9-213">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="401f9-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="401f9-214">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="401f9-214">Testing single sign-on</span></span>

<span data-ttu-id="401f9-215">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="401f9-215">In this section, you test your Azure AD SSOonfiguration using the Access Panel.</span></span>

<span data-ttu-id="401f9-216">Щелкнув плитку Splunk Enterprise и Splunk Cloud на панели доступа, вы автоматически войдете в приложение Splunk Enterprise и Splunk Cloud.</span><span class="sxs-lookup"><span data-stu-id="401f9-216">When you click the Splunk Enterprise and Splunk Cloud tile in the Access Panel, you should get automatically signed-on to your Splunk Enterprise and Splunk Cloud application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="401f9-217">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="401f9-217">Additional resources</span></span>

* [<span data-ttu-id="401f9-218">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="401f9-218">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="401f9-219">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="401f9-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-splunkenterpriseandsplunkcloud-tutorial/tutorial_general_203.png

