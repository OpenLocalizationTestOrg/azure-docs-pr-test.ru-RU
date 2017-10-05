---
title: "Руководство по интеграции Azure Active Directory с Atlassian Cloud | Документация Майкрософт"
description: "Сведения о настройке единого входа Azure Active Directory в приложении Atlassian Cloud."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 729b8eb6-efc4-47fb-9f34-8998ca2c9545
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: 2891838b56dd15cb5f97dcae391770143a80c781
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-atlassian-cloud"></a><span data-ttu-id="742a3-103">Руководство по интеграции Azure Active Directory с Atlassian Cloud</span><span class="sxs-lookup"><span data-stu-id="742a3-103">Tutorial: Azure Active Directory integration with Atlassian Cloud</span></span>

<span data-ttu-id="742a3-104">В этом руководстве описано, как интегрировать приложение Atlassian Cloud с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="742a3-104">In this tutorial, you learn how to integrate Atlassian Cloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="742a3-105">Интеграция Azure AD с приложением Atlassian Cloud обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="742a3-105">Integrating Atlassian Cloud with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="742a3-106">С помощью Azure AD вы можете контролировать доступ к Atlassian Cloud.</span><span class="sxs-lookup"><span data-stu-id="742a3-106">You can control in Azure AD who has access to Atlassian Cloud</span></span>
- <span data-ttu-id="742a3-107">Вы можете включить автоматический вход пользователей в Atlassian Cloud (единый вход) с использованием учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="742a3-107">You can enable your users to automatically get signed-on to Atlassian Cloud (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="742a3-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="742a3-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="742a3-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="742a3-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="742a3-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="742a3-110">Prerequisites</span></span>

<span data-ttu-id="742a3-111">Чтобы настроить интеграцию Azure AD с приложением Atlassian Cloud, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="742a3-111">To configure Azure AD integration with Atlassian Cloud, you need the following items:</span></span>

- <span data-ttu-id="742a3-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="742a3-112">An Azure AD subscription</span></span>
- <span data-ttu-id="742a3-113">подписка Atlassian Cloud с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="742a3-113">An Atlassian Cloud single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="742a3-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="742a3-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="742a3-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="742a3-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="742a3-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="742a3-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="742a3-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="742a3-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="742a3-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="742a3-118">Scenario description</span></span>
<span data-ttu-id="742a3-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="742a3-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="742a3-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="742a3-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="742a3-121">добавление Atlassian Cloud из коллекции;</span><span class="sxs-lookup"><span data-stu-id="742a3-121">Adding Atlassian Cloud from the gallery</span></span>
2. <span data-ttu-id="742a3-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="742a3-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-atlassian-cloud-from-the-gallery"></a><span data-ttu-id="742a3-123">Добавление Atlassian Cloud из коллекции</span><span class="sxs-lookup"><span data-stu-id="742a3-123">Adding Atlassian Cloud from the gallery</span></span>
<span data-ttu-id="742a3-124">Чтобы настроить интеграцию Atlassian Cloud с Azure AD, необходимо добавить Atlassian Cloud из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="742a3-124">To configure the integration of Atlassian Cloud into Azure AD, you need to add Atlassian Cloud from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="742a3-125">**Чтобы добавить Atlassian Cloud из коллекции, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="742a3-125">**To add Atlassian Cloud from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="742a3-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="742a3-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="742a3-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="742a3-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="742a3-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="742a3-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="742a3-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="742a3-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="742a3-133">В поле поиска введите **Atlassian Cloud**.</span><span class="sxs-lookup"><span data-stu-id="742a3-133">In the search box, type **Atlassian Cloud**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_search.png)

5. <span data-ttu-id="742a3-135">На панели результатов выберите **Atlassian Cloud** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="742a3-135">In the results panel, select **Atlassian Cloud**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="742a3-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="742a3-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="742a3-138">В этом разделе описана настройка и проверка единого входа Azure AD в Atlassian Cloud с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="742a3-138">In this section, you configure and test Azure AD single sign-on with Atlassian Cloud based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="742a3-139">Чтобы настроить единый вход в Azure AD необходимо знать, какой пользователь в Atlassian Cloud соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="742a3-139">For single sign-on to work, Azure AD needs to know what the counterpart user in Atlassian Cloud is to a user in Azure AD.</span></span> <span data-ttu-id="742a3-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в Atlassian Cloud.</span><span class="sxs-lookup"><span data-stu-id="742a3-140">In other words, a link relationship between an Azure AD user and the related user in Atlassian Cloud needs to be established.</span></span>

