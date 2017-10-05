---
title: "Руководство по интеграции Azure Active Directory с SAML SSO for Jira by resolution GmbH | Документация Майкрософт"
description: "Узнайте, как настроить единый вход для Azure Active Directory и SAML SSO for Jira by resolution GmbH."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 20e18819-e330-4e40-bd8d-2ff3b98e035f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: jeedes
ms.openlocfilehash: cde5983710185d1e46a5601b16bbfb1c0fcae382
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-saml-sso-for-jira-by-resolution-gmbh"></a><span data-ttu-id="6b026-103">Руководство по интеграции Azure Active Directory с SAML SSO for Jira by resolution GmbH</span><span class="sxs-lookup"><span data-stu-id="6b026-103">Tutorial: Azure Active Directory integration with SAML SSO for Jira by resolution GmbH</span></span>

<span data-ttu-id="6b026-104">В этом руководстве описано, как интегрировать SAML SSO for Jira by resolution GmbH с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6b026-104">In this tutorial, you learn how to integrate SAML SSO for Jira by resolution GmbH with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="6b026-105">Интеграция SAML SSO for Jira by resolution GmbH с Azure AD предоставляет следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="6b026-105">Integrating SAML SSO for Jira by resolution GmbH with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="6b026-106">Можно управлять доступом пользователей Azure AD к SAML SSO for Jira by resolution GmbH.</span><span class="sxs-lookup"><span data-stu-id="6b026-106">You can control in Azure AD who has access to SAML SSO for Jira by resolution GmbH</span></span>
- <span data-ttu-id="6b026-107">Можно включить автоматический вход пользователей в SAML SSO for Jira by resolution GmbH (единый вход) с учетными записями Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6b026-107">You can enable your users to automatically get signed-on to SAML SSO for Jira by resolution GmbH (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="6b026-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="6b026-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="6b026-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="6b026-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6b026-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="6b026-110">Prerequisites</span></span>

<span data-ttu-id="6b026-111">Для настройки интеграции Azure AD с SAML SSO for Jira by resolution GmbH требуется:</span><span class="sxs-lookup"><span data-stu-id="6b026-111">To configure Azure AD integration with SAML SSO for Jira by resolution GmbH, you need the following items:</span></span>

- <span data-ttu-id="6b026-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="6b026-112">An Azure AD subscription</span></span>
- <span data-ttu-id="6b026-113">подписка SAML SSO for Jira by resolution GmbH с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="6b026-113">A SAML SSO for Jira by resolution GmbH single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="6b026-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="6b026-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="6b026-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="6b026-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="6b026-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="6b026-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="6b026-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="6b026-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="6b026-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="6b026-118">Scenario description</span></span>
<span data-ttu-id="6b026-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="6b026-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="6b026-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="6b026-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="6b026-121">Добавление SAML SSO for Jira by resolution GmbH из коллекции</span><span class="sxs-lookup"><span data-stu-id="6b026-121">Adding SAML SSO for Jira by resolution GmbH from the gallery</span></span>
2. <span data-ttu-id="6b026-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="6b026-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-saml-sso-for-jira-by-resolution-gmbh-from-the-gallery"></a><span data-ttu-id="6b026-123">Добавление SAML SSO for Jira by resolution GmbH из коллекции</span><span class="sxs-lookup"><span data-stu-id="6b026-123">Adding SAML SSO for Jira by resolution GmbH from the gallery</span></span>
<span data-ttu-id="6b026-124">Чтобы настроить интеграцию SAML SSO for Jira by resolution GmbH в Azure AD, необходимо добавить SAML SSO for Jira by resolution GmbH из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="6b026-124">To configure the integration of SAML SSO for Jira by resolution GmbH into Azure AD, you need to add SAML SSO for Jira by resolution GmbH from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="6b026-125">**Чтобы добавить SAML SSO for Jira by resolution GmbH из коллекции, выполните следующее.**</span><span class="sxs-lookup"><span data-stu-id="6b026-125">**To add SAML SSO for Jira by resolution GmbH from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="6b026-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6b026-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="6b026-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="6b026-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="6b026-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="6b026-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="6b026-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="6b026-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="6b026-133">В поле поиска введите **SAML SSO for Jira by resolution GmbH**.</span><span class="sxs-lookup"><span data-stu-id="6b026-133">In the search box, type **SAML SSO for Jira by resolution GmbH**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_search.png)

