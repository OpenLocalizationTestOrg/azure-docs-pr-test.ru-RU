---
title: "Руководство по интеграции Azure Active Directory с Zscaler Two | Документация Майкрософт"
description: "Вы можете узнать, как настроить единый вход Azure Active Directory в Zscaler Two."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1fd8a940-7320-47e0-a176-2dd4eeca6db2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 38c9da0a6599bb66c452fdb8a8911338601155f9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler-two"></a><span data-ttu-id="ec484-103">Руководство по интеграции Azure Active Directory с Zscaler Two</span><span class="sxs-lookup"><span data-stu-id="ec484-103">Tutorial: Azure Active Directory integration with Zscaler Two</span></span>

<span data-ttu-id="ec484-104">Это руководство описывает, как интегрировать Zscaler Two с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ec484-104">In this tutorial, you learn how to integrate Zscaler Two with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ec484-105">Интеграция Azure AD с Zscaler Two обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="ec484-105">Integrating Zscaler Two with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="ec484-106">С помощью Azure AD вы можете контролировать доступ к Zscaler Two.</span><span class="sxs-lookup"><span data-stu-id="ec484-106">You can control in Azure AD who has access to Zscaler Two</span></span>
- <span data-ttu-id="ec484-107">Вы можете включить автоматический вход пользователей в Zscaler Two (единый вход) с использованием учетных записей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ec484-107">You can enable your users to automatically get signed-on to Zscaler Two (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ec484-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="ec484-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="ec484-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ec484-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ec484-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="ec484-110">Prerequisites</span></span>

<span data-ttu-id="ec484-111">Чтобы настроить интеграцию Azure AD с Zscaler Two, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="ec484-111">To configure Azure AD integration with Zscaler Two, you need the following items:</span></span>

- <span data-ttu-id="ec484-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="ec484-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ec484-113">подписка Zscaler Two с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="ec484-113">A Zscaler Two single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ec484-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="ec484-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ec484-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="ec484-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ec484-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="ec484-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ec484-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ec484-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ec484-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="ec484-118">Scenario description</span></span>
<span data-ttu-id="ec484-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="ec484-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ec484-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="ec484-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ec484-121">Добавление Zscaler Two из коллекции.</span><span class="sxs-lookup"><span data-stu-id="ec484-121">Adding Zscaler Two from the gallery</span></span>
2. <span data-ttu-id="ec484-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ec484-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zscaler-two-from-the-gallery"></a><span data-ttu-id="ec484-123">Добавление Zscaler Two из коллекции</span><span class="sxs-lookup"><span data-stu-id="ec484-123">Adding Zscaler Two from the gallery</span></span>
<span data-ttu-id="ec484-124">Чтобы настроить интеграцию Zscaler Two с Azure AD, нужно добавить Zscaler Two из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="ec484-124">To configure the integration of Zscaler Two into Azure AD, you need to add Zscaler Two from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="ec484-125">**Чтобы добавить Zscaler Two из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="ec484-125">**To add Zscaler Two from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="ec484-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ec484-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ec484-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="ec484-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="ec484-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="ec484-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="ec484-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="ec484-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="ec484-133">В поле поиска введите **Zscaler Two**.</span><span class="sxs-lookup"><span data-stu-id="ec484-133">In the search box, type **Zscaler Two**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zscaler-two-tutorial/tutorial_zscalertwo_search.png)

5. <span data-ttu-id="ec484-135">На панели результатов выберите **Zscaler Two** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="ec484-135">In the results panel, select **Zscaler Two**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zscaler-two-tutorial/tutorial_zscalertwo_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ec484-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ec484-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ec484-138">В этом разделе описана настройка и проверка единого входа Azure AD в Zscaler Two с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ec484-138">In this section, you configure and test Azure AD single sign-on with Zscaler Two based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="ec484-139">Чтобы единый вход работал, Azure AD необходима информация о том, какой пользователь в Zscaler Two соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ec484-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Zscaler Two is to a user in Azure AD.</span></span> <span data-ttu-id="ec484-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Zscaler Two.</span><span class="sxs-lookup"><span data-stu-id="ec484-140">In other words, a link relationship between an Azure AD user and the related user in Zscaler Two needs to be established.</span></span>

