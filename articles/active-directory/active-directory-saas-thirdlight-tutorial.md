---
title: "Руководство по интеграции Azure Active Directory с ThirdLight | Документы Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в приложении ThirdLight."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 168aae9a-54ee-4c2b-ab12-650a2c62b901
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: ee7710cfea3a13907c0cc940a98c875bf83607a9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-thirdlight"></a><span data-ttu-id="f973c-103">Учебник. Интеграция Azure Active Directory с ThirdLight</span><span class="sxs-lookup"><span data-stu-id="f973c-103">Tutorial: Azure Active Directory integration with ThirdLight</span></span>

<span data-ttu-id="f973c-104">В этом учебнике описано, как интегрировать ThirdLight с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f973c-104">In this tutorial, you learn how to integrate ThirdLight with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f973c-105">Интеграция Azure AD с приложением ThirdLight обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="f973c-105">Integrating ThirdLight with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f973c-106">С помощью Azure AD вы можете контролировать доступ к ThirdLight.</span><span class="sxs-lookup"><span data-stu-id="f973c-106">You can control in Azure AD who has access to ThirdLight</span></span>
- <span data-ttu-id="f973c-107">Вы можете включить автоматический вход пользователей в ThirdLight (единый вход) с использованием учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f973c-107">You can enable your users to automatically get signed-on to ThirdLight (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f973c-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="f973c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f973c-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в статье [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f973c-109">If you want to know more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f973c-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="f973c-110">Prerequisites</span></span>

<span data-ttu-id="f973c-111">Чтобы настроить интеграцию Azure AD с ThirdLight, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="f973c-111">To configure Azure AD integration with ThirdLight, you need the following items:</span></span>

- <span data-ttu-id="f973c-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="f973c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f973c-113">подписка ThirdLight с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="f973c-113">A ThirdLight single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f973c-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="f973c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f973c-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="f973c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f973c-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="f973c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f973c-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f973c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f973c-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="f973c-118">Scenario description</span></span>
<span data-ttu-id="f973c-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="f973c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f973c-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="f973c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f973c-121">Добавление ThirdLight из коллекции</span><span class="sxs-lookup"><span data-stu-id="f973c-121">Adding ThirdLight from the gallery</span></span>
2. <span data-ttu-id="f973c-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="f973c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-thirdlight-from-the-gallery"></a><span data-ttu-id="f973c-123">Добавление ThirdLight из коллекции</span><span class="sxs-lookup"><span data-stu-id="f973c-123">Adding ThirdLight from the gallery</span></span>
<span data-ttu-id="f973c-124">Чтобы настроить интеграцию ThirdLight с Azure AD, необходимо добавить ThirdLight из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="f973c-124">To configure the integration of ThirdLight into Azure AD, you need to add ThirdLight from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f973c-125">**Чтобы добавить ThirdLight из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="f973c-125">**To add ThirdLight from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f973c-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f973c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f973c-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="f973c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f973c-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="f973c-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="f973c-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="f973c-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="f973c-133">В поле поиска введите **Thirdlight**.</span><span class="sxs-lookup"><span data-stu-id="f973c-133">In the search box, type **ThirdLight**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_search.png)

5. <span data-ttu-id="f973c-135">На панели результатов выберите **ThirdLight** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="f973c-135">In the results panel, select **ThirdLight**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f973c-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="f973c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f973c-138">В этом разделе описана настройка и проверка единого входа Azure AD в ThirdLight с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f973c-138">In this section, you configure and test Azure AD single sign-on with ThirdLight based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f973c-139">Чтобы единый вход работал, Azure AD необходимо знать, какой пользователь в ThirdLight соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f973c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in ThirdLight is to a user in Azure AD.</span></span> <span data-ttu-id="f973c-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в ThirdLight.</span><span class="sxs-lookup"><span data-stu-id="f973c-140">In other words, a link relationship between an Azure AD user and the related user in ThirdLight needs to be established.</span></span>

<span data-ttu-id="f973c-141">Чтобы установить эту связь, следует назначить **имя пользователя** в Azure AD в качестве значения **имени пользователя** в ThirdLight.</span><span class="sxs-lookup"><span data-stu-id="f973c-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in ThirdLight.</span></span>

<span data-ttu-id="f973c-142">Чтобы настроить и проверить единый вход Azure AD в ThirdLight, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="f973c-142">To configure and test Azure AD single sign-on with ThirdLight, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f973c-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="f973c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f973c-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f973c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f973c-145">**[Создание тестового пользователя ThirdLight](#creating-a-thirdlight-test-user)** требуется для создания в ThirdLight пользователя Britta Simon, связанного с представлением этого пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f973c-145">**[Creating a ThirdLight test user](#creating-a-thirdlight-test-user)** - to have a counterpart of Britta Simon in ThirdLight that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f973c-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f973c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f973c-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="f973c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f973c-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="f973c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f973c-149">В данном разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении ThirdLight.</span><span class="sxs-lookup"><span data-stu-id="f973c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your ThirdLight application.</span></span>

<span data-ttu-id="f973c-150">**Чтобы настроить единый вход Azure AD в ThirdLight, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="f973c-150">**To configure Azure AD single sign-on with ThirdLight, perform the following steps:**</span></span>

1. <span data-ttu-id="f973c-151">На портале Azure на странице интеграции с приложением **ThirdLight** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="f973c-151">In the Azure portal, on the **ThirdLight** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="f973c-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="f973c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_samlbase.png)

3. <span data-ttu-id="f973c-155">В разделе **Домены и URL-адреса приложения ThirdLight** сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="f973c-155">On the **ThirdLight Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_url.png)

    <span data-ttu-id="f973c-157">а.</span><span class="sxs-lookup"><span data-stu-id="f973c-157">a.</span></span> <span data-ttu-id="f973c-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<subdomain>.thirdlight.com/`</span><span class="sxs-lookup"><span data-stu-id="f973c-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<subdomain>.thirdlight.com/`</span></span>

    <span data-ttu-id="f973c-159">b.</span><span class="sxs-lookup"><span data-stu-id="f973c-159">b.</span></span> <span data-ttu-id="f973c-160">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<subdomain>.thirdlight.com/saml/sp`</span><span class="sxs-lookup"><span data-stu-id="f973c-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<subdomain>.thirdlight.com/saml/sp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f973c-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="f973c-161">These values are not real.</span></span> <span data-ttu-id="f973c-162">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="f973c-162">Update these values with the actual Sign-On URL and Identiifer.</span></span> <span data-ttu-id="f973c-163">Чтобы получить их, обратитесь в [службу поддержки клиентов ThirdLight](https://www.thirdlight.com/support).</span><span class="sxs-lookup"><span data-stu-id="f973c-163">Contact [ThirdLight Client support team](https://www.thirdlight.com/support) to get these values.</span></span> 
 
