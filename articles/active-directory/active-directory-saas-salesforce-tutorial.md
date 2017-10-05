---
title: "Руководство по интеграции Azure Active Directory с Salesforce | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в приложении Salesforce."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2d7d420-dc91-41b8-a6b3-59579e043b35
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: 639e40ca7e406a1726033e9f5c5363c289087589
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-salesforce"></a><span data-ttu-id="e604c-103">Руководство по интеграции Azure Active Directory с Salesforce</span><span class="sxs-lookup"><span data-stu-id="e604c-103">Tutorial: Azure Active Directory integration with Salesforce</span></span>

<span data-ttu-id="e604c-104">В этом руководстве описано, как интегрировать Salesforce с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e604c-104">In this tutorial, you learn how to integrate Salesforce with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e604c-105">Интеграция Azure AD с приложением Salesforce обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="e604c-105">Integrating Salesforce with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="e604c-106">С помощью Azure AD можно управлять доступом к Salesforce.</span><span class="sxs-lookup"><span data-stu-id="e604c-106">You can control in Azure AD who has access to Salesforce</span></span>
- <span data-ttu-id="e604c-107">Вы можете включить автоматический вход пользователей в Salesforce (единый вход) с их учетными записями Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e604c-107">You can enable your users to automatically get signed-on to Salesforce (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e604c-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="e604c-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="e604c-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e604c-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e604c-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="e604c-110">Prerequisites</span></span>

<span data-ttu-id="e604c-111">Чтобы настроить интеграцию Azure AD с Salesforce, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="e604c-111">To configure Azure AD integration with Salesforce, you need the following items:</span></span>

- <span data-ttu-id="e604c-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="e604c-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e604c-113">подписка Salesforce с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="e604c-113">A Salesforce single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e604c-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="e604c-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e604c-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="e604c-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e604c-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="e604c-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e604c-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e604c-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e604c-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="e604c-118">Scenario description</span></span>
<span data-ttu-id="e604c-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="e604c-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e604c-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="e604c-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e604c-121">Добавление Salesforce из коллекции</span><span class="sxs-lookup"><span data-stu-id="e604c-121">Adding Salesforce from the gallery</span></span>
2. <span data-ttu-id="e604c-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="e604c-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-salesforce-from-the-gallery"></a><span data-ttu-id="e604c-123">Добавление Salesforce из коллекции</span><span class="sxs-lookup"><span data-stu-id="e604c-123">Adding Salesforce from the gallery</span></span>
<span data-ttu-id="e604c-124">Чтобы настроить интеграцию приложения Salesforce с Azure AD, вам нужно добавить Salesforce из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="e604c-124">To configure the integration of Salesforce into Azure AD, you need to add Salesforce from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="e604c-125">**Чтобы добавить Salesforce из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="e604c-125">**To add Salesforce from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="e604c-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e604c-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e604c-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="e604c-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="e604c-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="e604c-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="e604c-131">В верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="e604c-131">Click **New application** button on the top of the dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="e604c-133">В поле поиска введите **Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="e604c-133">In the search box, type **Salesforce**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_search.png)

5. <span data-ttu-id="e604c-135">На панели результатов выберите **Salesforce** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="e604c-135">In the results panel, select **Salesforce**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e604c-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="e604c-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e604c-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложение Salesforce с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e604c-138">In this section, you configure and test Azure AD single sign-on with Salesforce based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e604c-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Salesforce соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e604c-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Salesforce is to a user in Azure AD.</span></span> <span data-ttu-id="e604c-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Salesforce.</span><span class="sxs-lookup"><span data-stu-id="e604c-140">In other words, a link relationship between an Azure AD user and the related user in Salesforce needs to be established.</span></span>

<span data-ttu-id="e604c-141">Чтобы установить эту связь, следует назначить **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Salesforce.</span><span class="sxs-lookup"><span data-stu-id="e604c-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Salesforce.</span></span>

