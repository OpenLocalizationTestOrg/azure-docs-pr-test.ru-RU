---
title: "Руководство по интеграции Azure Active Directory с 123ContactForm | Документация Майкрософт"
description: "Узнайте, как настроить единый вход Azure Active Directory в приложении 123ContactForm."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5211910a-ab96-4709-959a-524c4d57c43e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 3a99f0841c3e0d973168991f5dbee40e54c1d054
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-azure-active-directory-integration-with-123contactform"></a><span data-ttu-id="f9543-103">Руководство по интеграции Azure Active Directory с 123ContactForm</span><span class="sxs-lookup"><span data-stu-id="f9543-103">Tutorial: Azure Active Directory integration with 123ContactForm</span></span>

<span data-ttu-id="f9543-104">В этом руководстве описано, как интегрировать 123ContactForm с Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f9543-104">In this tutorial, you learn how to integrate 123ContactForm with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f9543-105">Интеграция 123ContactForm с Azure AD обеспечивает следующие преимущества:</span><span class="sxs-lookup"><span data-stu-id="f9543-105">Integrating 123ContactForm with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="f9543-106">С помощью Azure AD вы можете контролировать доступ к 123ContactForm.</span><span class="sxs-lookup"><span data-stu-id="f9543-106">You can control in Azure AD who has access to 123ContactForm</span></span>
- <span data-ttu-id="f9543-107">Вы можете включить автоматический вход пользователей в 123ContactForm (единый вход) с использованием учетной записи Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f9543-107">You can enable your users to automatically get signed-on to 123ContactForm (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f9543-108">Вы можете управлять учетными записями централизованно — через портал Azure.</span><span class="sxs-lookup"><span data-stu-id="f9543-108">You can manage your accounts in one central location - the Azure portal</span></span>

