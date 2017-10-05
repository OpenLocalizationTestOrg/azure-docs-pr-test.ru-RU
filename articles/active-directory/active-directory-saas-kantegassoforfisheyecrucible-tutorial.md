---
title: "Руководство по интеграции Azure Active Directory с Kantega SSO for FishEye/Crucible | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в Kantega SSO for FishEye/Crucible."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9fe951fd-1530-4d33-a1a4-390385b99ce9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 9eaa2ec661a3488b0bef1f6b7cc7a82290720054
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/29/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kantega-sso-for-fisheyecrucible"></a><span data-ttu-id="62e10-103">Руководство по интеграции Azure Active Directory с Kantega SSO for FishEye/Crucible</span><span class="sxs-lookup"><span data-stu-id="62e10-103">Tutorial: Azure Active Directory integration with Kantega SSO for FishEye/Crucible</span></span>

<span data-ttu-id="62e10-104">В этом руководстве описано, как интегрировать Kantega SSO for FishEye/Crucible с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="62e10-104">In this tutorial, you learn how to integrate Kantega SSO for FishEye/Crucible with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="62e10-105">Интеграция Azure AD с приложением Kantega SSO for FishEye/Crucible обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="62e10-105">Integrating Kantega SSO for FishEye/Crucible with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="62e10-106">С помощью Azure AD вы можете контролировать доступ к Kantega SSO for FishEye/Crucible.</span><span class="sxs-lookup"><span data-stu-id="62e10-106">You can control in Azure AD who has access to Kantega SSO for FishEye/Crucible</span></span>
- <span data-ttu-id="62e10-107">Вы можете включить автоматический вход пользователей в Kantega SSO for FishEye/Crucible (единый вход) с использованием учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="62e10-107">You can enable your users to automatically get signed-on to Kantega SSO for FishEye/Crucible (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="62e10-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="62e10-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="62e10-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="62e10-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="62e10-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="62e10-110">Prerequisites</span></span>

<span data-ttu-id="62e10-111">Чтобы настроить интеграцию Azure AD с Kantega SSO for FishEye/Crucible, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="62e10-111">To configure Azure AD integration with Kantega SSO for FishEye/Crucible, you need the following items:</span></span>

- <span data-ttu-id="62e10-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="62e10-112">An Azure AD subscription</span></span>
- <span data-ttu-id="62e10-113">подписка Kantega SSO for FishEye/Crucible с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="62e10-113">A Kantega SSO for FishEye/Crucible single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="62e10-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="62e10-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="62e10-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="62e10-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="62e10-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="62e10-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="62e10-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="62e10-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="62e10-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="62e10-118">Scenario description</span></span>
<span data-ttu-id="62e10-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="62e10-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="62e10-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="62e10-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="62e10-121">Добавление Kantega SSO for FishEye/Crucible из коллекции.</span><span class="sxs-lookup"><span data-stu-id="62e10-121">Adding Kantega SSO for FishEye/Crucible from the gallery</span></span>
2. <span data-ttu-id="62e10-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="62e10-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kantega-sso-for-fisheyecrucible-from-the-gallery"></a><span data-ttu-id="62e10-123">Добавление Kantega SSO for FishEye/Crucible из коллекции</span><span class="sxs-lookup"><span data-stu-id="62e10-123">Adding Kantega SSO for FishEye/Crucible from the gallery</span></span>
<span data-ttu-id="62e10-124">Чтобы настроить интеграцию Kantega SSO for FishEye/Crucible с Azure AD, необходимо добавить Kantega SSO for FishEye/Crucible из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="62e10-124">To configure the integration of Kantega SSO for FishEye/Crucible into Azure AD, you need to add Kantega SSO for FishEye/Crucible from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="62e10-125">**Чтобы добавить Kantega SSO for FishEye/Crucible из коллекции, сделайте следующее.**</span><span class="sxs-lookup"><span data-stu-id="62e10-125">**To add Kantega SSO for FishEye/Crucible from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="62e10-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="62e10-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="62e10-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="62e10-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="62e10-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="62e10-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="62e10-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="62e10-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="62e10-133">В поле поиска введите **Kantega SSO for FishEye/Crucible**.</span><span class="sxs-lookup"><span data-stu-id="62e10-133">In the search box, type **Kantega SSO for FishEye/Crucible**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_search.png)