5. <span data-ttu-id="6b026-135">На панели результатов выберите **SAML SSO for Jira by resolution GmbH** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="6b026-135">In the results panel, select **SAML SSO for Jira by resolution GmbH**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="6b026-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="6b026-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="6b026-138">В этом разделе описана настройка и проверка единого входа Azure AD в SAML SSO for Jira by resolution GmbH с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6b026-138">In this section, you configure and test Azure AD single sign-on with SAML SSO for Jira by resolution GmbH based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="6b026-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в SAML SSO for Jira by resolution GmbH соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6b026-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SAML SSO for Jira by resolution GmbH is to a user in Azure AD.</span></span> <span data-ttu-id="6b026-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в SAML SSO for Jira by resolution GmbH.</span><span class="sxs-lookup"><span data-stu-id="6b026-140">In other words, a link relationship between an Azure AD user and the related user in SAML SSO for Jira by resolution GmbH needs to be established.</span></span>

<span data-ttu-id="6b026-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в SAML SSO for Jira by resolution GmbH.</span><span class="sxs-lookup"><span data-stu-id="6b026-141">In SAML SSO for Jira by resolution GmbH, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="6b026-142">Чтобы настроить и проверить единый вход Azure AD в SAML SSO for Jira by resolution GmbH, требуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="6b026-142">To configure and test Azure AD single sign-on with SAML SSO for Jira by resolution GmbH, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="6b026-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="6b026-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="6b026-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6b026-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="6b026-145">**[Создание тестового пользователя SAML SSO for Jira by resolution GmbH](#creating-a-saml-sso-for-jira-by-resolution-gmbh-test-user)** требуется, чтобы создать в SAML SSO for Jira by resolution GmbH пользователя Britta Simon, связанного с соответствующим пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6b026-145">**[Creating a SAML SSO for Jira by resolution GmbH test user](#creating-a-saml-sso-for-jira-by-resolution-gmbh-test-user)** - to have a counterpart of Britta Simon in SAML SSO for Jira by resolution GmbH that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="6b026-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6b026-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="6b026-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="6b026-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="6b026-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="6b026-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="6b026-149">В данном разделе описано, как включить единый вход в Azure AD на портале Azure и настроить его в приложении SAML SSO for Jira by resolution GmbH.</span><span class="sxs-lookup"><span data-stu-id="6b026-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SAML SSO for Jira by resolution GmbH application.</span></span>

<span data-ttu-id="6b026-150">**Чтобы настроить единый вход Azure AD в SAML SSO for Jira by resolution GmbH, выполните следующее.**</span><span class="sxs-lookup"><span data-stu-id="6b026-150">**To configure Azure AD single sign-on with SAML SSO for Jira by resolution GmbH, perform the following steps:**</span></span>

1. <span data-ttu-id="6b026-151">На портале Azure на странице интеграции с приложением **SAML SSO for Jira by resolution GmbH** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="6b026-151">In the Azure portal, on the **SAML SSO for Jira by resolution GmbH** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="6b026-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="6b026-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_samlbase.png)