<span data-ttu-id="ec484-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Zscaler Two.</span><span class="sxs-lookup"><span data-stu-id="ec484-141">In Zscaler Two, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="ec484-142">Чтобы настроить и проверить единый вход Azure AD в Zscaler Two, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="ec484-142">To configure and test Azure AD single sign-on with Zscaler Two, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="ec484-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="ec484-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="ec484-144">**[Настройка параметров прокси-сервера](#configuring-proxy-settings)** нужна для настройки параметров прокси-сервера в Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="ec484-144">**[Configuring proxy settings](#configuring-proxy-settings)** - to configure the proxy settings in Internet Explorer</span></span>
3. <span data-ttu-id="ec484-145">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ec484-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="ec484-146">**[Создание тестового пользователя Zscaler Two](#creating-a-zscaler-two-test-user)** требуется для того, чтобы в Zscaler Two существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ec484-146">**[Creating a Zscaler Two test user](#creating-a-zscaler-two-test-user)** - to have a counterpart of Britta Simon in Zscaler Two that is linked to the Azure AD representation of user.</span></span>
5. <span data-ttu-id="ec484-147">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ec484-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
6. <span data-ttu-id="ec484-148">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="ec484-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ec484-149">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="ec484-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ec484-150">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Zscaler Two.</span><span class="sxs-lookup"><span data-stu-id="ec484-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Zscaler Two application.</span></span>

<span data-ttu-id="ec484-151">**Чтобы настроить единый вход Azure AD в Zscaler Two, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="ec484-151">**To configure Azure AD single sign-on with Zscaler Two, perform the following steps:**</span></span>

1. <span data-ttu-id="ec484-152">На портале Azure на странице интеграции с приложением **Zscaler Two** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="ec484-152">In the Azure portal, on the **Zscaler Two** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="ec484-154">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="ec484-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-zscaler-two-tutorial/tutorial_zscalertwo_samlbase.png)

3. <span data-ttu-id="ec484-156">В разделе **Домены и URL-адреса приложения Zscaler Two** сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="ec484-156">On the **Zscaler Two Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-zscaler-two-tutorial/tutorial_zscalertwo_url.png)

   <span data-ttu-id="ec484-158">В текстовом поле "URL-адрес входа" введите URL-адрес, с помощью которого пользователи входят в приложение Zscaler Two.</span><span class="sxs-lookup"><span data-stu-id="ec484-158">In the Sign-on URL textbox, type the URL used by your users to sign-on to your ZScaler Two application.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ec484-159">Вместо него нужно указать фактический URL-адрес для входа.</span><span class="sxs-lookup"><span data-stu-id="ec484-159">You have to update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="ec484-160">Чтобы получить эти значения, обратитесь к [группе поддержки клиентов Zscaler Two](https://www.zscaler.com/company/contact).</span><span class="sxs-lookup"><span data-stu-id="ec484-160">Contact [Zscaler Two Client support team](https://www.zscaler.com/company/contact) to get these values.</span></span>

4. <span data-ttu-id="ec484-161">В разделе **Сертификат подписи SAML** щелкните **Сертификат (Base64)**, а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="ec484-161">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-zscaler-two-tutorial/tutorial_zscalertwo_certificate.png) 

5. <span data-ttu-id="ec484-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="ec484-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-zscaler-two-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ec484-165">В разделе **Конфигурация Zscaler Two** щелкните **настроить Zscaler Two**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="ec484-165">On the **Zscaler Two Configuration** section, click **Configure Zscaler Two** to open **Configure sign-on** window.</span></span> <span data-ttu-id="ec484-166">Скопируйте **URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="ec484-166">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-zscaler-two-tutorial/tutorial_zscalertwo_configure.png) 

