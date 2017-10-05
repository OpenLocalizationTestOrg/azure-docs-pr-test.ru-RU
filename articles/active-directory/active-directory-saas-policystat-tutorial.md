---
title: "Руководство по интеграции Azure Active Directory с PolicyStat | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в приложении PolicyStat."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: af5eb0f1-1c8e-4809-b0c4-8ccfb915ca42
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 704afd5515b02ce2a4fbf35da65fad74dc506271
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-policystat"></a><span data-ttu-id="b5395-103">Руководство по интеграции Azure Active Directory с PolicyStat</span><span class="sxs-lookup"><span data-stu-id="b5395-103">Tutorial: Azure Active Directory integration with PolicyStat</span></span>

<span data-ttu-id="b5395-104">В этом руководстве описано, как интегрировать PolicyStat с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b5395-104">In this tutorial, you learn how to integrate PolicyStat with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b5395-105">Интеграция Azure AD с приложением PolicyStat обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="b5395-105">Integrating PolicyStat with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b5395-106">С помощью Azure AD вы можете контролировать доступ к PolicyStat.</span><span class="sxs-lookup"><span data-stu-id="b5395-106">You can control in Azure AD who has access to PolicyStat</span></span>
- <span data-ttu-id="b5395-107">Вы можете включить автоматический вход пользователей в PolicyStat (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b5395-107">You can enable your users to automatically get signed-on to PolicyStat (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b5395-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="b5395-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b5395-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b5395-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b5395-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b5395-110">Prerequisites</span></span>

<span data-ttu-id="b5395-111">Чтобы настроить интеграцию Azure AD с PolicyStat, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="b5395-111">To configure Azure AD integration with PolicyStat, you need the following items:</span></span>

- <span data-ttu-id="b5395-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="b5395-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b5395-113">подписка PolicyStat с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="b5395-113">A PolicyStat single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b5395-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="b5395-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b5395-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="b5395-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b5395-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="b5395-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b5395-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b5395-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b5395-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="b5395-118">Scenario description</span></span>
<span data-ttu-id="b5395-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="b5395-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b5395-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="b5395-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b5395-121">Добавление PolicyStat из коллекции.</span><span class="sxs-lookup"><span data-stu-id="b5395-121">Adding PolicyStat from the gallery</span></span>
2. <span data-ttu-id="b5395-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b5395-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-policystat-from-the-gallery"></a><span data-ttu-id="b5395-123">Добавление PolicyStat из коллекции</span><span class="sxs-lookup"><span data-stu-id="b5395-123">Adding PolicyStat from the gallery</span></span>
<span data-ttu-id="b5395-124">Чтобы настроить интеграцию PolicyStat с Azure AD, необходимо добавить PolicyStat из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="b5395-124">To configure the integration of PolicyStat into Azure AD, you need to add PolicyStat from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b5395-125">**Чтобы добавить PolicyStat из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="b5395-125">**To add PolicyStat from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b5395-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b5395-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b5395-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="b5395-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b5395-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="b5395-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="b5395-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="b5395-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="b5395-133">В поле поиска введите **PolicyStat**.</span><span class="sxs-lookup"><span data-stu-id="b5395-133">In the search box, type **PolicyStat**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_search.png)

5. <span data-ttu-id="b5395-135">На панели результатов выберите **PolicyStat** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="b5395-135">In the results panel, select **PolicyStat**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b5395-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b5395-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b5395-138">В этом разделе описана настройка и проверка единого входа Azure AD в PolicyStat с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b5395-138">In this section, you configure and test Azure AD single sign-on with PolicyStat based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b5395-139">Чтобы единый вход работал, Azure AD необходима информация о том, какой пользователь в PolicyStat соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b5395-139">For single sign-on to work, Azure AD needs to know what the counterpart user in PolicyStat is to a user in Azure AD.</span></span> <span data-ttu-id="b5395-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в PolicyStat.</span><span class="sxs-lookup"><span data-stu-id="b5395-140">In other words, a link relationship between an Azure AD user and the related user in PolicyStat needs to be established.</span></span>

<span data-ttu-id="b5395-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в PolicyStat.</span><span class="sxs-lookup"><span data-stu-id="b5395-141">In PolicyStat, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="b5395-142">Чтобы настроить и проверить единый вход Azure AD в PolicyStat, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="b5395-142">To configure and test Azure AD single sign-on with PolicyStat, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b5395-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="b5395-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b5395-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b5395-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b5395-145">**[Создание тестового пользователя PolicyStat](#creating-a-policystat-test-user)** требуется для того, чтобы в PolicyStat существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b5395-145">**[Creating a PolicyStat test user](#creating-a-policystat-test-user)** - to have a counterpart of Britta Simon in PolicyStat that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b5395-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b5395-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b5395-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="b5395-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b5395-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b5395-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b5395-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении PolicyStat.</span><span class="sxs-lookup"><span data-stu-id="b5395-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your PolicyStat application.</span></span>

<span data-ttu-id="b5395-150">**Чтобы настроить единый вход Azure AD в PolicyStat, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="b5395-150">**To configure Azure AD single sign-on with PolicyStat, perform the following steps:**</span></span>

1. <span data-ttu-id="b5395-151">На портале Azure на странице интеграции с приложением **PolicyStat** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="b5395-151">In the Azure portal, on the **PolicyStat** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="b5395-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="b5395-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_samlbase.png)

3. <span data-ttu-id="b5395-155">В разделе **Домены и URL-адреса приложения PolicyStat** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="b5395-155">On the **PolicyStat Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_url.png)

    <span data-ttu-id="b5395-157">а.</span><span class="sxs-lookup"><span data-stu-id="b5395-157">a.</span></span> <span data-ttu-id="b5395-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<companyname>.policystat.com`</span><span class="sxs-lookup"><span data-stu-id="b5395-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.policystat.com`</span></span>

    <span data-ttu-id="b5395-159">b.</span><span class="sxs-lookup"><span data-stu-id="b5395-159">b.</span></span> <span data-ttu-id="b5395-160">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<companyname>.policystat.com/saml2/metadata/`</span><span class="sxs-lookup"><span data-stu-id="b5395-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.policystat.com/saml2/metadata/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b5395-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="b5395-161">These values are not real.</span></span> <span data-ttu-id="b5395-162">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="b5395-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="b5395-163">Чтобы получить эти значения, обратитесь к [группе поддержки клиентов PolicyStat](http://www.policystat.com/support/).</span><span class="sxs-lookup"><span data-stu-id="b5395-163">Contact [PolicyStat Client support team](http://www.policystat.com/support/) to get these values.</span></span> 
 
4. <span data-ttu-id="b5395-164">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="b5395-164">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_certificate.png) 