3. <span data-ttu-id="6b026-155">Если вы хотите настроить приложение в режиме, инициированном **IdP**, то в разделе **Домены и URL-адреса приложения SAML SSO for Jira by resolution GmbH** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="6b026-155">On the **SAML SSO for Jira by resolution GmbH Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_url_1.png)

    <span data-ttu-id="6b026-157">а.</span><span class="sxs-lookup"><span data-stu-id="6b026-157">a.</span></span> <span data-ttu-id="6b026-158">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="6b026-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>

    <span data-ttu-id="6b026-159">b.</span><span class="sxs-lookup"><span data-stu-id="6b026-159">b.</span></span> <span data-ttu-id="6b026-160">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате: `https://<server-base-url>/plugins/servlet/samlsso`.</span><span class="sxs-lookup"><span data-stu-id="6b026-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>

4. <span data-ttu-id="6b026-161">Установите флажок **Показать дополнительные параметры URL-адресов**,</span><span class="sxs-lookup"><span data-stu-id="6b026-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="6b026-162">если хотите настроить приложение для работы в режиме, инициируемом **поставщиком услуг**.</span><span class="sxs-lookup"><span data-stu-id="6b026-162">If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_url_2.png)

    <span data-ttu-id="6b026-164">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<server-base-url>/plugins/servlet/samlsso`</span><span class="sxs-lookup"><span data-stu-id="6b026-164">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/samlsso`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="6b026-165">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="6b026-165">These values are not real.</span></span> <span data-ttu-id="6b026-166">Замените их фактическими значениями идентификатора, URL-адреса ответа и URL-адреса входа.</span><span class="sxs-lookup"><span data-stu-id="6b026-166">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="6b026-167">Обратитесь к [группе поддержки SAML SSO for Jira by resolution GmbH](https://www.resolution.de/go/support) для получения этих значений.</span><span class="sxs-lookup"><span data-stu-id="6b026-167">Contact [SAML SSO for Jira by resolution GmbH Client support team](https://www.resolution.de/go/support) to get these values.</span></span> 

5. <span data-ttu-id="6b026-168">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="6b026-168">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_certificate.png) 

6. <span data-ttu-id="6b026-170">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="6b026-170">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-samlssojira-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="6b026-172">В другом окне браузера войдите на **портал администрирования SAML SSO for Jira by resolution GmbH** с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="6b026-172">In a different web browser window, log in to your **SAML SSO for Jira by resolution GmbH admin portal** as an administrator.</span></span>

8. <span data-ttu-id="6b026-173">Наведите указатель мыши на шестеренку и щелкните **Add-ons** (Надстройки).</span><span class="sxs-lookup"><span data-stu-id="6b026-173">Hover on cog and click the **Add-ons**.</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-samlssojira-tutorial/addon1.png)

9. <span data-ttu-id="6b026-175">Вы перейдете на страницу доступа с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="6b026-175">You are redirected to Administrator Access page.</span></span> <span data-ttu-id="6b026-176">Введите **пароль** и нажмите кнопку **Confirm** (Подтвердить).</span><span class="sxs-lookup"><span data-stu-id="6b026-176">Enter the **Password** and click **Confirm** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-samlssojira-tutorial/addon2.png)

10. <span data-ttu-id="6b026-178">На вкладке "Add-ons" (Надстройки) щелкните **Find new add-ons** (Найти новые надстройки).</span><span class="sxs-lookup"><span data-stu-id="6b026-178">Under Add-ons tab section, click **Find new add-ons**.</span></span> <span data-ttu-id="6b026-179">Найдите подключаемый модуль **SAML Single Sign On (SSO) for Jira** и нажмите кнопку **Install** (Установить), чтобы установить новый подключаемый модуль SAML.</span><span class="sxs-lookup"><span data-stu-id="6b026-179">Search **SAML Single Sign On (SSO) for JIRA** and click **Install** button to install the new SAML plugin.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-samlssojira-tutorial/addon7.png)

11. <span data-ttu-id="6b026-181">Начнется установка подключаемого модуля.</span><span class="sxs-lookup"><span data-stu-id="6b026-181">The plugin installation will start.</span></span> <span data-ttu-id="6b026-182">Нажмите кнопку **Закрыть**</span><span class="sxs-lookup"><span data-stu-id="6b026-182">Click **Close**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-samlssojira-tutorial/addon8.png)

    ![Настройка единого входа](./media/active-directory-saas-samlssojira-tutorial/addon9.png)

