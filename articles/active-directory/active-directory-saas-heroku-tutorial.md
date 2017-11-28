---
title: "Учебник. Интеграция Azure Active Directory с Heroku | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в Heroku."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d7d72ec6-4a60-4524-8634-26d8fbbcc833
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: d30605e4757b484f327a784b73f939b62ef59373
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-heroku"></a><span data-ttu-id="05dea-103">Учебник. Интеграция Azure Active Directory с Heroku</span><span class="sxs-lookup"><span data-stu-id="05dea-103">Tutorial: Azure Active Directory integration with Heroku</span></span>

<span data-ttu-id="05dea-104">В этом учебнике описано, как интегрировать Heroku с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="05dea-104">In this tutorial, you learn how to integrate Heroku with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="05dea-105">Интеграция Heroku с Azure AD дает приведенные далее преимущества:</span><span class="sxs-lookup"><span data-stu-id="05dea-105">Integrating Heroku with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="05dea-106">С помощью Azure AD вы можете контролировать доступ к Heroku.</span><span class="sxs-lookup"><span data-stu-id="05dea-106">You can control in Azure AD who has access to Heroku</span></span>
- <span data-ttu-id="05dea-107">Вы можете включить автоматический вход пользователей в Heroku (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="05dea-107">You can enable your users to automatically get signed-on to Heroku (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="05dea-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="05dea-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="05dea-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="05dea-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="05dea-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="05dea-110">Prerequisites</span></span>

<span data-ttu-id="05dea-111">Чтобы настроить интеграцию Azure AD с Heroku, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="05dea-111">To configure Azure AD integration with Heroku, you need the following items:</span></span>

- <span data-ttu-id="05dea-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="05dea-112">An Azure AD subscription</span></span>
- <span data-ttu-id="05dea-113">подписка Heroku с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="05dea-113">A Heroku single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="05dea-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="05dea-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="05dea-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="05dea-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="05dea-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="05dea-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="05dea-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="05dea-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="05dea-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="05dea-118">Scenario description</span></span>
<span data-ttu-id="05dea-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="05dea-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="05dea-120">Сценарий, описанный в этом руководстве, состоит из двух стандартных блоков.</span><span class="sxs-lookup"><span data-stu-id="05dea-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="05dea-121">Добавление Heroku из коллекции</span><span class="sxs-lookup"><span data-stu-id="05dea-121">Adding Heroku from the gallery</span></span>
2. <span data-ttu-id="05dea-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="05dea-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-heroku-from-the-gallery"></a><span data-ttu-id="05dea-123">Добавление Heroku из коллекции</span><span class="sxs-lookup"><span data-stu-id="05dea-123">Adding Heroku from the gallery</span></span>
<span data-ttu-id="05dea-124">Чтобы настроить интеграцию Heroku с Azure AD, необходимо добавить Heroku из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="05dea-124">To configure the integration of Heroku into Azure AD, you need to add Heroku from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="05dea-125">**Чтобы добавить Heroku из коллекции, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="05dea-125">**To add Heroku from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="05dea-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="05dea-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="05dea-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="05dea-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="05dea-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="05dea-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="05dea-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="05dea-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="05dea-133">В поле поиска введите **Heroku**.</span><span class="sxs-lookup"><span data-stu-id="05dea-133">In the search box, type **Heroku**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_search.png)

5. <span data-ttu-id="05dea-135">На панели результатов выберите **Heroku** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="05dea-135">In the results panel, select **Heroku**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="05dea-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="05dea-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="05dea-138">В этом разделе описана настройка и проверка единого входа Azure AD в Heroku с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="05dea-138">In this section, you configure and test Azure AD single sign-on with Heroku based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="05dea-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Heroku соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="05dea-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Heroku is to a user in Azure AD.</span></span> <span data-ttu-id="05dea-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Heroku.</span><span class="sxs-lookup"><span data-stu-id="05dea-140">In other words, a link relationship between an Azure AD user and the related user in Heroku needs to be established.</span></span>

<span data-ttu-id="05dea-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Heroku.</span><span class="sxs-lookup"><span data-stu-id="05dea-141">In Heroku, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="05dea-142">Чтобы настроить и проверить единый вход Azure AD в Heroku, вам потребуется выполнить действия в указанных далее стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="05dea-142">To configure and test Azure AD single sign-on with Heroku, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="05dea-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="05dea-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="05dea-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="05dea-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="05dea-145">**[Создание тестового пользователя Heroku](#creating-a-heroku-test-user)** требуется для создания в Heroku пользователя Britta Simon, связанного с представлением этого же пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="05dea-145">**[Creating a Heroku test user](#creating-a-heroku-test-user)** - to have a counterpart of Britta Simon in Heroku that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="05dea-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="05dea-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="05dea-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="05dea-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="05dea-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="05dea-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="05dea-149">В данном разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Heroku.</span><span class="sxs-lookup"><span data-stu-id="05dea-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Heroku application.</span></span>

<span data-ttu-id="05dea-150">**Чтобы настроить единый вход Azure AD в Heroku, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="05dea-150">**To configure Azure AD single sign-on with Heroku, perform the following steps:**</span></span>

1. <span data-ttu-id="05dea-151">На портале Azure на странице интеграции с приложением **Heroku** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="05dea-151">In the Azure portal, on the **Heroku** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="05dea-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="05dea-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_samlbase.png)