5. <span data-ttu-id="62e10-135">На панели результатов выберите **Kantega SSO for FishEye/Crucible** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="62e10-135">In the results panel, select **Kantega SSO for FishEye/Crucible**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="62e10-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="62e10-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="62e10-138">В этом разделе описана настройка и проверка единого входа Azure AD в Kantega SSO for FishEye/Crucible с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="62e10-138">In this section, you configure and test Azure AD single sign-on with Kantega SSO for FishEye/Crucible based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="62e10-139">Чтобы единый вход работал, Azure AD необходима информация о том, какой пользователь в Kantega SSO for FishEye/Crucible соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="62e10-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Kantega SSO for FishEye/Crucible is to a user in Azure AD.</span></span> <span data-ttu-id="62e10-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Kantega SSO for FishEye/Crucible.</span><span class="sxs-lookup"><span data-stu-id="62e10-140">In other words, a link relationship between an Azure AD user and the related user in Kantega SSO for FishEye/Crucible needs to be established.</span></span>

<span data-ttu-id="62e10-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Kantega SSO for FishEye/Crucible.</span><span class="sxs-lookup"><span data-stu-id="62e10-141">In Kantega SSO for FishEye/Crucible, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="62e10-142">Чтобы настроить и проверить единый вход Azure AD в Kantega SSO for FishEye/Crucible, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="62e10-142">To configure and test Azure AD single sign-on with Kantega SSO for FishEye/Crucible, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="62e10-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="62e10-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="62e10-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="62e10-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="62e10-145">**[Создание тестового пользователя Kantega SSO for FishEye/Crucible](#creating-a-kantega-sso-for-fisheyecrucible-test-user)** требуется для того, чтобы в Kantega SSO for FishEye/Crucible существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="62e10-145">**[Creating a Kantega SSO for FishEye/Crucible test user](#creating-a-kantega-sso-for-fisheyecrucible-test-user)** - to have a counterpart of Britta Simon in Kantega SSO for FishEye/Crucible that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="62e10-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="62e10-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="62e10-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="62e10-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="62e10-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="62e10-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="62e10-149">В данном разделе описано, как включить единый вход в Azure AD на портале Azure и настроить его в приложении Kantega SSO for FishEye/Crucible.</span><span class="sxs-lookup"><span data-stu-id="62e10-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Kantega SSO for FishEye/Crucible application.</span></span>

<span data-ttu-id="62e10-150">**Чтобы настроить единый вход Azure AD в Kantega SSO for FishEye/Crucible, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="62e10-150">**To configure Azure AD single sign-on with Kantega SSO for FishEye/Crucible, perform the following steps:**</span></span>

1. <span data-ttu-id="62e10-151">На портале Azure на странице интеграции с приложением **Kantega SSO for FishEye/Crucible** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="62e10-151">In the Azure portal, on the **Kantega SSO for FishEye/Crucible** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="62e10-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="62e10-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_samlbase.png)

3. <span data-ttu-id="62e10-155">Чтобы использовать режим, инициируемый **IdP**, в разделе **Домены и URL-адреса приложения Kantega SSO for FishEye/Crucible** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="62e10-155">In **IDP** initiated mode, on the **Kantega SSO for FishEye/Crucible Domain and URLs** section perform the following step :</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_url1.png)

    <span data-ttu-id="62e10-157">а.</span><span class="sxs-lookup"><span data-stu-id="62e10-157">a.</span></span> <span data-ttu-id="62e10-158">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="62e10-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

    <span data-ttu-id="62e10-159">b.</span><span class="sxs-lookup"><span data-stu-id="62e10-159">b.</span></span> <span data-ttu-id="62e10-160">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`.</span><span class="sxs-lookup"><span data-stu-id="62e10-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>

4. <span data-ttu-id="62e10-161">Чтобы использовать режим, инициируемый **поставщиком услуг**, установите флажок **Показать дополнительные параметры URL-адресов**.</span><span class="sxs-lookup"><span data-stu-id="62e10-161">In **SP** initiated mode, check **Show advanced URL settings** and perform the following step:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_url2.png)

    <span data-ttu-id="62e10-163">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span><span class="sxs-lookup"><span data-stu-id="62e10-163">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<server-base-url>/plugins/servlet/no.kantega.saml/sp/<uniqueid>/login`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="62e10-164">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="62e10-164">These values are not real.</span></span> <span data-ttu-id="62e10-165">Замените их фактическими значениями идентификатора, URL-адреса ответа и URL-адреса входа.</span><span class="sxs-lookup"><span data-stu-id="62e10-165">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="62e10-166">Эти значения предоставляются во время настройки подключаемого модуля FishEye/Crucible, которая описывается далее в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="62e10-166">These values are recieved during the configuration of FishEye/Crucible plugin which is explained later in the tutorial.</span></span>

