---
title: "Учебник. Интеграция Azure Active Directory с Jitbit Helpdesk | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и Jitbit Helpdesk."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 15ce27d4-0621-4103-8a34-e72c98d72ec3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 6523ee3179dafd79528093b856b0ec10fafb4f7b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-jitbit-helpdesk"></a><span data-ttu-id="b41c8-103">Руководство. Интеграция Azure Active Directory с Jitbit Helpdesk</span><span class="sxs-lookup"><span data-stu-id="b41c8-103">Tutorial: Azure Active Directory integration with Jitbit Helpdesk</span></span>

<span data-ttu-id="b41c8-104">В этом руководстве описано, как интегрировать Jitbit Helpdesk с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b41c8-104">In this tutorial, you learn how to integrate Jitbit Helpdesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b41c8-105">Интеграция Azure AD с приложением Jitbit Helpdesk обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="b41c8-105">Integrating Jitbit Helpdesk with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b41c8-106">С помощью Azure AD вы можете контролировать доступ к Jitbit Helpdesk.</span><span class="sxs-lookup"><span data-stu-id="b41c8-106">You can control in Azure AD who has access to Jitbit Helpdesk</span></span>
- <span data-ttu-id="b41c8-107">Вы можете включить автоматический вход пользователей в Jitbit Helpdesk (единый вход) с использованием учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b41c8-107">You can enable your users to automatically get signed-on to Jitbit Helpdesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b41c8-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="b41c8-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b41c8-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b41c8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b41c8-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b41c8-110">Prerequisites</span></span>

<span data-ttu-id="b41c8-111">Чтобы настроить интеграцию Azure AD с Jitbit Helpdesk, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="b41c8-111">To configure Azure AD integration with Jitbit Helpdesk, you need the following items:</span></span>

- <span data-ttu-id="b41c8-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="b41c8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b41c8-113">подписка с поддержкой единого входа Jitbit Helpdesk.</span><span class="sxs-lookup"><span data-stu-id="b41c8-113">A Jitbit Helpdesk single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b41c8-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="b41c8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b41c8-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="b41c8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b41c8-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="b41c8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b41c8-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b41c8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b41c8-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="b41c8-118">Scenario description</span></span>
<span data-ttu-id="b41c8-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="b41c8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b41c8-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="b41c8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b41c8-121">Добавление Jitbit Helpdesk из коллекции.</span><span class="sxs-lookup"><span data-stu-id="b41c8-121">Adding Jitbit Helpdesk from the gallery</span></span>
2. <span data-ttu-id="b41c8-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b41c8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-jitbit-helpdesk-from-the-gallery"></a><span data-ttu-id="b41c8-123">Добавление Jitbit Helpdesk из коллекции</span><span class="sxs-lookup"><span data-stu-id="b41c8-123">Adding Jitbit Helpdesk from the gallery</span></span>
<span data-ttu-id="b41c8-124">Чтобы настроить интеграцию Jitbit Helpdesk с Azure AD, необходимо добавить Jitbit Helpdesk из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="b41c8-124">To configure the integration of Jitbit Helpdesk into Azure AD, you need to add Jitbit Helpdesk from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b41c8-125">**Чтобы добавить Jitbit Helpdesk из коллекции, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="b41c8-125">**To add Jitbit Helpdesk from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b41c8-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b41c8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b41c8-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="b41c8-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b41c8-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="b41c8-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="b41c8-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="b41c8-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="b41c8-133">В поле поиска введите **Jitbit Helpdesk**.</span><span class="sxs-lookup"><span data-stu-id="b41c8-133">In the search box, type **Jitbit Helpdesk**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_search.png)

5. <span data-ttu-id="b41c8-135">На панели результатов выберите **Jitbit Helpdesk** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="b41c8-135">In the results panel, select **Jitbit Helpdesk**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b41c8-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b41c8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b41c8-138">В этом разделе описаны настройка и проверка единого входа Azure AD в Jitbit Helpdesk с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b41c8-138">In this section, you configure and test Azure AD single sign-on with Jitbit Helpdesk based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b41c8-139">Чтобы единый вход работал, Azure AD необходимо знать, какой пользователь в Jitbit Helpdesk соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b41c8-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Jitbit Helpdesk is to a user in Azure AD.</span></span> <span data-ttu-id="b41c8-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Jitbit Helpdesk.</span><span class="sxs-lookup"><span data-stu-id="b41c8-140">In other words, a link relationship between an Azure AD user and the related user in Jitbit Helpdesk needs to be established.</span></span>

