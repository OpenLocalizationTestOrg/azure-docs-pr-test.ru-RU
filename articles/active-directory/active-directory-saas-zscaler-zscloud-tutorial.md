---
title: "Руководство по интеграции Azure Active Directory с Zscaler ZSCloud | Документы Майкрософт"
description: "Вы можете узнать, как настроить единый вход Azure Active Directory в Zscaler ZSCloud."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 411d5684-a780-410a-9383-59f92cf569b5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: jeedes
ms.openlocfilehash: 2b6eb113e5725260bc04f50e9218939bf28b1ff0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler-zscloud"></a><span data-ttu-id="b60a0-103">Руководство. Интеграция Azure Active Directory с Zscaler ZSCloud</span><span class="sxs-lookup"><span data-stu-id="b60a0-103">Tutorial: Azure Active Directory integration with Zscaler ZSCloud</span></span>

<span data-ttu-id="b60a0-104">Это руководство описывает, как интегрировать Zscaler ZSCloud с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b60a0-104">In this tutorial, you learn how to integrate Zscaler ZSCloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b60a0-105">Интеграция Azure AD с Zscaler ZSCloud обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="b60a0-105">Integrating Zscaler ZSCloud with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b60a0-106">С помощью Azure AD вы можете контролировать доступ к Zscaler ZSCloud.</span><span class="sxs-lookup"><span data-stu-id="b60a0-106">You can control in Azure AD who has access to Zscaler ZSCloud</span></span>
- <span data-ttu-id="b60a0-107">Вы можете включить автоматический вход пользователей в Zscaler ZSCloud (единый вход) с использованием учетных записей Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b60a0-107">You can enable your users to automatically get signed-on to Zscaler ZSCloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b60a0-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="b60a0-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b60a0-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b60a0-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b60a0-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b60a0-110">Prerequisites</span></span>

<span data-ttu-id="b60a0-111">Чтобы настроить интеграцию Azure AD с Zscaler ZSCloud, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="b60a0-111">To configure Azure AD integration with Zscaler ZSCloud, you need the following items:</span></span>

- <span data-ttu-id="b60a0-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="b60a0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b60a0-113">подписка с поддержкой единого входа Zscaler ZSCloud.</span><span class="sxs-lookup"><span data-stu-id="b60a0-113">A Zscaler ZSCloud single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b60a0-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="b60a0-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b60a0-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="b60a0-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b60a0-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="b60a0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b60a0-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b60a0-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b60a0-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="b60a0-118">Scenario description</span></span>
<span data-ttu-id="b60a0-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="b60a0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b60a0-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="b60a0-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b60a0-121">Добавление Zscaler ZSCloud из коллекции</span><span class="sxs-lookup"><span data-stu-id="b60a0-121">Adding Zscaler ZSCloud from the gallery</span></span>
2. <span data-ttu-id="b60a0-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b60a0-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-zscaler-zscloud-from-the-gallery"></a><span data-ttu-id="b60a0-123">Добавление Zscaler ZSCloud из коллекции</span><span class="sxs-lookup"><span data-stu-id="b60a0-123">Adding Zscaler ZSCloud from the gallery</span></span>
<span data-ttu-id="b60a0-124">Чтобы настроить интеграцию Zscaler ZSCloud с Azure AD, нужно добавить Zscaler ZSCloud из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="b60a0-124">To configure the integration of Zscaler ZSCloud into Azure AD, you need to add Zscaler ZSCloud from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b60a0-125">**Чтобы добавить Zscaler ZSCloud из коллекции, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="b60a0-125">**To add Zscaler ZSCloud from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b60a0-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b60a0-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b60a0-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="b60a0-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b60a0-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="b60a0-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="b60a0-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="b60a0-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="b60a0-133">В поле поиска введите **Zscaler ZSCloud**.</span><span class="sxs-lookup"><span data-stu-id="b60a0-133">In the search box, type **Zscaler ZSCloud**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_search.png)