5. <span data-ttu-id="62e10-167">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="62e10-167">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_certificate.png) 

6. <span data-ttu-id="62e10-169">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="62e10-169">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="62e10-171">В другом окне веб-браузера войдите на свой локальный сервер FishEye/Crucible в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="62e10-171">In a different web browser window, log in to your FishEye/Crucible on premise server as an administrator.</span></span>

8. <span data-ttu-id="62e10-172">Наведите указатель мыши на шестеренку и щелкните **Add-ons** (Надстройки).</span><span class="sxs-lookup"><span data-stu-id="62e10-172">Hover on cog and click the **Add-ons**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon1.png)

9. <span data-ttu-id="62e10-174">В разделе "System Settings" (Параметры системы) щелкните **Find new add-ons** (Найти новые надстройки).</span><span class="sxs-lookup"><span data-stu-id="62e10-174">Under System Settings section, click **Find new add-ons**.</span></span> 

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/add-on2.png)

10. <span data-ttu-id="62e10-176">Найдите подключаемый модуль **Kantega SSO for Crucible (SAML & Kerberos)** и нажмите кнопку **Install** (Установить), чтобы установить новый подключаемый модуль SAML.</span><span class="sxs-lookup"><span data-stu-id="62e10-176">Search **Kantega SSO for Crucible** and click **Install** button to install the new SAML plugin.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon2.png)

11. <span data-ttu-id="62e10-178">Начнется установка подключаемого модуля.</span><span class="sxs-lookup"><span data-stu-id="62e10-178">The plugin installation starts.</span></span> 

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon33.png)

12. <span data-ttu-id="62e10-180">Установка завершится.</span><span class="sxs-lookup"><span data-stu-id="62e10-180">Once the installation is complete.</span></span> <span data-ttu-id="62e10-181">Нажмите кнопку **Закрыть**</span><span class="sxs-lookup"><span data-stu-id="62e10-181">Click **Close**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon34.png)

13. <span data-ttu-id="62e10-183">Нажмите кнопку **Управление**.</span><span class="sxs-lookup"><span data-stu-id="62e10-183">Click **Manage**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon35.png)

14. <span data-ttu-id="62e10-185">Щелкните **Configure** (Настройка), чтобы настроить новый подключаемый модуль.</span><span class="sxs-lookup"><span data-stu-id="62e10-185">Click **Configure** to configure the new plugin.</span></span>    

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon3.png)

15. <span data-ttu-id="62e10-187">В разделе **SAML** сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="62e10-187">In the **SAML** section.</span></span> <span data-ttu-id="62e10-188">Выберите **Azure Active Directory (Azure AD)** из раскрывающегося списка **Добавление поставщика удостоверений**.</span><span class="sxs-lookup"><span data-stu-id="62e10-188">Select **Azure Active Directory (Azure AD)** from the **Add identity provider** dropdown.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon4.png)

16. <span data-ttu-id="62e10-190">Выберите уровень подписки **Базовый**.</span><span class="sxs-lookup"><span data-stu-id="62e10-190">Select subscription level as **Basic**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon5.png)

17. <span data-ttu-id="62e10-192">В разделе **Свойства приложения** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="62e10-192">On the **App properties** section, perform following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon6.png)

    <span data-ttu-id="62e10-194">а.</span><span class="sxs-lookup"><span data-stu-id="62e10-194">a.</span></span> <span data-ttu-id="62e10-195">Скопируйте значение **App ID URI** (URI кода приложения) и используйте его как **идентификатор, URL-адрес ответа и URL-адрес входа** в разделе **Домены и URL-адреса приложения Kantega SSO for FishEye/Crucible** на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="62e10-195">Copy the **App ID URI** value and use it as **Identifier, Reply URL, and Sign-On URL** on the **Kantega SSO for FishEye/Crucible Domain and URLs** section in Azure portal.</span></span>

    <span data-ttu-id="62e10-196">b.</span><span class="sxs-lookup"><span data-stu-id="62e10-196">b.</span></span> <span data-ttu-id="62e10-197">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="62e10-197">Click **Next**.</span></span>