<span data-ttu-id="e604c-142">Чтобы настроить и проверить единый вход Azure AD в Salesforce, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="e604c-142">To configure and test Azure AD single sign-on with Salesforce, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="e604c-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="e604c-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="e604c-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e604c-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e604c-145">**[Создание тестового пользователя Salesforce](#creating-a-salesforce-test-user)** требуется для создания в Salesforce пользователя Britta Simon, связанного с представлением этого пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e604c-145">**[Creating a Salesforce test user](#creating-a-salesforce-test-user)** - to have a counterpart of Britta Simon in Salesforce that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="e604c-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e604c-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e604c-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="e604c-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e604c-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="e604c-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e604c-149">В данном разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Salesforce.</span><span class="sxs-lookup"><span data-stu-id="e604c-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Salesforce application.</span></span>

<span data-ttu-id="e604c-150">**Чтобы настроить единый вход Azure AD в Salesforce, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="e604c-150">**To configure Azure AD single sign-on with Salesforce, perform the following steps:**</span></span>

1. <span data-ttu-id="e604c-151">На портале Azure на странице интеграции с приложением **Salesforce** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="e604c-151">In the Azure portal, on the **Salesforce** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="e604c-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="e604c-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_samlbase.png)

3. <span data-ttu-id="e604c-155">В разделе **Домен и URL-адреса Salesforce** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="e604c-155">On the **Salesforce Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_url.png)

    <span data-ttu-id="e604c-157">В текстовом поле **URL-адрес для входа** введите значение в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="e604c-157">In the **Sign-on URL** textbox, type the value using the following pattern:</span></span> 
   * <span data-ttu-id="e604c-158">Учетная запись предприятия: `https://<subdomain>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="e604c-158">Enterprise account: `https://<subdomain>.my.salesforce.com`</span></span>
   * <span data-ttu-id="e604c-159">Учетная запись разработчика: `https://<subdomain>-dev-ed.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="e604c-159">Developer account: `https://<subdomain>-dev-ed.my.salesforce.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e604c-160">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="e604c-160">These values are not the real.</span></span> <span data-ttu-id="e604c-161">Замените эти значения фактическим URL-адресом для входа.</span><span class="sxs-lookup"><span data-stu-id="e604c-161">Update these values with the actual Sign-on URL.</span></span> <span data-ttu-id="e604c-162">Чтобы получить их, обратитесь в [службу поддержки клиентов Salesforce](https://help.salesforce.com/support).</span><span class="sxs-lookup"><span data-stu-id="e604c-162">Contact [Salesforce Client support team](https://help.salesforce.com/support) to get these values.</span></span> 
 
4. <span data-ttu-id="e604c-163">В разделе **Сертификат подписи SAML** щелкните **Сертификат**, а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="e604c-163">On the **SAML Signing Certificate** section, click **Certificate** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_certificate.png) 

5. <span data-ttu-id="e604c-165">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="e604c-165">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-salesforce-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e604c-167">В разделе **Конфигурация Salesforce** щелкните **Настроить Salesforce**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="e604c-167">On the **Salesforce Configuration** section, click **Configure Salesforce** to open **Configure sign-on** window.</span></span> <span data-ttu-id="e604c-168">Скопируйте **идентификатор сущности SAML и URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="e604c-168">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span> 

    <span data-ttu-id="e604c-169">![Настройка единого входа](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_configure.png) 
<CS></span><span class="sxs-lookup"><span data-stu-id="e604c-169">![Configure Single Sign-On](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_configure.png) 
<CS></span></span>
7.  <span data-ttu-id="e604c-170">Откройте новую вкладку в браузере и войдите в учетную запись администратора Salesforce.</span><span class="sxs-lookup"><span data-stu-id="e604c-170">Open a new tab in your browser and log in to your Salesforce administrator account.</span></span>

8.  <span data-ttu-id="e604c-171">В области навигации **Administrator** (Администратор) щелкните **Security Controls** (Управление безопасностью), чтобы развернуть соответствующий раздел.</span><span class="sxs-lookup"><span data-stu-id="e604c-171">Under the **Administrator** navigation pane, click **Security Controls** to expand the related section.</span></span> <span data-ttu-id="e604c-172">Затем щелкните **Параметры единого входа**.</span><span class="sxs-lookup"><span data-stu-id="e604c-172">Then click **Single Sign-On Settings**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso.png)

