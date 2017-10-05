---
title: "Руководство. Интеграция Azure Active Directory с решением EthicsPoint Incident Management (EPIM) | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и EthicsPoint Incident Management (EPIM)."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8cb31a4c-9309-469b-93ac-daf0d3c7a3e6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: jeedes
ms.openlocfilehash: b5ac3afd973b5765ba151e766754934b49ac0e0c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ethicspoint-incident-management-epim"></a><span data-ttu-id="725f5-103">Руководство. Интеграция Azure Active Directory с решением EthicsPoint Incident Management (EPIM)</span><span class="sxs-lookup"><span data-stu-id="725f5-103">Tutorial: Azure Active Directory integration with EthicsPoint Incident Management (EPIM)</span></span>

<span data-ttu-id="725f5-104">В этом руководстве описано, как интегрировать решение EthicsPoint Incident Management (EPIM) с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="725f5-104">In this tutorial, you learn how to integrate EthicsPoint Incident Management (EPIM) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="725f5-105">Интеграция EthicsPoint Incident Management (EPIM) с Azure AD обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="725f5-105">Integrating EthicsPoint Incident Management (EPIM) with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="725f5-106">С помощью Azure AD можно контролировать доступ к EthicsPoint Incident Management (EPIM).</span><span class="sxs-lookup"><span data-stu-id="725f5-106">You can control in Azure AD who has access to EthicsPoint Incident Management (EPIM)</span></span>
- <span data-ttu-id="725f5-107">Вы можете включить автоматический вход пользователей в EthicsPoint Incident Management (EPIM) (единый вход) с учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="725f5-107">You can enable your users to automatically get signed-on to EthicsPoint Incident Management (EPIM) (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="725f5-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="725f5-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="725f5-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="725f5-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="725f5-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="725f5-110">Prerequisites</span></span>

<span data-ttu-id="725f5-111">Чтобы настроить интеграцию Azure AD с EthicsPoint Incident Management (EPIM), вам потребуется следующее:</span><span class="sxs-lookup"><span data-stu-id="725f5-111">To configure Azure AD integration with EthicsPoint Incident Management (EPIM), you need the following items:</span></span>

- <span data-ttu-id="725f5-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="725f5-112">An Azure AD subscription</span></span>
- <span data-ttu-id="725f5-113">подписка EthicsPoint Incident Management (EPIM) с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="725f5-113">A EthicsPoint Incident Management (EPIM) single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="725f5-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="725f5-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="725f5-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="725f5-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="725f5-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="725f5-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="725f5-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="725f5-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="725f5-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="725f5-118">Scenario description</span></span>
<span data-ttu-id="725f5-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="725f5-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="725f5-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="725f5-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="725f5-121">Добавление решения EthicsPoint Incident Management (EPIM) из коллекции.</span><span class="sxs-lookup"><span data-stu-id="725f5-121">Adding EthicsPoint Incident Management (EPIM) from the gallery</span></span>
2. <span data-ttu-id="725f5-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="725f5-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ethicspoint-incident-management-epim-from-the-gallery"></a><span data-ttu-id="725f5-123">Добавление решения EthicsPoint Incident Management (EPIM) из коллекции</span><span class="sxs-lookup"><span data-stu-id="725f5-123">Adding EthicsPoint Incident Management (EPIM) from the gallery</span></span>
<span data-ttu-id="725f5-124">Чтобы настроить интеграцию EthicsPoint Incident Management (EPIM) с Azure AD, вам потребуется добавить EthicsPoint Incident Management (EPIM) из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="725f5-124">To configure the integration of EthicsPoint Incident Management (EPIM) into Azure AD, you need to add EthicsPoint Incident Management (EPIM) from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="725f5-125">**Чтобы добавить EthicsPoint Incident Management (EPIM) из коллекции, сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="725f5-125">**To add EthicsPoint Incident Management (EPIM) from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="725f5-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="725f5-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="725f5-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="725f5-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="725f5-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="725f5-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="725f5-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="725f5-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="725f5-133">В поле поиска введите **EthicsPoint Incident Management (EPIM)**.</span><span class="sxs-lookup"><span data-stu-id="725f5-133">In the search box, type **EthicsPoint Incident Management (EPIM)**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_ethicspoint_search.png)

5. <span data-ttu-id="725f5-135">На панели результатов выберите **EthicsPoint Incident Management (EPIM)** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="725f5-135">In the results panel, select **EthicsPoint Incident Management (EPIM)**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_ethicspoint_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="725f5-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="725f5-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="725f5-138">В этом разделе описывается настройка и проверка единого входа Azure AD в EthicsPoint Incident Management (EPIM) с помощью тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="725f5-138">In this section, you configure and test Azure AD single sign-on with EthicsPoint Incident Management (EPIM) based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="725f5-139">Для работы единого входа в Azure AD необходимо указать, какой пользователь в EthicsPoint Incident Management (EPIM) соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="725f5-139">For single sign-on to work, Azure AD needs to know what the counterpart user in EthicsPoint Incident Management (EPIM) is to a user in Azure AD.</span></span> <span data-ttu-id="725f5-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в EthicsPoint Incident Management (EPIM).</span><span class="sxs-lookup"><span data-stu-id="725f5-140">In other words, a link relationship between an Azure AD user and the related user in EthicsPoint Incident Management (EPIM) needs to be established.</span></span>