5. <span data-ttu-id="b60a0-135">На панели результатов выберите **Zscaler ZSCloud** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="b60a0-135">In the results panel, select **Zscaler ZSCloud**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b60a0-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b60a0-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b60a0-138">Этот раздел описывает настройку и проверку единого входа Azure AD в Zscaler ZSCloud с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b60a0-138">In this section, you configure and test Azure AD single sign-on with Zscaler ZSCloud based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="b60a0-139">Чтобы настроить единый вход в Azure AD, нужно знать, какой пользователь в Zscaler ZSCloud соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b60a0-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Zscaler ZSCloud is to a user in Azure AD.</span></span> <span data-ttu-id="b60a0-140">Иными словами, нужно установить связь между пользователем Azure AD и соответствующим пользователем в Zscaler ZSCloud.</span><span class="sxs-lookup"><span data-stu-id="b60a0-140">In other words, a link relationship between an Azure AD user and the related user in Zscaler ZSCloud needs to be established.</span></span>

<span data-ttu-id="b60a0-141">Чтобы установить эту связь, следует назначить **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Zscaler ZSCloud.</span><span class="sxs-lookup"><span data-stu-id="b60a0-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Zscaler ZSCloud.</span></span>

<span data-ttu-id="b60a0-142">Чтобы настроить и проверить единый вход Azure AD в Zscaler ZSCloud, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="b60a0-142">To configure and test Azure AD single sign-on with Zscaler ZSCloud, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b60a0-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="b60a0-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b60a0-144">**[Настройка параметров прокси-сервера](#configuring-proxy-settings)** нужна для настройки параметров прокси-сервера в Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="b60a0-144">**[Configuring proxy settings](#configuring-proxy-settings)** - to configure the proxy settings in Internet Explorer</span></span>
2. <span data-ttu-id="b60a0-145">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b60a0-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)**  - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b60a0-146">**[Создание тестового пользователя Zscaler ZSCloud](#creating-a-zscaler-zscloud-test-user)** требуется для создания в Zscaler ZSCloud пользователя Britta Simon, связанного с представлением этого пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b60a0-146">**[Creating a Zscaler ZSCloud test user](#creating-a-zscaler-zscloud-test-user)** - to have a counterpart of Britta Simon in Zscaler ZSCloud that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b60a0-147">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b60a0-147">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b60a0-148">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="b60a0-148">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b60a0-149">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b60a0-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b60a0-150">Этот раздел описывает, как включить единый вход Azure AD на портале Azure и настроить его в приложении Zscaler ZSCloud.</span><span class="sxs-lookup"><span data-stu-id="b60a0-150">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Zscaler ZSCloud application.</span></span>

<span data-ttu-id="b60a0-151">**Чтобы настроить единый вход Azure AD в Zscaler ZSCloud, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="b60a0-151">**To configure Azure AD single sign-on with Zscaler ZSCloud, perform the following steps:**</span></span>

1. <span data-ttu-id="b60a0-152">На портале Azure на странице интеграции с приложением **Zscaler ZSCloud** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="b60a0-152">In the Azure portal, on the **Zscaler ZSCloud** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="b60a0-154">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="b60a0-154">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_samlbase.png)