9.  <span data-ttu-id="e604c-174">На странице **Single Sign-On Settings** (Параметры единого входа) нажмите кнопку **Edit** (Изменить).</span><span class="sxs-lookup"><span data-stu-id="e604c-174">On the **Single Sign-On Settings** page, click the **Edit** button.</span></span>
    <span data-ttu-id="e604c-175">![Настройка единого входа](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-edit.png)</span><span class="sxs-lookup"><span data-stu-id="e604c-175">![Configure Single Sign-On](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-edit.png)</span></span>

      > [!NOTE]
      > <span data-ttu-id="e604c-176">Если не удается включить параметры единого входа для своей учетной записи Salesforce, возможно, вам придется обратиться за помощью в [службу поддержки Salesforce](https://help.salesforce.com/support).</span><span class="sxs-lookup"><span data-stu-id="e604c-176">If you are unable to enable Single Sign-On settings for your Salesforce account, you may need to contact [Salesforce Client support team](https://help.salesforce.com/support).</span></span> 

10. <span data-ttu-id="e604c-177">Выберите **SAML Enabled** (SAML включен), а затем щелкните **Save** (Сохранить).</span><span class="sxs-lookup"><span data-stu-id="e604c-177">Select **SAML Enabled**, and then click **Save**.</span></span>

      ![Настройка единого входа](./media/active-directory-saas-salesforce-tutorial/sf-enable-saml.png)
11. <span data-ttu-id="e604c-179">Чтобы настроить параметры единого входа SAML, щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="e604c-179">To configure your SAML single sign-on settings, click **New**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-salesforce-tutorial/sf-admin-sso-new.png)

12. <span data-ttu-id="e604c-181">На странице **Изменение параметров единого входа на основе SAML** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="e604c-181">On the **SAML Single Sign-On Setting Edit** page, make the following configurations:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-salesforce-tutorial/sf-saml-config.png)

    <span data-ttu-id="e604c-183">а.</span><span class="sxs-lookup"><span data-stu-id="e604c-183">a.</span></span> <span data-ttu-id="e604c-184">В поле **Имя** введите понятное имя конфигурации.</span><span class="sxs-lookup"><span data-stu-id="e604c-184">For the **Name** field, type in a friendly name for this configuration.</span></span> <span data-ttu-id="e604c-185">При вводе значения в поле **Name** (Имя) текстовое поле **API Name** (Имя API) заполняется автоматически.</span><span class="sxs-lookup"><span data-stu-id="e604c-185">Providing a value for **Name** automatically populate the **API Name** textbox.</span></span>

    <span data-ttu-id="e604c-186">b.</span><span class="sxs-lookup"><span data-stu-id="e604c-186">b.</span></span> <span data-ttu-id="e604c-187">Вставьте значение **идентификатора сущности SMAL** в поле **Издатель** в Salesforce.</span><span class="sxs-lookup"><span data-stu-id="e604c-187">Paste **SMAL Entity ID** value into the **Issuer** field in Salesforce.</span></span>

    <span data-ttu-id="e604c-188">c.</span><span class="sxs-lookup"><span data-stu-id="e604c-188">c.</span></span> <span data-ttu-id="e604c-189">Введите в текстовое поле **Идентификатор сущности**имя домена Salesforce в следующем формате.</span><span class="sxs-lookup"><span data-stu-id="e604c-189">In the **Entity Id textbox**, type your Salesforce domain name using the following pattern:</span></span>
      
      * <span data-ttu-id="e604c-190">Учетная запись предприятия: `https://<subdomain>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="e604c-190">Enterprise account: `https://<subdomain>.my.salesforce.com`</span></span>
      * <span data-ttu-id="e604c-191">Учетная запись разработчика: `https://<subdomain>-dev-ed.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="e604c-191">Developer account: `https://<subdomain>-dev-ed.my.salesforce.com`</span></span>
      
    <span data-ttu-id="e604c-192">г)</span><span class="sxs-lookup"><span data-stu-id="e604c-192">d.</span></span> <span data-ttu-id="e604c-193">Нажмите кнопку **Browse** (Обзор) или **Choose File** (Выбрать файл), чтобы открыть диалоговое окно **Choose File to Upload** (Выбор файла для передачи). Выберите сертификат Salesforce и нажмите кнопку **Open** (Открыть), чтобы передать его.</span><span class="sxs-lookup"><span data-stu-id="e604c-193">Click **Browse** or **Choose File** to open the **Choose File to Upload** dialog, select your Salesforce certificate, and then click **Open** to upload the certificate.</span></span>

    <span data-ttu-id="e604c-194">д.</span><span class="sxs-lookup"><span data-stu-id="e604c-194">e.</span></span> <span data-ttu-id="e604c-195">В поле **SAML Identity Type** (Тип удостоверения SAML) выберите значение **Assertion contains User's salesforce.com username** (Утверждение содержит имя пользователя salesforce.com).</span><span class="sxs-lookup"><span data-stu-id="e604c-195">For **SAML Identity Type**, select **Assertion contains User's salesforce.com username**.</span></span>

    <span data-ttu-id="e604c-196">Е.</span><span class="sxs-lookup"><span data-stu-id="e604c-196">f.</span></span> <span data-ttu-id="e604c-197">В поле **SAML Identity Location** (Расположение удостоверения SAML) выберите значение **Identity is in the NameIdentifier element of the Subject statement** (Удостоверение находится в элементе NameIdentifier оператора Subject).</span><span class="sxs-lookup"><span data-stu-id="e604c-197">For **SAML Identity Location**, select **Identity is in the NameIdentifier element of the Subject statement**</span></span>

    <span data-ttu-id="e604c-198">g.</span><span class="sxs-lookup"><span data-stu-id="e604c-198">g.</span></span> <span data-ttu-id="e604c-199">Вставьте **URL-адрес службы единого входа** в поле **URL-адрес входа поставщика удостоверений** в Salesforce.</span><span class="sxs-lookup"><span data-stu-id="e604c-199">Paste **Single Sign-On Service URL** into the **Identity Provider Login URL** field in Salesforce.</span></span>
    
    <span data-ttu-id="e604c-200">h.</span><span class="sxs-lookup"><span data-stu-id="e604c-200">h.</span></span> <span data-ttu-id="e604c-201">В поле **Service Provider Initiated Request Binding** (Связывание запросов, инициируемых поставщиком услуг) выберите значение **HTTP Redirect** (Перенаправление HTTP).</span><span class="sxs-lookup"><span data-stu-id="e604c-201">For **Service Provider Initiated Request Binding**, select **HTTP Redirect**.</span></span>
    
    <span data-ttu-id="e604c-202">i.</span><span class="sxs-lookup"><span data-stu-id="e604c-202">i.</span></span> <span data-ttu-id="e604c-203">Наконец, нажмите кнопку **Сохранить** , чтобы применить параметры единого входа SAML.</span><span class="sxs-lookup"><span data-stu-id="e604c-203">Finally, click **Save** to apply your SAML single sign-on settings.</span></span>