<span data-ttu-id="b41c8-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Jitbit Helpdesk.</span><span class="sxs-lookup"><span data-stu-id="b41c8-141">In Jitbit Helpdesk, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="b41c8-142">Чтобы настроить и проверить единый вход Azure AD в Jitbit Helpdesk, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="b41c8-142">To configure and test Azure AD single sign-on with Jitbit Helpdesk, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b41c8-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="b41c8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b41c8-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b41c8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b41c8-145">**[Создание тестового пользователя Jitbit Helpdesk](#creating-a-jitbit-helpdesk-test-user)** требуется для создания в Jitbit Helpdesk пользователя Britta Simon, связанного с представлением этого же пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b41c8-145">**[Creating a Jitbit Helpdesk test user](#creating-a-jitbit-helpdesk-test-user)** - to have a counterpart of Britta Simon in Jitbit Helpdesk that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b41c8-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b41c8-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b41c8-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="b41c8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b41c8-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b41c8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b41c8-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Jitbit Helpdesk.</span><span class="sxs-lookup"><span data-stu-id="b41c8-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Jitbit Helpdesk application.</span></span>

<span data-ttu-id="b41c8-150">**Чтобы настроить единый вход Azure AD в Jitbit Helpdesk, выполните следующее.**</span><span class="sxs-lookup"><span data-stu-id="b41c8-150">**To configure Azure AD single sign-on with Jitbit Helpdesk, perform the following steps:**</span></span>

1. <span data-ttu-id="b41c8-151">На портале Azure на странице интеграции с приложением **Jitbit Helpdesk** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="b41c8-151">In the Azure portal, on the **Jitbit Helpdesk** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="b41c8-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="b41c8-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_samlbase.png)

3. <span data-ttu-id="b41c8-155">В разделе **Домены и URL-адреса приложения Jitbit Helpdesk** выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="b41c8-155">On the **Jitbit Helpdesk Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_url.png)

    <span data-ttu-id="b41c8-157">а.</span><span class="sxs-lookup"><span data-stu-id="b41c8-157">a.</span></span> <span data-ttu-id="b41c8-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="b41c8-158">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span> 
    | |     
    | ----------------------------------------|
    | `https://<hostname>/helpdesk/User/Login`|
    | `https://<tenant-name>.Jitbit.com`|
    | |
    
    > [!NOTE] 
    > <span data-ttu-id="b41c8-159">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="b41c8-159">This value is not real.</span></span> <span data-ttu-id="b41c8-160">Вместо него необходимо указать фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="b41c8-160">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="b41c8-161">Для получения этого значения обратитесь в [службу поддержки клиентов Jitbit Helpdesk](https://www.jitbit.com/support/).</span><span class="sxs-lookup"><span data-stu-id="b41c8-161">Contact [Jitbit Helpdesk Client support team](https://www.jitbit.com/support/) to get this value.</span></span> 
    
    <span data-ttu-id="b41c8-162">b.</span><span class="sxs-lookup"><span data-stu-id="b41c8-162">b.</span></span>  <span data-ttu-id="b41c8-163">В текстовом поле **Идентификатор** введите URL-адрес в формате: `https://www.jitbit.com/web-helpdesk/`</span><span class="sxs-lookup"><span data-stu-id="b41c8-163">In the **Identifier** textbox, type a URL as following: `https://www.jitbit.com/web-helpdesk/`</span></span>

    
 


4. <span data-ttu-id="b41c8-164">В разделе **Сертификат подписи SAML** щелкните **Сертификат (Base64)**, а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="b41c8-164">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_certificate.png) 

5. <span data-ttu-id="b41c8-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="b41c8-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b41c8-168">В разделе **Настройка Jitbit Helpdesk** щелкните **Настроить Jitbit Helpdesk**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="b41c8-168">On the **Jitbit Helpdesk Configuration** section, click **Configure Jitbit Helpdesk** to open **Configure sign-on** window.</span></span> <span data-ttu-id="b41c8-169">Скопируйте **URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="b41c8-169">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_configure.png) 

