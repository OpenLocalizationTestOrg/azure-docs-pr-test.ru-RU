---
title: "Руководство по интеграции Azure Active Directory с Kantega SSO for Bamboo | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в Kantega SSO for Bamboo."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e238b574-9e9b-43b7-ab98-d2a87ff89d48
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: cc259bb6f9bdb2293b6935e45e2df52b9fee6873
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kantega-sso-for-bamboo"></a><span data-ttu-id="3ca98-103">Руководство по интеграции Azure Active Directory с Kantega SSO for Bamboo</span><span class="sxs-lookup"><span data-stu-id="3ca98-103">Tutorial: Azure Active Directory integration with Kantega SSO for Bamboo</span></span>

<span data-ttu-id="3ca98-104">В этом руководстве описано, как интегрировать Kantega SSO for Bamboo с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3ca98-104">In this tutorial, you learn how to integrate Kantega SSO for Bamboo with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="3ca98-105">Интеграция Azure AD с приложением Kantega SSO for Bamboo обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="3ca98-105">Integrating Kantega SSO for Bamboo with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="3ca98-106">С помощью Azure AD вы можете контролировать доступ к Kantega SSO for Bamboo.</span><span class="sxs-lookup"><span data-stu-id="3ca98-106">You can control in Azure AD who has access to Kantega SSO for Bamboo</span></span>
- <span data-ttu-id="3ca98-107">Вы можете включить автоматический вход пользователей в Kantega SSO for Bamboo (единый вход) с использованием учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3ca98-107">You can enable your users to automatically get signed-on to Kantega SSO for Bamboo (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="3ca98-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="3ca98-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="3ca98-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="3ca98-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3ca98-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="3ca98-110">Prerequisites</span></span>

<span data-ttu-id="3ca98-111">Чтобы настроить интеграцию Azure AD с Kantega SSO for Bamboo, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="3ca98-111">To configure Azure AD integration with Kantega SSO for Bamboo, you need the following items:</span></span>

- <span data-ttu-id="3ca98-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="3ca98-112">An Azure AD subscription</span></span>
- <span data-ttu-id="3ca98-113">подписка Kantega SSO for Bamboo с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="3ca98-113">A Kantega SSO for Bamboo single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="3ca98-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="3ca98-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="3ca98-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="3ca98-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="3ca98-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="3ca98-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="3ca98-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3ca98-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="3ca98-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="3ca98-118">Scenario description</span></span>
<span data-ttu-id="3ca98-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="3ca98-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="3ca98-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="3ca98-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="3ca98-121">Добавление Kantega SSO for Bamboo из коллекции.</span><span class="sxs-lookup"><span data-stu-id="3ca98-121">Adding Kantega SSO for Bamboo from the gallery</span></span>
2. <span data-ttu-id="3ca98-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="3ca98-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kantega-sso-for-bamboo-from-the-gallery"></a><span data-ttu-id="3ca98-123">Добавление Kantega SSO for Bamboo из коллекции</span><span class="sxs-lookup"><span data-stu-id="3ca98-123">Adding Kantega SSO for Bamboo from the gallery</span></span>
<span data-ttu-id="3ca98-124">Чтобы настроить интеграцию Kantega SSO for Bamboo с Azure AD, необходимо добавить Kantega SSO for Bamboo из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="3ca98-124">To configure the integration of Kantega SSO for Bamboo into Azure AD, you need to add Kantega SSO for Bamboo from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="3ca98-125">**Чтобы добавить Kantega SSO for Bamboo из коллекции, сделайте следующее.**</span><span class="sxs-lookup"><span data-stu-id="3ca98-125">**To add Kantega SSO for Bamboo from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="3ca98-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3ca98-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="3ca98-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="3ca98-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="3ca98-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="3ca98-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="3ca98-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="3ca98-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="3ca98-133">В поле поиска введите **Kantega SSO for Bamboo**.</span><span class="sxs-lookup"><span data-stu-id="3ca98-133">In the search box, type **Kantega SSO for Bamboo**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_search.png)