7. <span data-ttu-id="ec484-168">В другом окне веб-браузера войдите на свой корпоративный сайт ZScaler Two в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="ec484-168">In a different web browser window, log in to your ZScaler Two company site as an administrator.</span></span>

8. <span data-ttu-id="ec484-169">В верхнем меню щелкните **Администрирование**.</span><span class="sxs-lookup"><span data-stu-id="ec484-169">In the menu on the top, click **Administration**.</span></span>
   
    <span data-ttu-id="ec484-170">![Администрирование](./media/active-directory-saas-zscaler-two-tutorial/ic800206.png "Администрирование")</span><span class="sxs-lookup"><span data-stu-id="ec484-170">![Administration](./media/active-directory-saas-zscaler-two-tutorial/ic800206.png "Administration")</span></span>

9. <span data-ttu-id="ec484-171">В разделе **Manage Administrators & Roles** (Управление администраторами и ролями) щелкните **Manage Users & Authentication** (Управление пользователями и проверкой подлинности).</span><span class="sxs-lookup"><span data-stu-id="ec484-171">Under **Manage Administrators & Roles**, click **Manage Users & Authentication**.</span></span>   
            
    <span data-ttu-id="ec484-172">![Управление пользователями и проверкой подлинности](./media/active-directory-saas-zscaler-two-tutorial/ic800207.png "Управление пользователями и проверкой подлинности")</span><span class="sxs-lookup"><span data-stu-id="ec484-172">![Manage Users & Authentication](./media/active-directory-saas-zscaler-two-tutorial/ic800207.png "Manage Users & Authentication")</span></span>

10. <span data-ttu-id="ec484-173">В разделе **Выбор параметров проверки подлинности для организации** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="ec484-173">In the **Choose Authentication Options for your Organization** section, perform the following steps:</span></span>   
                
    <span data-ttu-id="ec484-174">![Аутентификация](./media/active-directory-saas-zscaler-two-tutorial/ic800208.png "Аутентификация")</span><span class="sxs-lookup"><span data-stu-id="ec484-174">![Authentication](./media/active-directory-saas-zscaler-two-tutorial/ic800208.png "Authentication")</span></span>
   
    <span data-ttu-id="ec484-175">а.</span><span class="sxs-lookup"><span data-stu-id="ec484-175">a.</span></span> <span data-ttu-id="ec484-176">Выберите параметр **Проверка подлинности с помощью единого входа SAML**.</span><span class="sxs-lookup"><span data-stu-id="ec484-176">Select **Authenticate using SAML Single Sign-On**.</span></span>

    <span data-ttu-id="ec484-177">b.</span><span class="sxs-lookup"><span data-stu-id="ec484-177">b.</span></span> <span data-ttu-id="ec484-178">Щелкните **Настроить параметры единого входа SAML**.</span><span class="sxs-lookup"><span data-stu-id="ec484-178">Click **Configure SAML Single Sign-On Parameters**.</span></span>