18. <span data-ttu-id="62e10-198">В разделе **Metadata import** (Импорт метаданных) выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="62e10-198">On the **Metadata import** section, perform following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon7.png)

    <span data-ttu-id="62e10-200">а.</span><span class="sxs-lookup"><span data-stu-id="62e10-200">a.</span></span> <span data-ttu-id="62e10-201">Щелкните **Metadata file on my computer** (Файл метаданных на моем компьютере) и передайте файл метаданных, который вы скачали с портала Azure.</span><span class="sxs-lookup"><span data-stu-id="62e10-201">Select **Metadata file on my computer**, and upload metadata file, which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="62e10-202">b.</span><span class="sxs-lookup"><span data-stu-id="62e10-202">b.</span></span> <span data-ttu-id="62e10-203">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="62e10-203">Click **Next**.</span></span>

19. <span data-ttu-id="62e10-204">В разделе **Name and SSO location** (Имя и расположение единого входа) выполните следующее.</span><span class="sxs-lookup"><span data-stu-id="62e10-204">On the **Name and SSO location** section, perform following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon8.png)

    <span data-ttu-id="62e10-206">а.</span><span class="sxs-lookup"><span data-stu-id="62e10-206">a.</span></span> <span data-ttu-id="62e10-207">В текстовом поле **Provider Name** (Имя поставщика) введите имя поставщика (например, Azure AD).</span><span class="sxs-lookup"><span data-stu-id="62e10-207">Add Name of the Identity Provider in **Identity provider name** textbox (e.g Azure AD).</span></span>

    <span data-ttu-id="62e10-208">b.</span><span class="sxs-lookup"><span data-stu-id="62e10-208">b.</span></span> <span data-ttu-id="62e10-209">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="62e10-209">Click **Next**.</span></span>

20. <span data-ttu-id="62e10-210">Проверьте сертификат для подписи и нажмите кнопку **Next** (Далее).</span><span class="sxs-lookup"><span data-stu-id="62e10-210">Verify the Signing certificate and click **Next**.</span></span>  

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon9.png)

21. <span data-ttu-id="62e10-212">В разделе **FishEye user accounts** (Учетные записи пользователей FishEye) выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="62e10-212">On the **FishEye user accounts** section, perform following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon10.png)

    <span data-ttu-id="62e10-214">а.</span><span class="sxs-lookup"><span data-stu-id="62e10-214">a.</span></span> <span data-ttu-id="62e10-215">Щелкните переключатель **Create users in FishEye's internal Directory if needed** (При необходимости создать пользователей во внутреннем каталоге FishEye) и введите соответствующее имя группы пользователей (это может быть несколько групп,</span><span class="sxs-lookup"><span data-stu-id="62e10-215">Select **Create users in FishEye's internal Directory if needed** and enter the appropriate name of the group for users (can be multiple no.</span></span> <span data-ttu-id="62e10-216">разделенных запятой).</span><span class="sxs-lookup"><span data-stu-id="62e10-216">of groups separated by comma).</span></span>

    <span data-ttu-id="62e10-217">b.</span><span class="sxs-lookup"><span data-stu-id="62e10-217">b.</span></span> <span data-ttu-id="62e10-218">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="62e10-218">Click **Next**.</span></span>

22. <span data-ttu-id="62e10-219">Нажмите кнопку **Готово**</span><span class="sxs-lookup"><span data-stu-id="62e10-219">Click **Finish**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon11.png)