13. <span data-ttu-id="e604c-204">В левой области навигации в Salesforce щелкните **Domain Management** (Управление доменами), чтобы развернуть соответствующий раздел, и нажмите кнопку **My Domain** (Мой домен).</span><span class="sxs-lookup"><span data-stu-id="e604c-204">On the left navigation pane in Salesforce, click **Domain Management** to expand the related section, and then click **My Domain**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-salesforce-tutorial/sf-my-domain.png)

14. <span data-ttu-id="e604c-206">Прокрутите страницу вниз до раздела **Authentication Configuration** (Конфигурация аутентификации) и нажмите кнопку **Edit** (Изменить).</span><span class="sxs-lookup"><span data-stu-id="e604c-206">Scroll down to the **Authentication Configuration** section, and click the **Edit** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-salesforce-tutorial/sf-edit-auth-config.png)

15. <span data-ttu-id="e604c-208">В разделе **Authentication Service** (Служба аутентификации) выберите понятное имя конфигурации единого входа SAML и нажмите кнопку **Save** (Сохранить).</span><span class="sxs-lookup"><span data-stu-id="e604c-208">In the **Authentication Service** section, select the friendly name of your SAML SSO configuration, and then click **Save**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-salesforce-tutorial/sf-auth-config.png)

    > [!NOTE]
    > <span data-ttu-id="e604c-210">Если выбрано несколько служб проверки подлинности, то при попытке инициировать единый вход в среду Salesforce пользователям будет предложено уточнить, с помощью какой службы проверки подлинности нужно выполнить вход.</span><span class="sxs-lookup"><span data-stu-id="e604c-210">If more than one authentication service is selected, users are prompted to select which authentication service they like to sign in with while initiating single sign-on to your Salesforce environment.</span></span> <span data-ttu-id="e604c-211">Чтобы этого избежать, **снимите флажки для всех других служб проверки подлинности**.</span><span class="sxs-lookup"><span data-stu-id="e604c-211">If you don’t want it to happen, then you should **leave all other authentication services unchecked**.</span></span>