11. <span data-ttu-id="ec484-179">На странице диалогового окна **Configure SAML Single Sign-On Parameters** (Настройка параметров единого входа в SAML) выполните указанные ниже действия и нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="ec484-179">On the **Configure SAML Single Sign-On Parameters** dialog page, perform the following steps, and then click **Done**</span></span>

    <span data-ttu-id="ec484-180">![Единый вход](./media/active-directory-saas-zscaler-two-tutorial/ic800209.png "Единый вход")</span><span class="sxs-lookup"><span data-stu-id="ec484-180">![Single Sign-On](./media/active-directory-saas-zscaler-two-tutorial/ic800209.png "Single Sign-On")</span></span>
    
    <span data-ttu-id="ec484-181">а.</span><span class="sxs-lookup"><span data-stu-id="ec484-181">a.</span></span> <span data-ttu-id="ec484-182">Вставьте значение **SAML Single Sign-On Service URL** (URL-адрес службы единого входа SAML), скопированное на портале Azure, в текстовое поле **URL of the SAML Portal to which users are sent for authentication** (URL-адрес портала SAML, куда пользователи направляются для аутентификации).</span><span class="sxs-lookup"><span data-stu-id="ec484-182">Paste the **SAML Single Sign-On Service URL** value, which you have copied from the Azure portal into the **URL of the SAML Portal to which users are sent for authentication** textbox.</span></span>
    
    <span data-ttu-id="ec484-183">b.</span><span class="sxs-lookup"><span data-stu-id="ec484-183">b.</span></span> <span data-ttu-id="ec484-184">В текстовом поле **Attribute containing Login Name** (Атрибут, содержащий имя входа) введите **NameID**.</span><span class="sxs-lookup"><span data-stu-id="ec484-184">In the **Attribute containing Login Name** textbox, type **NameID**.</span></span>
    
    <span data-ttu-id="ec484-185">c.</span><span class="sxs-lookup"><span data-stu-id="ec484-185">c.</span></span> <span data-ttu-id="ec484-186">Чтобы передать скачанный сертификат, щелкните **Zscaler pem**.</span><span class="sxs-lookup"><span data-stu-id="ec484-186">To upload your downloaded certificate, click **Zscaler pem**.</span></span>
    
    <span data-ttu-id="ec484-187">г)</span><span class="sxs-lookup"><span data-stu-id="ec484-187">d.</span></span> <span data-ttu-id="ec484-188">Выберите параметр **Включить автоматическую подготовку SAML**.</span><span class="sxs-lookup"><span data-stu-id="ec484-188">Select **Enable SAML Auto-Provisioning**.</span></span>

12. <span data-ttu-id="ec484-189">На странице **Настройка проверки подлинности пользователей** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="ec484-189">On the **Configure User Authentication** dialog page, perform the following steps:</span></span>

    <span data-ttu-id="ec484-190">![Администрирование](./media/active-directory-saas-zscaler-two-tutorial/ic800210.png "Администрирование")</span><span class="sxs-lookup"><span data-stu-id="ec484-190">![Administration](./media/active-directory-saas-zscaler-two-tutorial/ic800210.png "Administration")</span></span>
    
    <span data-ttu-id="ec484-191">а.</span><span class="sxs-lookup"><span data-stu-id="ec484-191">a.</span></span> <span data-ttu-id="ec484-192">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="ec484-192">Click **Save**.</span></span>

    <span data-ttu-id="ec484-193">b.</span><span class="sxs-lookup"><span data-stu-id="ec484-193">b.</span></span> <span data-ttu-id="ec484-194">Щелкните **Активировать сейчас**.</span><span class="sxs-lookup"><span data-stu-id="ec484-194">Click **Activate Now**.</span></span>

## <a name="configuring-proxy-settings"></a><span data-ttu-id="ec484-195">Настройка параметров прокси-сервера</span><span class="sxs-lookup"><span data-stu-id="ec484-195">Configuring proxy settings</span></span>
### <a name="to-configure-the-proxy-settings-in-internet-explorer"></a><span data-ttu-id="ec484-196">Настройка параметров прокси-сервера в Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="ec484-196">To configure the proxy settings in Internet Explorer</span></span>

1. <span data-ttu-id="ec484-197">Запустите **Internet Explorer**.</span><span class="sxs-lookup"><span data-stu-id="ec484-197">Start **Internet Explorer**.</span></span>

2. <span data-ttu-id="ec484-198">В меню **Сервис** выберите **Свойства браузера**, чтобы открыть диалоговое окно **Свойства браузера**.</span><span class="sxs-lookup"><span data-stu-id="ec484-198">Select **Internet options** from the **Tools** menu for open the **Internet Options** dialog.</span></span>   
    
     <span data-ttu-id="ec484-199">![Свойства браузера](./media/active-directory-saas-zscaler-two-tutorial/ic769492.png "Свойства браузера")</span><span class="sxs-lookup"><span data-stu-id="ec484-199">![Internet Options](./media/active-directory-saas-zscaler-two-tutorial/ic769492.png "Internet Options")</span></span>