7. <span data-ttu-id="b41c8-171">В другом окне браузера войдите на свой корпоративный веб-сайт Jitbit Helpdesk в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="b41c8-171">In a different web browser window, log into your Jitbit Helpdesk company site as an administrator.</span></span>

8. <span data-ttu-id="b41c8-172">На панели инструментов в верхней части страницы щелкните **Администрирование**.</span><span class="sxs-lookup"><span data-stu-id="b41c8-172">In the toolbar on the top, click **Administration**.</span></span>
   
    <span data-ttu-id="b41c8-173">![Администрирование](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "Администрирование")</span><span class="sxs-lookup"><span data-stu-id="b41c8-173">![Administration](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "Administration")</span></span>

9. <span data-ttu-id="b41c8-174">Щелкните **Общие параметры**.</span><span class="sxs-lookup"><span data-stu-id="b41c8-174">Click **General settings**.</span></span>
   
    <span data-ttu-id="b41c8-175">![Пользователи, организации и разрешения](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777680.png "Пользователи, организации и разрешения")</span><span class="sxs-lookup"><span data-stu-id="b41c8-175">![Users, companies, and permissions](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777680.png "Users, companies, and permissions")</span></span>

10. <span data-ttu-id="b41c8-176">В разделе конфигурации **Параметры проверки подлинности** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="b41c8-176">In the **Authentication settings** configuration section, perform the following steps:</span></span>
   
    <span data-ttu-id="b41c8-177">![Параметры аутентификации](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777683.png "Параметры аутентификации")</span><span class="sxs-lookup"><span data-stu-id="b41c8-177">![Authentication settings](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777683.png "Authentication settings")</span></span>
    
    <span data-ttu-id="b41c8-178">а.</span><span class="sxs-lookup"><span data-stu-id="b41c8-178">a.</span></span> <span data-ttu-id="b41c8-179">Установите флажок **Enable SAML 2.0 single sign on** (Включить единый вход SAML 2.0) для выполнения единого входа с помощью **OneLogin**.</span><span class="sxs-lookup"><span data-stu-id="b41c8-179">Select **Enable SAML 2.0 single sign on**, to sign in using Single Sign-On (SSO), with **OneLogin**.</span></span>

    <span data-ttu-id="b41c8-180">b.</span><span class="sxs-lookup"><span data-stu-id="b41c8-180">b.</span></span> <span data-ttu-id="b41c8-181">В текстовое поле **URL-адрес конечной точки** вставьте значение **URL-адрес службы единого входа SAML**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="b41c8-181">In the **EndPoint URL** textbox, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="b41c8-182">c.</span><span class="sxs-lookup"><span data-stu-id="b41c8-182">c.</span></span> <span data-ttu-id="b41c8-183">Откройте сертификат в кодировке **Base-64** в Блокноте, скопируйте его содержимое в буфер обмена, а затем вставьте его в текстовое поле **Сертификат X.509**.</span><span class="sxs-lookup"><span data-stu-id="b41c8-183">Open your **base-64** encoded certificate in notepad, copy the content of it into your clipboard, and then paste it to the **X.509 Certificate** textbox</span></span>

    <span data-ttu-id="b41c8-184">г)</span><span class="sxs-lookup"><span data-stu-id="b41c8-184">d.</span></span> <span data-ttu-id="b41c8-185">Нажмите кнопку **Сохранить изменения**.</span><span class="sxs-lookup"><span data-stu-id="b41c8-185">Click **Save changes**.</span></span>