4. <span data-ttu-id="f973c-164">В разделе **Сертификат подписи SAML** щелкните **XML метаданных** и сохраните XML-файл на компьютере.</span><span class="sxs-lookup"><span data-stu-id="f973c-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the XML file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_certificate.png) 

5. <span data-ttu-id="f973c-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="f973c-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-thirdlight-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f973c-168">В другом окне веб-браузера войдите на свой корпоративный веб-сайт ThirdLight в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="f973c-168">In a different web browser window, log in to your ThirdLight company site as an administrator.</span></span>

7. <span data-ttu-id="f973c-169">Выберите **Configuration (Конфигурация) \> System Administration (Системное администрирование)**, а затем щелкните **SAML2**.</span><span class="sxs-lookup"><span data-stu-id="f973c-169">Go to **Configuration \> System Administration**, and then click **SAML2**.</span></span>
   
    <span data-ttu-id="f973c-170">![Администрирование системы](./media/active-directory-saas-thirdlight-tutorial/ic805843.png "Администрирование системы")</span><span class="sxs-lookup"><span data-stu-id="f973c-170">![System Administration](./media/active-directory-saas-thirdlight-tutorial/ic805843.png "System Administration")</span></span>

8. <span data-ttu-id="f973c-171">В разделе конфигурации SAML2 выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="f973c-171">In the SAML2 configuration section, perform the following steps:</span></span>
   
    <span data-ttu-id="f973c-172">![Единый вход SAML](./media/active-directory-saas-thirdlight-tutorial/ic805844.png "Единый вход SAML")</span><span class="sxs-lookup"><span data-stu-id="f973c-172">![SAML Single Sign-On](./media/active-directory-saas-thirdlight-tutorial/ic805844.png "SAML Single Sign-On")</span></span>   

     <span data-ttu-id="f973c-173">а.</span><span class="sxs-lookup"><span data-stu-id="f973c-173">a.</span></span> <span data-ttu-id="f973c-174">Выберите параметр **Разрешить единый вход SAML2**.</span><span class="sxs-lookup"><span data-stu-id="f973c-174">Select **Enable SAML2 Single Sign-On**.</span></span>
 
     <span data-ttu-id="f973c-175">b.</span><span class="sxs-lookup"><span data-stu-id="f973c-175">b.</span></span> <span data-ttu-id="f973c-176">В качестве **источника для метаданных IdP** выберите **Load IdP Metadata from XML** (Загрузить метаданные IdP из XML).</span><span class="sxs-lookup"><span data-stu-id="f973c-176">As **Source for IdP Metadata**, select **Load IdP Metadata from XML**.</span></span>
 
     <span data-ttu-id="f973c-177">c.</span><span class="sxs-lookup"><span data-stu-id="f973c-177">c.</span></span> <span data-ttu-id="f973c-178">Откройте скачанный файл метаданных, скопируйте его содержимое и вставьте его в текстовое поле **XML с метаданными IdP** .</span><span class="sxs-lookup"><span data-stu-id="f973c-178">Open the downloaded metadata file, copy the content, and then paste it into the **IdP Metadata XML** textbox.</span></span> 
     
     <span data-ttu-id="f973c-179">d.</span><span class="sxs-lookup"><span data-stu-id="f973c-179">d.</span></span> <span data-ttu-id="f973c-180">Щелкните **Сохранить параметры SAML2**.</span><span class="sxs-lookup"><span data-stu-id="f973c-180">Click **Save SAML2 settings**.</span></span>