3. <span data-ttu-id="b60a0-156">В разделе **Домены и URL-адреса приложения Zscaler ZSCloud** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="b60a0-156">On the **Zscaler ZSCloud Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_url.png)

     <span data-ttu-id="b60a0-158">В текстовом поле **URL-адрес входа** введите URL-адрес, используемый пользователями для входа в приложение Zscaler ZSCloud.</span><span class="sxs-lookup"><span data-stu-id="b60a0-158">In the **Sign-on URL** textbox, type the URL used by your users to sign-on to your ZScaler ZSCloud application.</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="b60a0-159">Вместо него нужно указать фактический URL-адрес для входа.</span><span class="sxs-lookup"><span data-stu-id="b60a0-159">You have to update this value with the actual Sign-On URL.</span></span> <span data-ttu-id="b60a0-160">Для получения этого значения обратитесь в [службу поддержки клиентов Zscaler ZSCloud](https://support.zscaler.com/hc/articles/210172606-Zscaler-is-Expanding-Its-Zscloud-Global-Footprint).</span><span class="sxs-lookup"><span data-stu-id="b60a0-160">Contact [Zscaler ZSCloud Client support team](https://support.zscaler.com/hc/articles/210172606-Zscaler-is-Expanding-Its-Zscloud-Global-Footprint) to get this value.</span></span> 
 
4. <span data-ttu-id="b60a0-161">В разделе **Сертификат для подписи токена SAML** щелкните **Certificate (Base64)** (Сертификат (Base64)), а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="b60a0-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_certificate.png) 

5. <span data-ttu-id="b60a0-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="b60a0-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b60a0-165">В разделе **Конфигурация Zscaler ZSCloud** щелкните **настроить Zscaler ZSCloud**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="b60a0-165">On the **Zscaler ZSCloud Configuration** section, click **Configure Zscaler ZSCloud** to open **Configure sign-on** window.</span></span> <span data-ttu-id="b60a0-166">Скопируйте **URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="b60a0-166">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_configure.png) 

7. <span data-ttu-id="b60a0-168">В другом окне браузера войдите на свой корпоративный сайт Zscaler ZSCloud в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="b60a0-168">In a different web browser window, log in to your ZScaler ZSCloud company site as an administrator.</span></span>

8. <span data-ttu-id="b60a0-169">В верхнем меню щелкните **Администрирование**.</span><span class="sxs-lookup"><span data-stu-id="b60a0-169">In the menu on the top, click **Administration**.</span></span>
   
    <span data-ttu-id="b60a0-170">![Администрирование](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800206.png "Администрирование")</span><span class="sxs-lookup"><span data-stu-id="b60a0-170">![Administration](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800206.png "Administration")</span></span>

9. <span data-ttu-id="b60a0-171">В разделе **Manage Administrators & Roles** (Управление администраторами и ролями) щелкните **Manage Users & Authentication** (Управление пользователями и проверкой подлинности).</span><span class="sxs-lookup"><span data-stu-id="b60a0-171">Under **Manage Administrators & Roles**, click **Manage Users & Authentication**.</span></span>   
            
    <span data-ttu-id="b60a0-172">![Управление пользователями и проверкой подлинности](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800207.png "Управление пользователями и проверкой подлинности")</span><span class="sxs-lookup"><span data-stu-id="b60a0-172">![Manage Users & Authentication](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800207.png "Manage Users & Authentication")</span></span>

10. <span data-ttu-id="b60a0-173">В разделе **Выбор параметров проверки подлинности для организации** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="b60a0-173">In the **Choose Authentication Options for your Organization** section, perform the following steps:</span></span>   
                
    <span data-ttu-id="b60a0-174">![Аутентификация](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800208.png "Аутентификация")</span><span class="sxs-lookup"><span data-stu-id="b60a0-174">![Authentication](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800208.png "Authentication")</span></span>
   
    <span data-ttu-id="b60a0-175">а.</span><span class="sxs-lookup"><span data-stu-id="b60a0-175">a.</span></span> <span data-ttu-id="b60a0-176">Выберите параметр **Проверка подлинности с помощью единого входа SAML**.</span><span class="sxs-lookup"><span data-stu-id="b60a0-176">Select **Authenticate using SAML Single Sign-On**.</span></span>

    <span data-ttu-id="b60a0-177">b.</span><span class="sxs-lookup"><span data-stu-id="b60a0-177">b.</span></span> <span data-ttu-id="b60a0-178">Щелкните **Настроить параметры единого входа SAML**.</span><span class="sxs-lookup"><span data-stu-id="b60a0-178">Click **Configure SAML Single Sign-On Parameters**.</span></span>

11. <span data-ttu-id="b60a0-179">На странице диалогового окна **Configure SAML Single Sign-On Parameters** (Настройка параметров единого входа в SAML) выполните указанные ниже действия и нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="b60a0-179">On the **Configure SAML Single Sign-On Parameters** dialog page, perform the following steps, and then click **Done**</span></span>

    <span data-ttu-id="b60a0-180">![Единый вход](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800209.png "Единый вход")</span><span class="sxs-lookup"><span data-stu-id="b60a0-180">![Single Sign-On](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800209.png "Single Sign-On")</span></span>
    
    <span data-ttu-id="b60a0-181">а.</span><span class="sxs-lookup"><span data-stu-id="b60a0-181">a.</span></span> <span data-ttu-id="b60a0-182">Вставьте значение **SAML Single Sign-On Service URL** (URL-адрес службы единого входа SAML) в текстовое поле **URL of the SAML Portal to which users are sent for authentication** (URL-адрес портала SAML, куда пользователи направляются для проверки подлинности).</span><span class="sxs-lookup"><span data-stu-id="b60a0-182">Paste the **SAML Single Sign-On Service URL** value into the **URL of the SAML Portal to which users are sent for authentication** textbox.</span></span>
    
    <span data-ttu-id="b60a0-183">b.</span><span class="sxs-lookup"><span data-stu-id="b60a0-183">b.</span></span> <span data-ttu-id="b60a0-184">В текстовом поле **Attribute containing Login Name** (Атрибут, содержащий имя входа) введите **NameID**.</span><span class="sxs-lookup"><span data-stu-id="b60a0-184">In the **Attribute containing Login Name** textbox, type **NameID**.</span></span>
    
    <span data-ttu-id="b60a0-185">c.</span><span class="sxs-lookup"><span data-stu-id="b60a0-185">c.</span></span> <span data-ttu-id="b60a0-186">Чтобы передать скачанный сертификат, щелкните **Zscaler pem**.</span><span class="sxs-lookup"><span data-stu-id="b60a0-186">To upload your downloaded certificate, click **Zscaler pem**.</span></span>
    
    <span data-ttu-id="b60a0-187">г)</span><span class="sxs-lookup"><span data-stu-id="b60a0-187">d.</span></span> <span data-ttu-id="b60a0-188">Выберите параметр **Включить автоматическую подготовку SAML**.</span><span class="sxs-lookup"><span data-stu-id="b60a0-188">Select **Enable SAML Auto-Provisioning**.</span></span>

