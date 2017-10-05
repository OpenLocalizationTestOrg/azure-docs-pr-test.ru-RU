---
title: "Руководство по интеграции Azure Active Directory с SumoLogic | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в SumoLogic."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: fbb76765-92d7-4801-9833-573b11b4d910
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: e739106472ccf930b2942eb810dd844f2b1ade7c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sumologic"></a><span data-ttu-id="5ae8d-103">Руководство. Интеграция Azure Active Directory с SumoLogic</span><span class="sxs-lookup"><span data-stu-id="5ae8d-103">Tutorial: Azure Active Directory integration with SumoLogic</span></span>

<span data-ttu-id="5ae8d-104">В этом руководстве описано, как интегрировать SumoLogic с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5ae8d-104">In this tutorial, you learn how to integrate SumoLogic with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5ae8d-105">Интеграция Azure AD с приложением SumoLogic обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-105">Integrating SumoLogic with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="5ae8d-106">С помощью Azure AD вы можете контролировать доступ к SumoLogic.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-106">You can control in Azure AD who has access to SumoLogic</span></span>
- <span data-ttu-id="5ae8d-107">Вы можете включить автоматический вход пользователей в SumoLogic (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-107">You can enable your users to automatically get signed-on to SumoLogic (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5ae8d-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="5ae8d-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5ae8d-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5ae8d-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="5ae8d-110">Prerequisites</span></span>

<span data-ttu-id="5ae8d-111">Чтобы настроить интеграцию Azure AD с приложением SumoLogic, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="5ae8d-111">To configure Azure AD integration with SumoLogic, you need the following items:</span></span>

- <span data-ttu-id="5ae8d-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="5ae8d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5ae8d-113">подписка с поддержкой единого входа SumoLogic.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-113">A SumoLogic single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5ae8d-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5ae8d-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="5ae8d-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5ae8d-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5ae8d-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5ae8d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5ae8d-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="5ae8d-118">Scenario description</span></span>
<span data-ttu-id="5ae8d-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5ae8d-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="5ae8d-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5ae8d-121">Добавление SumoLogic из коллекции</span><span class="sxs-lookup"><span data-stu-id="5ae8d-121">Adding SumoLogic from the gallery</span></span>
2. <span data-ttu-id="5ae8d-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="5ae8d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sumologic-from-the-gallery"></a><span data-ttu-id="5ae8d-123">Добавление SumoLogic из коллекции</span><span class="sxs-lookup"><span data-stu-id="5ae8d-123">Adding SumoLogic from the gallery</span></span>
<span data-ttu-id="5ae8d-124">Чтобы настроить интеграцию SumoLogic с Azure AD, необходимо добавить SumoLogic из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-124">To configure the integration of SumoLogic into Azure AD, you need to add SumoLogic from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="5ae8d-125">**Чтобы добавить SumoLogic из коллекции, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="5ae8d-125">**To add SumoLogic from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="5ae8d-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5ae8d-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="5ae8d-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="5ae8d-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="5ae8d-133">В поле поиска введите **SumoLogic**.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-133">In the search box, type **SumoLogic**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_search.png)

5. <span data-ttu-id="5ae8d-135">На панели результатов выберите **SumoLogic** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-135">In the results panel, select **SumoLogic**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5ae8d-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="5ae8d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5ae8d-138">В этом разделе описана настройка и проверка единого входа Azure AD в SumoLogic с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-138">In this section, you configure and test Azure AD single sign-on with SumoLogic based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="5ae8d-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в SumoLogic соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-139">For single sign-on to work, Azure AD needs to know what the counterpart user in SumoLogic is to a user in Azure AD.</span></span> <span data-ttu-id="5ae8d-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в SumoLogic.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-140">In other words, a link relationship between an Azure AD user and the related user in SumoLogic needs to be established.</span></span>

<span data-ttu-id="5ae8d-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в SumoLogic.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-141">In SumoLogic, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="5ae8d-142">Чтобы настроить и проверить единый вход Azure AD в SumoLogic, выполните действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="5ae8d-142">To configure and test Azure AD single sign-on with SumoLogic, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="5ae8d-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="5ae8d-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5ae8d-145">**[Создание тестового пользователя SumoLogic](#creating-a-sumologic-test-user)** требуется для того, чтобы в SumoLogic существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-145">**[Creating a SumoLogic test user](#creating-a-sumologic-test-user)** - to have a counterpart of Britta Simon in SumoLogic that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="5ae8d-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5ae8d-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5ae8d-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="5ae8d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5ae8d-149">В этом разделе мы включим на портале Azure единый вход Azure AD и настроим его в приложении SumoLogic.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your SumoLogic application.</span></span>

<span data-ttu-id="5ae8d-150">**Чтобы настроить единый вход Azure AD в SumoLogic, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="5ae8d-150">**To configure Azure AD single sign-on with SumoLogic, perform the following steps:**</span></span>

1. <span data-ttu-id="5ae8d-151">На портале Azure на странице интеграции с приложением **SumoLogic** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-151">In the Azure portal, on the **SumoLogic** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="5ae8d-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_samlbase.png)

3. <span data-ttu-id="5ae8d-155">В разделе **Домены и URL-адреса приложения SumoLogic** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="5ae8d-155">On the **SumoLogic Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_url.png)

    <span data-ttu-id="5ae8d-157">а.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-157">a.</span></span> <span data-ttu-id="5ae8d-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<tenantname>.SumoLogic.com`</span><span class="sxs-lookup"><span data-stu-id="5ae8d-158">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<tenantname>.SumoLogic.com`</span></span>

    <span data-ttu-id="5ae8d-159">b.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-159">b.</span></span> <span data-ttu-id="5ae8d-160">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="5ae8d-160">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<tenantname>.us2.sumologic.com` |
    | `https://<tenantname>.sumologic.com` |
    | `https://<tenantname>.us4.sumologic.com` |
    | `https://<tenantname>.eu.sumologic.com` |
    | `https://<tenantname>.au.sumologic.com` |

    > [!NOTE] 
    > <span data-ttu-id="5ae8d-161">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-161">These values are not real.</span></span> <span data-ttu-id="5ae8d-162">Замените эти значения фактическим URL-адресом для входа и идентификатором.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-162">Update these values with the actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="5ae8d-163">Чтобы получить эти значения, обратитесь в [службу поддержки клиентов SumoLogic](https://www.sumologic.com/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="5ae8d-163">Contact [SumoLogic Client support team](https://www.sumologic.com/contact-us/) to get these values.</span></span> 
 
4. <span data-ttu-id="5ae8d-164">В разделе **Сертификат для подписи токена SAML** щелкните **Certificate (Base64)** (Сертификат (Base64)), а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-164">On the **SAML Signing Certificate** section, click **Certificate (Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_certificate.png) 

5. <span data-ttu-id="5ae8d-166">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="5ae8d-166">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-sumologic-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5ae8d-168">В разделе **Конфигурация SumoLogic** щелкните **Настроить SumoLogic**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-168">On the **SumoLogic Configuration** section, click **Configure SumoLogic** to open **Configure sign-on** window.</span></span> <span data-ttu-id="5ae8d-169">Скопируйте **идентификатор сущности SAML и URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-169">Copy the **SAML Entity ID, and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_configure.png) 

7. <span data-ttu-id="5ae8d-171">В другом окне веб-браузера войдите на корпоративный веб-сайт SumoLogic в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-171">In a different web browser window, log in to your SumoLogic company site as an administrator.</span></span>

8. <span data-ttu-id="5ae8d-172">Выберите **Manage (Управление) \> Security (Безопасность)**.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-172">Go to **Manage \> Security**.</span></span>
   
    <span data-ttu-id="5ae8d-173">![Управление](./media/active-directory-saas-sumologic-tutorial/ic778556.png "Управление")</span><span class="sxs-lookup"><span data-stu-id="5ae8d-173">![Manage](./media/active-directory-saas-sumologic-tutorial/ic778556.png "Manage")</span></span>

9. <span data-ttu-id="5ae8d-174">Нажмите кнопку **SAML**.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-174">Click **SAML**.</span></span>
   
    <span data-ttu-id="5ae8d-175">![Глобальные параметры безопасности](./media/active-directory-saas-sumologic-tutorial/ic778557.png "Глобальные параметры безопасности")</span><span class="sxs-lookup"><span data-stu-id="5ae8d-175">![Global security settings](./media/active-directory-saas-sumologic-tutorial/ic778557.png "Global security settings")</span></span>

10. <span data-ttu-id="5ae8d-176">В списке **Select a configuration or create a new one** (Выберите настройку или создайте новую) выберите **Azure AD**, а затем щелкните **Configure** (Настройка).</span><span class="sxs-lookup"><span data-stu-id="5ae8d-176">From the **Select a configuration or create a new one** list, select **Azure AD**, and then click **Configure**.</span></span>
   
    <span data-ttu-id="5ae8d-177">![Настройка SAML 2.0](./media/active-directory-saas-sumologic-tutorial/ic778558.png "Настройка SAML 2.0")</span><span class="sxs-lookup"><span data-stu-id="5ae8d-177">![Configure SAML 2.0](./media/active-directory-saas-sumologic-tutorial/ic778558.png "Configure SAML 2.0")</span></span>

11. <span data-ttu-id="5ae8d-178">В диалоговом окне **Настройка SAML 2.0** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="5ae8d-178">On the **Configure SAML 2.0** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="5ae8d-179">![Настройка SAML 2.0](./media/active-directory-saas-sumologic-tutorial/ic778559.png "Настройка SAML 2.0")</span><span class="sxs-lookup"><span data-stu-id="5ae8d-179">![Configure SAML 2.0](./media/active-directory-saas-sumologic-tutorial/ic778559.png "Configure SAML 2.0")</span></span>
   
    <span data-ttu-id="5ae8d-180">а.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-180">a.</span></span> <span data-ttu-id="5ae8d-181">В текстовом поле **Configuration Name** (Имя конфигурации) введите **Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-181">In the **Configuration Name** textbox, type **Azure AD**.</span></span> 

    <span data-ttu-id="5ae8d-182">b.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-182">b.</span></span> <span data-ttu-id="5ae8d-183">Выберите **Режим отладки**.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-183">Select **Debug Mode**.</span></span>

    <span data-ttu-id="5ae8d-184">c.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-184">c.</span></span> <span data-ttu-id="5ae8d-185">В текстовое поле **Issuer** (Издатель) вставьте значение **идентификатора сущности SAML**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-185">In the **Issuer** textbox, paste the value of **SAML Entity ID**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="5ae8d-186">d.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-186">d.</span></span> <span data-ttu-id="5ae8d-187">В текстовое поле **Authn Request URL** (URL-адрес запроса аутентификации) вставьте значение **URL-адрес службы единого входа SAML**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-187">In the **Authn Request URL** textbox, paste the value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="5ae8d-188">д.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-188">e.</span></span> <span data-ttu-id="5ae8d-189">Откройте сертификат в кодировке Base-64 в Блокноте, скопируйте его содержимое в буфер обмена и вставьте весь сертификат в текстовое поле **Сертификат X.509** .</span><span class="sxs-lookup"><span data-stu-id="5ae8d-189">Open your base-64 encoded certificate in notepad, copy the content of it into your clipboard, and then paste the entire Certificate into **X.509 Certificate** textbox.</span></span>

    <span data-ttu-id="5ae8d-190">f.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-190">f.</span></span> <span data-ttu-id="5ae8d-191">В поле **Email Attribute** (Атрибут электронной почты) задайте значение **Use SAML subject** (Использовать субъект SAML).</span><span class="sxs-lookup"><span data-stu-id="5ae8d-191">As **Email Attribute**, select **Use SAML subject**.</span></span>  

    <span data-ttu-id="5ae8d-192">g.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-192">g.</span></span> <span data-ttu-id="5ae8d-193">Выберите пункт **Конфигурация входа, инициируемая поставщиком услуг**.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-193">Select **SP initiated Login Configuration**.</span></span>

    <span data-ttu-id="5ae8d-194">h.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-194">h.</span></span> <span data-ttu-id="5ae8d-195">В текстовом поле **Login Path** (Путь входа) введите **Azure** и нажмите кнопку **Save** (Сохранить).</span><span class="sxs-lookup"><span data-stu-id="5ae8d-195">In the **Login Path** textbox, type **Azure** and click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="5ae8d-196">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-196">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="5ae8d-197">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-197">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="5ae8d-198">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="5ae8d-198">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5ae8d-199">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="5ae8d-199">Creating an Azure AD test user</span></span>
<span data-ttu-id="5ae8d-200">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-200">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="5ae8d-202">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="5ae8d-202">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="5ae8d-203">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-203">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sumologic-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5ae8d-205">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-205">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sumologic-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5ae8d-207">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-207">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sumologic-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5ae8d-209">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-209">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-sumologic-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5ae8d-211">а.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-211">a.</span></span> <span data-ttu-id="5ae8d-212">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-212">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5ae8d-213">b.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-213">b.</span></span> <span data-ttu-id="5ae8d-214">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-214">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5ae8d-215">c.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-215">c.</span></span> <span data-ttu-id="5ae8d-216">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-216">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="5ae8d-217">d.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-217">d.</span></span> <span data-ttu-id="5ae8d-218">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-218">Click **Create**.</span></span>
 
### <a name="creating-a-sumologic-test-user"></a><span data-ttu-id="5ae8d-219">Создание тестового пользователя SumoLogic</span><span class="sxs-lookup"><span data-stu-id="5ae8d-219">Creating a SumoLogic test user</span></span>

<span data-ttu-id="5ae8d-220">Чтобы пользователи Azure AD могли входить в SumoLogic, их необходимо подготовить для SumoLogic.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-220">In order to enable Azure AD users to log in to SumoLogic, they must be provisioned to SumoLogic.</span></span>  

* <span data-ttu-id="5ae8d-221">В случае SumoLogic подготовка пользователей осуществляется вручную.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-221">In the case of SumoLogic, provisioning is a manual task.</span></span>

<span data-ttu-id="5ae8d-222">**Чтобы подготовить учетную запись пользователя, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="5ae8d-222">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="5ae8d-223">Войдите в клиент **SumoLogic** .</span><span class="sxs-lookup"><span data-stu-id="5ae8d-223">Log in to your **SumoLogic** tenant.</span></span>

2. <span data-ttu-id="5ae8d-224">Выберите **Manage \> Users** (Управление > Пользователи).</span><span class="sxs-lookup"><span data-stu-id="5ae8d-224">Go to **Manage \> Users**.</span></span>
   
    <span data-ttu-id="5ae8d-225">![Пользователи](./media/active-directory-saas-sumologic-tutorial/ic778561.png "Пользователи")</span><span class="sxs-lookup"><span data-stu-id="5ae8d-225">![Users](./media/active-directory-saas-sumologic-tutorial/ic778561.png "Users")</span></span>

3. <span data-ttu-id="5ae8d-226">Щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-226">Click **Add**.</span></span>
   
    <span data-ttu-id="5ae8d-227">![Пользователи](./media/active-directory-saas-sumologic-tutorial/ic778562.png "Пользователи")</span><span class="sxs-lookup"><span data-stu-id="5ae8d-227">![Users](./media/active-directory-saas-sumologic-tutorial/ic778562.png "Users")</span></span>

4. <span data-ttu-id="5ae8d-228">В диалоговом окне **Новый пользователь** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="5ae8d-228">On the **New User** dialog, perform the following steps:</span></span>
   
    <span data-ttu-id="5ae8d-229">![Новый пользователь](./media/active-directory-saas-sumologic-tutorial/ic778563.png "Новый пользователь")</span><span class="sxs-lookup"><span data-stu-id="5ae8d-229">![New User](./media/active-directory-saas-sumologic-tutorial/ic778563.png "New User")</span></span> 
 
    <span data-ttu-id="5ae8d-230">а.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-230">a.</span></span> <span data-ttu-id="5ae8d-231">Введите сведения об учетной записи Azure AD, которую необходимо подготовить, в текстовые поля **First Name** (Имя), **Last Name** (Фамилия) и **Email** (Адрес электронной почты).</span><span class="sxs-lookup"><span data-stu-id="5ae8d-231">Type the related information of the Azure AD account you want to provision into the **First Name**, **Last Name**, and **Email** textboxes.</span></span>
  
    <span data-ttu-id="5ae8d-232">b.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-232">b.</span></span> <span data-ttu-id="5ae8d-233">Выберите роль.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-233">Select a role.</span></span>
  
    <span data-ttu-id="5ae8d-234">c.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-234">c.</span></span> <span data-ttu-id="5ae8d-235">Для параметра **Status** (Состояние) выберите значение **Active** (Активно).</span><span class="sxs-lookup"><span data-stu-id="5ae8d-235">As **Status**, select **Active**.</span></span>
  
    <span data-ttu-id="5ae8d-236">d.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-236">d.</span></span> <span data-ttu-id="5ae8d-237">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-237">Click **Save**.</span></span>

>[!NOTE]
><span data-ttu-id="5ae8d-238">Вы можете использовать любые другие средства создания учетной записи пользователя SumoLogic или API-интерфейсы, предоставляемые SumoLogic для подготовки учетных записей пользователя AAD.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-238">You can use any other SumoLogic user account creation tools or APIs provided by SumoLogic to provision AAD user accounts.</span></span> 
> 

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="5ae8d-239">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="5ae8d-239">Assigning the Azure AD test user</span></span>

<span data-ttu-id="5ae8d-240">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив доступ к SumoLogic.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-240">In this section, you enable Britta Simon to use Azure single sign-on by granting access to SumoLogic.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="5ae8d-242">**Чтобы назначить пользователя Britta Simon приложению SumoLogic, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="5ae8d-242">**To assign Britta Simon to SumoLogic, perform the following steps:**</span></span>

1. <span data-ttu-id="5ae8d-243">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-243">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="5ae8d-245">В списке приложений выберите **SumoLogic**.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-245">In the applications list, select **SumoLogic**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-sumologic-tutorial/tutorial_sumologic_app.png) 

3. <span data-ttu-id="5ae8d-247">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-247">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="5ae8d-249">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-249">Click **Add** button.</span></span> <span data-ttu-id="5ae8d-250">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-250">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="5ae8d-252">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-252">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="5ae8d-253">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-253">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5ae8d-254">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-254">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5ae8d-255">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="5ae8d-255">Testing single sign-on</span></span>

<span data-ttu-id="5ae8d-256">Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-256">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="5ae8d-257">Щелкнув плитку SumoLogic на панели доступа, вы автоматически войдете в приложение SumoLogic.</span><span class="sxs-lookup"><span data-stu-id="5ae8d-257">When you click the SumoLogic tile in the Access Panel, you should get automatically signed-on to your SumoLogic application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5ae8d-258">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="5ae8d-258">Additional resources</span></span>

* [<span data-ttu-id="5ae8d-259">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5ae8d-259">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5ae8d-260">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="5ae8d-260">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sumologic-tutorial/tutorial_general_203.png