12. <span data-ttu-id="6b026-185">Нажмите кнопку **Управление**.</span><span class="sxs-lookup"><span data-stu-id="6b026-185">Click **Manage**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-samlssojira-tutorial/addon10.png)
    
13. <span data-ttu-id="6b026-187">Щелкните **Configure** (Настройка), чтобы настроить новый подключаемый модуль.</span><span class="sxs-lookup"><span data-stu-id="6b026-187">Click **Configure** to configure the new plugin.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-samlssojira-tutorial/addon11.png)

14. <span data-ttu-id="6b026-189">На странице **SAML SingleSignOn Plugin Configuration** (Конфигурация подключаемого модуля единого входа SAML) нажмите кнопку **Add additional Identity Provider** (Добавить дополнительный поставщик удостоверений), чтобы настроить параметры поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="6b026-189">On **SAML SingleSignOn Plugin Configuration** page, click **Add additional Identity Provider** button to configure the settings of Identity Provider.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-samlssojira-tutorial/addon4.png)

15. <span data-ttu-id="6b026-191">На этой странице сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="6b026-191">Perform following steps on this page:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-samlssojira-tutorial/addon5.png)
 
    <span data-ttu-id="6b026-193">а.</span><span class="sxs-lookup"><span data-stu-id="6b026-193">a.</span></span> <span data-ttu-id="6b026-194">Добавьте **имя** поставщика удостоверений (например, Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6b026-194">Add **Name** of the Identity Provider (e.g Azure AD).</span></span>
    
    <span data-ttu-id="6b026-195">b.</span><span class="sxs-lookup"><span data-stu-id="6b026-195">b.</span></span> <span data-ttu-id="6b026-196">Добавьте **описание** поставщика удостоверений (например, Azure AD).</span><span class="sxs-lookup"><span data-stu-id="6b026-196">Add **Description** of the Identity Provider (e.g Azure AD).</span></span>

    <span data-ttu-id="6b026-197">c.</span><span class="sxs-lookup"><span data-stu-id="6b026-197">c.</span></span> <span data-ttu-id="6b026-198">Щелкните **XML** и выберите файл **метаданных**, скачанный с портала Azure.</span><span class="sxs-lookup"><span data-stu-id="6b026-198">Click **XML** and select the **Metadata** file, which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="6b026-199">г)</span><span class="sxs-lookup"><span data-stu-id="6b026-199">d.</span></span> <span data-ttu-id="6b026-200">Нажмите кнопку **Load** (Загрузить).</span><span class="sxs-lookup"><span data-stu-id="6b026-200">Click **Load** button.</span></span>

    <span data-ttu-id="6b026-201">д.</span><span class="sxs-lookup"><span data-stu-id="6b026-201">e.</span></span> <span data-ttu-id="6b026-202">Будут считаны метаданные поставщика удостоверений и заполнены поля, как показано на снимке экрана.</span><span class="sxs-lookup"><span data-stu-id="6b026-202">It reads the IdP metadata and populates the fields as highlighted in the screenshot.</span></span> 

16. <span data-ttu-id="6b026-203">Нажмите кнопку **Save settings** (Сохранить параметры), чтобы сохранить параметры.</span><span class="sxs-lookup"><span data-stu-id="6b026-203">Click **Save settings** button to save the settings.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-samlssojira-tutorial/addon6.png)