5. <span data-ttu-id="3ca98-135">На панели результатов выберите **Kantega SSO for Bamboo** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="3ca98-135">In the results panel, select **Kantega SSO for Bamboo**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="3ca98-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="3ca98-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="3ca98-138">В этом разделе описана настройка и проверка единого входа Azure AD в Kantega SSO for Bamboo с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3ca98-138">In this section, you configure and test Azure AD single sign-on with Kantega SSO for Bamboo based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="3ca98-139">Чтобы единый вход работал, Azure AD необходима информация о том, какой пользователь в Kantega SSO for Bamboo соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3ca98-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Kantega SSO for Bamboo is to a user in Azure AD.</span></span> <span data-ttu-id="3ca98-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Kantega SSO for Bamboo.</span><span class="sxs-lookup"><span data-stu-id="3ca98-140">In other words, a link relationship between an Azure AD user and the related user in Kantega SSO for Bamboo needs to be established.</span></span>

<span data-ttu-id="3ca98-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Kantega SSO for Bamboo.</span><span class="sxs-lookup"><span data-stu-id="3ca98-141">In Kantega SSO for Bamboo, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="3ca98-142">Чтобы настроить и проверить единый вход Azure AD в Kantega SSO for Bamboo, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="3ca98-142">To configure and test Azure AD single sign-on with Kantega SSO for Bamboo, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="3ca98-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="3ca98-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="3ca98-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3ca98-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="3ca98-145">**[Создание тестового пользователя Kantega SSO for Bamboo](#creating-a-kantega-sso-for-bamboo-test-user)** требуется для того, чтобы в Kantega SSO for Bamboo существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3ca98-145">**[Creating a Kantega SSO for Bamboo test user](#creating-a-kantega-sso-for-bamboo-test-user)** - to have a counterpart of Britta Simon in Kantega SSO for Bamboo that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="3ca98-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3ca98-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="3ca98-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="3ca98-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="3ca98-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="3ca98-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="3ca98-149">В данном разделе описано, как включить единый вход в Azure AD на портале Azure и настроить его в приложении Kantega SSO for Bamboo.</span><span class="sxs-lookup"><span data-stu-id="3ca98-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Kantega SSO for Bamboo application.</span></span>

<span data-ttu-id="3ca98-150">**Чтобы настроить единый вход Azure AD в Kantega SSO for Bamboo, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="3ca98-150">**To configure Azure AD single sign-on with Kantega SSO for Bamboo, perform the following steps:**</span></span>

1. <span data-ttu-id="3ca98-151">На портале Azure на странице интеграции с приложением **Kantega SSO for Bamboo** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="3ca98-151">In the Azure portal, on the **Kantega SSO for Bamboo** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="3ca98-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="3ca98-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_samlbase.png)