> [!TIP]
> <span data-ttu-id="f973c-181">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="f973c-181">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f973c-182">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="f973c-182">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f973c-183">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="f973c-183">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f973c-184">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="f973c-184">Creating an Azure AD test user</span></span>
<span data-ttu-id="f973c-185">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f973c-185">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="f973c-187">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="f973c-187">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f973c-188">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f973c-188">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-thirdlight-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f973c-190">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="f973c-190">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-thirdlight-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f973c-192">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="f973c-192">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-thirdlight-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f973c-194">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="f973c-194">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-thirdlight-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f973c-196">а.</span><span class="sxs-lookup"><span data-stu-id="f973c-196">a.</span></span> <span data-ttu-id="f973c-197">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f973c-197">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f973c-198">b.</span><span class="sxs-lookup"><span data-stu-id="f973c-198">b.</span></span> <span data-ttu-id="f973c-199">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f973c-199">In the **User name** textbox, type the **email address** of Britta Simon.</span></span>

    <span data-ttu-id="f973c-200">c.</span><span class="sxs-lookup"><span data-stu-id="f973c-200">c.</span></span> <span data-ttu-id="f973c-201">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="f973c-201">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f973c-202">d.</span><span class="sxs-lookup"><span data-stu-id="f973c-202">d.</span></span> <span data-ttu-id="f973c-203">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="f973c-203">Click **Create**.</span></span>
 
### <a name="creating-a-thirdlight-test-user"></a><span data-ttu-id="f973c-204">Создание тестового пользователя ThirdLight</span><span class="sxs-lookup"><span data-stu-id="f973c-204">Creating a ThirdLight test user</span></span>