5. <span data-ttu-id="b5395-166">В этом разделе показано, как разрешить пользователям проходить аутентификацию в PolicyStat со своей учетной записью Azure AD, используя федерацию на основе протокола SAML.</span><span class="sxs-lookup"><span data-stu-id="b5395-166">The objective of this section is to outline how to enable users to authenticate to PolicyStat with their account in Azure AD using federation based on the SAML protocol.</span></span>

    <span data-ttu-id="b5395-167">Приложение PolicyStat ожидает утверждения SAML в определенном формате, который требует добавить настраиваемые сопоставления атрибутов в вашу конфигурацию **атрибутов токена SAML**.</span><span class="sxs-lookup"><span data-stu-id="b5395-167">The PolicyStat application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your **SAML Token Attributes** configuration.</span></span>  

     <span data-ttu-id="b5395-168">На следующем снимке экрана приведен пример.</span><span class="sxs-lookup"><span data-stu-id="b5395-168">The following screenshot shows an example of this.</span></span>

     <span data-ttu-id="b5395-169">![Атрибуты](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_attribute.png "Атрибуты")</span><span class="sxs-lookup"><span data-stu-id="b5395-169">![Attributes](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_attribute.png "Attributes")</span></span>

6. <span data-ttu-id="b5395-170">Чтобы добавить обязательные сопоставления атрибутов, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="b5395-170">To add the required attribute mappings, perform the following steps:</span></span>

    | <span data-ttu-id="b5395-171">Имя атрибута</span><span class="sxs-lookup"><span data-stu-id="b5395-171">Attribute Name</span></span>    |   <span data-ttu-id="b5395-172">Значение атрибута</span><span class="sxs-lookup"><span data-stu-id="b5395-172">Attribute Value</span></span> |
    |------------------- | -------------------- |
    | <span data-ttu-id="b5395-173">uid</span><span class="sxs-lookup"><span data-stu-id="b5395-173">uid</span></span> | <span data-ttu-id="b5395-174">ExtractMailPrefix([mail])</span><span class="sxs-lookup"><span data-stu-id="b5395-174">ExtractMailPrefix([mail])</span></span> |
    
    <span data-ttu-id="b5395-175">а.</span><span class="sxs-lookup"><span data-stu-id="b5395-175">a.</span></span> <span data-ttu-id="b5395-176">Щелкните **Добавить атрибут**, чтобы открыть диалоговое окно **Добавление атрибута**.</span><span class="sxs-lookup"><span data-stu-id="b5395-176">Click **Add attribute** to open the **Add Attribute** dialog.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_04.png)

    ![Настройка единого входа](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_addatribute.png)
    
    <span data-ttu-id="b5395-179">b.</span><span class="sxs-lookup"><span data-stu-id="b5395-179">b.</span></span> <span data-ttu-id="b5395-180">В текстовом поле **Имя атрибута** введите значение **uid**.</span><span class="sxs-lookup"><span data-stu-id="b5395-180">In the **Attribute Name** textbox, type **uid**.</span></span>

    <span data-ttu-id="b5395-181">c.</span><span class="sxs-lookup"><span data-stu-id="b5395-181">c.</span></span> <span data-ttu-id="b5395-182">В текстовом поле **Значение атрибута** выберите **ExtractMailPrefix()**.</span><span class="sxs-lookup"><span data-stu-id="b5395-182">In the **Attribute Value** textbox, select **ExtractMailPrefix()**.</span></span>    
   
    <span data-ttu-id="b5395-183">г)</span><span class="sxs-lookup"><span data-stu-id="b5395-183">d.</span></span> <span data-ttu-id="b5395-184">Из списка **Почта** выберите пункт **User.mail**.</span><span class="sxs-lookup"><span data-stu-id="b5395-184">From the **Mail** list, select **User.mail**.</span></span>
    
    <span data-ttu-id="b5395-185">д.</span><span class="sxs-lookup"><span data-stu-id="b5395-185">e.</span></span> <span data-ttu-id="b5395-186">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="b5395-186">Click **Ok**</span></span>

