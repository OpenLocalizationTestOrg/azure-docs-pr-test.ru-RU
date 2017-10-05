---
title: "Руководство по интеграции Azure Active Directory с SugarCRM | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в приложении SugarCRM."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 3331b9fc-ebc0-4a3a-9f7b-bf20ee35d180
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: jeedes
ms.openlocfilehash: c27aef24e859522b8001ecb747906abdca14d87a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sugar-crm"></a><span data-ttu-id="b0ec8-103">Руководство по интеграции Azure Active Directory с SugarCRM</span><span class="sxs-lookup"><span data-stu-id="b0ec8-103">Tutorial: Azure Active Directory integration with Sugar CRM</span></span>

<span data-ttu-id="b0ec8-104">В этом руководстве описано, как интегрировать SugarCRM с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b0ec8-104">In this tutorial, you learn how to integrate Sugar CRM with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b0ec8-105">Интеграция Azure AD с приложением SugarCRM обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-105">Integrating Sugar CRM with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="b0ec8-106">С помощью Azure AD вы можете контролировать доступ к SugarCRM.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-106">You can control in Azure AD who has access to Sugar CRM</span></span>
- <span data-ttu-id="b0ec8-107">Вы можете включить автоматический вход пользователей в SugarCRM (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-107">You can enable your users to automatically get signed-on to Sugar CRM (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b0ec8-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="b0ec8-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b0ec8-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b0ec8-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="b0ec8-110">Prerequisites</span></span>

<span data-ttu-id="b0ec8-111">Чтобы настроить интеграцию Azure AD с приложением SugarCRM, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="b0ec8-111">To configure Azure AD integration with Sugar CRM, you need the following items:</span></span>

- <span data-ttu-id="b0ec8-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="b0ec8-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b0ec8-113">Подписка SugarCRM с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-113">A Sugar CRM single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b0ec8-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b0ec8-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="b0ec8-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b0ec8-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b0ec8-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b0ec8-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b0ec8-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="b0ec8-118">Scenario description</span></span>
<span data-ttu-id="b0ec8-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b0ec8-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="b0ec8-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b0ec8-121">Добавление SugarCRM из коллекции</span><span class="sxs-lookup"><span data-stu-id="b0ec8-121">Adding Sugar CRM from the gallery</span></span>
2. <span data-ttu-id="b0ec8-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b0ec8-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sugar-crm-from-the-gallery"></a><span data-ttu-id="b0ec8-123">Добавление SugarCRM из коллекции</span><span class="sxs-lookup"><span data-stu-id="b0ec8-123">Adding Sugar CRM from the gallery</span></span>
<span data-ttu-id="b0ec8-124">Чтобы настроить интеграцию SugarCRM с Azure AD, необходимо добавить SugarCRM из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-124">To configure the integration of Sugar CRM into Azure AD, you need to add Sugar CRM from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="b0ec8-125">**Чтобы добавить SugarCRM из коллекции, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="b0ec8-125">**To add Sugar CRM from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="b0ec8-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="b0ec8-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="b0ec8-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="b0ec8-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="b0ec8-133">В поле поиска введите **SugarCRM**.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-133">In the search box, type **Sugar CRM**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_search.png)

5. <span data-ttu-id="b0ec8-135">На панели результатов выберите **SugarCRM** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-135">In the results panel, select **Sugar CRM**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="b0ec8-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b0ec8-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="b0ec8-138">В этом разделе описана настройка и проверка единого входа Azure AD в SugarCRM с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-138">In this section, you configure and test Azure AD single sign-on with Sugar CRM based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b0ec8-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в SugarCRM соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Sugar CRM is to a user in Azure AD.</span></span> <span data-ttu-id="b0ec8-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в SugarCRM.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-140">In other words, a link relationship between an Azure AD user and the related user in Sugar CRM needs to be established.</span></span>

<span data-ttu-id="b0ec8-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в SugarCRM.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-141">In Sugar CRM, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="b0ec8-142">Чтобы настроить и проверить единый вход Azure AD в SugarCRM, выполните действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-142">To configure and test Azure AD single sign-on with Sugar CRM, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="b0ec8-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="b0ec8-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b0ec8-145">**[Создание тестового пользователя SugarCRM](#creating-a-sugar-crm-test-user)** требуется для того, чтобы в Sugar CRM существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-145">**[Creating a Sugar CRM test user](#creating-a-sugar-crm-test-user)** - to have a counterpart of Britta Simon in Sugar CRM that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="b0ec8-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b0ec8-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="b0ec8-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="b0ec8-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="b0ec8-149">В этом разделе мы включим на портале Azure единый вход Azure AD и настроим его в приложении SugarCRM.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Sugar CRM application.</span></span>

<span data-ttu-id="b0ec8-150">**Чтобы настроить единый вход Azure AD в SugarCRM, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="b0ec8-150">**To configure Azure AD single sign-on with Sugar CRM, perform the following steps:**</span></span>

1. <span data-ttu-id="b0ec8-151">На портале Azure на странице интеграции с приложением **SugarCRM** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-151">In the Azure portal, on the **Sugar CRM** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="b0ec8-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_samlbase.png)

