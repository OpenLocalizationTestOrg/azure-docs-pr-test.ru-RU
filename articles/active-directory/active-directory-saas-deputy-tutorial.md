---
title: "Учебник. Интеграция Azure Active Directory с Deputy | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и Deputy."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5665c3ac-5689-4201-80fe-fcc677d4430d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 51aed908208b7a40ea2ab710dffe84370b573991
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-deputy"></a><span data-ttu-id="07e6b-103">Руководство. Интеграция Azure Active Directory с Deputy</span><span class="sxs-lookup"><span data-stu-id="07e6b-103">Tutorial: Azure Active Directory integration with Deputy</span></span>

<span data-ttu-id="07e6b-104">В этом руководстве описано, как интегрировать Deputy с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="07e6b-104">In this tutorial, you learn how to integrate Deputy with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="07e6b-105">Интеграция Azure AD с приложением Deputy обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="07e6b-105">Integrating Deputy with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="07e6b-106">С помощью Azure AD вы можете контролировать доступ к Deputy.</span><span class="sxs-lookup"><span data-stu-id="07e6b-106">You can control in Azure AD who has access to Deputy</span></span>
- <span data-ttu-id="07e6b-107">Вы можете включить автоматический вход пользователей в Deputy (единый вход) с помощью учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="07e6b-107">You can enable your users to automatically get signed-on to Deputy (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="07e6b-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="07e6b-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="07e6b-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="07e6b-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="07e6b-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="07e6b-110">Prerequisites</span></span>

<span data-ttu-id="07e6b-111">Чтобы настроить интеграцию Azure AD с Deputy, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="07e6b-111">To configure Azure AD integration with Deputy, you need the following items:</span></span>

- <span data-ttu-id="07e6b-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="07e6b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="07e6b-113">подписка Deputy с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="07e6b-113">A Deputy single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="07e6b-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="07e6b-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="07e6b-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="07e6b-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="07e6b-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="07e6b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="07e6b-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="07e6b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="07e6b-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="07e6b-118">Scenario description</span></span>
<span data-ttu-id="07e6b-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="07e6b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="07e6b-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="07e6b-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="07e6b-121">Добавление Deputy из коллекции</span><span class="sxs-lookup"><span data-stu-id="07e6b-121">Adding Deputy from the gallery</span></span>
2. <span data-ttu-id="07e6b-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="07e6b-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-deputy-from-the-gallery"></a><span data-ttu-id="07e6b-123">Добавление Deputy из коллекции</span><span class="sxs-lookup"><span data-stu-id="07e6b-123">Adding Deputy from the gallery</span></span>
<span data-ttu-id="07e6b-124">Чтобы настроить интеграцию Deputy с Azure AD, необходимо добавить Deputy из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="07e6b-124">To configure the integration of Deputy into Azure AD, you need to add Deputy from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="07e6b-125">**Чтобы добавить Deputy из коллекции, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="07e6b-125">**To add Deputy from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="07e6b-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="07e6b-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="07e6b-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="07e6b-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="07e6b-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="07e6b-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="07e6b-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="07e6b-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="07e6b-133">В поле поиска введите **Deputy**.</span><span class="sxs-lookup"><span data-stu-id="07e6b-133">In the search box, type **Deputy**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_search.png)

5. <span data-ttu-id="07e6b-135">На панели результатов выберите **Deputy** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="07e6b-135">In the results panel, select **Deputy**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="07e6b-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="07e6b-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="07e6b-138">В этом разделе описана настройка и проверка единого входа Azure AD в приложение Deputy с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="07e6b-138">In this section, you configure and test Azure AD single sign-on with Deputy based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="07e6b-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в Deputy соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="07e6b-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Deputy is to a user in Azure AD.</span></span> <span data-ttu-id="07e6b-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Deputy.</span><span class="sxs-lookup"><span data-stu-id="07e6b-140">In other words, a link relationship between an Azure AD user and the related user in Deputy needs to be established.</span></span>

<span data-ttu-id="07e6b-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Deputy.</span><span class="sxs-lookup"><span data-stu-id="07e6b-141">In Deputy, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="07e6b-142">Чтобы настроить и проверить единый вход Azure AD в Deputy, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="07e6b-142">To configure and test Azure AD single sign-on with Deputy, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="07e6b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="07e6b-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="07e6b-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="07e6b-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="07e6b-145">**[Создание тестового пользователя Deputy](#creating-a-deputy-test-user)** требуется для создания в Deputy пользователя Britta Simon, связанного с представлением этого же пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="07e6b-145">**[Creating a Deputy test user](#creating-a-deputy-test-user)** - to have a counterpart of Britta Simon in Deputy that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="07e6b-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="07e6b-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="07e6b-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="07e6b-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="07e6b-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="07e6b-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="07e6b-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении Deputy.</span><span class="sxs-lookup"><span data-stu-id="07e6b-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Deputy application.</span></span>