3. <span data-ttu-id="05dea-155">В разделе **Домены и URL-адреса приложения Heroku** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="05dea-155">On the **Heroku Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_url.png)

    <span data-ttu-id="05dea-157">а.</span><span class="sxs-lookup"><span data-stu-id="05dea-157">a.</span></span> <span data-ttu-id="05dea-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="05dea-158">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span>    
    `https://sso.heroku.com/saml/<company-name>/init`

    <span data-ttu-id="05dea-159">b.</span><span class="sxs-lookup"><span data-stu-id="05dea-159">b.</span></span> <span data-ttu-id="05dea-160">В текстовом поле **Identifier URL** (URL-адрес идентификатора) введите URL-адрес в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="05dea-160">In the **Identifier URL** textbox, type a URL using the following pattern:</span></span>            
    `https://sso.heroku.com/saml/<company-name>`

    > [!NOTE]
    ><span data-ttu-id="05dea-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="05dea-161">These values are not real.</span></span> <span data-ttu-id="05dea-162">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="05dea-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="05dea-163">Вы получаете эти значения от команды Heroku. Как это сделать, описано в последующих разделах этой статьи.</span><span class="sxs-lookup"><span data-stu-id="05dea-163">You get these values from Heroku team, which is described in later sections of this article.</span></span> 
        
4. <span data-ttu-id="05dea-164">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="05dea-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_certificate.png) 

5. <span data-ttu-id="05dea-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="05dea-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-heroku-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="05dea-168">Чтобы включить единый вход в Heroku, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="05dea-168">To enable SSO in Heroku, perform the following steps:</span></span>
   
    <span data-ttu-id="05dea-169">а.</span><span class="sxs-lookup"><span data-stu-id="05dea-169">a.</span></span> <span data-ttu-id="05dea-170">Войдите в учетную запись Heroku с помощью прав администратора.</span><span class="sxs-lookup"><span data-stu-id="05dea-170">Log in to the Heroku account as an administrator.</span></span>

    <span data-ttu-id="05dea-171">b.</span><span class="sxs-lookup"><span data-stu-id="05dea-171">b.</span></span> <span data-ttu-id="05dea-172">Перейдите на вкладку **Параметры** .</span><span class="sxs-lookup"><span data-stu-id="05dea-172">Click the **Settings** tab.</span></span>

    <span data-ttu-id="05dea-173">c.</span><span class="sxs-lookup"><span data-stu-id="05dea-173">c.</span></span> <span data-ttu-id="05dea-174">На странице **Single Sign On Page** (Страница единого входа) щелкните **Upload Metadata** (Передать метаданные).</span><span class="sxs-lookup"><span data-stu-id="05dea-174">On the **Single Sign On Page**, click **Upload Metadata**.</span></span>

    <span data-ttu-id="05dea-175">г)</span><span class="sxs-lookup"><span data-stu-id="05dea-175">d.</span></span> <span data-ttu-id="05dea-176">Отправьте файл метаданных, который вы скачали с портала Azure.</span><span class="sxs-lookup"><span data-stu-id="05dea-176">Upload the metadata file, which you have downloaded from the Azure portal.</span></span>

    <span data-ttu-id="05dea-177">д.</span><span class="sxs-lookup"><span data-stu-id="05dea-177">e.</span></span> <span data-ttu-id="05dea-178">После успешной установки администраторы увидят диалоговое окно подтверждения. Для конечных пользователей будет отображен URL-адрес единого входа.</span><span class="sxs-lookup"><span data-stu-id="05dea-178">When the setup is successful, administrators see a confirmation dialog and the URL of the SSO Login for end users is displayed.</span></span> 

    <span data-ttu-id="05dea-179">f.</span><span class="sxs-lookup"><span data-stu-id="05dea-179">f.</span></span> <span data-ttu-id="05dea-180">Скопируйте **URL-адрес входа Heroku** и **идентификатор сущности Heroku**, а затем вернитесь в раздел **Домены и URL-адреса приложения Heroku** на портале Azure и вставьте эти значения в текстовые поля **URL-адреса входа** и **Идентификатор** соответственно.</span><span class="sxs-lookup"><span data-stu-id="05dea-180">Copy the **Heroku Login URL** and **Heroku Entity ID** values and go back to **Heroku Domain and URLs** section in Azure portal and paste these values into the **Sign-On Url** and **Identifier** textboxes respectively.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_52.png) 
    