3. <span data-ttu-id="b0ec8-155">В разделе **Домены и URL-адреса приложения SugarCRM** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="b0ec8-155">On the **Sugar CRM Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_url.png)

    <span data-ttu-id="b0ec8-157">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="b0ec8-157">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.sugarondemand.com` |
    | `https://<companyname>.trial.sugarcrm` |

    > [!NOTE] 
    > <span data-ttu-id="b0ec8-158">Это значение приведено для примера.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-158">The value is not real.</span></span> <span data-ttu-id="b0ec8-159">Вместо него необходимо указать фактический URL-адрес входа.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-159">Update the value with the actual Sign-On URL.</span></span> <span data-ttu-id="b0ec8-160">Чтобы получить это значение, обратитесь в [службу поддержки клиентов SugarCRM](https://support.sugarcrm.com/).</span><span class="sxs-lookup"><span data-stu-id="b0ec8-160">Contact [Sugar CRM Client support team](https://support.sugarcrm.com/) to get the value.</span></span> 
 
4. <span data-ttu-id="b0ec8-161">В разделе **Сертификат для подписи токена SAML** щелкните **Certificate (Base64)** (Сертификат (Base64)), а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-161">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_certificate.png) 

5. <span data-ttu-id="b0ec8-163">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="b0ec8-163">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b0ec8-165">В разделе **Конфигурация SugarCRM** щелкните **Настроить SugarCRM**, чтобы открыть окно **Настройка входа**.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-165">On the **Sugar CRM Configuration** section, click **Configure Sugar CRM** to open **Configure sign-on** window.</span></span> <span data-ttu-id="b0ec8-166">Скопируйте **URL-адрес выхода и URL-адрес службы единого входа SAML** из раздела **Quick Reference** (Краткий справочник).</span><span class="sxs-lookup"><span data-stu-id="b0ec8-166">Copy the **Sign-Out URL, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_configure.png) 

7. <span data-ttu-id="b0ec8-168">В другом окне веб-браузера войдите на корпоративный сайт SugarCRM с учетными данными администратора.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-168">In a different web browser window, log in to your Sugar CRM company site as an administrator.</span></span>

8. <span data-ttu-id="b0ec8-169">Откройте страницу **Администратор**.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-169">Go to **Admin**.</span></span>
   
    <span data-ttu-id="b0ec8-170">![Администратор](./media/active-directory-saas-sugarcrm-tutorial/ic795888.png "Администратор")</span><span class="sxs-lookup"><span data-stu-id="b0ec8-170">![Admin](./media/active-directory-saas-sugarcrm-tutorial/ic795888.png "Admin")</span></span>

9. <span data-ttu-id="b0ec8-171">В разделе **Administration** (Администрирование) щелкните **Password Management** (Управление паролями).</span><span class="sxs-lookup"><span data-stu-id="b0ec8-171">In the **Administration** section, click **Password Management**.</span></span>
   
    <span data-ttu-id="b0ec8-172">![Администрирование](./media/active-directory-saas-sugarcrm-tutorial/ic795889.png "Администрирование")</span><span class="sxs-lookup"><span data-stu-id="b0ec8-172">![Administration](./media/active-directory-saas-sugarcrm-tutorial/ic795889.png "Administration")</span></span>

10. <span data-ttu-id="b0ec8-173">Установите флажок **Включить проверку подлинности SAML**.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-173">Select **Enable SAML Authentication**.</span></span>
   
    <span data-ttu-id="b0ec8-174">![Администрирование](./media/active-directory-saas-sugarcrm-tutorial/ic795890.png "Администрирование")</span><span class="sxs-lookup"><span data-stu-id="b0ec8-174">![Administration](./media/active-directory-saas-sugarcrm-tutorial/ic795890.png "Administration")</span></span>