12. <span data-ttu-id="b60a0-189">На странице **Настройка проверки подлинности пользователей** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="b60a0-189">On the **Configure User Authentication** dialog page, perform the following steps:</span></span>

    <span data-ttu-id="b60a0-190">![Администрирование](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800210.png "Администрирование")</span><span class="sxs-lookup"><span data-stu-id="b60a0-190">![Administration](./media/active-directory-saas-zscaler-zscloud-tutorial/ic800210.png "Administration")</span></span>
    
    <span data-ttu-id="b60a0-191">а.</span><span class="sxs-lookup"><span data-stu-id="b60a0-191">a.</span></span> <span data-ttu-id="b60a0-192">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="b60a0-192">Click **Save**.</span></span>

    <span data-ttu-id="b60a0-193">b.</span><span class="sxs-lookup"><span data-stu-id="b60a0-193">b.</span></span> <span data-ttu-id="b60a0-194">Щелкните **Активировать сейчас**.</span><span class="sxs-lookup"><span data-stu-id="b60a0-194">Click **Activate Now**.</span></span>

## <a name="configuring-proxy-settings"></a><span data-ttu-id="b60a0-195">Настройка параметров прокси-сервера</span><span class="sxs-lookup"><span data-stu-id="b60a0-195">Configuring proxy settings</span></span>
### <a name="to-configure-the-proxy-settings-in-internet-explorer"></a><span data-ttu-id="b60a0-196">Настройка параметров прокси-сервера в Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="b60a0-196">To configure the proxy settings in Internet Explorer</span></span>

1. <span data-ttu-id="b60a0-197">Запустите **Internet Explorer**.</span><span class="sxs-lookup"><span data-stu-id="b60a0-197">Start **Internet Explorer**.</span></span>