> [!TIP]
> <span data-ttu-id="b41c8-186">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="b41c8-186">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b41c8-187">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="b41c8-187">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b41c8-188">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="b41c8-188">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b41c8-189">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="b41c8-189">Creating an Azure AD test user</span></span>
<span data-ttu-id="b41c8-190">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b41c8-190">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="b41c8-192">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="b41c8-192">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b41c8-193">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b41c8-193">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b41c8-195">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="b41c8-195">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b41c8-197">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="b41c8-197">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b41c8-199">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="b41c8-199">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-jitbit-helpdesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b41c8-201">а.</span><span class="sxs-lookup"><span data-stu-id="b41c8-201">a.</span></span> <span data-ttu-id="b41c8-202">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b41c8-202">In the **Name** textbox, type name as **BrittaSimon**.</span></span>

    <span data-ttu-id="b41c8-203">b.</span><span class="sxs-lookup"><span data-stu-id="b41c8-203">b.</span></span> <span data-ttu-id="b41c8-204">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b41c8-204">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b41c8-205">c.</span><span class="sxs-lookup"><span data-stu-id="b41c8-205">c.</span></span> <span data-ttu-id="b41c8-206">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="b41c8-206">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b41c8-207">d.</span><span class="sxs-lookup"><span data-stu-id="b41c8-207">d.</span></span> <span data-ttu-id="b41c8-208">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="b41c8-208">Click **Create**.</span></span>
 
### <a name="creating-a-jitbit-helpdesk-test-user"></a><span data-ttu-id="b41c8-209">Создание тестового пользователя Jitbit Helpdesk</span><span class="sxs-lookup"><span data-stu-id="b41c8-209">Creating a Jitbit Helpdesk test user</span></span>

<span data-ttu-id="b41c8-210">Чтобы пользователи Azure AD могли выполнять вход в Jitbit Helpdesk, они должны быть подготовлены для Jitbit Helpdesk.</span><span class="sxs-lookup"><span data-stu-id="b41c8-210">In order to enable Azure AD users to log into Jitbit Helpdesk, they must be provisioned into Jitbit Helpdesk.</span></span>  <span data-ttu-id="b41c8-211">В случае с Jitbit Helpdesk подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="b41c8-211">In the case of Jitbit Helpdesk, provisioning is a manual task.</span></span>

<span data-ttu-id="b41c8-212">**Чтобы подготовить учетную запись пользователя, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="b41c8-212">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="b41c8-213">Выполните вход в клиент **Jitbit Helpdesk** .</span><span class="sxs-lookup"><span data-stu-id="b41c8-213">Log in to your **Jitbit Helpdesk** tenant.</span></span>

2. <span data-ttu-id="b41c8-214">В верхнем меню щелкните **Администрирование**.</span><span class="sxs-lookup"><span data-stu-id="b41c8-214">In the menu on the top, click **Administration**.</span></span>
   
    <span data-ttu-id="b41c8-215">![Администрирование](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "Администрирование")</span><span class="sxs-lookup"><span data-stu-id="b41c8-215">![Administration](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777681.png "Administration")</span></span>

3. <span data-ttu-id="b41c8-216">Нажмите кнопку **Пользователи, компании и разрешения**.</span><span class="sxs-lookup"><span data-stu-id="b41c8-216">Click **Users, companies and permissions**.</span></span>
   
    <span data-ttu-id="b41c8-217">![Пользователи, организации и разрешения](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777682.png "Пользователи, организации и разрешения")</span><span class="sxs-lookup"><span data-stu-id="b41c8-217">![Users, companies, and permissions](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777682.png "Users, companies, and permissions")</span></span>

4. <span data-ttu-id="b41c8-218">Нажмите кнопку **Добавить пользователя**.</span><span class="sxs-lookup"><span data-stu-id="b41c8-218">Click **Add user**.</span></span>
   
    <span data-ttu-id="b41c8-219">![Добавление пользователя](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777685.png "Добавление пользователя")</span><span class="sxs-lookup"><span data-stu-id="b41c8-219">![Add user](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777685.png "Add user")</span></span>
   
