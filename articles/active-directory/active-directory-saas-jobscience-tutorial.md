---
title: "Учебник. Интеграция Azure Active Directory с Jobscience | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в приложении Jobscience."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 77282dcc-bbe2-4728-953d-adb4ab6a713b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 66bec35a8f17482433dbf02827b90620d1cff378
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jobscience"></a><span data-ttu-id="ae382-103">Руководство. Интеграция Azure Active Directory с Jobscience</span><span class="sxs-lookup"><span data-stu-id="ae382-103">Tutorial: Azure Active Directory integration with Jobscience</span></span>

<span data-ttu-id="ae382-104">В этом руководстве описано, как интегрировать Jobscience с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ae382-104">In this tutorial, you learn how to integrate Jobscience with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ae382-105">Интеграция Azure AD с приложением Jobscience обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="ae382-105">Integrating Jobscience with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ae382-106">С помощью Azure AD вы можете контролировать доступ к Jobscience.</span><span class="sxs-lookup"><span data-stu-id="ae382-106">You can control in Azure AD who has access to Jobscience</span></span>
- <span data-ttu-id="ae382-107">Вы можете включить автоматический вход пользователей в Jobscience (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ae382-107">You can enable your users to automatically get signed-on to Jobscience (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ae382-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="ae382-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ae382-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ae382-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ae382-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ae382-110">Prerequisites</span></span>

<span data-ttu-id="ae382-111">Чтобы настроить интеграцию Azure AD с Jobscience, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="ae382-111">To configure Azure AD integration with Jobscience, you need the following items:</span></span>

- <span data-ttu-id="ae382-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="ae382-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ae382-113">подписка Jobscience с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="ae382-113">A Jobscience single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ae382-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="ae382-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ae382-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="ae382-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ae382-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="ae382-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ae382-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ae382-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ae382-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="ae382-118">Scenario description</span></span>
<span data-ttu-id="ae382-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="ae382-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ae382-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="ae382-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ae382-121">Добавление Jobscience из коллекции.</span><span class="sxs-lookup"><span data-stu-id="ae382-121">Adding Jobscience from the gallery</span></span>
2. <span data-ttu-id="ae382-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae382-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jobscience-from-the-gallery"></a><span data-ttu-id="ae382-123">Добавление Jobscience из коллекции</span><span class="sxs-lookup"><span data-stu-id="ae382-123">Adding Jobscience from the gallery</span></span>
<span data-ttu-id="ae382-124">Чтобы настроить интеграцию Jobscience с Azure AD, необходимо добавить Jobscience из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="ae382-124">To configure the integration of Jobscience into Azure AD, you need to add Jobscience from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ae382-125">**Чтобы добавить Jobscience из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="ae382-125">**To add Jobscience from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ae382-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ae382-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ae382-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="ae382-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ae382-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="ae382-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="ae382-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="ae382-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="ae382-133">В поле поиска введите **Jobscience**.</span><span class="sxs-lookup"><span data-stu-id="ae382-133">In the search box, type **Jobscience**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_search.png)

5. <span data-ttu-id="ae382-135">На панели результатов выберите **Jobscience** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="ae382-135">In the results panel, select **Jobscience**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ae382-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae382-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ae382-138">В этом разделе описана настройка и проверка единого входа Azure AD в Jobscience с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ae382-138">In this section, you configure and test Azure AD single sign-on with Jobscience based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ae382-139">Чтобы единый вход работал, Azure AD необходима информация о том, какой пользователь в Jobscience соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ae382-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Jobscience is to a user in Azure AD.</span></span> <span data-ttu-id="ae382-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Jobscience.</span><span class="sxs-lookup"><span data-stu-id="ae382-140">In other words, a link relationship between an Azure AD user and the related user in Jobscience needs to be established.</span></span>

<span data-ttu-id="ae382-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Jobscience.</span><span class="sxs-lookup"><span data-stu-id="ae382-141">In Jobscience, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="ae382-142">Чтобы настроить и проверить единый вход Azure AD в Jobscience, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="ae382-142">To configure and test Azure AD single sign-on with Jobscience, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ae382-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="ae382-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ae382-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ae382-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ae382-145">**[Создание тестового пользователя Jobscience](#creating-a-jobscience-test-user)** требуется для того, чтобы в Jobscience существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ae382-145">**[Creating a Jobscience test user](#creating-a-jobscience-test-user)** - to have a counterpart of Britta Simon in Jobscience that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="ae382-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ae382-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ae382-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="ae382-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ae382-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae382-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ae382-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Jobscience.</span><span class="sxs-lookup"><span data-stu-id="ae382-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Jobscience application.</span></span>

<span data-ttu-id="ae382-150">**Чтобы настроить единый вход Azure AD в Jobscience, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="ae382-150">**To configure Azure AD single sign-on with Jobscience, perform the following steps:**</span></span>

1. <span data-ttu-id="ae382-151">На портале Azure на странице интеграции с приложением **Jobscience** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="ae382-151">In the Azure portal, on the **Jobscience** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="ae382-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="ae382-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_samlbase.png)

3. <span data-ttu-id="ae382-155">В разделе **Домены и URL-адреса приложения Jobscience** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="ae382-155">On the **Jobscience Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_url.png)

    <span data-ttu-id="ae382-157">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `http://<company name>.my.salesforce.com`.</span><span class="sxs-lookup"><span data-stu-id="ae382-157">In the **Sign-on URL** textbox, type a URL using the following pattern:  `http://<company name>.my.salesforce.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="ae382-158">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="ae382-158">This value is not real.</span></span> <span data-ttu-id="ae382-159">Вместо него необходимо указать фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="ae382-159">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="ae382-160">Данное значение можно получить у [группы поддержки клиентов Jobscience](https://www.jobscience.com/support) или из профиля единого входа, который вы создадите. Это описано далее в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="ae382-160">Get this value by [Jobscience Client support team](https://www.jobscience.com/support) or from the SSO profile you will create which is explained later in the tutorial.</span></span> 
 
4. <span data-ttu-id="ae382-161">В разделе **Сертификат для подписи токена SAML** щелкните **Certificate (Base64)** (Сертификат (Base64)), а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="ae382-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_certificate.png) 

5. <span data-ttu-id="ae382-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="ae382-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-jobscience-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ae382-165">В разделе **Конфигурация Jobscience** щелкните **Настроить Jobscience**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="ae382-165">On the **Jobscience Configuration** section, click **Configure Jobscience** to open **Configure sign-on** window.</span></span> <span data-ttu-id="ae382-166">Скопируйте **URL-адрес выхода, идентификатор сущности SAML и URL-адрес службы единого входа SAML**  из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="ae382-166">Copy the **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_configure.png) 

7. <span data-ttu-id="ae382-168">Выполните вход на веб-сайт компании Jobscience в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="ae382-168">Log in to your Jobscience company site as an administrator.</span></span>

8. <span data-ttu-id="ae382-169">Перейдите в раздел **Настройка**.</span><span class="sxs-lookup"><span data-stu-id="ae382-169">Go to **Setup**.</span></span>
   
   <span data-ttu-id="ae382-170">![Настройка](./media/active-directory-saas-jobscience-tutorial/IC784358.png "Настройка")</span><span class="sxs-lookup"><span data-stu-id="ae382-170">![Setup](./media/active-directory-saas-jobscience-tutorial/IC784358.png "Setup")</span></span>

9. <span data-ttu-id="ae382-171">В области навигации слева в разделе **Administer** (Администрирование) щелкните **Domain Management** (Управление доменами), чтобы развернуть соответствующий раздел, а затем щелкните **My Domain** (Мой домен), чтобы открыть страницу **My Domain** (Мой домен).</span><span class="sxs-lookup"><span data-stu-id="ae382-171">On the left navigation pane, in the **Administer** section, click **Domain Management** to expand the related section, and then click **My Domain** to open the **My Domain** page.</span></span> 
   
   <span data-ttu-id="ae382-172">![Мой домен](./media/active-directory-saas-jobscience-tutorial/ic767825.png "Мой домен")</span><span class="sxs-lookup"><span data-stu-id="ae382-172">![My Domain](./media/active-directory-saas-jobscience-tutorial/ic767825.png "My Domain")</span></span>

10. <span data-ttu-id="ae382-173">Чтобы проверить правильность настройки домена, убедитесь, что он находится на этапе **Step 4 Deployed to Users** (Шаг 4. Развернут для пользователей), и просмотрите раздел **My Domain Settings** (Параметры моего домена).</span><span class="sxs-lookup"><span data-stu-id="ae382-173">To verify that your domain has been set up correctly, make sure that it is in “**Step 4 Deployed to Users**” and review your “**My Domain Settings**”.</span></span>

    <span data-ttu-id="ae382-174">![Домен, развернутый для пользователя](./media/active-directory-saas-jobscience-tutorial/ic784377.png "Domain Deployed to User")</span><span class="sxs-lookup"><span data-stu-id="ae382-174">![Domain Deployed to User](./media/active-directory-saas-jobscience-tutorial/ic784377.png "Domain Deployed to User")</span></span>

11. <span data-ttu-id="ae382-175">На корпоративном сайте Jobscience щелкните **Security Controls** (Средства управления безопасностью), а затем выберите **Single Sign-On Settings** (Параметры единого входа).</span><span class="sxs-lookup"><span data-stu-id="ae382-175">On the Jobscience company site, click **Security Controls**, and then click **Single Sign-On Settings**.</span></span>
    
    <span data-ttu-id="ae382-176">![Security Controls](./media/active-directory-saas-jobscience-tutorial/ic784364.png "Security Controls") (Средства управления безопасностью)</span><span class="sxs-lookup"><span data-stu-id="ae382-176">![Security Controls](./media/active-directory-saas-jobscience-tutorial/ic784364.png "Security Controls")</span></span>

12. <span data-ttu-id="ae382-177">В разделе **Параметры единого входа** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="ae382-177">In the **Single Sign-On Settings** section, perform the following steps:</span></span>
    
    <span data-ttu-id="ae382-178">![Single Sign-On Settings](./media/active-directory-saas-jobscience-tutorial/ic781026.png "Single Sign-On Settings") (Параметры единого входа)</span><span class="sxs-lookup"><span data-stu-id="ae382-178">![Single Sign-On Settings](./media/active-directory-saas-jobscience-tutorial/ic781026.png "Single Sign-On Settings")</span></span>
    
    <span data-ttu-id="ae382-179">а.</span><span class="sxs-lookup"><span data-stu-id="ae382-179">a.</span></span> <span data-ttu-id="ae382-180">Установите флажок **SAML включен**.</span><span class="sxs-lookup"><span data-stu-id="ae382-180">Select **SAML Enabled**.</span></span>

    <span data-ttu-id="ae382-181">b.</span><span class="sxs-lookup"><span data-stu-id="ae382-181">b.</span></span> <span data-ttu-id="ae382-182">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="ae382-182">Click **New**.</span></span>

13. <span data-ttu-id="ae382-183">В диалоговом окне **Изменение параметров единого входа SAML** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="ae382-183">On the **SAML Single Sign-On Setting Edit** dialog, perform the following steps:</span></span>
    
    <span data-ttu-id="ae382-184">![Параметры единого входа SAML](./media/active-directory-saas-jobscience-tutorial/ic784365.png "Параметры единого входа SAML")</span><span class="sxs-lookup"><span data-stu-id="ae382-184">![SAML Single Sign-On Setting](./media/active-directory-saas-jobscience-tutorial/ic784365.png "SAML Single Sign-On Setting")</span></span>
    
    <span data-ttu-id="ae382-185">а.</span><span class="sxs-lookup"><span data-stu-id="ae382-185">a.</span></span> <span data-ttu-id="ae382-186">В текстовом поле **Имя** введите имя конфигурации.</span><span class="sxs-lookup"><span data-stu-id="ae382-186">In the **Name** textbox, type a name for your configuration.</span></span>

    <span data-ttu-id="ae382-187">b.</span><span class="sxs-lookup"><span data-stu-id="ae382-187">b.</span></span> <span data-ttu-id="ae382-188">В текстовое поле **Issuer** (Издатель) вставьте значение **SAML Entity ID** (Идентификатор сущности SAML), скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="ae382-188">In **Issuer** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="ae382-189">c.</span><span class="sxs-lookup"><span data-stu-id="ae382-189">c.</span></span> <span data-ttu-id="ae382-190">В текстовое поле **Entity id** (Идентификатор сущности) введите `https://salesforce-jobscience.com`.</span><span class="sxs-lookup"><span data-stu-id="ae382-190">In the **Entity Id** textbox, type `https://salesforce-jobscience.com`</span></span>

    <span data-ttu-id="ae382-191">г)</span><span class="sxs-lookup"><span data-stu-id="ae382-191">d.</span></span> <span data-ttu-id="ae382-192">Чтобы отправить сертификат Azure AD, нажмите кнопку **Обзор** .</span><span class="sxs-lookup"><span data-stu-id="ae382-192">Click **Browse** to upload your Azure AD certificate.</span></span>

    <span data-ttu-id="ae382-193">д.</span><span class="sxs-lookup"><span data-stu-id="ae382-193">e.</span></span> <span data-ttu-id="ae382-194">В поле **SAML Identity Type** (Тип удостоверения SAML) выберите значение **Assertion contains the Federation ID from the User object** (Проверочное утверждение содержит идентификатор федерации из объекта User).</span><span class="sxs-lookup"><span data-stu-id="ae382-194">As **SAML Identity Type**, select **Assertion contains the Federation ID from the User object**.</span></span>

    <span data-ttu-id="ae382-195">Е.</span><span class="sxs-lookup"><span data-stu-id="ae382-195">f.</span></span> <span data-ttu-id="ae382-196">В поле **SAML Identity Location** (Расположение удостоверения SAML) выберите значение **Identity is in the NameIdentfier element of the Subject statement** (Удостоверение находится в элементе NameIdentifier оператора Subject).</span><span class="sxs-lookup"><span data-stu-id="ae382-196">As **SAML Identity Location**, select **Identity is in the NameIdentfier element of the Subject statement**.</span></span>

    <span data-ttu-id="ae382-197">g.</span><span class="sxs-lookup"><span data-stu-id="ae382-197">g.</span></span> <span data-ttu-id="ae382-198">В текстовое поле **Identity Provider Login URL** (URL-адрес входа IdP) вставьте значение **SAML Single Sign-On Service URL** (URL-адрес службы единого входа SAML), скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="ae382-198">In **Identity Provider Login URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="ae382-199">h.</span><span class="sxs-lookup"><span data-stu-id="ae382-199">h.</span></span> <span data-ttu-id="ae382-200">В текстовое поле **Identity Provider Logout URL** (URL-адрес выхода IdP) вставьте значение **URL-адрес выхода**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="ae382-200">In **Identity Provider Logout URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="ae382-201">i.</span><span class="sxs-lookup"><span data-stu-id="ae382-201">i.</span></span> <span data-ttu-id="ae382-202">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="ae382-202">Click **Save**.</span></span>