<span data-ttu-id="f973c-205">Чтобы пользователи Azure AD могли выполнять вход в систему ThirdLight, они должны быть подготовлены для нее.</span><span class="sxs-lookup"><span data-stu-id="f973c-205">To enable Azure AD users to log in to ThirdLight, they must be provisioned into ThirdLight.</span></span>  
<span data-ttu-id="f973c-206">В случае с ThirdLight подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="f973c-206">In the case of ThirdLight, provisioning is a manual task.</span></span>

<span data-ttu-id="f973c-207">**Чтобы подготовить учетную запись пользователя, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="f973c-207">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="f973c-208">Выполните вход на веб-сайт **ThirdLight** вашей компании в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="f973c-208">Log in to your **ThirdLight** company site as an administrator.</span></span>

2. <span data-ttu-id="f973c-209">Перейдите на вкладку **Пользователи** .</span><span class="sxs-lookup"><span data-stu-id="f973c-209">Go to **Users** tab.</span></span>

3. <span data-ttu-id="f973c-210">Выберите пункт **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="f973c-210">Select **Users and Groups**.</span></span>

4. <span data-ttu-id="f973c-211">Щелкните **Добавить пользователя** .</span><span class="sxs-lookup"><span data-stu-id="f973c-211">Click **Add new User** button.</span></span>

5. <span data-ttu-id="f973c-212">Введите **имя пользователя, имя или описание, адрес электронной почты, выберите предустановку или группу новых участников** для действующей учетной записи AAD, которую необходимо подготовить.</span><span class="sxs-lookup"><span data-stu-id="f973c-212">Enter **the Username, Name or Description, Email, Choose a Preset or Group of New Members** of a valid AAD account you want to provision.</span></span>

6. <span data-ttu-id="f973c-213">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="f973c-213">Click **Create**.</span></span>

>[!NOTE]
><span data-ttu-id="f973c-214">Вы можете использовать любые другие инструменты создания учетных записей пользователя Thirdlight или API-интерфейсы, предоставляемые Thirdlight для подготовки учетных записей пользователей AAD.</span><span class="sxs-lookup"><span data-stu-id="f973c-214">You can use any other Thirdlight user account creation tools or APIs provided by Thirdlight to provision AAD user accounts.</span></span> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f973c-215">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="f973c-215">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f973c-216">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure путем предоставления доступа к ThirdLight.</span><span class="sxs-lookup"><span data-stu-id="f973c-216">In this section, you enable Britta Simon to use Azure single sign-on by granting access to ThirdLight.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="f973c-218">**Чтобы назначить пользователя Britta Simon в ThirdLight, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="f973c-218">**To assign Britta Simon to ThirdLight, perform the following steps:**</span></span>

1. <span data-ttu-id="f973c-219">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="f973c-219">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="f973c-221">В списке приложений выберите **ThirdLight**.</span><span class="sxs-lookup"><span data-stu-id="f973c-221">In the applications list, select **ThirdLight**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_app.png) 

3. <span data-ttu-id="f973c-223">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="f973c-223">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="f973c-225">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="f973c-225">Click **Add** button.</span></span> <span data-ttu-id="f973c-226">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="f973c-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="f973c-228">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="f973c-228">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f973c-229">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="f973c-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f973c-230">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="f973c-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f973c-231">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="f973c-231">Testing single sign-on</span></span>

<span data-ttu-id="f973c-232">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="f973c-232">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="f973c-233">Щелкнув элемент ThirdLight на панели доступа, вы автоматически войдете в приложение ThirdLight.</span><span class="sxs-lookup"><span data-stu-id="f973c-233">When you click the ThirdLight tile in the Access Panel, you should get automatically signed-on to your ThirdLight application.</span></span>
<span data-ttu-id="f973c-234">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f973c-234">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="f973c-235">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="f973c-235">Additional resources</span></span>

* [<span data-ttu-id="f973c-236">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f973c-236">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f973c-237">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f973c-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_203.png