3. <span data-ttu-id="3ca98-155">Чтобы использовать режим, инициируемый **IdP**, в разделе **Домены и URL-адреса приложения Kantega SSO for Bamboo** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="3ca98-155">In **IDP** initiated mode, on the **Kantega SSO for Bamboo Domain and URLs** section perform the following step :</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_url1.png)
    
    <span data-ttu-id="3ca98-157">а.</span><span class="sxs-lookup"><span data-stu-id="3ca98-157">a.</span></span> <span data-ttu-id="3ca98-158">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="3ca98-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

    <span data-ttu-id="3ca98-159">b.</span><span class="sxs-lookup"><span data-stu-id="3ca98-159">b.</span></span> <span data-ttu-id="3ca98-160">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`.</span><span class="sxs-lookup"><span data-stu-id="3ca98-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

4. <span data-ttu-id="3ca98-161">Чтобы использовать режим, инициируемый **поставщиком услуг**, установите флажок **Показать дополнительные параметры URL-адресов**.</span><span class="sxs-lookup"><span data-stu-id="3ca98-161">In **SP** initiated mode, check **Show advanced URL settings** and  perform the following step :</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_url2.png)
    
    <span data-ttu-id="3ca98-163">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="3ca98-163">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="3ca98-164">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="3ca98-164">These values are not real.</span></span> <span data-ttu-id="3ca98-165">Замените их фактическими значениями идентификатора, URL-адреса ответа и URL-адреса входа.</span><span class="sxs-lookup"><span data-stu-id="3ca98-165">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="3ca98-166">Эти значения предоставляются во время настройки подключаемого модуля Bamboo, которая описывается далее в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="3ca98-166">These values are recieved during the configuration of Bamboo plugin which is explained later in the tutorial.</span></span>

5. <span data-ttu-id="3ca98-167">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="3ca98-167">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_certificate.png) 

6. <span data-ttu-id="3ca98-169">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="3ca98-169">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="3ca98-171">В другом окне веб-браузера войдите на свой локальный сервер Bamboo в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="3ca98-171">In a different web browser window, log in to your Bamboo  on premise server as an administrator.</span></span>

8. <span data-ttu-id="3ca98-172">Наведите указатель мыши на шестеренку и щелкните **Add-ons** (Надстройки).</span><span class="sxs-lookup"><span data-stu-id="3ca98-172">Hover on cog and click the **Add-ons**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon1.png)

9. <span data-ttu-id="3ca98-174">На вкладке "Add-ons" (Надстройки) щелкните **Find new add-ons** (Найти новые надстройки).</span><span class="sxs-lookup"><span data-stu-id="3ca98-174">Under Add-ons tab section, click **Find new add-ons**.</span></span> <span data-ttu-id="3ca98-175">Найдите подключаемый модуль **Kantega SSO for Bamboo (SAML & Kerberos)** и нажмите кнопку **Install** (Установить), чтобы установить новый подключаемый модуль SAML.</span><span class="sxs-lookup"><span data-stu-id="3ca98-175">Search **Kantega SSO for Bamboo (SAML & Kerberos)** and click **Install** button to install the new SAML plugin.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon2.png)

10. <span data-ttu-id="3ca98-177">Начнется установка подключаемого модуля.</span><span class="sxs-lookup"><span data-stu-id="3ca98-177">The plugin installation will start.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon21.png)

11. <span data-ttu-id="3ca98-179">Установка завершится.</span><span class="sxs-lookup"><span data-stu-id="3ca98-179">Once the installation is complete.</span></span> <span data-ttu-id="3ca98-180">Нажмите кнопку **Закрыть**</span><span class="sxs-lookup"><span data-stu-id="3ca98-180">Click **Close**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon33.png)

12. <span data-ttu-id="3ca98-182">Нажмите кнопку **Управление**.</span><span class="sxs-lookup"><span data-stu-id="3ca98-182">Click **Manage**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon34.png)
    
13. <span data-ttu-id="3ca98-184">Щелкните **Configure** (Настройка), чтобы настроить новый подключаемый модуль.</span><span class="sxs-lookup"><span data-stu-id="3ca98-184">Click **Configure** to configure the new plugin.</span></span>    

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon3.png)

14. <span data-ttu-id="3ca98-186">В разделе **SAML** сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="3ca98-186">In the **SAML** section.</span></span> <span data-ttu-id="3ca98-187">Выберите **Azure Active Directory (Azure AD)** из раскрывающегося списка **Добавление поставщика удостоверений**.</span><span class="sxs-lookup"><span data-stu-id="3ca98-187">Select **Azure Active Directory (Azure AD)** from the **Add identity provider** dropdown.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon4.png)

15. <span data-ttu-id="3ca98-189">Выберите уровень подписки **Базовый**.</span><span class="sxs-lookup"><span data-stu-id="3ca98-189">Select subscription level as **Basic**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon5.png)

16. <span data-ttu-id="3ca98-191">В разделе **Свойства приложения** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="3ca98-191">On the **App properties** section, perform following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon6.png)

    <span data-ttu-id="3ca98-193">а.</span><span class="sxs-lookup"><span data-stu-id="3ca98-193">a.</span></span> <span data-ttu-id="3ca98-194">Скопируйте значение **App ID URI** (URI кода приложения) и используйте его как **идентификатор, URL-адрес ответа и URL-адрес входа** в разделе **Домены и URL-адреса приложения Kantega SSO for Bamboo** на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="3ca98-194">Copy the **App ID URI** value and use it as **Identifier, Reply URL, and Sign-On URL** on the **Kantega SSO for Bamboo Domain and URLs** section in Azure portal.</span></span>

    <span data-ttu-id="3ca98-195">b.</span><span class="sxs-lookup"><span data-stu-id="3ca98-195">b.</span></span> <span data-ttu-id="3ca98-196">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="3ca98-196">Click **Next**.</span></span>

17. <span data-ttu-id="3ca98-197">В разделе **Metadata import** (Импорт метаданных) выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="3ca98-197">On the **Metadata import** section, perform following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon7.png)

    <span data-ttu-id="3ca98-199">а.</span><span class="sxs-lookup"><span data-stu-id="3ca98-199">a.</span></span> <span data-ttu-id="3ca98-200">Щелкните **Metadata file on my computer** (Файл метаданных на моем компьютере) и передайте файл метаданных, который вы скачали с портала Azure.</span><span class="sxs-lookup"><span data-stu-id="3ca98-200">Select **Metadata file on my computer**, and upload metadata file, which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="3ca98-201">b.</span><span class="sxs-lookup"><span data-stu-id="3ca98-201">b.</span></span> <span data-ttu-id="3ca98-202">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="3ca98-202">Click **Next**.</span></span>

18. <span data-ttu-id="3ca98-203">В разделе **Name and SSO location** (Имя и расположение единого входа) выполните следующее.</span><span class="sxs-lookup"><span data-stu-id="3ca98-203">On the **Name and SSO location** section, perform following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon8.png)

    <span data-ttu-id="3ca98-205">а.</span><span class="sxs-lookup"><span data-stu-id="3ca98-205">a.</span></span> <span data-ttu-id="3ca98-206">В текстовом поле **Provider Name** (Имя поставщика) введите имя поставщика (например, Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3ca98-206">Add Name of the Identity Provider in **Identity provider name** textbox (e.g Azure AD).</span></span>

    <span data-ttu-id="3ca98-207">b.</span><span class="sxs-lookup"><span data-stu-id="3ca98-207">b.</span></span> <span data-ttu-id="3ca98-208">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="3ca98-208">Click **Next**.</span></span>

19. <span data-ttu-id="3ca98-209">Проверьте сертификат для подписи и нажмите кнопку **Next** (Далее).</span><span class="sxs-lookup"><span data-stu-id="3ca98-209">Verify the Signing certificate and click **Next**.</span></span>  

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon9.png)

20. <span data-ttu-id="3ca98-211">В разделе **Bamboo user accounts** (Учетные записи пользователей Bamboo) выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="3ca98-211">On the **Bamboo user accounts** section, perform following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon10.png)

    <span data-ttu-id="3ca98-213">а.</span><span class="sxs-lookup"><span data-stu-id="3ca98-213">a.</span></span> <span data-ttu-id="3ca98-214">Щелкните переключатель **Create users in Bamboo's internal Directory if needed** (При необходимости создать пользователей во внутреннем каталоге Bamboo) и введите соответствующее имя группы пользователей (это может быть несколько групп,</span><span class="sxs-lookup"><span data-stu-id="3ca98-214">Select **Create users in Bamboo's internal Directory if needed** and enter the appropriate name of the group for users (can be multiple no.</span></span> <span data-ttu-id="3ca98-215">разделенных запятой).</span><span class="sxs-lookup"><span data-stu-id="3ca98-215">of groups separated by comma).</span></span>

    <span data-ttu-id="3ca98-216">b.</span><span class="sxs-lookup"><span data-stu-id="3ca98-216">b.</span></span> <span data-ttu-id="3ca98-217">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="3ca98-217">Click **Next**.</span></span>

21. <span data-ttu-id="3ca98-218">Нажмите кнопку **Готово**</span><span class="sxs-lookup"><span data-stu-id="3ca98-218">Click **Finish**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon11.png)

22. <span data-ttu-id="3ca98-220">В разделе **Known domains for Azure AD** (Известные домены для Azure AD) выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="3ca98-220">On the **Known domains for Azure AD** section, perform following steps:</span></span> 

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforbamboo-tutorial/addon12.png)

    <span data-ttu-id="3ca98-222">а.</span><span class="sxs-lookup"><span data-stu-id="3ca98-222">a.</span></span> <span data-ttu-id="3ca98-223">Щелкните **Known domains** (Известные домены) на левой панели страницы.</span><span class="sxs-lookup"><span data-stu-id="3ca98-223">Select **Known domains** from the left panel of the page.</span></span>

    <span data-ttu-id="3ca98-224">b.</span><span class="sxs-lookup"><span data-stu-id="3ca98-224">b.</span></span> <span data-ttu-id="3ca98-225">Введите имя домена в текстовое поле **Known domains** (Известные домены).</span><span class="sxs-lookup"><span data-stu-id="3ca98-225">Enter domain name in the **Known domains** textbox.</span></span>

    <span data-ttu-id="3ca98-226">c.</span><span class="sxs-lookup"><span data-stu-id="3ca98-226">c.</span></span> <span data-ttu-id="3ca98-227">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="3ca98-227">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="3ca98-228">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="3ca98-228">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="3ca98-229">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="3ca98-229">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="3ca98-230">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="3ca98-230">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="3ca98-231">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="3ca98-231">Creating an Azure AD test user</span></span>
<span data-ttu-id="3ca98-232">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3ca98-232">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="3ca98-234">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="3ca98-234">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="3ca98-235">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="3ca98-235">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kantegassoforbamboo-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="3ca98-237">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="3ca98-237">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kantegassoforbamboo-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="3ca98-239">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="3ca98-239">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kantegassoforbamboo-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="3ca98-241">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="3ca98-241">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kantegassoforbamboo-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="3ca98-243">а.</span><span class="sxs-lookup"><span data-stu-id="3ca98-243">a.</span></span> <span data-ttu-id="3ca98-244">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="3ca98-244">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="3ca98-245">b.</span><span class="sxs-lookup"><span data-stu-id="3ca98-245">b.</span></span> <span data-ttu-id="3ca98-246">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="3ca98-246">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="3ca98-247">c.</span><span class="sxs-lookup"><span data-stu-id="3ca98-247">c.</span></span> <span data-ttu-id="3ca98-248">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="3ca98-248">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="3ca98-249">d.</span><span class="sxs-lookup"><span data-stu-id="3ca98-249">d.</span></span> <span data-ttu-id="3ca98-250">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="3ca98-250">Click **Create**.</span></span>
 
### <a name="creating-a-kantega-sso-for-bamboo-test-user"></a><span data-ttu-id="3ca98-251">Создание тестового пользователя Kantega SSO for Bamboo</span><span class="sxs-lookup"><span data-stu-id="3ca98-251">Creating a Kantega SSO for Bamboo test user</span></span>

<span data-ttu-id="3ca98-252">Чтобы пользователи Azure AD могли выполнять вход в Bamboo, они должны быть подготовлены в Bamboo.</span><span class="sxs-lookup"><span data-stu-id="3ca98-252">To enable Azure AD users to log in to Bamboo, they must be provisioned into Bamboo.</span></span> <span data-ttu-id="3ca98-253">В Kantega SSO for Bamboo подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="3ca98-253">In Kantega SSO for Bamboo, provisioning is a manual task.</span></span>

<span data-ttu-id="3ca98-254">**Чтобы подготовить учетную запись пользователя, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="3ca98-254">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="3ca98-255">Войдите на локальный сервер Bamboo в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="3ca98-255">Log in to your Bamboo on premise server as an administrator.</span></span>

2. <span data-ttu-id="3ca98-256">Наведите указатель мыши на шестеренку и щелкните **User management** (Управление пользователями).</span><span class="sxs-lookup"><span data-stu-id="3ca98-256">Hover on cog and click the **User management**.</span></span>

    ![Добавление сотрудника](./media/active-directory-saas-kantegassoforbamboo-tutorial/user1.png) 

3. <span data-ttu-id="3ca98-258">Выберите раздел **Пользователи**.</span><span class="sxs-lookup"><span data-stu-id="3ca98-258">Click **Users**.</span></span> <span data-ttu-id="3ca98-259">В разделе **Add user** (Добавление пользователя) выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="3ca98-259">Under the **Add user** section, Perform follwing steps:</span></span>

    ![Добавление сотрудника](./media/active-directory-saas-kantegassoforbamboo-tutorial/user2.png) 

    <span data-ttu-id="3ca98-261">а.</span><span class="sxs-lookup"><span data-stu-id="3ca98-261">a.</span></span> <span data-ttu-id="3ca98-262">В текстовом поле **Username** (Имя пользователя) введите электронный адрес пользователя, например Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="3ca98-262">In the **Username** textbox, type the email of user like Brittasimon@contoso.com.</span></span>
    
    <span data-ttu-id="3ca98-263">b.</span><span class="sxs-lookup"><span data-stu-id="3ca98-263">b.</span></span> <span data-ttu-id="3ca98-264">В текстовом поле **Password** (Пароль) введите пароль пользователя.</span><span class="sxs-lookup"><span data-stu-id="3ca98-264">In the **Password** textbox, type the password of user.</span></span>

    <span data-ttu-id="3ca98-265">c.</span><span class="sxs-lookup"><span data-stu-id="3ca98-265">c.</span></span> <span data-ttu-id="3ca98-266">В текстовом поле **Confirm Password** (Подтверждение пароля) введите пароль еще раз.</span><span class="sxs-lookup"><span data-stu-id="3ca98-266">In the **Confirm Password** textbox, reenter the password of user.</span></span>
    
    <span data-ttu-id="3ca98-267">г)</span><span class="sxs-lookup"><span data-stu-id="3ca98-267">d.</span></span> <span data-ttu-id="3ca98-268">В текстовом поле **Full Name** (Полное имя) введите полное имя пользователя, например Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="3ca98-268">In the **Full Name** textbox, type full name of the user like Britta Simon.</span></span>
    
    <span data-ttu-id="3ca98-269">д.</span><span class="sxs-lookup"><span data-stu-id="3ca98-269">e.</span></span> <span data-ttu-id="3ca98-270">В текстовом поле **Email** (Электронная почта) введите адрес электронной почты пользователя, например Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="3ca98-270">In the **Email** textbox, type the email address of user like Brittasimon@contoso.com.</span></span>
    
    <span data-ttu-id="3ca98-271">f.</span><span class="sxs-lookup"><span data-stu-id="3ca98-271">f.</span></span> <span data-ttu-id="3ca98-272">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="3ca98-272">Click **Save**.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="3ca98-273">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="3ca98-273">Assigning the Azure AD test user</span></span>

<span data-ttu-id="3ca98-274">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к Kantega SSO for Bamboo.</span><span class="sxs-lookup"><span data-stu-id="3ca98-274">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Kantega SSO for Bamboo.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="3ca98-276">**Чтобы назначить пользователя Britta Simon в Kantega SSO for Bamboo, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="3ca98-276">**To assign Britta Simon to Kantega SSO for Bamboo, perform the following steps:**</span></span>

1. <span data-ttu-id="3ca98-277">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="3ca98-277">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="3ca98-279">Из списка приложений выберите **Kantega SSO for Bamboo**.</span><span class="sxs-lookup"><span data-stu-id="3ca98-279">In the applications list, select **Kantega SSO for Bamboo**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_kantegassoforbamboo_app.png) 

3. <span data-ttu-id="3ca98-281">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="3ca98-281">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="3ca98-283">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="3ca98-283">Click **Add** button.</span></span> <span data-ttu-id="3ca98-284">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="3ca98-284">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="3ca98-286">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="3ca98-286">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="3ca98-287">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="3ca98-287">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="3ca98-288">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="3ca98-288">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="3ca98-289">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="3ca98-289">Testing single sign-on</span></span>

<span data-ttu-id="3ca98-290">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="3ca98-290">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="3ca98-291">Щелкнув элемент "Kantega SSO for Bamboo" на панели доступа, вы автоматически войдете в приложение Kantega SSO for Bamboo.</span><span class="sxs-lookup"><span data-stu-id="3ca98-291">When you click the Kantega SSO for Bamboo tile in the Access Panel, you should get automatically signed-on to your Kantega SSO for Bamboo application.</span></span>
<span data-ttu-id="3ca98-292">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="3ca98-292">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="3ca98-293">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="3ca98-293">Additional resources</span></span>

* [<span data-ttu-id="3ca98-294">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3ca98-294">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="3ca98-295">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="3ca98-295">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kantegassoforbamboo-tutorial/tutorial_general_203.png

