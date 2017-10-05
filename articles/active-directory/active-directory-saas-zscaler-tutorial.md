---
title: "Руководство. Интеграция Azure Active Directory с Zscaler | Документация Майкрософт"
description: "Вы можете узнать, как настроить единый вход Azure Active Directory в Zscaler."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 68c453f7-aff1-4614-92d3-9b86f3ad99dc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: 73c81691b68ee820e1d905a17b4f2ab6b6ceb5fd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler"></a><span data-ttu-id="f0320-103">Руководство. Интеграция Azure Active Directory с Zscaler</span><span class="sxs-lookup"><span data-stu-id="f0320-103">Tutorial: Azure Active Directory integration with Zscaler</span></span>

<span data-ttu-id="f0320-104">Это руководство описывает, как интегрировать Zscaler с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f0320-104">In this tutorial, you learn how to integrate Zscaler with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f0320-105">Интеграция Azure AD с Zscaler обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="f0320-105">Integrating Zscaler with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f0320-106">С помощью Azure AD вы можете контролировать доступ к Zscaler.</span><span class="sxs-lookup"><span data-stu-id="f0320-106">You can control in Azure AD who has access to Zscaler</span></span>
- <span data-ttu-id="f0320-107">Вы можете включить автоматический вход пользователей в Zscaler (единый вход) с использованием учетных записей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f0320-107">You can enable your users to automatically get signed-on to Zscaler (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f0320-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="f0320-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f0320-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f0320-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f0320-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="f0320-110">Prerequisites</span></span>

<span data-ttu-id="f0320-111">Чтобы настроить интеграцию Azure AD с Zscaler, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="f0320-111">To configure Azure AD integration with Zscaler, you need the following items:</span></span>

- <span data-ttu-id="f0320-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="f0320-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f0320-113">подписка Zscaler с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="f0320-113">A Zscaler single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f0320-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="f0320-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f0320-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="f0320-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f0320-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="f0320-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f0320-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f0320-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f0320-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="f0320-118">Scenario description</span></span>
<span data-ttu-id="f0320-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="f0320-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f0320-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="f0320-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f0320-121">Добавление Zscaler из коллекции.</span><span class="sxs-lookup"><span data-stu-id="f0320-121">Adding Zscaler from the gallery</span></span>
2. <span data-ttu-id="f0320-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="f0320-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zscaler-from-the-gallery"></a><span data-ttu-id="f0320-123">Добавление Zscaler из коллекции</span><span class="sxs-lookup"><span data-stu-id="f0320-123">Adding Zscaler from the gallery</span></span>
<span data-ttu-id="f0320-124">Чтобы настроить интеграцию Zscaler с Azure AD, нужно добавить Zscaler из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="f0320-124">To configure the integration of Zscaler into Azure AD, you need to add Zscaler from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f0320-125">**Чтобы добавить Zscaler из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="f0320-125">**To add Zscaler from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f0320-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f0320-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f0320-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="f0320-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f0320-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="f0320-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="f0320-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="f0320-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="f0320-133">В поле поиска введите **Zscaler**.</span><span class="sxs-lookup"><span data-stu-id="f0320-133">In the search box, type **Zscaler**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_search.png)

5. <span data-ttu-id="f0320-135">На панели результатов выберите **Zscaler** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="f0320-135">In the results panel, select **Zscaler**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f0320-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="f0320-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f0320-138">В этом разделе описана настройка и проверка единого входа Azure AD в Zscaler с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f0320-138">In this section, you configure and test Azure AD single sign-on with Zscaler based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="f0320-139">Чтобы единый вход работал, Azure AD необходима информация о том, какой пользователь в Zscaler соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f0320-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Zscaler is to a user in Azure AD.</span></span> <span data-ttu-id="f0320-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Zscaler.</span><span class="sxs-lookup"><span data-stu-id="f0320-140">In other words, a link relationship between an Azure AD user and the related user in Zscaler needs to be established.</span></span>