2. <span data-ttu-id="b60a0-198">В меню **Сервис** выберите **Свойства браузера**, чтобы открыть диалоговое окно **Свойства браузера**.</span><span class="sxs-lookup"><span data-stu-id="b60a0-198">Select **Internet options** from the **Tools** menu for open the **Internet Options** dialog.</span></span>   
    
     <span data-ttu-id="b60a0-199">![Свойства браузера](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769492.png "Свойства браузера")</span><span class="sxs-lookup"><span data-stu-id="b60a0-199">![Internet Options](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769492.png "Internet Options")</span></span>

3. <span data-ttu-id="b60a0-200">Щелкните вкладку **Подключения** .</span><span class="sxs-lookup"><span data-stu-id="b60a0-200">Click the **Connections** tab.</span></span>   
  
     <span data-ttu-id="b60a0-201">![Подключения](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769493.png "Подключения")</span><span class="sxs-lookup"><span data-stu-id="b60a0-201">![Connections](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769493.png "Connections")</span></span>

4. <span data-ttu-id="b60a0-202">Нажмите кнопку **Настройка сети**, чтобы открыть диалоговое окно **Настройка сети**.</span><span class="sxs-lookup"><span data-stu-id="b60a0-202">Click **LAN settings** to open the **LAN Settings** dialog.</span></span>

5. <span data-ttu-id="b60a0-203">В разделе "Прокси-сервер" выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="b60a0-203">In the Proxy server section, perform the following steps:</span></span>   
   
    <span data-ttu-id="b60a0-204">![Прокси-сервер](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769494.png "Прокси-сервер")</span><span class="sxs-lookup"><span data-stu-id="b60a0-204">![Proxy server](./media/active-directory-saas-zscaler-zscloud-tutorial/ic769494.png "Proxy server")</span></span>

    <span data-ttu-id="b60a0-205">а.</span><span class="sxs-lookup"><span data-stu-id="b60a0-205">a.</span></span> <span data-ttu-id="b60a0-206">Установите флажок **Использовать прокси-сервер для локальной сети**.</span><span class="sxs-lookup"><span data-stu-id="b60a0-206">Select **Use a proxy server for your LAN**.</span></span>

    <span data-ttu-id="b60a0-207">b.</span><span class="sxs-lookup"><span data-stu-id="b60a0-207">b.</span></span> <span data-ttu-id="b60a0-208">В текстовом поле "Адрес" введите **gateway.zscalerone.net**.</span><span class="sxs-lookup"><span data-stu-id="b60a0-208">In the Address textbox, type **gateway.zscalerone.net**.</span></span>

    <span data-ttu-id="b60a0-209">c.</span><span class="sxs-lookup"><span data-stu-id="b60a0-209">c.</span></span> <span data-ttu-id="b60a0-210">В текстовом поле "Порт" введите **80**.</span><span class="sxs-lookup"><span data-stu-id="b60a0-210">In the Port textbox, type **80**.</span></span>

    <span data-ttu-id="b60a0-211">г)</span><span class="sxs-lookup"><span data-stu-id="b60a0-211">d.</span></span> <span data-ttu-id="b60a0-212">Установите флаг **Не использовать прокси-сервер для локальных адресов**.</span><span class="sxs-lookup"><span data-stu-id="b60a0-212">Select **Bypass proxy server for local addresses**.</span></span>

    <span data-ttu-id="b60a0-213">д.</span><span class="sxs-lookup"><span data-stu-id="b60a0-213">e.</span></span> <span data-ttu-id="b60a0-214">Нажмите кнопку **ОК**, чтобы закрыть диалоговое окно **Настройка параметров локальной сети**.</span><span class="sxs-lookup"><span data-stu-id="b60a0-214">Click **OK** to close the **Local Area Network (LAN) Settings** dialog.</span></span>