<CE>    
> [!TIP]
> <span data-ttu-id="e604c-212">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="e604c-212">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="e604c-213">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="e604c-213">After adding this app from the **Active Directory > Enterprise Applications** section, simply click **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="e604c-214">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="e604c-214">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e604c-215">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="e604c-215">Creating an Azure AD test user</span></span>
<span data-ttu-id="e604c-216">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e604c-216">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="e604c-218">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="e604c-218">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="e604c-219">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e604c-219">On the left navigation pane in the **Azure portal**, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-salesforce-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e604c-221">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="e604c-221">To display the list of users, Go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-salesforce-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e604c-223">В верхней части диалогового окна щелкните **Добавить**, чтобы открыть диалоговое окно **Пользователь**.</span><span class="sxs-lookup"><span data-stu-id="e604c-223">At the top of the dialog, click **Add** to open the **User** dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-salesforce-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e604c-225">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="e604c-225">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-salesforce-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e604c-227">а.</span><span class="sxs-lookup"><span data-stu-id="e604c-227">a.</span></span> <span data-ttu-id="e604c-228">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e604c-228">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e604c-229">b.</span><span class="sxs-lookup"><span data-stu-id="e604c-229">b.</span></span> <span data-ttu-id="e604c-230">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e604c-230">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e604c-231">c.</span><span class="sxs-lookup"><span data-stu-id="e604c-231">c.</span></span> <span data-ttu-id="e604c-232">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="e604c-232">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="e604c-233">d.</span><span class="sxs-lookup"><span data-stu-id="e604c-233">d.</span></span> <span data-ttu-id="e604c-234">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="e604c-234">Click **Create**.</span></span>
 
### <a name="creating-a-salesforce-test-user"></a><span data-ttu-id="e604c-235">Создание тестового пользователя Salesforce</span><span class="sxs-lookup"><span data-stu-id="e604c-235">Creating a Salesforce test user</span></span>

<span data-ttu-id="e604c-236">В этом разделе вы создадите в Salesforce пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e604c-236">In this section, a user called Britta Simon is created in Salesforce.</span></span> <span data-ttu-id="e604c-237">Приложение Salesforce поддерживает JIT-подготовку. Эта функция включена по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="e604c-237">Salesforce supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="e604c-238">В этом разделе никакие действия с вашей стороны не требуются.</span><span class="sxs-lookup"><span data-stu-id="e604c-238">There is no action item for you in this section.</span></span> <span data-ttu-id="e604c-239">Если пользователь в Salesforce еще не существует, он создается при попытке доступа к приложению Salesforce.</span><span class="sxs-lookup"><span data-stu-id="e604c-239">If a user doesn't already exist in Salesforce, a new one is created when you attempt to access Salesforce.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="e604c-240">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="e604c-240">Assigning the Azure AD test user</span></span>

<span data-ttu-id="e604c-241">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure путем предоставления доступа к Salesforce.</span><span class="sxs-lookup"><span data-stu-id="e604c-241">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Salesforce.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="e604c-243">**Чтобы назначить пользователя Britta Simon в Salesforce, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="e604c-243">**To assign Britta Simon to Salesforce, perform the following steps:**</span></span>

1. <span data-ttu-id="e604c-244">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="e604c-244">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="e604c-246">В списке приложений выберите **Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="e604c-246">In the applications list, select **Salesforce**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-salesforce-tutorial/tutorial_salesforce_app.png) 

3. <span data-ttu-id="e604c-248">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="e604c-248">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="e604c-250">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="e604c-250">Click **Add** button.</span></span> <span data-ttu-id="e604c-251">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="e604c-251">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="e604c-253">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="e604c-253">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="e604c-254">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="e604c-254">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e604c-255">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="e604c-255">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e604c-256">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="e604c-256">Testing single sign-on</span></span>

<span data-ttu-id="e604c-257">Чтобы проверить параметры единого входа, откройте панель доступа по адресу [https://myapps.microsoft.com](https://myapps.microsoft.com/), выполните вход с тестовой учетной записью и щелкните **Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="e604c-257">To test your single sign-on settings, open the Access Panel at [https://myapps.microsoft.com](https://myapps.microsoft.com/), then sign into the test account, and click **Salesforce**.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e604c-258">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="e604c-258">Additional resources</span></span>

* [<span data-ttu-id="e604c-259">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e604c-259">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e604c-260">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="e604c-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="e604c-261">Руководство по настройке Google Apps для автоматической подготовки пользователей</span><span class="sxs-lookup"><span data-stu-id="e604c-261">Configure User Provisioning</span></span>](active-directory-saas-salesforce-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-salesforce-tutorial/tutorial_general_203.png