<span data-ttu-id="07e6b-150">**Чтобы настроить единый вход Azure AD в Deputy, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="07e6b-150">**To configure Azure AD single sign-on with Deputy, perform the following steps:**</span></span>

1. <span data-ttu-id="07e6b-151">На портале Azure на странице интеграции с приложением **Deputy** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="07e6b-151">In the Azure portal, on the **Deputy** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="07e6b-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="07e6b-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_samlbase.png)

3. <span data-ttu-id="07e6b-155">Если вы хотите настроить приложение в **режиме, инициированном поставщиком удостоверений**, то в разделе **Домен и URL-адреса приложения Deputy** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="07e6b-155">On the **Deputy Domain and URLs** section, If you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_url1.png)

    <span data-ttu-id="07e6b-157">а.</span><span class="sxs-lookup"><span data-stu-id="07e6b-157">a.</span></span> <span data-ttu-id="07e6b-158">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="07e6b-158">In the **Identifier** textbox, type a URL using the following pattern:</span></span>
    |  |
    | ----|
    | `https://<subdomain>.<region>.au.deputy.com` |
    | `https://<subdomain>.<region>.ent-au.deputy.com` |
    | `https://<subdomain>.<region>.na.deputy.com`|
    | `https://<subdomain>.<region>.ent-na.deputy.com`|
    | `https://<subdomain>.<region>.eu.deputy.com` |
    | `https://<subdomain>.<region>.ent-eu.deputy.com` |
    | `https://<subdomain>.<region>.as.deputy.com` |
    | `https://<subdomain>.<region>.ent-as.deputy.com` |
    | `https://<subdomain>.<region>.la.deputy.com` |
    | `https://<subdomain>.<region>.ent-la.deputy.com` |
    | `https://<subdomain>.<region>.af.deputy.com` |
    | `https://<subdomain>.<region>.ent-af.deputy.com` |
    | `https://<subdomain>.<region>.an.deputy.com` |
    | `https://<subdomain>.<region>.ent-an.deputy.com` |
    | `https://<subdomain>.<region>.deputy.com` |

    <span data-ttu-id="07e6b-159">b.</span><span class="sxs-lookup"><span data-stu-id="07e6b-159">b.</span></span> <span data-ttu-id="07e6b-160">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="07e6b-160">In the **Reply URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |----|
    | `https://<subdomain>.<region>.au.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-au.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.na.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-na.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.eu.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-eu.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.as.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-as.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.la.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-la.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.af.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-af.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.an.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.ent-an.deputy.com/exec/devapp/samlacs.` |
    | `https://<subdomain>.<region>.deputy.com/exec/devapp/samlacs.` |

4. <span data-ttu-id="07e6b-161">Установите флажок **Показать дополнительные параметры URL-адресов**,</span><span class="sxs-lookup"><span data-stu-id="07e6b-161">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="07e6b-162">если хотите настроить приложение для работы в режиме, инициируемом **поставщиком услуг**.</span><span class="sxs-lookup"><span data-stu-id="07e6b-162">If you wish to configure the application in **SP** initiated mode:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_url2.png)

    <span data-ttu-id="07e6b-164">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<your-subdomain>.<region>.deputy.com`</span><span class="sxs-lookup"><span data-stu-id="07e6b-164">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<your-subdomain>.<region>.deputy.com`</span></span>
    
    >[!NOTE]
    > <span data-ttu-id="07e6b-165">Суффикс региона Deputy необязательный, или следует использовать один из следующих: au | na | eu |as |la |af |an |ent-au |ent-na |ent-eu |ent-as | ent-la | ent-af | ent-an.</span><span class="sxs-lookup"><span data-stu-id="07e6b-165">Deputy region suffix is optional, or it should use one of these: au | na | eu |as |la |af |an |ent-au |ent-na |ent-eu |ent-as | ent-la | ent-af | ent-an</span></span>

    > [!NOTE] 
    > <span data-ttu-id="07e6b-166">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="07e6b-166">These values are not real.</span></span> <span data-ttu-id="07e6b-167">Замените их фактическими значениями идентификатора, URL-адреса ответа и URL-адреса входа.</span><span class="sxs-lookup"><span data-stu-id="07e6b-167">Update these values with the actual Identifier, Reply URL, and Sign-On URL.</span></span> <span data-ttu-id="07e6b-168">Чтобы получить эти значения, обратитесь в [службу поддержки Deputy](https://www.deputy.com/call-centers-customer-support-scheduling-software).</span><span class="sxs-lookup"><span data-stu-id="07e6b-168">Contact [Deputy support team](https://www.deputy.com/call-centers-customer-support-scheduling-software) to get these values.</span></span> 

5. <span data-ttu-id="07e6b-169">В разделе **Сертификат подписи SAML** щелкните **Сертификат (Base64)**, а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="07e6b-169">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_certificate.png) 