6. <span data-ttu-id="b60a0-215">Нажмите кнопку **ОК**, чтобы закрыть диалоговое окно **Свойства браузера**.</span><span class="sxs-lookup"><span data-stu-id="b60a0-215">Click **OK** to close the **Internet Options** dialog.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b60a0-216">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="b60a0-216">Creating an Azure AD test user</span></span>
<span data-ttu-id="b60a0-217">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b60a0-217">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="b60a0-219">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="b60a0-219">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b60a0-220">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b60a0-220">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b60a0-222">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="b60a0-222">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b60a0-224">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="b60a0-224">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b60a0-226">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="b60a0-226">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-zscaler-zscloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b60a0-228">а.</span><span class="sxs-lookup"><span data-stu-id="b60a0-228">a.</span></span> <span data-ttu-id="b60a0-229">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b60a0-229">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b60a0-230">b.</span><span class="sxs-lookup"><span data-stu-id="b60a0-230">b.</span></span> <span data-ttu-id="b60a0-231">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b60a0-231">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b60a0-232">c.</span><span class="sxs-lookup"><span data-stu-id="b60a0-232">c.</span></span> <span data-ttu-id="b60a0-233">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="b60a0-233">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b60a0-234">d.</span><span class="sxs-lookup"><span data-stu-id="b60a0-234">d.</span></span> <span data-ttu-id="b60a0-235">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="b60a0-235">Click **Create**.</span></span>

### <a name="creating-a-zscaler-zscloud-test-user"></a><span data-ttu-id="b60a0-236">Создание тестового пользователя Zscaler ZSCloud</span><span class="sxs-lookup"><span data-stu-id="b60a0-236">Creating a Zscaler ZSCloud test user</span></span>

<span data-ttu-id="b60a0-237">Чтобы пользователи Azure AD могли входить в ZScaler ZSCloud, их нужно подготовить для ZScaler ZSCloud.</span><span class="sxs-lookup"><span data-stu-id="b60a0-237">To enable Azure AD users to log in to ZScaler ZSCloud, they must be provisioned to ZScaler ZSCloud.</span></span>  
<span data-ttu-id="b60a0-238">В случае с ZScaler ZSCloud подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="b60a0-238">In the case of ZScaler ZSCloud, provisioning is a manual task.</span></span>

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a><span data-ttu-id="b60a0-239">Чтобы настроить подготовку учетных записей пользователей, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="b60a0-239">To configure user provisioning, perform the following steps:</span></span>

1. <span data-ttu-id="b60a0-240">Войдите в клиент **ZScaler** .</span><span class="sxs-lookup"><span data-stu-id="b60a0-240">Log in to your **Zscaler** tenant.</span></span>

2. <span data-ttu-id="b60a0-241">Щелкните **Администрирование**.</span><span class="sxs-lookup"><span data-stu-id="b60a0-241">Click **Administration**.</span></span>   
   
    <span data-ttu-id="b60a0-242">![Администрирование](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781035.png "Администрирование")</span><span class="sxs-lookup"><span data-stu-id="b60a0-242">![Administration](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781035.png "Administration")</span></span>

3. <span data-ttu-id="b60a0-243">Щелкните **Управление пользователями**.</span><span class="sxs-lookup"><span data-stu-id="b60a0-243">Click **User Management**.</span></span>   
        
     <span data-ttu-id="b60a0-244">![Добавление](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781037.png "Добавление")</span><span class="sxs-lookup"><span data-stu-id="b60a0-244">![Add](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781037.png "Add")</span></span>

4. <span data-ttu-id="b60a0-245">На вкладке **Users** (Пользователи) нажмите кнопку **Add** (Добавить).</span><span class="sxs-lookup"><span data-stu-id="b60a0-245">In the **Users** tab, click **Add**.</span></span>
      
    <span data-ttu-id="b60a0-246">![Добавление](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781037.png "Добавление")</span><span class="sxs-lookup"><span data-stu-id="b60a0-246">![Add](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781037.png "Add")</span></span>