<span data-ttu-id="725f5-141">Чтобы установить эту связь, следует назначить **имя пользователя** в Azure AD в качестве значения **имени пользователя** в EthicsPoint Incident Management (EPIM).</span><span class="sxs-lookup"><span data-stu-id="725f5-141">In EthicsPoint Incident Management (EPIM), assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="725f5-142">Чтобы настроить и проверить единый вход Azure AD в EthicsPoint Incident Management (EPIM), вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="725f5-142">To configure and test Azure AD single sign-on with EthicsPoint Incident Management (EPIM), you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="725f5-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="725f5-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="725f5-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="725f5-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="725f5-145">**[Создание тестового пользователя EthicsPoint Incident Management (EPIM)](#creating-a-ethicspoint-incident-management-epim-test-user)** требуется для создания пользователя Britta Simon в EthicsPoint Incident Management (EPIM), связанного с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="725f5-145">**[Creating a EthicsPoint Incident Management (EPIM) test user](#creating-a-ethicspoint-incident-management-epim-test-user)** - to have a counterpart of Britta Simon in EthicsPoint Incident Management (EPIM) that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="725f5-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="725f5-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="725f5-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="725f5-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="725f5-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="725f5-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="725f5-149">Цель этого раздела — включить единый вход Azure AD на портале Azure и настроить его в EthicsPoint Incident Management (EPIM).</span><span class="sxs-lookup"><span data-stu-id="725f5-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your EthicsPoint Incident Management (EPIM) application.</span></span>

<span data-ttu-id="725f5-150">**Чтобы настроить единый вход Azure AD в EthicsPoint Incident Management (EPIM), сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="725f5-150">**To configure Azure AD single sign-on with EthicsPoint Incident Management (EPIM), perform the following steps:**</span></span>

1. <span data-ttu-id="725f5-151">На портале Azure на странице интеграции с приложением **EthicsPoint Incident Management (EPIM)** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="725f5-151">In the Azure portal, on the **EthicsPoint Incident Management (EPIM)** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="725f5-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="725f5-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_ethicspoint_samlbase.png)

3. <span data-ttu-id="725f5-155">В разделе **Домены и URL-адреса приложения EthicsPoint Incident Management (EPIM)** выполните указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="725f5-155">On the **EthicsPoint Incident Management (EPIM) Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_ethicspoint_url.png)

    <span data-ttu-id="725f5-157">а.</span><span class="sxs-lookup"><span data-stu-id="725f5-157">a.</span></span> <span data-ttu-id="725f5-158">В текстовом поле **URL-адрес для входа** введите URL-адрес в следующем формате:</span><span class="sxs-lookup"><span data-stu-id="725f5-158">In the **Sign-on URL** textbox, type a URL using the following pattern:</span></span>
    | |
    |--|
    | `https://<companyname>.navexglobal.com`|
    | `https://<companyname>.ethicspointvp.com`|

    <span data-ttu-id="725f5-159">b.</span><span class="sxs-lookup"><span data-stu-id="725f5-159">b.</span></span> <span data-ttu-id="725f5-160">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://<companyname>.navexglobal.com/adfs/services/trust`</span><span class="sxs-lookup"><span data-stu-id="725f5-160">In the **Identifier** textbox, type a URL using the following pattern: `https://<companyname>.navexglobal.com/adfs/services/trust`</span></span>

    <span data-ttu-id="725f5-161">c.</span><span class="sxs-lookup"><span data-stu-id="725f5-161">c.</span></span> <span data-ttu-id="725f5-162">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате: `https://<servername>.navexglobal.com/adfs/ls/`.</span><span class="sxs-lookup"><span data-stu-id="725f5-162">In the **Reply URL** textbox, type a URL using the following pattern: `https://<servername>.navexglobal.com/adfs/ls/`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="725f5-163">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="725f5-163">These values are not real.</span></span> <span data-ttu-id="725f5-164">Укажите вместо них фактические значения URL-адреса ответа, идентификатора и URL-адреса входа.</span><span class="sxs-lookup"><span data-stu-id="725f5-164">Update these values with the actual Reply URL, Identifier, and Sign-On URL.</span></span> <span data-ttu-id="725f5-165">Чтобы получить эти значения, обратитесь в [службу поддержки клиентов EthicsPoint Incident Management (EPIM)](http://www.navexglobal.com/company/contact-us).</span><span class="sxs-lookup"><span data-stu-id="725f5-165">Contact [EthicsPoint Incident Management (EPIM) Client support team](http://www.navexglobal.com/company/contact-us) to get these values.</span></span> 

4. <span data-ttu-id="725f5-166">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="725f5-166">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_ethicspoint_certificate.png) 