6. <span data-ttu-id="07e6b-171">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="07e6b-171">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-deputy-tutorial/tutorial_general_400.png)
    
7. <span data-ttu-id="07e6b-173">В разделе **Конфигурация Deputy** щелкните **Настроить Deputy**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="07e6b-173">On the **Deputy Configuration** section, click **Configure Deputy** to open **Configure sign-on** window.</span></span> <span data-ttu-id="07e6b-174">Скопируйте **URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="07e6b-174">Copy the **SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_configure.png) 

8. <span data-ttu-id="07e6b-176">Перейдите по следующему URL-адресу: [https://(ваш_поддомен).deputy.com/exec/config/system_config]( https://(your-subdomain).deputy.com/exec/config/system_config).</span><span class="sxs-lookup"><span data-stu-id="07e6b-176">Navigate to the following URL:[https://(your-subdomain).deputy.com/exec/config/system_config]( https://(your-subdomain).deputy.com/exec/config/system_config).</span></span> <span data-ttu-id="07e6b-177">Выберите пункт **Параметры безопасности** и нажмите кнопку **Изменить**.</span><span class="sxs-lookup"><span data-stu-id="07e6b-177">Go to **Security Settings** and click **Edit**.</span></span>
   
    ![Настройка единого входа](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_004.png)

9. <span data-ttu-id="07e6b-179">На странице **Параметры безопасности** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="07e6b-179">On this **Security Settings** page, perform below steps.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_005.png)
    
    <span data-ttu-id="07e6b-181">а.</span><span class="sxs-lookup"><span data-stu-id="07e6b-181">a.</span></span> <span data-ttu-id="07e6b-182">разрешите **вход с помощью учетных записей социальных сетей**;</span><span class="sxs-lookup"><span data-stu-id="07e6b-182">Enable **Social Login**.</span></span>
   
    <span data-ttu-id="07e6b-183">b.</span><span class="sxs-lookup"><span data-stu-id="07e6b-183">b.</span></span> <span data-ttu-id="07e6b-184">Откройте в блокноте сертификат в кодировке Base-64, скачанный с портала Azure, скопируйте его в буфер обмена и вставьте в текстовое поле **Сертификат OpenSSL**.</span><span class="sxs-lookup"><span data-stu-id="07e6b-184">Open your Base64 encoded certificate downloaded from Azure portal in notepad, copy the content of it into your clipboard, and then paste it to the **OpenSSL Certificate** textbox.</span></span>
   
    <span data-ttu-id="07e6b-185">c.</span><span class="sxs-lookup"><span data-stu-id="07e6b-185">c.</span></span> <span data-ttu-id="07e6b-186">В текстовом поле SAML SSO URL (URL-адрес единого входа) введите `https://<your subdomain>.deputy.com/exec/devapp/samlacs?dpLoginTo=<saml sso url>`.</span><span class="sxs-lookup"><span data-stu-id="07e6b-186">In the SAML SSO URL textbox, type `https://<your subdomain>.deputy.com/exec/devapp/samlacs?dpLoginTo=<saml sso url>`</span></span>
    
    <span data-ttu-id="07e6b-187">г)</span><span class="sxs-lookup"><span data-stu-id="07e6b-187">d.</span></span> <span data-ttu-id="07e6b-188">в текстовом поле SAML SSO URL (URL-адрес единого входа) замените `<your subdomain>` на ваш поддомен;</span><span class="sxs-lookup"><span data-stu-id="07e6b-188">In the SAML SSO URL textbox, replace `<your subdomain>` with your subdomain.</span></span>
   
    <span data-ttu-id="07e6b-189">д.</span><span class="sxs-lookup"><span data-stu-id="07e6b-189">e.</span></span> <span data-ttu-id="07e6b-190">В текстовом поле SAML SSO URL (URL-адрес единого входа) замените `<saml sso url>` на **URL-адрес службы единого входа SAML**, скопированный c портала Azure.</span><span class="sxs-lookup"><span data-stu-id="07e6b-190">In the SAML SSO URL textbox, replace `<saml sso url>` with the **SAML Single Sign-On Service URL** you have copied from the Azure portal.</span></span>
   
    <span data-ttu-id="07e6b-191">f.</span><span class="sxs-lookup"><span data-stu-id="07e6b-191">f.</span></span> <span data-ttu-id="07e6b-192">Нажмите кнопку **Сохранить параметры**.</span><span class="sxs-lookup"><span data-stu-id="07e6b-192">Click **Save Settings**.</span></span>