<span data-ttu-id="f0320-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Zscaler.</span><span class="sxs-lookup"><span data-stu-id="f0320-141">In Zscaler, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f0320-142">Чтобы настроить и проверить единый вход Azure AD в Zscaler, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="f0320-142">To configure and test Azure AD single sign-on with Zscaler, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f0320-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="f0320-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f0320-144">**[Настройка параметров прокси-сервера](#configuring-proxy-settings)** нужна для настройки параметров прокси-сервера в Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="f0320-144">**[Configuring proxy settings](#configuring-proxy-settings)** - to configure the proxy settings in Internet Explorer</span></span>
3. <span data-ttu-id="f0320-145">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f0320-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="f0320-146">**[Создание тестового пользователя Zscaler](#creating-a-zscaler-test-user)** требуется для того, чтобы в Zscaler существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f0320-146">**[Creating a Zscaler test user](#creating-a-zscaler-test-user)** - to have a counterpart of Britta Simon in Zscaler that is linked to the Azure AD representation of user.</span></span>
5. <span data-ttu-id="f0320-147">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f0320-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
6. <span data-ttu-id="f0320-148">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="f0320-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f0320-149">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="f0320-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f0320-150">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Zscaler.</span><span class="sxs-lookup"><span data-stu-id="f0320-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Zscaler application.</span></span>

<span data-ttu-id="f0320-151">**Чтобы настроить единый вход Azure AD в Zscaler, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="f0320-151">**To configure Azure AD single sign-on with Zscaler, perform the following steps:**</span></span>

1. <span data-ttu-id="f0320-152">На портале Azure на странице интеграции с приложением **Zscaler** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="f0320-152">In the Azure portal, on the **Zscaler** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="f0320-154">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="f0320-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_samlbase.png)

3. <span data-ttu-id="f0320-156">В разделе **Домены и URL-адреса приложения Zscaler** сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="f0320-156">On the **Zscaler Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_url.png)

    <span data-ttu-id="f0320-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<companyname>.zsclaer.net`</span><span class="sxs-lookup"><span data-stu-id="f0320-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<companyname>.zsclaer.net`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f0320-159">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="f0320-159">This value is not real.</span></span> <span data-ttu-id="f0320-160">Вместо него необходимо указать фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="f0320-160">Update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="f0320-161">Для получения этого значения обратитесь к [группе поддержки клиентов Zscaler](https://www.zscaler.com/company/contact).</span><span class="sxs-lookup"><span data-stu-id="f0320-161">Contact [Zscaler Client support team](https://www.zscaler.com/company/contact) to get this value.</span></span> 

4. <span data-ttu-id="f0320-162">В разделе **Сертификат подписи SAML** щелкните **Сертификат (Base64)**, а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="f0320-162">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_certificate.png) 

5. <span data-ttu-id="f0320-164">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="f0320-164">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-zscaler-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f0320-166">В разделе **Конфигурация Zscaler** щелкните **настроить Zscaler**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="f0320-166">On the **Zscaler Configuration** section, click **Configure Zscaler** to open **Configure sign-on** window.</span></span> <span data-ttu-id="f0320-167">Скопируйте **URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="f0320-167">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_configure.png) 

7. <span data-ttu-id="f0320-169">В другом окне веб-браузера войдите на свой корпоративный сайт Zscaler в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="f0320-169">In a different web browser window, log in to your ZScaler company site as an administrator.</span></span>

8. <span data-ttu-id="f0320-170">В верхнем меню щелкните **Администрирование**.</span><span class="sxs-lookup"><span data-stu-id="f0320-170">In the menu on the top, click **Administration**.</span></span>
   
    <span data-ttu-id="f0320-171">![Администрирование](./media/active-directory-saas-zscaler-tutorial/ic800206.png "Администрирование")</span><span class="sxs-lookup"><span data-stu-id="f0320-171">![Administration](./media/active-directory-saas-zscaler-tutorial/ic800206.png "Administration")</span></span>

9. <span data-ttu-id="f0320-172">В разделе **Manage Administrators & Roles** (Управление администраторами и ролями) щелкните **Manage Users & Authentication** (Управление пользователями и проверкой подлинности).</span><span class="sxs-lookup"><span data-stu-id="f0320-172">Under **Manage Administrators & Roles**, click **Manage Users & Authentication**.</span></span>   
            
    <span data-ttu-id="f0320-173">![Управление пользователями и проверкой подлинности](./media/active-directory-saas-zscaler-tutorial/ic800207.png "Управление пользователями и проверкой подлинности")</span><span class="sxs-lookup"><span data-stu-id="f0320-173">![Manage Users & Authentication](./media/active-directory-saas-zscaler-tutorial/ic800207.png "Manage Users & Authentication")</span></span>

10. <span data-ttu-id="f0320-174">В разделе **Выбор параметров проверки подлинности для организации** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="f0320-174">In the **Choose Authentication Options for your Organization** section, perform the following steps:</span></span>   
                
    <span data-ttu-id="f0320-175">![Аутентификация](./media/active-directory-saas-zscaler-tutorial/ic800208.png "Аутентификация")</span><span class="sxs-lookup"><span data-stu-id="f0320-175">![Authentication](./media/active-directory-saas-zscaler-tutorial/ic800208.png "Authentication")</span></span>
   
    <span data-ttu-id="f0320-176">а.</span><span class="sxs-lookup"><span data-stu-id="f0320-176">a.</span></span> <span data-ttu-id="f0320-177">Выберите параметр **Проверка подлинности с помощью единого входа SAML**.</span><span class="sxs-lookup"><span data-stu-id="f0320-177">Select **Authenticate using SAML Single Sign-On**.</span></span>

    <span data-ttu-id="f0320-178">b.</span><span class="sxs-lookup"><span data-stu-id="f0320-178">b.</span></span> <span data-ttu-id="f0320-179">Щелкните **Настроить параметры единого входа SAML**.</span><span class="sxs-lookup"><span data-stu-id="f0320-179">Click **Configure SAML Single Sign-On Parameters**.</span></span>

11. <span data-ttu-id="f0320-180">На странице диалогового окна **Configure SAML Single Sign-On Parameters** (Настройка параметров единого входа в SAML) выполните указанные ниже действия и нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="f0320-180">On the **Configure SAML Single Sign-On Parameters** dialog page, perform the following steps, and then click **Done**</span></span>

    <span data-ttu-id="f0320-181">![Единый вход](./media/active-directory-saas-zscaler-tutorial/ic800209.png "Единый вход")</span><span class="sxs-lookup"><span data-stu-id="f0320-181">![Single Sign-On](./media/active-directory-saas-zscaler-tutorial/ic800209.png "Single Sign-On")</span></span>
    
    <span data-ttu-id="f0320-182">а.</span><span class="sxs-lookup"><span data-stu-id="f0320-182">a.</span></span> <span data-ttu-id="f0320-183">Вставьте значение **SAML Single Sign-On Service URL** (URL-адрес службы единого входа SAML), скопированное на портале Azure, в текстовое поле **URL of the SAML Portal to which users are sent for authentication** (URL-адрес портала SAML, куда пользователи направляются для аутентификации).</span><span class="sxs-lookup"><span data-stu-id="f0320-183">Paste the **SAML Single Sign-On Service URL** value, which you have copied from the Azure portal into the **URL of the SAML Portal to which users are sent for authentication** textbox.</span></span>
    
    <span data-ttu-id="f0320-184">b.</span><span class="sxs-lookup"><span data-stu-id="f0320-184">b.</span></span> <span data-ttu-id="f0320-185">В текстовом поле **Attribute containing Login Name** (Атрибут, содержащий имя входа) введите **NameID**.</span><span class="sxs-lookup"><span data-stu-id="f0320-185">In the **Attribute containing Login Name** textbox, type **NameID**.</span></span>
    
    <span data-ttu-id="f0320-186">c.</span><span class="sxs-lookup"><span data-stu-id="f0320-186">c.</span></span> <span data-ttu-id="f0320-187">Чтобы передать скачанный сертификат, щелкните **Zscaler pem**.</span><span class="sxs-lookup"><span data-stu-id="f0320-187">To upload your downloaded certificate, click **Zscaler pem**.</span></span>
    
    <span data-ttu-id="f0320-188">г)</span><span class="sxs-lookup"><span data-stu-id="f0320-188">d.</span></span> <span data-ttu-id="f0320-189">Выберите параметр **Включить автоматическую подготовку SAML**.</span><span class="sxs-lookup"><span data-stu-id="f0320-189">Select **Enable SAML Auto-Provisioning**.</span></span>

12. <span data-ttu-id="f0320-190">На странице **Настройка проверки подлинности пользователей** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="f0320-190">On the **Configure User Authentication** dialog page, perform the following steps:</span></span>

    <span data-ttu-id="f0320-191">![Администрирование](./media/active-directory-saas-zscaler-tutorial/ic800210.png "Администрирование")</span><span class="sxs-lookup"><span data-stu-id="f0320-191">![Administration](./media/active-directory-saas-zscaler-tutorial/ic800210.png "Administration")</span></span>
    
    <span data-ttu-id="f0320-192">а.</span><span class="sxs-lookup"><span data-stu-id="f0320-192">a.</span></span> <span data-ttu-id="f0320-193">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="f0320-193">Click **Save**.</span></span>

    <span data-ttu-id="f0320-194">b.</span><span class="sxs-lookup"><span data-stu-id="f0320-194">b.</span></span> <span data-ttu-id="f0320-195">Щелкните **Активировать сейчас**.</span><span class="sxs-lookup"><span data-stu-id="f0320-195">Click **Activate Now**.</span></span>

## <a name="configuring-proxy-settings"></a><span data-ttu-id="f0320-196">Настройка параметров прокси-сервера</span><span class="sxs-lookup"><span data-stu-id="f0320-196">Configuring proxy settings</span></span>
### <a name="to-configure-the-proxy-settings-in-internet-explorer"></a><span data-ttu-id="f0320-197">Настройка параметров прокси-сервера в Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="f0320-197">To configure the proxy settings in Internet Explorer</span></span>

1. <span data-ttu-id="f0320-198">Запустите **Internet Explorer**.</span><span class="sxs-lookup"><span data-stu-id="f0320-198">Start **Internet Explorer**.</span></span>

2. <span data-ttu-id="f0320-199">В меню **Сервис** выберите **Свойства браузера**, чтобы открыть диалоговое окно **Свойства браузера**.</span><span class="sxs-lookup"><span data-stu-id="f0320-199">Select **Internet options** from the **Tools** menu for open the **Internet Options** dialog.</span></span>   
    
     <span data-ttu-id="f0320-200">![Свойства браузера](./media/active-directory-saas-zscaler-tutorial/ic769492.png "Свойства браузера")</span><span class="sxs-lookup"><span data-stu-id="f0320-200">![Internet Options](./media/active-directory-saas-zscaler-tutorial/ic769492.png "Internet Options")</span></span>

3. <span data-ttu-id="f0320-201">Щелкните вкладку **Подключения** .</span><span class="sxs-lookup"><span data-stu-id="f0320-201">Click the **Connections** tab.</span></span>   
  
     <span data-ttu-id="f0320-202">![Подключения](./media/active-directory-saas-zscaler-tutorial/ic769493.png "Подключения")</span><span class="sxs-lookup"><span data-stu-id="f0320-202">![Connections](./media/active-directory-saas-zscaler-tutorial/ic769493.png "Connections")</span></span>

4. <span data-ttu-id="f0320-203">Нажмите кнопку **Настройка сети**, чтобы открыть диалоговое окно **Настройка сети**.</span><span class="sxs-lookup"><span data-stu-id="f0320-203">Click **LAN settings** to open the **LAN Settings** dialog.</span></span>

5. <span data-ttu-id="f0320-204">В разделе "Прокси-сервер" выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="f0320-204">In the Proxy server section, perform the following steps:</span></span>   
   
    <span data-ttu-id="f0320-205">![Прокси-сервер](./media/active-directory-saas-zscaler-tutorial/ic769494.png "Прокси-сервер")</span><span class="sxs-lookup"><span data-stu-id="f0320-205">![Proxy server](./media/active-directory-saas-zscaler-tutorial/ic769494.png "Proxy server")</span></span>

    <span data-ttu-id="f0320-206">а.</span><span class="sxs-lookup"><span data-stu-id="f0320-206">a.</span></span> <span data-ttu-id="f0320-207">Установите флажок **Использовать прокси-сервер для локальной сети**.</span><span class="sxs-lookup"><span data-stu-id="f0320-207">Select **Use a proxy server for your LAN**.</span></span>

    <span data-ttu-id="f0320-208">b.</span><span class="sxs-lookup"><span data-stu-id="f0320-208">b.</span></span> <span data-ttu-id="f0320-209">В текстовом поле "Адрес" введите **gateway.zscaler.net**.</span><span class="sxs-lookup"><span data-stu-id="f0320-209">In the Address textbox, type **gateway.zscaler.net**.</span></span>

    <span data-ttu-id="f0320-210">c.</span><span class="sxs-lookup"><span data-stu-id="f0320-210">c.</span></span> <span data-ttu-id="f0320-211">В текстовом поле "Порт" введите **80**.</span><span class="sxs-lookup"><span data-stu-id="f0320-211">In the Port textbox, type **80**.</span></span>

    <span data-ttu-id="f0320-212">г)</span><span class="sxs-lookup"><span data-stu-id="f0320-212">d.</span></span> <span data-ttu-id="f0320-213">Установите флаг **Не использовать прокси-сервер для локальных адресов**.</span><span class="sxs-lookup"><span data-stu-id="f0320-213">Select **Bypass proxy server for local addresses**.</span></span>

    <span data-ttu-id="f0320-214">д.</span><span class="sxs-lookup"><span data-stu-id="f0320-214">e.</span></span> <span data-ttu-id="f0320-215">Нажмите кнопку **ОК**, чтобы закрыть диалоговое окно **Настройка параметров локальной сети**.</span><span class="sxs-lookup"><span data-stu-id="f0320-215">Click **OK** to close the **Local Area Network (LAN) Settings** dialog.</span></span>

6. <span data-ttu-id="f0320-216">Нажмите кнопку **ОК**, чтобы закрыть диалоговое окно **Свойства браузера**.</span><span class="sxs-lookup"><span data-stu-id="f0320-216">Click **OK** to close the **Internet Options** dialog.</span></span>

> [!TIP]
> <span data-ttu-id="f0320-217">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="f0320-217">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f0320-218">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="f0320-218">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f0320-219">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="f0320-219">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f0320-220">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="f0320-220">Creating an Azure AD test user</span></span>
<span data-ttu-id="f0320-221">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f0320-221">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="f0320-223">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="f0320-223">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f0320-224">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f0320-224">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zscaler-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f0320-226">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="f0320-226">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zscaler-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f0320-228">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="f0320-228">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zscaler-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f0320-230">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="f0320-230">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zscaler-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f0320-232">а.</span><span class="sxs-lookup"><span data-stu-id="f0320-232">a.</span></span> <span data-ttu-id="f0320-233">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f0320-233">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f0320-234">b.</span><span class="sxs-lookup"><span data-stu-id="f0320-234">b.</span></span> <span data-ttu-id="f0320-235">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f0320-235">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f0320-236">c.</span><span class="sxs-lookup"><span data-stu-id="f0320-236">c.</span></span> <span data-ttu-id="f0320-237">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="f0320-237">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f0320-238">d.</span><span class="sxs-lookup"><span data-stu-id="f0320-238">d.</span></span> <span data-ttu-id="f0320-239">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="f0320-239">Click **Create**.</span></span>
 
### <a name="creating-a-zscaler-test-user"></a><span data-ttu-id="f0320-240">Создание тестового пользователя Zscaler</span><span class="sxs-lookup"><span data-stu-id="f0320-240">Creating a Zscaler test user</span></span>

<span data-ttu-id="f0320-241">Чтобы пользователи Azure AD могли выполнять вход в Zscaler, их необходимо подготовить в Zscaler.</span><span class="sxs-lookup"><span data-stu-id="f0320-241">To enable Azure AD users to log in to ZScaler, they must be provisioned to ZScaler.</span></span>  
<span data-ttu-id="f0320-242">В случае Zscaler подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="f0320-242">In the case of ZScaler, provisioning is a manual task.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="f0320-243">Чтобы настроить подготовку учетных записей пользователей, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="f0320-243">To configure user provisioning, perform the following steps:</span></span>

1. <span data-ttu-id="f0320-244">Войдите в клиент **ZScaler** .</span><span class="sxs-lookup"><span data-stu-id="f0320-244">Log in to your **Zscaler** tenant.</span></span>

2. <span data-ttu-id="f0320-245">Щелкните **Администрирование**.</span><span class="sxs-lookup"><span data-stu-id="f0320-245">Click **Administration**.</span></span>   
   
    <span data-ttu-id="f0320-246">![Администрирование](./media/active-directory-saas-zscaler-tutorial/ic781035.png "Администрирование")</span><span class="sxs-lookup"><span data-stu-id="f0320-246">![Administration](./media/active-directory-saas-zscaler-tutorial/ic781035.png "Administration")</span></span>

3. <span data-ttu-id="f0320-247">Щелкните **Управление пользователями**.</span><span class="sxs-lookup"><span data-stu-id="f0320-247">Click **User Management**.</span></span>   
        
     <span data-ttu-id="f0320-248">![Добавление](./media/active-directory-saas-zscaler-tutorial/ic781036.png "Добавление")</span><span class="sxs-lookup"><span data-stu-id="f0320-248">![Add](./media/active-directory-saas-zscaler-tutorial/ic781036.png "Add")</span></span>

4. <span data-ttu-id="f0320-249">На вкладке **Users** (Пользователи) нажмите кнопку **Add** (Добавить).</span><span class="sxs-lookup"><span data-stu-id="f0320-249">In the **Users** tab, click **Add**.</span></span>
      
    <span data-ttu-id="f0320-250">![Добавление](./media/active-directory-saas-zscaler-tutorial/ic781037.png "Добавление")</span><span class="sxs-lookup"><span data-stu-id="f0320-250">![Add](./media/active-directory-saas-zscaler-tutorial/ic781037.png "Add")</span></span>

5. <span data-ttu-id="f0320-251">В разделе "Добавить пользователя" выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="f0320-251">In the Add User section, perform the following steps:</span></span>
        
    <span data-ttu-id="f0320-252">![Добавление пользователя](./media/active-directory-saas-zscaler-tutorial/ic781038.png "Добавление пользователя")</span><span class="sxs-lookup"><span data-stu-id="f0320-252">![Add User](./media/active-directory-saas-zscaler-tutorial/ic781038.png "Add User")</span></span>
   
    <span data-ttu-id="f0320-253">а.</span><span class="sxs-lookup"><span data-stu-id="f0320-253">a.</span></span> <span data-ttu-id="f0320-254">Заполните текстовые поля **UserID** (Идентификатор пользователя), **User Display Name** (Отображаемое имя пользователя), **Password** (Пароль), **Confirm Password** (Подтверждение пароля) и выберите **Groups** (Группы) и **Department** (Отдел) действующей учетной записи AAD, которую необходимо подготовить.</span><span class="sxs-lookup"><span data-stu-id="f0320-254">Type the **UserID**, **User Display Name**, **Password**, **Confirm Password**, and then select **Groups** and the **Department** of a valid AAD account you want to provision.</span></span>

    <span data-ttu-id="f0320-255">b.</span><span class="sxs-lookup"><span data-stu-id="f0320-255">b.</span></span> <span data-ttu-id="f0320-256">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="f0320-256">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="f0320-257">Вы можете использовать любые другие инструменты создания учетных записей пользователя ZScaler или API, предоставляемые ZScaler для подготовки учетных записей пользователя Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f0320-257">You can use any other ZScaler user account creation tools or APIs provided by ZScaler to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f0320-258">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="f0320-258">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f0320-259">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к Zscaler.</span><span class="sxs-lookup"><span data-stu-id="f0320-259">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Zscaler.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="f0320-261">**Чтобы назначить пользователя Britta Simon в Zscaler, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="f0320-261">**To assign Britta Simon to Zscaler, perform the following steps:**</span></span>

1. <span data-ttu-id="f0320-262">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="f0320-262">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="f0320-264">Из списка приложений выберите **Zscaler**.</span><span class="sxs-lookup"><span data-stu-id="f0320-264">In the applications list, select **Zscaler**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-zscaler-tutorial/tutorial_zscaler_app.png) 

3. <span data-ttu-id="f0320-266">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="f0320-266">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="f0320-268">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="f0320-268">Click **Add** button.</span></span> <span data-ttu-id="f0320-269">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="f0320-269">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="f0320-271">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="f0320-271">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f0320-272">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="f0320-272">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f0320-273">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="f0320-273">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f0320-274">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="f0320-274">Testing single sign-on</span></span>

<span data-ttu-id="f0320-275">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="f0320-275">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="f0320-276">Щелкнув элемент "Zscaler" на панели доступа, вы автоматически войдете в приложение Zscaler.</span><span class="sxs-lookup"><span data-stu-id="f0320-276">When you click the Zscaler tile in the Access Panel, you should get automatically signed-on to your Zscaler application.</span></span>
<span data-ttu-id="f0320-277">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f0320-277">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f0320-278">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="f0320-278">Additional resources</span></span>

* [<span data-ttu-id="f0320-279">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f0320-279">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f0320-280">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f0320-280">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscaler-tutorial/tutorial_general_203.png