<span data-ttu-id="f9543-109">Подробнее узнать об интеграции приложений SaaS с Azure AD можно в разделе [Что такое доступ к приложениям и единый вход с помощью Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f9543-109">If you want to know more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f9543-110">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="f9543-110">Prerequisites</span></span>

<span data-ttu-id="f9543-111">Чтобы настроить интеграцию Azure AD с 123ContactForm, вам потребуется:</span><span class="sxs-lookup"><span data-stu-id="f9543-111">To configure Azure AD integration with 123ContactForm, you need the following items:</span></span>

- <span data-ttu-id="f9543-112">подписка Azure AD;</span><span class="sxs-lookup"><span data-stu-id="f9543-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f9543-113">подписка 123ContactForm с поддержкой единого входа.</span><span class="sxs-lookup"><span data-stu-id="f9543-113">A 123ContactForm single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f9543-114">Мы не рекомендуем использовать рабочую среду для проверки действий в этом учебнике.</span><span class="sxs-lookup"><span data-stu-id="f9543-114">To test the steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f9543-115">При проверке действий в этом учебнике соблюдайте следующие рекомендации:</span><span class="sxs-lookup"><span data-stu-id="f9543-115">To test the steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f9543-116">Не используйте рабочую среду без необходимости.</span><span class="sxs-lookup"><span data-stu-id="f9543-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f9543-117">Если у вас нет пробной среды Azure AD, вы можете получить пробную версию на один месяц по [этой ссылке](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f9543-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f9543-118">Описание сценария</span><span class="sxs-lookup"><span data-stu-id="f9543-118">Scenario description</span></span>
<span data-ttu-id="f9543-119">В рамках этого руководства проводится проверка единого входа Azure AD в тестовой среде.</span><span class="sxs-lookup"><span data-stu-id="f9543-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f9543-120">Сценарий, описанный в этом учебнике, состоит из двух основных блоков:</span><span class="sxs-lookup"><span data-stu-id="f9543-120">The scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f9543-121">Добавление 123ContactForm из коллекции</span><span class="sxs-lookup"><span data-stu-id="f9543-121">Adding 123ContactForm from the gallery</span></span>
2. <span data-ttu-id="f9543-122">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="f9543-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-123contactform-from-the-gallery"></a><span data-ttu-id="f9543-123">Добавление 123ContactForm из коллекции</span><span class="sxs-lookup"><span data-stu-id="f9543-123">Adding 123ContactForm from the gallery</span></span>
<span data-ttu-id="f9543-124">Чтобы настроить интеграцию 123ContactForm с Azure AD, необходимо добавить 123ContactForm из коллекции в список управляемых приложений SaaS.</span><span class="sxs-lookup"><span data-stu-id="f9543-124">To configure the integration of 123ContactForm into Azure AD, you need to add 123ContactForm from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="f9543-125">**Чтобы добавить 123ContactForm из коллекции, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="f9543-125">**To add 123ContactForm from the gallery, perform the following steps:**</span></span>

1. <span data-ttu-id="f9543-126">На **[портале Azure](https://portal.azure.com)** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f9543-126">In the **[Azure portal](https://portal.azure.com)**, on the left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f9543-128">Перейдите к разделу **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="f9543-128">Navigate to **Enterprise applications**.</span></span> <span data-ttu-id="f9543-129">Затем выберите **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="f9543-129">Then go to **All applications**.</span></span>

    ![Приложения][2]
    
3. <span data-ttu-id="f9543-131">Чтобы добавить новое приложение, в верхней части диалогового окна нажмите кнопку **Создать приложение**.</span><span class="sxs-lookup"><span data-stu-id="f9543-131">To add new application, click **New application** button on the top of dialog.</span></span>

    ![Приложения][3]

4. <span data-ttu-id="f9543-133">В поле поиска введите **123ContactForm**.</span><span class="sxs-lookup"><span data-stu-id="f9543-133">In the search box, type **123ContactForm**.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_search.png)

5. <span data-ttu-id="f9543-135">На панели результатов выберите **123ContactForm** и нажмите кнопку **Добавить**, чтобы добавить это приложение.</span><span class="sxs-lookup"><span data-stu-id="f9543-135">In the results panel, select **123ContactForm**, and then click **Add** button to add the application.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f9543-137">Настройка и проверка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="f9543-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f9543-138">В этом разделе описана настройка и проверка единого входа Azure AD в 123ContactForm с использованием тестового пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f9543-138">In this section, you configure and test Azure AD single sign-on with 123ContactForm based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f9543-139">Для работы единого входа в Azure AD необходимо знать, какой пользователь в 123ContactForm соответствует пользователю в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f9543-139">For single sign-on to work, Azure AD needs to know what the counterpart user in 123ContactForm is to a user in Azure AD.</span></span> <span data-ttu-id="f9543-140">Иными словами, необходимо установить связь между пользователем Azure AD и соответствующим пользователем в 123ContactForm.</span><span class="sxs-lookup"><span data-stu-id="f9543-140">In other words, a link relationship between an Azure AD user and the related user in 123ContactForm needs to be established.</span></span>

<span data-ttu-id="f9543-141">Чтобы установить эту связь, назначьте **имя пользователя** в Azure AD в качестве значения **имени пользователя** в 123ContactForm.</span><span class="sxs-lookup"><span data-stu-id="f9543-141">In 123ContactForm, assign the value of the **user name** in Azure AD as the value of the **Username** to establish the link relationship.</span></span>

<span data-ttu-id="f9543-142">Чтобы настроить и проверить единый вход Azure AD в 123ContactForm, вам потребуется выполнить действия в следующих стандартных блоках.</span><span class="sxs-lookup"><span data-stu-id="f9543-142">To configure and test Azure AD single sign-on with 123ContactForm, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="f9543-143">**[Настройка единого входа в Azure AD](#configuring-azure-ad-single-sign-on)** необходима, чтобы пользователи могли использовать эту функцию.</span><span class="sxs-lookup"><span data-stu-id="f9543-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - to enable your users to use this feature.</span></span>
2. <span data-ttu-id="f9543-144">**[Создание тестового пользователя Azure AD](#creating-an-azure-ad-test-user)** требуется для проверки работы единого входа Azure AD от имени пользователя Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f9543-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - to test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f9543-145">**[Создание тестового пользователя 123ContactForm](#creating-a-123contactform-test-user)** нужно для того, чтобы в 123ContactForm также существовал пользователь Britta Simon, связанный с одноименным пользователем в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f9543-145">**[Creating a 123ContactForm test user](#creating-a-123contactform-test-user)** - to have a counterpart of Britta Simon in 123ContactForm that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="f9543-146">**[Назначение тестового пользователя Azure AD](#assigning-the-azure-ad-test-user)** необходимо, чтобы позволить Britta Simon использовать единый вход в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f9543-146">**[Assigning the Azure AD test user](#assigning-the-azure-ad-test-user)** - to enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f9543-147">**[Testing Single Sign-On](#testing-single-sign-on)** необходима, чтобы убедиться в корректной работе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="f9543-147">**[Testing Single Sign-On](#testing-single-sign-on)** - to verify whether the configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f9543-148">Настройка единого входа в Azure AD</span><span class="sxs-lookup"><span data-stu-id="f9543-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f9543-149">В этом разделе описано, как включить единый вход Azure AD на портале Azure и настроить его в приложении 123ContactForm.</span><span class="sxs-lookup"><span data-stu-id="f9543-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your 123ContactForm application.</span></span>

<span data-ttu-id="f9543-150">**Чтобы настроить единый вход Azure AD в 123ContactForm, выполните следующие действия.**</span><span class="sxs-lookup"><span data-stu-id="f9543-150">**To configure Azure AD single sign-on with 123ContactForm, perform the following steps:**</span></span>

1. <span data-ttu-id="f9543-151">На портале Azure на странице интеграции с приложением **123ContactForm** щелкните **Единый вход**.</span><span class="sxs-lookup"><span data-stu-id="f9543-151">In the Azure portal, on the **123ContactForm** application integration page, click **Single sign-on**.</span></span>

    ![Настройка единого входа][4]

2. <span data-ttu-id="f9543-153">В диалоговом окне **Единый вход** в разделе **Режим** выберите **Вход на основе SAML**, чтобы включить функцию единого входа.</span><span class="sxs-lookup"><span data-stu-id="f9543-153">On the **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** to enable single sign-on.</span></span>
 
    ![Настройка единого входа](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_samlbase.png)

3. <span data-ttu-id="f9543-155">Если вы хотите настроить приложение в **режиме, инициируемом IdP**, то в разделе **Домены и URL-адреса приложения 123ContactForm** сделайте следующее.</span><span class="sxs-lookup"><span data-stu-id="f9543-155">On the **123ContactForm Domain and URLs** section, If you wish to configure the application in **IDP initiated mode**, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-123contactform-tutorial/url1.png)

    <span data-ttu-id="f9543-157">а.</span><span class="sxs-lookup"><span data-stu-id="f9543-157">a.</span></span> <span data-ttu-id="f9543-158">В текстовом поле **Идентификатор** введите URL-адрес в следующем формате: `https://www.123contactform.com/saml/azure_ad/<tenant_id>/metadata`</span><span class="sxs-lookup"><span data-stu-id="f9543-158">In the **Identifier** textbox, type a URL using the following pattern: `https://www.123contactform.com/saml/azure_ad/<tenant_id>/metadata`</span></span>

    <span data-ttu-id="f9543-159">b.</span><span class="sxs-lookup"><span data-stu-id="f9543-159">b.</span></span> <span data-ttu-id="f9543-160">В текстовом поле **URL-адрес ответа** введите URL-адрес в следующем формате: `https://www.123contactform.com/saml/azure_ad/<tenant_id>/acs`.</span><span class="sxs-lookup"><span data-stu-id="f9543-160">In the **Reply URL** textbox, type a URL using the following pattern: `https://www.123contactform.com/saml/azure_ad/<tenant_id>/acs`</span></span>

4. <span data-ttu-id="f9543-161">Если вы хотите настроить приложение в **режиме, инициируемом поставщиком услуг**, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="f9543-161">If you wish to configure the application in **SP initiated mode**, perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-123contactform-tutorial/url2.png)

    <span data-ttu-id="f9543-163">а.</span><span class="sxs-lookup"><span data-stu-id="f9543-163">a.</span></span> <span data-ttu-id="f9543-164">Щелкните параметр **Показать дополнительные параметры URL-адресов**.</span><span class="sxs-lookup"><span data-stu-id="f9543-164">Click the **Show advanced URL settings** option</span></span>

    <span data-ttu-id="f9543-165">b.</span><span class="sxs-lookup"><span data-stu-id="f9543-165">b.</span></span> <span data-ttu-id="f9543-166">В текстовом поле **URL-адрес для входа** введите следующий URL-адрес: `https://www.123contactform.com/saml/azure_ad/<tenant_id>/sso`.</span><span class="sxs-lookup"><span data-stu-id="f9543-166">In the **Sign On URL** textbox, type a URL as: `https://www.123contactform.com/saml/azure_ad/<tenant_id>/sso`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f9543-167">Эти значения приведены в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="f9543-167">These values are not real.</span></span> <span data-ttu-id="f9543-168">Необходимо будет обновить эти значения, указав фактические URL-адреса и идентификатор. Это описывается далее в этом руководстве.</span><span class="sxs-lookup"><span data-stu-id="f9543-168">You'll need to update these value from actual URLs and Identifier which is explained later in the tutorial.</span></span>
    
5. <span data-ttu-id="f9543-169">В разделе **Сертификат подписи SAML** щелкните **Metadata XML** (Метаданные XML) и сохраните файл метаданных на компьютере.</span><span class="sxs-lookup"><span data-stu-id="f9543-169">On the **SAML Signing Certificate** section, click **Metadata XML** and then save the metadata file on your computer.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_certificate.png) 

