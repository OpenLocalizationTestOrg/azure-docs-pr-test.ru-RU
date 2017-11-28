---
title: "Руководство по интеграции Azure Active Directory с O.C. Tanner — AppreciateHub | Документация Майкрософт"
description: "Узнайте, как настроить единый вход между Azure Active Directory и O.C. Tanner — AppreciateHub."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: dee8fbca-0b60-4a21-8917-1fb6919de5a0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: jeedes
ms.openlocfilehash: 9af12372b30d9ee1575e46be3b4144fc3b73ec69
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-oc-tanner---appreciatehub"></a><span data-ttu-id="a7a03-105">Руководство по интеграции Azure Active Directory с O.C.</span><span class="sxs-lookup"><span data-stu-id="a7a03-105">Tutorial: Azure Active Directory integration with O.C.</span></span> <span data-ttu-id="a7a03-106">Tanner — AppreciateHub</span><span class="sxs-lookup"><span data-stu-id="a7a03-106">Tanner - AppreciateHub</span></span>

<span data-ttu-id="a7a03-107">В этом руководстве вы узнаете, как интегрировать O.C.</span><span class="sxs-lookup"><span data-stu-id="a7a03-107">In this tutorial, you learn how to integrate O.C.</span></span> <span data-ttu-id="a7a03-108">Tanner — AppreciateHub с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a7a03-108">Tanner - AppreciateHub with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a7a03-109">Интеграция O.C.</span><span class="sxs-lookup"><span data-stu-id="a7a03-109">Integrating O.C.</span></span> <span data-ttu-id="a7a03-110">Tanner — AppreciateHub с Azure AD обеспечивает следующие преимущества.</span><span class="sxs-lookup"><span data-stu-id="a7a03-110">Tanner - AppreciateHub with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="a7a03-111">С помощью Azure AD вы можете контролировать доступ к O.C.</span><span class="sxs-lookup"><span data-stu-id="a7a03-111">You can control in Azure AD who has access to O.C.</span></span> <span data-ttu-id="a7a03-112">Tanner — AppreciateHub</span><span class="sxs-lookup"><span data-stu-id="a7a03-112">Tanner - AppreciateHub</span></span>
- <span data-ttu-id="a7a03-113">Вы можете включить автоматический вход пользователей в O.C.</span><span class="sxs-lookup"><span data-stu-id="a7a03-113">You can enable your users to automatically get signed-on to O.C.</span></span> <span data-ttu-id="a7a03-114">Tanner — AppreciateHub (единый вход) под учетной записью Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a7a03-114">Tanner - AppreciateHub (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a7a03-115">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="a7a03-115">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="a7a03-116">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a7a03-116">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a7a03-117">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="a7a03-117">Prerequisites</span></span>

<span data-ttu-id="a7a03-118">Чтобы настроить интеграцию Azure AD с O.C.</span><span class="sxs-lookup"><span data-stu-id="a7a03-118">To configure Azure AD integration with O.C.</span></span> <span data-ttu-id="a7a03-119">Tanner — AppreciateHub, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="a7a03-119">Tanner - AppreciateHub, you need the following items:</span></span>