3. <span data-ttu-id="ec484-200">Щелкните вкладку **Подключения** .</span><span class="sxs-lookup"><span data-stu-id="ec484-200">Click the **Connections** tab.</span></span>   
  
     <span data-ttu-id="ec484-201">![Подключения](./media/active-directory-saas-zscaler-two-tutorial/ic769493.png "Подключения")</span><span class="sxs-lookup"><span data-stu-id="ec484-201">![Connections](./media/active-directory-saas-zscaler-two-tutorial/ic769493.png "Connections")</span></span>

4. <span data-ttu-id="ec484-202">Нажмите кнопку **Настройка сети**, чтобы открыть диалоговое окно **Настройка сети**.</span><span class="sxs-lookup"><span data-stu-id="ec484-202">Click **LAN settings** to open the **LAN Settings** dialog.</span></span>

5. <span data-ttu-id="ec484-203">В разделе "Прокси-сервер" выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="ec484-203">In the Proxy server section, perform the following steps:</span></span>   
   
    <span data-ttu-id="ec484-204">![Прокси-сервер](./media/active-directory-saas-zscaler-two-tutorial/ic769494.png "Прокси-сервер")</span><span class="sxs-lookup"><span data-stu-id="ec484-204">![Proxy server](./media/active-directory-saas-zscaler-two-tutorial/ic769494.png "Proxy server")</span></span>

    <span data-ttu-id="ec484-205">а.</span><span class="sxs-lookup"><span data-stu-id="ec484-205">a.</span></span> <span data-ttu-id="ec484-206">Установите флажок **Использовать прокси-сервер для локальной сети**.</span><span class="sxs-lookup"><span data-stu-id="ec484-206">Select **Use a proxy server for your LAN**.</span></span>

    <span data-ttu-id="ec484-207">b.</span><span class="sxs-lookup"><span data-stu-id="ec484-207">b.</span></span> <span data-ttu-id="ec484-208">В текстовом поле «Адрес» введите **gateway.zscalertwo.net**.</span><span class="sxs-lookup"><span data-stu-id="ec484-208">In the Address textbox, type **gateway.zscalertwo.net**.</span></span>

    <span data-ttu-id="ec484-209">c.</span><span class="sxs-lookup"><span data-stu-id="ec484-209">c.</span></span> <span data-ttu-id="ec484-210">В текстовом поле "Порт" введите **80**.</span><span class="sxs-lookup"><span data-stu-id="ec484-210">In the Port textbox, type **80**.</span></span>

    <span data-ttu-id="ec484-211">г)</span><span class="sxs-lookup"><span data-stu-id="ec484-211">d.</span></span> <span data-ttu-id="ec484-212">Установите флаг **Не использовать прокси-сервер для локальных адресов**.</span><span class="sxs-lookup"><span data-stu-id="ec484-212">Select **Bypass proxy server for local addresses**.</span></span>

    <span data-ttu-id="ec484-213">д.</span><span class="sxs-lookup"><span data-stu-id="ec484-213">e.</span></span> <span data-ttu-id="ec484-214">Нажмите кнопку **ОК**, чтобы закрыть диалоговое окно **Настройка параметров локальной сети**.</span><span class="sxs-lookup"><span data-stu-id="ec484-214">Click **OK** to close the **Local Area Network (LAN) Settings** dialog.</span></span>

6. <span data-ttu-id="ec484-215">Нажмите кнопку **ОК**, чтобы закрыть диалоговое окно **Свойства браузера**.</span><span class="sxs-lookup"><span data-stu-id="ec484-215">Click **OK** to close the **Internet Options** dialog.</span></span>