6. <span data-ttu-id="f9543-171">Нажмите кнопку **Сохранить** .</span><span class="sxs-lookup"><span data-stu-id="f9543-171">Click **Save** button.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-123contactform-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="f9543-173">Чтобы настроить единый вход на стороне **123ContactForm**, перейдите по адресу [https://www.123contactform.com/form-2709121/](https://www.123contactform.com/form-2709121/) и выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="f9543-173">To configure single sign-on on **123ContactForm** side, go to [https://www.123contactform.com/form-2709121/](https://www.123contactform.com/form-2709121/) and perform the following steps:</span></span>

    ![Настройка единого входа](./media/active-directory-saas-123contactform-tutorial/submit.png) 

    <span data-ttu-id="f9543-175">а.</span><span class="sxs-lookup"><span data-stu-id="f9543-175">a.</span></span> <span data-ttu-id="f9543-176">В текстовое поле **Email** (Адрес электронной почты) введите адрес электронной почты пользователя, например</span><span class="sxs-lookup"><span data-stu-id="f9543-176">In the **Email** textbox, type the email of the user i.e</span></span> <span data-ttu-id="f9543-177">**BrittaSimon@Contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="f9543-177">**BrittaSimon@Contoso.com**.</span></span>

    <span data-ttu-id="f9543-178">b.</span><span class="sxs-lookup"><span data-stu-id="f9543-178">b.</span></span> <span data-ttu-id="f9543-179">Щелкните **Upload** (Передать) и выберите XML-файл метаданных, скачанный с портала Azure.</span><span class="sxs-lookup"><span data-stu-id="f9543-179">Click **Upload** and browse the Metadata XML file, which you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="f9543-180">c.</span><span class="sxs-lookup"><span data-stu-id="f9543-180">c.</span></span> <span data-ttu-id="f9543-181">Щелкните **SUBMIT FORM** (Отправить форму).</span><span class="sxs-lookup"><span data-stu-id="f9543-181">Click **SUBMIT FORM**.</span></span>

8. <span data-ttu-id="f9543-182">На странице **Microsoft Azure AD - Single sign-on - Configure App Settings** (Microsoft Azure AD — единый вход — настройка параметров приложения) выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="f9543-182">On the **Microsoft Azure AD - Single sign-on - Configure App Settings** perform the following steps:</span></span>
    
    ![Настройка единого входа](./media/active-directory-saas-123contactform-tutorial/url3.png)

    <span data-ttu-id="f9543-184">а.</span><span class="sxs-lookup"><span data-stu-id="f9543-184">a.</span></span> <span data-ttu-id="f9543-185">Если вы хотите настроить приложение в **режиме, инициируемом IdP**, скопируйте значение **IDENTIFIER** (Идентификатор) для своего экземпляра и вставьте его в текстовое поле **Идентификатор** в разделе **Домены и URL-адреса приложения 123ContactForm** на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="f9543-185">If you wish to configure the application in **IDP initiated mode**, copy the **IDENTIFIER** value for your instance and paste it in **Identifier** textbox in **123ContactForm Domain and URLs** section on Azure portal.</span></span>
    
    <span data-ttu-id="f9543-186">b.</span><span class="sxs-lookup"><span data-stu-id="f9543-186">b.</span></span> <span data-ttu-id="f9543-187">Если вы хотите настроить приложение в **режиме, инициируемом IdP**, скопируйте значение **REPLY URL** (URL-адрес ответа) для своего экземпляра и вставьте его в текстовое поле **URL-адрес ответа** в разделе **Домены и URL-адреса приложения 123ContactForm** на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="f9543-187">If you wish to configure the application in **IDP initiated mode**, copy the **REPLY URL** value for your instance and paste it in **Reply URL** textbox in **123ContactForm Domain and URLs** section on Azure portal.</span></span>

    <span data-ttu-id="f9543-188">c.</span><span class="sxs-lookup"><span data-stu-id="f9543-188">c.</span></span> <span data-ttu-id="f9543-189">Если вы хотите настроить приложение в **режиме, инициируемом поставщиком услуг**, скопируйте значение **SIGN ON URL** (URL-адрес для входа) для своего экземпляра и вставьте его в текстовое поле **URL-адрес для входа** в разделе **Домены и URL-адреса приложения 123ContactForm** на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="f9543-189">If you wish to configure the application in **SP initiated mode**, copy the **SIGN ON URL** value for your instance and paste it in **Sign On URL** textbox in **123ContactForm Domain and URLs** section on Azure portal.</span></span>

> [!TIP]
> <span data-ttu-id="f9543-190">Краткую версию этих инструкций теперь можно также прочитать на [портале Azure](https://portal.azure.com) во время настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="f9543-190">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="f9543-191">После добавления этого приложения из раздела **Active Directory > Корпоративные приложения** просто выберите вкладку **Единый вход** и откройте встроенную документацию через раздел **Настройка** в нижней части страницы.</span><span class="sxs-lookup"><span data-stu-id="f9543-191">After adding this app from the **Active Directory > Enterprise Applications** section, simply click the **Single Sign-On** tab and access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="f9543-192">Дополнительные сведения о встроенной документации см. в разделе [Встроенная документация Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="f9543-192">You can read more about the embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f9543-193">Создание тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="f9543-193">Creating an Azure AD test user</span></span>
<span data-ttu-id="f9543-194">Цель этого раздела — создать на портале Azure тестового пользователя с именем Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f9543-194">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Создание пользователя Azure AD][100]

<span data-ttu-id="f9543-196">**Чтобы создать тестового пользователя в Azure AD, выполните следующие действия:**</span><span class="sxs-lookup"><span data-stu-id="f9543-196">**To create a test user in Azure AD, perform the following steps:**</span></span>

1. <span data-ttu-id="f9543-197">На **портале Azure** в области навигации слева щелкните значок **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f9543-197">In the **Azure portal**, on the left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-123contactform-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f9543-199">Чтобы отобразить список пользователей, перейдите в раздел **Пользователи и группы** и щелкните **Все пользователи**.</span><span class="sxs-lookup"><span data-stu-id="f9543-199">To display the list of users, go to **Users and groups** and click **All users**.</span></span>
    
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-123contactform-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f9543-201">Чтобы открыть диалоговое окно **Пользователь**, в верхней части диалогового окна щелкните **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="f9543-201">To open the **User** dialog, click **Add** on the top of the dialog.</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-123contactform-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f9543-203">На странице диалогового окна **Пользователь** выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="f9543-203">On the **User** dialog page, perform the following steps:</span></span>
 
    ![Создание тестового пользователя Azure AD](./media/active-directory-saas-123contactform-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f9543-205">а.</span><span class="sxs-lookup"><span data-stu-id="f9543-205">a.</span></span> <span data-ttu-id="f9543-206">В текстовом поле **Имя** введите **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f9543-206">In the **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f9543-207">b.</span><span class="sxs-lookup"><span data-stu-id="f9543-207">b.</span></span> <span data-ttu-id="f9543-208">В текстовом поле **Имя пользователя** введите **адрес электронной почты** учетной записи BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="f9543-208">In the **User name** textbox, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="f9543-209">c.</span><span class="sxs-lookup"><span data-stu-id="f9543-209">c.</span></span> <span data-ttu-id="f9543-210">Выберите **Показать пароль** и запишите значение поля **Пароль**.</span><span class="sxs-lookup"><span data-stu-id="f9543-210">Select **Show Password** and write down the value of the **Password**.</span></span>

    <span data-ttu-id="f9543-211">d.</span><span class="sxs-lookup"><span data-stu-id="f9543-211">d.</span></span> <span data-ttu-id="f9543-212">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="f9543-212">Click **Create**.</span></span>
 
### <a name="creating-a-123contactform-test-user"></a><span data-ttu-id="f9543-213">Создание тестового пользователя 123ContactForm</span><span class="sxs-lookup"><span data-stu-id="f9543-213">Creating a 123ContactForm test user</span></span>

<span data-ttu-id="f9543-214">Приложение поддерживает JIT-подготовку пользователей, поэтому после проверки подлинности пользователи будут созданы в приложении автоматически.</span><span class="sxs-lookup"><span data-stu-id="f9543-214">Application supports Just in time user provisioning and after authentication users will be created in the application automatically.</span></span>

### <a name="assigning-the-azure-ad-test-user"></a><span data-ttu-id="f9543-215">Назначение тестового пользователя Azure AD</span><span class="sxs-lookup"><span data-stu-id="f9543-215">Assigning the Azure AD test user</span></span>

<span data-ttu-id="f9543-216">В этом разделе описано, как разрешить пользователю Britta Simon использовать единый вход Azure, предоставив этому пользователю доступ к 123ContactForm.</span><span class="sxs-lookup"><span data-stu-id="f9543-216">In this section, you enable Britta Simon to use Azure single sign-on by granting access to 123ContactForm.</span></span>

![Назначение пользователя][200] 

<span data-ttu-id="f9543-218">**Чтобы назначить пользователя Britta Simon в 123ContactForm, сделайте следующее.**</span><span class="sxs-lookup"><span data-stu-id="f9543-218">**To assign Britta Simon to 123ContactForm, perform the following steps:**</span></span>

1. <span data-ttu-id="f9543-219">На портале Azure откройте представление приложений, перейдите к представлению каталога, а затем выберите **Корпоративные приложения** и щелкните **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="f9543-219">In the Azure portal, open the applications view, and then navigate to the directory view and go to **Enterprise applications** then click **All applications**.</span></span>

    ![Назначение пользователя][201] 

2. <span data-ttu-id="f9543-221">Из списка приложений выберите **123ContactForm**.</span><span class="sxs-lookup"><span data-stu-id="f9543-221">In the applications list, select **123ContactForm**.</span></span>

    ![Настройка единого входа](./media/active-directory-saas-123contactform-tutorial/tutorial_123contactform_app.png) 

3. <span data-ttu-id="f9543-223">В меню слева выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="f9543-223">In the menu on the left, click **Users and groups**.</span></span>

    ![Назначение пользователя][202] 

4. <span data-ttu-id="f9543-225">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="f9543-225">Click **Add** button.</span></span> <span data-ttu-id="f9543-226">Затем в диалоговом окне **Добавление назначения** выберите **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="f9543-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Назначение пользователя][203]

5. <span data-ttu-id="f9543-228">В диалоговом окне **Пользователи и группы** в списке пользователей выберите **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="f9543-228">On **Users and groups** dialog, select **Britta Simon** in the Users list.</span></span>

6. <span data-ttu-id="f9543-229">В диалоговом окне **Пользователи и группы** нажмите кнопку **Выбрать**.</span><span class="sxs-lookup"><span data-stu-id="f9543-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f9543-230">В диалоговом окне **Добавление назначения** нажмите кнопку **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="f9543-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f9543-231">Проверка единого входа</span><span class="sxs-lookup"><span data-stu-id="f9543-231">Testing single sign-on</span></span>

<span data-ttu-id="f9543-232">В этом разделе описано, как проверить конфигурацию единого входа Azure AD с помощью панели доступа.</span><span class="sxs-lookup"><span data-stu-id="f9543-232">In this section, you test your Azure AD single sign-on configuration using the Access Panel.</span></span>

<span data-ttu-id="f9543-233">Щелкнув элемент "123ContactForm" на панели доступа, вы автоматически войдете в приложение 123ContactForm.</span><span class="sxs-lookup"><span data-stu-id="f9543-233">When you click the 123ContactForm tile in the Access Panel, you should get automatically signed-on to your 123ContactForm application.</span></span>
<span data-ttu-id="f9543-234">Дополнительные сведения о панели доступа см. в статье [Общие сведения о панели доступа](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f9543-234">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="f9543-235">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="f9543-235">Additional resources</span></span>

* [<span data-ttu-id="f9543-236">Список учебников по интеграции приложений SaaS с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f9543-236">List of Tutorials on How to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f9543-237">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f9543-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-123contactform-tutorial/tutorial_general_203.png