7. <span data-ttu-id="b5395-187">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="b5395-187">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-policystat-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="b5395-189">В другом окне веб-браузера войдите на сайт PolicyStat своей компании в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="b5395-189">In a different web browser window, log into your PolicyStat company site as an administrator.</span></span>

9. <span data-ttu-id="b5395-190">Щелкните вкладку **Admin** (Администрирование), а затем щелкните **Single Sign-On Configuration** (Конфигурация единого входа) в левой области навигации.</span><span class="sxs-lookup"><span data-stu-id="b5395-190">Click the **Admin** tab, and then click **Single Sign-On Configuration** in left navigation pane.</span></span>
   
    <span data-ttu-id="b5395-191">![Меню администратора](./media/active-directory-saas-policystat-tutorial/ic808633.png "Меню администратора")</span><span class="sxs-lookup"><span data-stu-id="b5395-191">![Administrator Menu](./media/active-directory-saas-policystat-tutorial/ic808633.png "Administrator Menu")</span></span>

10. <span data-ttu-id="b5395-192">В разделе **Setup** (Настройка) установите флажок **Enable Single Sign-on Integration** (Включить интеграцию единого входа).</span><span class="sxs-lookup"><span data-stu-id="b5395-192">In the **Setup** section, select **Enable Single Sign-on Integration**.</span></span>
   
    <span data-ttu-id="b5395-193">![Конфигурация единого входа](./media/active-directory-saas-policystat-tutorial/ic808634.png "Конфигурация единого входа")</span><span class="sxs-lookup"><span data-stu-id="b5395-193">![Single Sign-On Configuration](./media/active-directory-saas-policystat-tutorial/ic808634.png "Single Sign-On Configuration")</span></span>