<span data-ttu-id="742a3-141">Чтобы установить эту связь, следует назначить **имя пользователя** в Azure AD в качестве значения **имени пользователя** в Atlassian Cloud.</span><span class="sxs-lookup"><span data-stu-id="742a3-141">This link relationship is established by assigning the value of the **user name** in Azure AD as the value of the **Username** in Atlassian Cloud.</span></span>

<span data-ttu-id="742a3-142">Чтобы настроить и проверить единый вход Azure AD в Atlassian Cloud, выполните действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="742a3-142">To configure and test Azure AD single sign-on with Atlassian Cloud, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="742a3-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="742a3-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="742a3-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="742a3-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="742a3-145">**[Создание тестового пользователя Atlassian Cloud](#creating-an-atlassian-cloud-test-user)** требуется для создания в Atlassian Cloud пользователя Britta Simon, связанного с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="742a3-145">**[Creating an Atlassian Cloud test user](#creating-an-atlassian-cloud-test-user)** - to have a counterpart of Britta Simon in Atlassian Cloud that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="742a3-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="742a3-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="742a3-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="742a3-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="742a3-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="742a3-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="742a3-149">В этом разделе описано, как включить единый вход Azure AD на портале и настроить его в приложении Atlassian Cloud.</span><span class="sxs-lookup"><span data-stu-id="742a3-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your Atlassian Cloud application.</span></span>

<span data-ttu-id="742a3-150">**Чтобы настроить единый вход Azure AD в Atlassian Cloud, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="742a3-150">**To configure Azure AD single sign-on with Atlassian Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="742a3-151">На портале Azure на странице интеграции с приложением **Atlassian Cloud** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="742a3-151">In the Azure portal, on the **Atlassian Cloud** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="742a3-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="742a3-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_samlbase.png)

3. <span data-ttu-id="742a3-155">Если вы хотите настроить приложение в **режиме, инициированном поставщиком удостоверений**, то в разделе **Домены и URL-адреса приложения Atlassian Cloud** выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="742a3-155">On the **Atlassian Cloud Domain and URLs** section, perform the following steps if you wish to configure the application in **IDP** initiated mode:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_url.png)

    <span data-ttu-id="742a3-157">а.</span><span class="sxs-lookup"><span data-stu-id="742a3-157">a.</span></span> <span data-ttu-id="742a3-158">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<instancename>.atlassian.net/admin/saml/edit`</span><span class="sxs-lookup"><span data-stu-id="742a3-158">In the **Identifier** textbox, type a URL using the following pattern: `https://<instancename>.atlassian.net/admin/saml/edit`</span></span>

    <span data-ttu-id="742a3-159">b.</span><span class="sxs-lookup"><span data-stu-id="742a3-159">b.</span></span> <span data-ttu-id="742a3-160">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем виде: `https://id.atlassian.com/login/saml/acs`</span><span class="sxs-lookup"><span data-stu-id="742a3-160">In the **Reply URL** textbox, type a URL as: `https://id.atlassian.com/login/saml/acs`</span></span>

4. <span data-ttu-id="742a3-161">Установите флажок **Показать дополнительные параметры URL-адресов**, и выполните следующее действие, если хотите настроить приложение для работы в режиме, инициируемом **поставщиком услуг**:</span><span class="sxs-lookup"><span data-stu-id="742a3-161">Check **Show advanced URL settings** and perform the following step if you wish to configure the application in **SP** initiated mode:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_url1.png)

    <span data-ttu-id="742a3-163">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате: `https://<instancename>.atlassian.net`</span><span class="sxs-lookup"><span data-stu-id="742a3-163">In the **Sign-on URL** textbox, type a URL using the following pattern: `https://<instancename>.atlassian.net`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="742a3-164">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="742a3-164">These values are not real.</span></span> <span data-ttu-id="742a3-165">Измените их на фактические значения идентификатора и URL-адреса единого входа.</span><span class="sxs-lookup"><span data-stu-id="742a3-165">Update these values with the actual Identifier and Sign-On URL.</span></span> <span data-ttu-id="742a3-166">Точные значения можно получить на экране настройки SAML для Atlassian Cloud.</span><span class="sxs-lookup"><span data-stu-id="742a3-166">You can get the exact values from Atlassian Cloud SAML Configuration screen.</span></span>
 