14. <span data-ttu-id="ae382-203">В области навигации слева в разделе **Administer** (Администрирование) щелкните **Domain Management** (Управление доменами), чтобы развернуть соответствующий раздел, а затем щелкните **My Domain** (Мой домен), чтобы открыть страницу **My Domain** (Мой домен).</span><span class="sxs-lookup"><span data-stu-id="ae382-203">On the left navigation pane, in the **Administer** section, click **Domain Management** to expand the related section, and then click **My Domain** to open the **My Domain** page.</span></span> 
    
    <span data-ttu-id="ae382-204">![Мой домен](./media/active-directory-saas-jobscience-tutorial/ic767825.png "Мой домен")</span><span class="sxs-lookup"><span data-stu-id="ae382-204">![My Domain](./media/active-directory-saas-jobscience-tutorial/ic767825.png "My Domain")</span></span>

15. <span data-ttu-id="ae382-205">На странице **My Domain** (Мой домен) в разделе **Login Page Branding** (Фирменная символика страницы входа) нажмите кнопку **Edit** (Изменить).</span><span class="sxs-lookup"><span data-stu-id="ae382-205">On the **My Domain** page, in the **Login Page Branding** section, click **Edit**.</span></span>
    
    <span data-ttu-id="ae382-206">![Фирменная символика страницы входа](./media/active-directory-saas-jobscience-tutorial/ic767826.png "Фирменная символика страницы входа")</span><span class="sxs-lookup"><span data-stu-id="ae382-206">![Login Page Branding](./media/active-directory-saas-jobscience-tutorial/ic767826.png "Login Page Branding")</span></span>