11. <span data-ttu-id="b5395-194">Щелкните **Configure Attributes** (Настроить атрибуты), а затем в разделе **Configure Attributes** (Настройка атрибутов) сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="b5395-194">Click **Configure Attributes**, and then, in the **Configure Attributes** section, perform the following steps:</span></span>
   
    <span data-ttu-id="b5395-195">![Конфигурация единого входа](./media/active-directory-saas-policystat-tutorial/ic808635.png "Конфигурация единого входа")</span><span class="sxs-lookup"><span data-stu-id="b5395-195">![Single Sign-On Configuration](./media/active-directory-saas-policystat-tutorial/ic808635.png "Single Sign-On Configuration")</span></span>
   
    <span data-ttu-id="b5395-196">а.</span><span class="sxs-lookup"><span data-stu-id="b5395-196">a.</span></span> <span data-ttu-id="b5395-197">В текстовом поле **Username Attribute** (Атрибут имени пользователя) введите значение **uid**.</span><span class="sxs-lookup"><span data-stu-id="b5395-197">In the **Username Attribute** textbox, type **uid**.</span></span>

    <span data-ttu-id="b5395-198">b.</span><span class="sxs-lookup"><span data-stu-id="b5395-198">b.</span></span> <span data-ttu-id="b5395-199">В текстовое поле **First Name Attribute** (Атрибут имени) введите **имя** пользователя, **Britta**.</span><span class="sxs-lookup"><span data-stu-id="b5395-199">In the **First Name Attribute** textbox, type **firstname** of user **Britta**.</span></span>

    <span data-ttu-id="b5395-200">c.</span><span class="sxs-lookup"><span data-stu-id="b5395-200">c.</span></span> <span data-ttu-id="b5395-201">В текстовое поле **Last Name Attribute** (Атрибут фамилии) введите **фамилию** пользователя, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="b5395-201">In the **Last Name Attribute** textbox, type **lastname** of user **Simon**.</span></span>

    <span data-ttu-id="b5395-202">г)</span><span class="sxs-lookup"><span data-stu-id="b5395-202">d.</span></span> <span data-ttu-id="b5395-203">В текстовое поле **Email Attribute** (Атрибут электронной почты) введите значение **адрес электронной почты** пользователя, **BrittaSimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="b5395-203">In the **Email Attribute** textbox, type **emailaddress** of user **BrittaSimon@contoso.com**.</span></span>

    <span data-ttu-id="b5395-204">д.</span><span class="sxs-lookup"><span data-stu-id="b5395-204">e.</span></span> <span data-ttu-id="b5395-205">Нажмите кнопку **Сохранить изменения**.</span><span class="sxs-lookup"><span data-stu-id="b5395-205">Click **Save Changes**.</span></span>

12. <span data-ttu-id="b5395-206">Щелкните **Your IDP Metadata** (Метаданные вашего поставщика удостоверений), а затем в разделе **Your IDP Metadata** (Метаданные вашего поставщика удостоверений) сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="b5395-206">Click **Your IDP Metadata**, and then, in the **Your IDP Metadata** section, perform the following steps:</span></span>
   
    <span data-ttu-id="b5395-207">![Конфигурация единого входа](./media/active-directory-saas-policystat-tutorial/ic808636.png "Конфигурация единого входа")</span><span class="sxs-lookup"><span data-stu-id="b5395-207">![Single Sign-On Configuration](./media/active-directory-saas-policystat-tutorial/ic808636.png "Single Sign-On Configuration")</span></span>
   
    <span data-ttu-id="b5395-208">а.</span><span class="sxs-lookup"><span data-stu-id="b5395-208">a.</span></span> <span data-ttu-id="b5395-209">Откройте скачанный файл метаданных, скопируйте его содержимое и вставьте его в текстовое поле **Your Identity Provider Metadata** (Метаданные поставщика удостоверений).</span><span class="sxs-lookup"><span data-stu-id="b5395-209">Open your downloaded metadata file, copy the content, and  then paste it into the **Your Identity Provider Metadata** textbox.</span></span>

    <span data-ttu-id="b5395-210">b.</span><span class="sxs-lookup"><span data-stu-id="b5395-210">b.</span></span> <span data-ttu-id="b5395-211">Нажмите кнопку **Сохранить изменения**.</span><span class="sxs-lookup"><span data-stu-id="b5395-211">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="b5395-212">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="b5395-212">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b5395-213">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="b5395-213">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b5395-214">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="b5395-214">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b5395-215">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="b5395-215">Creating an Azure AD test user</span></span>