5. <span data-ttu-id="742a3-167">В разделе **Сертификат подписи SAML** щелкните **Сертификат (Base64)**, а затем сохраните файл сертификата на компьютере.</span><span class="sxs-lookup"><span data-stu-id="742a3-167">On the **SAML Signing Certificate** section, click **Certificate(Base64)** and then save the certificate file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_certificate.png) 

6. <span data-ttu-id="742a3-169">В разделе **Настройка Atlassian Cloud** щелкните **Настроить Atlassian Cloud**, чтобы открыть окно **Настройка единого входа**.</span><span class="sxs-lookup"><span data-stu-id="742a3-169">On the **Atlassian Cloud Configuration** section, click **Configure Atlassian Cloud** to open **Configure sign-on** window.</span></span> <span data-ttu-id="742a3-170">Скопируйте **идентификатор сущности SAML и URL-адрес службы единого входа SAML** из раздела **Краткий справочник**.</span><span class="sxs-lookup"><span data-stu-id="742a3-170">Copy the **SAML Entity ID and SAML Single Sign-On Service URL** from the **Quick Reference section.**</span></span>

    ![Настройка единого входа](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_configure.png) 

7. <span data-ttu-id="742a3-172">Чтобы настроить единый вход для вашего приложения, войдите на портал Atlassian с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="742a3-172">To get SSO configured for your application, login to the Atlassian Portal using the administrator rights.</span></span>

8. <span data-ttu-id="742a3-173">В левой области навигации в разделе Authentication (Проверка подлинности) выберите пункт **Domains** (Домены).</span><span class="sxs-lookup"><span data-stu-id="742a3-173">In the Authentication section of the left navigation click **Domains**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_06.png)

    <span data-ttu-id="742a3-175">а.</span><span class="sxs-lookup"><span data-stu-id="742a3-175">a.</span></span> <span data-ttu-id="742a3-176">В текстовом поле введите имя домена, а затем нажмите кнопку **Add domain** (Добавить домен).</span><span class="sxs-lookup"><span data-stu-id="742a3-176">In the textbox, type your domain name, and then click **Add domain**.</span></span>
        
    ![Настройка единого входа](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_07.png)

    <span data-ttu-id="742a3-178">b.</span><span class="sxs-lookup"><span data-stu-id="742a3-178">b.</span></span> <span data-ttu-id="742a3-179">Чтобы проверить домен, нажмите кнопку **Verify** (Проверить).</span><span class="sxs-lookup"><span data-stu-id="742a3-179">To verify the domain, click **Verify**.</span></span> 

    ![Настройка единого входа](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_08.png)

    <span data-ttu-id="742a3-181">c.</span><span class="sxs-lookup"><span data-stu-id="742a3-181">c.</span></span> <span data-ttu-id="742a3-182">Скачайте HTML-файл проверки домена, передайте его в корневую папку веб-сайта в домене и нажмите кнопку **Verify domain** (Проверить домен).</span><span class="sxs-lookup"><span data-stu-id="742a3-182">Download the domain verification html file, upload it to the root folder of your domain's website, and then click **Verify domain**.</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_09.png)

    <span data-ttu-id="742a3-184">г)</span><span class="sxs-lookup"><span data-stu-id="742a3-184">d.</span></span> <span data-ttu-id="742a3-185">После проверки домена значение в поле **Status** (Состояние) изменится на **Verified** (Проверено).</span><span class="sxs-lookup"><span data-stu-id="742a3-185">Once the domain is verified, the value of the **Status** field is **Verified**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_10.png)

9. <span data-ttu-id="742a3-187">В левой панели навигации щелкните **SAML**.</span><span class="sxs-lookup"><span data-stu-id="742a3-187">In the left navigation bar, click **SAML**.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_11.png)