11. <span data-ttu-id="b0ec8-175">В разделе **Проверка подлинности SAML** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="b0ec8-175">In the **SAML Authentication** section, perform the following steps:</span></span>
   
    <span data-ttu-id="b0ec8-176">![Аутентификация SAML](./media/active-directory-saas-sugarcrm-tutorial/ic795891.png "Аутентификация SAML")</span><span class="sxs-lookup"><span data-stu-id="b0ec8-176">![SAML Authentication](./media/active-directory-saas-sugarcrm-tutorial/ic795891.png "SAML Authentication")</span></span>  
 
    <span data-ttu-id="b0ec8-177">а.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-177">a.</span></span> <span data-ttu-id="b0ec8-178">В текстовое поле **Login URL** (URL-адрес входа) вставьте значение **SAML Single Sign-On Service URL** (URL-адрес службы единого входа SAML), скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-178">In the **Login URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="b0ec8-179">b.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-179">b.</span></span> <span data-ttu-id="b0ec8-180">В текстовое поле **SLO URL** (URL-адрес выхода) вставьте значение **URL-адрес выхода**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-180">In the **SLO URL** textbox, paste the value of **Sign-Out URL**, which you have copied from Azure portal.</span></span>
  
    <span data-ttu-id="b0ec8-181">c.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-181">c.</span></span> <span data-ttu-id="b0ec8-182">Откройте сертификат в кодировке Base-64 в Блокноте, скопируйте его содержимое в буфер обмена и вставьте весь сертификат в текстовое поле **Сертификат X.509** .</span><span class="sxs-lookup"><span data-stu-id="b0ec8-182">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste the entire Certificate into **X.509 Certificate** textbox.</span></span>
  
    <span data-ttu-id="b0ec8-183">d.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-183">d.</span></span> <span data-ttu-id="b0ec8-184">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-184">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="b0ec8-185">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-185">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="b0ec8-186">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-186">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="b0ec8-187">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="b0ec8-187">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="b0ec8-188">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="b0ec8-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="b0ec8-189">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-189">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="b0ec8-191">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="b0ec8-191">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="b0ec8-192">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-192">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b0ec8-194">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-194">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b0ec8-196">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-196">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b0ec8-198">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-198">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sugarcrm-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b0ec8-200">а.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-200">a.</span></span> <span data-ttu-id="b0ec8-201">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-201">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b0ec8-202">b.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-202">b.</span></span> <span data-ttu-id="b0ec8-203">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-203">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b0ec8-204">c.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-204">c.</span></span> <span data-ttu-id="b0ec8-205">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-205">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="b0ec8-206">d.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-206">d.</span></span> <span data-ttu-id="b0ec8-207">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-207">Click **Create**.</span></span>
 
### <a name="creating-a-sugar-crm-test-user"></a><span data-ttu-id="b0ec8-208">Создание тестового пользователя SugarCRM</span><span class="sxs-lookup"><span data-stu-id="b0ec8-208">Creating a Sugar CRM test user</span></span>

<span data-ttu-id="b0ec8-209">Чтобы пользователи Azure AD могли входить в SugarCRM, их необходимо подготовить для SugarCRM.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-209">In order to enable Azure AD users to log in to Sugar CRM, they must be provisioned to Sugar CRM.</span></span>

<span data-ttu-id="b0ec8-210">В случае SugarCRM подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-210">In the case of Sugar CRM, provisioning is a manual task.</span></span>

<span data-ttu-id="b0ec8-211">**Чтобы подготовить учетную запись пользователя, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="b0ec8-211">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="b0ec8-212">Войдите на веб-сайт **SugarCRM** компании в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-212">Log in to your **Sugar CRM** company site as administrator.</span></span>

2. <span data-ttu-id="b0ec8-213">Перейдите на страницу **Admin**(Администратор).</span><span class="sxs-lookup"><span data-stu-id="b0ec8-213">Go to **Admin**.</span></span>
   
    <span data-ttu-id="b0ec8-214">![Администратор](./media/active-directory-saas-sugarcrm-tutorial/ic795888.png "Администратор")</span><span class="sxs-lookup"><span data-stu-id="b0ec8-214">![Admin](./media/active-directory-saas-sugarcrm-tutorial/ic795888.png "Admin")</span></span>

3. <span data-ttu-id="b0ec8-215">В разделе **Administration** (Администрирование) щелкните **User Management** (Управление пользователями).</span><span class="sxs-lookup"><span data-stu-id="b0ec8-215">In the **Administration** section, click **User Management**.</span></span>
   
    <span data-ttu-id="b0ec8-216">![Администрирование](./media/active-directory-saas-sugarcrm-tutorial/ic795893.png "Администрирование")</span><span class="sxs-lookup"><span data-stu-id="b0ec8-216">![Administration](./media/active-directory-saas-sugarcrm-tutorial/ic795893.png "Administration")</span></span>