> [!TIP]
> <span data-ttu-id="ec484-216">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="ec484-216">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="ec484-217">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="ec484-217">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="ec484-218">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="ec484-218">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ec484-219">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="ec484-219">Creating an Azure AD test user</span></span>
<span data-ttu-id="ec484-220">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ec484-220">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="ec484-222">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="ec484-222">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="ec484-223">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ec484-223">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zscaler-two-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ec484-225">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="ec484-225">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zscaler-two-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ec484-227">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="ec484-227">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zscaler-two-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ec484-229">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="ec484-229">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zscaler-two-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ec484-231">а.</span><span class="sxs-lookup"><span data-stu-id="ec484-231">a.</span></span> <span data-ttu-id="ec484-232">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ec484-232">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ec484-233">b.</span><span class="sxs-lookup"><span data-stu-id="ec484-233">b.</span></span> <span data-ttu-id="ec484-234">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ec484-234">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ec484-235">c.</span><span class="sxs-lookup"><span data-stu-id="ec484-235">c.</span></span> <span data-ttu-id="ec484-236">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="ec484-236">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="ec484-237">d.</span><span class="sxs-lookup"><span data-stu-id="ec484-237">d.</span></span> <span data-ttu-id="ec484-238">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="ec484-238">Click **Create**.</span></span>
 
### <a name="creating-a-zscaler-two-test-user"></a><span data-ttu-id="ec484-239">Создание тестового пользователя Zscaler Two</span><span class="sxs-lookup"><span data-stu-id="ec484-239">Creating a Zscaler Two test user</span></span>

<span data-ttu-id="ec484-240">Чтобы пользователи Azure AD могли выполнять вход в Zscaler Two, их необходимо подготовить в Zscaler Two.</span><span class="sxs-lookup"><span data-stu-id="ec484-240">To enable Azure AD users to log in to ZScaler Two, they must be provisioned to ZScaler Two.</span></span> <span data-ttu-id="ec484-241">В случае с ZScaler Two подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="ec484-241">In the case of ZScaler Two, provisioning is a manual task.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="ec484-242">Чтобы настроить подготовку учетных записей пользователей, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="ec484-242">To configure user provisioning, perform the following steps:</span></span>

1. <span data-ttu-id="ec484-243">Войдите в клиент **Zscaler Two**.</span><span class="sxs-lookup"><span data-stu-id="ec484-243">Log in to your **Zscaler Two** tenant.</span></span>

2. <span data-ttu-id="ec484-244">Щелкните **Администрирование**.</span><span class="sxs-lookup"><span data-stu-id="ec484-244">Click **Administration**.</span></span>   
   
    <span data-ttu-id="ec484-245">![Администрирование](./media/active-directory-saas-zscaler-two-tutorial/ic781035.png "Администрирование")</span><span class="sxs-lookup"><span data-stu-id="ec484-245">![Administration](./media/active-directory-saas-zscaler-two-tutorial/ic781035.png "Administration")</span></span>

3. <span data-ttu-id="ec484-246">Щелкните **Управление пользователями**.</span><span class="sxs-lookup"><span data-stu-id="ec484-246">Click **User Management**.</span></span>   
        
     <span data-ttu-id="ec484-247">![Добавление](./media/active-directory-saas-zscaler-two-tutorial/ic781036.png "Добавление")</span><span class="sxs-lookup"><span data-stu-id="ec484-247">![Add](./media/active-directory-saas-zscaler-two-tutorial/ic781036.png "Add")</span></span>

4. <span data-ttu-id="ec484-248">На вкладке **Users** (Пользователи) нажмите кнопку **Add** (Добавить).</span><span class="sxs-lookup"><span data-stu-id="ec484-248">In the **Users** tab, click **Add**.</span></span>
      
    <span data-ttu-id="ec484-249">![Добавление](./media/active-directory-saas-zscaler-two-tutorial/ic781037.png "Добавление")</span><span class="sxs-lookup"><span data-stu-id="ec484-249">![Add](./media/active-directory-saas-zscaler-two-tutorial/ic781037.png "Add")</span></span>