<span data-ttu-id="b5395-216">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b5395-216">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="b5395-218">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="b5395-218">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b5395-219">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b5395-219">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-policystat-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b5395-221">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="b5395-221">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-policystat-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b5395-223">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="b5395-223">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-policystat-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b5395-225">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="b5395-225">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-policystat-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b5395-227">а.</span><span class="sxs-lookup"><span data-stu-id="b5395-227">a.</span></span> <span data-ttu-id="b5395-228">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b5395-228">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b5395-229">b.</span><span class="sxs-lookup"><span data-stu-id="b5395-229">b.</span></span> <span data-ttu-id="b5395-230">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b5395-230">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b5395-231">c.</span><span class="sxs-lookup"><span data-stu-id="b5395-231">c.</span></span> <span data-ttu-id="b5395-232">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="b5395-232">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b5395-233">d.</span><span class="sxs-lookup"><span data-stu-id="b5395-233">d.</span></span> <span data-ttu-id="b5395-234">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="b5395-234">Click **Create**.</span></span>
 
### <a name="creating-a-policystat-test-user"></a><span data-ttu-id="b5395-235">Создание тестового пользователя PolicyStat</span><span class="sxs-lookup"><span data-stu-id="b5395-235">Creating a PolicyStat test user</span></span>

<span data-ttu-id="b5395-236">Чтобы пользователи Azure AD могли выполнять вход в PolicyStat, они должны быть подготовлены для PolicyStat.</span><span class="sxs-lookup"><span data-stu-id="b5395-236">In order to enable Azure AD users to log into PolicyStat, they must be provisioned into PolicyStat.</span></span>  

<span data-ttu-id="b5395-237">PolicyStat поддерживает подготовку пользователей «на лету».</span><span class="sxs-lookup"><span data-stu-id="b5395-237">PolicyStat supports just in time user provisioning.</span></span> <span data-ttu-id="b5395-238">Это означает, что вам не надо вручную добавлять пользователей PolicyStat.</span><span class="sxs-lookup"><span data-stu-id="b5395-238">This means, you do not need to add the users manually to PolicyStat.</span></span> <span data-ttu-id="b5395-239">Пользователи будут добавляться автоматически при первом входе с помощью единого входа.</span><span class="sxs-lookup"><span data-stu-id="b5395-239">The users will get added automatically on their first login through SSO.</span></span>

>[!NOTE]
><span data-ttu-id="b5395-240">Вы можете использовать любые другие инструменты создания учетных записей пользователя PolicyStat или API, предоставляемые PolicyStat для подготовки учетных записей пользователя Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b5395-240">You can use any other PolicyStat user account creation tools or APIs provided by PolicyStat to provision Azure AD user accounts.</span></span>
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b5395-241">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="b5395-241">Assigning the Azure AD test user</span></span>

<span data-ttu-id="b5395-242">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к PolicyStat.</span><span class="sxs-lookup"><span data-stu-id="b5395-242">In this section, you enable Britta Simon to use Azure single sign-on by granting access to PolicyStat.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="b5395-244">**Чтобы назначить пользователя Britta Simon в PolicyStat, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="b5395-244">**To assign Britta Simon to PolicyStat, perform the following steps:**</span></span>

1. <span data-ttu-id="b5395-245">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="b5395-245">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="b5395-247">Из списка приложений выберите **PolicyStat**.</span><span class="sxs-lookup"><span data-stu-id="b5395-247">In the applications list, select **PolicyStat**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-policystat-tutorial/tutorial_policystat_app.png) 

3. <span data-ttu-id="b5395-249">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="b5395-249">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="b5395-251">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="b5395-251">Click **Add** button.</span></span> <span data-ttu-id="b5395-252">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="b5395-252">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="b5395-254">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="b5395-254">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b5395-255">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="b5395-255">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b5395-256">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="b5395-256">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b5395-257">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="b5395-257">Testing single sign-on</span></span>

<span data-ttu-id="b5395-258">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="b5395-258">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b5395-259">Щелкнув элемент "PolicyStat" на панели доступа, вы автоматически войдете в приложение PolicyStat.</span><span class="sxs-lookup"><span data-stu-id="b5395-259">When you click the PolicyStat tile in the Access Panel, you should get automatically signed-on to your PolicyStat application.</span></span>
<span data-ttu-id="b5395-260">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b5395-260">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b5395-261">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="b5395-261">Additional resources</span></span>

* [<span data-ttu-id="b5395-262">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b5395-262">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b5395-263">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b5395-263">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-policystat-tutorial/tutorial_general_203.png