> [!TIP]
> <span data-ttu-id="6b026-205">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="6b026-205">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="6b026-206">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="6b026-206">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="6b026-207">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="6b026-207">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="6b026-208">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="6b026-208">Creating an Azure AD test user</span></span>
<span data-ttu-id="6b026-209">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6b026-209">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="6b026-211">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="6b026-211">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="6b026-212">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="6b026-212">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="6b026-214">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="6b026-214">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="6b026-216">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="6b026-216">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="6b026-218">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="6b026-218">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-samlssojira-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="6b026-220">а.</span><span class="sxs-lookup"><span data-stu-id="6b026-220">a.</span></span> <span data-ttu-id="6b026-221">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="6b026-221">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="6b026-222">b.</span><span class="sxs-lookup"><span data-stu-id="6b026-222">b.</span></span> <span data-ttu-id="6b026-223">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="6b026-223">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="6b026-224">c.</span><span class="sxs-lookup"><span data-stu-id="6b026-224">c.</span></span> <span data-ttu-id="6b026-225">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="6b026-225">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="6b026-226">d.</span><span class="sxs-lookup"><span data-stu-id="6b026-226">d.</span></span> <span data-ttu-id="6b026-227">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="6b026-227">Click **Create**.</span></span>
 
### <a name="creating-a-saml-sso-for-jira-by-resolution-gmbh-test-user"></a><span data-ttu-id="6b026-228">Создание тестового пользователя SAML SSO for Jira by resolution GmbH</span><span class="sxs-lookup"><span data-stu-id="6b026-228">Creating a SAML SSO for Jira by resolution GmbH test user</span></span>

<span data-ttu-id="6b026-229">Чтобы пользователи Azure AD могли входить в SAML SSO for Jira by resolution GmbH, их необходимо подготовить в SAML SSO for Jira by resolution GmbH.</span><span class="sxs-lookup"><span data-stu-id="6b026-229">To enable Azure AD users to log in to SAML SSO for Jira by resolution GmbH, they must be provisioned into SAML SSO for Jira by resolution GmbH.</span></span>  
<span data-ttu-id="6b026-230">Подготовка в SAML SSO for Jira by resolution GmbH выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="6b026-230">In SAML SSO for Jira by resolution GmbH, provisioning is a manual task.</span></span>

<span data-ttu-id="6b026-231">**Чтобы подготовить учетную запись пользователя, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="6b026-231">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="6b026-232">Войдите на свой корпоративный сайт SAML SSO for Jira by resolution GmbH с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="6b026-232">Log in to your SAML SSO for Jira by resolution GmbH company site as an administrator.</span></span>

2. <span data-ttu-id="6b026-233">Наведите указатель мыши на шестеренку и щелкните **User management** (Управление пользователями).</span><span class="sxs-lookup"><span data-stu-id="6b026-233">Hover on cog and click the **User management**.</span></span>

    ![Добавление сотрудника](./media/active-directory-saas-samlssojira-tutorial/user1.png) 

3. <span data-ttu-id="6b026-235">Вы будете перенаправлены на страницу доступа с правами администратора. Введите **пароль** и нажмите кнопку **Confirm** (Подтвердить).</span><span class="sxs-lookup"><span data-stu-id="6b026-235">You are redirected to Administrator Access page to enter **Password** and click **Confirm** button.</span></span>

    ![Добавление сотрудника](./media/active-directory-saas-samlssojira-tutorial/user2.png) 

4. <span data-ttu-id="6b026-237">В разделе **User management** (Управление пользователями) щелкните **Create user** (Создать пользователя).</span><span class="sxs-lookup"><span data-stu-id="6b026-237">Under **User management** tab section, click **create user**.</span></span>

    ![Добавление сотрудника](./media/active-directory-saas-samlssojira-tutorial/user3.png) 