- <span data-ttu-id="a7a03-120">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="a7a03-120">An Azure AD subscription</span></span>
- <span data-ttu-id="a7a03-121">подписка с поддержкой единого входа O.C.</span><span class="sxs-lookup"><span data-stu-id="a7a03-121">A O.C.</span></span> <span data-ttu-id="a7a03-122">подписка Tanner — AppreciateHub с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="a7a03-122">Tanner - AppreciateHub single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a7a03-123">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="a7a03-123">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a7a03-124">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="a7a03-124">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a7a03-125">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="a7a03-125">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a7a03-126">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a7a03-126">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a7a03-127">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="a7a03-127">Scenario description</span></span>
<span data-ttu-id="a7a03-128">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="a7a03-128">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a7a03-129">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="a7a03-129">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a7a03-130">Добавление O.C.</span><span class="sxs-lookup"><span data-stu-id="a7a03-130">Adding O.C.</span></span> <span data-ttu-id="a7a03-131">Tanner — AppreciateHub из коллекции</span><span class="sxs-lookup"><span data-stu-id="a7a03-131">Tanner - AppreciateHub from the gallery</span></span>
2. <span data-ttu-id="a7a03-132">Настройка и проверка единого входа в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a7a03-132">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-oc-tanner---appreciatehub-from-the-gallery"></a><span data-ttu-id="a7a03-133">Добавление O.C.</span><span class="sxs-lookup"><span data-stu-id="a7a03-133">Adding O.C.</span></span> <span data-ttu-id="a7a03-134">Tanner — AppreciateHub из коллекции</span><span class="sxs-lookup"><span data-stu-id="a7a03-134">Tanner - AppreciateHub from the gallery</span></span>
<span data-ttu-id="a7a03-135">Чтобы настроить интеграцию O.C.</span><span class="sxs-lookup"><span data-stu-id="a7a03-135">To configure the integration of O.C.</span></span> <span data-ttu-id="a7a03-136">Tanner — AppreciateHub с Azure AD, необходимо добавить O.C.</span><span class="sxs-lookup"><span data-stu-id="a7a03-136">Tanner - AppreciateHub into Azure AD, you need to add O.C.</span></span> <span data-ttu-id="a7a03-137">Tanner — AppreciateHub из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="a7a03-137">Tanner - AppreciateHub from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="a7a03-138">**Чтобы добавить O.C. Tanner — AppreciateHub из коллекции, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="a7a03-138">**To add O.C. Tanner - AppreciateHub from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="a7a03-139">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a7a03-139">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a7a03-141">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="a7a03-141">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="a7a03-142">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="a7a03-142">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="a7a03-144">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="a7a03-144">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="a7a03-146">В поле поиска введите **O.C. Tanner — AppreciateHub**.</span><span class="sxs-lookup"><span data-stu-id="a7a03-146">In the search box, type **O.C. Tanner - AppreciateHub**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_search.png)

5. <span data-ttu-id="a7a03-148">На панели результатов выберите **O.C. Tanner — AppreciateHub** и нажмите кнопку **Добавить**, чтобы добавить приложение.</span><span class="sxs-lookup"><span data-stu-id="a7a03-148">In the results panel, select **O.C. Tanner - AppreciateHub**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a7a03-150">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="a7a03-150">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a7a03-151">В этом разделе описана настройка и проверка единого входа Azure AD в приложение O.C.</span><span class="sxs-lookup"><span data-stu-id="a7a03-151">In this section, you configure and test Azure AD single sign-on with O.C.</span></span> <span data-ttu-id="a7a03-152">Tanner — AppreciateHub с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a7a03-152">Tanner - AppreciateHub based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a7a03-153">Для работы единого входа в Azure AD необходимо знать, какой пользователь в O.C.</span><span class="sxs-lookup"><span data-stu-id="a7a03-153">For single sign-on to work, Azure AD needs to know what the counterpart user in O.C.</span></span> <span data-ttu-id="a7a03-154">Tanner — AppreciateHub соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a7a03-154">Tanner - AppreciateHub is to a user in Azure AD.</span></span> <span data-ttu-id="a7a03-155">Иными словами, необходимо установить связь между пользователям Azure AD и соответствующим пользователем в O.C.</span><span class="sxs-lookup"><span data-stu-id="a7a03-155">In other words, a link relationship between an Azure AD user and the related user in O.C.</span></span> <span data-ttu-id="a7a03-156">Необходимо установить связь Tanner — AppreciateHub.</span><span class="sxs-lookup"><span data-stu-id="a7a03-156">Tanner - AppreciateHub needs to be established.</span></span>