5. <span data-ttu-id="725f5-168">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="725f5-168">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="725f5-170">Для настройки единого входа на стороне **EthicsPoint Incident Management (EPIM)** необходимо отправить скачанный **XML-файл метаданных** в [службу поддержки EthicsPoint Incident Management (EPIM)](http://www.navexglobal.com/company/contact-us).</span><span class="sxs-lookup"><span data-stu-id="725f5-170">To configure single sign-on on **EthicsPoint Incident Management (EPIM)** side, you need to send the downloaded **Metadata XML** to [EthicsPoint Incident Management (EPIM) support team](http://www.navexglobal.com/company/contact-us).</span></span>

> [!TIP]
> <span data-ttu-id="725f5-171">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="725f5-171">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="725f5-172">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="725f5-172">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="725f5-173">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="725f5-173">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="725f5-174">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="725f5-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="725f5-175">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="725f5-175">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="725f5-177">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="725f5-177">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="725f5-178">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="725f5-178">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ethicspoint-incident-management-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="725f5-180">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="725f5-180">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ethicspoint-incident-management-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="725f5-182">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="725f5-182">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ethicspoint-incident-management-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="725f5-184">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="725f5-184">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-ethicspoint-incident-management-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="725f5-186">а.</span><span class="sxs-lookup"><span data-stu-id="725f5-186">a.</span></span> <span data-ttu-id="725f5-187">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="725f5-187">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="725f5-188">b.</span><span class="sxs-lookup"><span data-stu-id="725f5-188">b.</span></span> <span data-ttu-id="725f5-189">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="725f5-189">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="725f5-190">c.</span><span class="sxs-lookup"><span data-stu-id="725f5-190">c.</span></span> <span data-ttu-id="725f5-191">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="725f5-191">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="725f5-192">d.</span><span class="sxs-lookup"><span data-stu-id="725f5-192">d.</span></span> <span data-ttu-id="725f5-193">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="725f5-193">Click **Create**.</span></span>
 
### <a name="creating-a-ethicspoint-incident-management-epim-test-user"></a><span data-ttu-id="725f5-194">Создание тестового пользователя EthicsPoint Incident Management (EPIM)</span><span class="sxs-lookup"><span data-stu-id="725f5-194">Creating a EthicsPoint Incident Management (EPIM) test user</span></span>

<span data-ttu-id="725f5-195">В этом разделе описано, как создать пользователя Britta Simon в EthicsPoint Incident Management (EPIM).</span><span class="sxs-lookup"><span data-stu-id="725f5-195">In this section, you create a user called Britta Simon in EthicsPoint Incident Management (EPIM).</span></span> <span data-ttu-id="725f5-196">Чтобы добавить пользователей на платформу EthicsPoint Incident Management (EPIM), обратитесь в [службу поддержки EthicsPoint Incident Management (EPIM)](http://www.navexglobal.com/company/contact-us).</span><span class="sxs-lookup"><span data-stu-id="725f5-196">Please work with [EthicsPoint Incident Management (EPIM) support team](http://www.navexglobal.com/company/contact-us) to add the users in the EthicsPoint Incident Management (EPIM) platform.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="725f5-197">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="725f5-197">Assigning the Azure AD test user</span></span>

<span data-ttu-id="725f5-198">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив доступ к EthicsPoint Incident Management (EPIM).</span><span class="sxs-lookup"><span data-stu-id="725f5-198">In this section, you enable Britta Simon to use Azure single sign-on by granting access to EthicsPoint Incident Management (EPIM).</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="725f5-200">**Чтобы назначить пользователя Britta Simon в EthicsPoint Incident Management (EPIM), сделайте следующее:**</span><span class="sxs-lookup"><span data-stu-id="725f5-200">**To assign Britta Simon to EthicsPoint Incident Management (EPIM), perform the following steps:**</span></span>

1. <span data-ttu-id="725f5-201">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="725f5-201">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="725f5-203">В списке приложений выберите **EthicsPoint Incident Management (EPIM)**.</span><span class="sxs-lookup"><span data-stu-id="725f5-203">In the applications list, select **EthicsPoint Incident Management (EPIM)**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_ethicspoint_app.png) 

3. <span data-ttu-id="725f5-205">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="725f5-205">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="725f5-207">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="725f5-207">Click **Add** button.</span></span> <span data-ttu-id="725f5-208">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="725f5-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="725f5-210">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="725f5-210">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="725f5-211">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="725f5-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="725f5-212">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="725f5-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="725f5-213">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="725f5-213">Testing single sign-on</span></span>

<span data-ttu-id="725f5-214">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="725f5-214">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>
<span data-ttu-id="725f5-215">Щелкнув плитку EthicsPoint Incident Management (EPIM) на панели доступа, вы автоматически войдете в приложение EthicsPoint Incident Management (EPIM).</span><span class="sxs-lookup"><span data-stu-id="725f5-215">When you click the EthicsPoint Incident Management (EPIM) tile in the Access Panel, you should get automatically signed-on to your EthicsPoint Incident Management (EPIM) application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="725f5-216">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="725f5-216">Additional resources</span></span>

* [<span data-ttu-id="725f5-217">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="725f5-217">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="725f5-218">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="725f5-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ethicspoint-incident-management-tutorial/tutorial_general_203.png