5. <span data-ttu-id="6b026-239">На странице **Create New User** (Создание пользователя) выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="6b026-239">On the **“Create new user”** dialog page, perform the following steps:</span></span>

    ![Добавление сотрудника](./media/active-directory-saas-samlssojira-tutorial/user4.png) 

    <span data-ttu-id="6b026-241">а.</span><span class="sxs-lookup"><span data-stu-id="6b026-241">a.</span></span> <span data-ttu-id="6b026-242">В текстовом поле **Email address** (Адрес электронной почты) введите адрес электронной почты пользователя, например Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="6b026-242">In the **Email address** textbox, type the email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="6b026-243">b.</span><span class="sxs-lookup"><span data-stu-id="6b026-243">b.</span></span> <span data-ttu-id="6b026-244">В текстовом поле **Full Name** (Полное имя) введите полное имя пользователя, например Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="6b026-244">In the **Full Name** textbox, type full name of the user like Britta Simon.</span></span>

    <span data-ttu-id="6b026-245">c.</span><span class="sxs-lookup"><span data-stu-id="6b026-245">c.</span></span> <span data-ttu-id="6b026-246">В текстовом поле **Username** (Имя пользователя) введите электронный адрес пользователя, например Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="6b026-246">In the **Username** textbox, type the email of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="6b026-247">г)</span><span class="sxs-lookup"><span data-stu-id="6b026-247">d.</span></span> <span data-ttu-id="6b026-248">В текстовом поле **Password** (Пароль) введите пароль пользователя.</span><span class="sxs-lookup"><span data-stu-id="6b026-248">In the **Password** textbox, type the password of user.</span></span>

    <span data-ttu-id="6b026-249">д.</span><span class="sxs-lookup"><span data-stu-id="6b026-249">e.</span></span> <span data-ttu-id="6b026-250">Щелкните **Create user** (Создать пользователя).</span><span class="sxs-lookup"><span data-stu-id="6b026-250">Click **Create user**.</span></span>   

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="6b026-251">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="6b026-251">Assigning the Azure AD test user</span></span>

<span data-ttu-id="6b026-252">В этом разделе описано, как позволить пользователю Britta Simon использовать единый вход Azure путем предоставления доступа к SAML SSO for Jira by resolution GmbH.</span><span class="sxs-lookup"><span data-stu-id="6b026-252">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SAML SSO for Jira by resolution GmbH.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="6b026-254">**Чтобы назначить пользователя Britta Simon в SAML SSO for Jira by resolution GmbH, выполните следующее.**</span><span class="sxs-lookup"><span data-stu-id="6b026-254">**To assign Britta Simon to SAML SSO for Jira by resolution GmbH, perform the following steps:**</span></span>

1. <span data-ttu-id="6b026-255">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="6b026-255">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="6b026-257">Из списка приложений выберите **SAML SSO for Jira by resolution GmbH**.</span><span class="sxs-lookup"><span data-stu-id="6b026-257">In the applications list, select **SAML SSO for Jira by resolution GmbH**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-samlssojira-tutorial/tutorial_samlssojira_app.png) 

3. <span data-ttu-id="6b026-259">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="6b026-259">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="6b026-261">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="6b026-261">Click **Add** button.</span></span> <span data-ttu-id="6b026-262">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="6b026-262">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="6b026-264">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="6b026-264">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="6b026-265">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="6b026-265">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="6b026-266">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="6b026-266">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="6b026-267">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="6b026-267">Testing single sign-on</span></span>

<span data-ttu-id="6b026-268">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="6b026-268">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="6b026-269">Щелкнув элемент SAML SSO for Jira by resolution GmbH на панели доступа, вы должны автоматически войти в свое приложение SAML SSO for Jira by resolution GmbH.</span><span class="sxs-lookup"><span data-stu-id="6b026-269">When you click the SAML SSO for Jira by resolution GmbH tile in the Access Panel, you should get automatically signed-on to your SAML SSO for Jira by resolution GmbH application.</span></span>
<span data-ttu-id="6b026-270">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6b026-270">For more information about the Access Panel, see [introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="6b026-271">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="6b026-271">Additional resources</span></span>

* [<span data-ttu-id="6b026-272">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6b026-272">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="6b026-273">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="6b026-273">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-samlssojira-tutorial/tutorial_general_203.png