<span data-ttu-id="a7a03-157">В O.C.</span><span class="sxs-lookup"><span data-stu-id="a7a03-157">In O.C.</span></span> <span data-ttu-id="a7a03-158">Tanner —AppreciateHub назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя**, чтобы установить эту связь.</span><span class="sxs-lookup"><span data-stu-id="a7a03-158">Tanner - AppreciateHub, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="a7a03-159">Чтобы настроить и проверить единый вход Azure AD в O.C.</span><span class="sxs-lookup"><span data-stu-id="a7a03-159">To configure and test Azure AD single sign-on with O.C.</span></span> <span data-ttu-id="a7a03-160">Tanner — AppreciateHub, вам потребуется выполнить действия в следующих стандартных блоках:</span><span class="sxs-lookup"><span data-stu-id="a7a03-160">Tanner - AppreciateHub, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="a7a03-161">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="a7a03-161">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="a7a03-162">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a7a03-162">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a7a03-163">**[Создание тестового пользователя O.C. Tanner — AppreciateHub](#creating-a-oc-tanner---appreciatehub-test-user)** требуется для создания пользователя Britta Simon в O.C.</span><span class="sxs-lookup"><span data-stu-id="a7a03-163">**[Creating a O.C. Tanner - AppreciateHub test user](#creating-a-oc-tanner---appreciatehub-test-user)** - to have a counterpart of Britta Simon in O.C.</span></span> <span data-ttu-id="a7a03-164">Tanner — AppreciateHub, связанного с соответствующим представлением в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a7a03-164">Tanner - AppreciateHub that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="a7a03-165">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a7a03-165">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a7a03-166">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="a7a03-166">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a7a03-167">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="a7a03-167">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a7a03-168">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в O.C.</span><span class="sxs-lookup"><span data-stu-id="a7a03-168">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your O.C.</span></span> <span data-ttu-id="a7a03-169">Tanner — AppreciateHub.</span><span class="sxs-lookup"><span data-stu-id="a7a03-169">Tanner - AppreciateHub application.</span></span>

<span data-ttu-id="a7a03-170">**Чтобы настроить единый вход Azure AD в O.C. Tanner — AppreciateHub, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="a7a03-170">**To configure Azure AD single sign-on with O.C. Tanner - AppreciateHub, perform the following steps:**</span></span>

1. <span data-ttu-id="a7a03-171">На портале Azure на странице интеграции с приложением **O.C. Tanner — AppreciateHub** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="a7a03-171">In the Azure portal, on the **O.C. Tanner - AppreciateHub** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="a7a03-173">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="a7a03-173">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_samlbase.png)

3. <span data-ttu-id="a7a03-175">В разделе **Домены и URL-адреса приложения O.C. Tanner — AppreciateHub** сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="a7a03-175">On the **O.C. Tanner - AppreciateHub Domain and URLs** section, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_url.png)

    <span data-ttu-id="a7a03-177">а.</span><span class="sxs-lookup"><span data-stu-id="a7a03-177">a.</span></span> <span data-ttu-id="a7a03-178">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате: `https://<companyname>.appreciatehub.com/fed/sp/authnResponse20`.</span><span class="sxs-lookup"><span data-stu-id="a7a03-178">In the **Reply URL** textbox, type a URL using the following pattern: `https://<companyname>.appreciatehub.com/fed/sp/authnResponse20`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a7a03-179">Это значение приведено для справки.</span><span class="sxs-lookup"><span data-stu-id="a7a03-179">This value is not real.</span></span> <span data-ttu-id="a7a03-180">Вместо него нужно указать фактический URL-адрес ответа.</span><span class="sxs-lookup"><span data-stu-id="a7a03-180">Update this value with the actual Reply URL.</span></span> <span data-ttu-id="a7a03-181">Обратитесь в [службу поддержки O.C. Tanner — AppreciateHub](mailto:sso@octanner.com), чтобы получить это значение.</span><span class="sxs-lookup"><span data-stu-id="a7a03-181">Contact [O.C. Tanner - AppreciateHub support team](mailto:sso@octanner.com) to get this value.</span></span>

    <span data-ttu-id="a7a03-182">b.</span><span class="sxs-lookup"><span data-stu-id="a7a03-182">b.</span></span> <span data-ttu-id="a7a03-183">Откройте файл метаданных, используя следующую ссылку: [https://fed.appreciatehub.com/fed/sp/metadata](https://fed.appreciatehub.com/fed/sp/metadata).</span><span class="sxs-lookup"><span data-stu-id="a7a03-183">Open the metadata file using the following link: [https://fed.appreciatehub.com/fed/sp/metadata](https://fed.appreciatehub.com/fed/sp/metadata).</span></span>
   
    <span data-ttu-id="a7a03-184">c.</span><span class="sxs-lookup"><span data-stu-id="a7a03-184">c.</span></span> <span data-ttu-id="a7a03-185">Найдите узел **md:AssertionConsumerService** .</span><span class="sxs-lookup"><span data-stu-id="a7a03-185">Locate the **md:AssertionConsumerService** node.</span></span> 
   
    <span data-ttu-id="a7a03-186">г)</span><span class="sxs-lookup"><span data-stu-id="a7a03-186">d.</span></span> <span data-ttu-id="a7a03-187">Скопируйте значение атрибута **Location**.</span><span class="sxs-lookup"><span data-stu-id="a7a03-187">Copy the value of the **Location** attribute.</span></span> 
   
    ![Настройка параметров приложения][12]
   
    <span data-ttu-id="a7a03-189">д.</span><span class="sxs-lookup"><span data-stu-id="a7a03-189">e.</span></span> <span data-ttu-id="a7a03-190">Вставьте значение, полученное на предыдущем шаге, в текстовом поле **URL-адрес для входа**.</span><span class="sxs-lookup"><span data-stu-id="a7a03-190">In the **Sign On URL** textbox, past the value you have obtained in the previous step.</span></span>