5. <span data-ttu-id="ec484-250">В разделе "Добавить пользователя" выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="ec484-250">In the Add User section, perform the following steps:</span></span>
        
    <span data-ttu-id="ec484-251">![Добавление пользователя](./media/active-directory-saas-zscaler-two-tutorial/ic781038.png "Добавление пользователя")</span><span class="sxs-lookup"><span data-stu-id="ec484-251">![Add User](./media/active-directory-saas-zscaler-two-tutorial/ic781038.png "Add User")</span></span>
   
    <span data-ttu-id="ec484-252">а.</span><span class="sxs-lookup"><span data-stu-id="ec484-252">a.</span></span> <span data-ttu-id="ec484-253">Заполните текстовые поля **UserID** (Идентификатор пользователя), **User Display Name** (Отображаемое имя пользователя), **Password** (Пароль), **Confirm Password** (Подтверждение пароля) и выберите **Groups** (Группы) и **Department** (Отдел) для действительной учетной записи Azure AD, которую необходимо подготовить.</span><span class="sxs-lookup"><span data-stu-id="ec484-253">Type the **UserID**, **User Display Name**, **Password**, **Confirm Password**, and then select **Groups** and the **Department** of a valid Azure AD account you want to provision.</span></span>

    <span data-ttu-id="ec484-254">b.</span><span class="sxs-lookup"><span data-stu-id="ec484-254">b.</span></span> <span data-ttu-id="ec484-255">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="ec484-255">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="ec484-256">Вы можете использовать любые другие инструменты создания учетных записей пользователя ZScaler Two или API, предоставляемые ZScaler Two для подготовки учетных записей пользователя Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ec484-256">You can use any other ZScaler Two user account creation tools or APIs provided by ZScaler Two to provision Azure AD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="ec484-257">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="ec484-257">Assigning the Azure AD test user</span></span>

<span data-ttu-id="ec484-258">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к Zscaler Two.</span><span class="sxs-lookup"><span data-stu-id="ec484-258">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Zscaler Two.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="ec484-260">**Чтобы назначить пользователя Britta Simon в Zscaler Two, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="ec484-260">**To assign Britta Simon to Zscaler Two, perform the following steps:**</span></span>

1. <span data-ttu-id="ec484-261">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="ec484-261">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="ec484-263">Из списка приложений выберите **Zscaler Two**.</span><span class="sxs-lookup"><span data-stu-id="ec484-263">In the applications list, select **Zscaler Two**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-zscaler-two-tutorial/tutorial_zscalertwo_app.png) 

3. <span data-ttu-id="ec484-265">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="ec484-265">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="ec484-267">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="ec484-267">Click **Add** button.</span></span> <span data-ttu-id="ec484-268">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="ec484-268">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="ec484-270">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="ec484-270">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="ec484-271">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="ec484-271">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ec484-272">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="ec484-272">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ec484-273">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="ec484-273">Testing single sign-on</span></span>

<span data-ttu-id="ec484-274">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="ec484-274">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="ec484-275">Щелкнув элемент "Zscaler Two" на панели доступа, вы автоматически войдете в приложение Zscaler Two.</span><span class="sxs-lookup"><span data-stu-id="ec484-275">When you click the Zscaler Two tile in the Access Panel, you should get automatically signed-on to your Zscaler Two application.</span></span>
<span data-ttu-id="ec484-276">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ec484-276">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="ec484-277">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="ec484-277">Additional resources</span></span>

* [<span data-ttu-id="ec484-278">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ec484-278">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ec484-279">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ec484-279">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-zscaler-two-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscaler-two-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscaler-two-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscaler-two-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscaler-two-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscaler-two-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscaler-two-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscaler-two-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscaler-two-tutorial/tutorial_general_203.png