16. <span data-ttu-id="ae382-207">На странице **Login Page Branding** (Фирменная символика страницы входа) в разделе **Authentication Service** (Служба аутентификации) отображается имя **SAML SSO Settings** (Параметры единого входа SAML).</span><span class="sxs-lookup"><span data-stu-id="ae382-207">On the **Login Page Branding** page, in the **Authentication Service** section, the name of your **SAML SSO Settings** is displayed.</span></span> <span data-ttu-id="ae382-208">Выберите его, а затем нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="ae382-208">Select it, and then click **Save**.</span></span>
    
    <span data-ttu-id="ae382-209">![Фирменная символика страницы входа](./media/active-directory-saas-jobscience-tutorial/ic784366.png "Фирменная символика страницы входа")</span><span class="sxs-lookup"><span data-stu-id="ae382-209">![Login Page Branding](./media/active-directory-saas-jobscience-tutorial/ic784366.png "Login Page Branding")</span></span>

17. <span data-ttu-id="ae382-210">Чтобы получить URL-адрес единого входа, инициированный поставщиком услуг, в разделе меню **Security Controls** (Средства управления безопасностью) щелкните **Single Sign On settings** (Параметры единого входа).</span><span class="sxs-lookup"><span data-stu-id="ae382-210">To get the SP initiated Single Sign on Login URL click on the **Single Sign On settings** in the **Security Controls** menu section.</span></span>

    <span data-ttu-id="ae382-211">![Средства управления безопасностью](./media/active-directory-saas-jobscience-tutorial/ic784368.png "Средства управления безопасностью")</span><span class="sxs-lookup"><span data-stu-id="ae382-211">![Security Controls](./media/active-directory-saas-jobscience-tutorial/ic784368.png "Security Controls")</span></span>
    
    <span data-ttu-id="ae382-212">Выберите профиль единого входа, созданный на предыдущем этапе.</span><span class="sxs-lookup"><span data-stu-id="ae382-212">Click the SSO profile you have created in the step above.</span></span> <span data-ttu-id="ae382-213">На этой странице отображается URL-адрес единого входа для вашей компании (например, [https://название_компании.my.salesforce.com?so=companyid](https://companyname.my.salesforce.com?so=companyid)).</span><span class="sxs-lookup"><span data-stu-id="ae382-213">This page shows the Single Sign on URL for your company (for example, [https://companyname.my.salesforce.com?so=companyid](https://companyname.my.salesforce.com?so=companyid).</span></span>    

> [!TIP]
> <span data-ttu-id="ae382-214">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="ae382-214">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ae382-215">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="ae382-215">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ae382-216">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="ae382-216">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ae382-217">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae382-217">Creating an Azure AD test user</span></span>
<span data-ttu-id="ae382-218">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ae382-218">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="ae382-220">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="ae382-220">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ae382-221">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ae382-221">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jobscience-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ae382-223">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="ae382-223">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jobscience-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ae382-225">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="ae382-225">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jobscience-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ae382-227">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="ae382-227">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jobscience-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ae382-229">а.</span><span class="sxs-lookup"><span data-stu-id="ae382-229">a.</span></span> <span data-ttu-id="ae382-230">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ae382-230">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ae382-231">b.</span><span class="sxs-lookup"><span data-stu-id="ae382-231">b.</span></span> <span data-ttu-id="ae382-232">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ae382-232">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ae382-233">c.</span><span class="sxs-lookup"><span data-stu-id="ae382-233">c.</span></span> <span data-ttu-id="ae382-234">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="ae382-234">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ae382-235">d.</span><span class="sxs-lookup"><span data-stu-id="ae382-235">d.</span></span> <span data-ttu-id="ae382-236">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="ae382-236">Click **Create**.</span></span>
 
### <a name="creating-a-jobscience-test-user"></a><span data-ttu-id="ae382-237">Создание тестового пользователя Jobscience</span><span class="sxs-lookup"><span data-stu-id="ae382-237">Creating a Jobscience test user</span></span>

<span data-ttu-id="ae382-238">Чтобы пользователи Azure AD могли выполнять вход в Jobscience, они должны быть подготовлены в Jobscience.</span><span class="sxs-lookup"><span data-stu-id="ae382-238">In order to enable Azure AD users to log in to Jobscience, they must be provisioned into Jobscience.</span></span> <span data-ttu-id="ae382-239">В случае с Jobscience подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="ae382-239">In the case of Jobscience, provisioning is a manual task.</span></span>

>[!NOTE]
><span data-ttu-id="ae382-240">Вы можете использовать любые другие инструменты создания учетных записей пользователя Jobscience или API, предоставляемые Jobscience для подготовки учетных записей пользователя Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ae382-240">You can use any other Jobscience user account creation tools or APIs provided by Jobscience to provision Azure Active Directory user accounts.</span></span>
>  
        
<span data-ttu-id="ae382-241">**Чтобы настроить подготовку учетных записей пользователей, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="ae382-241">**To configure user provisioning, perform the following steps:**</span></span>

1. <span data-ttu-id="ae382-242">Выполните вход на веб-сайт **Jobscience** компании в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="ae382-242">Log in to your **Jobscience** company site as administrator.</span></span>

2. <span data-ttu-id="ae382-243">Перейдите в раздел "Настройка".</span><span class="sxs-lookup"><span data-stu-id="ae382-243">Go to Setup.</span></span>
   
   <span data-ttu-id="ae382-244">![Настройка](./media/active-directory-saas-jobscience-tutorial/ic784358.png "Настройка")</span><span class="sxs-lookup"><span data-stu-id="ae382-244">![Setup](./media/active-directory-saas-jobscience-tutorial/ic784358.png "Setup")</span></span>
3. <span data-ttu-id="ae382-245">Выберите **Manage Users \> Users** (Управление пользователями > Пользователи).</span><span class="sxs-lookup"><span data-stu-id="ae382-245">Go to **Manage Users \> Users**.</span></span>
   
   <span data-ttu-id="ae382-246">![Пользователи](./media/active-directory-saas-jobscience-tutorial/ic784369.png "Пользователи")</span><span class="sxs-lookup"><span data-stu-id="ae382-246">![Users](./media/active-directory-saas-jobscience-tutorial/ic784369.png "Users")</span></span>
4. <span data-ttu-id="ae382-247">Щелкните **Новый пользователь**.</span><span class="sxs-lookup"><span data-stu-id="ae382-247">Click **New User**.</span></span>
   
   <span data-ttu-id="ae382-248">![Все пользователи](./media/active-directory-saas-jobscience-tutorial/ic784370.png "Все пользователи")</span><span class="sxs-lookup"><span data-stu-id="ae382-248">![All Users](./media/active-directory-saas-jobscience-tutorial/ic784370.png "All Users")</span></span>
5. <span data-ttu-id="ae382-249">В диалоговом окне **Изменить пользователя** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="ae382-249">On the **Edit User** dialog, perform the following steps:</span></span>
   
   <span data-ttu-id="ae382-250">![Изменение пользователя](./media/active-directory-saas-jobscience-tutorial/ic784371.png "Изменение пользователя")</span><span class="sxs-lookup"><span data-stu-id="ae382-250">![User Edit](./media/active-directory-saas-jobscience-tutorial/ic784371.png "User Edit")</span></span>
   
   <span data-ttu-id="ae382-251">а.</span><span class="sxs-lookup"><span data-stu-id="ae382-251">a.</span></span> <span data-ttu-id="ae382-252">В текстовое поле **First Name** (Имя) введите имя пользователя, например Britta.</span><span class="sxs-lookup"><span data-stu-id="ae382-252">In the **First Name** textbox, type a first name of the user like Britta.</span></span>
   
   <span data-ttu-id="ae382-253">b.</span><span class="sxs-lookup"><span data-stu-id="ae382-253">b.</span></span> <span data-ttu-id="ae382-254">В текстовое поле **Last Name** (Фамилия) введите фамилию пользователя, например Simon.</span><span class="sxs-lookup"><span data-stu-id="ae382-254">In the **Last Name** textbox, type a last name of the user like Simon.</span></span>
   
   <span data-ttu-id="ae382-255">c.</span><span class="sxs-lookup"><span data-stu-id="ae382-255">c.</span></span> <span data-ttu-id="ae382-256">В текстовое поле **Alias** (Псевдоним) введите имя пользователя, например brittas.</span><span class="sxs-lookup"><span data-stu-id="ae382-256">In the **Alias** textbox, type an alias name of the user like brittas.</span></span>

   <span data-ttu-id="ae382-257">г)</span><span class="sxs-lookup"><span data-stu-id="ae382-257">d.</span></span> <span data-ttu-id="ae382-258">В текстовом поле **Email** (Электронная почта) введите адрес электронной почты пользователя, например Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="ae382-258">In the **Email** textbox, type the email address of user like Brittasimon@contoso.com.</span></span>

   <span data-ttu-id="ae382-259">д.</span><span class="sxs-lookup"><span data-stu-id="ae382-259">e.</span></span> <span data-ttu-id="ae382-260">В текстовом поле **User Name** (Имя пользователя) укажите имя пользователя, например Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="ae382-260">In the **User Name** textbox, type a user name of user like Brittasimon@contoso.com.</span></span>

   <span data-ttu-id="ae382-261">f.</span><span class="sxs-lookup"><span data-stu-id="ae382-261">f.</span></span> <span data-ttu-id="ae382-262">В текстовом поле **Nick Name** (Псевдоним) укажите псевдоним пользователя, например Simon.</span><span class="sxs-lookup"><span data-stu-id="ae382-262">In the **Nick Name** textbox, type a nick name of user like Simon.</span></span>

   <span data-ttu-id="ae382-263">g.</span><span class="sxs-lookup"><span data-stu-id="ae382-263">g.</span></span> <span data-ttu-id="ae382-264">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="ae382-264">Click **Save**.</span></span>

    
> [!NOTE]
> <span data-ttu-id="ae382-265">Владелец учетной записи Azure Active Directory получит по электронной почте сообщение со ссылкой для активации учетной записи.</span><span class="sxs-lookup"><span data-stu-id="ae382-265">The Azure Active Directory account holder receives an email and follows a link to confirm their account before it becomes active.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ae382-266">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="ae382-266">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ae382-267">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к Jobscience.</span><span class="sxs-lookup"><span data-stu-id="ae382-267">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Jobscience.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="ae382-269">**Чтобы назначить пользователя Britta Simon в Jobscience, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="ae382-269">**To assign Britta Simon to Jobscience, perform the following steps:**</span></span>

1. <span data-ttu-id="ae382-270">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="ae382-270">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="ae382-272">Из списка приложений выберите **Jobscience**.</span><span class="sxs-lookup"><span data-stu-id="ae382-272">In the applications list, select **Jobscience**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-jobscience-tutorial/tutorial_jobscience_app.png) 

3. <span data-ttu-id="ae382-274">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="ae382-274">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="ae382-276">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="ae382-276">Click **Add** button.</span></span> <span data-ttu-id="ae382-277">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="ae382-277">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="ae382-279">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="ae382-279">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ae382-280">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="ae382-280">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ae382-281">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="ae382-281">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ae382-282">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="ae382-282">Testing single sign-on</span></span>

<span data-ttu-id="ae382-283">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="ae382-283">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ae382-284">Щелкнув элемент "Jobscience" на панели доступа, вы автоматически войдете в приложение Jobscience.</span><span class="sxs-lookup"><span data-stu-id="ae382-284">When you click the Jobscience tile in the Access Panel, you should get automatically signed-on to your Jobscience application.</span></span>
<span data-ttu-id="ae382-285">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ae382-285">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ae382-286">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="ae382-286">Additional resources</span></span>

* [<span data-ttu-id="ae382-287">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ae382-287">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ae382-288">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ae382-288">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jobscience-tutorial/tutorial_general_203.png