> [!TIP]
> <span data-ttu-id="07e6b-193">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="07e6b-193">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="07e6b-194">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="07e6b-194">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="07e6b-195">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="07e6b-195">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="07e6b-196">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="07e6b-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="07e6b-197">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="07e6b-197">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="07e6b-199">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="07e6b-199">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="07e6b-200">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="07e6b-200">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-deputy-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="07e6b-202">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="07e6b-202">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-deputy-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="07e6b-204">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="07e6b-204">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-deputy-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="07e6b-206">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="07e6b-206">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-deputy-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="07e6b-208">а.</span><span class="sxs-lookup"><span data-stu-id="07e6b-208">a.</span></span> <span data-ttu-id="07e6b-209">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="07e6b-209">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="07e6b-210">b.</span><span class="sxs-lookup"><span data-stu-id="07e6b-210">b.</span></span> <span data-ttu-id="07e6b-211">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="07e6b-211">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="07e6b-212">c.</span><span class="sxs-lookup"><span data-stu-id="07e6b-212">c.</span></span> <span data-ttu-id="07e6b-213">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="07e6b-213">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="07e6b-214">d.</span><span class="sxs-lookup"><span data-stu-id="07e6b-214">d.</span></span> <span data-ttu-id="07e6b-215">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="07e6b-215">Click **Create**.</span></span>
 
### <a name="creating-a-deputy-test-user"></a><span data-ttu-id="07e6b-216">Создание тестового пользователя приложения Deputy</span><span class="sxs-lookup"><span data-stu-id="07e6b-216">Creating a Deputy test user</span></span>

<span data-ttu-id="07e6b-217">Чтобы пользователи Azure AD могли выполнять вход в Deputy, они должны быть подготовлены для Deputy.</span><span class="sxs-lookup"><span data-stu-id="07e6b-217">To enable Azure AD users to log in to Deputy, they must be provisioned into Deputy.</span></span> <span data-ttu-id="07e6b-218">В случае с Deputy подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="07e6b-218">In case of Deputy, provisioning is a manual task.</span></span>

#### <a name="to-provision-a-user-account-perform-the-following-steps"></a><span data-ttu-id="07e6b-219">Чтобы подготовить учетную запись пользователя, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="07e6b-219">To provision a user account, perform the following steps:</span></span>
1. <span data-ttu-id="07e6b-220">Войдите на сайт Deputy компании в качестве администратора.</span><span class="sxs-lookup"><span data-stu-id="07e6b-220">Log in to your Deputy company site as an administrator.</span></span>

2. <span data-ttu-id="07e6b-221">В верхней части области навигации щелкните **People**(Люди).</span><span class="sxs-lookup"><span data-stu-id="07e6b-221">On the top navigation pane, click **People**.</span></span>
   
   <span data-ttu-id="07e6b-222">![Люди](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_001.png "Люди")</span><span class="sxs-lookup"><span data-stu-id="07e6b-222">![People](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_001.png "People")</span></span>

3. <span data-ttu-id="07e6b-223">Нажмите кнопку **Add People** (Добавить людей) и выберите пункт **Add a single person** (Добавить одного человека).</span><span class="sxs-lookup"><span data-stu-id="07e6b-223">Click the **Add People** button and click **Add a single person**.</span></span>
   
   <span data-ttu-id="07e6b-224">![Добавить участников](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_002.png "добавить участников")</span><span class="sxs-lookup"><span data-stu-id="07e6b-224">![Add People](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_002.png "Add People")</span></span>