23. <span data-ttu-id="62e10-221">В разделе **Known domains for Azure AD** (Известные домены для Azure AD) выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="62e10-221">On the **Known domains for Azure AD** section, perform following steps:</span></span> 

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/addon12.png)

    <span data-ttu-id="62e10-223">а.</span><span class="sxs-lookup"><span data-stu-id="62e10-223">a.</span></span> <span data-ttu-id="62e10-224">Щелкните **Known domains** (Известные домены) на левой панели страницы.</span><span class="sxs-lookup"><span data-stu-id="62e10-224">Select **Known domains** from the left panel of the page.</span></span>

    <span data-ttu-id="62e10-225">b.</span><span class="sxs-lookup"><span data-stu-id="62e10-225">b.</span></span> <span data-ttu-id="62e10-226">Введите имя домена в текстовое поле **Known domains** (Известные домены).</span><span class="sxs-lookup"><span data-stu-id="62e10-226">Enter domain name in the **Known domains** textbox.</span></span>

    <span data-ttu-id="62e10-227">c.</span><span class="sxs-lookup"><span data-stu-id="62e10-227">c.</span></span> <span data-ttu-id="62e10-228">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="62e10-228">Click **Save**.</span></span>  

> [!TIP]
> <span data-ttu-id="62e10-229">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="62e10-229">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="62e10-230">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="62e10-230">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="62e10-231">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="62e10-231">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="62e10-232">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="62e10-232">Creating an Azure AD test user</span></span>
<span data-ttu-id="62e10-233">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="62e10-233">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="62e10-235">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="62e10-235">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="62e10-236">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="62e10-236">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="62e10-238">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="62e10-238">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="62e10-240">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="62e10-240">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="62e10-242">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="62e10-242">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="62e10-244">а.</span><span class="sxs-lookup"><span data-stu-id="62e10-244">a.</span></span> <span data-ttu-id="62e10-245">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="62e10-245">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="62e10-246">b.</span><span class="sxs-lookup"><span data-stu-id="62e10-246">b.</span></span> <span data-ttu-id="62e10-247">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="62e10-247">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="62e10-248">c.</span><span class="sxs-lookup"><span data-stu-id="62e10-248">c.</span></span> <span data-ttu-id="62e10-249">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="62e10-249">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="62e10-250">d.</span><span class="sxs-lookup"><span data-stu-id="62e10-250">d.</span></span> <span data-ttu-id="62e10-251">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="62e10-251">Click **Create**.</span></span>
 
### <a name="creating-a-kantega-sso-for-fisheyecrucible-test-user"></a><span data-ttu-id="62e10-252">Создание тестового пользователя Kantega SSO for FishEye/Crucible</span><span class="sxs-lookup"><span data-stu-id="62e10-252">Creating a Kantega SSO for FishEye/Crucible test user</span></span>

<span data-ttu-id="62e10-253">Чтобы пользователи Azure AD могли выполнять вход в FishEye/Crucible, они должны быть подготовлены в Freshservice.</span><span class="sxs-lookup"><span data-stu-id="62e10-253">To enable Azure AD users to log in to FishEye/Crucible, they must be provisioned into FishEye/Crucible.</span></span> <span data-ttu-id="62e10-254">В Kantega SSO for FishEye/Crucible подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="62e10-254">In Kantega SSO for FishEye/Crucible, provisioning is a manual task.</span></span>

<span data-ttu-id="62e10-255">**Чтобы подготовить учетную запись пользователя, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="62e10-255">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="62e10-256">Войдите на локальный сервер Crucible в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="62e10-256">Log in to your Crucible on premise server as an administrator.</span></span>

2. <span data-ttu-id="62e10-257">Наведите указатель мыши на шестеренку и щелкните **Users** (Пользователи).</span><span class="sxs-lookup"><span data-stu-id="62e10-257">Hover on cog and click the **Users**.</span></span>

    ![Добавление сотрудника](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/user1.png) 

3. <span data-ttu-id="62e10-259">В разделе **Users** (Пользователи) щелкните **Add user** (Добавить пользователя).</span><span class="sxs-lookup"><span data-stu-id="62e10-259">Under **Users** tab section, click **Add user**.</span></span>

    ![Добавление сотрудника](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/user2.png)