4. <span data-ttu-id="b0ec8-217">Выберите **Users (Пользователи) \> Create New User (Создать нового пользователя)**.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-217">Go to **Users \> Create New User**.</span></span>
   
    <span data-ttu-id="b0ec8-218">![Создание пользователя](./media/active-directory-saas-sugarcrm-tutorial/ic795894.png "Создание пользователя")</span><span class="sxs-lookup"><span data-stu-id="b0ec8-218">![Create New User](./media/active-directory-saas-sugarcrm-tutorial/ic795894.png "Create New User")</span></span>

5. <span data-ttu-id="b0ec8-219">На вкладке **Профиль пользователя** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="b0ec8-219">On the **User Profile** tab, perform the following steps:</span></span>
   
    <span data-ttu-id="b0ec8-220">![Новый пользователь](./media/active-directory-saas-sugarcrm-tutorial/ic795895.png "Новый пользователь")</span><span class="sxs-lookup"><span data-stu-id="b0ec8-220">![New User](./media/active-directory-saas-sugarcrm-tutorial/ic795895.png "New User")</span></span>

    <span data-ttu-id="b0ec8-221">а.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-221">a.</span></span> <span data-ttu-id="b0ec8-222">В соответствующие текстовые поля введите **имя**, **фамилию** и **электронный адрес** действующей учетной записи Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-222">Type the **user name**, **last name**, and **email address** of a valid Azure Active Directory user into the related textboxes.</span></span>
  
6. <span data-ttu-id="b0ec8-223">Для параметра **Status** (Состояние) выберите значение **Active** (Активно).</span><span class="sxs-lookup"><span data-stu-id="b0ec8-223">As **Status**, select **Active**.</span></span>

7. <span data-ttu-id="b0ec8-224">На вкладке «Пароль» выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="b0ec8-224">On the Password tab, perform the following steps:</span></span>
   
    <span data-ttu-id="b0ec8-225">![Новый пользователь](./media/active-directory-saas-sugarcrm-tutorial/ic795896.png "Новый пользователь")</span><span class="sxs-lookup"><span data-stu-id="b0ec8-225">![New User](./media/active-directory-saas-sugarcrm-tutorial/ic795896.png "New User")</span></span>

    <span data-ttu-id="b0ec8-226">а.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-226">a.</span></span> <span data-ttu-id="b0ec8-227">Введите пароль в соответствующее текстовое поле.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-227">Type the password into the related textbox.</span></span>

    <span data-ttu-id="b0ec8-228">b.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-228">b.</span></span> <span data-ttu-id="b0ec8-229">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-229">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="b0ec8-230">Вы можете использовать любые другие инструменты создания учетных записей пользователей SugarCRM или API, предоставляемые SugarCRM для подготовки учетных записей пользователей AAD.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-230">You can use any other Sugar CRM user account creation tools or APIs provided by Sugar CRM to provision AAD user accounts.</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="b0ec8-231">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="b0ec8-231">Assigning the Azure AD test user</span></span>

<span data-ttu-id="b0ec8-232">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив доступ к SugarCRM.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-232">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Sugar CRM.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="b0ec8-234">**Чтобы назначить пользователя Britta Simon в SugarCRM, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="b0ec8-234">**To assign Britta Simon to Sugar CRM, perform the following steps:**</span></span>

1. <span data-ttu-id="b0ec8-235">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-235">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="b0ec8-237">В списке приложений выберите **SugarCRM**.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-237">In the applications list, select **Sugar CRM**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-sugarcrm-tutorial/tutorial_sugarcrm_app.png) 

3. <span data-ttu-id="b0ec8-239">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-239">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="b0ec8-241">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-241">Click **Add** button.</span></span> <span data-ttu-id="b0ec8-242">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="b0ec8-244">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-244">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="b0ec8-245">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b0ec8-246">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="b0ec8-247">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="b0ec8-247">Testing single sign-on</span></span>

<span data-ttu-id="b0ec8-248">Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-248">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="b0ec8-249">Щелкнув плитку SugarCRM на панели доступа, вы автоматически войдете в приложение SugarCRM.</span><span class="sxs-lookup"><span data-stu-id="b0ec8-249">When you click the Sugar CRM tile in the Access Panel, you should get automatically signed-on to your Sugar CRM application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b0ec8-250">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="b0ec8-250">Additional resources</span></span>

* [<span data-ttu-id="b0ec8-251">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b0ec8-251">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b0ec8-252">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="b0ec8-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sugarcrm-tutorial/tutorial_general_203.png