4. <span data-ttu-id="a7a03-191">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="a7a03-191">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_certificate.png) 

5. <span data-ttu-id="a7a03-193">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="a7a03-193">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a7a03-195">Чтобы настроить единый вход на стороне приложения **O.C. Tanner — AppreciateHub**, необходимо отправить скачанный **XML-файл метаданных** [ службе поддержки О.С. Tanner — AppreciateHub](mailto:sso@octanner.com).</span><span class="sxs-lookup"><span data-stu-id="a7a03-195">To configure single sign-on on **O.C. Tanner - AppreciateHub** side, you need to send the downloaded **Metadata XML** to [O.C. Tanner - AppreciateHub support team](mailto:sso@octanner.com).</span></span>

> [!TIP]
> <span data-ttu-id="a7a03-196">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="a7a03-196">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="a7a03-197">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="a7a03-197">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="a7a03-198">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="a7a03-198">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a7a03-199">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="a7a03-199">Creating an Azure AD test user</span></span>
<span data-ttu-id="a7a03-200">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a7a03-200">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="a7a03-202">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="a7a03-202">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="a7a03-203">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a7a03-203">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a7a03-205">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="a7a03-205">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a7a03-207">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="a7a03-207">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a7a03-209">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="a7a03-209">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-oc-tanner-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a7a03-211">а.</span><span class="sxs-lookup"><span data-stu-id="a7a03-211">a.</span></span> <span data-ttu-id="a7a03-212">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a7a03-212">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a7a03-213">b.</span><span class="sxs-lookup"><span data-stu-id="a7a03-213">b.</span></span> <span data-ttu-id="a7a03-214">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a7a03-214">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a7a03-215">c.</span><span class="sxs-lookup"><span data-stu-id="a7a03-215">c.</span></span> <span data-ttu-id="a7a03-216">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="a7a03-216">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="a7a03-217">d.</span><span class="sxs-lookup"><span data-stu-id="a7a03-217">d.</span></span> <span data-ttu-id="a7a03-218">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="a7a03-218">Click **Create**.</span></span>
 
### <a name="creating-a-oc-tanner---appreciatehub-test-user"></a><span data-ttu-id="a7a03-219">Создание тестового пользователя O.C.</span><span class="sxs-lookup"><span data-stu-id="a7a03-219">Creating a O.C.</span></span> <span data-ttu-id="a7a03-220">Tanner — AppreciateHub</span><span class="sxs-lookup"><span data-stu-id="a7a03-220">Tanner - AppreciateHub test user</span></span>