5. <span data-ttu-id="b60a0-247">В разделе "Добавить пользователя" выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="b60a0-247">In the Add User section, perform the following steps:</span></span>
        
    <span data-ttu-id="b60a0-248">![Добавление пользователя](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781038.png "Добавление пользователя")</span><span class="sxs-lookup"><span data-stu-id="b60a0-248">![Add User](./media/active-directory-saas-zscaler-zscloud-tutorial/ic781038.png "Add User")</span></span>
   
    <span data-ttu-id="b60a0-249">а.</span><span class="sxs-lookup"><span data-stu-id="b60a0-249">a.</span></span> <span data-ttu-id="b60a0-250">Заполните текстовые поля **UserID** (Идентификатор пользователя), **User Display Name** (Отображаемое имя пользователя), **Password** (Пароль), **Confirm Password** (Подтверждение пароля) и выберите **Groups** (Группы) и **Department** (Отдел) действующей учетной записи AAD, которую необходимо подготовить.</span><span class="sxs-lookup"><span data-stu-id="b60a0-250">Type the **UserID**, **User Display Name**, **Password**, **Confirm Password**, and then select **Groups** and the **Department** of a valid AAD account you want to provision.</span></span>

    <span data-ttu-id="b60a0-251">b.</span><span class="sxs-lookup"><span data-stu-id="b60a0-251">b.</span></span> <span data-ttu-id="b60a0-252">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="b60a0-252">Click **Save**.</span></span>

> [!NOTE]
> <span data-ttu-id="b60a0-253">Вы можете использовать любые другие средства создания учетной записи пользователя ZScaler ZSCloud или API, предоставляемые ZScaler ZSCloud для подготовки учетных записей пользователя AAD.</span><span class="sxs-lookup"><span data-stu-id="b60a0-253">You can use any other ZScaler ZSCloud user account creation tools or APIs provided by ZScaler ZSCloud to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b60a0-254">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="b60a0-254">Assigning the Azure AD test user</span></span>

<span data-ttu-id="b60a0-255">Этот раздел описывает, как позволить пользователю Britta Simon использовать единый вход Azure путем предоставления доступа к Zscaler ZSCloud.</span><span class="sxs-lookup"><span data-stu-id="b60a0-255">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Zscaler ZSCloud.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="b60a0-257">**Чтобы назначить пользователя Britta Simon приложению Zscaler ZSCloud, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="b60a0-257">**To assign Britta Simon to Zscaler ZSCloud, perform the following steps:**</span></span>

1. <span data-ttu-id="b60a0-258">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="b60a0-258">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="b60a0-260">В списке приложений выберите **Zscaler ZSCloud**.</span><span class="sxs-lookup"><span data-stu-id="b60a0-260">In the applications list, select **Zscaler ZSCloud**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_zscalerzscloud_app.png) 

3. <span data-ttu-id="b60a0-262">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="b60a0-262">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="b60a0-264">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="b60a0-264">Click **Add** button.</span></span> <span data-ttu-id="b60a0-265">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="b60a0-265">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="b60a0-267">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="b60a0-267">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b60a0-268">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="b60a0-268">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b60a0-269">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="b60a0-269">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b60a0-270">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="b60a0-270">Testing single sign-on</span></span>

<span data-ttu-id="b60a0-271">Если вы хотите проверить параметры единого входа, откройте панель доступа.</span><span class="sxs-lookup"><span data-stu-id="b60a0-271">If you want to test your single sign-on settings, open the Access Panel.</span></span>

<span data-ttu-id="b60a0-272">Щелкнув плитку "Zscaler ZSCloud" на панели доступа, вы автоматически войдете в приложение Zscaler ZSCloud.</span><span class="sxs-lookup"><span data-stu-id="b60a0-272">When you click the Zscaler ZSCloud tile in the Access Panel, you should get automatically signed-on to your Zscaler ZSCloud application.</span></span>

<span data-ttu-id="b60a0-273">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="b60a0-273">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="b60a0-274">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="b60a0-274">Additional resources</span></span>

* [<span data-ttu-id="b60a0-275">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b60a0-275">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b60a0-276">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b60a0-276">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscaler-zscloud-tutorial/tutorial_general_203.png

