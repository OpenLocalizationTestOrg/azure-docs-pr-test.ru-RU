---
title: "Учебник. Интеграция Azure Active Directory с Huddle | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и Huddle."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8389ba4c-f5f8-4ede-b2f4-32eae844ceb0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 59d4019545d39ec76bf401696338140f430630c9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-huddle"></a><span data-ttu-id="8e6f7-103">Руководство. Интеграция Azure Active Directory с Huddle</span><span class="sxs-lookup"><span data-stu-id="8e6f7-103">Tutorial: Azure Active Directory integration with Huddle</span></span>

<span data-ttu-id="8e6f7-104">В этом руководстве описано, как интегрировать Huddle с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8e6f7-104">In this tutorial, you learn how to integrate Huddle with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="8e6f7-105">Интеграция Azure AD с приложением Huddle обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="8e6f7-105">Integrating Huddle with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="8e6f7-106">С помощью Azure AD вы можете контролировать доступ к Huddle.</span><span class="sxs-lookup"><span data-stu-id="8e6f7-106">You can control in Azure AD who has access to Huddle</span></span>
- <span data-ttu-id="8e6f7-107">Вы можете включить автоматический вход пользователей в Huddle (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8e6f7-107">You can enable your users to automatically get signed-on to Huddle (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="8e6f7-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="8e6f7-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="8e6f7-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="8e6f7-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8e6f7-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="8e6f7-110">Prerequisites</span></span>

<span data-ttu-id="8e6f7-111">Чтобы настроить интеграцию Azure AD с Huddle, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="8e6f7-111">To configure Azure AD integration with Huddle, you need the following items:</span></span>

- <span data-ttu-id="8e6f7-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="8e6f7-112">An Azure AD subscription</span></span>
- <span data-ttu-id="8e6f7-113">Подписка с поддержкой единого входа Huddle</span><span class="sxs-lookup"><span data-stu-id="8e6f7-113">A Huddle single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="8e6f7-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="8e6f7-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="8e6f7-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="8e6f7-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="8e6f7-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="8e6f7-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="8e6f7-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8e6f7-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="8e6f7-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="8e6f7-118">Scenario description</span></span>

<span data-ttu-id="8e6f7-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="8e6f7-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="8e6f7-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="8e6f7-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="8e6f7-121">Добавление Huddle из коллекции.</span><span class="sxs-lookup"><span data-stu-id="8e6f7-121">Adding Huddle from the gallery</span></span>
2. <span data-ttu-id="8e6f7-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="8e6f7-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-huddle-from-the-gallery"></a><span data-ttu-id="8e6f7-123">Добавление Huddle из коллекции</span><span class="sxs-lookup"><span data-stu-id="8e6f7-123">Adding Huddle from the gallery</span></span>
<span data-ttu-id="8e6f7-124">Чтобы настроить интеграцию Huddle с Azure AD, необходимо добавить Huddle из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="8e6f7-124">To configure the integration of Huddle into Azure AD, you need to add Huddle from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="8e6f7-125">**Чтобы добавить Huddle из коллекции, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="8e6f7-125">**To add Huddle from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="8e6f7-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8e6f7-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="8e6f7-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="8e6f7-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="8e6f7-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="8e6f7-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="8e6f7-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="8e6f7-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="8e6f7-133">В поле поиска введите **Huddle**.</span><span class="sxs-lookup"><span data-stu-id="8e6f7-133">In the search box, type **Huddle**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_search.png)

5. <span data-ttu-id="8e6f7-135">На панели результатов выберите **Huddle** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="8e6f7-135">In the results panel, select **Huddle**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="8e6f7-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="8e6f7-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="8e6f7-138">В этом разделе описана настройка и проверка единого входа Azure AD с Huddle с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8e6f7-138">In this section, you configure and test Azure AD single sign-on with Huddle based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="8e6f7-139">Чтобы единый вход работал, Azure AD необходимо знать, какой пользователь в Huddle соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8e6f7-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Huddle is to a user in Azure AD.</span></span> <span data-ttu-id="8e6f7-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Huddle.</span><span class="sxs-lookup"><span data-stu-id="8e6f7-140">In other words, a link relationship between an Azure AD user and the related user in Huddle needs to be established.</span></span>

<span data-ttu-id="8e6f7-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Huddle.</span><span class="sxs-lookup"><span data-stu-id="8e6f7-141">In Huddle, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="8e6f7-142">Чтобы настроить и проверить единый вход Azure AD в Huddle, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="8e6f7-142">To configure and test Azure AD single sign-on with Huddle, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="8e6f7-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="8e6f7-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>

2. <span data-ttu-id="8e6f7-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8e6f7-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>

3. <span data-ttu-id="8e6f7-145">**[Создание тестового пользователя Huddle](#creating-a-huddle-test-user)** требуется для создания в Huddle пользователя Britta Simon, связанного с представлением этого же пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8e6f7-145">**[Creating a Huddle test user](#creating-a-huddle-test-user)** - to have a counterpart of Britta Simon in Huddle that is linked to the Azure AD representation of user.</span></span>

4. <span data-ttu-id="8e6f7-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8e6f7-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>

5. <span data-ttu-id="8e6f7-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="8e6f7-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="8e6f7-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="8e6f7-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="8e6f7-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Huddle.</span><span class="sxs-lookup"><span data-stu-id="8e6f7-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Huddle application.</span></span>

<span data-ttu-id="8e6f7-150">**Чтобы настроить единый вход Azure AD в Huddle, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="8e6f7-150">**To configure Azure AD single sign-on with Huddle, perform the following steps:**</span></span>

1. <span data-ttu-id="8e6f7-151">На портале Azure на странице интеграции с приложением **Huddle** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="8e6f7-151">In the Azure portal, on the **Huddle** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="8e6f7-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="8e6f7-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_samlbase.png)

3. <span data-ttu-id="8e6f7-155">В разделе **Домены и URL-адреса приложения Huddle** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="8e6f7-155">On the **Huddle Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_url.png)

    <span data-ttu-id="8e6f7-157">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `http://<company name>.huddle.com`</span><span class="sxs-lookup"><span data-stu-id="8e6f7-157">In the **Sign-on URL** textbox, type a URL using the following pattern: `http://<company name>.huddle.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="8e6f7-158">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="8e6f7-158">This value is not real.</span></span> <span data-ttu-id="8e6f7-159">Вместо него необходимо указать фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="8e6f7-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="8e6f7-160">Для получения данного значения обратитесь в [службу поддержки клиентов Huddle](https://huddle.zendesk.com).</span><span class="sxs-lookup"><span data-stu-id="8e6f7-160">Contact [Huddle Client support team](https://huddle.zendesk.com) to get this value.</span></span> 

4. <span data-ttu-id="8e6f7-161">В разделе **Сертификат подписи SAML** щелкните **Сертификат (Base64)**, а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="8e6f7-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_certificate.png) 

5. <span data-ttu-id="8e6f7-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="8e6f7-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-huddle-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="8e6f7-165">В разделе **Настройка Huddle** щелкните **Настроить Huddle**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="8e6f7-165">On the **Huddle Configuration** section, click **Configure Huddle** to open **Configure sign-on** window.</span></span> <span data-ttu-id="8e6f7-166">Скопируйте **идентификатор сущности SAML и URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="8e6f7-166">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span> 

    ![Настройка единого входа](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_configure.png) 
    
7. <span data-ttu-id="8e6f7-168">Чтобы настроить единый вход на стороне Huddle, вам необходимо отправить скачанный файл **сертификата**, **URL-адрес службы единого входа SAML** и **идентификатор сущности SAML** в [службу поддержки клиентов Huddle](https://huddle.zendesk.com).</span><span class="sxs-lookup"><span data-stu-id="8e6f7-168">To configure single sign-on on Huddle side, you need to send the downloaded  **Certificate**, **SAML Single Sign-On Service URL**, and **SAML Entity ID** to [Huddle Client support team](https://huddle.zendesk.com).</span></span> <span data-ttu-id="8e6f7-169">Специалисты службы поддержки настроят подключение единого входа SAML на обеих сторонах.</span><span class="sxs-lookup"><span data-stu-id="8e6f7-169">They set this setting to have the SAML SSO connection set properly on both sides.</span></span>  
   
    >[!NOTE]
    > <span data-ttu-id="8e6f7-170">Единый вход должна включить служба поддержки Huddle.</span><span class="sxs-lookup"><span data-stu-id="8e6f7-170">Single sign-on needs to be enabled by the Huddle support team.</span></span> <span data-ttu-id="8e6f7-171">Сразу же после завершения настройки вы получите уведомление.</span><span class="sxs-lookup"><span data-stu-id="8e6f7-171">You get a notification when the configuration has been completed.</span></span> 
    > 

> [!TIP]
> <span data-ttu-id="8e6f7-172">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="8e6f7-172">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="8e6f7-173">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="8e6f7-173">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="8e6f7-174">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="8e6f7-174">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 
   
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="8e6f7-175">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="8e6f7-175">Creating an Azure AD test user</span></span>

<span data-ttu-id="8e6f7-176">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="8e6f7-176">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="8e6f7-178">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="8e6f7-178">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="8e6f7-179">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8e6f7-179">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-huddle-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="8e6f7-181">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="8e6f7-181">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-huddle-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="8e6f7-183">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="8e6f7-183">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-huddle-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="8e6f7-185">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="8e6f7-185">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-huddle-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="8e6f7-187">а.</span><span class="sxs-lookup"><span data-stu-id="8e6f7-187">a.</span></span> <span data-ttu-id="8e6f7-188">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="8e6f7-188">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="8e6f7-189">b.</span><span class="sxs-lookup"><span data-stu-id="8e6f7-189">b.</span></span> <span data-ttu-id="8e6f7-190">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="8e6f7-190">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="8e6f7-191">c.</span><span class="sxs-lookup"><span data-stu-id="8e6f7-191">c.</span></span> <span data-ttu-id="8e6f7-192">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="8e6f7-192">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="8e6f7-193">d.</span><span class="sxs-lookup"><span data-stu-id="8e6f7-193">d.</span></span> <span data-ttu-id="8e6f7-194">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="8e6f7-194">Click **Create**.</span></span>
 
### <a name="creating-a-huddle-test-user"></a><span data-ttu-id="8e6f7-195">Создание тестового пользователя Huddle</span><span class="sxs-lookup"><span data-stu-id="8e6f7-195">Creating a Huddle test user</span></span>

<span data-ttu-id="8e6f7-196">Чтобы пользователи Azure AD могли выполнить вход в Huddle, они должны быть подготовлены для Huddle.</span><span class="sxs-lookup"><span data-stu-id="8e6f7-196">To enable Azure AD users to log in to Huddle, they must be provisioned into Huddle.</span></span> <span data-ttu-id="8e6f7-197">В случае с Huddle подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="8e6f7-197">In the case of Huddle, provisioning is a manual task.</span></span>

<span data-ttu-id="8e6f7-198">**Чтобы настроить подготовку учетных записей пользователей, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="8e6f7-198">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="8e6f7-199">Выполните вход на веб-сайт компании **Huddle** в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="8e6f7-199">Log in to your **Huddle** company site as administrator.</span></span>
2. <span data-ttu-id="8e6f7-200">Нажмите **Рабочая область**.</span><span class="sxs-lookup"><span data-stu-id="8e6f7-200">Click **Workspace**.</span></span>
3. <span data-ttu-id="8e6f7-201">Щелкните **People \> Invite People** (Пользователи > Пригласить пользователей).</span><span class="sxs-lookup"><span data-stu-id="8e6f7-201">Click **People \> Invite People**.</span></span>
   
   <span data-ttu-id="8e6f7-202">![Люди](./media/active-directory-saas-huddle-tutorial/IC787838.png "Люди")</span><span class="sxs-lookup"><span data-stu-id="8e6f7-202">![People](./media/active-directory-saas-huddle-tutorial/IC787838.png "People")</span></span>

4. <span data-ttu-id="8e6f7-203">В разделе **Создание нового приглашения** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="8e6f7-203">In the **Create a new invitation** section, perform the following steps:</span></span>
   
   <span data-ttu-id="8e6f7-204">![Создание приглашения](./media/active-directory-saas-huddle-tutorial/IC787839.png "Создание приглашения")</span><span class="sxs-lookup"><span data-stu-id="8e6f7-204">![New Invitation](./media/active-directory-saas-huddle-tutorial/IC787839.png "New Invitation")</span></span>
   
   <span data-ttu-id="8e6f7-205">а.</span><span class="sxs-lookup"><span data-stu-id="8e6f7-205">a.</span></span> <span data-ttu-id="8e6f7-206">В списке **Choose a team to invite people to join** (Выберите группу, в которую следует пригласить пользователей) выберите **группу**.</span><span class="sxs-lookup"><span data-stu-id="8e6f7-206">In the **Choose a team to invite people to join** list, select **team**.</span></span>

   <span data-ttu-id="8e6f7-207">b.</span><span class="sxs-lookup"><span data-stu-id="8e6f7-207">b.</span></span> <span data-ttu-id="8e6f7-208">Введите **адрес электронной почты** действительной учетной записи Azure AD, которую вы хотите подготовить, в текстовом поле **Enter email address for people you'd like to invite** (Введите адреса электронной почты пользователей, которых вы хотите пригласить).</span><span class="sxs-lookup"><span data-stu-id="8e6f7-208">Type the **Email Address** of a valid Azure AD account you want to provision in to **Enter email address for people you'd like to invite** textbox.</span></span>

   <span data-ttu-id="8e6f7-209">c.</span><span class="sxs-lookup"><span data-stu-id="8e6f7-209">c.</span></span> <span data-ttu-id="8e6f7-210">Нажмите кнопку **Пригласить**.</span><span class="sxs-lookup"><span data-stu-id="8e6f7-210">Click **Invite**.</span></span>   
   
    >[!NOTE]
    > <span data-ttu-id="8e6f7-211">Владелец учетной записи Azure AD получит по электронной почте сообщение со ссылкой для активации учетной записи.</span><span class="sxs-lookup"><span data-stu-id="8e6f7-211">The Azure AD account holder will receive an email including a link to confirm the account before it becomes active.</span></span> 
    > 

>[!NOTE]
><span data-ttu-id="8e6f7-212">Вы можете использовать любые другие средства создания учетной записи пользователя Huddle или API, предоставляемые Huddle, для подготовки учетных записей пользователя Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8e6f7-212">You can use any other Huddle user account creation tools or APIs provided by Huddle to provision Azure AD user accounts.</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="8e6f7-213">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="8e6f7-213">Assigning the Azure AD test user</span></span>

<span data-ttu-id="8e6f7-214">В этом разделе описано, как предоставить пользователю Britta Simon доступ к Huddle, чтобы он мог использовать единый вход Azure.</span><span class="sxs-lookup"><span data-stu-id="8e6f7-214">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Huddle.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="8e6f7-216">**Чтобы назначить пользователя Britta Simon в приложении Huddle, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="8e6f7-216">**To assign Britta Simon to Huddle, perform the following steps:**</span></span>

1. <span data-ttu-id="8e6f7-217">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="8e6f7-217">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="8e6f7-219">В списке приложений выберите **Huddle**.</span><span class="sxs-lookup"><span data-stu-id="8e6f7-219">In the applications list, select **Huddle**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_app.png) 

3. <span data-ttu-id="8e6f7-221">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="8e6f7-221">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="8e6f7-223">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="8e6f7-223">Click **Add** button.</span></span> <span data-ttu-id="8e6f7-224">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="8e6f7-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="8e6f7-226">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="8e6f7-226">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="8e6f7-227">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="8e6f7-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="8e6f7-228">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="8e6f7-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="8e6f7-229">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="8e6f7-229">Testing single sign-on</span></span>

<span data-ttu-id="8e6f7-230">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="8e6f7-230">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="8e6f7-231">Щелкнув элемент Huddle на панели доступа, вы автоматически войдете в приложение Huddle.</span><span class="sxs-lookup"><span data-stu-id="8e6f7-231">When you click the Huddle tile in the Access Panel, you should get automatically login page of Huddle application.</span></span>
<span data-ttu-id="8e6f7-232">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8e6f7-232">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8e6f7-233">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="8e6f7-233">Additional resources</span></span>

* [<span data-ttu-id="8e6f7-234">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8e6f7-234">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="8e6f7-235">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="8e6f7-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_04.png
[100]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_100.png
[200]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_203.png