<span data-ttu-id="a7a03-221">Цель этого раздела — создать пользователя с именем Britta Simon в O.C.</span><span class="sxs-lookup"><span data-stu-id="a7a03-221">The objective of this section is to create a user called Britta Simon in O.C.</span></span> <span data-ttu-id="a7a03-222">Tanner — AppreciateHub.</span><span class="sxs-lookup"><span data-stu-id="a7a03-222">Tanner - AppreciateHub.</span></span>

<span data-ttu-id="a7a03-223">**Чтобы создать пользователя с именем Britta Simon в O.C. Tanner — AppreciateHub, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="a7a03-223">**To create a user called Britta Simon in O.C. Tanner - AppreciateHub, perform the following steps:**</span></span>

<span data-ttu-id="a7a03-224">Попросите [службу поддержки O.C. Tanner — AppreciateHub](mailto:sso@octanner.com) создать пользователя, у которого значение атрибута nameID совпадает с именем пользователя Britta Simon в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a7a03-224">Ask your [O.C. Tanner - AppreciateHub support team](mailto:sso@octanner.com) to create a user that has as nameID attribute the same value as the user name of Britta Simon in Azure AD.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="a7a03-225">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="a7a03-225">Assigning the Azure AD test user</span></span>

<span data-ttu-id="a7a03-226">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure путем предоставления доступа к O.C.</span><span class="sxs-lookup"><span data-stu-id="a7a03-226">In this section, you enable Britta Simon to use Azure single sign-on by granting access to O.C.</span></span> <span data-ttu-id="a7a03-227">Tanner — AppreciateHub.</span><span class="sxs-lookup"><span data-stu-id="a7a03-227">Tanner - AppreciateHub.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="a7a03-229">**Чтобы назначить пользователя Britta Simon в O.C. Tanner — AppreciateHub, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="a7a03-229">**To assign Britta Simon to O.C. Tanner - AppreciateHub, perform the following steps:**</span></span>

1. <span data-ttu-id="a7a03-230">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="a7a03-230">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="a7a03-232">В списке приложений выберите **O.C. Tanner — AppreciateHub**.</span><span class="sxs-lookup"><span data-stu-id="a7a03-232">In the applications list, select **O.C. Tanner - AppreciateHub**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-oc-tanner-tutorial/tutorial_octannerappreciatehub_app.png) 

3. <span data-ttu-id="a7a03-234">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="a7a03-234">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="a7a03-236">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="a7a03-236">Click **Add** button.</span></span> <span data-ttu-id="a7a03-237">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="a7a03-237">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="a7a03-239">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="a7a03-239">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="a7a03-240">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="a7a03-240">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a7a03-241">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="a7a03-241">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a7a03-242">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="a7a03-242">Testing single sign-on</span></span>

<span data-ttu-id="a7a03-243">Цель этого раздела — проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="a7a03-243">The objective of this section is to test your Azure AD single sign-on configuration using the Access Panel.</span></span>  
<span data-ttu-id="a7a03-244">Щелкнув плитку O.C.</span><span class="sxs-lookup"><span data-stu-id="a7a03-244">When you click the O.C.</span></span> <span data-ttu-id="a7a03-245">Tanner — AppreciateHub на панели доступа, вы автоматически войдете в приложение O.C.</span><span class="sxs-lookup"><span data-stu-id="a7a03-245">Tanner - AppreciateHub tile in the Access Panel, you should get automatically signed-on to your O.C.</span></span> <span data-ttu-id="a7a03-246">Tanner — AppreciateHub.</span><span class="sxs-lookup"><span data-stu-id="a7a03-246">Tanner - AppreciateHub application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a7a03-247">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="a7a03-247">Additional resources</span></span>

* [<span data-ttu-id="a7a03-248">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a7a03-248">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a7a03-249">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="a7a03-249">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_04.png

[12]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_octanner_08.png

[100]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-oc-tanner-tutorial/tutorial_general_203.png