10. <span data-ttu-id="742a3-189">Создайте конфигурацию SAML и задайте параметры поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="742a3-189">Create a SAML Configuration and add the Identity provider configuration.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_12.png)

    <span data-ttu-id="742a3-191">а.</span><span class="sxs-lookup"><span data-stu-id="742a3-191">a.</span></span> <span data-ttu-id="742a3-192">В текстовое поле **Identity Provider Entity ID** (Идентификатор сущности поставщика удостоверений) вставьте значение **Идентификатор сущности SAML**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="742a3-192">In the **Identity provider Entity ID** text box, paste the value of  **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="742a3-193">b.</span><span class="sxs-lookup"><span data-stu-id="742a3-193">b.</span></span> <span data-ttu-id="742a3-194">В текстовое поле **Identity Provider SSO URL** (URL-адрес единого входа поставщика удостоверений) вставьте значение **URL-адрес службы единого входа SAML**, скопированное на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="742a3-194">In the **Identity provider SSO URL** text box, paste the value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="742a3-195">c.</span><span class="sxs-lookup"><span data-stu-id="742a3-195">c.</span></span> <span data-ttu-id="742a3-196">Откройте сертификат, скачанный с портала Azure, скопируйте значения без строк Begin и End и вставьте их в поле **Public X509 certificate** (Общий сертификат X509).</span><span class="sxs-lookup"><span data-stu-id="742a3-196">Open the downloaded certificate from Azure portal and copy the values without the Begin and End lines and paste it in the **Public X509 certificate** box.</span></span>
    
    <span data-ttu-id="742a3-197">г)</span><span class="sxs-lookup"><span data-stu-id="742a3-197">d.</span></span> <span data-ttu-id="742a3-198">Чтобы сохранить параметры, нажмите кнопку **Save Configuration** (Сохранить конфигурацию).</span><span class="sxs-lookup"><span data-stu-id="742a3-198">Click **Save Configuration**  to Save the settings.</span></span>
     
11. <span data-ttu-id="742a3-199">В параметрах Azure AD задайте правильный URL-адрес идентификатора.</span><span class="sxs-lookup"><span data-stu-id="742a3-199">Update the Azure AD settings to make sure that you have setup the correct Identifier URL.</span></span>
  
    <span data-ttu-id="742a3-200">а.</span><span class="sxs-lookup"><span data-stu-id="742a3-200">a.</span></span> <span data-ttu-id="742a3-201">Скопируйте **идентификатор удостоверения поставщика услуг** на экране SAML и вставьте его в Azure AD в качестве значения поля **Идентификатор**.</span><span class="sxs-lookup"><span data-stu-id="742a3-201">Copy the **SP Identity ID** from the SAML screen and paste it in Azure AD as the **Identifier** value.</span></span>

    <span data-ttu-id="742a3-202">b.</span><span class="sxs-lookup"><span data-stu-id="742a3-202">b.</span></span> <span data-ttu-id="742a3-203">URL-адрес входа является URL-адресом клиента приложения Atlassian Cloud.</span><span class="sxs-lookup"><span data-stu-id="742a3-203">Sign On URL is the tenant URL of your Atlassian Cloud.</span></span>   

     ![Настройка единого входа](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_13.png)
    
12. <span data-ttu-id="742a3-205">На портале Azure нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="742a3-205">In the Azure portal, Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_400.png)