5. <span data-ttu-id="b41c8-220">В разделе Create (Создание) введите данные учетной записи Azure AD, которую необходимо подготовить, в следующие текстовые поля:</span><span class="sxs-lookup"><span data-stu-id="b41c8-220">In the Create section, type the data of the Azure AD account you want to provision as follows:</span></span>

    <span data-ttu-id="b41c8-221">![Создание](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777686.png "Создание")</span><span class="sxs-lookup"><span data-stu-id="b41c8-221">![Create](./media/active-directory-saas-jitbit-helpdesk-tutorial/ic777686.png "Create")</span></span>
   
   <span data-ttu-id="b41c8-222">а.</span><span class="sxs-lookup"><span data-stu-id="b41c8-222">a.</span></span> <span data-ttu-id="b41c8-223">В текстовое поле **Username** (Имя пользователя) введите имя пользователя **Britta Simon**, используемое на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="b41c8-223">In the **Username** textbox, type **BrittaSimon**, the user name as in the Azure portal.</span></span>

   <span data-ttu-id="b41c8-224">b.</span><span class="sxs-lookup"><span data-stu-id="b41c8-224">b.</span></span> <span data-ttu-id="b41c8-225">В текстовое поле **Email** (Адрес электронной почты) введите адрес электронной почты пользователя, например **BrittaSimon@contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="b41c8-225">In the **Email** textbox, type email of the user like **BrittaSimon@contoso.com**.</span></span>

   <span data-ttu-id="b41c8-226">c.</span><span class="sxs-lookup"><span data-stu-id="b41c8-226">c.</span></span> <span data-ttu-id="b41c8-227">В текстовое поле **First Name** (Имя) введите имя пользователя, например **Britta**.</span><span class="sxs-lookup"><span data-stu-id="b41c8-227">In the **First Name** textbox, type first name of the user like **Britta**.</span></span>

   <span data-ttu-id="b41c8-228">г)</span><span class="sxs-lookup"><span data-stu-id="b41c8-228">d.</span></span> <span data-ttu-id="b41c8-229">В текстовое поле **Last Name** (Фамилия) введите фамилию, например, **Simon**.</span><span class="sxs-lookup"><span data-stu-id="b41c8-229">In the **Last Name** textbox, type last name of the user like **Simon**.</span></span>
   
   <span data-ttu-id="b41c8-230">д.</span><span class="sxs-lookup"><span data-stu-id="b41c8-230">e.</span></span> <span data-ttu-id="b41c8-231">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="b41c8-231">Click **Create**.</span></span>

>[!NOTE]
><span data-ttu-id="b41c8-232">Вы можете использовать любые другие средства создания учетной записи пользователя Jitbit Helpdesk или API, предоставляемые Jitbit Helpdesk для подготовки учетных записей пользователя Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b41c8-232">You can use any other Jitbit Helpdesk user account creation tools or APIs provided by Jitbit Helpdesk to provision Azure AD user accounts.</span></span>
> 
        

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b41c8-233">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="b41c8-233">Assigning the Azure AD test user</span></span>

<span data-ttu-id="b41c8-234">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к Jitbit Helpdesk.</span><span class="sxs-lookup"><span data-stu-id="b41c8-234">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Jitbit Helpdesk.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="b41c8-236">**Чтобы назначить пользователя Britta Simon в Jitbit Helpdesk, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="b41c8-236">**To assign Britta Simon to Jitbit Helpdesk, perform the following steps:**</span></span>

1. <span data-ttu-id="b41c8-237">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="b41c8-237">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="b41c8-239">В списке приложений выберите **Jitbit Helpdesk**.</span><span class="sxs-lookup"><span data-stu-id="b41c8-239">In the applications list, select **Jitbit Helpdesk**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_jitbit-helpdesk_app.png) 

3. <span data-ttu-id="b41c8-241">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="b41c8-241">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="b41c8-243">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="b41c8-243">Click **Add** button.</span></span> <span data-ttu-id="b41c8-244">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="b41c8-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="b41c8-246">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="b41c8-246">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b41c8-247">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="b41c8-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b41c8-248">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="b41c8-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b41c8-249">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="b41c8-249">Testing single sign-on</span></span>

<span data-ttu-id="b41c8-250">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="b41c8-250">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b41c8-251">Когда вы щелкните элемент Jitbit Helpdesk на панели доступа, должна появиться страница входа в приложение Jitbit Helpdesk.</span><span class="sxs-lookup"><span data-stu-id="b41c8-251">When you click the Jitbit Helpdesk tile in the Access Panel, you should get login page of Jitbit Helpdesk application.</span></span>
<span data-ttu-id="b41c8-252">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b41c8-252">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b41c8-253">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="b41c8-253">Additional resources</span></span>

* [<span data-ttu-id="b41c8-254">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b41c8-254">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b41c8-255">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b41c8-255">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-jitbit-helpdesk-tutorial/tutorial_general_203.png