4. <span data-ttu-id="62e10-261">На странице диалогового окна **Add New User** (Добавление нового пользователя) выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="62e10-261">On the **Add New User** dialog page, perform the following steps:</span></span>

    ![Добавление сотрудника](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/user3.png) 

    <span data-ttu-id="62e10-263">а.</span><span class="sxs-lookup"><span data-stu-id="62e10-263">a.</span></span> <span data-ttu-id="62e10-264">В текстовом поле **Username** (Имя пользователя) введите электронный адрес пользователя, например Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="62e10-264">In the **Username** textbox, type the email of user like Brittasimon@contoso.com.</span></span>
    
    <span data-ttu-id="62e10-265">b.</span><span class="sxs-lookup"><span data-stu-id="62e10-265">b.</span></span> <span data-ttu-id="62e10-266">В текстовом поле **Display Name** (Отображаемое имя) введите отображаемое имя пользователя, например Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="62e10-266">In the **Display Name** textbox, type display name of the user like Britta Simon.</span></span>
    
    <span data-ttu-id="62e10-267">c.</span><span class="sxs-lookup"><span data-stu-id="62e10-267">c.</span></span> <span data-ttu-id="62e10-268">В текстовом поле **Email address** (Адрес электронной почты) введите адрес электронной почты пользователя, например Brittasimon@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="62e10-268">In the **Email address** textbox, type the email address of user like Brittasimon@contoso.com.</span></span>

    <span data-ttu-id="62e10-269">г)</span><span class="sxs-lookup"><span data-stu-id="62e10-269">d.</span></span> <span data-ttu-id="62e10-270">В текстовом поле **Password** (Пароль) введите пароль пользователя.</span><span class="sxs-lookup"><span data-stu-id="62e10-270">In the **Password** textbox, type the password of user.</span></span>  

    <span data-ttu-id="62e10-271">д.</span><span class="sxs-lookup"><span data-stu-id="62e10-271">e.</span></span> <span data-ttu-id="62e10-272">В текстовом поле **Confirm Password** (Подтверждение пароля) введите пароль еще раз.</span><span class="sxs-lookup"><span data-stu-id="62e10-272">In the **Confirm Password** textbox, reenter the password of user.</span></span>

    <span data-ttu-id="62e10-273">f.</span><span class="sxs-lookup"><span data-stu-id="62e10-273">f.</span></span> <span data-ttu-id="62e10-274">Щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="62e10-274">Click **Add**.</span></span>   

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="62e10-275">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="62e10-275">Assigning the Azure AD test user</span></span>

<span data-ttu-id="62e10-276">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к Kantega SSO for FishEye/Crucible.</span><span class="sxs-lookup"><span data-stu-id="62e10-276">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Kantega SSO for FishEye/Crucible.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="62e10-278">**Чтобы назначить пользователя Britta Simon в Kantega SSO for FishEye/Crucible, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="62e10-278">**To assign Britta Simon to Kantega SSO for FishEye/Crucible, perform the following steps:**</span></span>

1. <span data-ttu-id="62e10-279">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="62e10-279">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="62e10-281">Из списка приложений выберите **Kantega SSO for FishEye/Crucible**.</span><span class="sxs-lookup"><span data-stu-id="62e10-281">In the applications list, select **Kantega SSO for FishEye/Crucible**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_kantegassoforfisheyecrucible_app.png) 

3. <span data-ttu-id="62e10-283">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="62e10-283">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="62e10-285">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="62e10-285">Click **Add** button.</span></span> <span data-ttu-id="62e10-286">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="62e10-286">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="62e10-288">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="62e10-288">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="62e10-289">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="62e10-289">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="62e10-290">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="62e10-290">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="62e10-291">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="62e10-291">Testing single sign-on</span></span>

<span data-ttu-id="62e10-292">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="62e10-292">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="62e10-293">Щелкнув элемент "Kantega SSO for FishEye/Crucible" на панели доступа, вы автоматически войдете в приложение Kantega SSO for FishEye/Crucible.</span><span class="sxs-lookup"><span data-stu-id="62e10-293">When you click the Kantega SSO for FishEye/Crucible tile in the Access Panel, you should get automatically signed-on to your Kantega SSO for FishEye/Crucible application.</span></span>
<span data-ttu-id="62e10-294">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="62e10-294">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="62e10-295">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="62e10-295">Additional resources</span></span>

* [<span data-ttu-id="62e10-296">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="62e10-296">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="62e10-297">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="62e10-297">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kantegassoforfisheyecrucible-tutorial/tutorial_general_203.png