> [!TIP]
> <span data-ttu-id="742a3-207">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="742a3-207">You can now read a concise version of these instructions inside the [Azure  portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="742a3-208">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="742a3-208">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="742a3-209">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="742a3-209">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="742a3-210">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="742a3-210">Creating an Azure AD test user</span></span>
<span data-ttu-id="742a3-211">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="742a3-211">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="742a3-213">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="742a3-213">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="742a3-214">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="742a3-214">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="742a3-216">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="742a3-216">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="742a3-218">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="742a3-218">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="742a3-220">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="742a3-220">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-atlassian-cloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="742a3-222">а.</span><span class="sxs-lookup"><span data-stu-id="742a3-222">a.</span></span> <span data-ttu-id="742a3-223">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="742a3-223">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="742a3-224">b.</span><span class="sxs-lookup"><span data-stu-id="742a3-224">b.</span></span> <span data-ttu-id="742a3-225">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="742a3-225">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="742a3-226">c.</span><span class="sxs-lookup"><span data-stu-id="742a3-226">c.</span></span> <span data-ttu-id="742a3-227">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="742a3-227">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="742a3-228">d.</span><span class="sxs-lookup"><span data-stu-id="742a3-228">d.</span></span> <span data-ttu-id="742a3-229">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="742a3-229">Click **Create**.</span></span>
 
### <a name="creating-an-atlassian-cloud-test-user"></a><span data-ttu-id="742a3-230">Создание тестового пользователя Atlassian Cloud</span><span class="sxs-lookup"><span data-stu-id="742a3-230">Creating an Atlassian Cloud test user</span></span>

<span data-ttu-id="742a3-231">Чтобы пользователи Azure AD могли выполнять вход в Atlassian Cloud, они должны быть подготовлены в Atlassian Cloud.</span><span class="sxs-lookup"><span data-stu-id="742a3-231">To enable Azure AD users to log in to Atlassian Cloud, they must be provisioned into Atlassian Cloud.</span></span>  
<span data-ttu-id="742a3-232">В случае Atlassian Cloud подготовка выполняется вручную.</span><span class="sxs-lookup"><span data-stu-id="742a3-232">In case of Atlassian Cloud, provisioning is a manual task.</span></span>

<span data-ttu-id="742a3-233">**Чтобы подготовить учетную запись пользователя, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="742a3-233">**To provision a user account, perform the following steps:**</span></span>

1. <span data-ttu-id="742a3-234">В разделе "Site administration" (Администрирование сайта) нажмите кнопку **Users** (Пользователи).</span><span class="sxs-lookup"><span data-stu-id="742a3-234">In the Site administration section, click the **Users** button</span></span>

    ![Создание пользователя Atlassian Cloud](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_14.png) 

2. <span data-ttu-id="742a3-236">Нажмите кнопку **Create User** (Создать пользователя), чтобы создать пользователя в приложении Atlassian Cloud.</span><span class="sxs-lookup"><span data-stu-id="742a3-236">Click the **Create User** button to create a user in the Atlassian Cloud</span></span>

    ![Создание пользователя Atlassian Cloud](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_15.png) 

3. <span data-ttu-id="742a3-238">Введите **адрес электронной почты**, **имя пользователя** и **полное имя** и предоставьте доступ к приложению.</span><span class="sxs-lookup"><span data-stu-id="742a3-238">Enter the user's **Email address**, **Username**, and **Full Name** and assign the application access.</span></span> 

    ![Создание пользователя Atlassian Cloud](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_16.png)
 
4. <span data-ttu-id="742a3-240">Нажмите кнопку **Create user** (Создать пользователя). После этого пользователю будет отправлено приглашение по электронной почте. Как только пользователь примет приглашение, он станет активным в системе.</span><span class="sxs-lookup"><span data-stu-id="742a3-240">Click **Create user** button, it will send the email invitation to the user and after accepting the invitation the user will be active in the system.</span></span> 

>[!NOTE] 
><span data-ttu-id="742a3-241">Вы также можете создать несколько пользователей, нажав кнопку **Bulk Create** (Массовое создание) в разделе "Users" (Пользователи).</span><span class="sxs-lookup"><span data-stu-id="742a3-241">You can also create the bulk users by clicking the **Bulk Create** button in the Users section.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="742a3-242">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="742a3-242">Assigning the Azure AD test user</span></span>

<span data-ttu-id="742a3-243">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure путем предоставления доступа к Atlassian Cloud.</span><span class="sxs-lookup"><span data-stu-id="742a3-243">In this section, you enable Britta Simon to use Azure single sign-on by granting access to Atlassian Cloud.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="742a3-245">**Чтобы назначить пользователя Britta Simon в Atlassian Cloud, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="742a3-245">**To assign Britta Simon to Atlassian Cloud, perform the following steps:**</span></span>

1. <span data-ttu-id="742a3-246">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="742a3-246">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="742a3-248">В списке приложений выберите **Atlassian Cloud**.</span><span class="sxs-lookup"><span data-stu-id="742a3-248">In the applications list, select **Atlassian Cloud**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_atlassiancloud_app.png) 

3. <span data-ttu-id="742a3-250">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="742a3-250">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="742a3-252">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="742a3-252">Click **Add** button.</span></span> <span data-ttu-id="742a3-253">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="742a3-253">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="742a3-255">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="742a3-255">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="742a3-256">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="742a3-256">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="742a3-257">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="742a3-257">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="742a3-258">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="742a3-258">Testing single sign-on</span></span>

<span data-ttu-id="742a3-259">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="742a3-259">In this section, you test your Azure AD SSO configuration using the Access Panel.</span></span>

<span data-ttu-id="742a3-260">Щелкнув плитку Atlassian Cloud на панели доступа, вы автоматически войдете в приложение Atlassian Cloud.</span><span class="sxs-lookup"><span data-stu-id="742a3-260">When you click the Atlassian Cloud tile in the Access Panel, you should get automatically signed-on to your Atlassian Cloud application.</span></span> <span data-ttu-id="742a3-261">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="742a3-261">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="742a3-262">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="742a3-262">Additional resources</span></span>

* [<span data-ttu-id="742a3-263">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="742a3-263">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="742a3-264">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="742a3-264">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-atlassian-cloud-tutorial/tutorial_general_203.png