4. <span data-ttu-id="07e6b-225">Выполните следующие действия и нажмите кнопку **Save & Invite** (Сохранить и пригласить).</span><span class="sxs-lookup"><span data-stu-id="07e6b-225">Perform the following steps and click **Save & Invite**.</span></span>
   
   <span data-ttu-id="07e6b-226">![Новый пользователь](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_003.png "Новый пользователь")</span><span class="sxs-lookup"><span data-stu-id="07e6b-226">![New User](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_003.png "New User")</span></span>

   <span data-ttu-id="07e6b-227">а.</span><span class="sxs-lookup"><span data-stu-id="07e6b-227">a.</span></span> <span data-ttu-id="07e6b-228">В текстовом поле **Имя** введите имя, например **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="07e6b-228">In the **Name** textbox, type name of the user like **BrittaSimon**.</span></span>
   
   <span data-ttu-id="07e6b-229">b.</span><span class="sxs-lookup"><span data-stu-id="07e6b-229">b.</span></span> <span data-ttu-id="07e6b-230">В текстовое поле **Email** (Электронная почта) введите адрес электронной почты той учетной записи Azure AD, которую нужно подготовить.</span><span class="sxs-lookup"><span data-stu-id="07e6b-230">In the **Email** textbox, type the email address of an Azure AD account you want to provision.</span></span>
   
   <span data-ttu-id="07e6b-231">c.</span><span class="sxs-lookup"><span data-stu-id="07e6b-231">c.</span></span> <span data-ttu-id="07e6b-232">В текстовом поле **Work at** (Место работы) введите название компании.</span><span class="sxs-lookup"><span data-stu-id="07e6b-232">In the **Work at** textbox, type the business name.</span></span>
   
   <span data-ttu-id="07e6b-233">г)</span><span class="sxs-lookup"><span data-stu-id="07e6b-233">d.</span></span> <span data-ttu-id="07e6b-234">Нажмите кнопку **Save & Invite** (Сохранить и пригласить).</span><span class="sxs-lookup"><span data-stu-id="07e6b-234">Click **Save & Invite** button.</span></span>

5. <span data-ttu-id="07e6b-235">Владелец учетной записи AAD получит по электронной почте сообщение со ссылкой для активации учетной записи.</span><span class="sxs-lookup"><span data-stu-id="07e6b-235">The AAD account holder receives an email and follows a link to confirm their account before it becomes active.</span></span> <span data-ttu-id="07e6b-236">Вы можете использовать любые другие средства создания учетной записи пользователя Deputy или API, предоставляемые Deputy для подготовки учетных записей пользователя AAD.</span><span class="sxs-lookup"><span data-stu-id="07e6b-236">You can use any other Deputy user account creation tools or APIs provided by Deputy to provision AAD user accounts.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="07e6b-237">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="07e6b-237">Assigning the Azure AD test user</span></span>

<span data-ttu-id="07e6b-238">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure путем предоставления доступа к Deputy.</span><span class="sxs-lookup"><span data-stu-id="07e6b-238">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Deputy.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="07e6b-240">**Чтобы назначить пользователя Britta Simon в Deputy, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="07e6b-240">**To assign Britta Simon to Deputy, perform the following steps:**</span></span>

1. <span data-ttu-id="07e6b-241">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="07e6b-241">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="07e6b-243">В списке приложений выберите **Deputy**.</span><span class="sxs-lookup"><span data-stu-id="07e6b-243">In the applications list, select **Deputy**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-deputy-tutorial/tutorial_deputy_app.png) 

3. <span data-ttu-id="07e6b-245">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="07e6b-245">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="07e6b-247">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="07e6b-247">Click **Add** button.</span></span> <span data-ttu-id="07e6b-248">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="07e6b-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="07e6b-250">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="07e6b-250">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="07e6b-251">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="07e6b-251">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="07e6b-252">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="07e6b-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="07e6b-253">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="07e6b-253">Testing single sign-on</span></span>

<span data-ttu-id="07e6b-254">Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="07e6b-254">The objective of this section is to test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="07e6b-255">Щелкнув элемент Deputy на панели доступа, вы автоматически войдете в приложение Deputy.</span><span class="sxs-lookup"><span data-stu-id="07e6b-255">When you click the Deputy tile in the Access Panel, you should get automatically signed-on to your Deputy application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="07e6b-256">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="07e6b-256">Additional resources</span></span>

* [<span data-ttu-id="07e6b-257">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="07e6b-257">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="07e6b-258">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="07e6b-258">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-deputy-tutorial/tutorial_general_203.png