8. <span data-ttu-id="05dea-182">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="05dea-182">Click **Next**.</span></span>

> [!TIP]
> <span data-ttu-id="05dea-183">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="05dea-183">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="05dea-184">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="05dea-184">After adding this app from the **Active Directory Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="05dea-185">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="05dea-185">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="05dea-186">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="05dea-186">Creating an Azure AD test user</span></span>

<span data-ttu-id="05dea-187">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="05dea-187">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="05dea-189">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="05dea-189">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="05dea-190">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="05dea-190">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-heroku-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="05dea-192">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="05dea-192">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-heroku-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="05dea-194">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="05dea-194">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-heroku-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="05dea-196">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="05dea-196">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-heroku-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="05dea-198">а.</span><span class="sxs-lookup"><span data-stu-id="05dea-198">a.</span></span> <span data-ttu-id="05dea-199">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="05dea-199">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="05dea-200">b.</span><span class="sxs-lookup"><span data-stu-id="05dea-200">b.</span></span> <span data-ttu-id="05dea-201">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="05dea-201">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="05dea-202">c.</span><span class="sxs-lookup"><span data-stu-id="05dea-202">c.</span></span> <span data-ttu-id="05dea-203">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="05dea-203">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="05dea-204">d.</span><span class="sxs-lookup"><span data-stu-id="05dea-204">d.</span></span> <span data-ttu-id="05dea-205">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="05dea-205">Click **Create**.</span></span>
 
### <a name="creating-a-heroku-test-user"></a><span data-ttu-id="05dea-206">Создание тестового пользователя Heroku</span><span class="sxs-lookup"><span data-stu-id="05dea-206">Creating a Heroku test user</span></span>

<span data-ttu-id="05dea-207">В этом разделе описано, как создать пользователя Britta Simon в приложении Heroku.</span><span class="sxs-lookup"><span data-stu-id="05dea-207">In this section, you create a user called Britta Simon in Heroku.</span></span> <span data-ttu-id="05dea-208">Приложение Heroku поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="05dea-208">Heroku supports just-in-time provisioning, which is enabled by default.</span></span>

<span data-ttu-id="05dea-209">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="05dea-209">There is no action item for you in this section.</span></span> <span data-ttu-id="05dea-210">Новый пользователь, если он еще не существует, создается при доступе к Heroku.</span><span class="sxs-lookup"><span data-stu-id="05dea-210">A new user is created when accessing Heroku if the user doesn't exist yet.</span></span> <span data-ttu-id="05dea-211">После подготовки учетной записи конечный пользователь получает проверочное сообщение электронной почты, в котором ему нужно щелкнуть ссылку подтверждения.</span><span class="sxs-lookup"><span data-stu-id="05dea-211">After the account is provisioned, the end user receives a verification email and needs to click the acknowledgement link.</span></span>

>[!NOTE]
><span data-ttu-id="05dea-212">Если вам нужно вручную создать пользователя, необходимо обратиться в [службу поддержки клиентов Heroku](https://www.heroku.com/support).</span><span class="sxs-lookup"><span data-stu-id="05dea-212">If you need to create a user manually, you need to contact the [Heroku Client support team](https://www.heroku.com/support).</span></span>
>  

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="05dea-213">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="05dea-213">Assigning the Azure AD test user</span></span>

<span data-ttu-id="05dea-214">В этом разделе описано, как предоставить пользователю Britta Simon доступ к Heroku, чтобы он мог использовать единый вход Azure.</span><span class="sxs-lookup"><span data-stu-id="05dea-214">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Heroku.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="05dea-216">**Чтобы назначить пользователя Britta Simon в Heroku, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="05dea-216">**To assign Britta Simon to Heroku, perform the following steps:**</span></span>

1. <span data-ttu-id="05dea-217">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="05dea-217">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="05dea-219">В списке приложений выберите **Heroku**.</span><span class="sxs-lookup"><span data-stu-id="05dea-219">In the applications list, select **Heroku**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-heroku-tutorial/tutorial_heroku_app.png) 

3. <span data-ttu-id="05dea-221">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="05dea-221">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="05dea-223">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="05dea-223">Click **Add** button.</span></span> <span data-ttu-id="05dea-224">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="05dea-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="05dea-226">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="05dea-226">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="05dea-227">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="05dea-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="05dea-228">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="05dea-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="05dea-229">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="05dea-229">Testing single sign-on</span></span>

<span data-ttu-id="05dea-230">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="05dea-230">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="05dea-231">Щелкнув элемент Heroku на панели доступа, вы автоматически войдете в приложение Heroku.</span><span class="sxs-lookup"><span data-stu-id="05dea-231">When you click the Heroku tile in the Access Panel, you should get automatically signed-on to your Heroku application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="05dea-232">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="05dea-232">Additional resources</span></span>

* [<span data-ttu-id="05dea-233">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="05dea-233">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="05dea-234">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="05dea-234">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-heroku-tutorial/tutorial_general_203.png
